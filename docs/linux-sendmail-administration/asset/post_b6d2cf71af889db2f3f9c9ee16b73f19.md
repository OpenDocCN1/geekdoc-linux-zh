
# A Simple Mail Transport Protocol

helo robin

250 wren.foobirds.org Hello robin [172.16.5.2], pleased to meet you
help

214-2.0.0 This is Sendmail version 8.9.3
214-2.0.0 Topics:

```
214-2.0.0 HELLO EHLO MAIL RCP DATA
214-2.0.0 RSET NOOP QUIT HELP VRFY
214-2.0.0 EXPN VERB EXTRN DSN AUTH
214-2.0.0 STARTTLS
214-2.0.0 For more info use 'HELP <topic>'
214-2.0.0   sendmail-bugs@sendmail.org.
214-2.0.0 For local information send email to Postmaster at your site.
214-2.0.0 End of HELP info
```

vrfy <norml>
250 2.1.5 <norml@24seven.wrothetbook.com>

vrfy <frank>
550 5.1.1 <frank>>... User unknown

```
expn <staff>
250 2.1.5 <becky@ani>
250 2.1.5 <sara@hawk>
250 2.1.5 <david@ani>
250 2.1.5 Craig Hunt <craig@24seven.wrothetbook.com>
250 2.1.5 <kathy@robin>
```

quit
221 wen.foobirds.org closed connection
Connection closed by foreign host.

In Listing 1.1, a user sitting at the computer uses telnet to connect to the SMTP port on wen. The first three messages displayed (Trying, Connected, and Escape) are telnet messages that have nothing to do with SMTP or Sendmail. The first SMTP message begins with the code 220. This message comes from the remote server wren, and is issued in response to the TCP connection by telnet. This message lets the local system know that the remote system will accept SMTP commands. This first message reveals several pieces of information. The message

- identifies the remote host as wen.foobirds.org
- states that the remote system is running ESMTP, which is extended SMTP, a topic covered in this chapter
- says that wren is running Sendmail version 8.11.0
- displays the time the connection is made

# Chapter 1 Internet Mail Protocols

The first command entered by the user is HELO, which identifies the local system as robin and starts the SMTP session. The remote server responds with a message that begins with code 250, and indicates that the session has begun. In Listing 1.1, the user types in the HELP command. In response to that, the remote system displays 10 lines, all of which start with the code 214. The most interesting part of this response are the commands listed under the heading Topics. These are the SMTP commands supported by wren.

> NOTE There are more commands listed in response to the HELP command in Listing 1.1 than are listed as of RFC 821 in Table 1.1. Because of three of the commands in Listing 1.1 are extended SMTP commands that we have not discussed, there are new security protocol protocol keywords (AUTH and STARTTLS), and one (VERB) is a non-standard command supported by Sendmail that is also discussed later.

The next commands entered by the user are VRFY, which verify whether or not an e-mail address is valid. Listing 1.1 shows two different ones. One tells us that norm is a valid address and the other us that frank is not. If the address entered in a VRFY command does not contain a domain name or contains the domain name of the local computer, it is checked against both the user accounts and the aliases available on the system. If the address contains the domain name of a remote host, the address is forwarded to that host and that it is the responsibility of the remote host to determine whether or not the address is valid and the mail can be delivered.

The EXPN command is used to expand a mailing list. In Listing 1.1, the name of the mailing list is staff. The system responds to the query by listing all of the e-mail addresses contained in that list.

The strange thing about the HELP, VRFY, and EXPN commands is that they are designed for more interactive than interactive users. For communications between e-mail programs, the HELP command is clearly designed for interactive users. Program-to-program communications do not use the EXPN command because the responsibility for expanding a mailing list and delivering to the members of that list falls to the destination program. Therefore, the source program does not need to check the contents of the list. Even the VRFY command, which on the surface appears to have some utility in program-to-program communications, is not needed because the e-mail addresses are verified by default at the start of the delivery process, as shown below:

```
mail from: <craig@24seven>
250 <craig@24seven>... Sender ok
```

# A Simple Mail Transport Protocol

rcpt to: <frank>

550 <frank>... User unknown

The user closes the SMTP session in Listing 1.1 with the QUIT command. The remote system responds with a message that starts with the code 221. The last line in Listing 1.1 is not part of the SMTP session. The line that starts with “Connection closed” is a message from telnet.

# SMTP Response Codes

Listing 1.1 shows all of the messages from the remote server begin with a numeric code. Table 1.2 lists the response codes defined in the RFCs.

| Response Code | Meaning |
| :--- | :--- |
| 211 | This is a status message. |
| 214 | This is a help message. |
| 220 | The service is ready. |
| 221 | The connection is closing. |
| 250 | The requested action was completed. |
| 251 | The address is not local, and the mail will be forwarded. |
| 252 | The mail must be forwarded. |
| 354 | The server is ready to accept data. |
| 421 | The service is not available. |
| 450 | The requested action was not performed. |
| 451 | The action failed because of error. |
| 452 | The action aborted because of disk space. |
| 500 | The command was not recognized. |

# Table 1.2 SMTP Response Codes (continued)

| Response Code | Meaning |
| :--- | :--- |
| 501 | The command had a syntax error. |
| 502 | The command is not implemented on this server. |
| 503 | The sequence of commands is incorrect. |
| 504 | The parameter included is not implemented on this server. |
| 550 | The action was not performed. |
| 551 | The address is not local. |
| 552 | The transaction failed. |
| 553 | The mailbox was invalid. |
| 554 | The transaction failed. |

Every SMTP command elicits a response. From the response codes in Table 1.2, it is easy to tell that codes in the 200s and 300s indicate a successful transaction, while codes in 400s indicate a failure. Most of the time, of course, you don't see these. Cooperating Sendmail programs on the local system and the remote system go about their business silently. To watch Sendmail interact with the remote system, run the sendmail command in verbose mode.

# Observing SMTP with Verbose Mode

Using telnet to connect to the SMTP port is a useful way to get a feel for the SMTP protocol, and it can be a useful test technique when you want to completely bypass your local copy of Sendmail to test the responses of a remote server. A user typing in SMTP commands approximates the exchange of protocol information based on a best guess of how the two systems interact. In most cases, it is much better to sit back and observe the systems actually interacting. The -v (verbose) option of the sendmail command lets you do exactly that. Listing 1.2 a piece of mail being sent with verbose mode.

Listing 1.2 The Protocol as Displayed by Verbose Mode

```
[craig$ sendmail -v -t
To: craig@wren
From: craig@ani
Subject: Test
Please ignore this test.
^
craig@wren... Connecting to wen.foobirds.org via esmtp...
220 wen.foobirds.org SMTP Sendmail 8.11.0/8.11.0; Mon, 23 Oct 2000
11:32:-0400
>>> EHLO ani.foobirds.org
250-wren.foobirds.org Hello root@ani.foobirds.org [172.16.12.11],
pleased to meet you
250-ENHANCEDSTATUSCODES
250-EXPN
250-VERB
250-8BITIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-XUSR
250-AUTH DIGEST-MDS
250 HELP

>>> MAIL From:<craig@ani.foobirds.org> SIZE=73
250 <craig@ani.foobirds.org>... Sender ok
>>> RCPT To:<craig@wren.foobirds.org>
250 <craig@wren.foobirds.org>... Recipient ok
>>> DATA
```
```
