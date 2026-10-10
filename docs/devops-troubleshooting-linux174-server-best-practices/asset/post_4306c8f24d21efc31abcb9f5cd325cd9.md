
# with the URL of http://servername/server-status
# Uncomment and change the ".example.com" to allow
# access from other hosts.
#
<

```apache
<Location /server-status>
    SetHandler server-status

    Order deny,allow
    Deny from all
    Allow from localhost ip6-localhost

    # Allow from .example.com

</Location>
</IFmoduL>
```

Note that in this configuration example, we have really locked down who can access the page by saying `deny` from all hosts and only `allow` from localhost. This is a safe default because you generally don’t want the world to be able to view this kind of debugging information. As you can see in the commented-out example, you can add additional `Allow` from statements to add IPs or hostnames that are allowed to view the page.

For Nginx, you would add a configuration like the following to your existing Nginx config. In this example, Nginx will only listen on localhost, but you could change this to allow other machines on your local network:

```nginx
server {
    listen 127.0.0.1:80;

    location /nginx_status {
        stub_status on;
        access_log off;

        allow 127.0.0.1;
        deny all;
    }
}
```

Once you have your configuration set and have reloaded the web server, if you have allowed some remote IPs to view the page, open up a web browser and access `/server-status` on your web server. For instance, if your web server was located at `www.example.net`, you would load `http://www.example.net/server-status` and see a page like the one shown in Figure 8-1.

![](img/362b627595d4f10aae346cc0cc8e74eb_182_0.png)

Figure 8-1 Standard Apache status page

At the top of the status page, you will see general statistics about the web server including what version of Apache it is running and data about its uptime, overall traffic, and how many requests it is serving per second.

Below that is a scoreboard that gives a at-a-glance overview of how busy your web server is, and below that is a table that provides data on the last request that each process served.

Although all of this data is useful in different troubleshooting circumstances, the scoreboard is particularly handy to quickly gauge the health of a server. Each spot in the scoreboard corresponds to a particular web server process, and the character that is used for that process gives you information about what that process is doing:

- W
  - Waiting for a connection
- S
  - Starting up
- R
  - Reading the request
- W
  - Sending a reply
- K
  - Staying open as a keepalive process so it can send multiple files
- D
  - Performing DNS lookup
- C
  - Closing connection
- L
  - Logging
- G
  - Gracefully finishing
- I
  - Performing idle cleanup of worker
- .
  - Open slot with no current process

Figure 8-1 shows a fairly idle web server with only one process in a K (keepalive) state and one process in a W (sending reply) state. If you are curious about what each of those processes were doing last, just scroll down the page to the table and find the process of the correct number in the scoreboard. So, for instance, the W process would be found as server 2-16. It’s not apparent in the screenshot, but that process was actually the response to the request for the server-status page itself. You will also notice a few _ (waiting for connection) processes in the scoreboard, which correspond to the number of processes Apache is configured to always have running to respond to new requests. The rest of the scoreboard is full of ., which symbolize slots where new process could go—basically the MaxClients setting (the maximum number of processes Apache will spawn).

What you will notice as you refresh this page is that the objects in the scoreboard should change during each request. This scoreboard is handy when you want to keep an eye on your web server; just continually refresh the page. During a spike, you are able to see new processes get spawned, switch to W to serve the request, and then, if the spike in traffic subsides, those processes slowly change to _ and ultimately . as they are no longer needed.

Generally speaking, when you access the server status page, you do so from the command line while logged into the web server. This lets you restrict what hosts can view the page while still providing all the information you need. Now, by default, if you were to run `curl` against the regular server status page, you would get HTML output. However, if you pass the `auto` option to the server-status page, you will get text output that’s more useful for both command-line viewing and parsing by scripts:

