# Kudos Boards for IBM Cloud Private
Basic instructions for deploying Kudos Boards into IBM Cloud Private for on-premise IBM Connections environments

### Pre-Requisites
1. IBM Spectrum CFC is installed and running
2. WebSphere environment with Web Server
3. [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) is installed
4. Install helm (TODO add url)

### Login to kubectl
1. Open Spectrum Console
2. Go to `Admin` (top right)
3. Click `Config Client`
4. Copy the contents shown
5. Open your command line (cmd)
6. Paste the commands copied earlier and press enter


### Deploy Kudos Boards
1. Update helm values file
2. helm imstall command (TODO)
3. add new DNS record for Kudos Boards URL ie `boards.isw.net.au`
4. Open WebSphere ISC -> open web server -> edit `http.conf` -> add another VirtualHost
  <pre>
    &lt;VirtualHost *:443&gt;
      ServerName boards.isw.net.au
      #Kudos Boards
      ProxyPreserveHost On
      ProxyPass / http://<server-ip>/
      ProxyPassReverse / http://<server-ip>/
      #End Kudos Boards
      SSLEnable
        # Disable SSLv2
        SSLProtocolDisable SSLv2
        # Set strong ciphers
        SSLCipherSpec TLS_RSA_WITH_AES_128_CBC_SHA
        SSLCipherSpec TLS_RSA_WITH_AES_256_CBC_SHA
        SSLCipherSpec SSL_RSA_WITH_3DES_EDE_CBC_SHA
    &lt;/VirtualHost&gt;
  </pre>
5. Setup Community Widget

	Check out the widgets-config.xml file.

		execfile("profilesAdmin.py")
		ProfilesConfigService.checkOutWidgetConfig("/LCCheckedOut", AdminControl.getCell())

	Edit the widgets-config.xml file. Under the <resource type="community"> section, then under <widgets>, then within <definitions> add the following.

		<!-- Kudos Boards -->
		<widgetDef defId="KudosBoards" modes="view fullpage" url="https://<BOARDS_URL>/boards/community/connections" themes="wpthemeNarrow wpthemeWide wpthemeBanner" uniqueInstance="true">
			<itemSet>
				<item name="resourceId" value="{resourceId}"/>
			</itemSet>
		</widgetDef>
		<!-- END Kudos Boards -->

	Check in the widgets-config.xml file.

		ProfilesConfigService.checkInWidgetConfig()

8. Setup Activity Stream widget

	Access Homepage->Administrator

	Select the following:

    - Open Social Gadget
    - Trusted and Use SSO
    - Show for Activity Stream events
    - All servers

    Click the Add Mapping button.

	Add a Mapping for the Kudos Boards service to the Kudos client. Ensure OAuth Client is set to conn-ee and the Service name is Kudos Boards.
	Click the Ok button

	Enter The following:

    | Field | Value |
    | ----- | ----- |
    | Title| `Kudos Boards Activity Stream`|
    | Description| `Kudos Boards is awesome`|
    | URL Address| `http://<BOARDS_URL>/stream/connections`|
    | Secure URL Address| `https://<BOARDS_URL>/stream/connections`|
    | ICON URL| `http://<BOARDS_URL>/favicon.ico`|
    | ICON SECURE URL| `https://<BOARDS_URL>/favicon.ico`|

	Select:
* Use IBM Connections specific tags
* Opened by default

	Select the following Prerequisites:
* oauthprovider
* webresources
* oauth
* opensocial
	Scroll down and Click Save

9. Register Widgets (IBM Connections 6.0 CR1 onwards)

	```
	execfile("newsAdmin.py")

	NewsWidgetCatalogService.addWidget(title="Kudos Boards", url="http://<BOARDS_URL>/boards/community/connection" ,secureUrl="https://<BOARDS_URL>"/boards/community/connections, categoryName=WidgetCategories.NONE, isHomepageSpecific=0, isDefaultOpened=0, multipleInstanceAllowed=0, isGadget=0, policyFlags=[GadgetPolicyFlags.TRUSTED], prereqs=['communities'], appContexts=["IWIDGETS"])
	NewsWidgetCatalogService.enableWidget("<ID_RETURNED>")

	NewsWidgetCatalogService.clearWidgetCaches()
	```

10.	Register OAuth

	```
	execfile('oauthAdmin.py')
	OAuthApplicationRegistrationService.addApplication('kudosboards', 'KudosBoards', '<URL>')
	```

	<URL> should be your <BOARDS_URL>/auth/connections (TODO confirm)
	That will return with both a clientsecret and clientid that you need to input in the provider settings in Step 11.

### Notes on IBM Spectrum CFC Naming
- Application (aka Deployments)
- PetSet (aka Replica sets)
