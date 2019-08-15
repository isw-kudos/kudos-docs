# Boards in Microsoft Office 365 for Business

## Microsoft Teams

### Administrator approval required to add Kudos Boards as a Teams Tab

You may find that as a non-administrator Office 365 user, you cannot add Kudos Boards as a Teams Tab. In this case, after signing in to Kudos Boards in the tab configuration dialog view, the view will look like the screenshot below and all actions will be disabled.

![Admin Approval Required](../../assets/msgraph/teams_admin_approval_required.png)

Note that Kudos Boards can still be used as a Microsoft Teams personal app whilst in this state

#### Resolution

A user that has administrative capabilities within your Microsoft Office 365 organisation will need to sign in to Kudos Boards (either inside the Microsoft Teams configuration view or by going directly to [kudosboards.com](https://kudosboards.com)). They will then be presented with the following prompt:

![Admin Approval Toast](../../assets/msgraph/administrator_approval_toast.png)

After clicking `Approve`, the administrator will be directed to an approval screen that will allow them to accept all of the required permissions that Kudos Boards requires, on behalf of the entire organisation:

![Admin Approval View](../../assets/msgraph/administrator_approval_view.png)

Once these permissions have been accepted on behalf of the organisation, all users in the organisation will now be able to add Kudos Boards as a Microsoft Teams Tab.

##### Force Administrative Approval for Organisation

Administrative users for your Office 365 organisation can also force an approval of all permissions for the organisation from within the Org Administration screen by following these steps:

Click `Configuration` and then `Manage Org`:

![](/assets/boards/config-manage_org.png)

Under the Org Administration section, click the `Approve Advanced Features` button:

![](/assets/boards/org-admin-approve-advanced.png)

This will direct you to the Microsoft Office 365 **Permissions requested - Accept for your organisation** page, allowing you to force the consent of all permissions that Kudos Boards needs for your organisation:

![Admin Approval View](../../assets/msgraph/administrator_approval_view.png)
