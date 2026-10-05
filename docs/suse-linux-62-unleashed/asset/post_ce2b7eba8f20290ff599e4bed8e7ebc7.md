
# SMTP and Protocols CHAPTER 9 279

alphonse
joe
betty
george

the effect is the same as the alias
homeboys: alphonse, joe, betty, george

This directive is for mailing lists that are automatically generated

## Mail to Programs

The aliases can also be used to send the contents of email to a program. For example, many mailing lists are set up so you can get information about the list or subscribe to it by sending a letter to a special address, list-request. The letter usually contains a single word in its body, as help or subscribe, which causes a program to mail an information to the sender. Suppose the gonzo mailing list has such an address, called gonzo-request:

```
gonzo-request: :/usr/local/lib/auto-gonzo-reply
```

In this form of alias, the pipe symbol (!) tells sendmail to use the program mailer, which is usually defined as /bin/sh (see "The M Operator: Mailer Definitions" later in this chapter). sendmail feeds the message to the standard input of /usr/local/lib/auto-gonzo-reply, and if it exits normally, sendmail considers the letter to be delivered.

## Mail to Files

You can also create an alias that causes sendmail to send mail to files. This sort of alias begins with a forward slash (/) which will be a full pathname to the file you want to append. An example is the alias nobody, which is common on systems running the Network File System (NFS):

```
nobody: /dev/null
```

## Networking and Internet Services
PART II

Aliases that specify files cause sendmail to append its message to the named file. Because the special file `/dev/null` is the UNIX bit-bucket, this alias simply throws mail away.

## Setting Up sendmail

The easiest way to show you how to set up sendmail is to use a concrete example.

If you do not already have sendmail installed, the first step is to start YaST as root. Insert SuSE CD1 into your CD-ROM drive, start YaST (by typing YaST at the command prompt), select the Choose/Install Packages and then select the Change/Create Configuration option. You will now be able to browse to the “n” series and select the package “sendmail” for installation by highlighting it and pressing the space bar. After committing your changes by pressing F10 twice, you will be back at the installation screen. Choose Start Installation option and sendmail will be installed.

After sendmail is installed, the SuSE sendmail configuration program will begin. On the author’s SuSE 6.2 system, this program crashed with a segmentation fault. If it does, simply restart YaST, select System Administration, then Network Configuration, then Configure sendmail. You will be back in the sendmail configuration program, and it should not crash at this point.

The sendmail configuration program provides you with a simple way to configure sendmail for your site, with options for disconnected machines (where sendmail will only deliver mail locally) to machines that have a dedicated connection to the Internet. We will review several configuration possibilities below.

## Dedicated Connection to the Internet

If your machine has a dedicated connection to the Internet, you can simply select the Host with Permanent Network Connection (SMTP) option at the sendmail configuration menu. After committing your changes, type newaliases and sendmail will be properly configured. Simple!

## No Network Connection

If you have to have no network connection at all (not even a temporary network connection, such as a modern line), select the Single User Machine Without Network Connection option at the sendmail configuration menu. After selecting this option and typing newaliases (to update the aliases database), your machine will be properly configured to handle local mail.

## Temporary Dialup Connection

If you have a temporary connection to the Internet, such as a dialup line, sendmail setup is a bit more complicated, but the results are worth it. When we are done, sendmail will be configured so that when you send mail to a remote system, the mail will go into a local queue. Every five minutes, a script will run which will determine if you are connected to the Internet. If you are, it will instruct sendmail to deliver the queued messages immediately. The script can also be extended to retrieve remote messages and deliver them using fetchmail (we explore fetchmail later in this chapter). You will love this arrangement because it provides the benefits of a direct Internet connection using a standard phone line.

The first step is to select the Host with Temporarily (sp) Network Connection (Modem or ISDN) option from the YaST configuration screen. After your changes are committed, we need to change a few things in YaST to get things just right.

