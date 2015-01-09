{
    "title": "Building a folder and document based protocol",
    "description": "tbd.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "cmis" ],
    "status": "research"
}

_this page is not finished, see the [wiki home page](../wiki) to find out why..._ 

MediaGate for Java
UPnP Stacks + a picture
Apache Felix + Alfresco development tool roadmap
OpenCMIS
Learning Java

http://docs.alfresco.com/4.1/index.jsp?topic=%2Fcom.alfresco.enterprise.doc%2Fconcepts%2Fprotocols-about.html  
http://www.videolan.org/vlc/streaming.html  
http://shop.oreilly.com/product/9781849511384.do  
http://www.upnp-database.info/listDevices.jsp?filterType=servers  



The Alfresco content application server supports many folder and document-based protocols to access and manage content held within the content repository using familiar client tools.
All the protocol bindings expose folders and documents held in the Alfresco content repository. This means a client tool accessing the repository using the protocol can navigate through folders, examine properties, and read content. Most protocols also permit updates, allowing a client tool to modify the folder structure, create and update documents, and write content. Some protocols also allow interaction with capabilities such as version histories, search, and tasks.

Internally, the protocol bindings interact with the content repository services, which encapsulate the behavior of working with folders and files. This ensures a consistent view and update approach across all client tools interacting with the Alfresco content application server.

An Alfresco subsystem for file servers allows configuration and lifecycle management for each of the protocols either through property files or JMX.

http://blogs.alfresco.com/wp/pmonks/category/alfresco/
https://github.com/peterwatts/allegria/wiki/1.2.1-Where's-streaming-heading%3F:-IN-PROGRESS
http://docs.oasis-open.org/cmis/CMIS/v1.1/CMIS-v1.1.html
http://wiki.alfresco.com/wiki/CMIS
https://forums.alfresco.com/forum/developer-discussions/alfresco-api/cmis-resources-tutorials-and-examples-03212012-1456
http://cmis.alfresco.com/cmis-cheatsheet.pdf
http://tech.wrighting.org/category/cmis/
http://wiki.alfresco.com/wiki/CMIS#Query_Language
http://wiki.alfresco.com/wiki/CMIS_Query_Language 
http://wiki.alfresco.com/wiki/Full_Text_Search_Query_Syntax
http://www.scribd.com/doc/18495354/CMIS-CMIS-SQL-Search-Tutorial-ENG
http://forums.alfresco.com/forum/developer-discussions/alfresco-api/using-cmis-get-list-document-urls-11302011-2029
https://forums.alfresco.com/forum/developer-discussions/web-scripts/cmis-query-get-path-cmisdocument-11302011-1630
https://forums.alfresco.com/forum/developer-discussions/web-scripts/searching-documents-using-cmis-query-folder-hierarchy
http://yonaweb.be/using_cmis_query_content_query_navigation_model
http://blogs.alfresco.com/wp/pmonks/category/alfresco/

(consider use of CMIS protocol and Apache Felix upnp-av tools, consider also if content is stored in the cloud how can get to it).

**joining cmis libraries / capabilities to dlna libraries / capabilities with a smart set of queries**


Regardless of the binding, there is a set of services that a CMIS repository must provide. These services include:
•	Repository Services: Used to discover information and capabilities of the repository. 
•	Navigation Services: Used to traverse the repository’s folder hierarchy. 
•	Object Services: Used to perform CRUD functions on objects. 
•	Multi-filing Services: If the repository supports putting an object in  more than one folder, this service handles it. 
•	Discovery Services: Used to handle queries. 
•	Versioning Services: Used to checkout documents and work with  document versions. 
•	Relationship Services: Used to query an object for its relationships. 
•	Policy Services: Used to apply, remove, and query for policies. 
•	ACL Services: Not supported by all repositories, this service is used  to return and manage the ACL of an object. 
Some of these services share common characteristics. For example:
• Almost every service that returns a list can be returned as a paged
result set.
• Services that return objects can often return additional information
about those objects, if you ask for it, like relationships, ACLs,
renditions, and allowable actions.
• A repository may choose to give you a change token with an object to
reduce the chance that you don’t update an out-of-date object. If a repository gives you a change token, it expects it back when you post the change.
• Any of the services may throw an exception. For a list, check the spec.

