# Listing 16-2 (continued)

```
else {
    print $thismonth, ",$thisday;
}
$thisyear-100;
if ($thisyear < 0) {
    print " 0",$thisyear;
} else {
    print "",$thisyear;
}
print "</body></body></html>";
```

The first line of the output from a CGI program is a MIME-type header. This is an HTTP header that tells the client what sort of content it is receiving: in the case of this script, the client will be receiving content of the text/html variety. Secondly, the remaining output is in HTML, a format that the web browser understands and will be to display.

However, this script is not quite ready for prime time. When the Apache server starts up, it is running with the permissions of a user separate from the user who create the script. Thus the filesystem permissions of the file need to be changed so it can be read and executed by whatever user the webserver is running as.

```
chmod +x example.cgi
```

+   See Chapter 2 for more detail on using chmod.

All should be set. But most of the time when starting out, a CGI program or script will fail, because of a problem with the program itself, a syntax or logic error. Remember the web server logs are your friends. More than not, if things goes wrong, it will generate a message in the error log. Look first (/var/log/apache2/error.log). The error_log file contains entries about why something did not work. This could be an error from a PHP script or a Perl script, for example, and you will have to use your skills in these languages to understand what the log files are telling you.

Learn to read and manage the error (and access) logs that the web server creates, and you will find that almost all the problems are quickly identified and solved.

+   We discuss Apache logs in Chapter 7.