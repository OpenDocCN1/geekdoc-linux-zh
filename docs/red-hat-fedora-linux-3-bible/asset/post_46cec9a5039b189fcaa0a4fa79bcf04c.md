
# Chapter 9: Tools for Using the Internet and the Web

### Subscribing to newsgroups

The following procedure describes how to subscribe to a newsgroup in Mozilla.

- Open Mozilla Mail & Newsgroups (Window → Mail & Newsgroups from Mozilla).
- Right-click the news server name in the left column; then click Subscribe. A Subscribe window appears.
- What appears (after a few minutes) are top-level newsgroup names. Newsgroups are organized in a hierarchy, similar to Internet domain names -- levels are separated by dots (although newsgroup names start at the left and go down to the right).
- Click the arrow sign next to a category to see which groups in that category interest you.
- When you see a newsgroup that interests you, click it and select Subscribe.
- Click OK. The subscribed newsgroup appears in your Mail & Newsgroups window under the name of the news server.
- Click the newsgroup in the Mail & Newsgroups window. Recent messages from that newsgroup are downloaded to your Messenger window.

### Reading newsgroup messages

Reading newsgroup messages is similar to reading mail messages. You simply select a message that interests you or move to it using the up and down arrow keys. The message will appear in the message pane in the lower-right corner of the Mail & Newsgroups window.

The concept of threads should be mentioned here: When someone posts a message to a newsgroup, usually one or more people respond to it. Because it is useful to read messages and responses together, these messages are grouped together in threads. A plus (+) next to a message indicates there are responses to that message. Click the plus to see available threads. Threads make it easy to see messages on a topic that interests you or skip a topic that doesn’t.

### The Pan newssreader

> **NOTE:** To use pan, you need to install the pan RPM package from the DVD that comes with this book. For further information about pan, refer to http://pan.rebelbase.com.

The Pan newssreader is a graphical application for reading, managing, and interacting with newsgroups. It is particularly adept at displaying attached pictures and downloading binaries. The interface is very intuitive and easy to use.

Although Pan was originally designed for the GNOME desktop, GNOME libraries are no longer required to run Pan. For that reason, Pan will now work on KDE, Window Maker, or other desktop environments without any special software.

To open the Pan newssreader from the main red hat menu, choose Internet → Pan Newssreader. The first time you start Pan, the Pan wizard runs to let you set up the newssreader. Have your e-mail address and your news server’s name ready. When the wizard is done, you can download the list of newsgroups available from your news server.

### Instant Messaging with Gaim

Gaim is an Instant Messaging client program that runs in Linux. Because it is based on the America Online (AOL) Open IM architecture (www.aol.com), it has the same messaging features you get from AOL’s own messaging application.

To start Gaim from a red hat desktop menu, choose Internet → Messaging Client. Figure 9-9 contains an example of the Gaim window.

![](img/b22364e57409c2481ba806e4e6b9309c_367_0.png)

From the main Gaim window, you have the following options:

- **Accounts** — Add screen names, passwords, and options associated with your AOL Instant Messaging accounts.
- **Signon** — Sign on to AOL Instant Messaging by using your selected screen name.
- **Preferences** — Set preferences associated with AOL Instant Messaging and Chat windows. You can also load plug-ins that can perform special functions, such as spell checking and auto-reconnection.

Besides AOL IM protocols, Gaim supports other messaging protocols, including instant messaging protocols from Yahoo!, MSN, ICQ, Jabber, and IRC.

### Using Remote Login, Copy, and Execution

This section describes some features for allowing users to use resources across a network. They are the `telnet`, `ssh`, `ftp`, `wget`, `rsync`, `rlogin`, `rcp`, and `rsh` commands.

> **CROSS-REFERENCE:** Only the ssh service is turned on by default in Fedora Core. That is because the other remote login, execution, and copy commands described here do not provide encrypted communications by default, and so they can represent significant security risks. For information on how to turn on the services described in this chapter on a Fedora Core server, refer to Chapter 14 and Appendix C.

