## Adding Reverse Proxy
1. Open WebSphere ISC

    This is usually accessible through a URL like:

        https://[DEPLOY_MANAGER_ALIAS]:9043/ibm/console/logon.jsp

    ![example](/assets/connections/isc.png)

1. Open `Servers` -> `Server Types` => `Web servers`

    Click on the name of your web server

    ![example](/assets/connections/httpd1.png)

1. Click `Edit` on the `http.conf`

    ![example](/assets/connections/httpd2.png)

1. Add another VirtualHost after existing, with definition:

        <VirtualHost *:443>
          ServerName [BOARDS-URL]

          #Kudos Boards
          ProxyPreserveHost On
          ProxyPass / http://[SERVER-IP]/
          ProxyPassReverse / http://[SERVER-IP]/
          #End Kudos Boards

          SSLEnable
            # Disable SSLv2
            SSLProtocolDisable SSLv2
            # Set strong ciphers
            SSLCipherSpec TLS_RSA_WITH_AES_128_CBC_SHA
            SSLCipherSpec TLS_RSA_WITH_AES_256_CBC_SHA
            SSLCipherSpec SSL_RSA_WITH_3DES_EDE_CBC_SHA
        </VirtualHost>

    Where:

      `[BOARDS-URL]` is the URL of your boards Deployment</br>
      `[SERVER-IP]` is the IP of the master in your cluster
