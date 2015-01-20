{
    "title": "CMIS url",
    "description": "Urls alfresco uses for CMIS.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "alfresco", "cmis" ],
    "status": "research"
}

<html>
<table border="0">
<tr>
  <td>
    <p>
      <img src="./images/spaghetti-western.png?raw=true" alt="book">
    </p>
  </td>
  <td>
    <p>This spaghetti western applicable for:</p>
    <p><b>CMIS 1.1</b></p>
    <p><b>Alfresco 4.2</b></p>
  </td>
</tr>
</table> 
</html>

The url is where the rubber hits the road for cmis on Alfresco - a client will access a CMIS service endpoint described by a URL by either directly interacting with one of the CMIS bindings or against a CMIS client API.  It can be a little tricky to understand just which url is needed as there are many to choose from depending on:  
* what version of Alfresco is running  
* how the repository is deployed (i.e. on-premise, cloud, public)  
* which binding is being used (atompub, webservice, browser) and what version (1.0 or 1.1)  
* whether connecting using the OpenCMIS API or to services or service information.

Signs along the way to understanding what cmis url to use are in the following sections:
* on-premise model url
* cloud model url
* theory and practice
* other url styles
* other interesting url's

## on-premise model url

The [official documentation](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/pra/1/concepts/cmis-request-url-format-onpremise.html) for version 4.2 defines the request url for an on-premise repository using the bindings available in CMIS version 1.1 as:

**on-premise model url**: `{protocol}://{host}[:{port}]/{fixed ref}/{repository}/{api}/{versions/n}/{binding}/{cmis method}`  

