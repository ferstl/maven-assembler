# Maven Assembler
The Maven Assembler is a simple maven assembly that allows you to create your own customized maven distribution.

What's the difference to the original maven distribution at
[maven.apache.org](http://maven.apache.org)?
* It contains your customized `settings.xml` that fits to your build environment
* More restrictive file permissions, i.e. no world-writable directories
* more package formats besides zip and tar.gz (any format that the `maven-assembly-plugin supports`)

## How to use it
These commands will create a maven distribution as `tar.gz` with your own `settings.xml`
---
# Provide the maven version and the location of the settings.xml you want to use
mvn package -DmavenVersion=3.0.4 -DsettingsUrl=/Users/me/maven-config/settings.xml

# The url to the settings.xml can also be a remote location
mvn package -DmavenVersion=3.0.4 -DsettingsUrl=http://svn.example.com/svn/settings.xml
---

These are all properties that you can use:
|Name|Required|Default Value|Description|
|----|---------|------------|:-----------|
|`mavenVersion`|yes|n/a|The maven version to use|
|`settingsUrl`|yes|n/a|The `settings.xml` to put into your maven distro|
|`settingsFileName`|maybe|n/a|You need to define this property if your `settings.xml` has a different name than `settings.xml`|
|`format`|no|`tar.gz`|The package format of your maven distro|
|`finalName`|no|`apache-maven-<version>-bin-<format>`|The final name of your maven distro|
