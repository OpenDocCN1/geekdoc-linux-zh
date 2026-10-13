To access the script via a Web browser, I request the following URL:

```
http://wormhole.nitec.com/~kabir/test.pl
```

A CGI script is executed only after it passes all the security checks performed by suEXEC. suEXEC also logs the script request in its log file.

The log entry for my request looks as follows:

```
[1998-12-23 16:00:22]: uid: (kabir/kabir) gid:
(kabir/kabir) cmd: test.pl
```

If you are really interested in knowing that the script is running under the user's UID, insert a sleep command (such as sleep(10);) inside the foreach loop, which will slow down the execution and allow you to run commands such as top or ps on your Web server console to find out the UID of the process running test.pl. You also can change the ownership of the script using the chown command, try to access the script via your Web browser, and see the error message that suEXEC logs. For example, when I change the ownership of the test.pl script in the ~kabir/public_html directory as follows:

```
chown root test.pl
```

I get a server error, and the log file shows the following line:

```
[1998-12-23 16:00:22]: uid/gid (500/500) mismatch with directory (500/500) or program (0/500)
```

Here, the program is owned by UID 0, and the group is still kabir (500), so suEXEC refuses to run it, which means suEXEC is doing what it is supposed to do.