Two of the commands described in this section are generally available are remote login and file transfer programs: *telnet* and *ftp*, respectively. Other commands for accessing FTP servers are *ncftp* and *gFTP*.

Two newer commands for copying files over the network are *wget* and *rsync*. Both of these tools can be used for efficiently downloading files that you can identify on the network.

Other commands described in this section are more specific to Fedora Core and other UNIX systems, but they provide simplified ways of copying files, logging in, and executing commands among trusted systems: *rcp*, *rlogin*, and *rsh*, respectively. Also, a more secure tool for remote login, called *ssh*, is included with Fedora Core. The *ssh* command can be used for remote execution as well.

### Using telnet for remote login

Telnet is a service provided by many different types of computer systems to enable remote users to log in to their machines over TCP/IP networks. The *telnet* command is the client program that you use to do the remote login. The most common way to use telnet is with a host name. The following is a typical telnet session:

```text
$ telnet maple
Trying 10.0.0.11 ...
Connected to maple.linuxtux.net (10.0.0.11).
Escape character is '^l'.
Fedora Core release 3
Kernel 2.6.8-1 on an i686
login: mike
Password: *******
Last login: Mon Nov 28 13:15:57 from pine
[mike@maple mike]$
```

This example shows what happens when the *telnet* command is used to log in from a computer named *pine* to a computer named *maple* by typing *telnet maple*. My computer tries to connect to the telnet port on *maple* (IP address `10.0.0.11`). Because *maple* is also a Fedora system, once the connection is established, I see the standard *login:* prompt. I type the user name (*mike*) and the password when prompted. When the login and password are accepted, I see the shell prompt for the user *mike*.

The telnet service is disabled by default on Fedora Core systems (as are most network services). So, to be able to log in to your computer using telnet, refer to Appendix C for information on how to turn on the telnet service.

Here are a few useful options you can use with `telnet`:

- `-a` — Automatic login. With this option, your computer attempts to log in to the remote computer using your local user name. So, if you are logged in to your computer as `mike`, when you use `telnet` to log in to a remote computer, the remote computer assumes that you want to log in as `mike`. It simply prompts you for `mike`’s password.
- `-l user` — User name. This option is similar to the -a option, except that instead of using your current user name, you can ask to log in using any user name you choose.
- `-r` — Rlogin-style interface. This option lets you use `tilde ( ˜ )` options. For example, to disconnect while in rlogin mode, type `~.` (`tilde + dot`), or to suspend the telnet session, type `~^z` (`tilde + Ctrl + z`). Only use `~.` if your remote shell is hung (`exit` is a better way to quit normally). If you use `~^z` to suspend your telnet session temporarily, you are returned to your local system shell. To get back to the suspended session, type `fg` to put telnet back in the foreground. See the description of `rlogin` later in this chapter for more features you can use in rlogin mode.

Another way to use `telnet` is in command mode. Instead of using a host name, simply type the word `telnet`. You will see a `telnet` prompt as follows:

```text
$ telnet
telnet>
```

At this point, there are several commands available to you. You are not yet connected to a remote host. To open a login session to a remote computer from the telnet prompt (for example, to a computer named `maple`), type:

```text
telnet> open maple
```

After you do connect to a remote computer, you can return to the telnet session at any time by typing `Ctrl + l`. Here are other options you can use during your telnet session:

- `?` — Print help information.
- `!` — Escape to the shell. (Type `exit` to leave the subshell and return to telnet.)
- `close` — If you have an open connection, type `close` to close it.
- `display` — Shows the operating parameters that are in effect.
- `logout` — Logs you off any remote connection in this session and closes it.
- `mode` — Tries to enter line mode or character mode. (Type `mode ?` to see other options that go with the mode option.)
- `quit` — Close telnet and exit.
- `z` — Suspend the current telnet session. (Type `fg` to return to the suspended telnet session.)

If you suspend a telnet session or escape to the shell, return to telnet by typing `fg`.
