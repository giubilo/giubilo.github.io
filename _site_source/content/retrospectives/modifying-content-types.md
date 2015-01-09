{
    "title": "Modifying content types",
    "description": "Using content types for managing content.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "content", "taxonomies" ],
    "status": "research"
}

_this page is not finished, see the [wiki home page](../wiki) to find out why..._ 

There really is no need to write a [fully blown](http://www.imdb.com/title/tt0077631/) how-to of the technical aspects for [modifying content models in Alfresco](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/tasks/kb-define-custom-model.html) as Jeff Potts has written a [concise and complete tutorial](http://ecmarchitect.com/images/articles/alfresco-content/content-article-2ed.pdf) already including:

* what are the building blocks of a [content model](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/concepts/content-modeling-about.html) (Types, Properties, Property types, Constraints, Associations, and Aspects) and [relationships](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/concepts/metadata-model-define.html) between them   
* how to build on the out-of-the-box models
* best practices
* bootstrap or dynamic [approaches](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/concepts/content-model-deploy.html) to deploying custom model  
* what configuration of the interface is needed to take advantage of the custom model (e.g. change type selector)  
* how to create, read, update and delete (crud) content not using the share or explorer interfaces (e.g. with cmis)  

This how-to instead describes how we applied those principles to come up with the specific model to use for allegria (so we're not trying to re-invent the wheel here -although we have lifted some summary cliffsnotes out of Jeff's stuff):

Also, given allegria is adding to an existing piece of software and essentially borrowing from some pre-existing ideas, we're following a [software development life cycle approach](./HowTo:-setting-up-project-resources) down the leaner end of the 'blast away and code' to 'dot all i's and cross all t's' spectrum and so,  in the flavour of that, this how-to will essentially meld together some typically separate specifications and describe:

* broadly what trying to do (sort of requirements definition - although the requirements statements are in the [issues bit](../issues/1) of this repository)
* functionality needed (sort of functional specification)
* paint-by-numbers implementation (sort of technical specification)

## broadly what trying to do

In the [project blurb](http://peterwatts.github.io/allegria/) we talked about some of the [things families organise](../issues/1) like:

* closets full of paper  
* photo albums with handwritten reminders of locations, dates, and people  
* recipe books with post-it-notes to highlight favourite meals and tips to make them turn out  
* on-line photo sites or photo browsing applications to share holiday snaps and stories  
* shelves stacked with music, books and movies  
* music docks and subscription services to play tunes and create playlists  
* on-line social bookmark communities or collections of browser bookmarks to interesting sites  
* on-line file sharing or hard drives to hold electronic documents or emails  
* on-line video channels or media centre appliances to stream tv-shows, ebooks, podcasts and movies to big and small screens  

That's a lot to tackle all at once so for this first concept going to focus on organising movies (mainly because we like watching movies and even to add movies to alfresco will involve a wide range of concepts to look at like property types and inheritance and user interface considerations). 

We're starting this analysis with what [Alfresco describes](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/concepts/content-modeling-about.html#1) content modelling as:

>Content modeling is a fundamental building block of the Alfresco content repository that provides a foundation for structuring and working with content 

>A content model defines how a node [anything stored] in the content repository is constrained [what kind it is, what properties it has and how it relates to other nodes].

>The Alfresco content repository then provides services for querying nodes [searching] and manages events, processes and restrictions for maintaining them.

In a practical sense modelling movies involved understanding:

* **classifying**  (i.e. what kind it is) - it's a movie but a finer classification such as feature film, tv show or home video is useful.
* **describing** (i.e. properties) with information that is available and interesting e.g. release year, plot, actors, content rating etc.
* **relating** the movie file node to other nodes e.g. another episode or a poster
* **searching** (i.e querying) the model and returning results in a variety of ways
* **processing** events and workflows like capture / create, classify, tag / scrape etc.   
* **restricting** what can be done with a movie e.g. movie classifications, digital rights, retention/archive policies  
 
###Classify

Its a movie! but a finer classification would make it easier for searching, working with and presenting movie content, for example:

* adding a hollywood blockbuster (feature film) and tagging it with release year, plot and actors scraped from IMDB, ensuring its 'MA15+' content rating put it in the right access group to keep it safe from the kiddies and maybe having one format created to suit a big screen TV and another copy (a [rendition](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/references/API-JS-RenditionService.html) in Alfresco speak) made to suit a tablet.  
* a tv show might use some of the same information but also have season and episode information and get it from TVDB not IMDB. 
* a home movie that could have some of the information but with an alternative rating system and increased focus on locations in the movie and wouldn't scrape any of the info  

Three 'movies' but 3 different sets of properties (albeit some common) with 3 different ways of getting the information and when sitting on the couch with a big box of popcorn looking for a saturday night movie you're probably going to want to browse the covers of the latest blockbusters and not have to scan past all the other kinds.  Simple examples but show where using a more fine-grained type than just 'movie' helps.

The [DublinCore Metadata Initiative (DCMI)](http://en.wikipedia.org/wiki/Dublin_Core) provides a starting place (its [MovingImage](http://dublincore.org/documents/2012/06/14/dcmi-terms/?v=dcmitype#dcmitype-MovingImage) type is a work in progress) but doesn't provide the level of detail needed to form a content model adequate for configuring in alfresco (i.e. a set hierarchy of types with properties).  Fortunately, Allegria's not the first project to walk this road.  A whole ecosystem of [vertical](http://www.imdb.com/title/tt0190865/) (movie focussed) systems exists for video sharing, media streaming and digital asset management (DAM) - Alfresco itself has a start on DAM.  From the ecosystem we get a leg up with [thoughts and data structures](http://wiki.xbmc.org/index.php?title=Video_library) for some subtypes (pretty much just Feature Films, TV Shows and Music Videos) but still have a bit to do.

The kinds of MovingImages (movies) in our initial [classify requirement](../issues/2) list are:

* feature film
* tv show
* tv recording (a subset of tv show)
* music video
* home movie
* multimedia project (e.g a uni assignment where make a movie)
* exercise video
* learning series

MovingImages in the context of Allegria includes binary files that are stored in the repository and internet streams but not images embedded in a web page (this will be picked up under managing bookmarks in another concept).

###Describe

Describing MovingImages is important because while images might be worth a thousand words, they aren't words like documents which we can look for with a full text search or text mining.

To help with describing MovingImages there are:
* standards for embedding some limited words (metadata) with image files, like event name / date, location and technical details  
* beginnings of facial and landmark recognition software capable of 'indexing' or at least auto tagging images and it's probably possible to do something with audio and subtitle tracks
* online databases which have rich standardised descriptions available already for some MovingImage subtypes; e.g. scrapes of IMDB and TVDB for feature films and tv shows

All of these go some of the way to helping with descriptions but they are still a way off as they rely on the [evolution of metadata standards](http://www.stockartistsalliance.org/metadata-manifesto-1) and content creation tools or the willingness of contributors to define online sources.  I was hoping to grab some ready made metadata tags that systems are using out there and add them to the model but it didn't seem that easy so decided on a sort of hybrid approach which builds on some of the metadata theory and glues it into what is happening in the existing ecosystem for media systems.  In that way hopefully when the standards do mature can easily retrofit and integration with what is already happening will be more straightforward (and easier to explain).

_So, some theory first:_

* [wikipedia](http://en.wikipedia.org/wiki/Metadata) describes broadly metadata mechanics
* Dublin Core Metadata Initiative (DCMI) has some mature work on [core metadata elements](http://dublincore.org/documents/dces/) and creates a namespace for a specific type of [MovingImages](http://dublincore.org/documents/2012/06/14/dcmi-terms/?v=dcmitype#dcmitype-MovingImage)
* photometadata.org (who show up pretty regularly in search results for MovingImage metadata) have built on the wikipedia and Dublin Core categories of metadata to come up with some specific [classes of metadata](http://photometadata.org/META-101-metadata-classes) 
* Helsinki Institute for Information Technology - had an interesting article adding [Social Metadata](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.96.5752&rep=rep1&type=pdf) to Personal Photography
    
Threw all of these in the [cooking pot](http://www.imdb.com/title/tt0382932/), boiled it up and out came these categories of metadata:

* **Descriptive Metadata** : describes various information about an image’s contents  e.g. captions, headlines, titles, keywords, location of capture etc. such as that in [IPTC-Core](http://www.iptc.org/std/photometadata/specification/IPTC-PhotoMetadata-201007.pdf)
* **Technical Metadata**: describes an image’s technical characteristics e.g. its size, colour profile and other camera settings etc. which most modern image-capture devices generate about themselves and the pictures they record, such as that stored in [Exif](http://photometadata.org/META-Resources-metadata-types-standards-Exif).
* **Social Metadata**:  describes information about usage, events or interaction with the image e.g. is it well liked, for how long has it been viewed etc. (more about this in 'process')
* **Administrative Metadata**:  describes specific restrictions on using an image e.g. licensing or rights,  usage terms, identity of the creator, and contact information for the rights holder or licensor etc. such as in [PLUS](http://www.useplus.com/index.asp?) (more about this in 'restrict')

Some of this metadata may be embedded with the image, a separate sidecar file and/or stored in the image collection manager.

_Now for the ecosystem_ (there are tons out there but these are ones i've used a bit and thought they would generate a good cross section of requirements):

* [Alfresco](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/concepts/content-model-preconfigured.html) out-of-the-box content models (obvious one to start with - make use of what is already there):
  * Jeff describes on [page 10](http://ecmarchitect.com/images/articles/alfresco-content/content-article-2ed.pdf) some of the out-of-the-box models
  * `/WEB-INF/classes/alfresco/model` contains other models
  * Alfresco [data dictionary](http://wiki.alfresco.com/wiki/Data_Dictionary_Guide#Built-in_Content_Model_Namespaces) has further descriptions
  * has [metadata extraction](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/concepts/metadata-extraction-about.html) capabilities (particularly for technical metadata) 
* [Universal Plug and Play (UPnP)](http://upnp.org/sdcps-and-certification/standards/sdcps/) - [Digital Living Network Alliance (DLNA)](www.dlna.org):
  * there are many similarities between Alfresco and UPnP Media Servers such as 'content directory', 'content searching', 'metadata extraction' and protocols to deliver binary content (seems like a match made in [heaven](http://www.imdb.com/title/tt0425123/)) - Alfresco has a 'Content Model' and UPnP has a 'ContentDirectory Service Object Organization'
  * the [standardised device and service description](http://upnp.org/specs/av/UPnP-av-ContentDirectory-v4-Service.pdf) for a MediaServer-ContentDirectory has defined (see fig 4 on page 307) its hierarchy of content as objects such as imageItem, videoItem (movie:videoItem, musicVideoClip:videoItem, videoBroadcast:videoItem), playlistItem, audioItem (musicTrack:auditItem), textitem, bookmark, epgitem and collections (album:container)
  * there's also some containers for other related objects such as a person instance represents an unordered collection of objects associated with a person - e.g. a musicArtist instance is a person instance, where the person associated with the container is a music artist and can contain objects of class musicAlbum, musicTrack or musicVideoClip
  * the standard also describes properties needed for working with the content like 'browse', 'search' and 'update'    
* [Ember](https://github.com/DanCooper/Ember-MM-Newscraper) media manager: 
  * the user interface defines a set of metadata to store in the database against the 'MovingImage'
  * uses a 'scraper' to auto-fill the information from (predominantly) internet sources  
  * organises multiple content files into a folder (like the binary file container with the audio, video and subtitle tracks and thumbnails for posters and fanart)    
  * produces an NFO (info) xml file (which is essentially a mini content model) that structures the metadata and documents the location to the movie binaries and thumbnails and can include links to other metadata and binary content not stored in the folder such as trailers and actor information 
* [XBMC](http://xbmc.org) media centre:
  * the user interface has search and display capabilities for metadata
  * has a [database](http://wiki.xbmc.org/index.php?title=XBMC_databases) which stores metadata that can be scraped from internet or [read](http://forum.xbmc.org/forumdisplay.php?fid=195) from Ember Media Manager [NFO Files](http://wiki.xbmc.org/index.php?title=NFO_files/movies) 
* [IMDB](http://www.imdb.com), [TVDB](thetvdb.com), [IceTV](https://www.icetv.com.au) and many other online databases provide:
  * metadata (typically descriptive) such as title, release year, plot, studio, genre
  * related content such as actor thumbs and descriptions, trailers, electronic program guides (epg)

Added these ingredients to the pot that had the metadata theory simmering in it and served-up a tasty bowl of [ContentModelAnalysis](../tree/master/aaContentModel/ContentModelAnalysis.xlsx) which summarises the [describe requirement](../issues/3) as:

* hierarchy of types from; Alfresco core types -> Image -> MovingImage -> [MovingImage subtypes]
* descriptive, technical, social and administrative properties (developed predominantly by cherry picking the properties in Alfresco out-of-the-box models, Ember Media Manager schema and NFO's and the XBMC schema
* assignment of properties to types including use of inheritance

###Relate

Relationships can [look like many things](http://www.imdb.com/title/tt0314331/):  

* a single MovingImage is more than one piece of content (it's a tight hierarchy of associated types) including:
  * the binary file container with the audio, video and subtitle tracks
  * thumbnails for posters and fanart
  * additional containers for special features and trailers
  * thumbnails for artists
  * bookmarks to other content like reviews
  * an xml file that a renderer might use to show all these parts as one thing
* One MovingImage might relate to another one such as in the case of sets (e.g. Starwars Saga), tv seasons and episodes or even a favourite playlist
* the binary file container could be broken down into smaller related bits such as video, audio tracks, subtitle tracks, chapters 
* other relationships will exist also to non-MovingImage type content e.g. a cooking how-to video related to a recipe  

The content model [relate requirement](../issues/4) is key to structuring the information and the process requirement will be key to making them happen e.g. for a feature film getting the binary file and its metadata and linked to the other content like fan art and artist thumbs easily.

###Search

On the [face of](http://www.imdb.com/title/tt0119094/) it, the [search requirement](../issues/5) could well be the most important requirement of all.  After all, making things easy to find is why we are putting things in boxes (uploading to repository) and labelling them (classifying, describing and relating).

But does 'easy to find' mean we are looking for a single particular item?  It probably does sometimes, like:
* looking for a particular multimedia project for uni assignment we might use a unique code to do with the subject / assignment / question or search for a specific feature film we want to watch again by the title and year
* linking from other content using an internal system reference e.g.
  * a recipe linking to a particular demonstration video 
  * next episode for a tvshow or a sequel to a feature film
  * next in an exercise series (like beginner to advanced) or type (stamina, speed etc) based on performance in an exercise
  * next item in a series of holiday home movies based on a timeline or location or trip itinerary
  * to do with a stage in a process e.g. might have an approval step to say it is ok to publish a particular MovingImage on a social media site.

These searches are using a small set of specific or unique search criteria to go straight to a specific item so can start using it immediately.  A small clarification might be useful here - some MovingImage subtypes like 'feature film' will actually be a number of separate items in the repository such as the binary video, audio and subtitle tracks, links to posters and links to actors, i.e. while might be searching for a specific item, a number of tightly related items may actually be how it exists.

It is also fair to say that many times we're not looking for a specific thing, so 'easy to find' becomes more 'easy to look around and choose'.  

A quick internet search poll of 'how do we choose a movie', puts 'mood' overwhelmingly in front. While [Rocky III](http://www.imdb.com/title/tt0084602/) may be the only go-to movie for some eye of the tiger inspiration, it's more likely there are a bunch that can be matched to a mood. Do you remember ambling around the video store in the comedy or new releases sections because you felt like a laugh or something fresh.  You'd pick up a few because their cover or plot looked interesting, you knew the actors, a vote was taken with whoever came to the store with you or there was a deal on one new release and two weeklies.  The choosing had just as much to do with using the content model, like genre, actor and plot as it did with visual appeal like the covers or the other more non-specific factors like the group input or the deal the store was offering.  

The first bit of the search was the 'looking around' which could be summarised as the following three categories of browsing: 

* navigate and browse - go to (navigate) predetermined groups of items like:
  * media centre style containers like type (e.g. feature film, home movie, music video), recently added, genres, sets, years, actors - it's likely a MovingImage exists in more than one container e.g. music video in music and videos
  * youtube style containers like featured, top rated, most viewed, favourites, subscriptions, history
  * youtube style browsing using 'more from' (creator), 'related to' (e.g. mermaid), 'comments (with links)'
  * playlists of favourites or themes or date driven like wedding anniversary or event driven like the same feature films watched when a particular group of friends catch up
* filter and browse - set subtype dependent filter criteria like:
  * Classification such as feature film, home movie, music video 
  * Descriptive Metadata such as title, rating, year, genre (xbmc also lists moods, styles and themes in its music searches), actor, director, studio, language for an Alien or Schwarzenegger marathon night, foreign movie night, a festive choice or the anniversary of something
  * Technical Metadata such as size so can work out if it will look ok on a tablet or a projector 
  * Social Metadata such as in-progress to finish some that have started watching or which movies are in a 'hot picks' list 
  * Administrative Metadata such as creator to see all the home movies your child has taken
* sort and browse - to make the browsing orderly and intuitive e.g.
  * alphabetical on title
  * ordered by rating
  * ordered by number of times watched
  * ordered by duration
  * ordered by year

The second bit of the search, 'choosing', then might be:
* visual cues like:
  * images in a lightbox
  * facetted search results with categorisation (e.g. grouped by subtype) and relevance
  * nested search results like the YouTube style browsing example
  * augmented search results that overlay subtype specific cues like a world map, or timeline or geneological tree to a series of home movies or [augment](http://en.wikipedia.org/wiki/Augmented_reality) the descriptions in the search results with additional information 
* use [group opinion](http://www.drewsdirections.com/2010/06/27/the-system/) tools or overlay popular choice suggestions like IceTV Picks, www.suggestmemovie.com, www.jinni.com, [Metacritic](http://en.wikipedia.org/wiki/Metacritic) or [Rotten Tomatoes](http://en.wikipedia.org/wiki/Rotten_Tomatoes)
* add things to play queues like a wishlist or shopping cart idea
* using the search itself to drive future searches such as:
  * analytics about the number of times something has come up in a search
  * what search terms resulted in a particular thing being identified and selected
  * ways to make something appear higher in results or stand out from the pack

It seems obvious to say now but both the 'specific' type search and 'browse and choose' type search examples demonstrate that the application of the search criteria and how the search results are displayed and used are of equal importance.  What might not be obvious are the boundaries for searching:

* search will query internal and external / foreign metadata e.g. searching for MovingImages about Venice Italy might might bring up a home movie of a gondola ride and also bring up a news story of reparations to Venice foundations and today's prices for gondola rides or while watching an old feature film you might want to know what other later movies one of the actors was in  
* the binary MovingImage file might not be stored in the repository - could be:
  * 'offline' on a DVD because have chosen not to rip it
  * internet stream like [RTSP](http://en.wikipedia.org/wiki/Real_Time_Streaming_Protocol) not a link to a webpage
  * in an online database somewhere (including external review information) but not yet in the repository - might end up adding it
  
The gist of these boundaries is the idea of [universal search](./Point-of-View:-Where's-streaming-heading%3F) - that is a search that is informed but not constrained by what is in the repository (constraints will come later like processing restrictions applied).  Now the repository becomes more than a box to hoard stuff - it brings the contents to life.

###Process

ingest -> digest - > publish

what's all the stuff we do to / with content? - lifecycle??

The purpose statement for the [semantic web](http://en.wikipedia.org/wiki/Semantic_Web) describes it as:

>enabling users to find, share, and combine information more easily

not really about the other capture processes - we only capture it so we can do these things…

MediaServer - Content Creation (capture) Subsystem, Content Storage Database, Content Management Subsystem, Content Transfer Subsystem.

In many ways this is a good fit as a higher purpose statement for Allegria - 

UPnP Standardized Device Control Protocol Specification for a MediaServer (v4) defines the following services:

|Services             |Scenarios                        |Actions                                        |
|---------------------|---------------------------------|-----------------------------------------------|
|ContentDirectory Service (v4)|Generating Object ID Values, Content Setup for Browsing and Searching, Browsing, Searching and References, Object Creation, Importing a Resource, Exporting ContentDirectory Resources, Playlist Manipulation, Multi-component media representation, Segments Manipulation, Bookmark Manipulation, Processing FreeForm Queries, Foreign Metadata, Monitoring Changes, Browsing preserved transitory content, Object Linking, DEVICE_MODE feature, Synchronized Playback|GetSearchCapabilities(), GetSortCapabilities(), GetSortExtensionCapabilities(), GetFeatureList(), GetSystemUpdateID(),  GetServiceResetToken(), Browse(), Search(), Filter, CreateObject(), DestroyObject(), UpdateObject(), MoveObject(), ImportResource(), ExportResource(), DeleteResource(), StopTransferResource(), GetTransferProgress(), CreateReference(), FreeFormQuery(), GetFreeFormQueryCapabilities(), RequestDeviceMode(), ExtendDeviceMode(), CancelDeviceMode(), GetDeviceMode(), GetDeviceModeStatus(), GetPermissionsInfo()|
|ConnectionManager Service (v3)|ProtocolInfo Concept , Typical Control Point Operations, Relation to Devices without ConnectionManagers, PrepareForConnection() and ConnectionComplete(), Determining if ContentDirectory items are playable, CLOCKSYNC Feature|GetProtocolInfo(), PrepareForConnection(), ConnectionComplete(), GetCurrentConnectionIDs(), GetCurrentConnectionInfo(), GetRendererItemInfo(), GetFeatureList()|
|AVTransport Service (v3)|TransportState Control, Transport Settings, Navigation, AVTransportURI Concept, AVTransport Abstraction, Supporting Multiple Virtual Transports,   SetAVTransportURI(), Playlist Playback, Dynamic Playlists, CLOCKSYNC feature: Synchronized Playback|SetNextAVTransportURI(), GetMediaInfo(), GetMediaInfo_Ext(), GetTransportInfo(), GetPositionInfo(), GetDeviceCapabilities(), GetTransportSettings(), Stop(), Play(), Pause(), Record(), Seek(), Next(), Previous(), SetPlayMode(), SetRecordQualityMode(), GetCurrentTransportActions(), GetDRMState(), GetStateVariables(), SetStateVariables(), GetSyncOffset(), SetSyncOffset(), AdjustSyncOffset(), SyncPlay(), SyncStop(), SyncPause() , SetStaticPlaylist(), SetStreamingPlaylist(), GetPlaylistInfo()|
|ScheduledRecording (v2)|Checking the Capabilities of a ScheduledRecording Service, Adding a Scheduled Recording Entry to the List, Browsing recordSchedule and recordTask instances, Rating System, Conflict Detection and Resolution, Deleting a recordSchedule|GetSortCapabilities(), GetPropertyList(), GetAllowedValues(), GetStateUpdateID(), BrowseRecordSchedules(), BrowseRecordTasks(), CreateRecordSchedule(), DeleteRecordSchedule(), GetRecordSchedule(), EnableRecordSchedule(), DisableRecordSchedule(), DeleteRecordTask(), GetRecordTask(), EnableRecordTask(), DisableRecordTask(), ResetRecordTask() , GetRecordScheduleConflicts(), GetRecordTaskConflicts()|


Alfresco Services comprise the following:
* Content Services
  * Lifecycle: manage content over time such as using rules to automatically trigger behavior when certain defined conditions are met. You can extend a standard set of conditions and actions using scripts and custom actions.
  * Transformation: convert content from one type to another such as generating PDF files from Microsoft Office formats and converting between image formats. This service is extensible to allow the use of additional transformers.
  * Metadata extraction: synchronize document metadata with node metadata - automatically extracts metadata information from inbound and/or updated content and updates the corresponding nodes properties with the metadata values.
  * Tagging: arbitrary user-generated tags versus formally defined classifications
  * Thumbnailing service - creates a thumbnail of a given content property for a node. It can generate a number of different standard types of thumbnails, including Flash web previews and image thumbnails (small and medium sized).
* Control services (encapsulate processes through which content flows):
  * Workflow - structured process that includes a sequence of connected steps
  * Change set - working area for making safe content modifications
  * Preview - viewing content as it should be before publishing
  * Deployment - publishing content from one environment to another
* Collaboration services (integrate the production and publishing of content into social networks):
  * Social graph: represents people and their relationship to each other, either directly or indirectly through groups or teams
  * Activities: continuous personalized feed of activities performed by others in the social graph or by Alfresco
  * Wiki: easy creation and editing of interlinked web pages
  * Blog: log of regularly maintained entries of commentary, events, and other material, such as documents and videos
  * Discussions: threaded conversations
* Sites service - a key concept within Alfresco Share for managing documents, wiki pages, blog posts, discussions, and other collaborative content relating to teams, projects, communities of interest, and other types of collaborative sites.
* Invite service - maintains user and group memberships for sites.
* Activity service - Alfresco Share uses activities to track a range of changes, updates, events, and actions, allowing users to be aware of details of the changes.
* Tagging service - keywords or terms assigned to a piece of information including documents, blogs, wiki pages, and calendar events.
* Commenting service - comments are modeled as separate content items that are associated with the relevant node through child associations. The Commenting service provides a RESTful API for working with comments.
content centric app - no application database

Digital Asset Management (DAM) Ideas:

capture / create  
classify, tag / scrape 
associate / relate with other content  
renditions  - versioning, transcoding for different device formats or changes to embedded metadata  
check in/out  
review/approve  
assign tasks  
updating social metadata like most watched  
syndicate / publish  
auditing/reporting  
events/actions/notifications  






Social Metadata
request for assets like play, fast forward
e.g. 

'search' is also a process with metadata/metrics/restrictions

Also in understanding the metadata classes other requirements emerged
changes to embedded metadata, updating social metadata like most watched
uni-directional or bi-directional operation on the metadata - i.e. extracting the metadata from the content's binary file and putting it into the alfresco database and/or going back in the other direction to change the metadata in the content's binary file with data from the alfresco database (more about this in 'process').

this is locked in with [where streaming is heading](./Point-of-View:-Where's-streaming-heading%3F) because while use online sites to share photos and docs probably don't share all of them or might only share the final version of something and want to retain other versions

[process requirements](../issues/6)

###Restrict

e.g. movie classifications, digital rights, retention/archive policies

UPnP content protection stuff

[restrict requirements](../issues/7)

## functionality needed (sort of functional specification)

In reality it's a mash up between the alfresco types (content centric) and upnp objects (service centric).  It'll probably need a bit of tweaking particularly in working out an optimal model for inheritance of properties between types and the properties that 'search', 'process' and 'restrict' need - this mirrors Jeff's comments:

>'be conservative early on by adding only what you know you need. A corollary to that is prepare yourself to blow away the repository multiple times until the content model stabilizes.'

A UPnP media server (search and sort capabilities) does searches like Browse() using sorts on containers like album, person, genre and also straight searches on metadata properties like title, Ember and XBMC does similar.
Alfresco has exploring a folder structure and searching + it has full text searching of the content (for images although the do sometimes have text embedded such as Exif/XMP they are predominantly binary so not really useful), cmis has the concepts of navigating and searching
e.g. like using properties such as genre, title, year, artist, studio, unwatched, keywords  

design work in the process requirements as the rest is really the properties

XMP: http://en.wikipedia.org/wiki/Extensible_Metadata_Platform 

Ember MM has exact match and partial match

Alfresco - open source CMS, DAM component can read/write XMP (MS Windows, Linux)  - some work started with the metadata for digital assets (but I can't find it)

The most common metadata tags recorded in XMP data are those from the Dublin Core Metadata Initiative, which include things like title, description, creator, and so on. The standard is designed to be extensible, allowing users to add their own custom types of metadata into the XMP data. XMP generally does not allow binary data types to be embedded. This means that any binary data one wants to carry in XMP, such as thumbnail images, must be encoded in some XML-friendly format, such as Base64.
XMP metadata can describe a document as a whole (the "main" metadata), but can also describe parts of a document, such as pages or included images. This architecture makes it possible to retain authorship and rights information about, for example, images included in a published document. Similarly, it permits documents created from several smaller documents to retain the original metadata associated with the parts.

maybe also need to add a special content type of MediaServer so that can hold the device description xml files(s).


## paint-by-numbers implementation (sort of technical specification)

Here are the steps to follow when configuring a custom content model:
1. Create an extension directory
2. Create a custom model context file
3. Create a model file
4. Restart Tomcat

using xmp, what to about scrapers / uni-bi directional metadata updating (should keep the original file and create a rendition if updating metadata

change types
http://forums.alfresco.com/forum/end-user-discussions/alfresco-share/change-types-options-menu-labeleds-06082011-1023

Configuring the Custom Model in Alfresco Share

Adding Custom Types and Aspects to Lists
 “Is sub-type” criteria. When a user configures a rule on a space and uses content types as a criteria, the custom types should be a choice in the list of possible content types.
 “Has aspect” criteria. When a user configures a rule on a space and uses the presence of an aspect as a criteria, the custom aspects should be a choice in the list of possible aspects.
 Change type action. When a user runs the “specialize type” action, either as part of a rule configuration or through the “Change Type” UI action, the custom types should be available.
 Add aspect. When a user runs the “add aspect” action, either as part of a rule configuration or through the “Manage Aspects” UI action, the custom aspects should be available.

Configuring Forms for Custom Properties / Configuring the form service for a custom type / Configuring the form service for custom properties
 Document Details. When a user looks at the document details page for a piece of content
stored as one of the custom types or with one of the custom aspects attached, the properties section should show the custom properties.
 Edit Properties. When a user edits the properties of a piece of content, either with the “full” form or the abbreviated form, the appropriate properties should be shown.

Configuring Advanced Search in Alfresco Share
 Advanced search. When a user runs an advanced search, they should be able to restrict search results to instances of our custom types and/or content with specific values for the properties of our custom types.

Localizing Strings for Custom Content Models

You’ve seen that configuring Alfresco Share for your custom content model essentially involves adding XML to the share-config-custom.xml file and creating a properties file for your localized strings. All of this lives under the “web-extension” directory in the Share web application.
There are other things you might like to do to the Share user interface, but these are beyond the scope of this document:
• Add custom content types to the Create Content menu
• Add custom properties to the document library sort criteria
• Add custom properties to the document library data grid

http://wiki.alfresco.com/wiki/Data_Dictionary_Guide#Step_by_Step_Model_Definition  
http://wiki.alfresco.com/wiki/Displaying_Custom_Metadata  


[aaContentModel](../tree/master/aaContentModel)
 