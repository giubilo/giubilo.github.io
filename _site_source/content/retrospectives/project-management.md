{
    "title": "Project Management",
    "description": "Knowledge areas for managing projects.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "project management" ],
    "status": "research"
}

_this page is not finished, see the [wiki home page](../wiki) to find out why..._ 

allegria's objectives seem straightforward enough:

* work out how to make the processes and tools large organisations use to organise stuff, practical for a household.
* learn how to use some open source application lifecycle techniques, tools and technologies.  
* have some fun and pass back what's been learned to the community.  

But what will it take to achieve them - [where do we begin](www.imdb.com/title/tt0066011/)?   

Start at the beginning probably, although it may make more sense to start at the end, get a clear idea of [what success looks|Helicopter View: Success] like and write it down so there is a beacon to aim for and to keep the boat off the rocks.  

With a clear view on success I hear you say 'roll your sleeves up and get on with it' - the cunning plan - _just do it_. 

And sometimes that is the best way to get things done, particulalry when the thing being done (product) is well known, how to do it is well known (process) and the whoever is doing it have worked together to do it before (people) i.e. the [dynamics|Helicopter View: Dynamics] are well understood.  Just getting on with it might also be the best approach when doing something like writing and writer's block has set in making it difficult to start.  The [Forrestor Principle](www.imdb.com/title/tt0181536/) says to just sit down and write (but be prepared to re-write as well).

allegria as a product has parts well established (like the Alfresco platform), although in a corporate setting rather than for consumers and some of its technical parts are pretty new, and as is likely the case with most open source projects the people working on it also we have at the start none or limited experience with consumer content managemet and open source tools and techniques.  

at the At the other end of the spectrum to the cunning plan, is to follow a prescription project management philosophy.

cunning plan is doable when just 1 person will build and use the product but as soon as add another for either activity then need some way to engage other (that means will need to use one or more PM techniques - and really even if you are by yourself will get some value from PM techniques).

- project success
- HRM
- practitioner approaches
- project dynamics
- project lifecycle
- quality

Need a whole thing on the systems bit (not a PMBOK area but should add) as setting up an environment for manaing the project stuff and the development stuff and the overlap / integrations between them (think tasks / collaboration / consistency etc - all this is so integral to getting a project that has a systems flovour)


is this ia project or a product is it a number of projects to make a product - 

