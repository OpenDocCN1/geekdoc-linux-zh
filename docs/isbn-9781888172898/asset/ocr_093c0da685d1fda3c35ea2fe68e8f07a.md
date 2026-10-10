/usr/doc/HTML contains the HTML versions of all the HOWTOs and the *Linux Installation and Getting Started* guide. To view things here, just use a WWW browser like redbaron from Red Hat Software, or arena. You would do something like:

```
cd /usr/doc/HTML
arena index.html
```

/usr/doc/FAQ contains ASCII version (and some HTML versions) of some popular FAQs, including the RedHat-FAQ. All of them can be viewed using more or less.

# 6.1.4 The “locate” Command

When you don’t know the full name of a command or file, but need to find it, you can usually find it with locate. locate uses a database to find all files on your system. Normally, this database gets built from a cron job every night. This won’t happen, however, if your machine isn’t booted into Linux all the time. So, if that is the case, you may occasionally want to run the following command:

```
/etc/cron.daily/updatedb.cron
```

You will need to be root on your system when doing that. That will allow locate to work properly.

So, if you know you need to find all the “finger” files, you could run:

```
locate finger
```

It should return something like:

```
/usr/bin/finger
/usr/lib/irc/script/finger
/usr/man/man1/finger.1
/usr/man/man8/in.fingerd.8
/usr/sbin/in.fingerd
```