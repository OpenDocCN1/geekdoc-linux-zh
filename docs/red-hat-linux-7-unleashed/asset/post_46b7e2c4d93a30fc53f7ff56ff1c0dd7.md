
that they reference. If any of these files or parent directories have group or world writable permissions, the files will most likely be ignored, which might cause sendmail to cease working or not even start at all. These sorts of problems are usually logged to your system messages file (/var/log/messages or /var/log/maillog, depending on how your syslog is configured).

## Mail to Programs

The aliases file can also be used to send the contents of email to a program. For example, many mailing lists are set up so you can get information about the list or subscribe to it by sending a letter to a special address, list-request. The letter usually contains a single word in its body, such as help or subscribe, which causes a program to mail an information file to the sender. Suppose the gonzo mailing list has such an address, called gonzo-request:

```
gonzo-request: | /usr/local/lib/auto-gonzo-reply
```

In this form of alias, the pipe symbol (|) tells sendmail to use the program mailer, which is usually defined as /bin/sh (see “The M Operator: Mailer Definitions” later in this chapter). sendmail feeds the message to the standard input of /usr/local/lib/auto-gonzo-reply, and if it exits normally, sendmail considers the letter to be delivered.

## Mail to Files

You can also create an alias that causes sendmail to send mail to files. This sort of alias begins with a forward slash (/), which will be a full pathname to the file you want to append to. An example is the alias nobody, which is common on systems running the Network File System (NFS):

```
nobody: /dev/null
```

Aliases that specify files cause sendmail to append its message to the named file. Because the special file /dev/null is the UNIX bit-bucket, this alias simply throws mail away.

## Setting Up sendmail

The easiest way to show you how to set up sendmail is to use a concrete example.

To summarize, first, you must install the included sendmail RPM package as well as the sendmail-cs package that installs all the files required to build your own configuration file. Next, choose a sendmail.mc file that closely models your site’s requirements and tinker with it as necessary. The .mc files use a series of m4 macros, which will be covered later, to simplify the creation of the rather dense sendmail.cf file. To make the sendmail.cf from the .mc file you’ve modified, use the make utility. Then test sendmail and its configuration file. Finally, install sendmail.cf and other auxiliary files.

The preceding are the basic steps, but you might also have to make sure that **sendmail** is configured to start correctly when your system reboots. The easiest way to do this is to run the **control-panel** program as *root*. Then select the icon that looks like two traffic light symbols. This is the Runlevel editor and is shown in Figure 10.1.

### FIGURE 10.1
The Red Hat control-panel.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_319_0.png)

After you click the Runlevel editor, you will see a number of runlevels as displayed in Figure 10.2. Make sure **sendmail** is located in all runlevels that you require it in. By default it should be in all of those displayed. If it isn't, just put it in Runlevel 3 for now by clicking in the leftmost window, scrolling down to **sendmail**, selecting it, and then clicking **Add** and selecting Runlevel 3.

### FIGURE 10.2
The Runlevel editor.

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_319_1.png)

In addition, you must create an aliases file if your system doesn't already have one. In a Red Hat system it will be `/etc/aliases`, but some systems might locate it in `/usr/lib/aliases` depending on your version of UNIX. The location of the aliases file is given in `sendmail.cf`, so you can put it wherever you want. You might also have to make changes to your system's DNS database, but that information is not covered here (see Chapter 20). Future versions of `sendmail` will place all ancillary `sendmail` files into the `/etc/mail` directory.

## Obtaining the Source

Red Hat Linux ships with `sendmail` 8.10.1. Fortunately, this is the latest version at the time of this writing. If you are concerned with security (and you should be), you will want to keep track of any new versions by checking the `comp.security.announce` newsgroup regularly. The latest version of `sendmail` is always found at `http://www.sendmail.org`. New versions or patches are quickly brought out when a security flaw is found, and you should upgrade your own system as soon as possible after a new version is released. It would be wise to wait for a Red Hat RPM to be released with the new patches already applied; otherwise you need to get the patches and apply them to the source as well as the other Red Hat configuration changes. This process is not trivial. Check `ftp://updates.redhat.com/7.0/i386` or the various Red Hat mirror sites around the world for any Red Hat RPM updates.

Note that the exact names of the files to download differ depending on the most current version of `sendmail`. In the case of the `sendmail` included in Red Hat 7 the `sendmail` RPM is called `sendmail-8.11.0-8.i386.rpm`. Also, because the files are compressed, you must give FTP the `binary` command before transferring them. Note too that you should include your complete email address as the `FTP` password—for example, `mylogin@gonzo.gov`.

## Unpacking the Source and Compiling `sendmail`

You need to read this section only if there is a new version of `sendmail` that hasn't been released as an RPM yet and you need new features or bug fixes in place immediately. I assume you have downloaded the source from `ftp://ftp.sendmail.org`.

Now that you have the source, you need to unpack it. Because it's a compressed tar image, you must first decompress it and then extract the individual files from the tar archive. An example command to do this is

```
[root@gonzo src]# tar zxvf sendmail-8.10.1.tar.gz
```

Now you're almost ready to compile `sendmail`. But first read the following files, which contain the latest news about the specific release of `sendmail` you've downloaded:

- RELEASE_NOTES
- KNOWNBUGS
- README

You might also want to check the *Sendmail Frequently Asked Questions* (FAQ) located at `http://www.sendmail.org/faq`. This is a useful source of information on common configuration mistakes or questions on how to set up a particular configuration.

Also take note that the *Sendmail Installation and Operation Guide* (*SI(OG)* is in the `doc/op` subdirectory.

Now run `cd` and `ls` to see what files are in the source directory:

```
[root@gonzo src]# cd sendmail-8.11.0/src
[root@gonzo src]# ls
Makefile collect.c macro.c parseaddr.c srvsmtp.c
Makefiles conf.c mailq.0 pathnames.h stab.c
READ_ME conf.h mailq.1 queue.c stats.c
TRACFLAGS convtime.c mailstatus.h readcf.c syslogits.c
aliases.c daemon.c main.c recipient.c sysexts.h
aliases deliver.c makesendmail safeFile.c trace.c
aliases.0 domain.c map.c savemail.c udb.c
aliases.5 envelope.c mci.c sendmail.0 useful.c
arpadate.c headers.c mime.c sendmail.8 usersmtp.c
cdlock.c ldap_map.h newaliases.0 sendmail.h util.c
clock.c ldap_map.h newaliases.1 sendmail.hf version.c
```

Thankfully, Eric Allman and the `sendmail` crew have done a fantastic job of making the installation process very straightforward. To compile your new version of `sendmail`, simply run the following (from the `sendmail` `src` directory):

```
[root@gonzo src]# ./Build
```

And then watch it build.

This creates a directory `obj.*` that contains the result of the compilation (so you can build `sendmail` for different machines or operating systems in the same sources). Also check the `BuildTools/Site` and `BuildTools/OS` directories for further configuration.

## Caution

Before you install the new `sendmail` configuration, be sure to make a backup of any files you are going to replace, especially the old `sendmail` daemon you have. In the event that the new `sendmail` doesn't work for you, you will need to restore the old versions while you troubleshoot the new version.
