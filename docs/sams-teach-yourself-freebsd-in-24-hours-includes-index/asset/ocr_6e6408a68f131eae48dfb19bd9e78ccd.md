As a general security measure in the operating system, port numbers lower than 1024 can only be opened by the root user. Because of this, the parent Apache process needs to be run as root. However, the child processes are usually run as nobody, which is an account that has no special privileges and cannot log in to the system.

Note that Apache is subject to UNIX file permissions. Thus, in order for files and directories to be available to visitors to your site, they need to be readable by the user nobody. Usually, this will not be an issue because the files can just be world readable.

After the Apache server has been installed and started, you should be able to access it loading the following address into your Web browser (if you are attempting to access it from the same machine the Web server is running on.)

```
http://127.0.0.1
```

If the server is running, you should get the default Apache welcome page. Of course, you will want to replace this page with whatever the home page of your Web site will be.

Note that if the server is currently on a network, you should also be able to access the Web server from a different computer by entering the IP address of the Web server machine into the Web browser.

# CGI

CGI stands for Common Gateway Interface. It is a method through which Web servers can run external programs and even pass data entered on a Web page form to an external program. The external program can also send output back to the Web server, which can then be displayed on a Web page, for example.

Although these external programs are commonly referred to as CGI scripts, they do not necessarily have to be scripts. CGI programs can be written in any language. The most common language for writing CGI scripts in UNIX is Perl. However, CGI can also be written in Python, TCL, shell script, AWK, SED, Java, or even a fully compiled language such as C. A discussion of how to write and use CGI scripts in your Web pages is beyond the scope of this book. However, we will cover how to enable CGI in the Apache server, as well as how to ensure that they don't end up compromising the security of your system.

# Configuring Apache for CGI

CGI scripts generally have addresses that look something like the following:

```
http://www.mycompany.com/cgi-bin/myscript.pl
```