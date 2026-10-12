
## Initializing the Tripwire database

The first of the four modes that Tripwire can run in is database initialization mode. This mode creates a new checksum database for files on your system. While logged in as root, type the following command:

```
# tripwire --init
```

You are prompted for your site passphrase, after which the checksum database will be built. The database is written to the file /var/lib/tripwire/host.twd, where host is replaced by your computer's host name.

Tripwire selects which files and directories to checksum by examining its policy file. Tripwire ships with a policy file that is appropriate for most newly installed Red Hat Linux systems, but it is possible that it will try to look for a few files that your system does not contain. If this happens, you will see error messages similar to this:

```
### Warning: File system error.
### Filename: /usr/bin/dos
### No such file or directory
### Continuing...
```

These error messages do not affect the creation of the checksum database, but they can make it difficult to recognize real error messages. To get rid of them, you must modify the policy file.

## Rebuilding the policy file

A Tripwire policy file is used to describe the behavior that is expected of the system and data files. Tripwire uses the policy file information to create a snapshot of the file system. Later, this snapshot (referred to as the baseline) is compared against the running system, to see if your system has been modified by someone trying to break in.

To modify the policy file for Tripwire, you must first edit the text configuration file /etc/tripwire/twpol.txt. Open the file in an editor and comment out the lines that mention those missing files that resulted in error message. For example, if you wish to get rid of the error message for the missing /usr/bin/dos file, look for the following line in the policy text file:

```
/usr/bin/dos      -> $(SEC_SUID)  ;
```

Comment out the line by placing a # character at the beginning of it. It should now look like this:

```
#  /usr/bin/dos      -> $(SEC_SUID)  ;
```

You now must process the policy text file and create the encrypted and digitally signed policy file that Tripwire actually uses when creating or checking the checksum database. Type the tripwire command, passing it the --update-policy parameter and the name of the policy text file:

```
# tripwire --update-policy /etc/tripwire/twpol.txt
```

You will be prompted for your site and local passphrases. After that, a new policy will be built. You can then rebuild the checksum database with the `tripwire --init` command. The "No such file" error messages should not appear this time.

## Checking file integrity

After the checksum database is built, you should periodically run Tripwire in integrity-checking mode. Integrity-checking mode will recompute the checksum for each file and check it against the checksum stored in the database, printing a warning message for any files that have changed. Use the `--check` parameter to do this:

```
# tripwire --check
```

Normally, no error messages will be reported. If, however, a file has been modified, you may receive a message that indicates that a cracker has gotten into your system and modified some of the operating system files, such as the `telnetd` program. The `telnetd` program may have been replaced with a version containing a backdoor through your security. It is critical that you replace any altered programs with the original versions from your Linux install CD or from a valid Linux distribution FTP site. Also, remove your system from the Internet while you do a thorough audit of your security logs, closing any revealed security holes.

Tripwire may report file changes that are not the result of a break-in. This most often happens when you have upgraded your operating system or installed software patches. Your best strategy is to run a Tripwire check just before installing any upgrades or patches. Assuming that there are no errors, proceed with the upgrade or patch, then use the `tripwire` command to update the checksum database. It is not necessary to completely rebuild the database; you may run Tripwire in update mode to rebuild only the checksums of those files that changed.

## Updating the database

To run Tripwire in update mode, invoke it with the `--update` parameter.

```
# tripwire --update
```

This will recalculate the checksums for any files that have changed since the last update and save those changes to the database. This is much less time-consuming than totally rebuilding the checksum database with the `tripwire --init` command.

> **TIP:** You can greatly improve the security of Tripwire by running it from a read-only media such as a CD-ROM, or at least from a media that is only mounted when Tripwire is run. Also, storing the checksum database on a removable media that is mounted only when needed is another way of improving Tripwire security.

I store my Tripwire executable and database on a CD-R writable CD-ROM drive. You will, of course, need to specify the different file paths when running the `tripwire` command. The `-d` parameter can be used to change the location of the checksum database. On my Linux system ratbert, I run the `tripwire` command by loading my Tripwire CD and typing:

