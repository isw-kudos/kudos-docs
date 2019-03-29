
## Register OAuth
In order for Kudos Boards to authenticate with your Connections environment, you must define a new OAuth widget.  Please open an SSH to the IBM Connections Deployment Manager and run the following commands.

---

1. Start wsadmin

        cd /opt/IBM/WebSphere/AppServer/profiles/Dmgr01/bin/
        ./wsadmin.sh -lang jython -username connectionsadmin -password passw0rd
        execfile('oauthAdmin.py')

1. Register the new application definition

        OAuthApplicationRegistrationService.addApplication('kudosboards', 'Kudos Boards', 'https://kudosboards.com/auth/connections/[BASE64_CONNECTIONS_URL]/callback')

    Where `[BASE64_CONNECTIONS_URL]`is

      - your Connections hostname base64 encoded.  E.g.</br>
        `connections.example.com` => `Y29ubmVjdGlvbnMuZXhhbXBsZS5jb20=`</br>
        There are many free online services to do this, ie [here](https://www.base64encode.net/)</br></br>


1. To view the uniquely created client clientSecret

        OAuthApplicationRegistrationService.getApplicationById('kudosboards')


    These commands will print the definition. Please take note of the `clientSecret`.  We will use this later on as

        CONNECTIONS_URL=https://connections.example.com
        CONNECTIONS_CLIENT_ID=kudosboards
        CONNECTIONS_CLIENT_SECRET=[VALUE_PRINTED]
