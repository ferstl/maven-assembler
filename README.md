# Maven Assembler
The Maven Assembler is a simple maven assembly that allows you to create your own customized maven distribution.

What's the difference to the original maven distribution at
[maven.apache.org](http://maven.apache.org)?
- It contains your customized `settings.xml` that fits to your build environment
- More restrictive file permissions, i.e. no world-writable directories and files
- more package formats besides zip and tar.gz (any format that the `maven-assembly-plugin` supports)

## How to use it
Get the latest version of the Maven Assembler:

    git clone -n https://github.com/ferstl/maven-assembler.git
    git checkout maven-assembler-<latest-version>

Each of these commands will create a maven distribution as `tar.gz` package:

    # Provide the maven version and the folder where your settings.xml resides
    mvn package -DmavenVersion=3.0.4 -DsettingsUrl=file:///Users/me/maven-config
 
    # The URL can also be a remote location (protocol needs to be supported by the wagon-maven-plugin)
    mvn package -DmavenVersion=3.0.4 -DsettingsUrl=https://raw.github.com/me/my-repo
    
    # Use the settingsFileName property in case your maven settings are stored in a file that is not called settings.xml
    mvn package -DmavenVersion=3.0.4 -DsettingsUrl=https://raw.github.com/me/my-repo -DsettingsFileName=my-settings.xml

These are all properties to run the Maven Assembler:

| Name | Required | Default Value | Description |
| :--- | -------- | ------------- | :---------- |
| `mavenVersion` | yes | n/a | The maven version to use |
| `settingsUrl` | yes | n/a | The URL to the folder containing your `settings.xml` to use for your maven distro |
| `settingsFileName` | no | `settings.xml` | Use this property if your maven settings file has another name than `settings.xml` |
| `format` | no | `tar.gz`| The package format of your maven distro |
| `finalName` | no | `apache-maven-<mavenVersion>-bin`| The final name of your maven distro |
| `skip` | no | `false`| Skip creation of the maven distro. Useful for `mvn deploy` or `mvn release:xxx` |
