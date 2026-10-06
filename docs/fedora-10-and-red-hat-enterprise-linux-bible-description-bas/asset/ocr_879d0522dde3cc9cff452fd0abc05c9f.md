# Part IV: Fedora and RHEL Network and Server Setup

```
<IfModule worker.c>
StartServers 2
MaxClients 150
MinSpareThreads 25
MaxThreads 75
ThreadsPerChild 25
MaxRequestsPerChild 0
</IfModule>
```

Apache starts a daemon process by root that binds to the appropriate port, and switches to a privileged user. More servers (equivalent to the value of the StartServers directive in prefork.c) will be started as the same unprivileged user (the apache user in this case).

Apache attempts to intelligently start and kill servers on the current load. If the amount of traffic decreases and there are too many idle servers, some will be killed (down to the number of servers noted in MinSpareServers). Similarly, if many requests arrive in proximity and there are too few servers waiting for new connections, more servers will be started (up to the number of servers noted in MaxClients).

> NOTE: Getting the value of MaxClients is critical because it puts a lid on the total number of simultaneous client connections that can be active. If the number of MaxClients servers are in use, no will be created and subsequent requests to the server will wait until one is freed up.

Using the values specified above, when the daemon is started, the parent and eight child server processes will run, waiting for connections (as defined by StartServers). As more requests arrive, Apache will ensure that at least five server processes are ready to answer requests. When requests have been fulfilled and new connections arrive, Apache will be killing processes until the number of idle web server processes is below 20. The value of StartServers should always be somewhere between MinSpareServers and MaxServers.

Apache limits the total number of simultaneous threads by the MaxClients directive. The default value is 150, which should be sufficiently high. However, if you find that frequently have nearly many threads running, remember that any connection beyond the 150th will be rejected. In such cases, if your hardware is sufficiently powerful (and your network connection can handle the load), you should increase the value of MaxClients.

> NOTE: You can see the state of your Apache server processes and get a feel for the server's activity by viewing the server-status page for your server, described later in this chapter. The ps -fu apache command will show you if the Apache server processes (http daemon) are currently running.

To minimize the effect of possible memory leaks (to keep the server pool "fresh\ each server process is limited in the number of requests that it can handle (equal to the value of