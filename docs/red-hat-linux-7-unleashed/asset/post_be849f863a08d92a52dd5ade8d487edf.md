
This will create a file called *Configuration* in the *src/* subdirectory. It also generates the makefile that will be used to compile the server code.

Once this step is done, type *make* to compile the server code. After the compilation is completed, type *make install* to install the server. You can now configure the server via the configuration files. See the section “Runtime Server Configuration Settings” for more information.

### Note

> The Apache Autoconf-style interface (APACI), described here, is only available in version 1.3 and later.

### The Advanced Way

If you want to do things the old-fashioned way, or you just want more control over the way that your server is built, follow these steps:

1. In the source directory, copy the file *Configuration.templ* to *Configuration* and open up *Configuration* with your favorite editor.
2. Modify the compiler flags if, and only if, you know what you're doing.
3. Uncomment those modules that you would like included, comment out modules that you don't want, or add lines for custom modules that you have written or acquired elsewhere.
4. Run the *Configure* script to create the *Makefile*.
5. Finally, compile and install the server with *make* and *make install*.

### Tip

> You may want to symlink, using the *ln* command, the existing file locations (listed in the RPM installation section earlier in this chapter) to the new locations of the files because the default install locations are not the same as when the RPM installs the files. Failure to do this could result in your Web server process not being started automatically at system startup. I would strongly recommend that you stick with the RPM version of Apache until you really know your way around what happens at system startup.

## File Locations After Manual Installation

As of version 1.3.4, all of the files are placed in various subdirectories of /usr/local/apache (or whatever directory you specified with the -prefix parameter). Before version 1.3.4, files were placed in /usr/local/etc/httpd.

The following is a list of those directories that are used by Apache, as well as brief comments on their usage.

- /usr/local/apache/conf—This directory contains all the Apache configuration files, which include access.conf, httpd.conf, and srm.conf. See the section on configuration files later in this chapter.
- /usr/local/apache—the cgi-bin, icons, and htdocs subdirectories contain the CGI programs, standard icons, and default HTML documents, respectively.
- /usr/local/apache/bin—The executable programs are placed in this directory.
- /usr/local/apache/logs—The server log files are placed in this directory. By default, there are two log files—access_log and error_log—but you can define any number of custom logs containing a variety of information. See the section on logging later in this chapter.

## Runtime Server Configuration Settings

At this point, you have successfully installed the Apache server one way or another. It will run, but perhaps not quite the way that you want it to. This section talks about configuring the server so that it works exactly how you want it to work.

Traditionally, Apache had the runtime configurations in three files: httpd.conf, access.conf, and srm.conf. This was mainly because that’s how the config files were written for NCSA, and Apache grew out of NCSA. And although there was some logic behind the original decision to split configuration options into three files, this made less and less sense over time—especially since you could put any configuration option in any file and it would work.

So, starting with Apache 1.3.4, the runtime configurations are stored in just one file—httpd.conf. The other files are still there, but they contain only a comment telling you that the files are there for purely historical reasons and that you should really put all of your configuration files in httpd.conf.

### Note

You can still use the three-configuration-file approach if you really want to. It makes sense to some people. However, the distinction between what should go in one file or another has become increasingly blurred over the years.

If you want to keep using the three-file system, I’ve noted when these files appeared in *srm.conf* or *access.conf* prior to version 1.3.4.

Apache reads the data from the configuration file(s) when the parent process is started (or restarted). You can also cause the Apache process to reload configuration information with the command `/etc/rc.d/init.d/httpd reload`. This is discussed later in the section “Starting and Stopping the Server.”

You perform runtime configuration of your server with *configuration directives*, which are commands that set some option. You use them to tell the server about various options that you want to enable, such as the location of files important to the server configuration and operation. Configuration directives follow this syntax:

```
directive option option…
```

You specify one directive per line. Some directives only set a value such as a filename, whereas others let you specify various options. Some special directives, called *sections*, look like HTML tags. Section directives are surrounded by angle brackets, such as `<directive>`. Sections usually enclose a group of directives that apply only to the directory specified in the section:

```
<Directory someDir/inYour/tree>
directive option option
directive option option
</Directory>
```

All sections are closed with a matching section tag that looks like `</directive>`. Note that section tags, like any other directives, are specified one per line.

### Editing httpd.conf

Most of the default settings in the config files are okay to keep, particularly if you have installed the server in a default location and are not doing anything unusual on your server. In general, if you don’t understand what a particular directive is for, you should leave it set to the default value.

Table 12.1 lists some of the settings that you *might* want to change.

## TABLE 12.1 Some Commonly Used Configuration Directives

| Directive | Description |
| :------- | :------- |
| ServerType | This is mentioned more as a curiosity than anything else. The two server types are **standalone** and **inet**. You will want this to be **standalone** in almost every imaginable case. Setting the *ServerType* to *inet* will cause a new server to be spawned to handle every incoming HTTP request. That server will then die off immediately when the request has been served. This is presumably useful for testing configuration changes because the configuration files will be reloaded each time a new server process is spawned. Of course, this is extremely slow, since you have the overhead of server startup with every request. |
| ServerRoot | This directive sets the absolute path to your server directory. This directive tells the server where to find all the resources and configuration files. Many of these resources are specified in the configuration files relative to the *ServerRoot* directory. Your *ServerRoot* directive should be set to */etc/httpd* if you installed the RPM and */usr/local/apache* (or whatever directory you choose when you compiled Apache) if you installed from the source. |
| Port | The *Port* directive indicates which port you want your server to run on. By default, this is set to 80, which is the standard HTTP port number. You may want to run your server on another port, such as for running a test server that you don’t want people to find by accident. Don’t confuse this with real security! See the section “Authentication and Access Control” for more information on how to secure parts of your Web server. |
| User and Group | The *User* and *Group* directives should be set to the UID and group ID (GID) that the server will use to process requests. There are generally two ways to set this up. The most common way is to set user to *nobody* and group to *nobody*. The other way, which is used in Red Hat, is to set them to a user with few or no privileges. In this case, they are set to user *apache* and group *apache*. As you can imagine, this is a user defined specifically to run Apache. If you want to use a different UID or GID, you need to be aware that the server will run with the permissions of the user and group set here. This means that in the event of a security breach, whether on the server or (more likely) in your own CGI programs, those programs will run with the assigned UID. If the server runs as *root* or some other privileged user, someone can exploit the security holes and do nasty things to your site. Always think in terms of the specified user running a command like *rm -rf /*, since that would wipe all files from your system. That should convince you that leaving this as a user with no privileges is probably a good thing. |
