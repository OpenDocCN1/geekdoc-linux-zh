
## NOTE

Seeing messages in a mailq listing isn't necessarily a sign of trouble. If your system is processing very many or very large messages, they will appear in the queue for a time. Likewise, a slow network connection will cause messages to hang around for a while. If messages regularly stay in the queue for very long, though, your network connection may be unreliable or overloaded, or something about your mail server software's configuration may be suboptimal. Checking the mail log files (typically /var/log/mail) may provide you with more clues.

If mail has accumulated in the queue and you believe you've corrected the problem, it should eventually clear out on its own. To speed up the process, though, you can type **sendmail -q**. This command causes the mail server to immediately attempt delivery of all queued messages.

## Using Aliases and Forwarding E-mail

E-mail aliases enable one address to stand in for another one. For instance, all e-mail servers are supposed to maintain an account called postmaster. E-mail to this account should be read by somebody who's responsible for maintaining the system. One way to do this is to set up an alias linking the postmaster name to the name of a real account. You can do this by editing the aliases file, which usually resides in /etc or sometimes in /etc/mail.

The aliases file format is fairly straightforward. Comment lines begin with hash marks (#), and other lines take the following form:

```
name: addr1[,addr2[, ...]]
```

The name that leads the line is a local name, such as postmaster. Each address (addr1, addr2, and so on) can be a local account name to which the messages are forwarded, the name of a local file in which messages are stored (denoted by a leading slash), a command through which messages are piped (denoted by a leading vertical bar character), the name of a file whose contents are treated as a series of addresses (denoted by a leading include: string), or a full e-mail address (such as fred@example.com).

A typical default configuration includes a few useful aliases for accounts such as postmaster. Most such configurations map most of these aliases to root. Reading mail as root is inadvisable, though—doing so increases the odds of a security breach or other problem because of a typo or bug in the mail reader. Thus, you may want to set up an alias line like the following:

```
root: yourusername
```

This redirects all of root's mail, including mail directed to root via another alias, to yourusername, which can take any of the forms just described (it's most likely to be a local username or a valid remote e-mail address). Some mail servers, including sendmail and Postfix, require you to compile /etc/aliases into a binary file that can be processed more quickly. To do so, type newaliases as root.

Another approach to redirecting mail is to do so on the user level. In particular, you can edit the `~/.forward` file in a user's home directory to have mail that user sent to another address. Specifically, the `~/.forward` file should contain the new address—either a username on the current computer or an entire e-mail address on another computer. This approach has the advantage that it can be employed by individual users, too, to consolidate e-mail from multiple systems into one account without bothering system administrators. A drawback is that it can't be used to set up aliases for nonexistent accounts or for accounts that lack home directories. The `~/.forward` file can also be changed or deleted by the account owner, which might not be desirable if you want to enforce a forwarding rule that the user shouldn't be able to override.

## Choosing a POP or IMAP Server

POP and IMAP are both tools that are used to deliver e-mail to end users, who typically use mail clients on remote computers. The two protocols differ in that POP is much simpler; it provides users with direct access to their mail queues on the server computer. Users may read and delete messages from that queue, but they may not organize their mail queues. To store messages in multiple folders according to content, correspondent, or other criteria, users are expected to download the mail and store it locally. IMAP, by contrast, supports the use of mail folders on the server computer. This feature enables users to access the same mail structure from several computers (say, a desktop system and a notebook). The drawback is that IMAP, if fully utilized, increases server requirements—mail stored long-term on the server increases disk needs, and users referring repeatedly to the same e-mail message will push up network bandwidth used by the server.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_500_0.png)

Several different versions of POP and IMAP exist. In particular, POP2 and POP3 are distinct protocols, and versions of both POP and IMAP that employ Secure Sockets Layer (SSL) encryption also exist.

Quite a few POP and IMAP servers are available for Linux. (Many programs handle both protocols.) Examples include the following:

- **UW IMAP** Despite its name, the University of Washington IMAP server ([http://www.washington.edu/imap/](http://www.washington.edu/imap/)) supports POP2, POP3, and IMAP. This set of servers is extremely common; it ships with most Linux distributions, usually in a package called `imap` or `uw-imap`. The IMAP server stores user mail folders in users' home directories, which can be awkward if users also log into their accounts and store nonmail files there.

- **Cyrus IMAP** Like UW IMAP, Cyrus IMAP ([http://asg.web.cmu.edu/cyrus/imapd/](http://asg.web.cmu.edu/cyrus/imapd/)) supports more than just IMAP. Specifically, Cyrus IMAP supports IMAP, POP3, and a Kerberos-enabled POP3 variant (KPOP). This server stores IMAP mail folders in a proprietary file format in its own directory tree, so it can be a good choice if users store nonmail files in their home directories.

- **Courier** The Courier mail server (http://www.courier-mta.org) is an integrated set of SMTP, POP, and IMAP servers. Although the Courier SMTP server isn't very popular in Linux, the IMAP server can be installed separately, and it has a modest following.

- **Qpopper** This POP3 server was originally a commercial product released by the same people who developed the popular Eudora client and server packages. With version 4.0, though, Qpopper has gone open source. You can learn more at http://www.eudora.com/products/unsupported/qpopper/.

One issue you should consider when installing and configuring a pull mail server is password security. In a typical configuration, the traditional POP and IMAP servers require password authentication—users must enter their usernames and passwords. Most servers authenticate users against the normal Linux username and password database.

The basic protocols deliver the username and password over an unencrypted link. As a consequence, a miscreant with the appropriate access can sniff the password. The SSL variants fix this problem, but they require support in the mail clients. Another approach is to use the Secure Shell (SSH) to tunnel the pull mail protocol over an encrypted link, as outlined in Chapter 9. This approach requires configuring SSH on the server and on all the clients, though. If you don’t want to go to this effort, you may want to consider setting aside special mail-only accounts and instruct users to create unique passwords for these accounts. This practice will at least minimize the damage that a miscreant might do if pull mail passwords are compromised. You may also want to restrict access to your POP or IMAP ports using firewall rules, TCP Wrappers, or xinetd access restrictions.

Actual POP and IMAP configuration varies substantially from one server to another. Given this fact, and the fact that this level of detail is not covered on the Linux+ exam, I recommend you consult server-specific documentation if you need to configure a POP or IMAP server.

## Summary

Network servers are many and varied, and Linux provides programs to handle all common network protocols. These include DHCP for configuring clients’ network settings, DNS for resolving hostnames and IP addresses, NTP for managing time on a network, POP and IMAP for pull e-mail, and SMTP for push e-mail.

Although these servers share certain common features, such as their ability to be launched via SysV startup scripts or super servers, each protocol and server is unique. Indeed, for many protocols, multiple servers are available, and each server can have its own unique configuration style. Thus, you must study each server you install and run to determine how best to manage it.
