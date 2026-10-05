# Shell Programming · 193

```
case expression in
  pattern1)
    statements ;;
  pattern2)
    statements ;;
  *)
    statements that handle drop-through cases ;;
esesac
```

The asterisk handles those circumstances where the value of expression has no associated pattern. Programmers typically call this portion of the case statement the drop-through case.

A working example of a script that uses the case statement Apache s http script (which, on a Red Hat system, can be found in the /etc/rc/init.d directory). The portion of the script that predicates processing based on parameter I is shown in Figure 13.3.

```
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
esesac
```

Figure 13.3: Apache's httpd script uses a case statement to handle its various parameter options.

# Tomcat Code Review

A good way to show the power of shell programming is to review Apache's Tomcat script. The script is called tomcat.sh and is located under the bin directory where Tomcat is installed (/opt/jakarta-tomcat on our system). The tomcat.sh script shown in Figure 14.3 is devoid of comment (except for the first line), so it might be worthwhile to add comments to the script as you step through the code.