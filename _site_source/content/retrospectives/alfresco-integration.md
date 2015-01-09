{
    "title": "Alfresco Integration",
    "description": "Alfresco apis available for integration.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "alfresco", "integration" ],
    "status": "research"
}

_this page is not finished, see the [wiki home page](../wiki) to find out why..._ 

caching content stores, syncing content stores, s3 content stores...this detail is from the 2013 summit press - http://summit.alfresco.com/boston/sessions/getting-started-alfresco-development

include Alfresco Rumours XMPP.

alfresco embedded api
http://docs.alfresco.com/4.2/index.jsp?topic=%2Fcom.alfresco.enterprise.doc%2Fconcepts%2Fprotocols-about.html

cmis protocols
http://docs.alfresco.com/4.2/index.jsp?topic=%2Fcom.alfresco.enterprise.doc%2Fconcepts%2Fprotocols-about.html

[Alfresco api documentation](https://www.alfresco.com/cmis/browser?id=workspace%3A//SpacesStore/b09d212a-00c6-4ec3-9764-0eca67bb8529)![img](/assets/img/wiki-ext-link.jpg?raw=true)

> 
"The Alfresco API lets you access content managed by Alfresco Cloud from your own applications. The API is RESTful, which means each call is an HTTP request, so you don't even need a programming language to try it out. You can just type a URL address in a web browser. It consists of two parts, the standard CMIS API, which lets you manage and access content, and the new Alfresco REST API which lets you manage Alfresco's additional features such as ratings and comments, that are not covered by the CMIS standard."
> 

Integration options: http://docs.alfresco.com/4.2/index.jsp?topic=%2Fcom.alfresco.enterprise.doc%2Fconcepts%2Fintegration-options.html

* CMIS (Content Management Interoperability Services)
* Web scripts (RESTful api)
* File-based access (CIFS, WebDAV, NFS, or FTP)
* OpenSearch and feeds (RSS or Atom subscription protocols)
* Java applications (using the core API directly)
* PHP applications (through CMIS, through web scripts as a RESTful interface, or directly from the same application server as Alfresco. Alfresco has an optional extension that includes the Quercus PHP interpreter in a Tomcat server. The Quercus PHP interpreter is capable of running popular PHP applications, such as Joomla!, Drupal, WordPress, and MediaWiki.)
* .NET applications (similar to integrations with Java applications through remote interfaces such as web scripts or CMIS. Either the SOAP or Atom Publishing interfaces can be used.)
Integration patterns: http://docs.alfresco.com/4.2/index.jsp?topic=%2Fcom.alfresco.enterprise.doc%2Fconcepts%2Fintegration-options.html
* Surf components
* Authentication and directory services