```bash
$ curl http://localhost/server-status?auto
% Total   % Received  % Xferd   % Average Speed  Time    Time     Time  Current
                                      Dload  Upload   Total   Spent    Left  Speed

117    586  117  586    0  0   2579    0     42s  --:--:-- --:--:--     0
 117    586  117  586    0  0   1905    0     42s  0:00:00 --:--:-- 1905

Total Accesses: 2343235
Total kBytes: 265925501
CPUload: .0737342
Uptime: 6801454
ReqPerSec: .34452
BytesPerSec: 40036.7
BytesPerReq: 116210
BusyWorkers: 53
IdleWorkers: 28

Scoreboard: |_W_W_W__W_K_W_K__||||||||||||||||||||_Kw_CW________K__||||||||||||||||||||||||||||||||||||||||||||||||||||||||
........................................................................................................................
........................................................................................................................
...........................
```

When you want to monitor the status page of a server in the command line, although you could just run the `curl` command over and over, you could use a handy command called `watch`, which will run whatever command you specify every `x` number of seconds (by default 2). So if you wanted to keep an eye on the status page and have it refresh every 5 seconds on the command line, you would type

```bash
$ watch -n 5 'curl http://localhost/server-status?auto'
```

To exit out of `watch`, just hit Ctrl-C.

## Solve Common Web Server Problems

Although it's difficult to document how to solve any and all web server problems, you are likely to run into a few general classes of problems that have identifiable symptoms. This section will highlight some of the common types of problems you may find, their symptoms, and how to remedy them.

### Configuration Problems

One common and relatively simple problem to identify in a web server is a configuration problem. Since web servers need to be reloaded to take on changes in their configuration, it can be tempting to make many changes without reloading the web server; however, if you do so, you are likely to find out during a server maintenance (or when you need to restart the server to load new SSL certificates) that there's some syntax error in your configuration files and your server will refuse to start.

Both Apache and Nginx validate their configuration files when you start, restart, or reload the service, so that's one way to find configuration errors—unfortunately, it also means that in the case of a problem, the server is down while you fix the errors. Fortunately, both web servers provide means to test configuration syntax and highlight any syntax errors while the server is still running.

In the case of Apache, the command is `apache2ctl configtest`. Be sure to run this command as a user who can read all of the configuration files (probably the root user). A successful run looks like this:

```bash
$ sudo apache2ctl configtest
Syntax OK
```

When there is a syntax error, this command will identify the file and line number of the error so it's easy to find:

```bash
$ sudo apache2ctl configtest
apache2: Syntax error on line 233 of /etc/apache2/apache2.conf: Could not open configuration
file /etc/apache2/conf/: No such file or directory
```

In this case, the configuration file had a typo—the directory you wanted to include was /etc/apache2/conf.d.

Nginx also provides a syntax check by running nginx -t:

```bash
$ sudo nginx -t
the configuration file /etc/nginx/nginx.conf syntax is ok
configuration file /etc/nginx/nginx.conf test is successful
```

As with Apache, when Nginx detects an error, it tells you the file and line number:

```bash
$ sudo nginx -t
[emerg]: unknown directive "included" in /etc/nginx/nginx.conf:13
configuration file /etc/nginx/nginx.conf test failed
```

### Permissions Problems

A common headache, especially for new web server administrators, is permission problems on the web server. Although both Apache and Nginx's initial processes run as root, all subprocesses that actually do the work of serving content run as a user with more restricted permissions—usually a user like www-data or apache. If you are, for instance, uploading web pages as a different user, you may initially run into permissions problems until you make sure that each file you want to serve is readable by the www-data or apache user.

So what does a permissions problem look like from the outside? This example takes a basic Nginx setup and changes the permissions on the main index.html file so that it is no longer readable by the world. Then it uses curl to attempt to load the page:

```bash
$ curl http://localhost
<html>
<head><title>403 Forbidden</title></head>
<body bgcolor="white">
<center><h1>403 Forbidden</h1></center>
<hr><center>nginx/0.7.65</center>
</body>
</html>
```
