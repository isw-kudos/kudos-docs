# Kudos Boards for Docker Swarm
Basic instructions for deploying Kudos Boards into Docker Swarm for on-premise IBM Connections environments

---

### Pre-Requisites
1. Docker swarm with portainer is up and running [guide](/swarm/)
1. SMTP gateway setup for email notifications
1. [Config File](/assets/config/boards-swarm.yml) downloaded
1. Dockerhub account setup with access to Kudos Boards repository, send your account details to support@kudosboards.com if you don't already have this.
1. SSL certificate - You will need to use a certificate that covers at least the 2 domains you plan to use, for example Kudos Boards cloud uses the domains `https://kudosboards.com` and `https://api.kudosboards.com`. The certificate should be pem encoded with a separate key file.

---

### Update Config file

  | Key | Description |
  | --- | ----------- |
  | x-minio-access | Your minio ACCESS KEY as defined in your docker swarm config |
  | x-minio-secret | Your minio SECRET KEY as defined in your docker swarm config |
  | x-app-env.APP_URI | Your main URL |
  | services.webfront.deploy.labels | Update the <MAIN_URL> with your main URL |
  | services.webfront.environment.API_GATEWAY | Your api URL |
  | services.core.deploy.labels | Update the <API_URL> with your api URL |
  | services.user.environment.ENSURE_TEAMS | update the example team as follows:<br>__name__ Your company name<br>__externalId__ your connections url base64 encoded<br>__clientSecret__ Your oAuth client secret as defined in connections<br>__clientID__ Your oAuth client id<br>__baseURL__ Your connections URL |

---

### Deploy
1. Open portainer and login
1. Select your primary endpoint
1. Choose Stacks from the side menu
1. Click Add Stack
1. Name your stack kudos-boards
1. paste your config from from above into the web editor
1. Click "Deploy the stack"

---

### Update DNS
Update DNS records with a cname entry pointing to your swarm url.

For example:

    kudosboards.com -> swarm.isw.net.au
    api.kudosboards.com -> swarm.isw.net.au

---

### Add IBM Connections widgets
Please follow [these instructions](/boards/widgets/)

---

### Advanced
You can also run Kudos Boards with externally hosted mongo database and/or S3 storage.
For assistance with this contact support@kudosboards.com

---
