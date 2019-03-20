# Kudos Ideas for IBM Connections Cloud

### Oauth configuration
Please setup oAuth access for Kudos Ideas as follow

1. Login to connections cloud
1. Click your profile (top right) and select Account settings
1. On the left side of the page, click Internal Apps
1. Click Register App
1. Enter App Name and Description as Kudos Ideas
1. Choose OAuth 2.0 as the Auth Type
1. Enter `https://ideas.isw.net.au/auth/smartcloud` as the Callback URL
1. Click Register
1. Find Kudos Ideas in the list of Internal Apps, click the menu button next to it and select Edit Properties
1. Look at the App ID assigned, it should be in the form `app_(your org id)_(unique id)`
1. Copy the org id part of this App ID (the first set of numbers)
1. update the callback URL to `https://ideas.isw.net.au/auth/smartcloud/(your org id)/callback`
1. Click Ok
1. Click the menu button next to Kudos Ideas again and select Show Credentials
1. Copy the ClientID and Client Secret and send them, along with your business and contact information to <support@kudosbadges.com>

### NavBar Extension

- Click Admin, Manage Organisation
- Click Organisation Extensions

- Create a file called navbar.json in notepad or another text editor, copy the content below into it (replacing your team name where indicated)
- Click Add and select the file you created
```
{
  "extensions": [
	{
  	"path": "com.ibm.navbar",
  	"application": "Ideas",
  	"payload": {
    	"link": "https://ideas.isw.net.au/login?team=(your team name here)",
    	"icon": "https://ideas.isw.net.au/kudos_icon.png",
    	"tooltip": "Kudos Ideas"
  	},
  	"name": "Kudos Ideas",
  	"description": "Ideation done right",
  	"id": "576eccbe-c6ec-43b3-9053-a3e83e2f0875",
  	"type": "com.ibm.action.link",
  	"title": "Kudos Ideas"
	}
  ],
  "payload": {
	"pre-migration": {
  	"migration-type": "navbar",
  	"migration-date": "1492920891409"
	}
  },
  "translations": {},
  "name": "Ideas",
  "description": "Ideation done right for IBM Connections",
  "services": [
	"TopNavigationBar"
  ],
  "title": "Kudos Ideas"
}
```

### Community Extension

- Click Admin, Manage Organisation
- Click Organisation Extensions
- Click Add and choose manual Installation, fill in the details as below:

    - Service: Communities
    - Extension Point: Community App
    - Name: Kudos Ideas
    - Icon URL: https://ideas.isw.net.au/kudos_icon.png
    - URL: https://ideas.isw.net.au/widget/smartcloud
    - Properties:
```
{
	"defId": "kudos-ideas",
	"themes": "wpthemeThin wpthemeNarrow wpthemeWide wpthemeBanner",
	"modes": "view fullpage",
	"primaryWidget": "true",
	"showInPalette": "true",
	"itemSet": [
    	{
        	"name": "height",
        	"value": "500px"
    	},
    	{
        	"name": "width",
        	"value": "100%"
    	},
    	{
        	"name": "url",
        	"value": "https://ideas.isw.net.au/widget/smartcloud"
    	}
	],
	"url": "https://apps.na.collabserv.com/connections/resources/web/com.ibm.social.urliWidget.web.resources/widget/urlWidget.xml"
}
```
