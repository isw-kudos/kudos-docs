This integration enables you to manage users in Auth0 for login to Kudos Boards Cloud. This enables a standalone use of Kudos Boards if you do not have any of the other integrated services in your business.

You may also add any of our other integrations at a later stage should you wish.

### Setting up a new Auth0 tenant for use with Kudos Boards

- Sign up at [Auth0](https://auth0.com/) by providing your email and a suitable password.

![Sign Up](/assets/auth0/signup.png)

- Choose a tenant domain and region

![Tenant Selection](/assets/auth0/choose-tenant.png)

- Fill in your company details

![Company Details](/assets/auth0/account.png)

- Create a new application, providing `Kudos Boards` for the name and choose `Regular Web Application` as the type.

![Application Wizard 1](/assets/auth0/application1.png)

- Open your application and go to the settings tab.

![Application Wizard 2](/assets/auth0/application2.png)

- Provide the rest of the details as below:

  > In the table below, copy your auth0 domain (listed at the top of the page) into the relevant fields, replacing &lt;domain&gt; where applicable

  | Field                                | Value                                                |
  | ------------------------------------ | ---------------------------------------------------- |
  | Application Logo                     | https://kudosboards.com/img/logo-large.png           |
  | Token Endpoint Authentication Method | Post                                                 |
  | Allowed Callback URLs                | https://kudosboards.com/auth/auth0/&lt;domain&gt;/callback |
  | Allowed Web Origins                  | https://kudosboards.com                              |
  | Allowed Origins                      | https://*.kudosboards.com                            |

- Click Show Advanced Settings -> Grant Types and tick `Implicit`, `Authorization Code`, `Refresh Token` and `Client Credentials`
- Click Save Changes
- Send An email to [support@kudosboards.com](mailto:support@kudosboards.com?subject=Kudos Boards Auth0 activation) with your domain, Client ID and Client Secret.

### Adding Users to your Auth0 tenant

- Login or Sign up to [Auth0](https://auth0.com/)
- Click Users and Roles -> Users
- Click `Create New User` and provide the email and password for the user you wish to add. Leave the Connection as Username-Password-Authentication

![Create User](/assets/auth0/create-user.png)

> If you aren't redirected to the users page, click them to open it

- Click `Edit` under the users name

![Edit User](/assets/auth0/edit-name.png)

- Update the users full name and click `Save`

![Save User](/assets/auth0/save-name.png)

### Sign in to Kudos Boards with your Auth0 Tenant

Once your Auth0 tenant has been activated you will get an email from our support team with confirmation, you may then go to [Kudos Boards](https://kudosboards.com) and use your Auth0 domain as the team name to login.

![Kudos Boards Login](/assets/auth0/boards-login.png)
