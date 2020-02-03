#### Step 3: Install Kudos Mobile (Optional)

```
Kudos integrates into the IBM Connections Mobile native application and allows users to utilise Kudos features from their mobile device. The integration
is performed by modifying the mobile-config.xml configuration. This feature is optional.
```

##### Task 3.1 – Check out the mobile-config.xml file

To add ‘Kudos Badges’ to the Connections mobile native app menu you must edit the mobile-config.xml file.
To update this file, you must check the file out and, after making changes, you must check the file back in, as documented here.

```
The mobile-config.xml file is a standard IBM Connections file that is used to define the configuration settings for the Connections Mobile native
application. To update this file, you must check the file out and, after making changes, check the file back in during the same wsadmin session as the
checkout for the changes to take effect.
```

### Task 3.2 – Edit the mobile-config.xml

Then proceed to add the following Application definition under the <Applications> node
<Application name="Kudos" enabled="true">
<ApplicationIcon>
<Android>
<Hdpi> **../../** Kudos/images/mobile_android.png</Hdpi>
<Mdpi> **../../** Kudos/images/mobile_android.png</Mdpi>
<Ldpi> **../../** Kudos/images/mobile_android.png</Ldpi>
</Android>
<IOS>
<Reg> **../../** Kudos/images/mobile_iOS.png</Reg>
<Retina> **../../** Kudos/images/mobile_iOS.png</Retina>
</IOS>
<BB>
<HighDensity>http://<YOUR_CONNECTIONS_SERVER>/Kudos/images/mobile_BB.png</HighDensity>
<MedDensity>http://<YOUR_CONNECTIONS_SERVER>/Kudos/images/mobile_BB.png</MedDensity>
<LowDensity>http://<YOUR_CONNECTIONS_SERVER>/Kudos/images/mobile_BB.png</LowDensity>
</BB>
<DefaultLocation> **../../** Kudos/images/mobile_default.png</DefaultLocation>
</ApplicationIcon>
<ApplicationLabel>Kudos Badges</ApplicationLabel>
<ApplicationURL>http://<YOUR_CONNECTIONS_SERVER>/Kudos/mobile</ApplicationURL>
</Application>

For IBM Connections 5.0 only: Add the following to the <ApplicationList> node: Kudos.
The result should be similar to: <ApplicationsList>profiles,communities,files,wikis,activities,forums,blogs,bookmarks,Kudos</ApplicationsList>

**Please Notes: Make sure you replace <YOUR_CONNECTIONS_SERVER> in all places with the URL of your Connections Environment.
If you use a custom context root for Kudos, please ensure you update the references above appropriately.
You can customise the name/images shown in the Mobile application by changing the text/URLs above.**


Here is an example of how the definition should look once inserted into the mobile-config.xml and URLs replaced:

### Task 3.3 – Check in the mobile-config.xml file

Now that you have modified the mobile-config.xml, it must be checked back in to IBM Connections. Please refer to the IBM Connections product
documentation for instructions on how to check in the mobile-config.xml file, located here.

**Note: the configuration file must be checked in during the same wsadmin session in which it was checked out.**

