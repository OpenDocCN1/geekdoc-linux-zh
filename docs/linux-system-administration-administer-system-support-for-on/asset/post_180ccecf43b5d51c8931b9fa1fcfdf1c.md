
## Listing 12-1: Majordomo help file

>> help
This is Brent Chapman's "Majordomo" mailing list manager. Version 1.93.

In the description below, items contained in []'s are optional. When providing the item, do not include the []'s around it.

It understands the following commands:

- `subscribe <list> [<address>]`
  Subscribe yourself (or `<address>` if specified) to the named `<list>`.
- `unsubscribe <list> [<address>]`
  Unsubscribe yourself (or `<address>` if specified) from the named `<list>`.
- `get <list> <filename>`
  Get a file related to `<list>`.
- `index <list>`
  Return an index of files you can "get" for `<list>`.
- `which [<address>]`
  Find out which lists you (or `<address>` if specified) are on.
- `who <list>`
  Find out who is on the named `<list>`.
- `info <list>`
  Retrieve the general introductory information for the named `<list>`.
- `lists`
  Show the lists served by this Majordomo server.
- `help`
  Retrieve this message.
- `end`
  Stop processing commands (useful if your mailer adds a signature).

Commands should be sent in the body of an email message to "*Majordomo*".

Commands in the "Subject:" line are not processed.

If you have any questions or problems, please contact "Majordomo-Owner".

>> end
END OF COMMANDS

To send commands to a majordomo server, all you need do is send an e-mail to majordomo@site.that.has.majordomo.com and keep the subject line empty. Now move down to the body of the message.

If you have a signature file, you'll want to disable it or type `end` at the end of your commands. Now, you're able to enter the commands to the majordomo server. Table 12-1 lists some majordomo commands.

**TABLE 12-1 MAJORDOMO COMMANDS**

