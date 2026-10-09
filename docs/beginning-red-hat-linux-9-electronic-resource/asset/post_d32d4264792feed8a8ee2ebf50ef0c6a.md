
## The `smbmount` Utility (Mounting an SMB Share Locally)

The `smbmount` utility allows you to mount a (possibly) remote smb share on a client Linux computer. You can try this out if you have two Linux machines networked together – use the one with the Samba share as the server and the other one as the client. Alternatively, you can also try this out if you've only got a single Linux machine – in this case the machine acts as both file server and as client of its own service.

To get a list of all the commands you can use through the smbclient session, type `help` at the prompt:

```
smb: \>help
?      a      b      c      d
e      f      g
cancel cd     chmod  chown  del    dir
exit   du     get    help   directory
...
```

For more on using Samba shares via an smbclient session, see the documentation at [http://us3.samba.org/samba/ftp/docs/htmldocs/smbclient.1.html](http://us3.samba.org/samba/ftp/docs/htmldocs/smbclient.1.html). To exit the smbclient session, type `exit` at the `smb: \>` prompt.

The `smbmount` application uses a helper application called `smbmnt`, and the first thing to do is change the permissions on `smbmnt` so that your `smbmount` command can use it. By default, `smbmnt`'s permissions allow it to be used only by the root user of the machine on which it is running. Assuming you're using the client machine as a normal user, you'll need to use the root account to adjust these permissions, like this:

```
$ su -
Password:
# chmod s+u /usr/bin/smbmnt
```

You can check the new permissions, like this:

```
# ls -l /usr/bin/smbmnt
-rwsr-xr-x 1 root root 491096 Jan 10 00:05 /usr/bin/smbmnt
```

Now you're ready to test `smbmount`. Change back to your normal user account, and create the directory onto which you want to mount the Samba share:

```
# exit
$ mkdir /home/kapils/mnt
$ mkdir /home/kapils/mnt/remote
```

Here, we're using the local kapils account on the client machine, and we've created a directory called mnt/remote underneath this user's home directory /home/kapils.

Now, run the smbmount command to mount the remote Samba share on the local directory:

```
$ smbmount //linuxserver/linuxbox-share /home/kapils/mnt/remote -o username=kapils
Password:
```

Here, `linuxserver` is the name of the Linux server that is hosting the Samba share, and `linuxbox-share` is the name of the share; `/home/kapils/mnt/remote` is the mount point we've chosen; and `kapils` is the name of the Samba user on the Linux server. You're prompted for the password of the Samba user.

When you've done this, and assuming the connection is good, you can navigate the contents of the Samba share as if they were contents of the mount point. For example:

```
$ ls /home/kapils/mnt/remote
temp1.txt temp2.txt temp3.txt
```

To unmount, you can use the smbmount command. However, like `smbmnt`, you may first need to use the client machine's root account to change the permissions on `smbmount`:

```
# chmod s+u /usr/bin/smbmount
```

Now you can safely unmount the share from your mount point, using your normal user account:

```
$ smbmount /home/kapils/mnt/remote
```

### Accessing NT Shares from a Linux Machine

We've talked about how to set up and access a Linux-hosted Samba share, but what about if we want to use a Linux client machine to access a file system hosted by a Windows server? In fact, we can access Windows NT shares in the same way that we access Linux shares.

For example, suppose we have a Windows NT machine called `winserver`, which acts as a file server by hosting a share called `salesarchive`. We can treat the contents of this share as if it were part of the client machine's file system, by mounting it just as we've done before.

First, we'll need a directory that will act as our mount point. For example, let's create a local directory called `sales`, under our user's home directory:

```
$ mkdir /home/kapils/mnt/sales
```

Next, we use `smbmount` to mount the file system onto the mount point:

```
$ su -
Password:
# smbmount //winserserver/salesarchive /home/kapils/mnt/sales -o username=kapils
Password:
```

There are two points to note here. First, the normal user does not have permission to mount a filesystem, so we must change to root user before using `smbmount`. Second, the `smbmount` command itself requires that you specify a username and password. This username corresponds not necessarily to a user on the Linux machine, but to a network user that has permission to access the share.

Having achieved a connection, you can work with the files on the remote file server as if they were part of the local directory:

```
$ cd /home/kapils/mnt/sales
$ ls
sales2002Q2 sales2002Q3 sales2002Q4
sales2003Q1 salesnotes.txt
```

Your permissions on the contents of this folder will depend on the permissions assigned to the network user whose account you specified in the `smbmount` command. To unmount the share, use `smbumount` again:

```
# smbumount /home/kapils/mnt/sales
```

### Accessing SMB/CIFS Shares Using Nautilus

We can even use Nautilus file manager to access SMB/CIFS resources such as Windows and Linux Samba shares. To access Samba shares using Nautilus, first launch a Nautilus window (for example, by selecting **Main Menu | Run Program** and typing `nautilus`).

Then type `smb:` in the **Location** bar. This will cause Nautilus to show you a list of all local domains and workgroups. From here, double-click on the workgroup of your Windows machine, and then on the name of the Windows machine itself, to view all directory shares on that machine.

If you are connecting to `smb` shares that require a username and password, you can specify the username and password within Nautilus's **Location** bar. In this example, the **Location** bar with username and password should look like this:

```
smb://kapil:password@winserserver/salesarchive/
```

After successful authentication, Nautilus will show you all the files under that share:

![](img/b852150740856958b10aff9e8c9d2adc_390_0.png)

There's a lot to Samba, and we've covered only a little of the detail here. For more depth, take a look at Samba's software suite manual pages (using the `man` command), the SWAT documentation (on the HOME page of your SWAT tool), and the Samba official web site (http://www.samba.org). You must always check your firewall settings for SWAT port. Firewall must be configured to open port 901 for SWAT.

## Setting up a Mail Server

For many of us, e-mail has become an essential part of life. When you send an e-mail, it is a mail server that is responsible for dispatching that mail to its intended destination; and at the other end, another mail server receives that message and passes it on to the appropriate mailbox.

A mail server can be configured to handle small home network e-mails, or large complex networks with hundreds of users. Many home users tend to use the mail server provided by their ISP. Many medium-to-large organizations host their own mail servers.

It's unlikely that you'll need to set up your own mail server, but in some situations there are good reasons for doing so. For example:

- Your mail server will be on the same network as your client machine, and so connection between your client machine and mail server will be much faster.
- If you have a dial-up connection (rather than a dedicated Internet connection), then having your own mail server allows you to work on your e-mail without ever having to connect manually to the Internet. You can configure your email server to send and receive mail in batches, by connecting to Internet at specified times.
- You can customize a mail server’s security and monitoring rules, so that it alerts you if it receives a message that contains certain blocked words or if it detects unusual activity.

Hosting your own mail server comes with its burdens, too. There’s the increased cost of support and maintenance, and the additional chance of being compromised (you’re protected from this if you use an ISP’s mail server). It’s also more important to ensure that you keep your antivirus software up to date, and that it scans each e-mail. And there is a risk that your mail server will become an open relay SMTP server (this is where another user uses your mail server as a gateway for sending mail).

So, there’s much to consider, and debate of these issues is outside the scope of this book. However, if you do decide to host your own mail server, then you won’t be surprised to learn that the Red Hat Linux 9 operating system comes with a default mail server. It’s called Sendmail, and we’ll examine it briefly here.

### What Is a Mail Server?

A mail server is a collection of applications that provide the functionality to manage the tasks of sending and receiving of e-mail, and delivering e-mail to user’s mailboxes. A mail server uses a number of different protocols to transfer e-mail from one system to another. Here’s a brief description of these protocols:

- The Internet Message Access Protocol (IMAP) is a protocol used by an e-mail client application to access the remote e-mail mailbox. The main advantage of IMAP is that users can manage the e-mail messages on remote mailboxes instead of downloading the messages on to local machine. For more information about IMAP, take a look at http://www.imap.org/.
- The Post Office Protocol (POP) is used by e-mail clients to download e-mail messages from a remote server and save it on their local machine. For more information about POP, please refer to RFC 1939 at http://www.rfc-editor.org/in-notes/rfc1939.txt.
- The Simple Mail Transfer Protocol (SMTP) is used to send e-mails (this is in contrast with IMAP and POP, which are used to receive e-mails). Each e-mail message is transferred between remote e-mail servers using SMTP. Red Hat Linux 9 uses sendmail as its default SMTP software.

### E-mail Application Types

E-mail applications fall into the following three classes:

- Mail User Agents (MUAs). An MUA is an e-mail client – a program that is used to retrieve and manage e-mail messages via POP or IMAP protocols. Examples of MUAs
