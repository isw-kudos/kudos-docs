### Authenticating Kudos Boards Docker with Office 365

You must configure an OAuth Application in your Office 365 Tenant in order to use Kudos Boards with O365. To access this configuration you must be logged in as a tenant admin

---

## Register OAuth Application

### Open the [Azure App Portal](https://portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

  ![example](/assets/msgraph/appreg.png)

### Configure Callback URL

![example](/assets/msgraph/appreg2.png)

Fill out the details:

    Kudos Boards
    https://[BOARDS_URL]/auth/msgraph/callback

  Where BOARDS_URL is the URL to access your main Kudos Boards page. For example:

  - `https://connections.example.com/boards/auth/msgraph/callback` OR
  - `https://boards.example.com/auth/msgraph/callback`

  Click `Register`


### Configure Required Scopes

1. Open `Manifest` section

1. Replace the `requiredResourceAccess` section with below then press `Save`

    ![example](/assets/msgraph/appreg-scopes.png)

        "requiredResourceAccess": [
          {
            "resourceAppId": "00000003-0000-0000-c000-000000000000",
            "resourceAccess": [
              {
                "id": "06da0dbc-49e2-44d2-8312-53f166ab848a",
                "type": "Scope"
              },
              {
                "id": "64a6cdd6-aab1-4aaf-94b8-3cc8405e90d0",
                "type": "Scope"
              },
              {
                "id": "863451e7-0667-486c-a5d6-d135439485f0",
                "type": "Scope"
              },
              {
                "id": "4e46008b-f24c-477d-8fff-7bb4ec7aafe0",
                "type": "Scope"
              },
              {
                "id": "7427e0e9-2fba-42fe-b0c0-848c9e6a8182",
                "type": "Scope"
              },
              {
                "id": "37f7f235-527c-4136-accd-4a02d197296e",
                "type": "Scope"
              },
              {
                "id": "ba47897c-39ec-4d83-8086-ee8256fa737d",
                "type": "Scope"
              },
              {
                "id": "14dad69e-099b-42c9-810b-d002981feec1",
                "type": "Scope"
              },
              {
                "id": "205e70e5-aba6-4c52-a976-6d2d46c48043",
                "type": "Scope"
              },
              {
                "id": "e1fe6dd8-ba31-4d61-89e7-88639da4683d",
                "type": "Scope"
              },
              {
                "id": "b340eb25-3456-403f-be2f-af7a0d370277",
                "type": "Scope"
              }
            ]
          }
        ],

### Check/Grant permissions

Open `API permissions`. Notice that all the scopes are now pre-filled.

Click `Grant admin consent for kudosdev`

![example](/assets/msgraph/appreg-scopes2.png)

Click `Yes`

![example](/assets/msgraph/appreg-consent.png)

### Config MSGraph OAuth in Boards

1. Open `Overview` section

      Copy `Application (client) ID` & `Directory (tenant) ID`

      ![example](/assets/msgraph/appreg-client-id.png)

1. Open `Certificates & secrets` section

    Click `New client secret`

    ![example](/assets/msgraph/appreg-client-secret.png)

    Select `Never` expire and click `Add`

    ![example](/assets/msgraph/appreg-client-secret2.png)

    Copy the secret value shown

    ![example](/assets/msgraph/appreg-client-secret3.png)

1. Add OAuth and Tenant values to YAML config (ie `boards.yaml` or `boards-cp.yaml`)

        global:
          env:
            MSGRAPH_CLIENT_ID: "<your-application-id>"
            MSGRAPH_CLIENT_SECRET: "<your-application-secret>"
            MSGRAPH_LOGIN_TENANT: "<your-tenant-id>"

1. Redeploy Boards Helm Chart

    For Component Pack

        helm upgrade kudos-boards-cp https://docs.kudosapps.com/assets/config/kubernetes/kudos-boards-cp-1.0.0.tgz -i -f ./boards.yaml --namespace connections --recreate-pods

    For Kubernetes

        helm upgrade boards https://docs.kudosapps.com/assets/config/kubernetes/kudos-boards-2.0.2.tgz -i -f ./boards.yaml --namespace boards --recreate-pods

    Where `--recreate-pods` will ensure all images are updated to `latest`
