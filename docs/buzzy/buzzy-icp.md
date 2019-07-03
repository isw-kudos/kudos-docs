# Buzzy for Connections On-Prem Help Guide
Basic instructions for deploying buzzy into Kubernetes -or- IBM Cloud Private for on-premise IBM Connections environments

### Pre-Requisites
1. Kubernetes -or- IBM Cloud Private is installed and running
1. WebSphere environment with Web Server
1. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) is installed
1. mongodb setup and running
1. minio setup and running
1. SMTP gateway setup for email notifications
1. [Config file](/assets/config/buzzy.yml) downloaded
1. [Logging Config file](/assets/config/buzzy-logging.yml) downloaded
1. Dockerhub account setup with access to Buzzy repository


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


### Setup Buzzy namespace
    kubectl create namespace buzzy

### Setup secrets
1.  Dockerhub credentials

        kubectl create secret docker-registry dockerhub --docker-server=docker.io --docker-username=<username> --docker-password=<password> --docker-email=<email> --namespace=buzzy

### Setup OAuth

Please follow [these instructions](/buzzy/buzzy-oauth/)

### Deploy Buzzy

NOTE: Is using self-signed certificates you will need to uncomment NODE_TLS_REJECT_UNAUTHORIZED at lines 55 & 56

1. Edit buzzy.yml and enter details at the following lines:	 

| Key | Line | Description |
| --- | ---- | ----------- |
| spec.containers.env.value | 58 | URL you are deploying Buzzy to, including https://  |
| spec.containers.env.value | 62 | Enter your mongoDB credentials   |
| spec.containers.env.value | 64 | Enter your mongoDB debug credentials   |
| spec.containers.env.value | 66 | Enter your SMTP details |
| spec.containers.env.AWS_BUZZY_FILES | 79-88 | Your individual AWS details for file storage  |
| spec.containers.env.MAIL_URL | 137 | Enter your SMTP details as above |
| spec.containers.env.BUZZY_ADMIN_EMAIL | 139 | OPTIONAL: Enter Admin user email, used as the primary owner of the default buzzes and resources that appear on the palette |
| spec.containers.env.DEFAULT_OAUTH_PROVIDERS | 140-153 | Details for the OAuth provider(s) to be setup. ClientID and ClientSecret are from the OAuth setup in the previous step |
| spec.containers.env.BUZZY_ADMIN_IDS | 154 | Enter Admin user ids |
| spec.containers.env.BUZZY_LOGGING_TOKEN | 156 | Token used for access to the Buzzy logging server |
| spec.containers.env.BUZZY_CREATE_DEFAULT_ACCOUNTS  | 171 | Default accounts created. Set isAdmin for these accounts to be considered the same as BUZZY_ADMIN_EMAIL. Make the email the same as one from the OAuth provider to be able to view and edit the provider settings |
| spec.containers.env.public.AWS_BUZZY_FILES | 257 | More AWS details for files |
| spec.containers.env.public.IBMConnectionsOnPrem.signInDomains | 280 | IBM Connections URLs you are connecting to this Buzzy instance |
| spec.containers.env.public.BUZZY_CUSTOM.NAME | 389 | Company Name |
| spec.containers.env.public.BUZZY_CUSTOM.LOGO_MAIN | 401 | URL of your main logo |
| spec.containers.env.public.BUZZY_CUSTOM.LOGO_MAIL | 402 | URL of us in Email |
| spec.containers.env.public.BUZZY_CUSTOM.EMAIL_FOOTER | 405 | Email Footer |
| spec.containers.env.public.BUZZY_CUSTOM.PROMO_URL | 408 | Splash image |
| spec.containers.env.public.BUZZY_CUSTOM.WELCOME_IMAGE | 409 | Welcome Image |
| spec.containers.env.public.BUZZY_CUSTOM.BUZZY_LOGGING_SERVER | 445 | URL of the Buzzy logging server |

1. Create your services   
`kubectl apply -f buzzy.yml`   
service has NodePort (ie 30289 which maps to 30buz on keypads)   
accessible on `<server-ip>:30289`
1. Add new DNS record for Buzzy URL   
ie `buzzy.net.au`

1. Login to Buzzy with the account set up in BUZZY_CREATE_DEFAULT_ACCOUNTS above and confirm the org and provider details are correct

1. Restart the Buzzy Application

### Deploy Buzzy Logging

NOTE: This is optional and will not work if you are using IHS

1. Edit buzzy-logging.yml and enter details at the following lines:	 

| Key | Line | Description |
| --- | ---- | ----------- |
| spec.containers.env.value | 51 | URL you are deploying Buzzy logging to, including https://  |
| spec.containers.env.value | 55 | Enter your mongoDB credentials   |
| spec.containers.env.value | 57 | Enter your mongoDB debug credentials   |
| spec.containers.env.value | 59 | Enter your SMTP details |
| spec.containers.env.public.BUZZY_LOGGING_SERVER | 64 | URL you are deploying Buzzy logging to, including https:// |
| spec.containers.env.public.BUZZY_APP_SERVER | 65 | Buzzy URL |
| spec.rules.host | 105 | URL you are deploying Buzzy logging to, excluding https://  |

1. Create your services   
`kubectl apply -f buzzy-logging.yml`   
1. Add new DNS record for Buzzy URL   
ie `logging.buzzy.net.au`

### Add Websphere Config
Please follow [these instructions](/buzzy/buzzy-wasconfig/)

### Add IBM Connections widgets
Please follow [these instructions](/buzzy/buzzy-widgets/)
