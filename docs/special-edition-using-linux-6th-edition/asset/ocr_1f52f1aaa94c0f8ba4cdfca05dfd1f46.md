> **Note:** For changes to this file to take effect, you must run the newaliases utility.

# ## Notes on Debian Systems

Although sendmail is sendmail regardless of the system you’re running on (any of the various Linux distributions, or even other UNIX systems), some distribution-specific quirks exist of which you must be aware.

The information in the preceding section will work on Debian, but you need to do a few things in addition to just changing some pathnames and filenames.

Debian has a sendmailconfig script that can be used to do basic sendmail system setup. This script will work for most sendmail installations. Only special or advanced configurations need be added.

When sendmailconfig runs, one of the things it does is create a /etc/mail/sendmail.mc from the debproto.mc file previously mentioned. If this sendmail.mc file does not exist, sendmail will not start at bootup. You might find it easier to use sendmailconfig first, and then if the resulting configuration doesn’t fit your needs, modify the sendmail.mc file and use it to create subsequent sendmail.cf files.

You can do this by making modifications by hand to the /etc/mail/sendmail.mc file and invoking sendmailconfig again. Changes added to the bottom of the file will not be touched.

Debian also uses a differently named file as its SysV boot file. This file is /etc/init.d/sendmail, and takes any of the following arguments: start, stop, restart, reload, force-reload, or debug.

# ## Notes on Red Hat Systems

Red Hat maintains a sendmail.mc file in /etc as well as /usr/lib/sendmail-cf/cf. The redhat.mc file in the sendmail-cf directory and the /etc/sendmail.cf file are basically copies of each other. Decide which you want to use, modify it, and create the new sendmail.cf from it. A fairly generic sendmail.cf is provided during installation.

For bootup, Red Hat’s init script looks in a file /etc/sysconfig/sendmail to determine whether to run. If you want sendmail to run, just make sure that /etc/sysconfig/sendmail contains a line DAEMON=yes. Change to no to stop running sendmail at bootup.

In the /etc/sysconfig/sendmail file you can also modify the queue setting. By default, Red Hat runs the queue once an hour. Just change the 1h to 15m or 30m to run the queue more often (every 15 or 30 minutes).

# # Delivery Agents

The Delivery Agent is very similar to the user agent; it is merely a method of getting the actual message into the recipient’s hands. For example, with conventional mail the recipient