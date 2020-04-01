### Testing an oauth2 connections configuration

This will test a Kudos Boards / Activities Plus oauth setup

#### Update WAS httpd.conf

  change ProxyPass and ProxyPassReverse entries to use a different (invalid) port number.

#### Install and open postman or another api testing tool

#### In postman prepare a request as below


  Method: POST

  Request URL: https://(connections url)/oauth2/endpoint/connectionsProvider/token

  On the Body tab fill in the following:


  | KEY           | VALUE                                                      |
  | ------------- | ---------------------------------------------------------- |
  | client_id     | kudosboards                                                |
  | client_secret | your client secret                                         |
  | redirect_uri  | https://(connections url)/boards/auth/connections/callback |
  | grant_type    | authorization_code                                         |
  | code          | (paste the code from the next step here)                   |

#### Open connections auth

  replace connections url in both places below

    https://(connections url)/oauth2/endpoint/connectionsProvider/authorize?client_id=kudosboards&redirect_uri=https%3A%2F%2F(connections url)%2Fapi-boards%2Fauth%2Fconnections%2Fcallback&response_type=code

#### Click approve

#### Copy code from redirected url

#### Paste the code into postman and hit Send, you should get a response as below:

    {
      "access_token": "s67MkH8LYMMKiP0q2gtVKQxkD0gBcXJJlSCdvQw3",
      "token_type": "Bearer",
      "expires_in": 43199,
      "scope": "",
      "refresh_token": "EcO9hDYdU3tL2BE0xRSPNlYIGvZhYV9yezb14YKNglkFPwq4St"
    }
