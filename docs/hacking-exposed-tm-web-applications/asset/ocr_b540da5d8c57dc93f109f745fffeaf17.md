# Chapter 13: Case Studies

contain information such as the location of secret PGP keys. It revealed roots located in ineffective chroot environments: /home/jail/usr/bank/AXIS.cfg.

One unique thing about the directory traversal exploit that enabled us to view directory contents as well as files. We were able to poke around the Web server's directories and discover Web server configuration files (magnus.conf for i). We discovered that the ASP was using hosting sites for over dozen banks—on the same Web server! More importantly, we found a directory that contained the administration scripts for the Web server.

The initial survey of the Web application identified an administration interface in the /admin URI. Unfortunately, the server seemed to use proper ACLs that limited access to specific IP addresses for this directory. We verified this by viewing the configuration file for the /admin site.

What we also discovered in the file system with our friendly DIML_FILE parameter was that some older shells had never been removed. UNIX shells are the antithesis of secure CGI programs. A command shell is intended to be a powerful, complex interface to the operating system. Consequently, there are numerous methods for executing arbitrary commands or otherwise breaking out of the shell. One script presented a set of options for the user to generate a customized http log report:

```
/cgi-bin/admin/allstats.cgi
```

This form POSTed a long string of parameters starting with:

```
server_name=...
```

These arguments were passed to the a_form.cgi script. We verified this by checking the "action" tag:

```
/cgi-bin/admin/a_form.cgi
```

If we passed the data to run: server_name=... argument list, the a_form.cgi produces this output:

```
<Attempting to analyze -n https-80-bank-64 -x
-i /u/webs/logs/https-80-bank-64/access -c hnrfeuokc -t
s5m5h24 -1 c55h5 ptl 2>&</p>
```

The arguments are actually being passed to a script called analyze. The script was also nice enough to echo the command line. It was time to see what analyze could do. First, we tried to pass the ls command to the script:

```
/cgi-bin/admin/a_form.cgi?server_name=ls...
```