
You can learn which e-mail server your Linux distribution runs in several ways. The two most reliable are to use `ps` (described in Chapter 2, “Managing Software”) to look for running processes, or to use your package management tools (also described in Chapter 2) to see which package is installed. In either case, you may need to check for each of the programs in turn. For instance, you might see results like these:

```bash
$ ps ax | grep send
  31129 pts/2     R+     0:00 grep send
$ ps ax | grep post
   7778 ?         Ss     0:45 /usr/lib/postfix/master
  31132 pts/2     S+     0:00 grep post
```

The search for a process containing the string `send` failed, so the search for `post` returned a process called `/usr/lib/postfix/master`—thus, it appears that Postfix is running on this system.

You can also look for executable filenames for each e-mail server in `/usr/bin` or `/usr/sbin`; but be aware that most Linux e-mail servers include a program called `sendmail`. This is done for compatibility reasons; because the original `sendmail` program was once ubiquitous, providing a compatible interface for scripts and administrators helps other SMTP servers work.

In addition to the SMTP server, a fully functional Linux e-mail system is likely to include other software:

- **Pull mail servers** Two pull mail protocols, POP and IMAP, are popular. If a Linux system should function as a mail server from which users can read their e-mail remotely, chances are you’ll install a POP or an IMAP server package, such as Cyrus IMAP (http://cyrusimap1.andrew.cmu.edu/imapd/) or Dovecot (http://dovecot.org).

- **Fetchmail** This program, based at http://fetchmail.berlios.de, fills an odd gap in the e-mail delivery chain. If you run a small site that relies on an external ISP for e-mail delivery, chances are the ISP supports only POP or IMAP. If you want to use a variety of e-mail clients, you may want to run your own SMTP server, and perhaps your own POP or IMAP server, to deliver mail locally. To do this, you need a program that pulls mail using POP or IMAP and then injects it into a local SMTP mailbox. This is the job of Fetchmail. Most sites don’t need it, but for those that do, it’s indispensable.

- **Mail readers** The final link in the e-mail chain is the mail reader. Examples in Linux include Evolution (http://www.gnome.org/projects/evolution/), KMail (http://kontact.kde.org/kmail/), pine (http://www.washington.edu/pine/), and Mutt (http://www.mutt.org). The `mail` utility, which is installed on most Linux systems by default, is the lowest-common-denominator e-mail utility. It’s described shortly, in “Sending and Receiving E-mail.” Most Linux e-mail clients enable reading either from a local mail queue or from a remote POP or IMAP mail server. A multi-user system is likely to have multiple e-mail clients installed, enabling each user to choose which client to use.

Neither this book nor the Linux exam covers pull mail servers, Fetchmail, or mail readers in any detail. As a practical matter, you may need to learn how to configure any or all of these packages, depending on your site's needs. Fortunately, mail reader configuration, which is the most common task, is usually fairly straightforward, as long as you have information on the hostnames of your outgoing (SMTP) and incoming (POP, IMAP, or local queue) e-mail servers.

## Managing E-mail

Although setting up an e-mail server for a site is beyond the scope of this book and the LPI Level 1 exam, managing a few common e-mail server administrative tasks is not. I therefore describe some common administrative tasks involving sending and receiving mail using the `mail` utility, e-mail queue management, configuring aliases, and forwarding e-mail.

### Sending and Receiving E-mail

Linux supports a wide variety of e-mail clients, some of which were mentioned earlier, in “Choosing E-mail Software.” Chances are, you’ll use a full-fledged e-mail client for your personal e-mail; however, you should also know how to use the `mail` program. This tool is a very basic command-line e-mail utility. It has the advantage of being usable from a script, so you can write a script to automatically handle some e-mail tasks, and perhaps even run that script automatically. For instance, you might write a script to check for user passwords that are about to expire and then e-mail the users about this impending event so that they can change their passwords before their accounts are locked.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_509_0.png)

> Some Linux systems ship with a program called `mail` rather than `mail`. The `mail` program supports additional features compared to the original `mail`, such as the ability to add attachments; but the two programs are very similar in basic operation. Typically, a link with the name `mail` points to `mail`, so you can call `mail` as `mail`.

The `mail` program is intended to be used on the command line to send or receive messages. The basic syntax for `mail`, including its most useful options, is as follows:

```bash
mail [-v] [-s subject] [-c cc-addr] [-b bcc-addr] to-addr
mail [-v] [-f [name] | -u user]
```

The first of these syntax lines is used for sending e-mail; the second is used for reading e-mail. (Unlike most e-mail readers, `mail` only supports reading the local e-mail queue, not e-mail stored on remote servers and read via POP or IMAP.) You can achieve various goals with the options to `mail`:

- **Use verbose operation** As with many commands, the `-v` option produces more verbose output. This may be helpful if you need to debug problems.

- **Specify a subject line** The `-s subject` option enables you to specify a subject line.

- **Set a carbon copy address** You can send a message to multiple people by sending a *carbon copy* using the `-c cc-addr` or `-b bcc-addr` options. These options vary in that the `-b` option produces a “blind” carbon copy, meaning that the recipient’s address doesn’t appear in the address list. This is useful if you want to discreetly send a copy of an e-mail to somebody, but some spam filters may delete such e-mails.

- **Set the recipient’s address** The main recipient’s e-mail address terminates the `mail` command’s line for an outgoing e-mail.

- **Read e-mail** To read your e-mail, pass the `-f` option to the program, optionally followed by the name of the mail spool file. Alternatively, you can use the `-u user` option to read the mail of the specified user.

This list of options is incomplete, but it includes the most important features. You should consult the man page for `mail` to learn about more exotic options. Remember that some systems use `mail` whereas others use `mail`, and available options differ for these two programs. The preceding options have the same effect for both programs; but some options, such as `-a`, have different meanings for the two programs. (The `-a` option enables you to insert an arbitrary e-mail header in the original `mail` but in `mail` it’s how you attach a file to an outgoing message.)

As an example of `mail` in action, consider the task of sending a quick e-mail message. Suppose you want to send an e-mail to two recipients informing them of a meeting. You can do so as follows:

```bash
$ mail -s 'Meeting reminder' -c benf@example.com sallyg@example.com
Remember the meeting at 4:00 today!
Cc: benf@example.com
```

After you type the `mail` command, the program waits for input via standard input, but there’s no prompt. You signal the end of the message by pressing Ctrl+D. This example shows a simple one-line message. After you press Ctrl+D, the program displays the `Cc:` line to verify this option. You can still change the address at this point, but if you don’t want to, you can press the Enter key and the message will be on its way.

To use `mail` in a script, you can use input redirection to pass it the contents of a file to be mailed:

```bash
mail -s 'Automated alert!' < /tmp/alert.txt benf@example.com
```

This line, if included in a script, sends the contents of `/tmp/alert.txt` to `benf@example.com` with the specified subject.

You can use `mail` to read incoming e-mail, too, but only if it’s stored on a local Linux mail spool. In this case, you’ll normally use `mail` interactively. Type `mail`, and you’ll see the contents of your mail spool. Each message has a summary line that lists the sender, date, and subject, among other things:

```
0046 sally@luna.edu Sun Aug 17 18:27 116/4262 Priorities
```
