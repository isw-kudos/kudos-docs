# Buzzy for Connections On-Prem Help Guide
Basic instructions for deploying buzzy into IBM Spectrum for on-premise IBM Connections environments

### Pre-Requisites
1. IBM Cloud Private is installed and running
1. WebSphere environment with Web Server
1. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) is installed
1. mongodb setup and running
1. SMTP gateway setup for email notifications
1. [Config file](/assets/config/buzzy.yml) downloaded
1. Dockerhub account setup with access to Buzzy repository



### Login to kubectl
1. Open ICP Console
2. Go to `Admin` (top right)
3. Click `Config Client`
4. Copy the contents shown
5. Open your command line (cmd)
6. Paste the commands copied earlier and press enter


### Setup Buzzy namespace
    kubectl create namespace buzzy

### Setup secrets
1.  Dockerhub credentials

            kubectl create secret docker-registry dockerhub --docker-server=docker.io --docker-username=<username> --docker-password=<password> --docker-email=<email> --namespace=buzzy

### Deploy Buzzy

1. edit buzzy.yml and enter details at the following lines:	 

| Key | Line | Description |
| --- | ---- | ----------- |
| spec.containers.env.value | 50 | URL you are deploying Buzzy to  |
| spec.containers.env.value | 54 | Enter your mongoDB credentials   |
| spec.containers.env.value | 56 | Enter your mongoDB debug credentials   |
| spec.containers.env.value | 58 | Enter your SMTP details |
| spec.containers.env.AWS_BUZZY_FILES | 68-74 | Your individual AWS details for file storage  |
| spec.containers.env.BUZZY_ADMIN_IDS | 126 | Enter Admin user ids |
| spec.containers.env.public.AWS_BUZZY_FILES | 228 | More AWS details for files |
| spec.containers.env.public.BUZZY_CUSTOM.NAME | 364 | Company Name |
| spec.containers.env.public.BUZZY_CUSTOM.LOGO_MAIN | 367 | URL of your main logo |
| spec.containers.env.public.BUZZY_CUSTOM.LOGO_MAIL | 368 | URL of us in Email |
| spec.containers.env.public.BUZZY_CUSTOM.EMAIL_FOOTER | 371 | Email Footer |
| spec.containers.env.public.BUZZY_CUSTOM.PROMO_URL | 374 | Splash image |
| spec.containers.env.public.BUZZY_CUSTOM.WELCOME_IMAGE | 375 | Welcome Image |

1. create your services   
`kubectl apply -f buzzy.yml`   
service has NodePort (ie 30289 which maps to 30buz on keypads)   
accessible on `<server-ip>:30289`
1. add new DNS record for Buzzy URL   
ie `buzzy.isw.net.au`

### Add Websphere Config
Please follow [these instructions](/buzzy/buzzy-wasconfig/)

### Add IBM Connections widgets
Please follow [these instructions](/buzzy/buzzy-widgets/)

### Setup SSO

* Login with email address - eg as Admin  
* Create a new team - eg Org Name (Hamburger -> Billing & Teams -> New Team) - choose a really short team name as users will need to type this in and it's case sensitive.  
* Go to Team -> Settings -> Add Provider -> IBM Connections On Premise  
* Fill out provider settings for the On Premise server  
* Restart the Buzzy server  
* Login with Connections On Prem button and type the team name in.  
