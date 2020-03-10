JBoss Community IDE Configuration Files
=======================================
The directories below contain instructions, and IDE configuration files for eclipse, IDEA, and NetBeans.  See below for additional information.

IDE Agnostic Conventions
------------------------

*Formatting Java Files*

* JavaDoc parameter information is on the same line, not indented
* Line length is 120 characters
* Spaces are used instead of tabs
* Indentation size is 4
* Switch blocks are indented 
 
*Formatting Other Files*

* Line length is 120 characters
* Spaces are used instead of tabs
* Indentation size is 4

Projects following these conventions
------------------------------------

* [JBoss-AS](https://github.com/jbossas)
* [RichFaces](https://github.com/richfaces)
* TODO

If your JBoss project follows these conventions,
[fork and edit this file](https://github.com/jboss/ide-config/edit/master/README.md) and add your project.


# Intellij setup with the eclipse formatter xml

1. On Intellij, install the 'Eclipse Code Formatter' plugin
2. Restart Intellij for the plugin to be installed
3. Click on File -> Settings -> Other Settings -> Eclipse Code Formatter
4. Select 'Use the Eclipse Code Formatter' option on the top
5. On the 'Eclipse Java Formatter config file' section, specify the path to the eclipse formatter xml file (ide-config/eclipse/jboss-java-formatter.xml)
6. Finally, click 'OK'. When formatting your code, it'll format according to the recommened codestyle now

PS: we are not using the built-in Intellij 'Eclipse import Java codestyle' since it is lacking in a lot of places and the formatting is not a good representation of what we have in Eclipse.
