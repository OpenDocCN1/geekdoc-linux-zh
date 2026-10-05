# 196 · CHAPTER 13

```
# 1) It frees up your command window
# 2) You should use 'stop' option instead of ^C to bring down the server
if [ "$1" = "start" ]; then
shift
echo Using classpath: ${CLASSPATH}
if [ "$1" = "-security" ]; then
shift
echo Starting with a SecurityManager
$JAVACMD TOMCAT_OPTS -Djava.security.manager
-Djava.security.policy=${TOMCAT_HOME}/conf/tomcat.policy
-Dtomcat.home=${TOMCAT_HOME} org.apache.tomcat.startup "$0" & \
else
$JAVACMD TOMCAT_OPTS -Dtomcat.home=${TOMCAT_HOME}
org.apache.tomcat.startup "$0" & \i
$JAVACMD TOMCAT_OPTS -Dtomcat.shell.Startup "$0" &

elif [ "$1" = "stop" ]; then
shift
echo Using classpath: ${CLASSPATH}
$JAVACMD TOMCAT_OPTS -Dtomcat.home=${TOMCAT_HOME}
org.apache.tomcat.startup -stop "$0"
# stop
org.apache.tomcat.shell.Shutdown "$0"

elif [ "$1" = "run" ]; then
shift
echo Using classpath: ${CLASSPATH}
if [ "$1" = "-security" ]; then
shift
echo Starting with a SecurityManager
$JAVACMD TOMCAT_OPTS -Djava.security.manager
-Djava.security.policy=${TOMCAT_HOME}/conf/tomcat.policy
-Dtomcat.home=${TOMCAT_HOME} org.apache.tomcat.startup "$0" & \
else
$JAVACMD TOMCAT_OPTS -Dtomcat.home=${TOMCAT_HOME}
org.apache.tomcat.startup "$0" & \i
$JAVACMD TOMCAT_OPTS -Dtomcat.shell.Startup "$0"
# no &\n
elif [ "$1" = "ant" ]; then
shift
$JAVACMD $ANT_OPTS -Dtomcat.home=${TOMCAT_HOME} -Dtomcat.home=${TOMCAT_HOME}
org.apache.tools.ant.Main $0

elif [ "$1" = "jsp" ]; then
shift
$JAVACMD $JSPC_OPTS -Dtomcat.home=${TOMCAT_HOME} org.apache.jasper.JspC "$0"

elif [ "$1" = "env" ]; then
# # Call it with source tomcat.sh to set the env for tomcat
shift
echo Setting classpath to: ${CLASSPATH}
oldCP=${CLASSPATH}
else
echo "Usage:"
```

Figure 13.4: Apache's Tomcat script uses many of the features of shell script programming (part 3 of 4).