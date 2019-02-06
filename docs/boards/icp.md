# Kudos Boards for IBM Cloud Private
Basic instructions for deploying Kudos Boards into IBM Cloud Private for on-premise IBM Connections environments

---

### Pre-Requisites
1. IBM Cloud Private is installed and running
1. WebSphere environment with Web Server
1. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) is installed
1. [helm](https://docs.helm.sh/using_helm/#installing-helm) is installed
1. mongodb setup and running
1. S3 storage setup and running. For local S3 we recommend [minio](https://www.minio.io/)
1. SMTP gateway setup for email notifications
1. [Kudos Boards helm chart](/assets/kudos-boards.tgz) downloaded
1. [Config file](/assets/config/boards-icp.yml) downloaded
1. Dockerhub account setup with access to Kudos Boards repository, send your account details to support@kudosboards.com if you don't already have this.
1. SSL certificate - You will need to use a certificate that covers at least the 2 domains you plan to use, for example Kudos Boards cloud uses the domains `https://kudosboards.com` and `https://api.kudosboards.com`. The certificate should be pem encoded with a separate key file.

---

### Login to kubectl
1. Open ICP Console
2. Go to `Admin` (top right)
3. Click `Config Client`
4. Copy the contents shown
5. Open your command line (cmd)
6. Paste the commands copied earlier and press enter

---

### Setup Kudos Boards namespace
    kubectl create namespace kudosboards

---

### Setup secrets
1. Dockerhub credentials

        kubectl create secret docker-registry dockerhub --docker-server=docker.io --docker-username=<username> --docker-password=<password> --docker-email=<email> --namespace=kudosboards

1. SSL certificate details

        kubectl create secret tls kudosboards-domain-secret --key </path/to/keyfile> --cert </path/to/certificate> --namespace=kudosboards

---

### Deploy Kudos Boards
1. Update Config file

    | Key | Description |
    | --- | ----------- |
    | global.env.APP_URI | Your `<BOARDS_URL>` |
    | global.env.API_GATEWAY | You need to provide an alternate url here for the app to communicate with the api, for example our cloud app uses `https://api.kudosboards.com` |
    | global.env.S3_ENDPOINT | Enter your S3 URL |
    | global.env.S3_ACCESS_KEY | Enter your S3 Access Key |
    | global.env.S3_SECRET_KEY | Enter your S3 Secret Key |
    | boards.ingress.hosts | Your API_GATEWAY url as above without https |
    | boards.ingress.tls.hosts | Your API_GATEWAY url as above without https |
    | boards.webfront.ingress.hosts | Your APP_URI url as above without https |
    | boards.webfront.ingress.tls.hosts | Your APP_URI url as above without https |
    | boards.core.env.NOTIFIER_EMAIL_HOST | Your SMTP gateway URL |
    | boards.core.env.NOTIFIER_EMAIL_USERNAME | Your SMTP gateway username |
    | boards.core.env.NOTIFIER_EMAIL_PASSWORD | Your SMTP gateway password |
    | boards.app.env.MONGO_URI | Your mongo connection string, which should include all servers from your replica set, username and password, default database and any required options. This database will store all information about boards, lists and cards |
    | boards.licence.env.MONGO_URI | Your mongo connection string, which should include all servers from your replica set, username and password, default database and any required options. This database will store all licencing information |
    | boards.notification.env.MONGO_URI | Your mongo connection string, which should include all servers from your replica set, username and password, default database and any required options. This database will store all information about notifications |
    | boards.user.env.MONGO_URI | Your mongo connection string, which should include all servers from your replica set, username and password, default database and any required options. This database will store all information about users |

2. Use helm to install boards with your values

        helm init
        helm upgrade kudos-boards kudos-boards.tgz -f boards-icp.yml --namespace kudosboards -i

3. add new DNS record for Kudos Boards URL ie `boards.example.com`

---

### Add Websphere Config
Please follow [these instructions](/boards/wasconfig/)

---

### Add IBM Connections widgets
Please follow [these instructions](/boards/widgets/)

---
