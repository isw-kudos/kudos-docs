### Getting Started with Kudos Boards for Office 365

To get the most out of Kudos Boards in your Office 365 tenant, there are a few steps to take to make the experience seamless for your users.

> The Steps on this page (other than just logging in) require that you are an admin in your Office 365 tenant. if you are not an admin, please refer this page to your Administrator, Manager or IT department.

---

### Login

Kudos Boards uses OAuth for login and user access, This means your users can just click the Office 365 logo at [kudosboards.com](https://kudosboards.com) and use their existing Microsoft credentials.

> If you would like to link to Kudos Boards from another site, you can use [https://kudosboards.com/auth/msgraph ](https://kudosboards.com/auth/msgraph) which will skip the list of login options.

![Login Page](/assets/msgraph/sign_in.png)

---

### Admin Approval

Microsofts API requires that you grant admin access to Kudos Boards before your users are able to search for groups, to enable this log into [Kudos Boards](https://kudosboards.com) and you should be prompted to grant admin approval.

![Approval Toast](/assets/msgraph/approval.png)

After clicking Approve, you may be asked to login to Office 365 again, then you will be prompted to approve Kudos Boards access on behalf of your organisation.

> Note: you can revoke this approval at any stage via the Office 365 admin app.

![Approval Prompt](/assets/msgraph/approval2.png)

The requested permissions are:

| Permission                                          | Use in Kudos Boards                                                                                                                 |
| --------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Maintain access to data you have given it access to | Allows us to remember who you are logged in as, so you don't have to login every time you use Kudos Boards                          |
| Sign in and read user profile                       | Allows login to Kudos Boards                                                                                                        |
| Read all users' basic profiles                      | Allows us to get names and profile pictures of others in your tenant                                                                |
| Read directory data                                 | As Above                                                                                                                            |
| Read users' relevant people lists                   | As Above                                                                                                                            |
| Read and write all groups                           | Allows us to search for groups you are a member of. Write access is only used to add Kudos Boards bot to a Group in Microsoft Teams |
| Have full access to all files user can access       | Allows us to link to your OneDrive files                                                                                            |
| Read items in all site collections                  | Allows us to link to OneDrive files owned by your Groups or Teams                                                                   |

> You can also go to [Your Admin Page](https://kudosboards.com/admin/clients/manage) to approve the above.

![Manage Client](/assets/msgraph/manage-org.png)

---

### Start a free trial

After logging in, you will also be prompted to start a free (30 day) trial. Enabling this will allow other users in your Office 365 tenant to login and use Kudos Boards.

> You may also go to [Your Admin Page](https://kudosboards.com/admin/licences/manage) to Start Your free trial, get a Quote or Purchase licences online.

![Manage Licences](/assets/msgraph/licences.png)

---

### Enable Integrations between Kudos Boards and Office 365

These guides also require admin access and enable some advanced features of Kudos Boards in your Office 365 environment.

> These are also in the side menu of this page

- [Office Menu App Tile](/boards/msgraph/custom-tiles/)
- [Teams integration](/boards/msgraph/teams/)
- [Outlook plugin](/boards/msgraph/outlook/)
- [Sharepoint](/boards/msgraph/sharepoint/)
