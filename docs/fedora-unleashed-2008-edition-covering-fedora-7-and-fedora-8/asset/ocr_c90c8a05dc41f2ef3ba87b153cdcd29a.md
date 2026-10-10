# ## **Editing httpd.conf**

Most of the default settings in the config file are okay to keep, particularly if you've installed the server in a default location and aren't doing anything unusual on your server. In general, if you don't understand what a particular directive is for, you should leave it set to the default value.

The following sections describe some of the configuration file settings you *might* want to change concerning operation of your server.

# ### **ServerRoot**

The `ServerRoot` directive sets the absolute path to your server directory. This directive tells the server where to find all the resources and configuration files. Many of these resources are specified in the configuration files relative to the `ServerRoot` directory.

Your `ServerRoot` directive should be set to `/etc/httpd` if you installed the `RPM` or `/usr/local/apache` (or whatever directory you chose when you compiled Apache) if you installed from the source.

# ### **Listen**

The `Listen` directive indicates on which port you want your server to run. By default, this is set to 80, which is the standard HTTP port number. You might want to run your server on another port──for example, when running a test server that you don't want people to find by accident. Don't confuse this with real security! See the “File System Authentication and Access Control” section for more information about how to secure parts of your web server.

# ### **User and Group**

The `User` and `Group` directives should be set to the UID and group ID (GID) the server uses to process requests. In Fedora, set these configurations to a user with few or no privileges. In this case, they're set to user `apache` and group `apache`─a user defined specifically to run Apache. If you want to use a different UID or GID, be aware that the server runs with the permissions of the user and group set here. That means in the event of a security breach, whether on the server or (more likely) in your own CGI programs, those programs run with the assigned UID. If the server runs as `root` or some other privileged user, someone can exploit the security holes and do nasty things to your site. Always think in terms of the specified user running a command such as `rm -rf /` because that would wipe all files from your system. That should convince you that leaving `apache` as a user with no privileges is probably a good thing.

Instead of using names to specify the `User` and `Group` directives, you can specify them with the UID and GID numbers. If you use numbers, be sure that the numbers you specify correspond to the user and group you want and that they're preceded by the pound (\#) symbol.

Here's how these directives look if specified by name:

```
User apache
Group apache
```