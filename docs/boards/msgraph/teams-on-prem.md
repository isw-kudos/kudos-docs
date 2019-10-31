## Kudos Boards On-Premise with Microsoft Teams

### Pre-requisites

1. Microsoft Teams

1. Office 365 tenant admin account

1. OAuth client is configured as [per doc](/boards/msgraph/auth/)

1. Notification Bot configured as [per doc](/boards/msgraph/notification-bot/)

    > **Optional** - not available to internal Kudos Boards deployments

---

### Install Application

1. Download Kudos Boards Application File

     - Login to Kudos Boards with your Microsoft Tenant Admin account

     - Click the `Configuration` icon and then `Manage Org`

     ![example](/assets/boards/admin.png)

     - Click on your Organisation

     ![example](/assets/msgraph/teams/admin-orgs.png)

     - Click on your Microsoft client

     ![example](/assets/msgraph/teams/admin-org.png)

     - Click `Download Teams app package`

     ![example](/assets/msgraph/teams/app-download.png)

1. Open the [Teams App](https://teams.microsoft.com)

    Click `Apps` -> `Upload a custom app` -> `Upload for [COMPANY_NAME]`
    > where `[COMPANY_NAME]` is the name of your company

    ![example](/assets/msgraph/teams/teams1.png)

1. Upload the Zip file you downloaded above

    ![example](/assets/msgraph/teams/teams2.png)

1. The Kudos Boards app will now appear under the section `[COMPANY_NAME]`

    ![example](/assets/msgraph/teams/teams3.png)


---

### Verification

1. Click on `Kudos Boards`

1. Click `Add`

    ![example](/assets/msgraph/teams/add-app.png)

1. Kudos Boards personal will now open

    ![example](/assets/msgraph/teams/personal.png)

---

### How To

For a full how-to guide on using Kudos Boards in Microsoft Teams, please see [our documentation](/boards/msgraph/teams/).
