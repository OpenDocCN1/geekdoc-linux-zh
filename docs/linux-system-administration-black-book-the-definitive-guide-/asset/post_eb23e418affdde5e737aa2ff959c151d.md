
## Table 12.2 The full list of standard Message Identification And Referral header fields.

| Header | Purpose |
| --- | --- |
| Content-Base: | Identifies a URL with the directory in which you can find the Web page for a piece of HTML email. |
| Content-Id: | Specifies a special identifier to uniquely label MIME message content for high-level user agents. |
| Content-Location: | Identifies the exact URL where you can find the Web page for a piece of HTML email. |
| In-Reply-To: | Usually includes the Message-Id value from the email this mail contains a response to. |
| Message-Id: | Identifies the unique ID value generated for this message. |
| References: | Specifies the Message-IDs that this email refers to. |

Often, this means that this user uses both Post Office Protocol (POP) and SMTP mail servers and has his or her primary email address set as the POP address. However, you have to use SMTP to send email—you cannot use POP. Therefore, the X-Sender header item was added to tell the recipient's mail client which account to send to when sending responses. X-Sender is part of the Sender And Recipient Indication mail header options, shown in Table 12.3.

After this line comes another Sender And Recipient Indication item:

```
X-Mailer: QUALCOMM Windows Eudora Pro Version 4.2.2
```

Then comes this line:

```
Date: Wed, 08 Nov 2000 18:47:34 -0800
```

## Table 12.3 The full list of standard Sender And Recipient Indication header fields.

| Header | Purpose |
| --- | --- |
| bcc: | Identifies recipients not listed for others to see. |
| cc: | Identifies secondary recipients copied on the mail. |
| From: | Identifies the account the email came from. |
| Sender: | Identifies the account the email came from. Often not used. |
| To: | Identifies the intended recipients. |
| X-Mailer: | Includes information about the mail client used by the sender. |
| X-Sender: | Specifies an email address you can use to reply to if the From: address is not able to accept replies. |

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_384_0.png)

# Chapter 12 Internet Email: sendmail + lDA

The Date header is part of a small group that refers to date and time information. It is the only header item in its group that is standard for email use. This header specifies either when the mail was written or when the mail was passed to the sender's mail server, depending on how this server is set up.

After the Date header is a pair already covered in the Sender And Recipient Indication headers in Table 12.3:

- To: "Diane Smith" <dsmith@inventors.com>
- From: Mary Smith <msmith@spices.com>

The following is a miscellaneous header type:

- Subject: Movies

It is listed with its cousins in Table 12.4.

Another item already mentioned is the In-Reply-To header, which tells you which email this particular mail was written in response to:

- In-Reply-To: <NOBB LM LFK LJ PNF AH B B D I E EKJCHAA.dsmith@inventors.com>

After this is another header that is the only one in its class that is standard for email use:

- MIME-Version: 1.0

This header contains information about which MIME standard the message was formatted to adhere to. Finally, the following line ends the mail header:

- Content-Type: text/plain; charset="us-ascii"; format=flawed

Content-Type is one of two headers used in email among the Encoding Information type of headers:

## Table 12.4 Miscellaneous mail header fields.

| Header | Purpose |
| --- | --- |
| Comments: | Includes meta-information about the mail message. Should be enclosed in parentheses. |
| Content-Description: | Often contains labels for attached files. |
| Keywords: | Includes comma-separated terms or phrases used for database searches. |
| Subject: | Specifies the email's topic. |

- *Content-Transfer-Encoding:*—The coding method used in a MIME message
- *Content-Type:*—The format used to view this mail's content

## How Mail Queues Are Put Together

When one of your users sends a piece of email that has to pass through **sendmail**, that mail at some point has to spend time in the mail queue. How long it spends there depends on how large your mail volume is at the moment, how fast your machine is, how much RAM it has, how fast your connection is, how large the mail is, and how much bandwidth is available for sending mail over the connection at this moment.

You can find your mail queues in `/var/spool/mail`. Any user that has mail in their inbox has a file in this directory. This file is a text file containing all mail the user has in their inbox in the order it arrived. The fact that your queue is a text file is what makes mail insecure. Any curious system administrator could waltz through anyone's mail queue on their site, as could anyone who gained root access on the system.

## Introduction To sendmail

Just as email is one of the most popular services on the Internet, **sendmail** is one of the most popular servers on the Internet. It is a powerful tool that lets you finely configure many aspects of your site's mail handling. Unfortunately, this means that **sendmail** traditionally has been a daunting server to configure. IDA's additions to this server have greatly reduced this concern. You now configure **sendmail** by using macros, which enables you to just give the key information. The macro processor, **m4**, does the rest when it builds your full configuration file for you.

## The MC File

Configuring **sendmail** + IDA begins with the macro configuration file, which ends in the extension _.mc_. You can make this file from scratch, or use the example files often provided along with the **sendmail** code. This is the first file you edit when you begin to set up your email server. The Red Hat macro configuration file is relatively short, so I will walk you through it.

> **TIP:** Go to [www.sendmail.org](http://www.sendmail.org) if you want to download a fresh version of this code.

The first line in the macro configuration file is almost always the following:

```
divert(-1)
```

![](img/e612d46dba3c9205aa19fee9eb8dd0a4_386_0.png)

This line should appear before any large comment section that you do not want to include in the final **sendmail** configuration file. Typically, it is used only at the beginning of the MC file. Its presence there ensures that the instructions included for the user are not transferred to the resulting file during the macro conversion process.

Next is the section that you do not want to have sent to the new file: the instructions. Each line may begin with either of two things: a hash mark (#) or a delete through newline (**dnl**). The **dnl** format is shown in the following code section. The **dnl** codes tell the macro processor to ignore everything from its location to the end of the line.

> **NOTE:** Because **dnl** codes are used here instead of hash marks, you could actually skip the *divert* statements altogether.

```
dnl This is the macro config file used to generate the /etc/sendmail.cf

dnl file. If you modify the file you will have to regenerate the
dnl /etc/sendmail.cf by running this macro config through the m4
dnl preprocessor:
dnl
dnl	m4 /etc/sendmail.mc > /etc/sendmail.cf
dnl
dnl You will need to have the sendmail-cf package installed for this to
dnl work.
divert(0)
```

After you get past the instructions, the first line tends to be an **include** statement. Notice that the first quote is a backward quote, whereas the ending one is an apostrophe. All string data must be surrounded by this configuration of quotes. Next is an **include** statement, which tells the macro processor to open the specified file and insert its contents in place of the statement. In this case, the **include** is as follows:

```
include(`../m4/cf.m4')
```

The file you include here is the following:

```
divert(-1)
#
# Copyright (c) 1998 Sendmail, Inc. All rights reserved.
# Copyright (c) 1983, 1995 Eric P. Allman. All rights reserved.
# Copyright (c) 1988, 1993
# The Regents of the University of California. All rights reserved.
#
```
