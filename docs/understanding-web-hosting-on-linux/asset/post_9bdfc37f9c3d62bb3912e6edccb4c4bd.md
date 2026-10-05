
# Shell Programming · 193

```bash
case expression in
  pattern1)
    statements ;;
  pattern2)
    statements ;;
  *)
    statements that handle drop-through cases ;;
esac
```

The asterisk handles those circumstances where the value of expression has no associated pattern. Programmers typically call this portion of the case statement the drop-through case.

A working example of a script that uses the case statement Apache Apache http script (which, on a Red Hat system, can be found in the /etc/rc/init.d directory). The portion of the script that predicates processing based on parameter $1 is shown in Figure 13.3.

```bash
case "$1" in
  start)
    ;
  stop)
    ;
  status)
    status $httpd
    ;
  restart)
    stop
    start
    ;
  reload)
    echo -n"Reloading $prog"
    killproc $httpd -HUP
    RETRIEVAL=$7
    echo
    ;
  condrestart)
    if [ -f /var/run/httpd.pid ]; then
      stop
      start
    fi
    ;
  echo $"Usage: $prog {start|stop|restart|reload|condrestart|status}"
  exit 1
esac
```

Figure 13.3: Apache's httpd script uses a case statement to handle its various parameter options.

# Tomcat Code Review

A good way to show the power of shell programming is to review Apache's Tomcat script. The script is called tomcat.sh and is located under the bin directory where Tomcat is installed (/opt/jakarta-tomcat on our system). The tomcat.sh script shown in Figure 14.3 is devoid of comment (except for the first line), so it might be worthwhile to add comments to the script as you step through the code.

