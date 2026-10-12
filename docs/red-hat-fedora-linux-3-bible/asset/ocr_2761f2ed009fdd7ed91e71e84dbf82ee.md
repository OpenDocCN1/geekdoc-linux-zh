# Disabling indexes in root directory

The following directives disable indexing for the root directory (probably /var/www/html), so that your index.html, or the default one put there by the Fedora Project, is displayed when that directory is requested. (The default way of listing the contents of directories on your Apache Web server is defined in the “Defining Indexing” section later in this chapter.)

```
# # Disable autoindex for the root directory, and present a
# default Welcome page if no other index page is present.
#
<LocationMatch "\*/$">
    Options -Indexes
    ErrorDocument 403 /error/noindex.html
</LocationMatch>
```

# Identifying user directories

If you have multiple users on your server and you want each to be able to publish their own Web content, it is common practice to identify a directory name that users can create in their own home directories to store that content. When you identify the name that is appended to a user’s home directory, that directory is used to respond to requests to the server for the user’s name(~user). This directory name used to be set to public_html by default; however, it is now turned off by default.

To allow access to your users’ personal Web pages, add a comment character (#) to the UserDir disable line. Then remove the # from the UserDir public_html line to make users’ personal public_html directories accessible through the Web server. After removing extra comment lines, the following text shows what the enabled section looks like:

```
# UserDir: The name of the directory which is appended onto a user’s
# home directory if a ~user request is received.

<IfModule mod_userdir.c>
#  UserDir disable
    UserDir public_html
</IfModule>
```

Besides uncommenting the UserDir public_html line shown in the previous example, you must make both the user’s home directory and public_html directory executable by everyone in order for the UserDir directive to allow access to a particular user’s public_html directory. For example, the user cjb could type the following to make those directories accessible.

```
$ chmod 711 /home/cjb
$ mkdir /home/cjb/public_html
$ chmod 755 /home/cjb/public_html
```