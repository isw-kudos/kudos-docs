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

1. edit buzzy.yml and enter details at the following lines:	 

| Key | Line | Description |
| --- | ---- | ----------- |
| spec.containers.env.value | 50 | URL you are deploying Buzzy to, including https://  |
| spec.containers.env.value | 54 | Enter your mongoDB credentials   |
| spec.containers.env.value | 56 | Enter your mongoDB debug credentials   |
| spec.containers.env.value | 58 | Enter your SMTP details |
| spec.containers.env.AWS_BUZZY_FILES | 71-77 | Your individual AWS details for file storage  |
| spec.containers.env.MAIL_URL | 126 | Enter your SMTP details as above |
| spec.containers.env.BUZZY_ADMIN_EMAIL | 128 | OPTIONAL: Enter Admin user email, used as the primary owner of the default buzzes and resources that appear on the palette |
| spec.containers.env.DEFAULT_OAUTH_PROVIDERS | 129-142 | Details for the OAuth provider(s) to be setup. ClientID and ClientSecret are from the OAuth setup in the previous step. |
| spec.containers.env.BUZZY_ADMIN_IDS | 143 | Enter Admin user ids |
| spec.containers.env.BUZZY_CREATE_DEFAULT_ACCOUNTS  | 160 | Default accounts created. Set isAdmin for these accounts to be considered the same as BUZZY_ADMIN_EMAIL. Make the email the same as one from the OAuth provider to be able to view and edit the provider settings |
| spec.containers.env.public.AWS_BUZZY_FILES | 246 | More AWS details for files |
| spec.containers.env.public.BUZZY_CUSTOM.NAME | 382 | Company Name |
| spec.containers.env.public.BUZZY_CUSTOM.LOGO_MAIN | 385 | URL of your main logo |
| spec.containers.env.public.BUZZY_CUSTOM.LOGO_MAIL | 386 | URL of us in Email |
| spec.containers.env.public.BUZZY_CUSTOM.EMAIL_FOOTER | 389 | Email Footer |
| spec.containers.env.public.BUZZY_CUSTOM.PROMO_URL | 391 | Splash image |
| spec.containers.env.public.BUZZY_CUSTOM.WELCOME_IMAGE | 393 | Welcome Image |

1. Create your services   
`kubectl apply -f buzzy.yml`   
service has NodePort (ie 30289 which maps to 30buz on keypads)   
accessible on `<server-ip>:30289`
1. Add new DNS record for Buzzy URL   
ie `buzzy.isw.net.au`

1. Login to Buzzy with the account set up in BUZZY_CREATE_DEFAULT_ACCOUNTS above and confirm the org and provider details are correct

1. Restart the Buzzy Application

### Add Websphere Config
Please follow [these instructions](/buzzy/buzzy-wasconfig/)

### Add IBM Connections widgets
Please follow [these instructions](/buzzy/buzzy-widgets/)

### Setup SSO

* Login with email address - eg as Admin  
* Create a new Organization, under Organizations
* Go to Organization -> Settings -> Add Provider -> IBM Connections On Premise. Use the OAuth ID & Secret setup previously.
* Create a new team - choose a really short team name as users will need to type this in and it's case sensitive.  
* Restart the Buzzy server  
* Login with Connections On Prem button and type the team name in.  
