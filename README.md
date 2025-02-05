ProjectNCL IDE Configuration Files
=======================================

The directories below contain instructions and IDE configuration files for Eclipse.  See below for additional information.

This was originally based upon https://github.com/jboss/ide-config and https://github.com/quarkusio/quarkus/blob/main/independent-projects/ide-config/src/main/resources/eclipse-format.xml


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


## Intellij setup with the eclipse formatter xml

1. On Intellij, install the 'Eclipse Code Formatter' plugin
2. Restart Intellij for the plugin to be installed
3. Click on File -> Settings -> Other Settings -> Eclipse Code Formatter
4. Select 'Use the Eclipse Code Formatter' option on the top
5. On the 'Eclipse Java Formatter config file' section, specify the path to the eclipse formatter xml file (ide-config/eclipse/jboss-java-formatter.xml)
6. Finally, click 'OK'. When formatting your code, it'll format according to the recommened codestyle now

PS: we are not using the built-in Intellij 'Eclipse import Java codestyle' since it is lacking in a lot of places and the formatting is not a good representation of what we have in Eclipse.


# Integration With Maven

There are a couple of options using either `net.revelc.code.formatter:formatter-maven-plugin` or `com.diffplug.spotless:spotless-maven-plugin`.

Note that there is **no** need to store a local copy of the formatter (any of those can be removed).

## revelc:formatter

A typical pom could contain:

```
<properties
   <formatter-maven-plugin.version>2.24.1</formatter-maven-plugin.version>
   <impsort-maven-plugin.version>1.12.0</impsort-maven-plugin.version>
   <format.skip>false</format.skip>
</properties>

<plugin>
  <groupId>net.revelc.code.formatter</groupId>
  <artifactId>formatter-maven-plugin</artifactId>
  <version>${formatter-maven-plugin.version}</version>
  <dependencies>
    <dependency>
      <groupId>org.jboss.pnc</groupId>
      <artifactId>ide-config</artifactId>
      <version>1.1.0</version>
    </dependency>
  </dependencies>
  <configuration>
    <!-- store outside of target to speed up formatting when mvn clean is used -->
    <cachedir>.cache/formatter-maven-plugin-${formatter-maven-plugin.version}</cachedir>
    <configFile>java-formatter.xml</configFile>
    <lineEnding>LF</lineEnding>
    <skip>${format.skip}</skip>
  </configuration>
</plugin>
<plugin>
  <groupId>net.revelc.code</groupId>
  <artifactId>impsort-maven-plugin</artifactId>
  <version>${impsort-maven-plugin.version}</version>
  <configuration>
    <!-- store outside of target to speed up formatting when mvn clean is used -->
    <cachedir>.cache/impsort-maven-plugin-${impsort-maven-plugin.version}</cachedir>
    <groups>java.,javax.,jakarta.,org.,com.</groups>
    <staticGroups>*</staticGroups>
    <lineEnding>LF</lineEnding>
    <skip>${format.skip}</skip>
    <removeUnused>true</removeUnused>
  </configuration>
</plugin>
```

Note that configuration for `impsort-maven-plugin` has also been added as its a common extra with `formatter-maven-plugin`.

## spotless

A typical pom could contain:

```
<properties
   <spotless-maven-plugin.version>2.44.2</spotless-maven-plugin.version>
</properties>

<plugin>
  <groupId>com.diffplug.spotless</groupId>
  <artifactId>spotless-maven-plugin</artifactId>
  <version>${spotless-maven-plugin.version}</version>
  <dependencies>
    <dependency>
      <groupId>org.jboss.pnc</groupId>
      <artifactId>ide-config</artifactId>
      <version>1.1.0</version>
    </dependency>
  </dependencies>
  <configuration>
    <java>
      <removeUnusedImports/>
      <importOrder>
        <file>java-import-order.txt</file>
      </importOrder>
      <eclipse>
        <file>java-formatter.xml</file>
      </eclipse>
      <lineEndings>UNIX</lineEndings>
    </java>
  </configuration>
  <executions>
    <execution>
      <goals>
        <goal>apply</goal>
      </goals>
      <phase>compile</phase>
    </execution>
  </executions>
</plugin>
```
