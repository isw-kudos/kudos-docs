# Kudos Boards for Docker Swarm

Basic instructions for deploying Kudos Boards into Docker Swarm for on-premise IBM Connections environments

---

### Pre-Requisites

1. Docker swarm with portainer is up and running [Guide here](/swarm/setup/)
1. SMTP gateway setup for email notifications
1. [Config File](/assets/config/boards-swarm.yml) downloaded
1. Dockerhub account setup with access to Kudos Boards repository, send your account details to support@kudosboards.com if you don't already have this.
1. SSL certificate - You will need to use a certificate that covers at least the 2 domains you plan to use, for example Kudos Boards cloud uses the domains `https://kudosboards.com` and `https://api.kudosboards.com`. The certificate should be pem encoded with a separate key file.

---

### Setup OAuth

Kudos Boards currently supports the following oauth providers for authentication and integration: IBM Connections (on premise), IBM Connections Cloud and Microsoft Office 365.

You will need to setup an OAuth application with one (or more) of these providers for Kudos Boards to function. please refer to the following documentation:

| Provider                     | Registration / Documentation                                                                                                          | Callback URL                  | Scopes |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------- | ------ |
| IBM Connections (on premise) | [IBM Knowledge Centre](https://www.ibm.com/support/knowledgecenter/en/SSYGQH_6.0.0/admin/admin/r_admin_common_oauth_manage_list.html) | [BOARDS_URL]/auth/connections/callback |
| Microsoft Office 365         | [Azure app registrations](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)                         | [BOARDS_URL]/auth/msgraph/callback     |
| Google                       | [Google Console](https://console.developers.google.com/apis/credentials)                                                              | [BOARDS_URL]/auth/google/callback      |
| LinkedIn                     | [LinkedIn](https://www.linkedin.com/developers/apps)                                                                                  | [BOARDS_URL]/auth/linkedin/callback    |
| Facebook                     | [Facebook developer centre](https://developers.facebook.com/apps/2087069981334024/fb-login/settings/)                                 | [BOARDS_URL]/auth/facebook/callback    |

---

### Update Config file

| Key                                        | Description                                                                                                      |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| x-minio-access                             | Your minio ACCESS KEY as defined in your docker swarm config                                                     |
| x-minio-secret                             | Your minio SECRET KEY as defined in your docker swarm config                                                     |
| x-app-env.APP_URI                          | Your main URL                                                                                                    |
| services.webfront.deploy.labels            | Update the `traefik.frontend.rule` your [BOARDS_URL]
| services.webfront.environment.API_GATEWAY  | Your api URL                                                                                                     |
| services.webfront.environment.DEFAULT_TEAM | provide a unique simple (alphanumeric) name for the default login team, see ENSURE_TEAMS below                   |
| services.core.deploy.labels                | Update the `traefik.frontend.rule` with your [API_URL]
| services.user.environment.ENSURE_TEAMS     | See the table below                                                                                              |
| CONNECTIONS_NAME                           | If you have customised the name of connections on premise in your environment you may adjust it here accordingly |
| CONNECTIONS_CLIENT_ID                      | Your oAuth client secret as defined in connections                                                               |
| CONNECTIONS_CLIENT_SECRET                  | Your oAuth client id                                                                                             |
| CONNECTIONS_URL                            | Your connections URL                                                                                             |
| SMARTCLOUD_CLIENT_ID                       | Your oAuth client id                                                                                             |
| SMARTCLOUD_CLIENT_SECRET                   | Your oAuth client secret as defined in connections                                                               |

Values for ENSURE_TEAMS

| Key           | Description                                                                                                                                                       |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| name          | If defining multiple teams you may use this long description to help determine which is which                                                                     |
| teamName      | A Unique name to identify your team, this should be kept short and not contain any spaces, punctuation or special characters                                      |
| provider      | Your oauth provider, available options are <br>'connections' - Connections on premise<br>'smartcloud' - Connections cloud<br>'msgraph' - Office 365 or Azure AD   |
| externalId    | based on the provider you chose above:<br>'connections' base64 string of your connections domain<br>'smartcloud' your organisation id<br>'msgraph' your tenant id |
| oAuth.baseURL | your connections url, only needed if you chose 'connections' as your provider.                                                                                    |
| globalOAuth   | as you may only have one team defined for each provider, please always set this to true                                                                           |

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
