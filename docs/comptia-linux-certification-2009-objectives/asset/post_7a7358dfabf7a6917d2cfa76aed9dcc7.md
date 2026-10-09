
## 13 Configuring Basic Internet Services

Lesson Time: 2 hour(s)

### Lesson Objectives

In this lesson, you will configure basic Internet services.

You will:
- Configure a web server.
- Implement Apache access control.
- Configure a Squid proxy server.
- Configure email services.
- Control Internet services.

### Introduction

In the previous lesson, you configured basic client services. Now, you want to implement a business-oriented service that allows you to share resources and communicate across various platforms on a network. In this lesson, you will implement web services.

The Internet offers various services such as email, file sharing and downloading, and web browsing. Employees of an organization will often need to access the Internet and communicate with clients across various platforms. As a system administrator, you want to implement a simplified service that provides interoperability among applications and involves cost-effective communication. Internet services facilitate the ability to share and transfer resources across various networks securely.

This lesson covers all or part of the following CompTIA Linux+ (2009) certification objectives:
- Topic A
    - Objective 3.3
    - Objective 3.4
    - Objective 3.5
- Topic B
    - Objective 3.3
- Topic C
    - Objective 3.4
- Topic D
    - Objective 3.8
- Topic E
    - Objective 3.1
    - Objective 3.5

## Topic A

### Configure a Web Server

You managed remote network systems. Now, you need to share information through the Internet because this is the most simplified and standardized way of communication. To begin with, you want to host a website on a web server. In this topic, you will configure a web server.

Your company is growing with an increasing customer base. Management is determined to establish the company worldwide. As a Linux+ administrator, you may need to implement a service, such as a web server, that enables a simplified and efficient way of communication with low technology cost, thereby improving the business process. Your ability to configure web servers appropriately will enable you to meet this business need.

### Web Servers

**Definition:**  
*A web server* is a software application that is run on a system to provide world wide web services. It has a static IP address and a domain name, and is always connected to the Internet. The server provides web pages to client web browsers across the Internet. The web server can host web pages, scripts, multimedia files, and programs and serve them to clients using HTTP.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_624_0.png)

**Example:**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_624_1.png)

*Figure 13-1: A web server provides web pages to a client computer.*

![](img/477ccb2f05b6ba1b2d563ea74f18c197_625_0.png)

### The Apache Web Server

The Apache web server is an open source web server in which multiple user requests are processed by relocating them into separate modules known as Multiprocessing Modules (MPMs). An MPM combines all network ports on a machine, accepts requests, and reallocates these requests to separate handlers. After processing the requests, the Apache web server responds to them based on the MPM that is used. These modules are chosen during the configuration and then compiled on the server. Only one MPM can be chosen at a time.

Apache also allows you to choose between processes and threads. Threads are processes that consume fewer resources and improve the performance of the server. These processes can be executed as threads based on the MPM that is chosen. Apache supports a wide variety of operating systems each of which supports a default MPM. Apache also provides the functionality of dynamically loaded modules, where the modules are compiled separately and loaded on the server any time, using the LoadModule directive rather than initially building the modules on the server. This avoids the process of recompiling the server whenever the modules are added to or removed from the server.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_625_1.png)

### Enable and Disable Modules

The LoadModule directive allows you to enable a specific module on the web server. To disable a module, locate the line containing the module in the httpd.conf file and uncomment or remove the line. Save the file and restart the httpd service for the changes to apply.

### Popularity

The Apache web server is the most frequently used web server on Linux networks. The original version of Apache was developed for UNIX. The later versions of Apache supports other operating systems including Windows, Solaris, and OS X.

### Apache Modules

Apache has a set of compiled modules that extend its core functionality. The modules can be integrated with Apache as add-ons.

| **Module** | **Description** |
| :--- | :--- |
| mod_access | Used for restricting access to clients, based on the client request that involves the characteristics such as the client hostname and IP address. |
| mod_ssl | Used for providing a secure support for the Apache server using the Securer Socket Layer (SSL) and Transport Layer Security (TLS) protocols. |
| mod_php | Used for recognizing PHP scripts. |
| mod_spelling | Used for correcting URLs written with any capitalization issues and misspelling issues. |
| mod_perl | Used for recognizing Perl scripts. |
| mod_cgi | Used for recognizing Common Gateway Interface (CGI) scripts. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_626_0.png)

### Hypertext Preprocessor (PHP)

Hypertext Preprocessor (PHP) is an open source scripting language that is used to create dynamic web pages. PHP is a server-side scripting language, and so scripts written in PHP are executed on the server and the client will not be able to view the code. PHP is compatible with any type of database.

The php.ini configuration file controls the behavior of PHP in Linux. By default, PHP looks for the file in the current working directory, using the path specified by the environment variable PHPRC or the path specified while compiling. It has various functions, for example, it can be used to change the severity of errors that need to be logged.

### Apache Configuration Directives

There are a set of directives defined in the Apache distribution. Each directive is set to specific values and defines specific formats. Some of the frequently used directives are listed in the table.

| **Directive** | **Description** |
| :--- | :--- |
| ServerAdmin | Specifies the email address that is used in error messages sent to a client. |
| CustomLog<br>LogFormat | Specifies the log file name and the log format. Describes the format of the access log files. It defines either of the two forms; the form that uses a single argument, which specifies the explicit format or the form that uses a nickname to define the explicit format. |
| MinSpareServers | Specifies the minimum number of idle child server processes. |
| MaxSpareServers | Specifies the maximum number of idle child server processes. |
| DocumentRoot | Defines the path of the directory from which httpd will run the files to serve web hosting. When a user requests a path, it is appended to the URL path defined in the DocumentRoot directive. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_626_1.png)

### The httpd.conf File

The httpd.conf file is the main configuration file that is used to configure the Apache web server. It is stored in the /etc/httpd/conf directory. The http service is enabled using the httpd package. By default, httpd is installed in the /usr/sbin directory and the initialization script runs from the /etc/init.d/httpd file. The httpd.conf file uses directives to control the operations of the Apache web server, define its parameters, and set virtual hosts.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_627_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_627_1.png)

Figure 13-3: Various directives defined in the httpd.conf file.

> The hash (#) sign is used to comment a line.

By default, the httpd.conf file contains all possible directives. Some of the frequently used directives are explained in the table.
