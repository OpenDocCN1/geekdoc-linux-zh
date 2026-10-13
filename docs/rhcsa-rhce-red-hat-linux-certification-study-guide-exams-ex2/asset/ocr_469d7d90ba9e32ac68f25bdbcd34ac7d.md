# Lab 7

The process required to set up a group-managed directory is a hybrid. The overall basic steps are as follows.

+   - Create a regular user and group named techsupport. While not required, it can be helpful to configure that user with a higher UID and GID, to avoid interfering with other future users and groups.
+   - Make the other users a member of that group named techsupport.
+   - Set up appropriate permissions to support access by members of the techsupport group, normally 2770 permissions. It should also include either regular executable permissions by other users, or executable permissions by the user named apache.
+   - Create a public_html/ subdirectory of the new user's home directory.
+   - Set up an index.html file in that subdirectory. It should already be set with ownership by the techsupport group.

# Lab 8

The specified hello.pl script should include something like the following entries:

```
#!/usr/bin/perl
print "Content-type: text/html\n\n";
print "Hello World";
```

That script should be located in the directory specified by a ScriptAlias /cgi-bin/ directive, in the big.example.com virtual host container. That container should also include the Options ExecCGI, and AddHandler cgi-script .pl directives. While it's normally best to have scripts in the same DirectoryRoot as that configured for a virtual host, it's not required.

In addition, the permissions on the hello.pl file should be set to 755, and the SELinux contexts on the file (and directory) should be of the httpd_sys_script_exec_t file type. Of course, you'll have run an appropriate semanage fcontext -a command to make the change permanent, with the SELinux file type documented in the file_contexts.local file in the /etc/selinux/targeted/contexts/files directory. In any case, a successful result is as suggested in the lab question.