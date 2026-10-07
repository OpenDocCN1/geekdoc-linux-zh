
# Linux Web Server Toolkit

processing in httpd.conf, server-level resources in srm.conf, and access control options in access.conf. The use and location of each directive will be covered in the sections that follow.

## Setting Up Server Configuration

The directives in the httpd.conf file are used to control the overall system settings for your Web server, including things like which user and port are used to run the server. This section reviews each of the default settings and describes the options you can use in this configuration file.

The httpd.conf is located in the /etc/httpd/ directory. You can edit it with any text editor, including vi or the graphical Site editor in Chapter 6. There are many more options available than any single Web server would be likely to require. Those that are most commonly used are discussed in this chapter.

I'll start by discussing the meaning of the lines in the default httpd.conf file that you can review after you install the OpenLinux Lite CD-ROM. Many lines in that file are commented out (start with a #), with other values changed from what a default Apache installation uses. I'll explain the commented-out lines, as well as the changes to default values that I recommend.

## Basic Server Directives

Server Directives control how the Web server starts and runs, apart from its interaction with other programs and Web clients.

### SERVERTYPE

The ServerType directive indicates that the httpd server should run all the time, with requests being passed directly to it from the network. The other option for this directive is inevent, which means that the httpd daemon isn't running until a request comes in. Then the Web server is started and the request is processed. OpenLinux uses the standalone option, shown here, for reasons:

```
ServerType standalone
```

First, OpenLinux uses the Web server for all documentation, so the Web server is used even if you don't intend to provide a public web page. Second, OpenLinux follows the latest trend in using Apache, as previously described. That is, one program is always running and manages the overall load for the Web server, starting and stopping other copies of the Web server to handle requests according to the traffic load and the other parameters you set in the httpd.conf.

### PORT 80

The network port is the port that the Web server expects requests to arrive on. Port 80 is the standard for Web servers.

## Chapter 11: Configuring the Apache Web Server

If you don't use port 80, you must make sure that all URLs referring to your site include the correct port number. For example, if your port is 8080, the URL of your main page would be the following:

```
http://www.myplace.org:8080/
```

Nonstandard ports are most often used if you are not the root user of the system or you want a less public Web server.
In addition, if you use a nonstandard port numbered less than 1023 (you can go up to about 65,000), you must be logged in as the root user when you start the httpd daemon. Every spawned copies will use the user ID defined in httpd.conf.

### HOSTNAMELOKUPS

The HostnameLookups directive, shown here, determines what type of information is stored in the standard log files:

```
HostnameLookups on
```

Every request processed by your Apache Web server is logged in /etc/httpd/apache/logs/access.log. Several types of information can be specified in that file. One standard part of a logged request is the address of the person requesting a Web page. If this directive is off, the domain name (mydesk.bigorg.com) is stored in the log file; if this is off, the IP address is stored.

Using the domain name (the default in OpenLinux) increases the load on your Web server, but makes the logs a lot more useful. (See Chapter 13 for details on using the log files to review your server statistics.) Turning this directive saves the step of looking up the IP address for each request that comes in.

### USER AND GROUP DIRECTIVES

The User and Group directives define which user and group the server runs as, as shown in the following example:

```
User nobody
Group #-1
```

If the user listed after User is not the user you log in as, then you must be logged in as the root user when starting the Web server (the automatic startup in OpenLinux takes care of this). After the Web server is started, it switches automatically to use the security access granted to the user and group listed after the User and Group directives.

The User and Group directives maintain the security of your Web server. For example, suppose a user found a security hole allowing that user to make the Web server execute commands on your system. If the Web server is running as user nobody, the script run doesn't have access to anything else on the system because user nobody has no access permissions, and hence a malicious user can do little damage to the security hole.

For this reason, the default setting is nobody – a user created during the installation for just such purposes. User nobody doesn't have a home directory and has very few access rights. This helps keep your Web server secure. But you must also be certain that all the documents you want your Web server to send to clients are readable by everyone, otherwise use nobody, and consequently the Web server, can't access them.

OpenLinux leaves the group undefined to increase security further. The value of both the User directive and the Group directive can be entered in the httpd.conf file as a name or as an ID number for the user or group. Whichever is most convenient for you.

![](img/e01f1106dd2902613fa0789c8baa7e6_311)

To set the permissions of any file so that everyone can read, use the chmod command. The BindAddress directive is used, as shown in the following:

```
chmod+r
```

### SERVERADMIN

The ServerAdmin directive gives the e-mail address of the administrator who should be notified of any problems. The OpenLinux default is root, but you should change this value to Webmaster.

### SERVERROOT

The ServerRoot directive specifies the directory where the server's configuration files, error logs, and log files are stored, as follows:

```
ServerRoot /etc/apache
```

### BINDADDRESS

The BindAddress directive tells the Web server which IP address or domain name to listen to, and is used as follows:

```
#BindAddress *
```

The BindAddress directive is commented out in the default configuration because it's assumed that you'll be serving one IP address and one domain name.

![](img/e01f1106dd2902613fa07890c8baa7e6_312_0)

The BindAddress directive allows you to have one physical computer acting as a Web server for numerous domain names, such as abc.com, nbc.com, and cbs.com, all on one computer.

If you use multiple domain names on one system, the ServerRoot and DocumentRoot define where files are stored for each domain name. The value of the BindAddress directive determines which domain or IP address the Web server requests for.

![](img/e01f1106dd2902613fa07890c8baa7e6_312_1)

### ERRORLOG

The ErrorLog directive defines the location where the error log file is stored, as follows:

```
ErrorLog /var/log/httpd/apache/error.log
```

The error log is assumed to be stored in a sub True of the directory given as the ServerRoot. To change that, start the value of this directive with a slash (/) in the default example just shown. If you check the inode (use ls -li) in both the /etc/httpd/apache/logs and /var/log/httpd/apache/, you'll see that the files are linked to the same inode — they are aliases to the same file. This maintains compatibility

![](img/e01f1106dd2902613fa07890c8baa7e6_312_2)
