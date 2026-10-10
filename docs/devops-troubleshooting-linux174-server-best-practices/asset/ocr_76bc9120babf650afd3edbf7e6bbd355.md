You can also confirm that MySQL is running using a combination of ps and grep:

```
$ ps -ef | grep mysql
mysql       735     1 0 Jun12 ?    02:02:56 /usr/sbin/mysqld
```

Notice that the process ID that the status command returned (735) matches what you get from ps. Of course, if MySQL is running but listening to the wrong port (or only listening on localhost and you need it to listen on all interfaces), you still may not be able to connect to it even though it is running. So next you will want to test that MySQL is listening on the correct port. By default, MySQL should listen on port 3306; of course, if you have configured it to listen on a different port, you will need to change the following command to match your environment. The netstat command, when passed the -lnp options, will display all ports that are in a listening state along with the process that has that port open:

```
$ sudo netstat -lnp | grep :3306
tcp        0      0 127.0.0.1:3306           0.0.0.0:*            LISTEN   735/mysqld
```

Again, notice that the MySQL process in the output has the same process ID (735) as in the earlier commands. If you don't get any output from this command, then there is no process listening on port 3306. You may want to just view the output of netstat with no grep (or grep for mysql instead) and see if any processes come up. In this example, it's also worth noting that the MySQL process is listening only on localhost (127.0.0.1:3306), which is fine since the web service that accesses it is located on the same server. However, if you needed to access MySQL from another machine and you got this output, you would want to reconfigure MySQL so it listens either on the IP of your network interface or on all interfaces (0.0.0.0).

# PostgreSQL

As with MySQL, you can query the init script or use ps to test whether PostgreSQL is running, but depending on your system, the PostgreSQL init script may have a different name. For instance, on Debian-based systems