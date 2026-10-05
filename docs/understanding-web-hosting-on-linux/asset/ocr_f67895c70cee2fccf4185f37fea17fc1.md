If the Tomcat home environment variable was not set, the next block tries to see if it is under the conventional opt directory, either under the user's home directory or the root directory, with the following two conditions:

```
if [ ${HOME}/opt/tomcat/conf ]; then
if [ -d /opt/tomcat/conf ]; then
```

In the third and final "Tomcat home is blank", the tomcat.sh script echoes a message and gives up, with an exit code of one. Tomcat then checks for the existence of three optional environment variables: STOMAC_OPTS, SANT_OPTS, and SJSPSC_OPTS. If any of those environment variables does not exist, Tomcat creates them with empty string values.

# Which Java

The next problem that the Tomcat shell script has to handle is finding Java's home directory. If the system already has the JAVA_HOME environment variable set, this isn't a problem at all. When the following predicate is true, however, tomcat.sh attempts to find Java's home directory by asking the which command to find the java command:

```
if -z "JAVA_HOME" ]; then
```

As long as the Java home block of code doesn't exit, the next block checks for the existence of an environment variable called JAVACMD. Tomcat allows users to qualify the Java command string with site-specific Java command flags. If the JAVACMD variable does not exist, tomcat.sh sets it to the qualified location of the java command

# Classpath

The next four blocks of code set the Java environment variable, CLSPATH. Tomcat begins this chunk by politely saving the existing value of CLSPATH in oldCP. When tomcat.sh completes processing, CLSPATH is set back to its original value.

The value for CLSPATH is saved, the environment variable is destroyed with the unset command. The for loop that follows rebuilds CLSPATH:

```
for i in ${TOMCAT_HOME}/lib/* ; do
```

The body of the for loop appends the name of every file in Tomcat lib directory to CLSPATH. Those files are the Java archives that contain the Java code required to run Tomcat.

The next code block handles a discrepancy between the way Java works between JDKs 1.1 and 1.2. JDK 1.2 requires the tools.jar file to be in CLSPATH. Tomcat determines a JDK1.2 environment with the following predicate:

```
if [ -f ${JAVA_HOME}/lib/tools.jar ]; then
```