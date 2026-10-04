
## 646 Trying Anonymous FTP

The output is something like this:
```
x:14:50:FTP User:/var/ftp/sbin/nologin
```

The x in the second field means that no one can log in with the user name ftp.

- Here is the full permission setting and owner information for the /var/ftp directory:
drwxr-xr-x 3 root root 4096 Jun 22 12:10 ftp

As this line shows, the /var/ftp directory is owned by root, and the permission is set to 755 (only root can read, write and execute; everyone can only read and execute).

- You can view the contents of the /var/ftp directory with the ls -la command. The result is as follows:
total 12
drwxr-xr-x 3 root root 4096 Jun 22 12:10 .
drwxr-xr-x 21 root root 4096 Jun 22 12:10 .
drwxr-xr-x 2 root root 4096 Jun 6 00:36 pub

- The pub directory is where you place any files you want to enable others to download from your system through anonymous FTP.

## Chapter 4: Serving Up Mail and News

### In This Chapter

- Installing and using sendmail
- Testing mail delivery manually
- Configuring sendmail
- Installing the InterNetNews (INN) server
- Configuring INN
- Setting up local newsgroups

Electronic mail (e-mail) is one of the popular services available on Internet hosts. E-mail software comes in two parts: a mail-transport agent (MTA), which physically sends and receives mail messages; and a mail-user agent (MUA), which reads messages and prepares new messages. In this chapter, I describe the e-mail service and show you how to configure the sendmail server on a Fedora Core PC.

Internet newsgroups provide another convenient way, besides e-mail, to discuss topics and to share your knowledge with others. Fedora Core comes with the software you need to read newsgroups and set up your system as a news server. In this chapter, I describe how to configure and run the InterNetNews server. I also show you how to set up local newsgroups for your corporate intranet (or even your home network).

## Installing the Mail Server

If you install the mail server software during Fedora Core installation, you don't have to do much more to begin the mail service. To see whether the mail server is already installed, type the following command:

```
rpm - q sendmail
```

You're all set if the response looks like this:

```
sendmail-8.12.11-3.2.1
```

This output says that sendmail version 8.12.11 is installed on the system.

If the output message tells you that sendmail isn't installed, you can use the Red Hat Package Manager (RPM) to install the individual packages needed for running and configuring sendmail. To install the RPM files, insert the DVD-ROM in the DVD-ROM drive. If you're using GNOME or KDE, the DVD-ROM automatically mounts. Otherwise, type the following command to mount the DVD-ROM:

```
mount /mnt/cdrom
```

Then type the commands to install the sendmail files:

```
cd /mnt/cdrom/Fedora/RPMS
rm -ivh sendmail*
```

This command installs two packages:

- sendmail: A complex mail transport agent (MTA)
- sendmail -cf: Configuration files for sendmail

## Using sendmail

To set up your system as a mail server, you must configure the sendmail-transport agent properly. sendmail has the reputation of being a complex but mail-delivery system. Just one look at /etc/sendmail.cf can convince you that sendmail is indeed complex. Luckily, you don't need to be an expert on the sendmail configuration file. All you need is one of the predefined configuration files — the one that is installed on your system — to use sendmail.

Your system already has a working sendmail configuration file — /etc/sendmail.cf. The default file assumes you have an Internet connection and your system has an official domain name; you can send and receive e-mail from your Fedora Core PC.

To ensure that mail delivery works correctly, your system name must match the name your ISP has assigned to you. Although you can give your system any host name you want, other systems can successfully deliver mail to your system only if your system's name is in the ISP's name server.

![](img/d9230b719dc0efd80851f363d8c6f571_674_0.png)

### A mail-delivery test

To try out the sendmail mail-transfer agent, you can use the mail command to compose and send a mail message to any user account on Fedora Core system. For example, here's how I send myself using the mail command:

```
mail naba
Subject: Testing e-mail
This is from my Fedora Core system.
Cc: Ctrl+D
```

The mail command is a simple mail-user agent. In the command line, specify the address — naba@comcast.net — the program prompts for a subject line. Following the subject, I enter my message and end it with a line that contains only a period. When prompted for a Cc, press Ctrl+D. The mail command is a simple mail-user agent. In the command line, specify the address — naba@comcast.net — the program prompts for a subject line. Following the subject, I enter my message and end it with a line that contains only only period. When prompted for a Cc, press Ctrl+D.

To ensure that mail delivery works correctly, your system name must match the name your ISP has assigned to you. Although you can give your system any host name you want, other systems can successfully deliver mail to your system only if your system's name is in the ISP's name server.

![](img/d9230b719dc0efd80851f363d8c6f571_675_0.png)

### The mail-delivery mechanism

To try out the sendmail mail-transfer agent, you can use the mail command to compose and send a mail message to any user account on Fedora Core system. For example, here's how I send myself using the mail command:

```
mail naba
Subject: Testing e-mail
This is from my Fedora Core system.
Cc: Ctrl+D
```

The mail command is a simple mail-user agent. In the command line, specify the address — naba@comcast.net — the program prompts for a subject line. Following the subject, I enter my message and end it with a line that contains only a period. When prompted for a Cc, press Ctrl+D.

To ensure that mail delivery works correctly, your system name must match the name your ISP has assigned to you. Although you can give your system any host name you want, other systems can successfully deliver mail to your system only if your system's name is in the ISP's name server.

To try out the sendmail mail-transfer agent, you can use the mail command to compose and send a mail message to any user account on Fedora Core system. For example, here's how I send myself using the mail command:

```
mail naba
Subject: Testing e-mail
This is from my Fedora Core system.
Cc: Ctrl+D
```

The mail command is a simple mail-user agent. In the command line, specify the address — naba@comcast.net — the program prompts for a subject line. Following the subject, I enter my message and end it with a line that contains only a period. When prompted for a Cc, press Ctrl+D.

The **telnet** command opens a TELNET session to port 25 — the port on which sendmail expects SMTP commands.

```
telnet localhost
```
```

| Book | Chapter |
| :--- | :--- |
| 4 | Serving Up Mail and News |
| 646 | Trying Anonymous FTP |

The **telnet** command opens a TELNET session to port 25 — the port on which sendmail expects SMTP commands.

```
telnet localhost
```
