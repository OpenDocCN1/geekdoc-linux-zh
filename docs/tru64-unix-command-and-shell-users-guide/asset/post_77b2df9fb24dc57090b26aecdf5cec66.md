
## Sending and Receiving Messages

This chapter describes how to send or receive messages over the network by using one of the following commands:

- mailx or Mail
- write
- Message Handling (MH) program
- talk

Examples in this chapter use the mailx program rather than Mail. Using mailx, you can do the following tasks:

- Send a message to a user
- Edit a message before sending it
- Include files within messages
- Save or organize incoming messages

Using mailx you can also send entire files, a task described in Chapter 12.

The Tru64 UNIX mailx or Mail command accesses the same mail program as the ULTRIX mail (that is, /usr/ucb/mail) command. Refer to Chapter 2 of the ULTRIX to DIGITAL UNIX Migration Guide for more information.

The write and talk commands work interactively; the recipient must be logged in. Before using these interactive commands, you can verify the name and availability of a user or host by using the following commands described in Chapter 10:

- finger or who to find a user on the local host
- finger, rwho, or ruptime to find a user on a remote host
- ping or ruptime to find a currently reachable host

### 11.1 Addressing Mail Messages

Using mailx, you can send a message to one or more users at the following locations:

- On your local host
- On a remote host connected to your local host through TCP/IP
- On a host in another network, through either TCP/IP, DECnet, or UUCP addressing

Use the following syntax for the mailx command:

```
mailx user [@ { host | domain | host.domain}] ...
```

To send mail to users on the local host, enter the mailx command and specify a user parameter for each user. For users on remote hosts, you must specify additional information about the location of the host after the “at sign” (@).

For example, to send mail from host orange to users smith and jones on the same local host, you would enter the following command:

```
orange% mailx smith jones
```

To send mail to user hobbes on a different host, pluto, in the same **domain**, you would enter the following command:

```
orange% mailx hobbes@pluto
```

In the preceding example, if user hobbes were in another domain called planets, you would add the name of the remote network domain, as shown in the following command:

```
orange% mailx hobbes@pluto.planets
```

The domain is sometimes split into further subdivisions with the name of each separated by a period (.) in the destination name. Depending on how the network has been configured by the network administrator, you can address a user on a remote host in another domain by specifying only the domain name, as in the following command:

```
orange% mailx hobbes@planets
```

If necessary, see your system administrator for help addressing a mail message.

### 11.2 Sending a Mail Message Using mailx

This section explains how to use mailx to send a message to a user on a local host and a copy of the message to other users. To begin the example, user Jones enters the mailx command at the local system prompt, orange%:

```
orange% mailx suzuki  Return
```

After pressing the Return key, the Subject: prompt is displayed. Pressing the Return key again immediately would leave the subject blank. Instead, user Jones enters the subject of the message before pressing the Return key, and then begins writing the message:

```
Subject: Baseball question  Return
Are there any Japanese baseball simulation games?
I want to compare Sadaharu Oh’s hitting statistics
to those of Hank Aaron. To do this, I need to set
up a simulated baseball season having each hitter
play for one year in the other player’s league.
```

User Jones ends the message by typing a period (.) on a blank line, followed by the Return key, as shown:

```
play for one year in the other player’s league.
.  Return
```

Cc:

In this example, the message has not yet been sent; instead the Cc: (that is, “carbon copy”) prompt appears because user Jones has customized his mail session by adding set askcc to the .mailrc file in his home directory. (See Section 11.6 and Appendix D on customizing your mail session.)

The Cc: prompt enables you to send copies to other users. If you choose not to, press the Return key to exit mailx, and send the message; the end-of-text message (EOT), then appears followed by the system prompt.

In this example, user Jones sends copies to local user cranton and remote users gillis and vincep by entering the appropriate address for each at the Cc: prompt and pressing the Return key to exit mailx and send the message:

```
Cc: cranton gillis@strato vincep@mlb.bbs.com  Return
EOT
orange%
```

The mailx program enables you to recover from addressing errors. For example, if your intended recipient on the local host is cranton, but you mistakenly type crantom, the following message appears immediately on your screen:

```
crantom... User unknown
```

The message is mailed back to you. You can then save and resend it to the right person.

If you send a message to an unknown person on a remote host, it may take as long as three days before mailx sends it back to you. Section 11.3.3.1 explains how to save and resend a returned message.
