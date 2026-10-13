By far, the most popular item set in this manner is the domain used for outgoing email. Chapter 28, “Email Clients and Servers,” addresses configuration issues and schemes used with sendmail; the m4 configuration system discussed in that chapter is used to accomplish masquerading a domain name.

Simply put, the following two lines are added to your system’s .mc file:

```
MASQUERADE_AS(isp-domain.net)
FEATURE(masquerade_envelope)
```

Afterward, a new /etc/sendmail.cf file is created as follows:

```
cp /etc/sendmail.cf /etc/sendmail.cf.backup
m4 ../m4/cf.m4 yourmcfile.mc > /etc/sendmail.cf
```

Note that you must have the sendmail-cf package installed (not applicable to Debian) to do this (see Chapter 16, “Software Package Management,” for information on package management). After performing this step, sendmail needs to be stopped and started again as follows (for Caldera):

```
/etc/rc.d/init.d/mta stop
/etc/rc.d/init.d/mta start
```

Or (for Debian):

```
/etc/init.d/sendmail restart
```

Or (for Red Hat):

```
/etc/rc.d/init.d/sendmail restart
```

With that done, all outgoing email is sent as username@isp-domain.net. To change the domain name that is used, change the MASQUERADE_AS() line in the system’s .mc file and recompile the /etc/sendmail.cf file.

Setting up systems to read news from a remote NNTP host is another common change to Linux systems. Luckily, it requires fewer steps than masquerading mail addresses.

The address of a remote NNTP news server is typically stored in an environment variable called NNTP​SERVER. Setting this with the bash shell is fairly simple:

```
export NNTP​SERVER=news.isp-domain.net
```

Using the C shell (csh), the command looks more like the following:

```
setenv NNTP​SERVER news.isp-domain.net
```

The command can be placed in the appropriate rc file in a user’s home directory (.profile or .cshrc, respectively) to set the variable automatically every time a shell is started, or it can be placed in one of the main shell configuration files in /etc (profile or csh.cshrc, respectively) to have the variable set systemwide when the system is started.