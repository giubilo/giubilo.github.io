{
    "title": "Alfresco oAuth sample application",
    "description": "Authenticating to alfreasco cloud with oAuth.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "oauth" ],
    "status": "research"
}

<html>
<table border="0">
<tr>
  <td>
    <p>
      <img src="/assets/mages/paint-by-numbers.png?raw=true" alt="book">
    </p>
  </td>
  <td>
    <p>This paint by numbers has used:</p>
    <p><b>Alfresco 4.2</b></p>
    <p><b>CMIS Workbench 0.9.0-beta-1 & 0.10.0</b></p>
  </td>
  <td>
    <p></p>
    <p><b>oAuth Sample webapp</b></p>
  </td></tr>
</table> 
</html>

In October 2012, Alfresco [announced](http://www.alfresco.com/news/press-releases/alfrescos-cloud-api-mobile-apps-now-available) an open application-programming interface [(API) for Alfresco in the cloud](https://www.alfresco.com/develop/cloud).

There are some great resources available to show how to use the cloud api, including:  
* [video tutorials](https://www.youtube.com/watch?v=TdAFYy0QttU&list=PLOEM5PcngNJV3weFgkCI6_yYdaYEPjQqc) from Jeff Potts
* [Alfresco API documentation](https://www.alfresco.com/cmis/browser?id=workspace%3A//SpacesStore/b09d212a-00c6-4ec3-9764-0eca67bb8529) from the [Alfresco Developer Portal](https://www.alfresco.com/develop/cloud)

To access Alfresco in the cloud:

>
an Alfresco application uses the OAuth 2.0 authorization code flow to authenticate itself with Alfresco Cloud and to allow users to authorize the application to access data on their behalf.  
>

[oAuth](http://oauth.net) is an open protocol to allow secure authorization in a simple and standard method from web, mobile and desktop applications.  The [oAuth protocol flow](http://tools.ietf.org/html/rfc6749#section-1.2) starts with making an authorisation request through to receiving initial and refresh access tokens for using in sessions. 
  
![oauth-flow](/assets/img/ietf-oauth-flow.png?raw=true)  

In addition to the [Alfresco API documentation for the cloud](http://www.alfresco.com/cmis/browser?id=workspace%3A//SpacesStore/b09d212a-00c6-4ec3-9764-0eca67bb8529 and [Jeff Potts' video tutorials](https://www.youtube.com/watch?v=TdAFYy0QttU&list=PLOEM5PcngNJV3weFgkCI6_yYdaYEPjQqc) showing how to do this, [Jeff also highlights](http://forums.alfresco.com/forum/developer-discussions/alfresco-api/cloud-api-oauth-tokens-10202013-0243) on the developer forum Gethin Jame's [oAuth sample application](https://github.com/Alfresco/alfresco-oauth-sample) that demonstrates using the oAuth authentication protocol.  

To get an access token to use with CMIS Workbench, Allegria has used Gethin's oAuth sample application:

## Steps
1. Get the Alfresco oAuth application
1. Register for the Cloud api
1. Create an API key
1. Configure oAuth web app
1. Authorisation request
1. Access token request

### 1. Get the Alfresco oAuth application   
 
Gethin's Alfresco oAuth Sample Application (uses gradle and runs in jetty servlet engine and http server) is easily used with CMIS workbench, so [[fork|Paint-by-numbers:-GitHub]] his [alfresco-oauth-sample repository](https://github.com/Alfresco/alfresco-oauth-sample) and [[import|Paint-by-numbers:-Eclipse]] it to Eclipse eGit.  

The readme has simple instructions to get things running.  For now just need to : 
* Ensure you have an <a href="https://www.java.com/en/download/installed.jsp" target="_blank">up to date Java VM</a> installed and port 8181 is not in use  
* take note of the callback url `http://localhost:8181/oauthsample/mycallback.html` which will be used when registering the application with Alfresco in later steps  

### 2. Register for the Cloud api 

Need to follow a [registration process](https://www.alfresco.com/develop/cloud/signup) with Alfresco to obtain api access by following the steps on the [Alfresco developer portal](http://www.alfresco.com/develop) (click on the 'register for the cloud api' button):

![portal](/assets/img/Alfresco-developer-portal.png?raw=true)  

### 3. Create an API key

Register cmis-workbench on the Alfresco Developer site to to get authentication configuration details
 
![action](/assets/img/Alfresco-portal-manage-applications.png?raw=true)  

The application can be called anything, just needs to have a name so can get an 'API Key', so have called it 'cmis-workbench to make things easier.  
Edit the API Details and on the 'Auth' tab enter the callback url `http://localhost:8181/oauthsample/mycallback.html` (this comes from Gethin's repository readme):  

![action](/assets/img/Alfresco-portal-oAuth.png?raw=true)  

### 4. Configure oAuth web app

Follow the next next steps in Gethin's readme:
* Edit `src/main/webapp/config.js` and put in the client_id, client_secret and callback urls registered at The Alfresco Developer Portal (For this app, the redirect_uri should be `http://localhost:8181/oauthsample/mycallback.html`)  
* Run the Alfresco-oAuth-Sample application:
```
 # change to the folder holding the imported project  
 ./gradlew  jettyRun
```

  The first time it runs, the following output will appear:  

  ![oauth-flow](/assets/img/oAuth-sample-1st-run.png?raw=true)  

  After the initial build, each subsequent time will output:  

  ![oauth-flow](/assets/img/oAuth-sample-run.png?raw=true)  

### 5. Authorisation request 

In a web browser go to `http://localhost:8181/oauthsample` to see the first step in the oAuth protocol flow (authorisation request).      

![request](/assets/img/oAuth-1.png?raw=true)  

The values in this screen should come from the `config.js` file configured in the previous step so just hit submit.  

The authorisation screen from Alfresco Cloud will appear to allow entry of username and password that was set up when registered for api account:  

![auth-credentials](/assets/img/oAuth-1-1.png?raw=true)  

### 6. Access token request

Send the authorisation grant - nothing to do here but hit submit (the client secret will have come from `config.js` - it is blanked out here):  
  
![step2](/assets/img/oAuth-2.png?raw=true)  

Will get a response from the cloud with the access token:  

![step2-1](/assets/img/oAuth-3.png?raw=true)  

### Other oAuth resources:

* The [Alfresco API documentation for the cloud](http://www.alfresco.com/cmis/browser?id=workspace%3A//SpacesStore/b09d212a-00c6-4ec3-9764-0eca67bb8529) describes a number of tools:
  * [cURL](http://curl.haxx.se)
  * [RESTCLient]http://restclient.org)
* Jeff Potts uses [Google's Java oAuth2 client](https://code.google.com/p/google-oauth-java-client/) in his Alfresco cloud how-to [video tutorials](https://www.youtube.com/watch?v=TdAFYy0QttU&list=PLOEM5PcngNJV3weFgkCI6_yYdaYEPjQqc) and highlights Jared Ottley's [Spring Social plug-in](https://github.com/Alfresco/spring-social-alfresco) in the [developer forums](http://forums.alfresco.com/forum/developer-discussions/alfresco-api/cloud-api-oauth-tokens-10202013-0243)
* CPAN oAuth modules:  
  * Net::OAuth provides a low-level API for reading and writing OAuth messages (probably should start with Net::OAuth::Client).  Net::OAuth provides; classes that encapsulate OAuth messages (requests and responses),
message signing, message serialization and parsing, 2-legged requests (aka. tokenless requests, aka. consumer requests)
  * Net::OAuth::Simple - a simple wrapper round the OAuth protocol
  * OAuth::Simple - Simple OAuth authorization on your site
  * OAuth::Consumer - LWP based user agent with OAuth for consumer application
  * OAuth::Lite - OAuth framework (CONSUMER SIDE see OAuth::Lite::Consumer, SERVICE PROVIDER SIDE see OAuth::Lite::ServerUtil or to build server on mod_perl2, see OAuth::Lite::Server::mod_perl2.
  * OAuth::Lite::Util - utility for OAuth