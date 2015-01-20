{
    "title": "Launchng OSX scripts",
    "description": "Creating launchers in OSX.",
    "date": "2014-02-01",
    "categories" : [
    	 "posts"
    ],
    "tags": [ "osx", "automation" ],
    "status": "research"
}

<html>
<table border="0">
<tr>
  <td>
    <p>
      <img src="./images/paint-by-numbers.png?raw=true" alt="book">
    </p>
  </td>
  <td>
    <p>This paint by numbers has used:</p>
    <p><b>Alfresco 4.2</b></p>
    <p><b>CMIS Workbench 0.9.0-beta-1 & 0.10.0</b></p>
  </td>
</tr>
</table> 
</html> 

The CMIS Workbench application in its default download launches with a shell script rather than a neat osx package.  The osx Automator can be used to launch it from an icon in the osx launchpad or dock.   

## Steps 

**1.** Create an 'application' from the osx Automator:  

![automator](/assets/img/mac-osx-automator-type.png?raw=true)  

**2.** Drag run shell script to the action window and enter the path to workbench.sh:  

![action](/assets/img/mac-osx-automator.png?raw=true)  

**3.** Save the package as 'CMIS Workbench.app' to the 'Applications' folder.  

**4.** Go to the 'Applications' folder, right-click on the 'CMIS Workbench.app' file,'Get Info'and and click on the icon at the top left until it has a blue outline:  

![finder](/assets/img/mac-osx-getinfo.png?raw=true)

**5.** [Download](https://svn.apache.org/repos/asf/chemistry/opencmis/trunk/chemistry-opencmis-workbench/chemistry-opencmis-workbench/src/main/resources/images/) the CMIS Workbench icon (or use the pic below), open it in a paint application, copy to the clipboard and use the Finder [Edit] menu to paste the CMIS Workbench icon onto the 'Get Info' icon.  

![icon](/assets/img/cmis-wb-icon.png?raw=true)  