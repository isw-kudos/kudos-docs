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
          <Hdpi>http://<BOARDS_URL>.com/img/logo-small.png</Hdpi>
          <Mdpi>http://<BOARDS_URL>.com/img/logo-small.png</Mdpi>
          <Ldpi>http://<BOARDS_URL>.com/img/logo-small.png</Ldpi>
        </Android>
        <IOS>
          <Reg>http://<BOARDS_URL>.com/img/logo-small.png</Reg>
          <Retina>http://<BOARDS_URL>.com/img/logo-small.png</Retina>
        </IOS>
        <BB>
          <HighDensity>http://<BOARDS_URL>.com/img/logo-small.png</HighDensity>
          <MedDensity>http://<BOARDS_URL>.com/img/logo-small.png</MedDensity>
          <LowDensity>http://<BOARDS_URL>.com/img/logo-small.png</LowDensity>
        </BB>
        <DefaultLocation>http://<BOARDS_URL>.com/img/logo-small.png</DefaultLocation>
      </ApplicationIcon>
      <ApplicationLabel>Kudos Boards</ApplicationLabel>
      <ApplicationURL>https://<BOARDS_URL>.com/auth/connections/</ApplicationURL>
    </Application>

Where `<BOARDS_URL>` your configured URL for Boards.

For Kudos Boards to appear in the app menu, add 'Boards' to the ApplicationList

Check in the widgets-config.xml file.

    MobileConfigService.checkInConfig("/LCCheckedOut", AdminControl.getCell())
