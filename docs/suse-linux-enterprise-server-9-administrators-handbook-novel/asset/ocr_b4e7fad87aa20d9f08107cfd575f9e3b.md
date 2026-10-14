protocol, be it httpd, sshd, or telnetd, offers a specific port to the network, you can quickly check for an open listener process on the port. The netstat command can list various attributes of a server’s networking environment. You can specify the -l parameter to list all listeners and the -p parameter to identify the program offering the service. The output would look like the following:

```
Athena:~ # netstat -lp | grep -e http
 tcp        0     0 *:https        *:*        LISTEN  4601/httpd2-prefork
Athena:~ #
```

By using the process ID, you can find all related processes and identify the routines offering the service:

```
Athena:~ # ps -ef | grep -e 4601
root      4601     1  0 04:31 ?        00:00:00 /usr/sbin/httpd2-prefork -f
→ /etc/apache2/httpd.conf
wwwrun    4602  4601  0 04:31 ?        00:00:00 /usr/sbin/httpd2-prefork -f
→ /etc/apache2/httpd.conf
wwwrun    4603  4601  0 04:31 ?        00:00:00 /usr/sbin/httpd2-prefork -f
→ /etc/apache2/httpd.conf
wwwrun    4604  4601  0 04:31 ?        00:00:00 /usr/sbin/httpd2-prefork -f
→ /etc/apache2/httpd.conf
wwwrun    4605  4601  0 04:31 ?        00:00:00 /usr/sbin/httpd2-prefork -f
→ /etc/apache2/httpd.conf
wwwrun    4606  4601  0 04:31 ?        00:00:00 /usr/sbin/httpd2-prefork -f
→ /etc/apache2/httpd.conf
root      6807  5920  0 13:28 pts/1    00:00:00 grep -e 4601
Athena:~ #
```

Using this approach , you can quickly verify the presence of a service through its process name or port offerings. You can now verify the application-specific log files for possible errors. If none are present, the process unresponsiveness may be due to resource constraints from other processes.

# System Resource Check

A server can be thought of as a container for resources. Application programs, in turn, consume these resources. Well-behaved applications start up, allocate a portion of available memory, utilize a moderate amount of CPU, write a controlled amount of information back to the appropriate files, and then terminate.

Of the resources used by an application, only the CPU resource can be thought of as unlimited. Though only so much processing power is available at any moment in time, a well-behaved application consumes only a little bit at a time. The faster the CPU, the faster the job completes. After the job has terminated, the portion of the CPU’s time spent processing the application is now available for other processes.