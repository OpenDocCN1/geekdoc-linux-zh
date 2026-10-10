Table 4.4 is incomplete; sed (like awk) is quite complex, and this section merely introduces it.

You can use sed to further clean up the output of the preceding grep/awk command. For instance, if you want only the e-mail address and not the to= string and surrounding punctuation, you could use the following command:

```
$ grep "to=" /var/log/mail.log | awk '/.*/ {print $7} | sed {s/to=<>///}\nsed [s/^>\,///]
```

The backslash character (\) is used to signify that the following character should be interpreted as a literal part of the regular expression rather than as a special control character.

The result of the preceding command will be a series of e-mail addresses, one to a line, as in:

+   - jennie@luna.edu
+   - frank@example.com

Although they’re conceptually simple, both sed and awk are very complex tools; even a modest summary of their capabilities would fill a chapter. You can consult their man pages for basic information, but to fully understand these tools, you may want to consult a book on the subject, such as Dale Dougherty and Arnold Robbins’ sed & awk, 2nd Edition (O’Reilly, 1997).

# Using Additional Log File Analysis Tools

Manually examining log files with tail, less, and similar tools can be informative, but other tools exist to help you analyze your log files. One of these is Logcheck, which is part of the Sentry Tools package (http://sourceforge.net/projects/sentrytools/). This package comes with some distributions, such as Debian. Unfortunately, it requires a fair amount of customization for your own system, so it’s most easily implemented if it comes with your distribution, preconfigured for its log file format. If you want to use it on another distribution, you must edit the logcheck.sh file that’s at the heart of the package. This file calls the logtail utility that checks log file contents, so you must configure the script to check the log files you want monitored. You can also adjust features such as the user who’s to receive violation reports and the locations of files that contain strings for which the utility should look in log files. Once it’s configured, you call logcheck.sh in a cron job. Logcheck then e-mails a report concerning any suspicious system logs to the user defined in logcheck.sh (root, by default).