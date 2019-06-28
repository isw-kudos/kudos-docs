# IBM Connections Widget Setup
Basic instructions for adding Kudos Boards Docker widgets into IBM Connections on-premise environments

---

### Community Widget

Check out the widgets-config.xml file.

    execfile("profilesAdmin.py")
    ProfilesConfigService.checkOutWidgetConfig("/LCCheckedOut", AdminControl.getCell())

Edit the widgets-config.xml file. Under the <resource type="community"> section, then under <widgets>, then within <definitions> add the following.

    <!-- BUZZY -->
    <widgetDef defId="Buzzy" modes="view fullpage" url="https://<BUZZY_URL>/widget/widget.xml" themes="wpthemeNarrow wpthemeWide wpthemeBanner" uniqueInstance="true">
      <itemSet>
        <item name="resourceId" value="{resourceId}"/>
      </itemSet>
    </widgetDef>
    <!-- END BUZZY -->

Check in the widgets-config.xml file.

    ProfilesConfigService.checkInWidgetConfig()

### Register Widget

Required for IBM Connections 6.0 CR1 onwards

        execfile("newsAdmin.py")

        NewsWidgetCatalogService.addWidget(title="Buzzy", url="http://<BUZZY_URL>/widget/widget.xml" ,secureUrl="https://<BUZZY_URL>/widget/widget.xml", categoryName=WidgetCategories.NONE, isHomepageSpecific=0, isDefaultOpened=0, multipleInstanceAllowed=0, isGadget=0, policyFlags=[GadgetPolicyFlags.TRUSTED], prereqs=['communities'], appContexts=["IWIDGETS"])

        NewsWidgetCatalogService.enableWidget("<ID_RETURNED>")

        NewsWidgetCatalogService.clearWidgetCaches()


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
  | Title| Buzzy Activity Stream |
  | URL Address| `http://<BUZZY_URL>/assets/connections/gadget.xml`|
  | Secure URL Address| `https://<BUZZY_URL>/assets/connections/gadget.xml`|
  | ICON URL| `http://<BUZZY_URL>/assets/ico/favicon-32x32.png`|
  | ICON SECURE URL| `https://<BUZZY_URL>/assets/ico/favicon-32x32.png`|

Select:

  - Use IBM Connections specific tags
  - Opened by default
  - Display on Updates pages

Select the following Prerequisites:

  - oauthprovider
  - webresources
  - oauth
  - opensocial

  Scroll down and Click Save
