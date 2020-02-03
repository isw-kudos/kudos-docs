## Step 6: Additional properties for Communities Widgets (OPTIONAL)

```
At this stage, the Kudos Configuration Widgets show in the Communities Customization Palette for all Communities. This means they can be added to
any community.
```
```
However, they are restriced to function only in their respective Community created during this installation process. This message will be shown if they
are added to any other community.
```
```
It is possible to remove these Widgets from the Customizations Palette, so that users cannot see/add them to their Communties. This requires modifying
the Configuration Widget definitions we created earlier in the widgets-config.xml file and restarting the clusters again.
```
Checkout and edit the widgets-config.xml file as per Task 2.4

Locate the Configuration Widget definitions

- Under <resources type="community"> section
- under <widgets>
- within <definitions>


Add the attribute showInPalette="false" to each Configurator you wish to hide from the Customizations page.
We could not define this attribute earlier, as otherwise we wouldn’t have been able to add the Widgets to the
Configuration Communities.

Add the attribute loginRequired="true" to each Community widget if you wish to hide the widgets from users that are not logged in.
This is only applicable if your security settings for the Communities application allow users to view communities without logging in.

Your configuration should now look like this:
<widgetDef defId="BadgesConfigurator" description="badgesConfigurator" modes="view fullpage" url="https://<CONNECTIONS_SERVER_URL>/Kudos/BadgesConfigurator.xml"
themes="wpthemeWide" showInPalette="false" loginRequired="true">
<itemSet>
<item name="resourceId" value="{resourceId}"/>
<item name="communityId" value="YOUR_BADGES_COMMUNITY_UUID"/>
</itemSet>
</widgetDef>
<widgetDef defId="MetricsConfigurator" description="metricsConfigurator" modes="view fullpage" url="https://<CONNECTIONS_SERVER_URL>/Kudos/MetricsConfigurator.xml"
themes="wpthemeWide" showInPalette="false" loginRequired="true">
<itemSet>
<item name="resourceId" value="{resourceId}"/>
<item name="communityId" value="YOUR_METRICS_COMMUNITY_UUID"/>
</itemSet>
</widgetDef>
<widgetDef defId="FiltersConfigurator" description="filtersConfigurator" modes="view fullpage" url="https://<CONNECTIONS_SERVER_URL>/Kudos/FiltersConfigurator.xml"
themes="wpthemeWide" showInPalette="false" loginRequired="true">
<itemSet>
<item name="resourceId" value="{resourceId}"/>
<item name="communityId" value="YOUR_FILTERS_COMMUNITY_UUID"/>
</itemSet>
</widgetDef>
<widgetDef defId="KudosCommunity" modes="view" url="https://<CONNECTIONS_SERVER_URL>/Kudos/CommunityRankingDisplay.xml" themes="wpthemeNarrow wpthemeWide"
showInPalette="false" loginRequired="true">
<itemSet>
<item name="communityId" value="{resourceId}"/>
</itemSet>
</widgetDef>

Check-in the widgets-config.xml (as per Task 2.8) and restart the clusters (as per Step 4).
