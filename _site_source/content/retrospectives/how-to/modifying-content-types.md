{
    "title": "Modifying content types",
    "description": "Using content types for managing content.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts", "how-to"
    ],
    "tags": [ "content", "taxonomies" ],
    "status": "research"
}

_this page is not finished, see the [wiki home page](../wiki) to find out why..._ 

There really is no need to write a [fully blown](http://www.imdb.com/title/tt0077631/) how-to of the technical aspects for [modifying content models in Alfresco](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/tasks/kb-define-custom-model.html) as Jeff Potts has written a [concise and complete tutorial](http://ecmarchitect.com/images/articles/alfresco-content/content-article-2ed.pdf) already including:




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
 