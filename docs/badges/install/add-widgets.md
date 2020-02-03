## Step 5: Add the Kudos Widgets to the interface

```
So far, you have configured the location of the Kudos widgets. You will now add the widgets to the user interface.
```
### Task 5.1 – Add the Badges Configurator Widget to the Community

```
Login to IBM Connections
```
```
Navigate to the Badges
Configurator Community
```
```
Click Community Actions
```
```
Select Customize from the
drop down menu
```

```
Select
BadgesConfigurator
```
```
Click X
```
The BadgesConfigurator will now be added to the main view.

```
We recommend removing all the default widgets from the main page (i.e. Forums, Bookmarks, Files and Feeds) to conserve screen real-estate, and
making use of the Configurator widget easier. The default widgets may be removed or added back at any stage.
```

### Task 5.2 – Remove the Default Widgets (Optional)

```
Click the Actions drop-down
```
```
Select Remove from the
menu
```

```
Click the Remove button on the Remove
Widget prompt
```
You will now have the BadgesConfigurator Widget showing on the main page within the Community, and can also open it to the full page by clicking
BadgesConfigurator


The full-page view removes the header and sidebar, and expands the table to allow easier browsing of Badges.


### Task 5.3 – Add the Metrics Configurator Widget to the Community

```
Login to IBM
Connections
```
```
Navigate to the
Metrics Configurator
Community
```
```
Click Community
Actions
```
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


### Task 5.5 – Add the Kudos Analytics Widget to Communities

```
Login to IBM Connections
```
```
Navigate to the Kudos
Analytics Community
```
```
Click Community Actions
```
```
Select Customize from the
drop down menu
```
```
Select KudosAnalytics
```
```
Click X
```

```
We recommend removing all the default widgets from the main page (i.e. Forums, Bookmarks, Files and Feeds) to conserve screen
real-estate, and making use of the Analytics widgets easier. The default widgets may be removed or added back at any stage.
```
Your first Kudos Analytics widget will now be added to the main view.

The default view shows the report categories. Once a report category is selected, default report instances for that category can be selected.


Once the report instance is selected, further options for that report can be selected.


The report currently configured is previewed below the options and can be saved for quick viewing on all subsequent page loads.

In the Kudos Analytics community, the Kudos Analytics widgets provide access to Connections Administrator level reports.
In other communities, the Kudos Analytics widgets can be added to provide access to Community Manager level reports.

Multiple Kudos Analytics widgets are designed to exist in each community.


### Task 5.6 – Add the Leaderboard Widget to the Home page

```
The Kudos Leaderboard Widget allows users to view the top 10 contributors either in the entire organisation or in a specific user’s network. Adding the
Kudos Leaderboard to all users Home page provides easy access for users to view their progress and drive their behaviour.
```
Adding the Leaderboard Widget to the Home page of Connections is done through the Connections Web page. To do this you must be logged in
as a Connections Administrator.

(^)
Login to IBM Connections
Navigate to the Administration tab


Click the Add another widget button


Select iWidget

Specify Kudos Leaderboard as the
Widget Title

Specify /Kudos/RankingDisplay.xml
as the URL Address


Check Display on the Updates page

Check Opened by default

Check profiles within the
Prerequisites options

Click Save


Highlight Kudos Leaderboard in the
Disabled widgets section

Click Enable


The Kudos Leaderboard will now show
in the Enabled widgets list.

It will also show on the Updates and
Widgets tabs, if these options were
selected.


### Task 5.7 – Configure the Kudos News Gadget

```
By defining the Kudos News Gadget in the Homepage Administration tab, the Kudos News Gadget will be made available to the end users. The following
diagram shows how the gadget will be embedded.
```

Login to Connections as a user assigned to the admin security role of the Homepage application.

Click Administration


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

Click the Ok button

Enter a Widget Title and Description.
For example:

Kudos News Gadget

For the URL Address and SECURE URL
Address you must enter the absolute path
of Kudos on your Connections installation.
For example:

[http://<CONNECTIONS_SERVER_URL>](http://<CONNECTIONS_SERVER_URL>)
/Kudos/KudosNewsGadget.xml

https://<CONNECTIONS_SERVER_URL>
/Kudos/KudosNewsGadget.xml


Select:

- Use IBM Connections
    specific tags
- Opened by default


Select the following Pre-
requisites:

- oauthprovider
- webresources
- oauth
- opensocial

Scroll down and Click Save


Select the Kudos News Gadget from the Disabled widgets list

Click Enable


### Task 5.8 A – Define the Kudos Awarder Widget

```
The Kudos Awarder Widget allows an administrator, manager or supervisor to give users awards. Adding the Kudos Awarder Widget to the My Page
section provides easy access to the awarder tool.
```
Adding the Kudos Awarder Widget to the Home page of Connections is done through the Connections Web page. To do this you must be logged
in as a Connections Administrator.


Login to Connections as a user assigned to the admin security role of the Homepage application.

Click Administration


Click Add another widget


Select iWidget

Specify Kudos Awarder as the Widget
Title

Specify /Kudos/KudosAwarder.xml
as the URL Address

If on Connections 4, select Display on
the Widgets Page

If on Connections 4.5+, Select Display
on My Page


Leave all Prerequisites empty.

Select Save


Select the Kudos Awarder from the Disabled widgets list

Click Enable


### Task 5.8 B – Add the Kudos Awarder Widget to My Page

```
Please note that in IBM Connections 5.0 onwards a default widget provided by Connections is required on ‘My Page’ for the Kudos widgets to function.
```
```
Open My Page through the Sidebar link or Home button
```
```
Select Customize
```

Select Kudos Awarder

Click X

You will now have the Kudos Awarder Widget displayed in the My Page section.
**Please Note: The Kudos Awarder cannot be used by a user until they have been allocated awards for distribution. See the User Guide for further
information.**



### Task 5.9 A – Define the Kudos User Analytics Widget

```
The Kudos User Analytics Widget allows people to access user level reports and graphs. Adding the Kudos User Analytics Widget to the My Page
section provides easy access to reports and graphs.
```
Adding the Kudos User Analytics Widget to the Home page of Connections is done through the Connections Web page. To do this you must be
logged in as a Connections Administrator.


Login to Connections as a user assigned to the admin security role of the Homepage application.

Click Administration


Click Add another widget


Select iWidget

Specify Kudos User Analytics as the
Widget Title

Specify
/Kudos/AnalyticsDashboard.xml as
the URL Address

If on Connections 4, select Display on
the Widgets Page

If on Connections 4.5+, Select Display
on My Page

Select Multiple Widgets


Leave all Prerequisites empty.

Select Save


Select Kudos User Analytics from the Disabled widgets list

Click Enable


### Task 5.9 B – Add the Kudos User Analytics Widget to My Page

```
This step will ensure the User Analytics widget was defined successfully in the Administration section, and is working as expected.
This step is a good introduction to User Reports, however is optional.
```
```
Please note that in IBM Connections 5.0 onwards a default widget provided by Connections is required on ‘My Page’ for the Kudos widgets to function.
```
```
Open My Page through the Sidebar link or Home button
```
```
Select Customize
```

Select Kudos User Analytics

Click X


You will now have your first Kudos User Analytics Widget displayed in the My Page section.
From here you can start using Analytics by selecting a report category, and then a specific reports instance.


Multiple Kudos User Analytics widgets are designed to exist on My Page.

