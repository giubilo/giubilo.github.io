{
    "title": "cmis dlna connector",
    "description": "library to connect cmis compliant repository to dlna devices.",
    "publishdate": "2014-02-01",
    "categories" : [
    	 "summary"
    ],
    "tags": [ "roadmap" ]
}

<a name="Concepts"></a>  
##![Concepts](/assets/img/paint-by-numbers-50.png?raw=true) Concepts  

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
