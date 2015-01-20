_this page is not finished, see the [wiki home page](../wiki) to find out why..._ 

Project Allegria Objective #1: help organise all the electronic stuff in the home

Project Allegria Objective #2: build some cool Enterprise Content Management skills and give information to help others also build skills

Project Allegria Objective #3: build skills in effective open source project management.


* [Concepts](#Concepts)  
* [How To's](#HowTo)  
* [Paint by Numbers](#PaintByNumbers)  
* [Helicopter Views](#HelicopterView)  
* [Spaghetti Westerns](#SpaghettiWestern)  
* [Point of Views](#PointOfViews)  

Because writing takes time - was it Edison who said creativity is 1% inspiration and 99% perspiration - and technology moves at an ever increasing pace - pages in the wiki are being made visible as they are developed (Manning Press do something similar with their [MEAP](http://www.manning.com/about/meap.html)). So **in many cases you will see the work as it is being developed - warts and all** - could be a few random thoughts, or some structure, or some copy and paste of some information that looked interesting and would provoke thought. You will be watching the creative writing process and hopefully collaborating with it as it happens. 

The following status descriptions, attached to each wiki page, will give you an idea as to where the page is on the creative writing process:

|Status Code        |Description                                    |
|-------------------|-----------------------------------------------|
|TO-START |There is nothing to see yet, the page is just a placeholder for some future content |
|RESEARCH |Just a cut and paste of possibly relevant text from the internet or brain-dump ideas |
|EDIT |Starting to shape and organise the research material |
|READABLE |An initial draft of information, should be able to read all the way through |


<a name="Concepts"></a>  
##![Concepts](./images/paint-by-numbers-50.png?raw=true) Concepts  

Building a full platform for Consumer Content Management is a big job and doing it in an open source project (read: in spare time) could take forever.

To get things moving - and get some early successes to keep the momentum rolling - the elephant has been broken down into some interesting bite sized pieces that build on each other.  As get success with each one and [learn](#HowTo) more about what Allegria looks like this list will change.  Eventually should have enough things in the bag to move far enough along the [roadmap](http://peterwatts.github.io/allegria/) to get some funding to industrialise the project.


 as follows:

|Reference           |Description                                    |Status                  |
|--------------------|-----------------------------------------------|------------------------|
|[[aaContentModel|Concept: aaContentModel]] |Modify Alfresco repository content / meta types to support consumer content types like movies, music, photos etc.| EDIT |
|[[CmisDlnaConnector|Concept: CmisDlnaConnector]] |Allow MediaControllers and MediaRenderers to consume content stored in the Alfresco Repository.| EDIT  |
|CapTag |Capture and tagging of content (consider implementing the best bits of Ember Media Manager and Media Monkey applications using Alfresco Share / Workdesk or Spring for the user interface and Alfresco Activiti and Tikka for workflows / meta data extraction). | TO-START |  
|PlayList |Modify Alfresco content / meta model to support playlist type functionality (consider how to support using playlists to use internet streams).| TO-START |
|FacetedSearch |Extend Alfresco search interface to provide basic faceted search functionality i.e. to categorise search results into primary types like movie, song, photo etc or even collections like album and include relevance and social context.| TO-START |
|Linkages |Work out how to build linkages between content e.g. recipe, recipe email tips and recipe demonstration video. Provide example for how to do some common linkages.| TO-START |
|Deployment |Evaluate different models of physically implementing the Alfresco Repository (such as on a NAS appliance or in the cloud and produce guidance for backup).| TO-START |
|TagSync |Build basic photo browser functionality to allow building up of tags on photos (consider leveraging existing tools that can write tags and then a sync done to Alfresco repository).| TO-START |
|NavPlus |Further extend the search interface to bring up the 'related' / 'more from' and allow navigation.| TO-START |
|SocialConnector |Provide a connector to allow choice and publishing of content to social sites e.g. a photo to a photo sharing site. This provides, controlled and monitored sharing. | TO-START |
|NavPlus2 |Further extend the search interface to build contextual photo browser that allows overlays to be applied to photo navigation e.g. a family tree based on people tagged to photos, or world map based on location tags, or a date line.| TO-START |
|BamCam |Further extend the workflow / activity monitoring to provide analytics such as 'amount watched', 'peak days', 'edit effort', 'common searches'.| TO-START |
|BamCamPlus |Further extend the workflow / activity monitoring to provide integrations with household calendars. | TO-START | 
|BamCamPlus2 |Further extend the workflow / activity monitoring with Activiti to build 'Internet of Things' automation examples like temperature monitoring and garden watering.| TO-START |

<a name="HowTo"></a> 
##![HowTo](./images/paint-by-numbers-50.png?raw=true) How To's  

The how-to's aren't designed to be a collection of highly polished specs or dictate a single way to do things.  They are really more of a collection of tips from internet research and lessons learned from creating the concepts.  The hope is that by grouping together a number of bits of research and explaining something a bit more than the original blog, it will make it dead simple to understand and replicate:

|Reference           |Description                                    |Status                  |
|--------------------|-----------------------------------------------|------------------------|
|[[setting up project resources|HowTo: setting up project resources]] | |READABLE |  
|[[modifying content-types|HowTo: modifying content types]] | |EARLY-EDIT |  
|[[building a folder and document-based protocols|HowTo:-building-a-folder-and-document-based-protocol]]. | |RESEARCH |  
|[[Development LifeCycle|HowTo: Development Lifecycle]] | |RESEARCH |  
|[[Project Management|HowTo: Project Management]] | |RESEARCH |  
|deploying alfresco in a mixed cloud mode / peer backup. | |TO-START |  
|working with automated metadata | |TO_START |  
|implementing playlists | |TO-START |  
|building cool search and navigation interfaces | hopefully with spring (surf?). |TO-START |
|content sensitive security models. | |TO-START |
|using advanced case management capabilities | hopefully using Activiti. |TO-START |

<a name="PaintByNumbers"></a>  
##![Paint](./images/paint-by-numbers-50.png?raw=true) Paint by Numbers  

The Paint by Numbers pages provide step-by-step instructions for a particular concept, usually in support of a how-to:  

|Reference           |Description                                    |Status                  |
|--------------------|-----------------------------------------------|------------------------|
|[[Alfresco oAuth|Paint by numbers: Alfresco oAuth sample application]]| To get an access token using Gethin's oAuth sample application for CMIS Workbench to login to Allegria in the cloud. |READABLE |
|[[CMIS Workbench|Paint by numbers: CMIS Workbench]] |Using the CMIS Workbench to browse and manipulate Alfresco using the OpenCMIS client API.  |READABLE |
|[[Eclipse|Paint by numbers: Eclipse]] |Setup and use the Eclipse Integrated Development Environment. |READABLE |
|[[GitHub|Paint by numbers: GitHub]] |Setup GitHub for use as distributed code version control, application build and a module and documentation repository.  |READABLE |
|[[Java|Paint by numbers: Java]] |Using Java for development. |RESEARCH |
|[[Launching osx scripts|Paint by numbers: Launching osx scripts]] |Example to run the CMIS Workbench script from the osx dock. |READABLE |
|[[Perl|Paint by numbers: Perl]] |Using Perl for development. |READABLE |

<a name="HelicopterView"></a>  
##![HelicopterView](./images/paint-by-numbers-50.png?raw=true) Helicopter Views  

Sometimes a topic is just too big for [mere mortals](www.imdb.com/title/tt1981115/‎) to understand.  An overview from 10,000ft up can sometime help with taking the whole thing in before getting down into the detail (sometimes a picture on a page is helpful):

|Reference           |Description                                    |Status                  |
|--------------------|-----------------------------------------------|------------------------|
|[[Alfresco Integration|Helicopter view: Alfresco Integration]] |Technical architecture for integrating with Alfresco. |RESEARCH |  
|[[CMIS|Helicopter view: CMIS]] |Content Management Interoperability Services (CMIS) is an open standard that allows different content management systems to inter-operate over the Internet. |RESEARCH    
|[[UPnP|Helicopter view: UPnP]] | Universal Plug and Play (UPnP) is a set of networking protocols that permits networked devices, such as personal computers, printers, Internet gateways, Wi-Fi access points and mobile devices to seamlessly discover each other's presence on the network and establish functional network services for data sharing, communications, and entertainment.  |TO-START |    

<a name="SpaghettiWestern"></a>  
##![SpaghettiWestern](./images/spaghetti-western-50.png?raw=true) Spaghetti Westerns (a.k.a it's all greek to me!)  

A more detailed explanation about a particularly confusing concept.

|Reference           |Description                                    |Status                  |
|--------------------|-----------------------------------------------|------------------------|
|[[CMIS URL|Spaghetti western: CMIS URL]] |access point for connecting to Alfresco CMIS application programming interface (API). |READABLE |
|[[Reporting project effort|Spaghetti western: Reporting project effort]] |A model for reporting project effort |RESEARCH |


<a name="PointOfViews"></a>  
##![PointOfViews](./images/paint-by-numbers-50.png?raw=true) Point of Views  

Organising digital stuff at home is still embryonic. These Points of View describe some crystal ball gazing as to where particular aspects of it might all be going.

|Reference           |Description                                    |Status                  |
|--------------------|-----------------------------------------------|------------------------|
|[[Where's Streaming Heading?|Point of View: Where's streaming heading?]] |Emerging trends in media streaming.  |RESEARCH
|[[Where's Content Management heading?|Point of View: Where's Content Management heading?]] |Consumers need a consumer level experience (read:iPhone usage easy) to use content tools.  Ingestion and publishing need to be easy.  |RESEARCH