Repository Services
•	Get Repositories: Get a list of repositories that can be accessed from this service endpoint
•	Get Repository Info: Get information about the specified repository
•	Get Type Children, Get Type Descendants: Various ways to discover the object types in a repository
•	Get Type Definition: Get the definition (list of properties) of the specified type
Navigation Services
▪	Get Folder Tree, Get Descendants, Get Children: Retrieve descendant objects (each one has slightly different nuances)
▪	Get Folder Parent, Get Object Parents: Retrieve an object's parent folder(s)
▪	Get Checkedout Docs: Retrieve list of checked out documents
Discovery Services
▪	Query: Execute a CMIS query
▪	Get Content Changes: Gets a list of changes to the repository; the client can provide an optional change log token that specifies the first event to be included in the list.
Object Services
▪	Get Object, Get Object By Path: Retrieve objects
▪	Get Properties, Get Allowable Actions, Get Renditions: Get information about objects
▪	Get Content Stream: Retrieve an object's content stream
▪	Create Relationship, Create Document, Create Document From Source, Create Policy, Create Folder: Create objects
▪	Update Properties, Move Object: Update objects
▪	Delete Object, Delete Tree: Remove objects
▪	Set Content Stream, Delete Content Stream: Update content streams
Versioning Services
▪	Get Properties Of Latest Version, Get Object Of Latest Version: Get information about latest version of object
▪	Get All Versions: Retrieve an object's version history
▪	Check Out, Check In, Cancel Check Out: Control locking/unlocking of an object for the purpose of updating
▪	Delete All Versions: Remove version history
Relationship Services
▪	Get Object Relationships: Get the relationships associated with an object
Multi-Filing Services
▪	Add Object To Folder, Remove Object From Folder: File and un-file objects;
▪	If multi-filing is supported in the repository, then an object can be added to multiple folders
▪	If un-filing is supported in the repository, then an object can be removed from all folders that it is filed in without deleting the object
ACL Services
▪	Get ACL: Get the permissions associated with an object
▪	Apply ACL: Set the permissions associated with an object
Policy Services
▪	Get Applied Policies: Get the policies that are applied to an object
Apply Policy, Remove Policy: Apply and remove policies to/from an object

CMIS Query	What it does
SELECT cmis:name FROM sc:whitepaper where contains(‘sample’)	Select the name of every whitepaper with “sample” somewhere in their text.
SELECT cmis:name, Score() as relevance FROM sc:whitepaper where contains('sample') order by relevance DESC	Select the name of whitepapers with “sample” somewhere in their text, ordered by full-text relevance, descending.
SELECT cmis:name from sc:whitepaper where sc:isActive = true
	Select whitepapers with the isActive flag set to true (which happens to be a property defined by an aspect).

	
SELECT cmis:name from sc:whitepaper where not(sc:isActive = true)	Select whitepapers with the isActive flag not set to true. This will return whitepapers where the property is not true as well as whitepapers where the property is unset.
   
SELECT cmis:name from sc:marketingDoc where any sc:campaign in ('Social Shopping')	Select instances of Marketing Documents and their children where the multi-value property, sc:campaign, contains the value “Social Shopping” (note that Whitepaper is a child type of Marketing Document).
SELECT cmis:name,sc:published from sc:whitepaper where sc:published >= '2009-11-10T00:00:00.000-06:00' and sc:published < '2009-11- 18T00:00:00.000-06:00'	Select whitepapers published (sc:published, a property of the sc:webable aspect) on or after November 10, 2009 and before 18, 2009.
SELECT cmis:name from cmis:document where in_folder('workspace://SpacesStore/393 5ce21-9f6f-4d46-9e22-4f97e1d5d9d8') and contains('contract')	Select all content in the Sales folder containing the word “contract”.
   
SELECT cmis:name from cmis:document where in_tree('workspace://SpacesStore/3935c e21-9f6f-4d46-9e22-4f97e1d5d9d8') and contains('contract') and cm:description like “%sign%”	Select all content in the Sales folder or any of its descendant folders containing the word “contract” and a description like “%sign%”.



The DLNA Certified Device Classes are separated as follows:[9]
Home Network Devices[edit source | editbeta]
•	Digital Media Server (DMS): store content and make it available to networked digital media players (DMP) and digital media renderers (DMR). Examples include PCs and network-attached storage(NAS) devices.
•	Digital Media Player (DMP): find content on digital media servers (DMS) and provide playback and rendering capabilities. Examples include TVs, stereos and home theaters, wireless monitors and game consoles.
•	Digital Media Renderer (DMR): play content as instructed by a digital media controller (DMC), which will find content from a digital media server (DMS). Examples include TVs, audio/video receivers, video displays and remote speakers for music. It is possible for a single device (e.g. TV, A/V receiver, etc.) to function both as a DMR (receives "pushed" content from DMS) and DMP ("pulls" content from DMS)
•	Digital Media Controller (DMC): find content on digital media servers (DMS) and instruct digital media renderers (DMR) to play the content. Content doesn't stream from or through the DMC. Examples include Internet tablets, Wi-Fi enabled digital cameras and smartphones.
•	Digital Media Printer (DMPr): provide printing services to the DLNA home network. Generally, digital media players (DMP) and digital media controllers (DMC) with print capability can print to DMPr. Examples include networked photo printers and networked all-in-one printers
Mobile Handheld Devices[edit source | editbeta]
▪	Mobile Digital Media Server (M-DMS): store content and make it available to wired/wireless networked mobile digital media players (M-DMP), digital media renderers (DMR) and digital media printers (DMPr). Examples include mobile phones and portable music players.
▪	Mobile Digital Media Player (M-DMP): find and play content on a digital media server (DMS) or mobile digital media server (M-DMS). Examples include mobile phones and mobile media tablets designed for viewing multimedia content.
▪	Mobile Digital Media Uploader (M-DMU): send (upload) content to a digital media server (DMS) or mobile digital media server (M-DMS). Examples include digital cameras and mobile phones.
▪	Mobile Digital Media Downloader (M-DMD): find and store (download) content from a digital media server (DMS) or mobile digital media server (M-DMS). Examples include portable music players and mobile phones.
▪	Mobile Digital Media Controller (M-DMC): find content on a digital media server (DMS) or mobile digital media server (M-DMS) and send it to digital media renderers (DMR). Examples include personal digital assistants (PDAs) and mobile phones.
Home Infrastructure Devices[edit source | editbeta]
▪	Mobile Network Connectivity Function (M-NCF): provide a bridge between mobile handheld device network connectivity and home network connectivity.
▪	Media Interoperability Unit (MIU): provide content transformation between required media formats for home network and mobile handheld devices.
The specification uses Digital Transmission Content Protection|DTCP-IP as "link protection" for copyright-protected commercial content between one device to another.[1][10]

