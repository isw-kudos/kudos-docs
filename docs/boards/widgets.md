# IBM Connections Widget Setup
Basic instructions for adding Kudos Boards Docker widgets into IBM Connections on-premise environments

---

### Community Widget

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

---

### Activity Stream widget

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
  | Title| Kudos Boards Activity Stream |
  | URL Address| `http://<BOARDS_URL>/stream/connections`|
  | Secure URL Address| `https://<BOARDS_URL>/stream/connections`|
  | ICON URL| `http://<BOARDS_URL>/favicon.ico`|
  | ICON SECURE URL| `https://<BOARDS_URL>/favicon.ico`|

Select:

  - Use IBM Connections specific tags
  - Opened by default

Select the following Prerequisites:

  - oauthprovider
  - webresources
  - oauth
  - opensocial

  Scroll down and Click Save

---

### Register Widget

Required for IBM Connections 6.0 CR1 onwards

    execfile("newsAdmin.py")

    NewsWidgetCatalogService.addWidget(title="Kudos Boards", url="http://<BOARDS_URL>/boards/community/connection" ,secureUrl="https://<BOARDS_URL>/boards/community/connections", categoryName=WidgetCategories.NONE, isHomepageSpecific=0, isDefaultOpened=0, multipleInstanceAllowed=0, isGadget=0, policyFlags=[GadgetPolicyFlags.TRUSTED], prereqs=['communities'], appContexts=["IWIDGETS"])

    NewsWidgetCatalogService.enableWidget("<ID_RETURNED>")

    NewsWidgetCatalogService.clearWidgetCaches()

### Add to Apps Menu
- If you have not customised the apps.jsp file for your connections environment, please make a copy of the file.

    - You can access the file from:

            <WAS_home>/profiles/<profile_name>/installedApps/<cell_name>/Homepage.ear/homepage.war/nav/templates/menu

    - Paste the copy into the common\nav\templates subdirectory in the customization directory:

            <installdir>\data\shared\customization\common\nav\templates\menu\apps.jsp

- To add the Kudos Boards App Link add the following lines towards the bottom of the apps.jsp file before the </table> element, replacing <BOARDS_URL> with your URL

        --%><tr><%--
          --%><th scope="row" class="lotusNowrap"><%--
            --%><img width="16" src="https:/<BOARDS_URL><strong><fmt:message key="connections.component.name.kudos.boards" /></strong></a><%--
          --%></th><%--
          --%><td class="lotusNowrap lotusLastCell"><%--
            --%><a href="https://<BOARDS_URL>/todos/assigned"><fmt:message key="label.menu.kudos.boards.todos" /></a><%--
          --%></td><%--
          --%><td class="lotusNowrap lotusLastCell"><%--
            --%><a href="https://<BOARDS_URL>/boards/templates/public"><fmt:message key="label.menu.kudos.boards.templates" /></a><%--
          --%></td><%--
        --%></tr><%--

- Save and close the file

- Add the Kudos Boards Strings for the Apps Menu
    - Download the [strings files](/assets/strings.zip) and extract the files to the Connections strings customisation directory:

            <CONNECTIONS_CUSTOMIZATION_PATH>/strings

    - Note: Please append the lines to the files if they already exist. Extra languages can also be added

- The changes will take effect when the cluster(s) are restarted
