# Maven Assembler
The Maven Assembler is a simple maven assembly that allows you to create your own customized maven distribution.

What's the difference to the original maven distribution at
[maven.apache.org](http://maven.apache.org)?
- It contains your customized `settings.xml` that fits to your build environment
- More restrictive file permissions, i.e. no world-writable directories and files
- more package formats besides zip and tar.gz (any format that the `maven-assembly-plugin` supports)

## How to use it
These commands will create a maven distribution as `tar.gz` package:

    # Provide the maven version and the folder where your settings.xml resides
    mvn package -DmavenVersion=3.0.4 -DsettingsUrl=/Users/me/maven-config
 
    # The url can also be a remote location (protocol needs to be supported by the wagon-maven-plugin)
    mvn package -DmavenVersion=3.0.4 -DsettingsUrl=http://svn.example.com/svn/my-repo
    
    # Use the settingsFileName property in case your maven settings are stored in a file that is not called settings.xml
    mvn package -DmavenVersion=3.0.4 -DsettingsUrl=http://svn.example.com/svn/my-repo -DsettingsFileName=my-settings.xml

These are all properties that you can use:

| Name | Required | Default Value | Description |
| :--- | -------- | ------------- | :---------- |
| `mavenVersion` | yes | n/a | The maven version to use |
| `settingsUrl` | yes | n/a | The `settings.xml` to put into your maven distro |
| `settingsFileName` | maybe | `settings.xml` | Use this property if your maven settings file has another name than `settings.xml` |
| `format` | no | `tar.gz`| The package format of your maven distro |
| `finalName` | no | `apache-maven-<mavenVersion>-bin`| The final name of your maven distro |
