The Kudos Application is provided as a .war file that is to be installed as a WebSphere Application in your Connections server environment.
The application provides the Kudos Badges & Analytics engines that drives the reward and recognition of user performance, as well as the widgets for user
interaction.

### Login to the WebSphere Integrated Solution

Login to the WebSphere Integrated Solution Console for your Connections environment via a webbrowser.

Enter your administrator User ID and Password, then click the “Log in” button.

![login](/assets/badges/install/app/WAS_Console_login.png)

### Install the Kudos.war file

Navigate to Applications → Application Types → WebSphere enterprise applications

![install app](/assets/badges/install/app/install_app.png)

Click the Install button

![install button](/assets/badges/install/app/install_button.png)

Browse the Local File System Path for the downloaded Kudos.war file then Click Next

![browse war](/assets/badges/install/app/browse_war.png)

Check the Fast Path Option then Click Next

![fastpath](/assets/badges/install/app/fastpath.png)

Change the Application name to Kudos then Click Next

![app name](/assets/badges/install/app/app_name.png)

Highlight the Nodes for the Application, including the IHS Node. Select the Badges Module, click Apply then Next.

**_Please Note:_** _It’s recommended that you create a separate cluster for Kudos if your Connections install is bigger than 10,000 users. You can do this via the ISC by clicking on_ **_Servers > Clusters > WebSphere_** _application server clusters and then clicking New._

![server mapping](/assets/badges/install/app/server_mapping.png)

Click on Browse and map the default resources as shown. Click Next.
<!--- //cluster??? -->
![resource mapping](/assets/badges/install/app/resource_mapping.png)

Enter Kudos as the Context Root, then click Next.

**_Please Note:_** _The Kudos Installation guide assumes that the Context Root is set as ‘/Kudos’. If you set the Context Root to something other than ‘/Kudos’, then make sure that you replace ‘/Kudos’ with your Context Root when entering addresses._

![context root](/assets/badges/install/app/context_root.png)

Review the Installation Summary. Click Finish.

![summary](/assets/badges/install/app/summary.png)

Review the Installation Results. Click Save.

![save install](/assets/badges/install/app/save_install.png)

Review the Synchronisation Summary. Click OK.

You have now successfully installed Kudos as a WebSphere Enterprise Application. Next, you will need to edit the security settings.


### Modify the Kudos Application Security Role assignments

During this step, we will be defining the authenticated users/groups for each Security Role.

Find Kudos in the list of enterprise applications and click on Kudos to open the application configuration screen

![app list](/assets/badges/install/app/kudos_app_list.png)

Click Security role to user/group mapping

![security role](/assets/badges/install/app/security_role_link.png)

To ensure that only authorised users have access to Kudos and its data, modify the mapping of the AllServlets and Reader roles to the Special Subjects: **All Authenticated in Application/Trusted Realm**, then Click OK

**_Please note:_** _You may set the Reader role to Everyone to grant read-only access to Kudos widget data to unauthenticated users._

![role mapping](/assets/badges/install/app/role_mapping.png)

### Ensure the Signer Certificate for the Connections URL is Trusted

In order for Kudos to post entries into the Homepage Activity Stream, WebSphere must trust the certificate for the secure URL of your Connections
Environment. During this step, we will be importing the environment certificate into the CellDefaultTrustStore.

Navigate to **_Security_** → **_SSL certificate and key management_** and then select **_Key stores and certificates_**

![ssl cert](/assets/badges/install/app/SSL_cert_link.png)

Select **_CellDefaultTrustStore_**

![trust store](/assets/badges/install/app/celldefaulttruststore.png)

Select **_Signer certificates_**

![signer cert](/assets/badges/install/app/signer_cert_link.png)

You will now see a list of all trusted certificates.

**If the URL of your Connections Environment is listed, skip to [Add Kudos Related Strings to Connections](/badges/install/app/app/#add-kudos-related-strings-to-connections)**

We will now import the public certificate from the IBM HTTP Server to the default trust store in IBM WebSphere Application Server

Click Retrieve from port

![retrieve link](/assets/badges/install/app/retrieve_link.png)

Enter the following details of the web server, then click Retrieve Signer Information:

- **Host** (e.g. connections.company.com)
- **SSL Port** (443)
- **Alias**

![port details](/assets/badges/install/app/port_details.png)


The certificate will now be retrieved. Please confirm the details of the certificate, Click **OK**.
The root certificate is then added to the list of signer certificates.

### Add Kudos Related Strings to Connections

This change will not be picked up by Connections until the servers are restarted. This will be performed at the end of the configuration.

Copy the .properties files from the folder Kudos.ear/Kudos.war/installFiles to the Connections strings customisation directory:
<CONNECTIONS_CUSTOMIZATION_PATH>/strings
Where **CONNECTIONS_CUSTOMIZATION_PATH** is defined by the WebSphere variable.
e.g. /opt/Connections/data/shared/customization/strings

**IMPORTANT: If a file of the same name already exists, merge the contents into the existing file.**

![customisation path](/assets/badges/install/app/conn_customisation_path.png)