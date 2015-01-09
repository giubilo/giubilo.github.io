{
    "title": "Github",
    "description": "Using Github for managing software projects.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ ""github", "sdlc", "dvcs" ],
    "status": "research"
}

First things first! There's a lot of stuff to manage; source code objects, project information, documentation, issues and will need to see how this stuff changes over time.  Had mainly used commercial implementations of source repositories and team collaboration / wiki tools.  Looked at a few open source ones (GitHub, BitBucket, SourceForge) and chose GitHub because; it had plenty of [documentation](http://git-scm.com/about) and [training](http://teach.github.com), active community, mac client, eclipse plug-in and there are other modules such as cmis-perl, pDLNA and ember media manager - that the project will be leveraging - are also on GitHub.

So we are going to use Git for:  

|GitHub Capability  |Use  | 
|------------------------------------|--------------------------------------------------------------|  
|GitHubPages |project information  |  
|source code management tools (<> icon) | code storage, organisation, versioning, collaboration, backup, code review  |  
|wiki (the book icon) | how to documentation  |  
|issues (the (!) icon) | requirements and issue tracking   |
|GitHub stats  | use the graphs and [social stuff](https://help.github.com/articles/be-social) to see how we are going |  

There's a bit of a hill to climb to get the most out of Git but it was great to put a [resource](./HowTo:-setting-up-project-resources) in like this as a first thing for the project as everything had a place to go and when talking to people could point them to it no matter where they were in the world.  We're just using some of the basic bits.  

## Steps 

1. Setup GitHub account  
1. Setup repository
1. Clone to desktop  
1. Edit README  
1. Setup GitHubPages  
1. Setup wiki
1. Setup issues  

### 1. Setup GitHub account

Simple registration, can do a free account or various paid ones if want more functionality, just go to [github.com](github.com).  Can have individual accounts or organisation accounts.

### 2. Setup repository(s)

Just used the online prompts but there is an excellent [bootcamp tutorial](https://help.github.com). Currently the project has repos for;

* allegria - the main repository that this wiki is in
* pDLNA - a 'forked' repository of some modules that allegria will customise

Have initially set the allegria repo up as a catchall for all the concepts being developed.  Later on may make submodules of each of the big areas to make cloning easier but just keeping it simple for now.  

### 3. Clone to desktop

So you need a client application on your desktop to clone your repository to so that you can work on it.  Can do this with the [commandline client](http://git-scm.com/downloads), which is ok and has lots of [documentation](http://git-scm.com/about).  Or can use a [graphical client](http://git-scm.com/downloads/guis) (had a brief look at the mac client and it was pretty cool).  But for this project's purposes we are using a graphical client that is embedded into the Eclipse Integrated Development Environment [see the paint-by numbers here](./Paint-by-numbers:-Eclipse-with-Epic-and-Egit).

### 4. Edit README

The [create a repo](https://help.github.com/articles/create-a-repo) tutorial suggests that it is a good idea for your GitHub repository to have a [README](.) (or README.md) file which is like a summary landing page for the online webclient. If you create a repo through the command line there's a few hoops to jump through but if you use the online webclient there is a checkbox to initialise the repo with a readme (that's the easiest way to go).  The readme's a good place to put some summary detail about the project and kick off some links to things like a project page, the wiki or to related sites.

The readme can use a 'markdown' type language and there is tons of help for it like; [articles in GitHub](https://help.github.com/articles/github-flavored-markdown) or [blogs](http://daringfireball.net/projects/markdown/syntax#link).

### 5. Setup GitHub Pages

The readme file is a good start to give people a snapshot of the project, but we wanted to have something a bit more, so are using [GitHubPages](http://pages.github.com).  It is initially a bit tricky to set up. We used the wizard that is on the GitHubPages site but it seemed to not do anything (it says to wait 10 mins).  After a while if you go to the url (username.github.io/repository) that the wizard gives you (in our case it was http://peterwatts.github.io/allegria/) then you should see the default page.

Underneath, the GitHubPages is a gh-pages branch under your repo and you can go into there and customise it to your heart's content (we initially just tweaked the index page (by editing it online) with project information).  You could probably use some cool tools to manage it much as you would any normal html website but we are doing it all manually at the moment.

### 6. Setup wiki

Using the wiki for the majority of documentation for the project other than read-me's and release notes etc which are included in each of the development directories.

Generally the wiki makes it easy to put up some information relatively quickly.  Needed to play around with getting the markup correct (e.g. putting spaces after text on end of line to get to display on next line, using relative links and embedding images in the pages).  

Using predominantly the "Markdown" editing mode as it's the default ([MediaWiki](http://www.mediawiki.org/wiki/MediaWiki) would also be useful) and just using basic functionality to begin with including:

* simple naming standard of Home, Concept, HowTo, Paint-by-numbers, Point-of-view so the 'Pages' page looks organised and relative links are easy to guess.  
* formatting like; headings, bold, code blocks, unordered lists, ordered lists and quotes.  
* relative links for content inside the Github repository (including for images).  

There is plenty of raw documentation out there about the wiki syntax including:

* [GitHub Help](https://help.github.com/categories/88/articles) including; Writing on GitHub, Markdown Basics and GitHub Flavoured Markdown
* http://guides.github.com/overviews/mastering-markdown/
* https://github.com/gollum/gollum/wiki
* https://github.com/mojombo/gollum-demo/wiki
* https://help.github.com/articles/github-flavored-markdown
* https://github.com/blog/1395-relative-links-in-markup-files
* https://help.github.com/articles/relative-links-in-readmes
* https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet  
* http://daringfireball.net/projects/markdown/
* http://designshack.net/articles/html/mastering-markdown-30-resources-apps-and-tutorials-to-get-you-started/
 

Also a few forum examples for some of the trickier formatting stuff such as:
 
* [embedding images into a wiki page](http://webapps.stackexchange.com/questions/29602/markdown-to-insert-and-display-an-image-on-github-repo) - some of the standard information available looked confusing or inaccurate - but this explanation seems to work.
* [example Github wiki](https://github.com/snowplow/snowplow/wiki) that has some nice table footer and sidebar functionality.
* plenty of forum examples out there on using the Eclipse IDE to author the wiki rather than typing into the online webclient but need to test out how to do this before write about it.
* can get some of the work in formatting tables done with a [table generator](http://www.tablesgenerator.com/markdown_tables)

"Github Flavoured Markdown (GFM) Markdown table syntax is quite simple. It does not allow row or cell spanning as well as putting multi-line text in a cell".  To get a bit fancier can use some inline HTML.  The [W3Schools site](http://www.w3schools.com/html/html_tables.asp) has some good documentation for this (and syntax in general).

Simple example using the info from W3Schools:

```
  <table border="0">
  <!--tr gives you a new table row and td gives you a new cell in the row-->
  <tr>
    <td>For more information on using groovy with cmis:
     <ul>
     <li><a href="http://groovy.codehaus.org">Groovy home</a></li>
     <li><a href="http://groovy.codehaus.org/Documentation">Groovy documentation</a> including getting started and tutorials</li>
     <li><a href="http://www.ibm.com/developerworks/java/tutorials/j-groovy">IBM groovy tutorial</a> includes using with Eclipse IDE</li>
     <li><a href="http://www.gradle.org">Gradle</a> build system for groovy</li>
     <li>books with groovy code examples</li>
     </ul>
    </td>
    <td>
      <!--The target="_blank" tag opens in a new browser tab when click on image-->
      <p><a href="http://www.manning.com/mueller" target="_blank">
        <img src="./images/manning-cmis.png?raw=true" alt="book"></a>
      </p>
    </td>
  </tr>
  </table>  
```

which produces:

<table border="0">
<tr>
  <td>For more information on using groovy with cmis:
   <ul>
   <li><a href="http://groovy.codehaus.org">Groovy home</a></li>
   <li><a href="http://groovy.codehaus.org/Documentation">Groovy documentation</a> including getting started and tutorials</li>
   <li><a href="http://www.ibm.com/developerworks/java/tutorials/j-groovy">IBM groovy tutorial</a> includes using with Eclipse IDE</li>
   <li><a href="http://www.gradle.org">Gradle</a> build system for groovy</li>
   <li>books with groovy code examples</li>
   </ul>
  </td>
  <td>
    <p><a href="http://www.manning.com/mueller" target="_blank">
      <img src="./images/manning-cmis.png?raw=true" alt="book"></a>
    </p>
  </td>
</tr>
</table>

Examples of coding with images:

```
<a name="PaintByNumbers"></a> 
##![Paint](/assets/img/paint-by-numbers-50.png?raw=true) Paint by Numbers  

<a name="HowTo"></a> 
<html>
  <h2>
      <img src="../blob/master/images/paint-by-numbers-50.png?raw=true" alt="icon" style="float:left"> How To's
  </h2>
</html> 

[![Gem Version](https://badge.fury.io/rb/gollum.png)](http://rubygems.org/gems/gollum)

```

### 7. Setup issues log

Not getting too funky here but will use the issues list capability to store:

* requirements definitions (green label)
* project issues / key decisions
* bugs, enhancements etc