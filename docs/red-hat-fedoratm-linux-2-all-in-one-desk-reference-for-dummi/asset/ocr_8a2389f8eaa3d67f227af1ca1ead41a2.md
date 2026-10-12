# Using chkconfig to disable standalone services

To provide Internet services such as Web, mail, and FTP, your Fedora Core system has to run server programs that listen to incoming TCP/IP network requests. Some of these servers are started when your system boots, and they run all the time. Such servers are called *standalone* servers. The Web server and mail server are examples of standalone servers. Another server, called *xinetd*, starts on demand the other servers.

You can turn the standalone servers on or off by using the `chkconfig` command. Here’s how you use `chkconfig` to stop unneeded services:

+   Log in as `root` and type `chkconfig --list` to view all the services set to start automatically at run levels 0 through 6 (see Book VI, Chapter 1 for more on run levels).

+   The services for run levels 3 and 5 matter most because your Fedora Core system is usually at run level 3 (text mode) or 5 (graphical login). Type `runlevel` to see the current run level.

+   Decide which services you don’t need. What you need or don’t need depends on how you use your Fedora Core system. For example, if it’s just a personal workstation, you don’t have to run most services.

+   To stop a service, use the following form of the `chkconfig` command:
+   ```text
+   chkconfig --level 345 service_name off
+   ```
+   where `service_name` is the name of the service you want to turn off. For example, to prevent the `ypserv` service from automatically starting at run levels 3, 4, and 5, type the following command:
+   ```text
+   chkconfig --level 345 ypserv off
+   ```

Using this approach, you can use `chkconfig` to stop all unneeded services from starting at boot time.

To stop a service immediately, use the `service` command like this:
```text
service service_name stop
```
where `service_name` is the name of the service to stop. For example, if the mail server (`sendmail`) is already running, you can stop it with the following command:
```text
service sendmail stop
```

# Configuring the xinetd server to disable services

In addition to standalone servers such as a Web server (`httpd`), mail (`sendmail`), and domain name server (`named`), you have to configure another