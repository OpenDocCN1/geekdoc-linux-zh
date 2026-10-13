There's an alternative, if the filesystem with the /home directory has been mounted with the Access Control Lists discussed in Chapter 4. You could create ACLs on the noted directories specifically for the user named apache. For user michael and his home directory, that would work with the following commands:

```
# setfacl -m u:apache:x /home/michael
# setfacl -m u:apache:x /home/michael/public_html
```

Whether permissions are set directly, or through ACLs, the logical next step as a web server, is to add an index.html file to this directory. For our purposes, it can be a text file. The commented stanza that follows is one excellent way to help keep home directories so shared a bit more secure.

In addition, SELinux must be configured to “Allow HTTPd To Read Home Directories,” associated with the httpd_enable_homedirs boolean. You can activate that option either with the SELinux Administration tool or with the setsebool -P httpd_enable_homedirs 1 command.

At that point, a web server that's directed to user michael's directory can read an index.html file in the public_html subdirectory. Figure 14-8 illustrates the result, where the noted text is the only contents of index.html.

Of course, additional changes are suggested in the httpd.conf file. If you activate the stanza that starts with the <Directory /home/*/public_html> container, it supports additional levels of access to the public_html subdirectory of all user's home directories.

```
#<Directory /home/*/public_html>
```

# FIGURE 14-8

View the index.
html file for user
michael

![](bbox=[0.35, 0.68, 0.85, 0.92])