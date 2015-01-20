{
    "title": "CMIS Workbench",
    "description": "Using CMIS Workbench to manage cmis repositories.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "cmis" ],
    "status": "research"
}

<html>
<table border="0">
<tr>
  <td>
    <p>
      <img src="./images/paint-by-numbers.png?raw=true" alt="book">
    </p>
  </td>
  <td>
    <p>This paint by numbers has used:</p>
    <p><b>Alfresco 4.2</b></p>
    <p><b>CMIS Workbench 0.9.0-beta-1 & 0.10.0</b></p>
  </td>
</tr>
</table> 
</html> 

The [CMIS Workbench](http://chemistry.apache.org/java/developing/tools/dev-tools-workbench.html) is a desktop (osx, win, linux) repository browser and development tool for working with the OpenCMIS client API (there's an [introductory video](http://chemistry.apache.org/java/developing/tools/dev-tools-workbench.html) that provides a simple overview).  

Things it's being used on Allegria for include:
* quickly prototyping and checking content types and properties
* working out syntax for cmis queries
* running quick scripts for changing objects in the repositories
  
The OpenCMIS API it uses, is an open source implementation of the [Content Management Interoperability Services (CMIS) specification](http://docs.oasis-open.org/cmis/CMIS/v1.1/CMIS-v1.1.pdf) provided by the [Apache Chemistry project](http://chemistry.apache.org "target=_blank").  The CMIS Workbench is also one of the tools from the apache project:  

![logo](/assets/img/chemistry_tm_logo_small.png?raw=true)  
![img](/assets/img/apache-chemistry.png?raw=true)    

Alfresco being a cmis-compliant rich content repository, means that it provides a set of [[services for working with objects|Helicopter view: CMIS]] defined by the specification (which are then wrapped in the OpenCMIS implementation that a client like the CMIS Workbench can use).  With CMIS, most capabilities of the Alfresco repository are accessible and for the rest there are [[other interfaces|Helicopter view: Alfresco integration]] available.

Florian Muller, Jay Brown and Jeff Potts have written [CMIS and Apache Chemistry in Action](http://www.manning.com/mueller), which they describe as a hands on experience with the [cmis] standard and with the Apache Chemistry libraries and tools [including CMIS Workbench].  In a very similar vein to Allegria, the focus of the book is on:
>
getting a good general understanding of CMIS, enough to build a useful (and we hope fun) application  
>

This paint-by-numbers is not to redo the work inside their book but does summarise some of the key aspects of the CMIS Workbench, in particular using it with an Alfresco repository. 

## Steps

1. Get CMIS Workbench
1. Connecting the workbench to repositories
1. Browsing objects in the repository
1. Querying the repository
1. CMIS Types
1. The groovy console
1. Advanced features

### 1. Get CMIS Workbench

The CMIS Workbench can be [downloaded](http://www.apache.org/dyn/closer.cgi/chemistry/opencmis/0.10.0/chemistry-opencmis-workbench-0.10.0-full.zip) as a zip from the [Apache Chemistry project](http://chemistry.apache.org). 

Florian Muller has also created a [GitHub Repository](https://github.com/fmui/ApacheChemistryInAction) for readers of [CMIS and Apache Chemistry in Action](http://www.manning.com/mueller) which contains; a zip of the CMIS Workbench, an in-memory cmis compliant repository (another one of the apache project's tools) and the source code for each chapter's examples.  To use the ApacheChemistryInAction GitHub repository, fork it and import it to Eclipse eGit as per the paint-by-numbers directions for [[GitHub|Paint by numbers: GitHub]]![icon](/assets/img/paint-by-numbers-10.png?raw=true) and the ones for [[Eclipse|Paint by numbers: Eclipse]]![icon](/assets/img/paint-by-numbers-10.png?raw=true).

Unzip the chemistry-opencmis-workbench-0.10.0-full.zip.  Using a linux or osx terminal type:
```
cd [directory where extracted workbench to]
./workbench.sh
```

**Note:** the workbench.sh file from Florian's GitHub repo is tailored to use the apache in-memory repository.  To use the CMIS Workbench with Alfresco it is better to also get the one from the ApacheProject (so rename Florian's to something like `workbench.in-memory.sh`).

To have a neater installation and run it from the osx launchpad or dock follow this [[paint-by-numbers|Paint by numbers: Launching osx scripts]]![icon](/assets/img/paint-by-numbers-10.png?raw=true).  

### 2. Connecting the workbench

The connection window will appear either when starting the application or using the 'Connection' menu button:  
  
![connection](./images/cmis workbench on-premise connection.png?raw=true)  

The three key items needed to make a connection to a repository host are:
* **BINDING** - the bindings (atompub, webservice, browser) are explained in detail in the cmis specification (the 'browser' binding is the fullest and most lightweight implementation but not always available). 

* **URL** - the url is where the rubber hits the road for cmis on Alfresco, however it is a little tricky to understand just which url is needed as there are many to choose from depending on; what version of Alfresco is running, how the repository is deployed (i.e. on-premise, cloud, public), which binding is being used (atompub, webservice, browser) and whether connecting to the OpenCMIS API or to services or service information.  To keep this step readable the unravelling of this is in [[Spaghetti western: CMIS URL|Spaghetti western: CMIS URL]]![icon](/assets/img/spaghetti-western-10.png?raw=true) (although the examples below have the answers anyway).  

* **AUTHENTICATION CREDENTIALS / METHOD** - just like the url, we are spoilt for choice on what authentication methods and credentials may be used, and there is a proliferation of documentation to go along with that.  To keep things simple going to use the standard, non-https, user name and password for connecting to Alfresco on-premise and when connecting to Alfresco in the cloud, use the required oAuth implementation (how to do this is in the examples below). 

The 'basic' tab provides, well, basic input boxes for these key parameters plus some performance tuning parameters (which [CMIS and Apache Chemistry in Action](http://www.manning.com/mueller) explains in Part 3 - advanced topics).  The 'expert' tab allows an expanded syntax of [OpenCMIS session parameters](http://chemistry.apache.org/java/0.9.0/maven/apidocs/org/apache/chemistry/opencmis/commons/SessionParameter.html) to fine tune the [values](http://chemistry.apache.org/java/0.9.0/maven/apidocs/constant-values.html#org.apache) that can be used.  The expert tab has a drop down of some preset connection parameters (such as Alfresco) to make things easier.

So, to connect to an Alfresco 4.2e, on-premise repository with the OpenCMIS browser binding use the following parameters:

```
org.apache.chemistry.opencmis.binding.spi.type=browser
org.apache.chemistry.opencmis.binding.browser.url=http://[host]/alfresco/cmisbrowser
org.apache.chemistry.opencmis.user=<user>
org.apache.chemistry.opencmis.password=<password>
org.apache.chemistry.opencmis.binding.compression=true
org.apache.chemistry.opencmis.binding.cookies=true
```

Given only simple parameters were chosen in the on-premise example above, they could have also been entered in the basic tab for the same result.  Connecting to the Alfresco in the cloud repository requires the use of the expert tab though as it uses parameter values that cannot be set on the basic tab.

The example syntax below was generated by selecting 'Alfresco Cloud AtomPub' from the parameter template drop down list at the top of the expert tab (at present it doesn't seem like the browser binding is available in the cloud repository). The value for the oAuth access token is obtained from an oAuth authentication flow which is described in [[Paint by numbers: Alfresco oAuth sample application|Paint by numbers: Alfresco oAuth sample application]]![icon](./images/paint-by-numbers-10.png?raw=true):   

```
# Alfresco Cloud (CMIS 1.0 AtomPub)
org.apache.chemistry.opencmis.binding.spi.type=atompub
org.apache.chemistry.opencmis.binding.atompub.url=https://api.alfresco.com/cmis/versions/1.0/atom
org.apache.chemistry.opencmis.binding.auth.http.basic=false

# Please provide a valid OAuth access token in the following property
# Note that Alfresco Cloud access tokens have a limited lifetime (currently 1 hour) and the OpenCMIS Workbench does not auto-refresh the access token when it expires
org.apache.chemistry.opencmis.binding.header.0=Authorization:Bearer ####ACCESS_TOKEN####

# Other optional options - compression etc. - may be provided here
```

Once all the relevant parameters are entered, pressing the 'load repositories' button, presents a choice of instances on the host (as can run multiples), choose a repository from the drop down, press the login button and [voila!](http://www.imdb.com/title/tt2379418/) you are into the default configuration of the CMIS Workbench user interface.

The CMIS Workbench can also be configured through [system properties or additional properties](http://chemistry.apache.org/java/developing/tools/dev-tools-workbench.html) in the expert login dialog. An [Alfresco forum post](http://forums.alfresco.com/comment/75223#comment-75223) explains this as:  

>
The CMIS Workbench, for example, makes use of the OperationContext. It sets up two OperationContext objects when it starts:  
* One OperationContext object is used for the folder list on left. This OperationContext only selects the data that is needed for this view: a handful of properties, no Allowable Actions, no ACLs, etc. That [as with paging] speeds up the retrieval of the list.  
* The second OperationContext is used to populate the right hand panels. It selects everything because it displays everything.  
>  

The current values for the OperationContexts can be seen if press the Info button.  The notion of OperationContext is explained more fully in [CMIS and Apache Chemistry in Action](http://www.manning.com/mueller) and the [Apache OpenCMIS API docs](http://chemistry.apache.org/java/developing/guide.html).

Once connected the features of the tool are available.

### 3. Browsing objects in the repository

Browse the repository's objects, actions, properties, relationships, ACL, policies, versions, types and extensions: 
 
![browse](/assets/img/cmis-workbench-main.png?raw=true)  

### 4. Querying the repository

The CMIS query syntax is defined in detail in:  
* 2.1.14 Query of [Content Management Interoperability Services (CMIS) specification](http://docs.oasis-open.org/cmis/CMIS/v1.1/CMIS-v1.1.pdf)
* [Alfresco wiki](http://wiki.alfresco.com/wiki/CMIS_Query_Language)
* Chapter 5 - Query of [CMIS and Apache Chemistry in Action](http://www.manning.com/mueller)
 
![query](/assets/img/cmis-workbench-query.png?raw=true)  

### 5. CMIS Types

The type function exposes the content model through the workbench:
  
![type](/assets/img/cmis-workbench-type.png?raw=true)  

The ability to create and update types allows programatic deployment of a content model eliminating the need for custom configuration scripts for the various repositories to configure types.  

Chapter 4 - CMIS metadata: types and properties of [CMIS and Apache Chemistry in Action](http://www.manning.com/mueller) describes how:

>
OpenCMIS provides the TypeUtils class, which can read and write type definitions from and to XML and JSON.
>

### 6. The groovy console

The groovy console provides a quick and easy development environment to use the [Apache Chemistry OpenCMIS API](http://chemistry.apache.org/java/0.9.0/maven/apidocs/overview-summary.html):
 
![groovy](/assets/img/cmis-workbench-groovy.png?raw=true)  

In addition to the default API, [CMIS and Apache Chemistry in Action](http://www.manning.com/mueller) highlights two other API's that can be accessed from the Groovy console:

_Chapter 3: Part 3 Advanced Topics - low-level api_
>
The APIs provide an object-oriented interface with a lot of convenience, simplified data structures, and high-level operations that don’t exist in CMIS. On the other hand, these APIs hide extension points and access to the data structures that are transferred over the wire.  
It turns out that there’s a layer between the bindings and these APIs called the low- level API. The low-level API provides a set of interfaces and operations that model all the services and operations in the CMIS specification one-to-one. For each of the nine CMIS services, there’s an interface. For each operation, there’s a method with exactly the same name and the same parameters, in the same order. The data objects are very close to the data structures used on the wire. The semantics and behavior are as described in the CMIS domain model. You can use the CMIS specification as a manual for these interfaces.
>

_Chapter 3: Creating, updating, and deleting objects with CMIS - groovy helper scripts_
>
CMIS helper scripts distributed with the CMIS Workbench can make your Groovy code more succinct. What other shortcuts are available? If you take a look at the source code for the CMIS Workbench, you’ll find the Groovy file that defines the CMIS helper scripts in /src/main/resources/scripts/CMIS.groovy. Consult that file for the full list.
>

The Florian Muller GitHub Repository workbench version ships with chapter scripts which can be accessed when use the Console button.  The apache project's version ships with other scripts that can be accessed from the Console button of that version.

**Note:** if get the unauthorised error when accessing the cloud repository then the token has probably timed out - need to close the groovy console, regenerate an access token, reconnect with the new token and reopen the console.

For information on groovy:
* [Groovy home](http://groovy.codehaus.org)
* [documentation](http://groovy.codehaus.org/Documentation) including getting started and tutorials
* [Gradle](http://www.gradle.org) build system for groovy

Some books on Groovy and CMIS (with source code):

<html>
<table border="0">
<tr>
  <td>
    <p><a href="http://www.manning.com/mueller" target="_blank">
      <img src="./images/manning-cmis.png?raw=true" alt="book"></a>
    </p>
  </td>
  <td>
    <p><a href="http://www.manning.com/koenig2" target="_blank">
      <img src="./images/manning-groovy.png?raw=true" alt="book"></a>
    </p>
  </td>
  <td>
    <p><a href="http://www.packtpub.com/develop-applications-and-integrations-that-can-interact-with-cmis-alfresco/book" target="_blank">
      <img src="./images/pakt-cmis.png?raw=true" alt="book"></a>
    </p>
  </td>
  <td>
    <p><a href="http://www.packtpub.com/groovy-2-cookbook/book" target="_blank">
      <img src="./images/pakt-groovy.png?raw=true" alt="book"></a>
    </p>
  </td>
</tr>
</table> 
</html> 


### 7. Advanced features

Other features of CMIS Workbench are:  
* Repository info
* [Change Logger](http://wiki.alfresco.com/wiki/CMIS#Change_Log)
* TCK (Test Compatibility Kit)
* CMIS Client Logging (filtered logging)