This tells you that the suEXEC is active. Now, test suEXEC’s functionality. In the `httpd.conf` file, add these lines:

UserDir public_html
AddHandler cgi-script .pl

The first directive (UserDir) sets the document root of a user’s Web site to be `~username/public_html`, where username can be any user on the system. The second directive associates the cgi-script handler with the .pl files. This is done so that Perl scripts with .pl extensions can run as CGI scripts. For this test, you will need a user account. In this example, I use the host wormhole.nitec.com and a user called kabir. Copy the script shown in Listing 18-4 to a file called test.pl and put it in a user’s public_html directory. In my case, I put the file in the `~kabir/public_html` directory.

# ## Listing 18-4: A CGI Script to Test suEXEC Support

```
```perl
#!/usr/bin/perl
#
# Make sure the preceding line is pointing to the
# right location. Some people keep perl in
# /usr/local/bin.

my ($key,$value);
  print "Content-type: text/html\n\n";
  print "<h1>Test of suEXEC<h1>";

  foreach $key (sort keys %ENV){
    $value = $ENV{$key};
    print "$key = $value <br>";
  }

  exit 0;
```
```

To access the script via a Web browser, I request the following URL: http://wormhole.nitec.com/~kabir/test.pl.

A CGI script is executed only after it passes all the security checks performed by suEXEC. suEXEC also logs the script request in its log file. The log entry for my request looks as follows:

[2001-03-29 16:00:22]: uid: (kabir/kabir) gid: (kabir/kabir) cmd: test.pl

If you are really interested in knowing that the script is running under the user’s UID, insert a sleep command (such as `sleep(10)`) inside the `foreach` loop, which will slow the execution and allow you to run commands such as `top` or `ps` on your Web server console to learn the UID of the process running test.pl. You also can