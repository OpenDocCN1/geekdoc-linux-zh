
## 7.6 Qmail: Better Than sendmail?

```bash
echo "-config gastro gastro.admin" | mail majordomdo
```

And the lists will have some default configurations put in. If you choose to change the defaults (and you should!) edit the ~majordomo/lists/astro.config file. This has the configuration settings for that particular list.

Now that your mailing list is set up, you should be able to E-mail to the list by just sending mail to "gastro@host" and the E-mail will be sent to all the subscribers of the gastro list. There are a number of extra features that majordomo has, and you should check out the Web site for more information and to get the latest updates.

One of the better known replacements for sendmail is called qmail. There are two reasons for its popularity: ease of use and security. This doesn't mean that qmail is best for everyone, since there are a number of changes in thought that your system has to go through to use qmail. It's also not perfect in a large installation (yet) also because of the ways that sendmail and qmail differ. The configuration for qmail is much simpler than sendmail, but it doesn't offer the "Swiss army knife" of Mail Transport Agents (MTAs) that many experts expect to see.

## 7.6 Qmail: Better Than sendmail?

Here are a few of the ways in which qmail and sendmail differ in methodology.

- **mail file location**: Sendmail prefers to use /usr/spool/mail/user as a location for incoming mail. Qmail prefers to use ~user/Mailbox as a location for storing mail files. This is for two reasons. First, putting the mail in the user's home directory provides for better quota checking and prevents overfilling a central location. Second, there are fewer security problems since there isn't a central location to store files.

- **Permissions**: Sendmail runs almost always as root or with root privileges in order to write files, and so forth. Qmail runs as root only when necessary and otherwise runs as a qmail user who has no special permissions.

- **Mailing list integration**: Sendmail has external programs to create and it administers mailing lists (majordomo and listproc). Qmail supports a method where individual users can have their own mailing lists and administer them themselves with no extra accounts or permissions.

## Installing Qmail

- **Size**: Sendmail is a monolithic MTA, where everything is done in the program itself. Qmail has a number of smaller programs to handle each aspect of mail receipt, delivery, sending, and forth.

After you get the qmail-1.01.tar.gz file from http://www.qmail.org/ (or newer version if it's available), untar and uncompress the file. This will create a qmail-1.01 directory with the source code in it. Review the INSTALL file so you know what the full install procedure is. This procedure allows you to build and install qmail without affecting the sendmail you already have installed until you are satisfied that qmail is working correctly. Qmail resides in the /var/qmail directory, so you'll need to create that directory and remember that so you can monitor that directory. Next you'll need to create users for qmail to use. Since security is a big component of qmail, these new users will need to be separate qmail from the root user and regular users.

Now for the simple part. Enter make to build qmail. The compile should take a few minutes to complete, and you'll be ready for the installation and testing. The biggest problem you may run across is the fact that your home directory and .qmail files cannot be group or world writable. This will show up in the logs as something like

```
Feb 16:50:00 wayga qmail: 886974600.032889 delivery 10: deferral:
Uh-oh:._qmail_file_is_writable._(#4.7/0)/
```

In this event, find the .qmail file it's referring to and change the permissions. You'll also want to check for other copies of the sendmail program floating around the filesystem (like /usr/bin/, for example) and change those to the qmail version. While testing, remember that mail is no longer being delivered to /usr/spool/mail/user, but ~user/Mailbox.

Once the testing and configuration are done (the INSTALL file is pretty thorough on this), you can tell your users about the changes and start using qmail.

A few notes you should know of if you're considering changing MTAs.

- Don't put this on your main server! If you're upgrading or changing software to something you're not used to, always use a staging machine. There are instructions in the FAQ file on how to upgrade slowly from sendmail to qmail with a minimum of fuss and trouble. This upgrade path allows you to use both qmail and sendmail until you get the bugs worked out before you move to qmail.

- You may not want to put this on a connection that goes down frequently. One of the features of qmail is that it continually tries to deliver mail. If the Internet link goes down often, you could be in a situation where qmail is trying to deliver lots of mail at the same time. If it's enough, it could potentially chew up all your CPU resources.

- In addition to the /usr/spool/mail directory changing, the .forward file is ignored in favor of the .qmail file. The .qmail file has a number of features that can't be put in .forward, but programs that operate on .forward won't work anymore.

Once qmail is configured and working properly, you'll need to make sure that you can deliver mail to each user (check their mail file and the syslog output in /var/log to make sure mail is delivered properly).

There are a few things that you will notice once qmail is installed. For the benefit of your users, you should warn ahead of them.

- As previously mentioned, mail now gets stored in ~user/Mailbox instead of /usr/spool/mail/user. You'll need to make sure that the MAIL environment variable is changed (/etc/profile). There are two problems with the /usr/spool/mail approach to delivering mail. First, a security risk. Second, the sendmail does local mail delivery is prone to losing mail if the mail directory is mounted on NFS or if the server goes down while writing E-mail. The "Mailbox" format is written to the disk before it reports back to the mail program. If there is a locking problem or the machine goes down while a message is being delivered, it will get delivered when the machine restarts or the lock goes away.

- Qmail does not look in the .forward file for forwarding E-mail to other users. The replacement file, .qmail, handles this. The nice thing about this is that it allows you as a user to create your own mailing lists. For example, if I wanted to create a simple mailing list related to this book, I could create a .qmail-linux file in my home directory. That file then gets a list of the people I want to be on. This is done, any E-mail sent to every-linux.wayga.net gets sent to the entire list. You can also have a .qmail-default to catch all E-mail that comes in. Note that this isn't a fully-featured mailing list system that doesn't handle automatic subscribe or unsubscribes. This is where ezml comes in (see next section).

- Qmail also does not use /etc/aliases at all. There is a global way of setting up E-mail aliases, which is a bit easier to use. The alias user is used by q-mail to handle addresses that don't exist. For example, you could have ~alias/.qmail-markk contain the line

```
enry@wayage.net
```

to forward E-mail that comes in markk@wayage.net to enry@wayage.net. A common use of this is setting up postmaster, abuse, or aliases.

- The root user does not receive E-mail. Due to the number of security problems this could cause, it was determined that root should be aliased to someone else (like the actual administrators of the machine). It makes cracking a root account much harder.

## Ezlm

The ezlm package allows for easy mailing list setups. It has all the functionality commonly needed in mailing list applications: automatic subscribe/unsubscribe, moderated lists, and digest creation (handled by ezlm-idx). Unlike many other mailing list applications, ezlm is command based—there should be no need for the mailing list administrator to edit files. Another feature of ezlm (and qmail) is that mailing list creation and administration do not require the root account.

By default, many of the ezlm programs get installed in /usr/local/bin/ezlm. The install instructions are in the INSTALL file (located in the ezlm-0.53 directory) and are also straightforward. Once installed and tested, users can create their own mailing lists with the following commands:

```
ezlm-make ~/list ~/.qmail-list user-list host
```

This creates the mailing list. The mailing list itself is contained in ~list. This mailing list is not moderated in that anyone can subscribe and unsubscribe. If you want a private mailing list where only the moderator can add or remove members, you can add the -P option. Once the mailing list is created, you can just remove ~list/public to create a moderated list or just create the file to create a public list:

```
ezlm-sub ~/list e-mail
```

This subscribes the E-mail to list. The new member is subscribed to the list.
