
### Setting up DNS for new virtual hosts

You can set up DNS for each new virtual host on Linux as follows:

- 1. Create a zone file for the new domain. (See the preceding section for more on zone files.)

- 2. In the `/etc/named.conf` file, add the following lines to enable the newdomain zone.

```
zone "newdomain.com" IN {
    type master;
    file "newdomain.zone";
    allow-update { none; };
};
```

This tells the named (DNS daemon) that the zone file for newdomain.com is /var/named/newdomain.zone and that it is the primary (master) DNS server for this zone.

- 3. Run the `killall -HUP named` command to force the name server to reload the `/etc/named.conf` and the new zone file.

- 4. Try to ping www.newdomain.com. If you do not get a response, check the `/var/log/messages` file for any types or other errors that name server (named.) might have reported in either `/etc/named.conf` or `/var/named/newdomain._zone` files. In such case, correct the types or errors and restart the server as discussed in the previous step.

- 5. Once you can ping the www.newdomain.com, you are ready to create Apache configuration for this virtual host as described in earlier sections of this chapter.

## Offering virtual mail services

To provide virtual mail service for the new virtual hosts you add, you have to modify the `newdomain.zone` file and add one or more appropriate MX record(s). For example, say that your mail server is `mail.domain.com` and it is configured to accept mail for `newdomain.com`. In such a case, you can modify the `/var/named/newdomain.zone` to be as follows:

```
@ IN SOA newdomain.com. hostmaster.newdomain.com.
20011201002 ; Serial YYYYMMDDXXX
7200 ; refresh
3600 ; (1 hour) retry
1728000 ; (20 days) expire
3600 ; (1 hr) minimum ttl

; Name Servers
IN NS ns1.domain.com.
IN NS ns2.domain.com.
IN MX 10 mail.domain.com.

; CNAME for name-based virtual hosting
www.newdomain.com. IN CNAME www.domain.com.
```

Note that if you have multiple mail servers you can add them using a simple priority scheme. For example, say that you want all mail for newdomain.com to go to `mail.domain.com` and if this mail server is unavailable, you want to use `bkupmail.domain.com`. You can simply add a second MX record as shown here:

```
IN MX 10 mail.domain.com.
IN MX 20 bkupmail.domain.com.
```

The lower number in front of `mail.domain.com` makes it a higher priority mail server than `bkupmail.domain.com`. Make sure you have configured your mail server software to support virtual mail domains.

## Setting User and Group per Virtual Host

If you have compiled Apache using the `Perchild MPM` module, you can set user and group per virtual host, which is discussed here. But the biggest benefit of using this method instead of a multiple `httpd.conf`-based mail server setup is simplicity of configuration.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_199_0.png)

This approach is slower than running multiple main Apache servers with different IP addresses and different `User` and `Group` directives. The speed is lost because of the increased complexity in internal request processing. The concept behind this method is as follows: you instruct Apache to run a cluster of child processes with a given user ID and group ID. When a request for a virtual host comes in and a child process is given the request, the child process first determines whether it can handle the request. If the child is not responsible for the requested virtual host it must pass the request to the appropriate child process via socket calls, which slows the request processing. Because this is a new concept, the speed issue might be resolved or reduced in the future versions of Apache.

The material that follows assumes that you want to set up two virtual hosts called `vhost1.domain.com` and `vhost2.domain.com`. Make sure to replace them with whatever hostnames you need to use. Table 6-1 shows the user IDs and group IDs to be used for these virtual domains.

| | Table 6-1 User and Group IDs for the Virtual Hosts |
|---|---|
| Virtual Host | User ID | Group ID |
| `vhost1.domain.com` | `vh1user` | `vh1group` |
| `vhost2.domain.com` | `vh2user` | `vh2group` |

Apache can be configured to support different user and group ID per virtual host as follows:

- 1. Add the following lines to `httpd.conf`:

```
ChildPerUserID 10 vh1user vh1group
ChildPerUserID 10 vh2user vh2group
```

The `ChildPerUser` directive tells Apache to associate ten child processes (each being multiple threads that service requests) to user and group ID for the `vhost1.domain.com` site. Similarly, the second line associates another ten child processes to user and group ID for the `vhost2.domain.com` site.

- 2. Add the following lines to `httpd.conf`:

```
NameVirtualHost 192.168.1.100

<VirtualHost 192.168.1.100>
    ServerName vhost1.domain.com
    AssignUserID vh1user vh1group
    #
    # Other directives go here
    #
</VirtualHost>

<VirtualHost 192.168.1.100>
    ServerName vhost2.domain.com
    AssignUserID vh2user vh2group
    #
    # Other directives go here
    #
</VirtualHost>
```

The *AssignUserID* directive used in each of the virtual host configuration tells Apache to associate each of the virtual hosts to appropriate user and group ID. Don’t forget to change the IP address as necessary.

- 3. Restart the Apache server using the /usr/local/apache/bin/apachectl restart command and you are done.

## Managing a Large Number of Virtual Hosts

If you maintain a lot of virtual hosts, the *httpd.conf* file could become very long and cumbersome to manage. An easy solution is to put each virtual host configuration in a file by itself and to include each file by using the *Include* directive. For example, Listing 6-4 shows a *httpd.conf* file with two virtual host configurations that are external to main configuration file.

### Listing 6-4: httpd.conf with two external virtual host configurations

```
ServerType standalone
ServerRoot "/usr/local/apache"
PidFile /usr/local/apache/logs/httpd.pid
ScoreBoardFile /usr/local/apache/logs/httpd.scoreboard
Timeout 300
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
MinSpareServers 5
MaxSpareServers 10
StartServers 5
MaxClients 10
MaxRequestsPerChild 0
Port 80
User httpd
Group httpd
ServerName www.domain.com
ServerAdmin webmaster@domain.com
DocumentRoot "/www/mysite/htdocs"

# Name Virtual Hosts
NameVirtualHost 192.168.1.100
Include vhost1.domain.com.conf
Include vhost2.domain.com.conf
```

Notice that the **NameVirtualHost** directive is followed by the **Include** directive, which tells Apache to read the **vhost1.domain.com.conf** and **vhost2.domain.com.conf** files to load virtual host configuration. These files can simply contain the <VirtualHost> containers that you would normally put in **httpd.conf**. The benefit of this approach is that you can create a very elaborate configuration for each virtual host without cluttering up **httpd.conf**.

### Automating Virtual Host Configuration using mod_perl

Although using the **Include** directive (as discussed in the previous section) helps to make **httpd.conf** manageable, it is still not good enough solution for sites that use many Web servers, which, in turn, run many virtual Web sites. Ideally, you want to write Apache configuration with a program or script, if possible, so that many common configuration options are automatically created.

If you use the **mod_perl** module with Apache (discussed in Chapter 16), you can write Perl code to generate your Apache configuration. Because **mod_perl** compilation and installation is covered in Chapter 16 I will not repeat it here. I discuss how you can use Perl code to generate Apache configuration next.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_201_0.png)

> See Chapter 16 if you still need to compile and installed **mod_perl** support in Apache. Just remember when compiling **mod_perl** by following the instructions in Chapter 16 that you have to use either the **EVERYTHING=1** option or **PERL_SECTIONS=1** option with the configure script.
