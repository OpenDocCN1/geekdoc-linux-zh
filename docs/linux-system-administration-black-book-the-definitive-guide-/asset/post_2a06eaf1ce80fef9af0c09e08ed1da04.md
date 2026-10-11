
## A **Listen** directive can refer to a port (1000), an IP address (192.168.10.1), or a specific port at a specific IP address (192.168.10.1:1000). This directive refers to additional places to listen, on top of the defaults already set. It does not supersede the defaults.

The next item is important to anyone who intends to do virtual hosting:

```
#BindAddress *
```

The **BindAddress** directive tells Apache where to listen for connection requests. You can tell it to listen on any of the following:

- **\*—All IP addresses** assigned to interfaces on this machine
- **IPAddress**—A single IP address
- **.domain.extension**—Your domain name

Only one **BindAddress** directive can be included in /etc/httpd.conf.

Next is a long section containing instructions for each module that Apache loads when it starts. The **LoadModule** directive is fairly self-descriptive. It loads the listed module from the listed library into the Web server. The first four lines of the module loading section of /etc/httpd.conf are listed here:

```
#LoadModule mmap_static_module modules/mod_mmap_static.so
LoadModule env_module modules/mod_env.so
LoadModule config_log_module modules/mod_log_config.so
LoadModule agent_log_module modules/mod_log_agent.so
```

Some of the listed modules are commented out, such as the first line in the previous snippet. Many Web administrators simply leave the modules as they are unless they need to add new functionality to the Web server. If you are very security-conscious and do not have a lot of people creating their own Web pages on your server—which usually broadens the types of modules you need to have loaded—then you may want to trim down this list.

Loading a module does not actually mean that it is activated in the server. Some modules must be in a particular order, because some are dependent on others. For this reason, the loading and activating are done separately. Apache actually has a default list that it activates if you do not give it specific instructions. The following line clears that default list so that you can repopulate it on your own:

```
ClearModuleList
```

### In Depth 13. The Apache Web Server

After this happens, every module that you intend to use has to be activated in the proper order. This activation is accomplished with the **AddModule** directive. The following are the first four of these directives:

```
#AddModule mod_mmap_static.c
AddModule mod_env.c
AddModule mod_log_config.c
AddModule mod_log_agent.c
```

Once you finish with the modules, you reach:

```
#ExtendedStatus On
```

The **ExtendedStatus** directive is either **On** or **Off**. If you have the status module activated, you can utilize this directive to create Web server status reports on the fly whenever people go to a certain URL. After this comes the network port that **httpd** listens on when Apache is set to **standalone**:

```
Port 80
```

Next, you tell **httpd** which login name and group to run under. I highly recommend that you do not change this information! The **nobody** user and group is important for system security, because **httpd** runs SUID. This section contains the following:

```
User nobody
Group nobody
```

After this is where you set the contact information for the Web server administrator:

```
ServerAdmin root@localhost
```

Once you have the Web administrator's email set, you get to:

```
#ServerName localhost
```

The **ServerName** directive sets the host name for your Web server. This is a useful statement for when you have more than one name assigned to the server machine. Now you move on to setting where the server looks for files:

```
DocumentRoot /home/httpd/html
```

The **DocumentRoot** directive tells Apache where to look for the Web files. This is the Web server's root directory. Anyone who goes to **http://www.domain.extension** is actually looking at the contents of DocumentRoot. Next, you get into setting parameters for parts of the file system:

```
<Directory />
Options None
AllowOverride None
</Directory>
```

The <Directory *path*> tag is used to block off a section of the access configuration file that refers to a specific segment of your file system. Items within the tag are referred to as *directives*. In this case, the directives refer to the entire file system, because the root directory is specified.

The first directive in this section of code is the **Options** directive. This feature accepts the arguments listed in Table 13.3.

The second unknown is **AllowOverride**. The options available with this statement are listed in Table 13.4.

> Note: As you can see, a lot of features are available with Apache. For a full listing with explanations, see www.apache.org/docs/mod/core.html.

### Table 13.3 Features available with the Options directive.

| Feature | Result |
| :--- | :--- |
| All | Specifies to include all features listed in this table except **None** and **MultiViews**. Default setting. |
| ExecCGI | Specifies that CGI scripts can be run from this location. |
| FollowSymLinks | Specifies that Apache can follow symbolic links here, unless in a **Location** setting. |
| Includes | Specifies to allow SSI here. |
| IncludesNOEXEC | Specifies to allow SSIs here but disable the **#exec** and **#include** CGI directives. |
| Indexes | Specifies that when following a URL to a directory where no default page exists, Apache should give a list of the directory's contents. |
| MultiViews | Specifies to activate the **MultiViews** feature. See the module mod_negotiation for more on **MultiViews** (www.apache.org/docs/content-negotiation.html). |
| None | Specifies that no features are activated. |
| SymLinksIfOwnerMatch | Specifies that Apache should follow symbolic links if the target is owned by the UID who created the link, unless inside a **Location** directive. |

### Table 13.4 Features available with the AllowOverride directive.

| Feature | Result |
|---|---|
| **All** | Includes all features except **None**. |
| **AuthConfig** | Allows the family of authorization directives listed in Table 13.5. |
| **FileInfo** | Allows the family of document type directives listed in Table 13.6. |
| **Indexes** | Allows the directory indexing family of directives listed in Table 13.7. |
| **Limit** | Allows host access directives: **allow**, **deny**, and **order**. |
| **Options** | Allows directory feature directives: **Options** and **XBitHack**. |
| **None** | Disallows all features listed. |

### Table 13.5 The authorization family of directives.

| Directive | Purpose |
|---|---|
| **AuthDBMGroupFile** | Sets the name of a DBM file containing group authentication data. |
| **AuthDBMUserFile** | Sets the name of a DBM file containing user authentication data. |
| **AuthGroupFile** | Sets the name of a text file containing group authentication data. |
| **AuthName** | Sets a name for a directory's authentication requirements so the end user has context when asked to log in. |
| **AuthType** | Sets the type of user authentication required for this directory. |
| **AuthUserFile** | Sets the name of a text file containing user authentication data. |
| **require** | Sets which users, once authenticated, can access the directory. |

### Table 13.6 The document type family of directives.

| Directive | Purpose |
|---|---|
| **AddEncoding** | Sets certain file name extensions to specific encoding types. |
| **AddHandler** | Maps file extensions to the internal routine that knows how to work with them. |
| **AddLanguage** | Sets certain file name extensions to represent specific languages. |
| **AddType** | Sets certain file name extensions to specific content types. |
| **DefaultType** | Specifies the file type to assume when there is no extension. |
| **ErrorDocument** | Specifies error responses. |
| **LanguagePriority** | Sets a list of priorities for which language to display information in if multiple languages are available and the end user does not make a specific request. |
