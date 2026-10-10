
Finally, log files are much less useful when no one is reading them. Take some time out every once in a while to look over your log files, and get a feeling for what they look like on a normal day. Knowing this can help make unusual things stand out.

## Apply All New System Updates

Most Linux users install from a CD-ROM. Due to the fast-paced nature of security fixes, new (fixed) programs are always being released. Before you connect your machine to the network, it's a good idea to check with your distribution's ftp site and get all the updated packages since you received your distribution CD-ROM. Many times these packages contain important security fixes, so it's a good idea to get them installed.

# What to Do During and After a Break-In

So you have followed some of the advice here (or elsewhere) and have detected a break-in? The first thing to do is to remain calm. Hasty actions can cause more harm than the attacker would have caused.

## Security Compromise Underway

Spotting a security compromise underway can be a tense undertaking. How you react can have large consequences.

If the compromise you are seeing is a physical one, odds are you have spotted someone who has broken into your home, office, or lab. You should notify your local authorities. In a lab, you might have spotted someone trying to open a case or reboot a machine. Depending on your authority and procedures, you might ask them to stop, or contact your local security people.

If you have detected a local user trying to compromise your security, the first thing to do is confirm they are in fact who you think they are. Check the site they are logging in from. Is it the site they normally log in from? No? Then use a nonelectronic means of getting in touch. For instance, call them on the phone or walk over to their office/house and talk to them. If they agree that they are on, you can ask them to explain what they were doing or tell them to cease doing it. If they are not on, and have no idea what you are talking about, odds are this incident requires further investigation. Look into such incidents, and have lots of information before making any accusations.

If you have detected a network compromise, the first thing to do (if you are able) is to disconnect your network. If they are connected via modem, unplug the modem cable; if they are connected via Ethernet, unplug the Ethernet cable. This will prevent them from doing any further damage, and they will probably see it as a network problem rather than detection.

If you are unable to disconnect the network (if you have a busy site, or you do not have physical control of your machines), the next best step is to use something like tcpwrappers or ipfwadm to deny access from the intruder’s site.

If you can’t deny all people from the same site as the intruder, locking the user’s account will have to do. Note that locking an account is not an easy thing. You have to keep in mind .rhosts files, ftp access, and a host of possible backdoors.

After you have done one of the above (disconnected the network, denied access from their site, and/or disabled their account), you need to kill all their user processes and log them off.

You should monitor your site well for the next few minutes, as the attacker will try to get back in—perhaps using a different account, and/or from a different network address.

## Security Compromise Has Already Happened

So you have either detected a compromise that has already happened or you have detected it and locked (hopefully) the offending attacker out of your system. Now what?

### Closing the Hole

If you are able to determine what means the attacker used to get into your system, you should try to close that hole. For instance, perhaps you see several ftp entries just before the user logged in. Disable the ftp service and check and see if there is an updated version, or if any of the lists know of a fix.

Check all your log files, and make a visit to your security lists and pages and see if there are any new common exploits you can fix. You can find Caldera security fixes at http://www.caldera.com/tech-ref/security/ . Red Hat has not yet separated their security fixes from bug fixes, but their distribution errata is available at http://www.redhat.com/errata .

Debian now has a security mailing list and Web page. See http://www.debian.com/security/ for more information.

It is very likely that if one vendor has released a security update, most other Linux vendors will as well.

There is now a Linux security auditing project. They are methodically going through all the userspace utilities and looking for possible security exploits and overflows. From their announcement:

> We are attempting a systematic audit of Linux sources with a view to being as secure as OpenBSD. We have already uncovered (and fixed) some problems, but more help is welcome. The list is unmoderated and also a useful resource for general security discussions. The list address is: security-audit@ferret.lmh.ox.ac.uk. To subscribe, send mail to: security-audit-subscribe@ferret.lmh.ox.ac.uk.

If you don’t lock the attacker out, they will likely be back. Not just back on your machine, but back somewhere on your network. If they were running a packet sniffer, odds are good they have access to other local machines.

### Assessing the Damage

The first thing is to assess the damage. What has been compromised? If you are running an Integrity Checker like Tripwire, you can use it to perform an integrity check, and it should help to tell you. If not, you will have to look around at all your important data.

Since Linux systems are getting easier and easier to install, you might consider saving your config files and then wiping your disk(s) and reinstalling, then restoring your user files from backups and your config files. This will ensure that you have a new, clean system. If you have to back up files from the compromised system, be especially cautious of any binaries you restore, as they may be Trojan horses placed there by the intruder.

Re-installation should be considered mandatory upon an intruder obtaining root access. Additionally, you’d like to keep any evidence there is, so having a spare disk in the safe may make sense.

Then you have to worry about how long ago the compromise happened, and whether the backups hold any damaged work. More on backups later.

## Backups, Backups, Backups!

Having regular backups is a godsend for security matters. If your system is compromised, you can restore the data you need from backups. Of course, some data is valuable to the attacker too, and they will not only destroy it, they will steal it and have their own copies; but at least you will still have the data.

You should check several backups back into the past before restoring a file that has been tampered with. The intruder could have compromised your files long ago, and you could have made many successful backups of the compromised file!!!

Of course, there are also a raft of security concerns with backups. Make sure you are storing them in a secure place. Know who has access to them. (If an attacker can get your backups, they can have access to all your data without you ever knowing it.)

## Tracking Down the Intruder

Ok, you have locked the intruder out, and recovered your system, but you're not quite done yet. While it is unlikely that most intruders will ever be caught, you should report the attack.

You should report the attack to the admin contact at the site where the attacker attacked your system. You can look up this contact with whois or the Interim database. You might send them an e-mail with all applicable log entries and dates and times. After sending the e-mail, you should (if you are so inclined) follow up with a phone call. If that admin in turn spots your attacker, they might be able to talk to the admin of the site where they are coming from and so on.

Good crackers often use many intermediate systems, some (or many) of which may not even know they have been compromised. Trying to track a cracker back to their home system can be difficult. Being polite to the admins you talk to can go a long way to getting help from them.

You should also notify any security organizations you are a part of (CERT [http://www.cert.org/] or similar), as well as your Linux system vendor.
