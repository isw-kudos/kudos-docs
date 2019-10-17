## Installation in Verse for Connections Cloud

Download Kudos Boards [applications.json file](https://kudosboards.com/widgets/verse/applications.json) and import as below.

> The information below is an excerpt from
> [HCL Connections Developers](https://www-10.lotus.com/ldd/appdevwiki.nsf/xpDocViewer.xsp?lookupName=Dev+Guide+topics#action=openDocument&res_title=Managing_applications_for_Verse_or_the_Top_Navigation_Bar&content=sdkcontent)

To work with the Organization Extensions page, open a browser and sign in to your Connections Cloud organization as an administrator. Click Admin > Manage Organization, then click Organization Extensions in the navigation list.

Click the Add button.

__Import an application__: This is typically the simplest method for adding applications and extensions because you can model your code on existing examples and then import it into Connections Cloud without needing to fill in the entire dialog box. To import your application, click Choose File, browse for the JSON file containing the application, and select it. The code that you import is validated and error messages display in the editing pane, where you can make corrections.

  ![Manage Extensions](/assets/connections/verse-cloud-extension.png)

## Installation in Verse On Premise

You may either download Kudos Boards [applications.json file](https://kudosboards.com/widgets/verse/applications.json) and use it as a localFileProvider or just copy the url for it and use it as a httpDataProvider ny following the instructions below.

> The information below is an excerpt from
> [HCL Verse Developers](https://ibmverse.github.io/verse-developer/developers/#registering-an-application-in-ibm-verse)

#### Deploying extensions using the built-in endpoint
Verse On-Premises implemented a built-in endpoint to serve the application’s JSON data from a local file or an HTTP hosted file. If storing the applications JSON data as a static file works for you, this is the way to go.

Two data providers are implemented in the built-in endpoint:

- __Local file data provider__: Serves the applications JSON data from a local file on the Domino server. This allows you to deploy extensions without dependency on another server. The path of the file can be specified using a `notes.ini` parameter `VOP_Extensibility_Applications_Json_FilePath`.

- __HTTP data provider__: Serves the applications JSON data from an HTTP hosted file. This allows you to deploy `applications.json` to a centralized HTTP server. The HTTP URL of the file can be specified using `notes.ini` parameter `VOP_Extensibility_Applications_Json_URL`.

The `notes.ini` parameter `VOP_Extensibility_Data_Provider_Name` controls which data provider to use, either `localFileProvider` or `httpDataProvider`. By default, if none is specified, `localFileProvider` will be used. In either case, the data provider will periodically check the source `applications.json` file for updates, so you don’t have to restart the server after a new version of `applications.json` is deployed.

To use the local file data provider:

- Make sure `notes.ini` parameter `VOP_Extensibility_Data_Provider_Name` is either clear or set to `localFileProvider`.

- Deploy `applications.json` to the Domino server.

- Make sure notes.ini parameter `VOP_Extensibility_Applications_Json_FilePath` is set to the file path of `applications.json`. For example:

        VOP_Extensibility_Applications_Json_FilePath=D:\data\applications.json

To use the HTTP data provider:

- Make sure `notes.ini` parameter `VOP_Extensibility_Data_Provider_Name` is set to `httpDataProvider.`

        VOP_Extensibility_Data_Provider_Name=httpDataProvider

- Deploy `applications.json` to the HTTP server.

- Make sure `notes.ini` parameter `VOP_Extensibility_Applications_Json_URL` is set to the HTTP URL of `applications.json`. For example:

        VOP_Extensibility_Applications_Json_URL=https://files.renovations.com/vop/applications.json
