# ### Setting the server root directory

The `ServerRoot` directive specifies the directory that contains the configuration files, a link to the log file directory, and a link to the module directory. An alternative `ServerRoot` path name can be specified using the -d command-line argument to httpd.

```
ServerRoot "/etc/httpd"
```

# ### Storing the server’s PID file

The Apache Web server keeps track of the PID for the running server process. You can change the locations of this file using the entry following:

```
PidFile run/httpd.pid
```

Apache uses the `PidFile` to store the process ID of the first (root-owned) master daemon process. This information is used by the `/etc/init.d/httpd` script when shutting down the server and also by the server-status handler (as described later in this chapter).

# ### Configuring timeout values

You can set several values that relate to timeout. Some of these values are described in the text following the code:

```
```apache
Timeout 120
KeepAlive Off
MaxKeepAliveRequests 100
KeepAliveTimeout 15
```
```

The `Timeout` directive determines the number of seconds that Apache will hold a connection open between the receipt of packets, between the receipt of acknowledgements on sent responses, or while receiving an incoming request. The default of two minutes (120 seconds) can be reduced if you find an excessive number of open, idle connections on your machine.

The `KeepAlive` directive instructs Apache to hold a connection open for a period of time after a request has been handled. This enables subsequent requests from the same client to be processed faster, as a new connection doesn’t need to be created for each request.

The `MaxKeepAliveRequests` directive sets a limit on the number of requests that can be handled with one open connection. The default value is certainly reasonable because most connections will hit the `KeepAliveTimeout` before `MaxKeepAliveRequests`.

The `KeepAliveTimeout` directive specifies the number of seconds to hold the connection while awaiting another request. You might want to increase the default (15 seconds). Reasons for having a longer timeout could be to allow all the images on the page to be downloaded on the same connection or to take into account how long it may take a client to peruse your average page and select a link from it. The Web application you are using may also need a longer persistent connection. (Of course, a longer `KeepAliveTimeout` prevents each server from moving on to another client during this time period, so you may find that you need to add more request processes to account for that.)