produces the following output on my sendmail server:

```
Version 8.9.3
  Compiled with: MAP REGEX LOG MATCHGECOS MIME/TQ8
MIME8TO7 NAMED BIND NETINET NETUNIX NENDB NIS QUEUE SCANF
SMTP USERDB XDEBUG


========== SYSTEM IDENTITY (after readcf) ===========
(short domain name) $w = picao
(canonical domain name) $j = picao.nitac.com
(subdomain name) $m = nitac.com
(node name) $k = picao.nitac.com
========== SYSTEM IDENTITY (after readcf) ==========

kabir@nitac.com... deliverable: mailer local, user kabir
```

The `-d0` option causes sendmail to display various items of information about itself. The last line shows how sendmail will handle the given address. Specifying `-d` without any debug level number shows all the debugging information you'll ever want.

# ## Using a test configuration file

When you are modifying sendmail.cf, it is a good idea to create a test version of the/etc/sendmail.cf file and modify only the test copy, so that you don't lose any working configuration. Here is how you can test a new configuration:

+   1. Create a copy of /etc/sendmail.cf with a new name. For this example, call the test configuration /etc/sendmail-test.cf.
+   2. To run sendmail with your new test configuration file, use the -C option. For example,/usr/sbin/sendmail -Csendmail-test.cf uses /etc/sendmail-test.cf.