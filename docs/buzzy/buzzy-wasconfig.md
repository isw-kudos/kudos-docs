
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

1. Register OAuth

        execfile('oauthAdmin.py')
        OAuthApplicationRegistrationService.addApplication('buzzyop', 'buzzyop', '<BUZZY_URL>/pre-oauth-connections/buzzyop')
  This will return with both a clientsecret and clientid that you need to input in the provider settings. 
