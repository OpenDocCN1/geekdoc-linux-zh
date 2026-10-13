/usr/local/etc/rc.d. However, if you want to start the server manually at any time, you can use the apachectl program. For example,

```
#apachectl start
/usr/local/sbin/apachectl start: httpd started
```

The apachectl program can also be used to stop the server, and it is the easiest and best way to do this. For example,

```
#apachectl stop
/usr/local/sbin/apachectl stop: httpd stopped
```

If you want to restart the server, apachectl also has a command to do this rather than having to issue two commands:

```
#apachectl restart
/usr/local/sbin/apachectl restart: httpd restarted
```

Note that Apache only reads its configuration files once when it first starts. So any changes you make to them while Apache is running will not take effect until it has been restarted by issuing the previous command.

If you look at the process list while Apache is running, you will see multiple httpd processes because the main Apache process spawns several child processes to handle the incoming httpd requests. Apache always keeps several processes running to handle the requests—even if there currently is no Web site traffic. If, for whatever reason, you want to kill the Apache server by issuing a kill command directly to the process, you must make sure that you issue the command to the parent process. If you kill one of the child processes, the parent process will simply spawn a new one to replace it.

![](bbox=[0.22, 0.78, 0.32, 0.88])

> The apachectl restart command will immediately kill the parent process as well as all the child processes, even if the child processes are currently handling a request. This means that any visitors to your site who are currently receiving or sending data to your Web server will basically “have the rug pulled out from under them.” Because of this, the apachectl program also provides the graceful option that you can use instead of the restart option (for example, apachectl graceful). This command will restart the server but will not interrupt any transactions that are currently in process. Processes that are currently handling transactions will not be restarted until the current transaction has been completed.

By default, Apache runs on network port 80, and for a public Web server, you probably won't want to change this. Web browsers assume port 80 unless otherwise specified in the URL.