```
# /mnt/cdrom/tss/bin/tripwire --check -d /mnt/cdrom/tss/db/ratbert.db
```

If I upgrade my operating system, I must generate a new database and burn that to a new CD, but that is a small price to pay to be certain that my Tripwire database has not been compromised.

## Protection from Denial-of-Service Attacks

Break-ins are not the only security risk your system may face. Your computer could suffer from a denial-of-service attack. This is an attack that attempts to crash your computer or at least degrade its performance to an unusable level. There are a variety of denial-of-service exploits. Most focus on overloading some system resource, such as your available disk space or your Internet connection. The most common attacks and their defenses are discussed in the following sections.

## Mailbombing

*Mailbombing* is the practice of sending so much e-mail to a particular user or system that the computer's hard drive becomes full. There are several ways to protect yourself from mailbombing. You can install an e-mail-filtering tool such as Procmail or configure your sendmail daemon.

> **CROSS-REFERENCE:** See Chapter 19 for a more complete description of sendmail.

### Blocking mail with Procmail

The Procmail e-mail-filtering tool is installed by default with Red Hat Linux and is tightly integrated with the sendmail e-mail daemon and thus can be used to selectively block or filter out specific types of e-mail. You can learn more about Procmail at the Procmail Web site www.procmail.org.

To enable Procmail for your user account, create a `.procmailrc` file in your home directory. The file should be mode 0600 (readable by you but nobody else). Type in the following, replacing *evilmailer* with the actual e-mail address that is mailbombing you.

```
# Delete mail from evilmailer
:0
* ^From.*evilmailer
/dev/null
```

The online manual page for Procmail explains its capabilities in greater detail. Type `man procmail` at a command prompt to view it. The `procmailrc` and `procmallex` man pages will tell you more about the `.procmailrc` file and give numerous examples of how to selectively process different types of mail. You should also examine the Web page "Timo's procmail tips and recipes" located at www.wasasa.fi/~ts/info/proctips.html.

### Blocking mail with sendmail

The Procmail e-mail tool works quite well when only one user is being mailbombed. If, however, the mailbombing affects many users, you should probably configure your sendmail daemon to block all e-mail from the mailbomber. You do this by adding the mailbomber's e-mail address or system name to the access file located in the /etc/mail directory.

Each line of the access file contains an e-mail address, host name, domain, or IP address followed by a tab and then a keyword specifying what action to take when that entity sends you a message. Valid keywords are OK, RELAY, REJECT, DISCARD, and ERROR. Using the REJECT keyword will cause a sender's e-mail to be bounced back with an error message. The keyword DISCARD will cause the message to be silently dropped without sending an error back. You can even return a custom error message by using the ERROR keyword.

Thus, an example /etc/mail/access file may look similar to this:

```
# Check the /usr/share/doc/sendmail/README.cf file
# for a description of the format of this file. (search for
# access_db in that file) The
# /usr/share/doc/sendmail/README.cf is part of the
# sendmail-doc package.
#
# by default we allow relaying from localhost...
localhost.localdomain	RELAY
localhost	RELAY
127.0.0.1	RELAY
#
# Senders we want to Block
#
evilmailer@yahoo.com	REJECT
stumpy.glaci.com	REJECT
cyberpromo.com	DISCARD
199.170.176.99	ERROR:"550 Die Spammer Scum!"
199.170.177	ERROR:"550 Email Refused"
```

As with most Linux configuration files, lines that begin with a # pound sign are comments. Our list of blocked spammers is at the end of this example file. Note that the address to block can be a complete e-mail address, a full host name, a domain only, an IP address, or a subnet.

To block a particular e-mail address or host from mailbombing you, log in to your system as root, edit the /etc/mail/access file, and add a line to DISCARD mail from the offending sender. After saving the file and exiting the editor, you must convert the access text file to the database format used by the sendmail daemon by using the makemap command. To convert the deny file into a hash indexed database called access.db, type the following:
