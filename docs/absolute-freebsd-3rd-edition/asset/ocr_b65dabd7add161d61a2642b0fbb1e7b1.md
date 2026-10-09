In my experience, the phrase *enterprise network* is synonymous with “we have lots of ancient stuff that nobody dares touch.” Jails can help you cope with some of these systems. In 2014, I worked at a company that ran a critical custom-built PHP and MySQL application on FreeBSD 4.10. I don’t know when this server was installed, but FreeBSD 4.11 came out in January 2005, so: before then. This application used ancient versions of Perl, PHP, OpenSSL, and more.

Worse, this application lived on a repurposed desktop machine. With a standard-issue, high-quality desktop hard drive. I hid a spare desktop machine of the same vintage under my desk, just so I had a hope of getting FreeBSD 4.10 onto it. The most proper solution was to rewrite or replace this application. Several sysadmins had faced that task—and failed. I decided to virtualize it. FreeBSD 4.10 doesn’t run well on VMware—yes, you can find de(4) and fxp(4) drivers, but they’re for versions of those cards over a decade old. Here’s how I got this ancient FreeBSD system into a jail.

Drop to single-user mode. Unmount */proc*—yes, FreeBSD 4 still used */proc*. Those were the days. Tar up the entire filesystem, including temporary directories, like */usr/obj*, */usr/ports*, */var/tmp*, and suchforth. By modern standards, they won’t use much space at all, and you have no way to know what files you might need later. You can probably find an old PHP 5.0.whatever tarball out on the internet, but that would involve work.

Copy the tar file to your jail host and extract it in your jail directory.

```
# tar -C /jail/oldserver -xvpf oldserver.tgz
```

Be sure to use the -p flag to preserve permissions.

Now look at /etc/rc.conf. The jail host will handle all networking functions, so turn off any statements that set IP addresses or set routes. Get rid of daemons that provide services the jail host offers, such as time, packet filters, and SSH. Your jailed host needs only the functions that directly support the application. In this case, I needed Apache and MySQL.