# OAuth2.0
## Types of Roles

- User: Resource Owner
- Device: User Agent
- Application: Client
- Authorization Server
- API: Resource Server

## OAuth Flow

1. User makes a request through User Agent(Browser)- "I want to login to this app"  
2. Before **REDIRECT_URI** by the App, it generates PKCE(Proof Code for Key Exchange) Code Verifier which is stored in app server and which then generates the hashed value **PKCE Code Exchange**(One-way hashing).  
3. Authorization Server gives back Authorization code back added to REDIRECT_URI to the user
4. Along with ClientId, Client_Secret and PKCE, the authorization code is handed back to authorization server to exchange Access Token. It validates everything and then it hands back Access Token
5. Access Token is requested from the App Server from the OAuth Server without using Browser.
6. PKCE prevents Authorization code injection attack
7. PKCE Code verifier is hashed into Code Exchange which is validated at the Authorization Server end.

```bash
https://dev-v0p3runb2af8sosz.us.auth0.com/authorize?response_type=code&client_id=KlwQZtwSEnl5DM8YydRnuo62O5Y0WXUh&state=shljkahjhshkjssj&
redirect_uri=https://example-app.com/redirect&code_challenge=Dtw1aDnweAf141bUROxMGzzZAIQWTz1hr4UH3aKHL4E&
code_challenge_method=S256

```


---

## Challenges of opening Native Application

1. Not to leave the context of the web app
2. Integrating the Webview: The User can't see the address bar and system doesn't let share the cookies

## To resolve this:
1. We have special APIs to open webview within the Native Application. Both are decoupled.  
2. And we don't even have to exit these application while securing login to these webviews and document

## Refresh Tokens

1. Stored with the help of Secured Storage API requests
2. Even the app's code can't access it, it is that much secure

## XSS/Cross-Site Scripting

1. Running code within application which looks like a legitimate code and making request to get access token and refresh token

2. CSP is the answer but it makes running Analytics and Ad related things difficult to run on the web page.

3. No secure-storage API is available in browser

## Flow for SPA

1. Only Client ID is used
2. On the first instance, the PKCE Code verifier is hashed.
3. On the Authorization Server, we pass on hash, Client ID, redirect URL and scope.
4. The request is forwarded to web browser to handle it with Auth Server
5. After getting Authorization code, it makes back channel request from javascript code to get Access-Token and refresh-Token and validation of Code verifier with the hash takes place
6. Cross-Site Scripting makes the access-token vulnerable. We may store tokens only in memory, use Service Worker(not supported in IE 11) to handle API requests or use WebCrypto API(Not supported in IE or Safari) and uses private key to store tokens which can still be exploited in XSS.

## Using Dynamic Backend Server to handle OAuth Flow

1. HttpOnly Session cookie is handled from a browser, even a session cookie won't be stolen.

2. Authorization Code is handled via Browser from Authorization server. It is then passed on to Dynamic Backend Server via front-channel request and setting cookie only on web browser.

3. And then API is requested via Cookie

## OAuth for IOT Devices

1. Device requests for Device Code and user code with ClientId and scope in payload.

2. User enters the code in another device while the IoT device polls continuously to check if the user has logged in or not.

3. And refresh token is used to handle expiry and get Access Tokens

## Client Credentials Grant

1. Machine-to-Machine / Service Account which gives you Client ID or Client Secret enabling communication and authorization without user in between.

2. Request Client ID and Client Secret through web app.

| Access Token | ID Token |
|---|---|
|Access Token are opaque to applications which are using it | ID token has three parts: **Headers**(Algorithm used to encrypt as well as the key which signed the ID Token) , **Payload**: base64 encrypted JSON and **Signature**
|Access token have audience as the Resource Server | ID token has application as an audience |

