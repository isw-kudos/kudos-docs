So far, you have configured the location of the Kudos widgets. You will now add the widgets to the user interface.

### Add the Configurators Widgets to their Communities

Login to IBM Connections

Navigate to the Badges Configurator Community

Click Community Actions

Select Customize from the drop down menu

Select BadgesConfigurator

Click X

The BadgesConfigurator will now be added to the main view.

We recommend removing all the default widgets from the main page (i.e. Forums, Bookmarks, Files and Feeds) to conserve screen real-estate, and
making use of the Configurator widget easier. The default widgets may be removed or added back at any stage.

### Remove the Default Widgets (Optional)

Click the Actions drop-down

Select Remove from the menu

Click the Remove button on the Remove Widget prompt

You will now have the BadgesConfigurator Widget showing on the main page within the Community, and can also open it to the full page by clicking BadgesConfigurator

The full-page view removes the header and sidebar, and expands the table to allow easier browsing of Badges.

### Add the Metrics Configurator Widget to the Community

Login to IBM Connections

Navigate to the Metrics Configurator Community

Click Community Actions

```
Select Customize
from the drop down
menu
```
```
Select
MetricsConfigurator
```
```
Click X
```

```
We recommend removing all the default widgets from the main page (i.e. Forums, Bookmarks, Files and Feeds) to conserve
screen real-estate, and making use of the Configurator widget easier. The default widgets may be removed or added back at any stage.
```
The MetricsConfigurator will now be added to the main view.

If you see an error message saying you are not authorised to use this Widget, then double check you copied the entire CommunityUuid into the
correct widget-config.xml definition


### Task 5.4 – Add the Filters Configurator Widget to the Community

```
Login to IBM Connections
```
```
Navigate to the Filters
Configurator Community
```
```
Click Community
Actions
```
```
Select Customize from
the drop down menu
```
```
Select
FiltersConfigurator
```
```
Click X
```

```
We recommend removing all the default widgets from the main page (i.e. Forums, Bookmarks, Files and Feeds) to conserve screen
real-estate, and making use of the Configurator widget easier. The default widgets may be removed or added back at any stage.
```
The FiltersConfigurator will now be added to the main view.

If you see an error message saying you are not authorised to use this Widget, then double check you copied the entire CommunityUuid into the
correct widget-config.xml definition


### Add the Kudos Analytics Widget to Communities

Login to IBM Connections

Navigate to the Kudos Analytics Community

Click Community Actions

Select Customize from the drop down menu

Select KudosAnalytics

Click X

We recommend removing all the default widgets from the main page (i.e. Forums, Bookmarks, Files and Feeds) to conserve screen real-estate, and making use of the Analytics widgets easier. The default widgets may be removed or added back at any stage.

Your first Kudos Analytics widget will now be added to the main view.

The default view shows the report categories. Once a report category is selected, default report instances for that category can be selected.

Once the report instance is selected, further options for that report can be selected.

The report currently configured is previewed below the options and can be saved for quick viewing on all subsequent page loads.

In the Kudos Analytics community, the Kudos Analytics widgets provide access to Connections Administrator level reports. In other communities, the Kudos Analytics widgets can be added to provide access to Community Manager level reports.

Multiple Kudos Analytics widgets are designed to exist in each community.

### Add the Widgets to the Home page

The Kudos Leaderboard Widget allows users to view the top 10 contributors either in the entire organisation or in a specific user’s network. Adding the
Kudos Leaderboard to all users Home page provides easy access for users to view their progress and drive their behaviour.

By defining the Kudos News Gadget in the Homepage Administration tab, the Kudos News Gadget will be made available to the end users. The following diagram shows how the gadget will be embedded.

Adding widgets to the Home page of Connections is done through the Connections Web page. 

Login to Connections as a user assigned to the admin security role of the Homepage application and navigate to the Administration tab.

Click the Add another widget button and enter the following details. Once you have defined each widget, click Save and then click the 'Add another widget' button to add the next.

|                | Widget Type        | Widget Title         | URL Address                                                     | Display on Updates Page | Display on My Page | Opened by Default | Multiple Widgets | Prerequisites                                  |
|----------------|--------------------|----------------------|-----------------------------------------------------------------|-------------------------|--------------------|-------------------|------------------|------------------------------------------------|
| Leaderboard    | iWidget            | Kudos Leaderboard    | https://`<CONNECTIONS_SERVER_URL>`/Kudos/RankingDisplay.xml     | True                    | False              | True              | False            | profiles                                       |
| News Gadget    | Open Social Gadget | Kudos News Gadget    | https://`<CONNECTIONS_SERVER_URL>`/Kudos/KudosNewsGadget.xml    | False                   | True               | True              | False            | oauthprovider, webresources, oauth, opensocial |
| Awarder        | iWidget            | Kudos Awarder        | https://`<CONNECTIONS_SERVER_URL>`/Kudos/KudosAwarder.xml       | False                   | True               | False             | False            | -                                              |
| User Analytics | iWidget            | Kudos User Analytics | https://`<CONNECTIONS_SERVER_URL>`/Kudos/AnalyticsDashboard.xml | False                   | True               | False             | True             | -                                              |

Highlight each Kudos widget in the Disabled widgets section and click Enable

The Kudos widgets will now show in the Enabled widgets list.

It will also show on the Updates and Widgets tabs, if these options were selected.

### Task Configure the Kudos News Gadget

Click Add another widget

Select the following:

- Open Social Gadget
- Trusted and Use SSO
- Show for Activity Stream
    events
- All servers

Click the Add Mapping button.

Add a Mapping for the Kudos service to
the Kudos client. Ensure OAuth Client is
set to Kudos and the Service name is
Kudos.

Select:

- Use IBM Connections
    specific tags

### Add the Kudos Awarder Widget to My Page

**Please Note:** A default widget provided by Connections is required on ‘My Page’ for the Kudos widgets to function.

Open My Page through the Sidebar link or Home button

Select Customize

Select Kudos Awarder

Click X

You will now have the Kudos Awarder Widget displayed in the My Page section.
**Please Note:** The Kudos Awarder cannot be used by a user until they have been allocated awards for distribution. See the User Guide for further
information.

### Add the Kudos User Analytics Widget to My Page

This step will ensure the User Analytics widget was defined successfully in the Administration section, and is working as expected. This step is a good introduction to User Reports, however is optional.

**Please Note:** A default widget provided by Connections is required on ‘My Page’ for the Kudos widgets to function.

Open My Page through the Sidebar link or Home button

Select Customize

Select Kudos User Analytics

Click X

You will now have your first Kudos User Analytics Widget displayed in the My Page section. From here you can start using Analytics by selecting a report category, and then a specific reports instance.

Multiple Kudos User Analytics widgets are designed to exist on My Page.