
common to send requests to a "listserv" address, and this occasionally gets confused and translated into "listserve" or "listserver," so those are acceptable as well.

The next block establishes a list related to biochemistry. Similar to the listserv itself, each list has an owner who can control its configuration and is notified of error messages. Each message sent to the address biochem@mail.mybox.com is distributed to the recipients listed in the /var/lib/majordomo/lists/biochem file. The message is also sent to the archive2.pl Perl script. Archived messages are stored in files such as /var/lib/majordomo/archives/biochem/biochem.200205 (the archive for May 2002).

## Running majordomo

Unfortunately, none of these wonderful features works quite yet. First, the alias database needs to be rebuilt, using the newaliases command or sendmail -bi. Next, because all mail delivered directly to a program is handled by the smrsh program, the smrsh program needs to be configured to allow majordomo's wrapper program to receive mail. To accomplish this, just create the appropriate symbolic link using the following command:

```
# ln -s /var/lib/majordomo/wrapper /etc/smrsh/wrapper
```

I also recommend that you add the line T:majordomo to the /etc/sendmail.cf file to avoid any extraneous X-Authentication-Warning header lines.

Now the listserv can be tested. Run the following command:

```
# echo "help" | mail majordomo@mail.mybox.com
```

You should quickly receive majordomo's Help Document in your mailbox.

The programs included with the majordomo distribution are summarized in Table 19-6.

### Table 19-6: Programs Included with Majordomo

| Program | Description |
|---|---|
| Approve | Approves majordomo requests and handles bounce messages. |
| Archive2.pl | Archives messages for later retrieval. |
| Bounce | Automatically removes an address (usually because of repeated delivery failures) from a list and subscribes that address to the "bounce" list (if it exists). |
| Bounce-remind | Sends a notice to subscribers of the "bounce" list, informing them that they have been removed from the list to which they were once subscribed. |
| Config-test | Verifies the majordomo installation and points out current and potential problems. |
| Digest | Packages messages into digests, to be sent when a particular time limit or message size is reached. |
| Majordomo | Performs most of the tasks involved in managing the distribution lists. |
| Medit | Locks a majordomo file for editing and unlocks the file when the editing session is completed. |
| resend | Retransmits outgoing messages to the distribution list. |
| request-answer | Responds to a subscription request and forwards the request to the list owner. |
| wrapper | Allows other programs to always run as the majordomo user, and simplifies running under smrsh (only one link to place in `/etc/smrsh`). |

## Summary

Installing a mail server in Red Hat Linux is the easy part; it’s the configuration that takes patience, resolve, and a fair bit of experimentation. Sendmail can take some patience to configure properly. Even though it may be considerably faster and easier to utilize the m4 macros, eventually you’ll need to edit the `sendmail.cf` file. Just hope that it’s not the rewriting rules that need editing.

With Red Hat Linux 7.3 you can replace Sendmail with Postfix as your mail-transfer agent. To make the transition a bit easier, Red Hat provides the alternatives feature. Alternatives enables you to switch one MTA for another by linking essential files to the package you choose.

Sooner or later, an alias definition in `/etc/aliases` will become unmanageable. At this point, mailing list software, such as Majordomo, can provide the flexibility necessary to manage a large distribution list, with the added benefits of archiving, moderation, digesting, and automated administration.

# Chapter 20: Setting up an FTP Server

### In This Chapter

- Understanding FTP servers
- Using the WU-FTPD FTP server
- Using the vsFTPd FTP server
- Getting more information about FTP servers
- Trying out your FTP server

File Transfer Protocol (FTP) has been the standard method for sharing files over the Internet for many years. Even with the popularity of the Web, which made document database services such as Gopher and WAIS almost obsolete, FTP servers are still the most common way to make directories of documents and software available to the public over the Internet.

File-sharing applications, such as NFS and Samba, are excellent tools for sharing files and directories over a private network. For organizations that need to share large numbers of files over public networks, however, FTP server software provides more robust tools for sharing files and protecting your computer systems. Also, FTP client software (for accessing FTP servers) is available for any type of computer that can access a network.

This chapter describes how to set up and maintain an FTP server, focusing on two different FTP server packages provided with Red Hat Linux: the Washington University FTP Server software (WU-FTPD) and the Very Secure FTP Server software (vsFTPd). While WU-FTPD has been around for a while, vsFTPd is considered to be better for high-volume FTP servers.

> **CAUTION:** If you are using an FTP server only to allow users to download public files, security risks are minimal. However, sharing private files or allowing users to upload files to your server involves additional risks. Risks include attackers intercepting and replacing files that are being uploaded or downloaded, and denial-of-service (DoS) attacks. See the end of this chapter for references to documents from CERT that provide FTP-security tips.

### Understanding FTP Servers

The first implementations of FTP date back to 1971, predating the Web by more than a decade. FTP was created at a time when most computing was done on large mainframe computers and minicomputers. The predominant platforms using FTP were UNIX systems.

FTP set out to solve the need to publish documents and software so that people could get them easily from other computer systems. On the FTP server, files were organized in a directory structure; users could connect to the server over the network (usually the Internet), move up and down the directory structure to find the files that interested them, and download files from (or possibly upload files to) the server.

Originally, a drawback of FTP servers was that people looking for a file or a document on the Internet had to have an idea of which FTP server held the files they were looking for. Tools such as Gopher and WAIS helped in such searches. With the advent of the Web, however, users can now rely on a variety of search engines and Web pages to help point them to the FTP servers that have the files they want. In fact, when you download files by clicking on a link from a Web page, you may not even be aware that the file is being downloaded from an FTP server.

### Attributes of FTP servers

That FTP was implemented on large, multiuser UNIX systems accounts for many of the design decisions that remain a part of FTP today. As the most popular free version of UNIX, Linux in general (and Red Hat Linux in particular) has drawn on FTP features that have resulted from years of testing and experience gained from other UNIX versions of FTP. Some attributes of FTP servers follow:

- Because FTP was originally used on multiuser systems, only restricted parts of the file system in Red Hat Linux are devoted to FTP. Those who access FTP from a public user account (usually the anonymous user name) are automatically given an FTP directory (often /var/ftp) as their root directory. From there, the anonymous user can access only files and directories below that point in the file system.
- Access to the FTP server relies on a login process that uses standard UNIX login names (that is, those user names found in /etc/passwd). Although anonymous was the user name that strangers would use, users with their own accounts on the system could log in with their own user names through FTP and most likely have access to a greater part of the file system (in particular, their own private files and directories).
- The ftp command and other FTP client programs let you log in and then operate from a command interpreter (similar to a very simple shell). Many of the commands that you use from that command interpreter are familiar UNIX commands. You change directories with cd, list files with ls, change permissions with chmod, and check your location with pwd (to name a few). When you find where you want to be, you use the get command to download a file or the put command to upload one.
