# OAuth2.0
## Types of Roles

- User: Resource Owner
- Device: User Agent
- Application: Client
- Authorization Server
- API: Resource Server

## OAuth Flow

1. User makes a request through User Agent(Browser)- "I want to login to this app"  
2. Before **REDIRECT_URI** by the App, it generates PKCE(Proof Code for Key Exchange) Code Verifier which is stored in app server and which then generates the hashed value **PKCE Code Exchange**.  
3. Authorization Server gives back Authorization code back added to REDIRECT_URI to the user
4. Along with ClientId, Client_Secret and PKCE, the authorization code is handed back to authorization server to exchange Access Token. It validates everything and then it hands back Access Token
5. Access Token is requested from the App Server from the OAuth Server without using Browser.
6. PKCE prevents Authorization code injection attack
7. PKCE Code verifier is hashed into Code Exchange which is validated at the Authorization Server end.


---