| Command | What It Does |
| --- | --- |
| subscribe | Subscribes you to the specified mailing list |
| unsubscribe | Unsubscribes you from the specified mailing list |
| get | Gets a file from a particular list |
| index | Gets the index of files available from a particular list |
| which | Finds out which lists you are subscribed to on this server |
| who | Finds out who is subscribed to a particular list |
| info | Finds out introductory information about this list. It may be a text file that was sent to you if you're already subscribed |
| lists | Finds out what lists are available on this server |
| help | Prints the help document |
| end | Finishes inputting commands. (Great if you can't figure out how to disable your signature file.) |

Here are some examples of commands and their output. Any command entered in a message will be "quoted" (with `>>` preceding the command) to separate it from the output.

If I want to see who's on the vax-plus mailing list, the output would look like this:

```text
>> who vax-plus
Members of list 'vax-plus':
User1@host.com
User2@host1.com
User4@myhost.org
User5@yourhost.net
```

If I want to see what lists are available on Majordomo@the.vax.com, I send it the lists command:

```text
>> lists
Majordomo@the.vax.com serves the following lists:
```

| List | Description |
| --- | --- |
| row_h-i | Keeping old and new VAXers together. Announcements only. |
| test | Testing only. Don't. |
| tigerjokes | Jokes and amusement from [HOBBS] |
| unixtips | Unix Tip o' the Day from [HOBBS] |
| vax-plus | General discussions, musings, and rantings. |
| vp-digest | Digest version of vax-plus |
| weird | Flakes, wacos and weirdos and holders of SleazeFest. |

If I wanted to find out which lists on this server I'm subscribed to, I'd send it the following command:

```text
>> which stripes@tigerlair.com
The string 'stripes@tigerlair.com' appears in the following
entries in lists served by Majordomo@the.vax.com:
```

| List | Address |
| --- | --- |
| row_h-i | stripes@tigerlair.com |
| tigerjokes | stripes@tigerlair.com |
| unixtips | stripes@tigerlair.com |
| vax-plus | stripes@tigerlair.com |

If I wanted to see the index of files available from the vax-plus mailing list, I would get an index of the files.

```text
>> index vax-plus
#### No files available for vax-plus.
```

When I'm done with the commands, I issue the end command, like this:

```text
>> end
END OF COMMANDS
```

> Majordomo is written in Perl and maintained by Great Circle and Associates. To get a copy of Majordomo, check out http://www.greatcircle.com/majordomo.

## LISTSERV

Listserv was the original mailing-list management software. It originated on BIT-NET, a now-defunct academic network. Listserv migrated to the Internet and still administers many mailing lists today. Its commands give it functionality similar to that of Majordomo, and it's not as easy to customize. Table 12-2 lists the basic commands for Listserv.

**TABLE 12-2 LISTSERV BASIC COMMANDS**

| Command | What It Does |
| :--- | :--- |
| subscribe | Subscribes you to the Listserv |
| unsubscribe | Unsubscribes you from the Listserv |
| conceal | Hides your name so others can't see you're on the list. |
| noconceal | Makes your name publicly available to the mailing list |
| set acknowledgement | Gets notified each time you send to the Listserv |
| set noacknowledgement | Doesn't get notified each time you send to the Listserv |
| set nomail | Temporarily suspends the Listserv messages |
| set mail | Restores receiving messages from the Listserv |
| set digests | Receives digests from the mailing list instead of one message at a time |
| review list | Sees who else is on the mailing list |
| search | Searches the archives for a particular string |

![](img/8ad518fddafc7f5e73715a2604b61d50_408_0.png)

Listserv is not freeware. If you are interested in the Listserv software, however, check out http://www.lsoft.com.

## Daemons

E-mail is managed by daemons such as POP3 (which enables you to download your mail remotely and read it off-line); IMAP (which enables you to read your mail remotely); and sendmail (which enables you to be the mail authority for a certain domain). Except for sendmail, these daemons are managed by inetd, the networking super-daemon. All work in a client-server model; the daemons perform as servers. POP3 and IMAP both let the users start the clients (Pine uses IMAP, and POP can be used with other clients such as Mutt). To use a client with POP or IMAP, you don’t have to have the daemons running.

As with POP and IMAP, sendmail is a delivery agent – but its workings are a little more complicated. You can use sendmail to filter messages (for example), and you may find its design less friendly than that of POP or IMAP.

![](img/8ad518fddafc7f5e73715a2604b61d50_408_1.png)

Sendmail is known to be a major security hole. Additionally, some cleartext-related holes have appeared recently in IMAP and in POP (especially since they send passwords over the wire). If you’re going to use a mailer, first try using qmail instead. It’s not only easier to use, but more secure. You can find it at http://www.qmail.org.

## Using Client Applications

Several clients are available for the World Wide Web, including Netscape, as shown in Figure 12-4. Some Web browsers include the functionality needed to read e-mail or USENET news.

![](img/8ad518fddafc7f5e73715a2604b61d50_409_0.png)

Figure 12-4: Using the Netscape Web browser

Another common text-based browser is Lynx, shown in Figure 12-5. Although Lynx enables you to view information on a Web page, sometimes the formatting needs to be tinkered with. It can offer some World Wide Web access, even if you don't currently have X capabilities.

Web servers, or HTTP daemons, can provide Web pages through port 80. These Web pages can also include CGI programs, Java, and JavaScript as well. You can run httpd through inetd if you wish (probably a good idea). Slackware comes with the Apache HTTP daemon. Apache is freeware and currently one of the most popular Web servers available.

![](img/8ad518fddafc7f5e73715a2604b61d50_410_0.png)

## Setting Up the Apache Web Server

Various Web servers are available for Linux - Netscape, NCSA, and Apache. Conveniently enough, Apache comes on the Slackware CD-ROM included with this book, and is available for downloading from http://www.apache.org.

To install the Slackware package, you can go to the Slackware disk sets and find the *apache.tgz* package in the set labeled n1. If you've installed Apache during the Slackware installation process, all you have to do is start the *httpd* daemon.

> You can have the daemon started by the *inetd* daemon to enhance manageability.

To start the daemon from the command line, type `# httpd &` at the prompt.

When you have the daemon up and running, you should be able to see the startup screen. To see the startup screen, start your Web browser and open the URL *http://localhost/* . It should look like Figure 12-6.
