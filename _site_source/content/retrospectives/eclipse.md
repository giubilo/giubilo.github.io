{
    "title": "Eclipse",
    "description": "Using the Eclipse IDE.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "ide", "eclipse", "development" ],
    "status": "edit"
}

_this page is not finished, see the [wiki home page](../wiki) to find out why..._ 


hidden stuff
-rw-r--r--@.DS_Store
-rw-r--r-- .classpath
drwxr-xr-x .git
-rw-r--r-- .gitignore
drwxr-xr-x .gradle
-rw-r--r-- .project
drwxr-xr-x	 .settings

eclipse project import will create some (particulalry if using the gradle plugin)
gradle build will create some
.gitignore is also in the Atlassian SourceTree global gitignore (there is a decision here about whether or not to store the .gitignore stuff in the reporsitory to maintain consistency across the team - prob would put in a dev note so that could have the best of both worlds in case someone is working on a few projects and have different things in their gitignore - although could prob have a base one in here that includes the .gitignore file as well so it doesn't get changed back on commit - would have to add manually through the GitHub gui I think)


No matter how advanced system modelling and code generation gets there's seems to be no escaping the need to hand write some code.  So, we could have broken out our favourite text editor (Xcode, Sublime, Notepad, vi, joe, nano), interpreter / compiler, debugger, command line to package and read logs, manuals, specs, html editor, documentation editor, xml editor...but chose instead to take a sec to look at using an open source [Integrated Development Environment](http://en.wikipedia.org/wiki/Integrated_development_environment) (IDE).  

In one interface (with multiple perspectives) we get a ton of [resources](./HowTo:-setting-up-project-resources) to help with the [tasks of the project](http://www.ibm.com/developerworks/opensource/tutorials/os-perlecl/section2.html) including; 

* writing code (there'll be all sorts - perl, xml, html, text, makefile, markdown code)
* formatting code so it's readable, valid and conforms to best practice techniques for the language (like project structures)
* execute and debug the code (postmortem/live/cgi-remote)
* build/package/implement code
* get help writing internal comments, documentation and todo's
* get access to documentation (like perldoc for modules)

Wow, that's a lot of things, but which one to choose?  There are heaps of IDE's out there.  We have chosen [Eclipse](http://www.eclipse.org) because; there's tons of documentation, examples and community surrounding it.  Also, because we have also chosen Perl as a development language for the CmisDlnaConnector and Git (GitHub) for source control, Eclipse is a good choice for us because it has really cool plugins [EPIC](http://www.epic-ide.org) and [EGit](http://www.eclipse.org/egit/) to support both of them.

## Steps

1. Getting and configuring Eclipse
1. Getting and configuring Epic
1. Getting and configuring EGit
1. Importing projects

### Getting and configuring Eclipse

Downloaded [Eclipse Kepler (4.3.1)](http://www.eclipse.org/downloads/) for MacOSX (and can get a Windows and Linux one as well).  

It comes as an archive which we unstuffed. Then [drag](http://www.imdb.com/title/tt0109045/) the "eclipse" folder into your Applications folder. [The easiest way to do so](http://www.cs.dartmouth.edu/~cs5/install/eclipse-osx/) is to open a new window in the Finder and click on Applications in the list you get on the left-hand side. Then drag the "eclipse" folder in with the other applications. Make sure that you do not drag it into a folder that's already within Applications. In other words, when you're done, the Applications folder should have directly within it a folder named "eclipse."
(This step is not required, but handy.) Double click the "eclipse" folder. You'll see an application named "Eclipse"; it has a purple icon with white horizontal stripes. Drag it into your dock. Now you will be able to launch Eclipse by clicking on the icon in the dock.

Launch the application and set up the default workspace preferences (we've just put it in the ~/Documents/workspace folder ).

Didn't really do any other configuration as most of the preferences that are important to us are in the Epic and EGit plugins.  Didn't look at many support docs to get going as its pretty self explanatory but the [basic tutorial](http://help.eclipse.org/kepler/topic/org.eclipse.platform.doc.user/gettingStarted/qs-01.htm?cp=0_1_0) and some descriptions of the [icons](http://help.eclipse.org/kepler/index.jsp?topic=/org.eclipse.jdt.doc.user/reference/ref-icons.htm) were useful (if could find a similar icons ref for Epic that would be cool). 

### Getting and configuring Epic

Even though the project repository is foundational, we've put this section in before setting up EGit as when we connect to the repo and import projects we wanted to import them as Perl projects (and wanted Perl frameworks and Epic plugin installed first to do this).

And, in order to have all EPIC [features](http://www.epic-ide.org/articles.php) like template project model (Module::Starter), source formatting (PerlTidy), syntax checking, coding standards (PerlCritic), interactive debug etc., you need to have a [Perl interpreter and some supporting perl modules installed](./Paint-by-numbers:-Perl). 

The Epic [installation](http://www.epic-ide.org/guide/ch01s02.php) is done by using the Eclipse Update Manager by entering 'epic - http://e-p-i-c.sf.net/updates/testing' into the “Help > Install new software” dialog.  Chose the testing version 'cause saw some posts that said it was stable and had good advantages over the current released version (and who doesn't like a shiny new toy).

Once the plugin is installed, updated the "Eclipse > Preferences > Perl EPIC" preferences:

> Perl EPIC: 
>   ~ Perl Executable: "/usr/bin/perl"  
>   ~ Interpreter Type: Standard  
> Module::Starter:  
>   ~ Select Enable Module::Starter  
>   ~ Custom location: /usr/local/bin/module-starter  
>   ~ Select Override module-starter config file  
>   ~ Module Author:  
>   ~ Module Author Email:  
> Perl::Critic:  
>   ~ Select Enable Critic  
>   ~ Custom location: /usr/local/bin/perlcritic  

That's the ones we tweaked but there are heaps of other ones as well.

So now you've got the [eagles nest](http://www.imdb.com/title/tt0659325/) for a birds eye view of the project.  The main structure of Eclipse are perspectives.  _Perspectives control what appears in certain menus and toolbars. They define visible action sets, which you can change to customize a perspective. You can save a perspective that you build in this manner, making your own custom perspective that you can open again later._
_You can set your Workbench preferences to open perspectives in the same window or in a new window._

The main perspectives for developing Perl applications are:
* Perl - This is the main perspective for coding Perl scripts.  
* Debug - Provides the main functionality for debugging and executing Perl scripts.  

Did have an error setting up EPIC;

>“An internal error occurred during: "Launching MyRSSFeeder".java.lang.NullPointerException"  

This happened because had mistakenly set the interpreter type in the Perl EPIC preferences to 'cygwin'. Need to make sure use the “Standard” Interpreter type. 

### Getting and configuring EGit

The [download page](http://www.eclipse.org/egit/download/) for EGit says to; _install via one of the update site URLs listed below, copy and paste it into the “Help > Install new software” dialog_.

There is a [huge user guide](http://wiki.eclipse.org/EGit/User_Guide) for EGit.  We skimmed it.

Once installed go to the Eclipse > Preferences menu and set the >Team>Git Default repository folder: which we set to the Eclipse workspace directory /Documents/workspaces (it will actually go into each imported project's folder).  The other settings within Eclipse will get set when you actually import projects (and these will be stored in ~/.gitconfig).  The later section on importing projects will detail other settings.

### Importing projects

Now, you can connect Eclipse through EGit to a locally cloned repository (like one cloned by the Git commandline client or graphical client), which will give you an Eclipse workspace, a local Git repo and an online Git repo.  We have chosen to clone directly into the Eclipse workspace area so only have the Eclipse workspace directory for the project (like /Documents/workspace/allegria) which will have a hidden .git directory in it with relevant repo config files.  

To do this you will need to:

* prepare for [ssh connection](http://wiki.eclipse.org/EGit/User_Guide#Eclipse_SSH_Configuration)  
* [clone a remote repository](http://wiki.eclipse.org/EGit/User_Guide#Working_with_remote_Repositories)

The ssh connection was a bit tricky and when doing it we got a few error messages.  

* the first error message was a problem with validation and there are many [posts](http://stackoverflow.com/questions/3225862/multiple-github-accounts-ssh-config) describing the need to create a ~.ssh/config file (the ~.ssh directory is the same directory that the ssh keys are stored).  We used our favourite editor to create ~.ssh/config with the following entries;

```
    Host github.com  
    HostName github.com  
    User git  
    PreferredAuthentications publickey  
    IdentityFile ~/.ssh/id_rsa  
```

* the second error was about [permission denied public key](https://help.github.com/articles/error-permission-denied-publickey) and related to the 'User' entry in the ~.ssh/config file, initially we were using the username for the repo but need to use the generic 'git' user name.

* a third error concerned the need to fix the [permissions on id_rsa key files]
(http://www.howtogeek.com/168119/fixing-warning-unprotected-private-key-file-on-linux/) by resetting them back to default;

```
    sudo chmod 600 ~/.ssh/id_rsa  
    sudo chmod 600 ~/.ssh/id_rsa.pub  
```

Once have prepared the ssh connection then can clone the remote repo by choosing "File > Import > Git > Project from Git" and then on the next screen select Clone URI.  Paste in the URI from the repo (in our case github.com/peterwatts/allegria) and select protocol ssh (this will change the URI to ssh://github.com/peterwatts/allegria).  Choose the branches on the next screen and select a directory in the next (in our case ~/Documents/workspace/).  Will then ask you 'import projects' which you can select and do.

Choose the New Project Wizard (as the other two options; 'Import existing projects' and 'Import as general project' will cause an error as they probably don't have the necessary eclipse setting files).