# Continuous Integration for Classroom Assignments
Through building Gradle projects in IntelliJ IDEA to be tested through Travis CI, this guide will introduce test-driven development facilitated by practicing continuous integration.
## Configuring an Existing Project
1. Add the given build.gradle file to the project’s main directory. Note that the SourceSets naming the main and test directories will be marked as the appropriate modules once the project has been imported into IntelliJ.

`build.gradle`
```
/** build.gradle file */

apply plugin: 'java'

sourceCompatibility = 1.8

// Define source sets which deviate from the default setup expected in Gradle projects
sourceSets {
    main {
         java {
              srcDir 'src'
              }
         }
    test {
         java {
              srcDir 'test'
              }
         }
}

// Define external dependencies using Maven
repositories {
    mavenCentral()
}

// Access JUnit testing library
dependencies {
    testCompile group: 'junit', name: 'junit', version: '4.12'
}
```

2. Create or modify the project’s .gitignore file as written in the following:

`.gitignore`
```
### Java template  ###

# Compiled class file
*.class

# Log file
*.log

# BlueJ files
*.ctxt

# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files ###
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar

# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*

### Gradle template ###

.gradle
/build/

# Ignore Gradle GUI config
gradle-app.setting

# Avoid ignoring Gradle wrapper jar file (.jar files are usually ignored)
!gradle-wrapper.jar

# Cache of project
.gradletasknamecache

# # Work around https://youtrack.jetbrains.com/issue/IDEA-116898
# gradle/wrapper/gradle-wrapper.properties

### Ignore IntelliJ ###
.idea
*.iml
```

3. From the IntelliJ IDEA ‘Welcome’ screen, select Import Project, locate the project’s main directory, and select the build.gradle file that had just been created. Selecting the file directly guarantees that the IDE will recognize the project as a Gradle project.

4. On the Import Project from Gradle page, uncheck Create separate module per source set, and select the radio button for Use default gradle wrapper. This allows students to use Gradle without having to install it manually.

5. Proceed with the remaining import settings for the project to complete its importation. Create or push changes to its repository in the class’s GitHub organization.

6. Access GitHub Classroom and create a new individual assignment using the repository that had just been created under **Add your starter code from GitHub**.

7. Access travis-ci.com. Select the (+) next to My Repositories and select Sync account. Locate the project as listed, and toggle the tick mark to the left of it.

8. For Travis to recognize the project and begin testing, commit and push with the given .travis.yml file in the main directory. This is a simple build that runs and tests based on the project’s Gradle script.

`.travis.yml`
```
install: gradle wrapper --gradle-version 4.2

language: java

jdk:
  - oraclejdk8
```
