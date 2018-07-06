# Resolve multiple binding issue when using Spring Boot with Gradle

When a SpringBoot application startp fails which is using Gradle for build & dependency with issue related to slf4j mulitple binding issue, add the below configuration block in `build.gradle`

### Use Logback instead of Log4j
```
// Exclude log4j and use logback for logging as there is cause of multiple binding exceptions during startup
configurations.all {
   exclude group: "org.apache.logging.log4j"
}
```
