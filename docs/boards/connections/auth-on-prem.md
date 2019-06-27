![Outcome](/assets/connections/auth.png)


## Register OAuth
In order for Kudos Boards to authenticate with your Connections environment, you must define a new OAuth widget.

---

1. SSH to the IBM Connections Deployment Manager (substitute the alias)

        ssh root@[DEPLOY_MANAGER_ALIAS]

1. Start `wsadmin` (substitute your credentials)

        cd /opt/IBM/WebSphere/AppServer/profiles/Dmgr01/bin/
        ./wsadmin.sh -lang jython -username connectionsadmin -password passw0rd

1. Register the new application definition

        execfile('oauthAdmin.py')
        OAuthApplicationRegistrationService.addApplication('kudosboards', 'Kudos Boards', '[BOARDS_URL]/auth/connections/callback')

    Where `[BOARDS_URL]` is the URL of the Boards installation specified previously


1. To view the uniquely created client clientSecret

        OAuthApplicationRegistrationService.getApplicationById('kudosboards')


    These commands will print the definition. Please take note of the `clientSecret`.  We will use this later on as

        CONNECTIONS_URL=https://connections.example.com
        CONNECTIONS_CLIENT_ID=kudosboards
        CONNECTIONS_CLIENT_SECRET=[VALUE_PRINTED]
