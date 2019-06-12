# Kudos Boards for Kubernetes and IBM Cloud Private

Deploying Kudos Boards into Kubernetes -or- IBM Cloud Private for on-premise environments

---

### Pre-Requisites

1. Kubernetes or IBM Cloud Private is installed and running
1. WebSphere environment with Web Server (or another reverse proxy)
1. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) is installed
1. [helm](https://docs.helm.sh/using_helm/#installing-helm) is installed
1. SMTP gateway setup for email notifications if required
1. Ansible is installed, see [Ansible](/tools/ansible/)
1. [Kudos Boards ansible roles](/assets/config/boards-docker-ansible.zip) downloaded and extracted
1. [Dockerhub](https://hub.docker.com) account setup with access to Kudos Boards repository, send your account details to support@kudosboards.com if you don't already have this.

---

### SSL / Network setup

Kubernetes for on-premise environments requires a reverse proxy to route traffic. There are a number of different ways this reverse proxy can be configured and Kudos Boards aims to match whatever you already have in place. Some examples of network routing:

|                         | New domain                                                                                                                                                                                            | Path on existing domain                                                            |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Example of `BOARDS_URL` | `https://boards.example.com`                                                                                                                                                                                | `https://example.com/boards`                                                       |
| Example of `API_URL`    | `https://api.example.com`                                                                                                                                                                                   | `https://example.com/api-boards`                                                   |
| Requirement             | 1. Reverse proxy able to match any current domains as well as the new one for Kudos Boards (either by using SNI or a compatible certificate for all domains).</br>2. Certificate coverage for the 2 domains | Ability to proxy the 2 paths                                                       |
| Certificate Resolution  | a) in your proxy and forward the unencrypted traffic to kubernetes</br>**-OR-**</br>b) forward the encrypted traffic and perform the certificate resolution in kubernetes (described in config below).      | All certificate resolution on the proxy server                                     |
| Notes                   | IBM HTTP WebServer supports only one certificate. You must have a Wildcard certificate to cover all of your domains including the new Boards domains (ie \*.example.com).                                   | Additional config required to make Boards webfront handle redirects, details below |

Please decide on which configuration will suit your environment best and the corresponding `BOARDS_URL` & `API_URL`. These values will then be used in the following documentation.

For more details on configuring an IBM HTTP WebServer as reverse proxy, [please see here](/boards/connections/httpd/)

---

### Setup OAuth

Kudos Boards currently supports the following oauth providers for authentication and integration: IBM Connections (on premise), IBM Connections Cloud and Microsoft Office 365.

You will need to setup an OAuth application with one (or more) of these providers for Kudos Boards to function. please refer to the following documentation:

| Provider                     | Registration / Documentation                                                                                  | Callback URL                           | Scopes |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------- | -------------------------------------- | ------ |
| IBM Connections (on premise) | [Kudos instructions](/boards/connections/auth-on-prem/)                                                       | [BOARDS_URL]/auth/connections/callback |
| Microsoft Office 365         | [Azure app registrations](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade) | [BOARDS_URL]/auth/msgraph/callback     |
| Google                       | [Google Console](https://console.developers.google.com/apis/credentials)                                      | [BOARDS_URL]/auth/google/callback      |
| LinkedIn                     | [LinkedIn](https://www.linkedin.com/developers/apps)                                                          | [BOARDS_URL]/auth/linkedin/callback    |
| Facebook                     | [Facebook developer centre](https://developers.facebook.com/apps/2087069981334024/fb-login/settings/)         | [BOARDS_URL]/auth/facebook/callback    |

---

### Configure kubectl

**Kubernetes**

- copy \$HOME/kube/.config from the primary server to the same location locally (backup any existing local config)

**IBM Cloud Private**

- Open ICP Console
- Go to `Admin` (top right)
- Click `Config Client`
- Copy the contents shown
- Open your command line / terminal
- Paste the commands copied earlier and press enter

---

### Setup Kudos Boards namespace

    kubectl create namespace boards

---

### Setup Storage

Kudos Boards uses mongodb database and S3 file storage, If you have these services already then you can use your existing details in the config below, otherwise you may include one or both of these as follows:

a) Deploy both storage services

    ansible-playbook -i hosts/kubernetes.yml boards-docker.yml -v --tags "storage"

b) Deploy mongodb only

    ansible-playbook -i hosts/kubernetes.yml boards-docker.yml -v --tags "mongo"

c) Deploy S3 (using minio) only

    ansible-playbook -i hosts/kubernetes.yml boards-docker.yml -v --tags "minio"

---

### Setup secrets

1.  Dockerhub credentials

        kubectl create secret docker-registry dockerhub --docker-server=docker.io --docker-username=<username> --docker-password=<password> --docker-email=<email> --namespace=boards

1.  SSL certificate details

    > Only perform this step if you need to resolve certificates in kubernetes

        kubectl create secret tls kudosboards-domain-secret --key </path/to/keyfile> --cert </path/to/certificate> --namespace=boards

---

### Update Config file

Open the file at boards_docker_ansible/roles/docker-boards/files/boards.yaml and update the values as below.

**Kubernetes Variables**:

| Key                       | Description                                                                           |
| ------------------------- | ------------------------------------------------------------------------------------- |
| global.env.APP_URI        | Your BOARDS_URL                                                                       |
| global.env.MONGO_USER     | Your mongodb user, if using our storage above you may leave this commented out        |
| global.env.MONGO_PASSWORD | Your mongodb password, if using our storage above you may leave this commented out    |
| global.env.MONGO_HOST     | Your mongodb host, if using our storage above you may leave the default               |
| global.env.MONGO_PARAMS   | Your mongodb request parameters, if using our storage above you may leave the default |
| global.env.S3_ENDPOINT    | Enter your S3 URL, if using our storage above you may leave the default               |
| global.env.S3_ACCESS_KEY  | Enter your S3 Access Key, if using our storage above you may leave the default        |
| global.env.S3_SECRET_KEY  | Enter your S3 Secret Key, if using our storage above you may leave the default        |
| boards.ingress.hosts      | Your API_URL without the protocol e.g. api.kudosboards.com                            |
| webfront.ingress.hosts    | Your BOARDS_URL url as above without http                                             |

**Boards Variables**:

Follow instructions on [this page](/boards/env/common/)

---

### Deploy Boards

1.  deploy redis cache

        ansible-playbook -i hosts/kubernetes.yml boards-docker.yml -v --tags "redis"

2.  deploy all boards services

        ansible-playbook -i hosts/kubernetes.yml boards-docker.yml -v --tags "boards"

---

### Add Proxy Config

## Connections On Premise - update WAS config

> in the linked document you should use the IP of your kubernetes manager and the http port for your ingress (32080 if you have component pack installed)

Please follow [these instructions](/boards/connections/httpd/)

## Connections Cloud or Microsoft Office 365

Add a reverse proxy entry in your network that resolves your certificates and forwards your 2 domains to the IP of the kubernetes manager and the http port for your ingress. If any assistance is required

---

### IBM Connections integrations

- [Header](/boards/connections/header-on-prem/)
- [Apps Menu](/boards/connections/apps-menu-on-prem/)
- [Widgets](/boards/connections/widgets-on-prem/)

---
