<h1>Changes needed for hosting in your Azure Environment</h1>

<b>App Service Detail</b>

OS:
 - Linux OS
App Settings:
 - CLIENT_ID
   Value: <your registered application's client ID>
 - CLIENT_SECRET
   Value: <your registered application's client secret>
 - DIRECTORY_ID
   Value: <tenant ID for your registered application>
 - NODE_ENV
   Value: "production"
 - port
   Value: 8080
 - SERVER_SOURCE
   Value: <site_url_for_example_https://office-sso.azurewebsites.net>

<b> Azure AD Changes </b>
- Update Exposed API in the Application to be your registered App Service URI

<b>Code Changes needed:</b>
1) /bin/www
- Replace the following line which loads the dev certs 

        var devCerts = require('office-addin-dev-certs');

    WITH

    var devCerts;
    if (process.env.NODE_ENV === 'development') {
        devCerts = require('office-addin-dev-certs');
    }

2) /manifest/manifest.xml
- Replace all occurences of https://localhost:44355/ with your hosted App Service URL
- Ensure to replace the API in WebApplicationInfo-->Resource

3) authConfig.js
- Replace the redirect URI with your App Service's URI
- Replace the postLogoutRedirectURI with your App Service's URI