Durable storage (glacier), resilient storage.
Commercial Content Management -> Consumer Content Management <-Consumer media management.
UPnP Design by Example, by Michael Jeronimo and Jack Weast
UPnP Media Server implements the;
-	Content Directory Service - provides a logical structure for the media library available in the Server
-	Connection Manager Service

Most AV scenarios involve the flow of (entertainment) content (i.e. a movie, song, picture, etc.) from one device to another. As shown in Figure 2, an AV control point interacts with two or more UPnP devices acting as source and sink, respectively. Although the control point coordinates and synchronizes the behavior of both devices, the devices themselves interact with each other using a non-UPnP (“out-of- band”) communication protocol. The control point uses UPnP to initialize and configure both devices so that the desired content is transferred from one device to the other. However, since the content is transferred using an “out-of-band” transfer protocol, the control point is not directly involved in the actual transfer of the content. The control point configures the devices as needed, triggers the flow of content, then gets out of the way. Thus, after the transfer has begun, the control point can be disconnected without disrupting the flow of content. In other words, the core task (i.e. transferring the content) continues to function even without the control point present.

A MediaServer’s primary purpose is to allow control points to enumerate (i.e. browse or search for) content items that are available for the user to render. The MediaServer contains a ContentDirectory Service [CDS], a ConnectionManager Service [CM], and an optional AVTransport Service [AVT] (depending on the supported transfer protocols).
Some MediaServers are capable of transferring multiple content items at the same time, e.g. a hard-disk- based audio jukebox may be able to simultaneously stream multiple audio files to the network. In order to support this type of MediaServer, the ConnectionManager assigns a unique Connection ID to each “connection” (i.e. each stream) that is made. This ConnectionID allows a third-party control points to obtain information about active connections of the MediaServer.
3.1.1. Content Directory Service
This service provides a set of actions that allow the control point to enumerate the content that the Server can provide to the home network. The primary action of this service is ContentDirectory::Browse(). This action allows control points to obtain detailed information about each Content Item that the Server can provide. This information (i.e. meta-data) includes properties such as its name, artist, date created, size, etc. Additionally, the returned meta-data identifies the transfer protocols and data formats that are supported by the Server for that particular Content Item. The control point uses this information to determine if a given MediaRenderer is capable of rendering that content in its available format.
3.1.2. ConnectionManager Service
This service is used to manage the connections associated with a particular device. The primary action of this service (within the context of a MediaServer) is ConnectionManager::PrepareForConnection(). When implemented, this optional action is invoked by the control point to give the Server an opportunity to prepare itself for an upcoming transfer. Depending on the specified transfer protocol and data format, this action may return the InstanceID of an AVTransport service that the control point can use to control the flow of this content (e.g. Stop, Pause, Seek, etc). As described below, this InstanceID is used to distinguish multiple (virtual) instances of the AVTransport service, each of which is associated with a particular connection to Renderer. Multiple (virtual) instances of the AVTransport service allow the MediaServer to support multiple Renderers at the same time. When the control point wants to terminate this connection, it should invoke the MediaServer’s ConnectionManager::ConnectionComplete() action (if implemented) to release the connection.
If the ConnectionManager::PrepareForConnection() action is not implemented, the control point is only able to support a single Renderer at an given time. In this case, the control point should use InstanceID=0.
3.1.3. AVTransport Service
This (optional) service is used by the control point to control the “playback” of the content that is associated with the specified AVTransport. This includes the ability to Stop, Pause, Seek, etc. Depending on the supported transfer protocols and/or data formats, a MediaServer may or may not implement this service. If supported, the MediaServer can distinguish between multiple instances of the service by using the InstanceID that is included in each AVTransport action. New instances of the AVTransport service are created via the ConnectionManager’s ConnectionManager::PrepareForConnection() action. A new Instance Id is allocated for each new Service Instance.