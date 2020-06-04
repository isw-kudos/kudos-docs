# HCL Connections Widget Setup

Basic instructions for adding Kudos Boards Docker widgets into HCL Connections on-premise environments

---

### Community Widget

1.  Check out the widgets-config.xml file.

        execfile("profilesAdmin.py")
        ProfilesConfigService.checkOutWidgetConfig("/LCCheckedOut", AdminControl.getCell())

1.  Edit the widgets-config.xml file.

    Find the resource element with the type of community, e.g. `<resource ... type="community" ... >`, then under `<widgets>`, then within `<definitions>` add the following, replacing `[BOARDS_URL]` with your URL:

        <!-- Kudos Boards -->
        <widgetDef defId="Kudos Boards" modes="view fullpage" url="{webresourcesSvcRef}/web/com.ibm.social.urliWidget.web.resources/widget/urlWidget.xml" themes="wpthemeNarrow wpthemeWide wpthemeBanner" uniqueInstance="true">
            <itemSet>
                <item name="resourceId" value="{resourceId}"/>
                <item name="width" value="100%"/>
                <item name="height" value="500px"/>
                <item name="url" value="https://[BOARDS_URL]/boards/community/connections"/>
            </itemSet>
        </widgetDef>
        <!-- END Kudos Boards -->

1.  Check in the widgets-config.xml file.

        ProfilesConfigService.checkInWidgetConfig()

1.  Restart the `Communities` application via the ISC

---

### Activity Stream widget

1. Open `Homepage` => `Administration`

   Click `Add another app`

   ![Example](/assets/connections/homepage-admin.png)

1. Select the following:

   - `OpenSocial Gadget`
   - `Trusted` and `Use SSO`
   - `Show for Activity Stream events`
   - `All servers`

   Click the `Add Mapping` button.

   ![Example](/assets/connections/homepage-admin2.png)

1. Enter values:

   - OAuth Client: `conn-ee`
   - Service name: `connections_service`

   Click `Ok`

1. Enter the following, replacing `[BOARDS_URL]` with your URL:

   | Field           | Value                                                     |
   | --------------- | --------------------------------------------------------- |
   | App Title       | Kudos Boards Stream                                       |
   | URL Address     | `https://[BOARDS_URL]/widgets/connections/url-gadget.xml` |
   | Icon URL        | `https://[BOARDS_URL]/favicon.ico`                        |
   | Icon Secure URL | `https://[BOARDS_URL]/favicon.ico`                        |

   Scroll down and click `Save`

1. Select the newly defined app and click `Enable`

   ![Example](/assets/connections/homepage-admin6.png)