|url part             |Description                             |Example value|
|---------------------|----------------------------------------|-------------|
|protocol|likely to be (or should be) https but is dependant on what is set up in the `alfresco-global.properties` [file](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/tasks/global-props-config.html)|`https`|
|host|ip address or hostname of the host|`localhost`|
|[port]|optional - usually 8080 but could be configured (usually in `alfresco-global.properties`)|`8080`|
|fixed ref|this is set to `alfresco/api` for the alfresco one on-premise api|`alfresco/api`|
|repository|this is sort of a pseudo fixed name for the repository (see further explanation in 'other url styles'  below)|`-default`|
|api|using the public cmis api (could use public/cmis or cmis here) but there are others including alfresco rest and workflow|`cmis`|
|versions/n|version using of [Content Management Interoperability Services (CMIS) specification](http://docs.oasis-open.org/cmis/CMIS/v1.1/CMIS-v1.1.pdf) currently either 1.0 or 1.1 (should use 1.1 if can, as get access to newer capabilities such as the browser binding and secondary object types)|`1.1`
|binding|atompub (atom), webservices (cmisws) or browser (browser) - use browser if can as it is the fullest and most lightweight|`browser`
|cmis method|from the specification, but won't need to use if interacting through a cmis client API such as Apache's OpenCMIS|

_resultant on-premise example url_: `https://localhost:8080/alfresco/api/-default-/cmis/versions/1.1/browser/`

## cloud model url

The [official documentation](http://docs.alfresco.com/4.2/index.jsp?topic=%2Fcom.alfresco.enterprise.doc%2Fpra%2F1%2Fconcepts%2Fcmis-get-service-document.html) for version 4.2 defines the request url for a cloud repository using the bindings available in CMIS version 1.1 as:

**cloud model url**: `{protocol}://{host}/{network id}/{api}/{versions/n}/{binding}/{cmis method}`

|url part             |Description                             |Example value|
|---------------------|----------------------------------------|-------------|
|protocol|will always be https |`https`|
|host|will always be api.alfresco.com|`api.alfresco.com`|
|network id|name of the company registered with alfresco|`yourcompany.com`|
|api|using the public cmis api (could use public/cmis or cmis here) but there are others including alfresco rest and workflow|`cmis`|
|versions/n|version using of [Content Management Interoperability Services (CMIS) specification](http://docs.oasis-open.org/cmis/CMIS/v1.1/CMIS-v1.1.pdf) currently either 1.0 or 1.1 (should use 1.1 as newer)|`1.1`
|binding|atompub (atom), webservices (cmisws) or browser (browser)|`atom`
|cmis method|from the specification, but won't need to use if interacting through a cmis client API such as Apache's OpenCMIS|

_resultant cloud example url_: `https://api.alfresco.com/yourcompany.com/cmis/versions/1.1/atom/`

## theory and practice

That's the theory...in practice using the model url in the CMIS Workbench, while it's [just right](www.imdb.com/title/tt0172505/‎
) for some, it doesn't necessarily work for all combinations:
* the on-premise atom binding with cmis version 1.1 will get a parsing error
* for on-premise, webservices won't work with this model so will need to use the CMIS Workbench template (see below)
* the browser binding is not available for the cloud version (even though running cmis version 1.1 and the documentation says it is)

## other url styles

There are also some other styles of url's out there in [documentation land](www.imdb.com/title/tt0069762/‎
), (adding to the confusion). Some still work with the 4.2 implementation of the api including:  
* The Alfresco [CMIS Wiki](http://wiki.alfresco.com/wiki/CMIS#CMIS_Index_Page) hasn't caught up yet (it's describing 4.1 and cmis 1.0 but the url's for the defined AtomPub `http://[host]:[port]/alfresco/cmisatom` and webservices `http://[host]:[port]/alfresco/cmisw` still work.
* The [Alfresco developer forum](http://forums.alfresco.com/forum/developer-discussions/alfresco-api/cmis-resources-tutorials-and-examples-03212012-1456) describes some great cmis information and an update to the atom url which works:  
    >
  please note that when you are using the CMIS ATOM Pub binding against Alfresco 4, you should use the new OpenCMIS-based URL (`http://localhost:8080/alfresco/cmisatom`) instead of the old web script-based URL (http://localhost:8080/alfresco/s/api/cmis). The old URL should be considered deprecated. This is not just a URL change - these are two different implementations, so you will see differences in how they behave
    >  
* The Apache Chemistry download for CMIS Workbench tool itself has connection templates that describe a range of url's that work:
  ```
  # Alfresco 4 AtomPub
  http://<host>/alfresco/cmisatom

  # Alfresco 4 Web Services
  http://<host>/alfresco/cmisws/RepositoryService?wsdl
  http://<host>/alfresco/cmisws/NavigationService?wsdl
  http://<host>/alfresco/cmisws/ObjectService?wsdl
  http://<host>/alfresco/cmisws/VersioningService?wsdl
  http://<host>/alfresco/cmisws/DiscoveryService?wsdl
  http://<host>/alfresco/cmisws/MultiFilingService?wsdl
  http://<host>/alfresco/cmisws/RelationshipService?wsdl
  http://<host>/alfresco/cmisws/ACLService?wsdl
  http://<host>/alfresco/cmisws/PolicyService?wsdl

  # Alfresco Cloud (CMIS 1.0 AtomPub)
  https://api.alfresco.com/cmis/versions/1.0/atom
  ```

* The CMIS specification allows a CMIS service endpoint to advertise one or more repositories.  This may be the thinking behind the `-default-`, part of the on-premise url - `https://localhost:8080/alfresco/api/-default-/cmis/versions/1.1/browser/`.  In CMIS Workbench when use the model url -default- appears in the repository list:  

  ![connection](./images/cmis-wb-repo-default.png?raw=true)  

  When use the CMIS Workbench template url `http://<host>/alfresco/cmisatom` then see the actual repository name in the list:  
  
  ![connection](.images/cmis-wb-repo-name.png?raw=true)  


Even though you can connect with these other url styles it is probably best to try and move to the model urls as this is driving towards a more consistent approach. 

## other interesting url's

* The Alfresco [CMIS Wiki](http://wiki.alfresco.com/wiki/CMIS#CMIS_Index_Page) describes the _CMIS Index Page_:
  >
  For any releases the [CMIS Index] page `http://[host]:[port]/alfresco/service/cmis/index.html` provides an overview of the Alfresco CMIS implementation, and links to all the resources you'll need to use the CMIS bindings.
  >  

  ![connection](/assets/img/cmis-index.png?raw=true)  

  This page has some useful information about cmis compliance of the running version and some tools including the OpenCMIS Browser and the Web Scripts CMIS Browser.  This would be an awesome page it it also listed the binding url's for connection - just saying - must put it on Allegria's things to do list.

* The Alfresco [Official Documentation for 4.2](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/pra/1/concepts/cmis-get-service-document.html) describes getting the cmis service document at:
  ```
  https://localhost:8080/alfresco/api/cmis/versions/1.1/atom/              #on-premise repository
  https://api.alfresco.com/cmis/versions/1.1/atom/                         #cloud repository (current authenticated network)
  https://api.alfresco.com/yourcompany.com/public/cmis/versions/1.1/atom   #specific cloud network
  ```
  Retrieving the service document using the HTTP GET method to one of those URL's will return a response body that is an AtomPub XML document which describes the CMIS capabilities in a standard way (see the CMIS specification for more details).  The service document contains information on the repository, the CMIS methods that can be called on it, and the parameters for those methods.  

  ![connection](/assets/img/cmis-service-document.png?raw=true)  

* The cxf service list url `http://[host]/alfresco/cmis` lists cmis services available with web services:  

  ![connection](/assets/img/cmis-cxf-service-url.png?raw=true)  