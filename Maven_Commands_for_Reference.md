# Maven Commands for Reference

## References
* [Apache Maven](http://maven.apache.org/guides/getting-started/index.html)

## Usual Commands
* `mvn clean` - Remove the target directory with all the build data before starting so that it is fresh
* `mvn clean install` - Use this command to invoke the clean lifecycle and the build lifecycle.
* `mvn clean deploy` - Use this command to cleanly build and deploy artifacts into the shared repository
* `mvn install -Dmaven.test.skip=true` - Use this command to skip compiling and invoking tests during build phase
* `mvn dependency:tree -Dverbose -Dincludes=log4j:log4j` - Use this command to get the dependency tree for the provided artifact. This is helpful to know which library is trying to refer to log4j indirectly.

## Build Lifecycle Phases
* `mvn validate` - Validate the project is correct and all necessary information is available
* `mvn compile` - Compile the source code of the project
* `mvn test` - Test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
* `mvn package` - Take the compiled code and package it in its distributable format, such as a JAR.
* `mvn verify` - Run any checks on results of integration tests to ensure quality criteria are met
* `mvn install` - Install the package into the local repository, for use as a dependency in other projects locally
* `mvn deploy` - Done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

# Maven Plugins

## Jetty Plugin

## Mobertura Plugin

## Checkstyle Plugin

## PMD Plugin
