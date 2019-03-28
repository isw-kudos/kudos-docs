
### WebSphere config for Kudos Boards

1. Open WebSphere ISC -> open web server -> edit `http.conf` -> add another VirtualHost

        <VirtualHost *:443>
          ServerName boards.isw.net.au

          #Kudos Boards
          ProxyPreserveHost On
          ProxyPass / http://<server-ip>/
          ProxyPassReverse / http://<server-ip>/
          #End Kudos Boards

          SSLEnable
            # Disable SSLv2
            SSLProtocolDisable SSLv2
            # Set strong ciphers
            SSLCipherSpec TLS_RSA_WITH_AES_128_CBC_SHA
            SSLCipherSpec TLS_RSA_WITH_AES_256_CBC_SHA
            SSLCipherSpec SSL_RSA_WITH_3DES_EDE_CBC_SHA
        </VirtualHost>

1. Register OAuth

        cd /opt/IBM/WebSphere/AppServer/profiles/Dmgr01/bin/
        ./wsadmin.sh -lang jython -username connectionsadmin -password passw0rd
        execfile('oauthAdmin.py')
        OAuthApplicationRegistrationService.addApplication('kudosboards', 'Kudos Boards', '<BOARDS_URL>/auth/connections/callback')
        OAuthApplicationRegistrationService.getApplicationById('kudosboards')

> These commands will define a new OAuth application with `CONNECTIONS_CLIENT_ID=kudosboards`. It will also print the definition. Please take note of the `clientSecret`.  We will refer to this later as `CONNECTIONS_CLIENT_SECRET`.
