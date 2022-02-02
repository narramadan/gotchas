# Java JVM Tuning Gotchas

`ps -ef` - Command to list jvm stats

Below are some useful links:
* https://www.oracle.com/technical-resources/articles/java/g1gc.html
* https://blog.cloudera.com/tuning-java-garbage-collection-for-hbase/
* https://docs.docker.com/config/containers/resource_constraints/

Tomcat JVM tuning in setenv.sh

```
#!/usr/bin/env sh
HOSTNAME="$(</etc/hostname)"
export JAVA_HOME="/etc/java11/jre_11"
export JAVA_OPTS="${JAVA_OPTS} -Djava.net.preferIPv4Stack=true"
export JAVA_OPTS="${JAVA_OPTS} -XX:HeapDumpPath=/local"
export JAVA_OPTS="${JAVA_OPTS} -XX:+HeapDumpOnOutOfMemoryError"
export JAVA_OPTS="${JAVA_OPTS} -XX:+UnlockExperimentalVMOptions"
export JAVA_OPTS="${JAVA_OPTS} -XX:+ExitOnOutOfMemoryError"
export JAVA_OPTS="${JAVA_OPTS} -XX:InitialRAMPercentage=50.0"
export JAVA_OPTS="${JAVA_OPTS} -XX:MinRAMPercentage=40.0"
export JAVA_OPTS="${JAVA_OPTS} -XX:MaxRAMPercentage=75.0"
export JAVA_OPTS="${JAVA_OPTS} -XX:MaxHeapFreeRatio=60"
export JAVA_OPTS="${JAVA_OPTS} -XX:+ScavengeBeforeFullGC"
export JAVA_OPTS="${JAVA_OPTS} -XX:+CMSScavengeBeforeRemark"
export JAVA_OPTS="${JAVA_OPTS} -XX:+UseSerialGC"
export JAVA_OPTS="${JAVA_OPTS} -XX:+PrintFlagsFinal"
export JAVA_OPTS="${JAVA_OPTS} -XX:TieredStopAtLevel=1"
export JAVA_OPTS="${JAVA_OPTS} -Djava.security.egd=file:/dev/./urandom"
export JAVA_OPTS="${JAVA_OPTS} -Dlog4j2.formatMsgNoLookups=true"
export SECURITY_MANAGER="false"
export SHUTDOWN_WAIT="5"
export SHUTDOWN_VERBOSE="false"
export JARS="{{ catalina_base }}"
export CLASSPATH="$JARS/log4j2/lib/*:$JARS/log4j2/conf:"
export CATALINA_OPTS="${CATALINA_OPTS} -Djava.security.egd=file:/dev/./urandom"
export CATALINA_PID="/var/run/tomcat/tomcat.pid"
export CATALINA_OPTS="${CATALINA_OPTS} -Xlog:gc*:file=/logs/${API_SVC_NAME}/${HOSTNAME}/gc.log:tags,uptime,time,level:filecount=5,filesize=2048000"
export CATALINA_OPTS="${CATALINA_OPTS} -Dgateway.host=${GATEWAY_HOST}"
export CATALINA_OPTS="${CATALINA_OPTS} -Dgateway.scheme=${GATEWAY_SCHEME:-https}"
export CATALINA_OPTS="${CATALINA_OPTS} -Dgateway.port=${GATEWAY_PORT:-443}"

#Only set for Log4j debugging# export CATALINA_OPTS="${CATALINA_OPTS} -Dlog4j.debug"
## https://logging.apache.org/log4j/2.x/manual/async.html
export CATALINA_OPTS="${CATALINA_OPTS} -Dlog4j2.contextSelector=xxx.xxx.xxx.xxxContextSelector"
```
