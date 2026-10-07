
or you can substitute your site name if you renamed your sendmail.m4 file to reflect your site name (in other words, if you created a file called tcp1.m4, you should specify tcp1.cf in the command).

After the file has been processed, copy it to the /etc directory (which is where the file normally resides) and start up sendmail with the command

```
/usr/lib/sendmail -bd -q1h
```

or reboot your machine (because sendmail usually starts from the rc startup files). The exact paths may be different on your system, so check where these configuration files are stored.

## Using sendmail Version 8

The latest version of sendmail supplied for most Linux systems is version 8. If you didn’t see versions 6 or 7, don’t worry: They never existed. The sendmail system jumped from release 5.X to 8. (One of the important additions to version 8 of sendmail is the anti-spam filters that lets you remove spam email. If you are getting a lot of spam, this feature alone is worth the upgrade trouble!)

For the most part, sendmail version 8 is similar in configuration details to the other releases of sendmail. One change is the inclusion of four different UUCP mail routines. Choose one of the four UUCP versions based on the following features:

- uucp-old (same as “uucp”) Classic UUCP that uses a bang-style address and can send to only one address at a time (duplicate messages are sent when multiple recipients are specified). This version should be used only if you really need compatibility with old-style UUCP systems.
- uucp-new (previously known as “suucp”) The same as UUCP except that it provides the rmail command to allow several recipients. This version is not much of an improvement over uucp-old.
- uucp-dom Allows domain name-style addressing. May not be compatible with some systems you may have to connect to.
- uucp-udom A combination of uucp-new and uucp-dom to provide the best features of both. Allows bang- and DNS-style addresses with proper handling of headers.

Whichever version of UUCP you choose, it should be copied or linked to the normal UUCP binary on your Linux system.

## smail

The smail mail system is similar to the sendmail system in most of its actions, although the configuration process is different. In some ways, smail is easier to work with than sendmail and can be a good choice for smaller systems. If you choose to use smail as your mailer, you will have to make some manual modifications to configuration files because there are few automated or scripted routines available.

The smail system has many options and configuration details, most of which are never used. We'll look at the primary controlling parameters that most Linux users will need, and essentially ignore those that are very seldom (if ever) used in real situations. For more information on the options and configuration controls we skip over in this chapter, see the man pages or smail documentation. We'll focus this chapter on showing you how to get smail up and running quickly and easily to handle the situations most Linux systems will find themselves working with.

### Setting Up smail

The smail system requires several links to exist so smail can execute properly. The two most important links are to the files `/usr/bin/rmail` and `/usr/lib/sendmail` (sometimes located as `/usr/sbin/sendmail`, depending on the version of Linux). These links are necessary because most user mail applications send outgoing mail to either rmail or sendmail (depending on the mail software), and this has to be redirected to smail. Links allow this redirection to occur transparently without altering the user mail applications.

You should verify that the rmail and sendmail files are linked to smail, and if not, establish the links. Usually, the links established are symbolic and will show in a directory listing with an entry like this:

```
lrwxrwxrwx 1 root root 6 Sep 16:35 file1 -> file2
```

The arrow (->) shows that a symbolic link exists. (For more information on links and symbolic links, see Chapter 8, “Using the File System.”) Check both the rmail and sendmail binaries for these symbolic links. If the symbolic links do not exist already, create them with the following commands:

```
ln -s /usr/local/bin/smail /usr/bin/rmail
ln -s /usr/local/bin/smail /usr/lib/sendmail
```

Of course you should substitute whatever directory pathnames are valid on your system for smail, sendmail, and rmail. After you have created the links, verify that they exist by displaying the directories and look for the symbolic link notation shown earlier.

If there is the possibility of mail either entering or leaving your system through an SMTP channel, you should also establish a link between the smail program and the SMTP system. Use the command:

```
ln -s /usr/local/bin/smail /usr/sbin/smtpd
```

to set up the link (substituting proper paths for your system). Next, the SMTP service has to be allowed through the TCP configuration files. This is enabled by setting the /etc/services file to specifically allow SMTP connections. There is a line in the /etc/services file that looks like

```
smtp 25/tcp # Simple Mail Transfer Protocol
```

which you should verify to be not commented out (indicated by a pound sign as the first character). This allows the SMTP link to be established as TCP port number 25 (the default value).

If you are going to leave smail as a daemon (started automatically with the system boot), ensure that the smail daemon is started in the rc files (such as rc.inet2). The usual command line for the smail daemon looks like this:

```
/usr/local/bin/smail -bd -q15m
```

The -bd option turns the daemon operation of smail on, which the -q15m tells smail to process messages every fifteen minutes. If you want more frequent mail delivery, change the value in the rc file. Alternatively, if you want mail processing less often to relieve a heavily loaded system, increase the value.

If you decide not to run smail as a daemon and want it spawned by inetd whenever mail arrives, comment out the daemon lines in the rc files (usually rc.inet2). You can not run smail in both daemon and spawned mode. Next, you should modify the /etc/inetd.conf file to contain an entry like this:

```
smtp stream tcp nowait root /usr/sbin/smtpd smtpd
```

You must have the symbolic link between smtpd and the smail program for this command to function properly.

The configuration file changes necessary for smail depend on which connection system you use for obtaining mail. In other words, the configurations change if you are using UUCP (which is the easiest to set up) or a TCP connection on a network. We can look at each of the configuration processes separately. You can follow both, if you allow mail through both methods.

## Configuring smail for UUCP

Configuring the smail system for use with UUCP incoming and outgoing mail messages is very simple. You need to edit the default smail configuration file, usually stored as /usr/lib/smail/config. Some versions of smail include a sample configuration file such as config.sample in the same directory. You can use either as a template for the UUCP modifications.

Use any ASCII editor to edit /usr/lib/smail/config (the path in your distribution may be different). There are four changes you need to make. The changes are for these variables:

- visible_domain: The domain names your site belongs to
- visible_name: Your site's full domain name
- uucp_name: Your site's UUCP-based name (usually the same as visible_name)
- smart_host: The name of the UUCP host

Each parameter in the /usr/lib/smail/config file uses the same format of variable=value. There should be no spaces on either side of the equals sign on any line. Comments in the file are preceded by a pound sign.

### Setting the Local Domain Names

Begin by setting the domain name of the local machines. Locate the line in the /usr/lib/smail/config file that defines the variable visible_domain, which usually looks similar to this:

```
# Our domain name
visible_domain=tpci
```

The visible_domain variable sets the domain names your site belongs to and will usually be the fully qualified domain name and any aliases that may be in effect. This field is used by smail to find out whether the recipient of a message is local or not. The smail system takes the message and extracts the recipient's address, comparing it against the local machine name (from the hostname command) and all values specified on the visible_domain variable. If there is a match to any of these names, the message is for a local recipient. If no match occurs, the message is routed externally.

If there is more than one valid value for a local domain name, the values are separated by colons, as shown in this example:

```
visible_domain=tpci:tpci.com:tpci.UUCP
```
