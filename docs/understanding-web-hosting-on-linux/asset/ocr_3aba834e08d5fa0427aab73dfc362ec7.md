```
#!/bin/sh
#
# $Id: tomcat.sh v.1.17.2.2 2001/01/10 22:55:48 glenn Exp $

# Shell script to start and stop the server

# There are other, simpler commands to startup the runner. The two
# commented commands good replacements. The first works well with
# Java Platform 1 based runtimes. The second works well with
# Java2 Platform based runtimes.

# -jcp runner.jar:servlet.jar:classes org.apache.shell.Startup $
# java -jcp runner.jar:servlet.jar:classes org.apache.shell.Startup $
\nif [ -f ${HOME}/tomcat ]; then
    ${HOME}/tomcat
fi

if [ "${TOMCAT_HOME}" = """ ]; then
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
if [ -d \${TOMCAT_HOME_1}/conf ] ]; then
    TOMCAT_HOME=\${TOMCAT_HOME_1}
    echo "Setting Tomcat_HOME to \${TOMCAT_HOME}"
fi

if [ "${TOMCAT_HOME}" = """ ]; then
    # try to find tomcat
    if [ -d \${HOME}/opt/tomcat/conf ] ]; then
        TOMCAT_HOME=\${HOME}/opt/tomcat
        echo "Defaulting TOMCAT_HOME to \${TOMCAT_HOME}"
    fi
fi

if [ -d /opt/tomcat/conf ] ]; then
    TOMCAT_HOME=-/opt/tomcat
    echo "Defaulting TOMCAT_HOME to \${TOMCAT_HOME}"
fi

# Add other "standard" locations for tomcat

if [ "${TOMCAT_HOME}" = """ ]; then
    echo TOMCAT_HOME not set, you need to set it or install it in a standard location
```

Figure 13.4: Apache's Tomcat script uses many of the features of shell script programming (part 1 of 4).