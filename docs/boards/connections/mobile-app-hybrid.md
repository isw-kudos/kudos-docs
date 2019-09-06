# IBM Connections Mobile App Setup
Basic instructions for adding Kudos Boards into the HCL Connections mobile application

---

### Mobile App Integration

Check out the mobile-config.xml file.

    execfile("mobileAdmin.py")
    MobileConfigService.checkOutConfig("/LCCheckedOut", AdminControl.getCell())

Edit the mobile-config.xml file. Find the Applications element and add the following Application:

    <Application name="Boards" enabled="true">
      <ApplicationIcon>
        <Android>
          <Hdpi>http://kudosboards.com/img/logo-small.png</Hdpi>
          <Mdpi>http://kudosboards.com/img/logo-small.png</Mdpi>
          <Ldpi>http://kudosboards.com/img/logo-small.png</Ldpi>
        </Android>
        <IOS>
          <Reg>http://kudosboards.com/img/logo-small.png</Reg>
          <Retina>http://kudosboards.com/img/logo-small.png</Retina>
        </IOS>
        <BB>
          <HighDensity>http://kudosboards.com/img/logo-small.png</HighDensity>
          <MedDensity>http://kudosboards.com/img/logo-small.png</MedDensity>
          <LowDensity>http://kudosboards.com/img/logo-small.png</LowDensity>
        </BB>
        <DefaultLocation>http://kudosboards.com/img/logo-small.png</DefaultLocation>
      </ApplicationIcon>
      <ApplicationLabel>Kudos Boards</ApplicationLabel>
      <ApplicationURL>https://kudosboards.com/auth/connections/[CONNECTIONS_HOSTNAME_BASE64]</ApplicationURL>
    </Application>

Where `[CONNECTIONS_HOSTNAME_BASE64]` is your Connections hostname base64 encoded.  E.g.</br>
      `connections.example.com` => `Y29ubmVjdGlvbnMuZXhhbXBsZS5jb20=`</br>

For Kudos Boards to appear in the app menu, add 'Boards' to the ApplicationList

Check in the widgets-config.xml file.

    MobileConfigService.checkInConfig("/LCCheckedOut", AdminControl.getCell())