```bash
#!/bin/sh
#
# $Id: tomcat.sh v.1.17.2.2 2001/01/10 22:55:48 glenn Exp $

# Shell script to start and stop the server

# There are other, simpler commands to startup the runner. The two
# commented commands are good replacements. The first works well with
# Java Platform 1 based runtimes. The second works well with
# Java2 Platform based runtimes.

# -jcp runner.jar:servlet.jar:classes org.apache.shell.Startup $
# java -jcp runner.jar:servlet.jar:classes org.apache.shell.Startup $
if [ -f ${HOME}/tomcat ]; then
    ${HOME}/tomcat
fi

if [ "${TOMCAT_HOME}" = "" ]; then
    # resolve links
    # $0 may be a link to home
    PRG=$0
    progname=$(basename $0)

    while [ -h "$PRG" ]; do
        link=$(ls -ld "$PRG" | awk '{print $9}' | sed 's/.*\///')
        if echo "$link" | grep -q /dev/null; then
            PRG="$link"
        else
            PRG="$(dirname "$PRG")/$link"
        fi
    done

    TCAT_HOME_1=$(dirname "$PRG")
    echo "Guessing Tomcat_HOME from tomcat.sh to \${TOMCAT_HOME_1}"
    if [ -d \${TOMCAT_HOME_1}/conf ]; then
        TOMCAT_HOME=\${TOMCAT_HOME_1}
        echo "Setting Tomcat_HOME to \${TOMCAT_HOME}"
    fi

    if [ "${TOMCAT_HOME}" = "" ]; then
        # try to find tomcat
        if [ -d \${HOME}/opt/tomcat/conf ]; then
            TOMCAT_HOME=\${HOME}/opt/tomcat
            echo "Defaulting TOMCAT_HOME to \${TOMCAT_HOME}"
        fi
    fi

    if [ -d /opt/tomcat/conf ]; then
        TOMCAT_HOME=/opt/tomcat
        echo "Defaulting TOMCAT_HOME to \${TOMCAT_HOME}"
    fi

    # Add other "standard" locations for tomcat
if [ "${TOMCAT_HOME}" = "" ]; then
    echo TOMCAT_HOME not set, you need to set it or install it in a standard location
    exit 1
fi

if [ "${TOMCAT_OPTS}" = "" ]; then
    TOMCAT_OPTS=""
fi

if [ "${ANT_OPTS}" = "" ]; then
    ANT_OPTS=""
fi

if [ "${JSPC_OPTS}" = "" ]; then
    JSPC_OPTS=""
fi

if [ -z "$JAVA_HOME" ]; then
    JAVA=$(which java)
    if [ -z "$JAVA" ]; then
        echo "Cannot Find JAVA. Please set your PATH."
        exit 1
    fi
    JAVA_BINDIR=$(dirname $JAVA)
fi

if [ "$JAVACMD" = "" ]; then
    # it may be defined in env flags!
    JAVACMD=$JAVA_HOME/bin/java
fi

oldCP=$CLASSP
unset CLASSP
for i in ${TOMCAT_HOME}/lib/*; do
    if [ "$CLASSP" = "" ]; then
        CLASSP=$i
    else
        CLASSP=$CLASSP:$i
    fi
done

if [ -f ${JAVA_HOME}/lib/tools.jar ]; then
    # We are probably in a JDK 1.2 environment
    CLASSP=$CLASSP:${JAVA_HOME}/lib/tools.jar
fi

# Backdoor for development purposes when classes are compiled but not yet jarred.
if -d ${TOMCAT_HOME}/classes ]; then
    CLASSP=$CLASSP:${TOMCAT_HOME}/classes
fi

if [ "$oldCP" = "" ]; then
    CLASSP=$CLASSP:$oldCP
fi
export CLASSP

# We start the server in the background for a couple of reasons:
# 1) It frees up your window
# 2) You should use 'stop' option instead of ^C to bring down the server
if [ "$1" = "start" ]; then
    shift
    echo Using classpath: ${CLASSP}
    if [ "$1" = "-security" ]; then
        shift
        echo Starting with a SecurityManager
        $JAVACMD TOMCAT_OPTS -Djava.security.manager -Djava.security.policy=${TOMCAT_HOME}/conf/tomcat.policy -Dtomcat.home=${TOMCAT_HOME} org.apache.startup "$0" &
    else
        $JAVACMD TOMCAT_OPTS -Dtomcat.home=${TOMCAT_HOME} org.apache.startup "$0" &
    fi
    $JAVACMD TOMCAT_OPTS -Dtomcat.shell.Startup "$0" &
elif [ "$1" = "stop" ]; then
    shift
    echo Using classpath: ${CLASSP}
    $JAVACMD TOMCAT_OPTS -Dtomcat.home=${TOMCAT_HOME} org.apache.startup -stop "$0"
    org.apache.shell.Shutdown "$0"
elif [ "$1" = "run" ]; then
    shift
    echo Using classpath: ${CLASSP}
    if [ "$1" = "-security" ]; then
        shift
        echo Starting with a SecurityManager
        $JAVACMD TOMCAT_OPTS -Djava.security.manager -Djava.security.policy=${TOMCAT_HOME}/conf/tomcat.policy -Dtomcat.home=${TOMCAT_HOME} org.apache.startup "$0" &
    else
        $JAVACMD TOMCAT_OPTS -Dtomcat.home=${TOMCAT_HOME} org.apache.startup "$0" &
    fi
    $JAVACMD TOMCAT_OPTS -Dtomcat.shell.Startup "$0" &
elif [ "$1" = "ant" ]; then
    shift
    $JAVACMD $ANT_OPTS -Dtomcat.home=${TOMCAT_HOME} -Dtomcat.home=${TOMCAT_HOME} org.apache.tools.ant.Main $0
elif [ "$1" = "jsp" ]; then
    shift
    $JAVACMD $JSPC_OPTS -Dtomcat.home=${TOMCAT_HOME} org.apache.jasper.JspC "$0"
elif [ "$1" = "env" ]; then
    # Call it with source tomcat.sh to set the env for tomcat
    shift
    echo Setting classpath to: ${CLASSPATH}
    oldCP=${CLASSPATH}
else
    echo "Usage:"
    | tomcat(start|run|stop) |
| start - start tomcat in the background |
| run - start tomcat in the foreground |
| -security - use a SecurityManager when starting |
| stop tomcat |
| env - set CLASPATH and TOMCAT_HOME variables |
| ant - run ant script in tomcat context (classes, directories, etc) |
| jsp - run jsp compiler |
exit 0
if [ "$oldCP" = "" ]; then
    CLASSP=$(oldCP)
    export CLASSP
else
    unset CLASSP
fi
```

Figure 13.4: Apache's Tomcat script uses many of the features of shell script programming (part 1 of 4/2 of 4/3 of 4/4 of 4). 

The script begins by checking to see if a special file called .tomcatrc (Tomcat resource) exists under the user's home directory. (Refer to Table 13.2 to find the meaning of the operators used in the tomcat.sh conditionals.) If .tomcat exists, tomcat.sh executes it with the dot sourcing operator.

The next three blocks of code are aligned with the same predicate:

```bash
if [ "${TOMCAT_HOME}" = "" ]; then
```

The first two code blocks attempt to set the value of TOMCAT_HOME, while the third echoes a message to the user and gives up (exits with an error code of one). That first block uses the qualified name of the script (with the $0 variable) to guide where TOMCAT_HOME should be. The while loop that begins with the following condition is decided by:

```bash
while [ -h "$PRG" ]; do
```

It handles circumstances where the qualified tomcat.sh file name is a link, by back-peddling links until the real file is found. The while loop uses the expr and an odd search string to retrieve the linked name from a directory list:

```bash
link=expr "$ls" : \'.*\.(.*)$
```

Note that a long directory list will show that a file is a link by listing the name of the linked file after the -> operator.

The while loop uses basename to strip the directory and extension from $0 and dirname to strip the nondirectory extension from a qualified file name. After the while loop terminates (because there are no more links), Tomcat checks if the directory, so laboriously found by back-peddling links, contains a directory called conf. If it does, Tomcat assumes that's the proper directory and sets TOMCAT_HOME to it.
