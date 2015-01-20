{
    "title": "Application Lifecycle Management",
    "description": "End-to-end management of development.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts", "how-to"
    ],
    "tags": [ "alm", "sdlc" ],
    "status": "research"
}

_this page is not finished, see the [wiki home page](../wiki) to find out why..._ 

how to manage all the activities that occur from birth to death of an application (includes strategy / portfolio performance management, project management, Agile/DevOps including capacity/incident/problem/config/change etc, Financial Management - CAPEX/OPEX, supplier management / strategic sourcing, license management) - all the stuff ITIL/CObIT talk about.

Agile/DevOps about focus/flow

something to do - task / context used to:  

* build a project schedule / demand forecast
* focus work by attaching task to requirements / defect and relevant source code / documentation (and when work is attached end to end like that then it is also self documenting so don't have to explain to the next person who picks it up either for review or later maintenance tasks what all the relevant bits are + get traceability)
* at the really detailed end can build as go by putting in TODO' in the code so know what is left, less to fall through the cracks
* easy to see status
(need a user interface for developer to pick and use tasks, project manager to summarise, a task bus to shuffle tasks from developers code, issues logged - and the social commentary around them, code reviews, builds and a repository to store the tasks - mylyn / tasktop / jira - all about focus and flow - books aplenty on this like mikado, lean/alm, requirements management, project management)

develop some code

No matter how advanced system modelling and code generation gets there's seems to be no escaping the need to hand write some code.  So, we could have broken out our favourite text editor (Xcode, Sublime, Notepad, vi, joe, nano), interpreter / compiler, debugger, command line to package and read logs, manuals, specs, html editor, documentation editor, xml editor...but chose instead to take a sec to look at using an open source [Integrated Development Environment](http://en.wikipedia.org/wiki/Integrated_development_environment) (IDE).  

In one interface (with multiple perspectives) we get a ton of [resources](./HowTo:-setting-up-project-resources) to help with the [tasks of the project](http://www.ibm.com/developerworks/opensource/tutorials/os-perlecl/section2.html) including; 

* writing code (there'll be all sorts - java, go, ruby, json, perl, xml, html, text, makefile, markdown code)
* model driven development / test driven development / content driven development (all wrapped up in Agile)
* formatting code so it's readable (syntax highlighting), valid (syntax checking) and conforms to best practice techniques for the language (like project structures, code quality and vulnerabilities)
* execute and debug the code (postmortem/live/cgi-remote)
* get help writing internal comments, documentation and todo's
* get access to documentation (like perldoc for modules)
* source code management / version control - branching / merging strategies (GitFlow)
* code review - GitHub pull request vs Gerrit review

(Eclipse + plugins, Atlassian SourceTree + GitFlow, Mou - sometimes it makes sense to come outside of the IDE, Gerrit, GitHub + badges)

environments

* build/package/implement code - release strategy / cycle
* testing not a separate step but baked into everything else (e.g. requirements management, code reviews)
* Vagrant + Docker (+ CoreOS) + Chef/Puppet - continuous build / integration (DevOps)
* Gradle

(need a repository to put released code, binaries, release notes and setup scripts + badges)

http://secretgeek.net/lifecycle.asp  
http://www.top-q.co.il/services/alm/  
http://blogs.technet.com/b/doug_mccutcheon/archive/2009/05/19/the-new-application-lifecycle-management-demo-image-built-on-sharepoint-server-2007-enterprise-project-management-epm-solution.aspx  
http://blog.programmableweb.com/2013/07/10/new-wso2-app-factory-allows-management-of-complete-enterprise-application-lifecycle/  
http://www.mountainview-itsm.com/itil-training/downloads/itil-pocket-guide/itil-pocket-guide.swf  
http://en.wikipedia.org/wiki/Systems_development_life-cycle  

somewhere between what's needed to deliver a textbook hello world output example application and enterprise methodologies and frameworks for delivering outcomes.



Application lifecycle management (ALM) is the product lifecycle management (governance, development, and maintenance) of application software. It encompasses requirements management, software architecture, computer programming, software testing, software maintenance, change management, project management, and release management.

In software engineering, software configuration management (SCM)[1] is the task of tracking and controlling changes in the software, part of the larger cross-discipline field of configuration management.[2] SCM practices include revision control and the establishment of baselines - software development is considered separately.

The goals of SCM are generally:[citation needed]
* Configuration identification - Identifying configurations, configuration items and baselines.
* Configuration control - Implementing a controlled change process. This is usually achieved by setting up a change control board whose primary function is to approve or reject all change requests that are sent against any baseline.
* Configuration status accounting - Recording and reporting all the necessary information on the status of the development process.
* Configuration auditing - Ensuring that configurations contain all their intended parts and are sound with respect to their specifying documents, including requirements, architectural specifications and user manuals.
* Build management - Managing the process and tools used for builds.
* Process management - Ensuring adherence to the organization's development process.
* Environment management - Managing the software and hardware that host the system.
* Teamwork - Facilitate team interactions related to the process.
* Defect tracking - Making sure every defect has traceability back to the source.

DevOps integration targets product delivery, quality testing, feature development and maintenance releases in order to improve reliability and security and faster development and deployment cycles. 


http://en.wikipedia.org/wiki/Agile_software_development  
http://guide.agilealliance.org/subway.html  
http://en.wikipedia.org/wiki/Community-driven_development  
http://en.wikipedia.org/wiki/Kanban_(development)  kanban / process driven development  / content driven development  
The Kanban method – An approach to incremental, evolutionary process improvement for organisations.  
http://en.wikipedia.org/wiki/Feature-driven_development  (decomposition approach)  
http://en.wikipedia.org/wiki/Test-driven_development  

http://en.wikipedia.org/wiki/Model-driven_software_development / business driven development  
Model-driven software development (MDSD) is an alternative to round-trip engineering. Round-trip engineering is the concept of being able to make any kind of change to a model as well as to the code generated from that model. The changes always propagate bidirectional and both artifacts are always consistent. 

The Agile Manifesto is based on twelve principles:[9]  
Customer satisfaction by rapid delivery of useful software  
Welcome changing requirements, even late in development  
Working software is delivered frequently (weeks rather than months)  
Working software is the principal measure of progress  
Sustainable development, able to maintain a constant pace   
Close, daily cooperation between business people and developers  
Face-to-face conversation is the best form of communication (co-location)  
Projects are built around motivated individuals, who should be trusted  
Continuous attention to technical excellence and good design  
Simplicity—the art of maximizing the amount of work not done—is essential  
Self-organizing teams  
Regular adaptation to changing circumstances  

Agile development is supported by a bundle of concrete practices suggested by the agile methods, covering areas like requirements, design, modeling, coding, testing, project management, process, quality, etc. Some notable agile practices include:
Acceptance test-driven development (ATDD)  
Agile Modeling  
Backlogs (Product and Sprint)  
Behavior-driven development (BDD)  
Cross-functional team  
Continuous integration (CI)  
Domain-driven design (DDD)  
Information radiators (Scrum board, Kanban board, Task board, Burndown chart)  
Iterative and incremental development (IID)  
Pair programming  
Planning poker  
Refactoring  
Scrum meetings (Sprint planning, Daily scrum, Sprint review and retrospective)  
Test-driven development (TDD)  
Agile testing  
Timeboxing  
Use case  
User story  
Story-driven modelling  
Velocity tracking  

