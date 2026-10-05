# Networking and Internet Services

# PART II

You might also want to check the Sendmail Frequently Asked Questions (FAQ) located at http://www.sendmail.org/faq. This is a useful source of information on common configuration mistakes or questions on how to set up a particular configuration.

Also take note that the Sendmail Installation and Operating Guide (SIOG) is in the doc/out subdirectory.

Now run cd and ls to see what files are in the source directory:

```
[root@gonzo src]# cd ../sendmail-8.9.3/src
[root@gonzo src]# ls
```

```
Build clock.c err.c m1.c savemail.c sysexits.h
Makefile.m collect.c headers.c mime.c sendmail.@ trace.c
README conf.c ldap_map.h newalies.0 sendmail.8 udb.c
TRACEFLAGS conf.h macro.c newalies.1 sendmail.h useful.h
alias control.c mailq.0 parseaddr.c snprintf.c usersmpt.c
aliases convime.c mailq.1 pathways.h svrvrsmptp.c util.c
aliales.0 daemon.c mailsts.h queue.c version.c
aliales.5 deliver.c main.c readof.c stab.c
arpadate.c domain.c makesmail recipient.c stats.c
cndefs.h envelope.c map.c safefile.c sysexits.c
```

Thankfully, Eric Allman and the sendmail crew have done a fantastic job of making the installation process very straightforward. To compile your new version of sendmail, simply run the following (from the sendmail src directory):

```
[root@gonzo src]# ./Build
```

and watch it build.

This creates a directory obj.* that contains the result of the compilation (so you can build sendmail for different machines or operating systems in the same sources). Also check the BuildTools/Site and BuildTools/OS directories for further configuration.

# Caution

Before you install the new sendmail configuration, be sure to make a backup of any files you are going to replace, especially the old sendmail daemon you have. In the event that the new sendmail doesn't work for you, you will need to restore the old versions while you troubleshoot the new version.

![](bbox=[0.158, 0.733, 0.918, 0.903])