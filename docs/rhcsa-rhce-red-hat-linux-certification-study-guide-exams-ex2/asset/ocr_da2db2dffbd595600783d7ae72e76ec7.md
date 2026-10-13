If CGI scripts are required for one of the previously configured virtual hosts, you'll need to set up a different ScriptAlias and a corresponding <Directory> container. For the vhost1.example.com site described previously, I add the following directive:

```
ScriptAlias /cgi-bin/ /www/docs/vhost1.example.com/cgi-bin/
```

The Apache documentation continues with instructions on how you can write a simple CGI script.

# Set Up a Simple CGI Script

The Apache documentation includes instructions on how to set up a simple CGI script, in the Perl programming language. Make sure the httpd-manual package is installed, and the local httpd service is active. In a browser, navigate to http://localhost/manual. Under the How-To / Tutorials section, click CGI: Dynamic Content. Scroll down to the "Writing a CGI Program" section.

In this section, the Apache documentation suggests a simple Perl script, called hello.pl, based on the following code:

```
#!/usr/bin/perl
print "Content-type: text/html\n\n";
print "Hello, World!";
```

The first line is similar to the #!/bin/bash found in many scripts; in this case, perl is the command interpreter. The content type is declared, followed by two carriage returns (as symbolized by the \n\n). The final line prints the expression commonly used for introductory program scripts. Such scripts need to be executable, with 755 permissions. In other words, once the hello.pl file is saved, you'd apply the noted permissions with the following command:

```
# chmod 755 hello.pl
```

Run the ls -Z command on the script. In the /var/www/cgi-bin directory, it should inherit the httpd_sys_script_exec_t SELinux file type associated with the directory. If necessary, you can apply the file type to the file and directory with the chcon command, and then make sure the file type stays applied after a SELinux relabel with the semanage fcontext -a command. Both commands were described earlier in this chapter and in Chapter 11.