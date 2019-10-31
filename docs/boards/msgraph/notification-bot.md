## Microsoft Teams Notification Bot

This bot will be used for notification in Teams from actions taken in Kudos Boards.

![Bot notifications](/assets/msgraph/teams/bot_conversations.png)

---

### Pre-Requisites

- **Boards deployment is accessible from the Web (no VPN)**

  > Note: Microsoft Teams notifications requires 2-way web communication.

  > For example, the following URL must be accessible by Microsoft's servers: `https://[BOARDS_URL]/webhook/teams`

  > i.e. `https://[CONNECTIONS_URL]/boards/webhook/teams`

---

### Register Bot

1.  Open [Bot Registration](https://dev.botframework.com/bots/new) and sign-in with a Microsoft Tenant admin

1.  Enter the following values

        Kudos Boards
        kudosboards
        https://[BOARDS_URL]/webhook/teams
        [MSGRAPH_CLIENT_ID]

    Where:

    - `[BOARDS_URL]` is the URL to your Kudos Boards installation
    - `[MSGRAPH_CLIENT_ID]` is the OAuth Client ID from [Auth setup](/boards/msgraph/auth/)

    For example:

        Kudos Boards
        kudosboards
        https://connections.example.com/boards/webhook/teams
        b0e1e4a3-3df0-4c0a-8a2a-c1d630bb52b8

    ![enter these values](/assets/msgraph/teams/bot1.png)

---

1. Scroll down, read/agree to the terms and click `Register`

   ![register](/assets/msgraph/teams/bot2.png)

---

1. Click the `Teams` icon


    ![click teams](/assets/msgraph/teams/bot3.png)

---

1. Click `Save`


    ![save](/assets/msgraph/teams/bot4.png)

---

1. The bot setup is complete


    ![save](/assets/msgraph/teams/bot5.png)

---
