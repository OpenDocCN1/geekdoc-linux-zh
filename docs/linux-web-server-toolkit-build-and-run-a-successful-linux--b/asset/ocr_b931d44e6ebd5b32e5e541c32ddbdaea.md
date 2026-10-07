# Linux Web Server Toolkit

processing in httpd.conf, server-level resources in srm.conf, and access control options in access.conf. The use and location of each directive will be covered in the sections that follow.

# Setting Up Server Configuration

The directives in the httpd.conf file are used to control the overall system settings for your Web server, including things like which user and port are used to run the server. This section reviews each of the default settings and describes the options you can use in this configuration file.

The httpd.conf is located in the /etc/httpd/ directory. You can edit it with any text editor, including vi or the graphical CRISite editor in Chapter 6. There are many more options available than any single Web server would be likely to require. Those that are most commonly used are discussed in this chapter.

I'll start by discussing the meaning of the lines in the default httpd.conf file that you can review after you install the OpenLinux Lite CD-ROM. Many lines in that file are commented out (start with a #), with other values changed from what a default Apache installation uses. I'll explain the commented-out lines, as well as the changes to default values that I recommend.

# Basic Server Directives

Server Directives control how the Web server starts and runs, apart from its interaction with other programs and Web clients.

# SERVERTYPE

The ServerType directive indicates that the httpd server should run all the time, with requests being passed directly to it from the network. The other option for this directive is inevent, which means that the httpd daemon isn't running until a request comes in. Then the Web server is started and the request is processed. OpenLinux uses the standalone option, shown here, for reasons:

```
ServerType standalone
```

First, OpenLinux uses the Web server for all documentation, so the Web server is used even if you don't intend to provide a public web page. Second, OpenLinux follows the latest trend in using Apache, as previously described. That is, one program is always running and manages the overall load for the Web server, starting and stopping other copies of the Web server to handle requests according to the traffic load and the other parameters you set in the httpd.conf.

# PORT 80

The network port is the port that the Web server expects requests to arrive on. Port 80 is the standard for Web servers.