In [Karate Kid III (1989)](http://www.imdb.com/title/tt0097647/) Mr. Miyagi sagely tells his pupil (but about karate);  
_Mr. Kesuke Miyagi: Ah. Only root [development] come from Miyagi. Just like bonsai choose own way grow because root strong you choose own way do karate same reason._  
_Daniel Larusso: I do it your way._  
_Mr. Kesuke Miyagi: Hai. One day you do own way._

Setting up some basic project resources for allegria was a bit like Miyagi San's bonsai analogy for karate...we wanted to have some basis in the steps of the [root] development process like:
* propagate the idea - build the business case and project plan
* work out the boundaries and requirements
* define detailed design
* specify technical elements and tools
* determine the build, test and implement approach
 
...but there really isn't a traditional business case for this, we just want to do something [fun](http://dictionary.reverso.net/italian-english/allegria) and interesting - build [a field of dreams](http://www.imdb.com/title/tt0097351/). It's not going to be sold and nobody's getting paid for this, which means even though there's no fixed schedule, need to get quick, easy successes that build momentum and enthusiasm.  So our 'own karate way' is somewhere in the middle of a spectrum of a sensible structured approach and the just-do-it cunning plan.

The [project page](http://peterwatts.github.io/allegria/) describes the idea, objectives of the project and broadly a plan to get there.  The [readme](../blob/master/README.md), [wiki](./) and [issues](../issues) describe a mixture of requirements and design (the summary [concept](./Concept-Work) and [how to](./How-To's) pages hold the 1000ft descriptions and will look to flesh this out in each of the underlying detail pages). We might be schmicky later with some traceability from objectives through requirements to code, test and implementation but for now going to take a pragmatic middle ground).

That leaves the technical elements.  Yes, it would be nice to have a bit more detail up front about what this thing is going to look like to determine an appropriate architecture, tools and approach but without trying to incite some zealous rage from technical purists the reality for this project is that there are some other drivers to these choices including:
* the [64 million dollar](http://www.imdb.com/title/tt0880557/) question you're probably thinking though is 'why build a home media centre on top of a document management system - who does that? movies aren't documents or web pages, just build a streaming app with genre folders'...and I say, 'it's all content man!', its just a content centric app...not convinced? have a read of the [project page](http://peterwatts.github.io/allegria/) and choose then.
* once had settled on doing this in a Content Management System had to pick a horse from the pack --have looked at dozens of open source content / process tools but for whatever reason keep gravitating back to Alfresco - it might be the some of the words like 'simple' and 'solid' in the [guiding design principles](http://docs.alfresco.com/4.2/topic/com.alfresco.enterprise.doc/concepts/alfresco-principles.html) or that it was quick to get a feel for it and put content in, or the size of the surrounding community, or the shiny new Activiti tool, whatever it was we're here. And now that have picked, a key objective of the project is to get better at using the Alfresco platform and use / enhance all of its capabilities and show others how we did it (interestingly Git is also a contender particularly for its feature of all collaborators having equal status of document versions - no single authoritative copy of something - and using sophisticated merge capabilities to sort out the logistics of merging updates).
* for us, key to Alfresco 'making sense' as a media centre is how it fits into the consumer ecosystems surrounding streaming stuff (movies, songs, pictures etc).  The horse race for technology contenders for this is close, none (and this will likely rattle more than a few cages) have really stuck out for us as THE ONE to choose.  This is crystal ball gazing rather than any scientific thinking about [where things are heading](./1.2.1-Where's-streaming-heading%3F)...really just picked some 'standards' that had some definition and community and will give them a crack (DLNA - Digital Living Network Alliance, UPnP - Universal Plug an Play and plug these into a content management standard CMIS -Content Management Interoperability Services).
* another key objective is to get a better understanding of [open source projects](http://www.ibm.com/developerworks/opensource/newto/), so; using open source tools in a distributed collaborative approach (Alfresco and its addons and interfaces are developed in SpringSurf, Java, Python, Perl, C, Ruby etc and many are hosted on GitHub - so made sense to select from them).



• Integration Management  
• Scope Management  
• Time Management  
• Cost Management  
• Quality Management  
• Human Resources Management  
• Communications Management  
• Risk Management  
• Procurement Management  
• Stakeholder Management  

2. orGAnIZAtIonAL InFLuEncES And ProJEct LIFE cYcLE .............................................. 19
2.1 organizational Influences on Project Management ................................................ 20 2.1.1 organizational cultures and Styles ............................................................. 20 2.1.2 organizational communications ................................................................. 21 2.1.3 organizational Structures ............................................................................ 21 2.1.4 organizational Process Assets .................................................................... 27 2.1.5 Enterprise Environmental Factors ............................................................... 29

2.2 Project Stakeholders and Governance .................................................................... 30 2.2.1 Project Stakeholders.................................................................................... 30 2.2.2 Project Governance ...................................................................................... 34 2.2.3 Project Success............................................................................................ 35
2.3 Project team ............................................................................................................. 35 2.3.1 composition of Project teams ..................................................................... 37 2.4 Project Life cycle ...................................................................................................... 38 2.4.1 characteristics of the Project Life cycle ..................................................... 38 2.4.2 Project Phases.............................................................................................. 41


Organizational culture is shaped by the common experiences of members of the organization and most organizations have developed unique cultures over time by practice and common usage. Common experiences include, but are not limited to:
• Shared visions, mission, values, beliefs, and expectations;  
• Regulations, policies, methods, and procedures;  
• Motivation and reward systems;  
• Risk tolerance;  
• View of leadership, hierarchy, and authority relationships;  
• Code of conduct, work ethic, and work hours; and  
• Operating environments.  

Many organizational structures include strategic, middle management, and operational levels. The project manager may interact with all three levels depending on factors such as:
• Strategic importance of the project,  
• Capacity of stakeholders to exert influence on the project,  
• Degree of project management maturity,  
• Project management systems, and  
• Organizational communications.  
This interaction determines project characteristics such as:  
• Project manager’s level of authority,  
• Resource availability and management,  
• Entity controlling the project budget,  
• Project manager’s role, and  
• Project team composition.  

The project life cycle is independent from the life cycle of the product produced by or modified by the project. However, the project should take the current life-cycle phase of the product into consideration.  A project may be divided into any number of phases. A project phase is a collection of logically related project activities that culminates in the completion of one or more deliverables. Project phases are used when the nature of the work to be performed is unique to a portion of the project, and are typically linked to the development of a specific major deliverable. A phase may emphasize processes from a particular Project Management Process Group, but it is likely that most or all processes will be executed in some form in each phase. Project phases typically are completed sequentially, but can overlap in some project situations. Different phases typically have a different duration or effort. The high-level nature of project phases makes them an element of the project life cycle.

* Phase-to-Phase relationships: sequential and overlapping    
* Predictive Life cycles  
* Iterative and Incremental Life cycles  
* Adaptive life cycles (also known as change-driven or agile methods) are intended to respond to high levels of change and ongoing stakeholder involvement. Adaptive methods are also iterative and incremental, but differ in that iterations are very rapid (usually with a duration of 2 to 4 weeks) and are fixed in time and cost. Adaptive projects generally perform several processes in each iteration, although early iterations may concentrate more on planning activities.  

Adaptive methods are generally preferred when dealing with a rapidly changing environment, when requirements and scope are difficult to define in advance, and when it is possible to define small incremental improvements that will deliver value to stakeholders.

The project processes are performed by the project team with stakeholder interaction and generally fall into one of two major categories:
• Project management processes. These processes ensure the effective flow of the project throughout its life cycle. These processes encompass the tools and techniques involved in applying the skills and capabilities described in the Knowledge Areas (Sections 4 through 13).  
• Product-oriented processes. These processes specify and create the project’s product. Product- oriented processes are typically defined by the project life cycle (as discussed in Section 2.4) and vary by application area as well as the phase of the product life cycle. The scope of the project cannot be defined without some basic understanding of how to create the specified product. For example, various construction techniques and tools need to be considered when determining the overall complexity of the house to be built.  

Stakeholder Management:

Project Stakeholder Management includes the processes required to identify the people, groups, or organizations that could impact or be impacted by the project, to analyze stakeholder expectations and their impact on the project, and to develop appropriate management strategies for effectively engaging stakeholders in project decisions and execution. Stakeholder management also focuses on continuous communication with stakeholders to understand their needs and expectations, addressing issues as they occur, managing conflicting interests and fostering appropriate stakeholder engagement in project decisions and activities. Stakeholder satisfaction should be managed as a key project objective.


Integration:

Project Charter:
• Project purpose or justification,  
• Measurable project objectives and related success criteria,  
• High-level requirements,  
• Assumptions and constraints,  
• High-level project description and boundaries,  
• High-level risks,  
• Summary milestone schedule,  
• Summary budget,  
• Stakeholder list,  
• Project approval requirements (i.e., what constitutes project success, who decides the project is successful, and who signs off on the project),  
• Assigned project manager, responsibility, and authority level, and  
• Name and authority of the sponsor or other person(s) authorizing the project charter.  

Scope:

Requirements documentation describes how individual requirements meet the business need for the project. Requirements may start out at a high level and become progressively more detailed as more about the requirements is known. Before being baselined, requirements need to be unambiguous (measurable and testable), traceable, complete, consistent, and acceptable to key stakeholders. The format of a requirements document may range from a simple document listing all the requirements categorized by stakeholder and priority, to more elaborate forms containing an executive summary, detailed descriptions, and attachments.
Components of requirements documentation can include, but, are not limited to:  
• Business requirements, including:  
○ Business and project objectives for traceability;  
○ Business rules for the performing organization; and  
○ Guiding principles of the organisation.  
• Stakeholder requirements, including:  
○ Impacts to other organizational areas;  
○ Impacts to other entities inside or outside the performing organization; and ○ Stakeholder communication and reporting requirements.  
• Solution requirements, including:  
○ Functional and nonfunctional requirements;  
○ Technology and standard compliance requirements;  
○ Support and training requirements;  
○ Quality requirements; and  
○ Reporting requirements, etc. (solution requirements can be documented textually, in models, or both).  
• Project requirements, such as:  
○ Levels of service, performance, safety, compliance, etc.; and ○ Acceptance criteria.  
• Transition requirements.  
• Requirements assumptions, dependencies, and constraints.  

The requirements traceability matrix is a grid that links product requirements from their origin to the deliverables that satisfy them. The implementation of a requirements traceability matrix helps ensure that each requirement adds business value by linking it to the business and project objectives. It provides a means to track requirements throughout the project life cycle, helping to ensure that requirements approved in the requirements documentation are delivered at the end of the project. Finally, it provides a structure for managing changes to the product scope.
Tracing includes, but is not limited to, tracing requirements for the following:
• Business needs, opportunities, goals, and objectives;  
• Project objectives;  
• Project scope/WBS deliverables;  
• Product design;  
• Product development;  
• Test strategy and test scenarios; and  
• High-level requirements to more detailed requirements.  
Attributes associated with each requirement can be recorded in the requirements traceability matrix. These attributes help to define key information about the requirement. Typical attributes used in the requirements traceability matrix may include: a unique identifier, a textual description of the requirement, the rationale for inclusion, owner, source, priority, version, current status (such as active, cancelled, deferred, added, approved, assigned, completed), and status date. Additional attributes to ensure that the requirement has met stakeholders’ satisfaction may include stability, complexity, and acceptance criteria.

(docs, decisions)

Quality:

In the context of achieving ISO compatibility, modern quality management approaches seek to minimize variation and to deliver results that meet defined requirements. These approaches recognize the importance of:
• customer satisfaction. Understanding, evaluating, defining, and managing requirements so that customer expectations are met. This requires a combination of conformance to requirements (to ensure the project produces what it was created to produce) and fitness for use (the product or service needs to satisfy the real needs).  
• Prevention over inspection. Quality should be planned, designed, and built into—not inspected into the project’s management or the project’s deliverables. The cost of preventing mistakes is generally much less than the cost of correcting mistakes when they are found by inspection or during usage.  
• continuous improvement. The PDCA (plan-do-check-act) cycle is the basis for quality improvement as defined by Shewhart and modified by Deming. In addition, quality improvement initiatives such as Total Quality Management (TQM), Six Sigma, and Lean Six Sigma could improve the quality of the project’s management as well as the quality of the project’s product. Commonly used process improvement models include Malcolm Baldrige, Organizational Project Management Maturity Model (OPM3®), and Capability Maturity Model Integrated (CMMI®).  
• Management responsibility. Success requires the participation of all members of the project team.  Nevertheless, management retains, within its responsibility for quality, a related responsibility to provide suitable resources at adequate capacities.  
• cost of quality (coQ).   

(Requirements detail / req wiki, ADG, development workflows / branching strategies)

HR:
A responsibility assignment matrix (RAM) is a grid that shows the project resources assigned to each work package. It is used to illustrate the connections between work packages or activities and project team members. 

One example of a RAM is a RACI (responsible, accountable, consult, and inform) chart.

(GitHub team stuff)

The use of virtual teams creates new possibilities when acquiring project team members. Virtual teams can be defined as groups of people with a shared goal who fulfill their roles with little or no time spent meeting face to
face. The meetings
• • • • • •
availability of communication technology such as e-mail, audio conferencing, social media, web-based and video conferencing has made virtual teams feasible. The virtual team model makes it possible to:
Form teams of people from the same organization who live in widespread geographic areas;
Add special expertise to a project team even though the expert is not in the same geographic area; Incorporate employees who work from home offices;
Form teams of people who work different shifts, hours, or days;
Include people with mobility limitations or disabilities; and
Move forward with projects that would have been ignored due to travel expenses.

(GitHub social, code of conduct - no flame wars or trolls)

Communication:

• Listening actively and effectively;  
• Questioning and probing ideas and situations to ensure better understanding;  
• Educating to increase team’s knowledge so that they can be more effective;  
• Fact-finding to identify or confirm information;  
• Setting and managing expectations;  
• Persuading a person, a team, or an organization to perform an action;  
• Motivating to provide encouragement or reassurance;  
• Coaching to improve performance and achieve desired results;  
• Negotiating to achieve mutually acceptable agreements between parties;  
• Resolving conflict to prevent disruptive impacts; and  
• Summarizing, recapping, and identifying the next steps.  

• Who needs what information, and who is authorized to access that information;  
• When they will need the information;  
• Where the information should be stored;  
• What format the information should be stored in;  
• How the information can be retrieved; and  
• Whether time zone, language barriers, and cross-cultural considerations need to be taken into account.  

The communications management plan is a component of the project management plan that describes how project communications will be planned, structured, monitored, and controlled. The plan contains the following information:
• Stakeholder communication requirements;  
• Information to be communicated, including language, format, content, and level of detail;  
• Reason for the distribution of that information;  
• Time frame and frequency for the distribution of required information and receipt of acknowledgment or response, if applicable;  
• Person responsible for communicating the information;  
• Person responsible for authorizing release of confidential information;  
• Person or groups who will receive the information;  
• Methods or technologies used to convey the information, such as memos, e-mail, and/or press releases;  
• Resources allocated for communication activities, including time and budget;  
• Escalation process identifying time frames and the management chain (names) for escalation of issues that cannot be resolved at a lower staff level;  
• Method for updating and refining the communications management plan as the project progresses and develops;  
• Glossary of common terminology;  
• Flow charts of the information flow in the project, workflows with possible sequence of authorization, list
of reports, and meeting plans, etc.; and  
• Communication constraints usually derived from a specific legislation or regulation, technology, and organizational policies, etc.  

Risk:

Risk Management Plan

Methodology.  
roles and responsibilities.  
Budgeting.  
timing.  
risk categories.  
definitions of risk probability and impact.  
Probability and impact matrix.  
revised stakeholders’ tolerances.  
reporting formats.  
tracking.  

risk management plan (compare these against the standard)  
- Strategies for negative risks or threats; avoid, transfer, mitigate, accept   
- Positive risks or opportunities; exploit, enhance, share, accept  
risk register  
risk reporting  

Procurement:

- hosting  
- industrialising kickstarter / outsourcing / imaging  
- donations  

