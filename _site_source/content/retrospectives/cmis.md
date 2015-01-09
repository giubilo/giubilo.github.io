{
    "title": "CMIS",
    "description": "Understanding the CMIS standards.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "cmis" ],
    "status": "research"
}

_this page is not finished, see the [[wiki home|home]] to find out why..._ 

![logo](/assets/img/cmis11-types-uml.png?raw=true)  


![logo](/assets/img/cmis11-highlevel-uml.png?raw=true)  

http://docs.alfresco.com/4.2/index.jsp?topic=%2Fcom.alfresco.enterprise.doc%2Fpra%2F1%2Ftopics%2Fcmis-welcome.html

Alfresco CMIS information: http://www.alfresco.com/cmis

*********************

http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/pra/1/concepts/cmis-1.1-browser-binding.html
The Browser Binding

In addition to the existing XML-based AtomPub and Web services bindings, CMIS 1.1 provides a simpler JSON-based binding. The browser binding is designed for web applications and is easy to use just with HTML and JavaScript. It uses just two verbs, GET and POST, and resources are referenced using simple and predictable URLs.
You reference content in the repository by using the two URLs returned by the getRepositories or getRepositoryInfo service:
rootFolderUrl
repositoryUrl
Objects can then be referenced in two ways;
by their Id
<rootFolderUrl>?objectId=<objectId>
by their path
<rootFolderUrl>/<object path>
Content that is independent of a folder, for example a Type definition be accessed using the repositoryUrl service.
<repositoryUrl>?cmisselector=<selector>

*********************


## cmis 1.1 standard  

new cmis:item type - can use for config - types without content streams, secondary types...both really cool.new browser binding - preferred  

put in the pictures from the standard for objects, and create a picture that highlights the services...

basically create a really condensed version of the spec.

To use CMIS, you can either directly interact with one of the CMIS bindings or develop against a CMIS client API. Several APIs are "in development" for the following programming languages: [cient cmis api's](http://wiki.alfresco.com/wiki/CMIS#CMIS_Client_APIs)

[cmis wiki](http://wiki.alfresco.com/wiki/CMIS)

IBM CMIS
http://www-01.ibm.com/software/ecm/cmis.html

CMIS Poster Lab videos
https://www.youtube.com/watch?v=_koCqeYic1k



http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/pra/1/concepts/cmis-1.1-browser-binding-get.html
The URL to get all of the children of the root/test node in the repository looks like this:
http://localhost:8080/alfresco/api/-default-/public/cmis/versions/1.1/browser/root/test?cmisselector=children