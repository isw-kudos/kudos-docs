## Download the Application
The latest .ear from [releases page](https://github.com/isw-kudos/connections-apps-loader/releases)

## Open WebSphere ISC
This is usually accessible through a URL like:</br>
`https://[DEPLOY_MANAGER_ALIAS]:9043/ibm/console/login.do?action=secure`

## Create Config
Set WebSphere variable to configure the apps/urls to open through the frame:

Open Environment => WebSphere Variables</br>
Set `Scope: Cell`</br>
Create `New` with:

    EXTERNAL_APPS_CONFIG =
      {"[APP_NAME]":"[URL_OF_APP]","[APP_NAME_2]":"[URL_OF_APP_2]"}

Where:

  - `[APP_NAME]` is unique, without spaces or special characters
  - `[URL_OF_APP]` is a web address, ie `https://google.com`


For example, here are 3 apps we load:

    EXTERNAL_APPS_CONFIG =
    {"ideas":"https://ideas.isw.net.au","buzzy":"https://buzzy.buzz","contacts":"https://apps.isw.net.au"}

## Install the App

__a)__ Install EAR in WebSphere using default binding of `/apps`</br>
Load `https://connections.company.com/apps` to see all apps defined above.</br>
Each app will be available at this path, ie:

    https://connections.company.com/apps/[APP-NAME]

__AND/OR__

__b)__ Install EAR multiple times, with customised contextRoot</br>
This method will allow you to load the app without the /apps prefix.</br>
The context root must be in the format `/[APP_NAME]`</br></br>

For example, install the Application as:</br>
Name: `Ideas Frame`</br>
Context root: `/ideas`</br>
The Ideas app will load at this path:</br>
`https://connections.company.com/ideas`

## Start the New App
Tick the box next to the app name, and click `Start`
