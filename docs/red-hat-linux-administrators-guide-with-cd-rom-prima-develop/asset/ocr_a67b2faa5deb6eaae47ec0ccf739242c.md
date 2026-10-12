If the sendmail daemon is running, a message similar to the following will be printed to your display. Verify that the version number that you just installed is the same as that which is printed to your screen on the last line:

```
$ telnet localhost 25
    Trying 127.0.0.1...
    Connected to localhost.localhostdomain.
    Escape character is '^J'.
220 antares.astronomy.org ESMTF Sendmail 8.11.1/8.11.0; Mon, 15 Aug
2000 10:30:00 -0700
```

You are now ready to try out your connection. Once you have a sendmail con-nection, enter the following:

```
hello antares.astronomy.org
```

Alternatively, enter the name of the server on which sendmail is running. The command should return the following message:

```
pleased to meet you.
```

Congratulations, you now have sendmail up and running. Try sending a mes-sage. If you have a viable Internet connection and your domain hostname is fully qualified, mail will proceed directly to its destination. Most sendmail commands or options use all uppercase letters. Here is an example e-mail from myself to another fictional user whose domain does actually exist:

```
MAIL FROM: kerry@antares.astronomy.org
250 kerry@antares.astronomy.org... Sender ok
RCPT TO: calvin@vega.nasa.gov
250 calvin@vega.nasa.gov... Recipient ok
DATA
354 Enter mail, end with "." on a line by itself
This is just a test
.
250 MAA19900 Message accepted for delivery
quit
221 antares.astronomy.org closing connection
Connection closed by foreign host.
```