Under the YaST System Administration menu, you will notice an option called Change Configuration File. Select this option. You will then be presented with a screen that provides a simple interactive interface to the /etc/rc.config file. If you prefer, you modify the /etc/rc.config file directly using your favorite text editor. If you modify this file, remember to run SuUseconf afterwards. Table 9.1 displays the values you want to change:

Table 9.1 sendmail.cf Command Characters
| Variable | Value |
|---|---|
| SENDMAIL_ARGS | -bd -om |
| SENDMAIL_EXPENSIVE | yes |
| SENDMAIL_NOCANONIFY | yes |
| SENDMAIL_SMARTHOST | mail.<yourisp>.com |

After you have made these changes, type newaliases (to rebuild the /etc/rc.d/init.d/sendmail database), and then /etc/rc.d/init.d/sendmail start. sendmail will now be up and running on your system. We now need to configure the system to deliver remote mail properly.

We are going to create a script that, when executed, will instruct sendmail to send to your queued mail. I think you will find this script rather interesting. It reads as follows:

```
#!/bin/sh
IFACE=ppp0
val=`netstat -i | grep $IFACE`
if [ $val ]
then
```

```
date >> /tmp/.deliver
touch /tmp/.sendingmail
/usr/bin/sendmail q
rm -rf /tmp/.sendingmail
```

Before you save the file, there are a few things we need to review in the script itself. First, IFACE be set to your temporary network interface. Second, the quotes that surround the netstat command are not regular single quotes—they are back-quotes. You will find this key above the Tab key on most U.S. keyboards. If you use a singlequote instead, the script will not work!

After you're typing in the script, save it as /usr/local/bin/sendow. Then, type chmod +x /usr/local/bin/sendow. This script, when executed, will detect whether your temporary interface is active. The date of delivery will be appended to /tmp/.deliver. We now have a /tmp/.sendingmail. To make sure cron is running, type /etc/rc.d/init.d/start. This script, when executed, will instruct sendmail to send to your queued mail. The script can also be extended to retrieve remote messages and deliver them using fetchmail (we explore fetchmail later in this chapter). You will love this arrangement because it provides the benefits of a direct Internet connection using a standard phone line. We now have a crontab. Now, as root, type crontab -e, and add the following line:

```
*/ * * * /usr/local/bin/sendow
```

# SMTP and Protocols
CHAPTER 9 283

setenv VISUAL <your-favorite-editor>

Since my favorite editor is pico, I export VISUAL=pico. Now, as root, type crontab -e, and your favorite editor will start:

```
*/ * * * /usr/local/bin/sendow
```

After saving this file, cron will be configured to run sendnow every five minutes. The final step is to make sure cron daemon is running by typing /etc/rc.d/init.d/start. Your mail system is now properly configured!

## Obtaining the Source

SuSE Linux ships with sendmail 8.9.3. Frankly, this is the latest version at the time of this writing. If you are concerned with security (and you should), you will want to keep track of any new versions by checking the comp.security.announce newsgroup regularly. The latest version of sendmail is always found at http://www.sendmail.org. New versions or patches are quickly brought out when a security flaw is found, and you should upgrade your system as soon as possible release. It would be wise to wait for a SuSE RPM to be released with the new patches applied; otherwise you need to get the patches and apply them to the source as well as the other SuSE configuration changes.

## Unpacking the Source and Compiling sendmail

You only need to read this section if there is a new version of sendmail that hasn't been released as an RPM yet. assume you have downloaded the source from ftp://ftp.sendmail.org.

Now that you have the source, you need to unpack it. Because it's a compressed tar image, you must first decompress it and then extract the individual files from the tar archive. An example to do this

```
[root@onzo]# tar zxf sendmail-8.9.3.tar.gz
```

Now you' almost ready to compile sendmail. But first read the following files, which contain the latest news about the specific release of sendmail you've downloaded:

- RELEASE_NOTES
- KNOWNBUGS
- READ_ME
