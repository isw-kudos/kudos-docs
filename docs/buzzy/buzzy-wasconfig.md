
### WebSphere config for Buzzy

1. Open WebSphere ISC -> open web server -> edit `http.conf` -> add another VirtualHost

        <VirtualHost *:443>
          ServerName buzzy.isw.net.au

          #Buzzy On-prem
          ProxyPreserveHost On
          ProxyPass / http://<server-ip>:30289/
          ProxyPassReverse / http://<server-ip>:30289/
          #End Buzzy On-prem

          SSLEnable
            # Disable SSLv2
            SSLProtocolDisable SSLv2
            # Set strong ciphers
            SSLCipherSpec TLS_RSA_WITH_AES_128_CBC_SHA
            SSLCipherSpec TLS_RSA_WITH_AES_256_CBC_SHA
            SSLCipherSpec SSL_RSA_WITH_3DES_EDE_CBC_SHA
        </VirtualHost>

### Register OAuth

  In order for Buzzy to authenticate with your Connections environment, you must define a new OAuth widget.

  ---

  1. SSH to the IBM Connections Deployment Manager (substitute the alias)

          ssh root@[DEPLOY_MANAGER_ALIAS]

  1. Start `wsadmin` (substiture your credentials)

          cd /opt/IBM/WebSphere/AppServer/profiles/Dmgr01/bin/
          ./wsadmin.sh -lang jython -username connectionsadmin -password passw0rd

  1. Register the new application definition

          execfile('oauthAdmin.py')
          OAuthApplicationRegistrationService.addApplication('buzzy', 'buzzy', '<BUZZY_URL>/pre-oauth-connections/buzzy')

      Where `[BUZZY_URL]` is the URL of the Buzzy installation specified previously


  1. To view the uniquely created client clientSecret

          OAuthApplicationRegistrationService.getApplicationById('buzzy')


      These commands will print the definition. Please take note of the `clientSecret`.  We will use this later on as
