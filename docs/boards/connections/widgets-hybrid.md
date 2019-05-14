# IBM Connections Widget Setup
Basic instructions for adding Kudos Boards Hybrid widgets into IBM Connections on-premise environments

---

### Community Widget

Check out the widgets-config.xml file.

    execfile("profilesAdmin.py")
    ProfilesConfigService.checkOutWidgetConfig("/LCCheckedOut", AdminControl.getCell())

Edit the widgets-config.xml file. Find the resource element with the type of community, e.g. `<resource ... type="community" ... >`, then under `<widgets>`, then within `<definitions>` add the following:

    <!-- Kudos Boards -->
    <widgetDef defId="Kudos Boards" modes="view fullpage" url="{webresourcesSvcRef}/web/com.ibm.social.urliWidget.web.resources/widget/urlWidget.xml" themes="wpthemeNarrow wpthemeWide wpthemeBanner" uniqueInstance="true">
      <itemSet>
      <item name="resourceId" value="{resourceId}"/>
        <item name="width" value="100%"/>
        <item name="height" value="500px"/>
        <item name="url" value="https://kudosboards.com/boards/community/connections"/>
      </itemSet>
    </widgetDef>
    <!-- END Kudos Boards -->

Check in the widgets-config.xml file.

    ProfilesConfigService.checkInWidgetConfig()

---

### Activity Stream widget

Access `Homepage`->`Administrator`

Select the following:

  - Open Social Gadget
  - Trusted and Use SSO
  - Show for Activity Stream events
  - All servers

  Click the `Add Mapping` button.

Add a Mapping for the Kudos Boards service to the Kudos client. Ensure OAuth Client is set to conn-ee and the Service name is Kudos Boards.
Click the Ok button

Enter the following:

  | Field | Value |
  | ----- | ----- |
  | Title| Kudos Boards Activity Stream |
  | URL Address| `http://kudosboards.com/stream/connections`|
  | Secure URL Address| `https://kudosboards.com/stream/connections`|
  | ICON URL| `http://kudosboards.com/favicon.ico`|
  | ICON SECURE URL| `https://kudosboards.com/favicon.ico`|

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

<!-- This is not needed for the iframe widget
### Register Widget

Required for IBM Connections 6.0 CR1 onwards:

    execfile("newsAdmin.py")
    NewsWidgetCatalogService.addWidget(title="Kudos Boards", url="http://kudosboards.com/boards/community/connections" ,secureUrl="https://kudosboards.com/boards/community/connections", categoryName=WidgetCategories.NONE, isHomepageSpecific=0, isDefaultOpened=0, multipleInstanceAllowed=0, isGadget=0, policyFlags=[GadgetPolicyFlags.TRUSTED], prereqs=['communities'], appContexts=["IWIDGETS"])
    NewsWidgetCatalogService.enableWidget("<ID_RETURNED>")
    NewsWidgetCatalogService.clearWidgetCaches()
-->
