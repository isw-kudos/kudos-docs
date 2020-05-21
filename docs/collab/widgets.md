# HCL Connections Multi-Tenant Widget Setup

Adding Activities Plus widgets into HCL Connections Multi-Tenant environments

---

### Community Widget

1. Check out the widgets-config.xml file.

        execfile("profilesAdmin.py")
        ProfilesConfigService.checkOutWidgetConfig("/tmp", AdminControl.getCell())

1. Edit the widgets-config.xml file

    Find the resource element with the type of community, e.g. `<resource ... type="community" ... >`, then under `<widgets>`, then within `<definitions>` add the following:

        <!-- Activities Plus -->
        <widgetDef defId="Activities Plus" modes="view fullpage" url="{webresourcesSvcRef}/web/com.ibm.social.urliWidget.web.resources/widget/urlWidget.xml" themes="wpthemeNarrow wpthemeWide wpthemeBanner" uniqueInstance="true">
        <itemSet>
        <item name="resourceId" value="{resourceId}"/>
            <item name="width" value="100%"/>
            <item name="height" value="500px"/>
            <item name="url" value="https://kudosboards.com/community/collab"/>
        </itemSet>
        </widgetDef>
        <!-- END Activities Plus -->

1. Check in the widgets-config.xml file.

        ProfilesConfigService.checkInWidgetConfig()

1. Restart the `Communities` application via the ISC

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
    - Service name: `Activities Plus`

    Click `Ok`


1. Enter the following:


    | Field              | Value                                        |
    | ------------------ | -------------------------------------------- |
    | App Title              | Activities Plus Stream                 |
    | URL Address        | `https://kudosboards.com/stream/collab`  |
    | Icon URL           | `http://kudosboards.com/favicon.ico`         |
    | Icon Secure URL    | `https://kudosboards.com/favicon.ico`        |


    Select:

    - `Use HCL Connections specific tags`
    - `Opened by default`


1. Select the following Prerequisites:

    - `oauthprovider`
    - `oauth`
    - `opensocial`
    - `webresources`

    Scroll down and click `Save`

    ![Example](/assets/connections/homepage-admin5.png)


1. Select the newly defined app and click `Enable`

    ![Example](/assets/connections/homepage-admin6.png)
