```
```perl
close(FP);
close(OUT);
}

sub syntax{
    print <<SYNTAX;

makesite <virtual Internet domain>
Example: makesite nitec.com

SYNTAX
    exit 0;
}
```
```

The purpose of this Perl script is to allow you to create a virtual Web site with the proper DNS and Apache Web server configuration without doing many file-editing tasks. For example, suppose you want to create a new Web site called www.newdomain.com. To do this manually, you would have to do the following:

+   1. Add a new zone statement in the /etc/named.conf file for newdomain.com.
+   2. Add a new zone file for newdomain.com in the working directory of the name server. I would have to create this from scratch or copy and modify an existing domain file.
+   3. Create a Web site document root and CGI script directory for the domain in the appropriate Web space on the server.
+   4. Modify the Apache Server configuration file so that Apache treats www.newdomain.com as a new Web site.

Because manually configuring these important files can be error-prone, you should write the makesite script to do all of these steps. For example, to create the www.newdomain.com site with the proper DNS and Apache configuration, you can run the following:

```
```bash
makesite newdomain.com
```
```