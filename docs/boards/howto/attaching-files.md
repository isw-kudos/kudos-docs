<img style="float: right" src="/assets/images/boards-logo.jpg" height="100" alt="My Boards" />

Kudos Boards allows files under `20mb` to be attached to cards directly.

### Office 365 & IBM Connections

If you use Office 365 or IBM Connections as your authentication method, uploaded files and the security will be managed by your respective provider.  

### Auth0, Google, Facebook, LinkedIn

If you use Auth0, Google, Facebook or LinkedIn to authenticate your entry into Kudos Boards, uploaded files will be managed by Kudos Boards, not your respective provider. Anyone who has access to view the card will be able to view and download the attachment.

File upload to Kudos Boards with Auth0, Google, Facebook, and LinkedIn can be disabled by an administrator if desired.

### Attaching a File to a Card

Enter your desired card, click the + next to Links and Attachments
![](/assets/boards/attaching1.png)

In the menu that appears, choose Upload.

![](/assets/boards/attaching2.png)

Locate the file(s) you wish to attach and click Open, Boards will examine the selected files and prompt you where to upload them as below. choose `Upload to Kudos Boards` and click `Upload`.

![](/assets/boards/attaching3.png)

Your file will now appear in the Links and Attachments list.

![](/assets/boards/attaching4.png)

### Removing an Attached File

To remove an attached file, hover over the file in the card and click the `X` to remove the link. The file will be deleted and the link will no longer work. Please ensure you still have a copy of the file if needed before doing this.

### Who Can Remove Files?

Anyone who can edit the card can also remove the attached files.

### Where are Files Stored?

Files attached to cards in Kudos Boards Cloud with Auth0, Google, Facebook, LinkedIn authentication providers are stored in <a target="_blank" href="https://cloud.google.com/storage/">Google Cloud Storage</a>

If you are hosting Kudos Boards yourself then files are stored in the default file storage as defined in your environment.

If you are using Office 365 or IBM Connections, your files are stored within these environments.

### Deleting a Card that has Attachments

When you archive a card, the attachments will still be accessible however, if you delete the card permanently then the attachments will also be deleted.

