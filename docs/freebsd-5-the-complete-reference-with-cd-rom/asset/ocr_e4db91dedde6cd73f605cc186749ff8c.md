# **Note**

It’s possible to configure a domain so that a mail server in another domain handles the mail. This configuration is convenient if you use an ISP to host your mail, even as a backup for your main mail server.

# ### Sendmail Configuration Files

Sendmail uses `/etc/mail/sendmail.cf` as its configuration file. Unfortunately, the format of this file reminds most new administrators of gobbledygook. Indeed, even many experienced administrators are well advised not to touch the file; it’s too easy to make a single-character typo that ruins the file and is very difficult to track down. Instead, you should edit the `/etc/mail/FreeBSD.mc` file. The `FreeBSD.mc` file uses a format that’s substantially more intelligible than the `sendmail.cf` file format. When you’re done editing the `FreeBSD.mc` file, you can convert it into an equivalent `sendmail.cf` file by typing these commands:

```
`# cd /usr/share/sendmail/cf/m4` 
`# m4 cf.m4 /etc/mail/FreeBSD.mc > /etc/mail/sendmail.cf`
```

# **Caution**

You should back up the `FreeBSD.mc` file before changing it, or copy it to another name, edit the copy, and type the copy’s name in the preceding command. Likewise, you should back up the `sendmail.cf` file before typing the preceding commands. Both steps ensure that you can return to a known standard configuration if something goes wrong.

Once you’ve run these commands, you’ll have a new `sendmail.cf` file, and you can tell sendmail to read this file and implement its changes by typing the following command:

```
`# killall -SIGHUP sendmail`
```

# ### Adjusting the Default Configuration

The default sendmail configuration works, at least to a minimal extent. When first installed, sendmail will accept mail addressed to users at the computer’s hostname, but not to other hostnames. You may need to alter this configuration, particularly if a computer is to function as a mail server for a domain. In terms of outgoing mail, a default sendmail installation delivers the mail directly. This configuration is probably acceptable for a mail server computer and for some workstations with direct connectivity. In some cases, though, you may want to have sendmail relay its outgoing mail through another server, as `morse.pangaea.edu` does in Figure 19-1. Such a configuration is desirable, or sometimes even necessary, for computers with dial-up or broadband Internet links. The basic configuration steps described here are the simplest changes that are commonly necessary. Sendmail supports many far more advanced options. A few of these, including some important security features, are described in the upcoming section, “Blocking Spam.”