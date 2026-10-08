
## mailstats 765

-v
Print verbose information. This option adds the priority of the message and a single character indicator (+ or blank) on the first line of the message indicating whether a warning message has been sent. Additionally, extra lines can be intermixed with the recipients indicating the "controlling user"; this information shows owns any programs that are executed on behalf of this message and the name of the alias this command is expanded from, if any.

## Exit Status

- +0 Successful completion.
- >0 An error occurred.

## Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNWndmu |

## See Also

sendmail(1M), prof_attr(4), attributes(5)

![](img/185d23104c385dfb6a62d64cc96b8997_794_0.png)

## mailstats — Print Statistics Collected by sendmail

## Synopsis

```
/usr/bin/mailstats [-o] [-c configfile] [-C configfile]
[-f statisticsfile] [-p] [-P]
```

## Description

The mailstats command prints the statistics collected by the sendmail(1M) program on mail usage. These statistics are collected if the file indicated by the StatusFile configuration option of sendmail (defined in /etc/mail/sendmail.cf) exists. The StatusFile configuration option is new in the Solaris 9 release. Starting with the Solaris 9 release, the default statistics file is /etc/mailstats.

The mailstats command first prints the time that the statistics file was created and the last time it was modified. It then prints a table with statistics for each mailer displayed on a single line, each with the following whitespace-separated fields.

- M The mailer number.
- msgsfr Number of messages from the mailer.
- bytes_from Kilobytes from the mailer.
- msgto Number of messages to the mailer.
- bytes_to Kilobytes to the mailer.

![](img/185d23104c385dfb6a62d64cc96b8997_794_1.png)

![](img/185d23104c385dfb6a62d64cc96b8997_794_2.png)

![](img/185d23104c385dfb6a62d64cc96b8997_794_3.png)

## 766

## mailstats

- msgsrej Number of messages rejected by the mailer.
- msgsdis Number of messages discarded by the mailer.
- Mailer The name of the mailer.

![](img/185d23104c385dfb6a62d64cc96b8997_795_0.png)

After this display, a line totaling the values for all the mailers is displayed, separated from the previous information by a line containing only equal sign (=) characters.
To reinitialize the statistics file once a night, add the following entry to the crontab(1).

![](img/185d23104c385dfb6a62d64cc96b8997_795_1.png)

```
mailstats -p > /dev/null
```

## Options

- -c configfile
-C configfile

Specify a sendmail configuration file. The -C option is new in the Solaris 9 release.

```
-f statisticsfile
```

Specify a sendmail statistics file.

![](img/185d23104c385dfb6a62d64cc96b8997_795_2.png)

- -o Don't display the name of the mailer. New in the Solaris 9

![](img/185d23104c385dfb6a62d64cc96b8997_795_3.png)

- -p Output information in program-readable mode, and clear statistics. New in the Solaris 9 release.

![](img/185d23104c385dfb6a62d64cc96b8997_795_4.png)

- -P Output information in program-readable mode without clearing statistics. New in the Solaris 9 release.

## Examples

The following example shows the output for a system that uses the ESMTP and Cyrus mailers.

```
$ mailstats
Statistics from Fri Jul 20 14:23:08 2001
M msgsfr bytes_from msgoito bytes_to msgsrej msgsdis Mailer
5 1501 33183K 302 10612K 57 0 esmtp
9 290 23568K 1523 44588K 1 0 cyrus

T 1791 56751K 55200K 58 0
C 1791 1825 58
Statistics from Sun Mar 14 12:16:39 1999 Mailer
M msgsfr bytes_from msgoito bytes_to msgsrej msgsdis
3 1791 1825 58
C 1791 56751K 55200K 58 0 local
1 1K OK 0
T 1K OK 0
$ 
```

## Usage

See largefile(5) for the description of the first behavior of mailstats when encountering files greater than 2KB (bytes).

## mailx, mail, Mail

## Files

/dev/null
Zero-lined file.
/etc/mail/statistics
Default sendmail statistics file. Changed from /etc/mail/sendmail.st to /etc/mail/statistics in the Solaris 9 release.
/etc/mail/sendmail.cf
Default configuration file.

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNWmu |

## See Also

crontab(1), cron(1), sendmail(1M), attributes(5), largefile(5)

## mailx, mail, Mail – Interactive Message System

## Synopsis

```
mailx [-Bfile] [-f file|folder] [-T file] [-u user]
mailx [-Bdf] [-c cc] [-h number] [-r address]
[-s subject] recipient...
/usr/ucb/mail...
```

## Description

The mail commands listed above provide a comfortable environment for sending and receiving mail.
When mail is read, the mail commands facilitate saving, deleting, and responding to messages. When mail is sent, the mail commands enable editing, reviewing, and other modification of the message you enter it.
Incoming mail for each user is stored in a standard file, called mailbox. When mail commands are called to read messages, the mailbox is the default place to find them. As messages are read, they are moved to a secondary file for storage, unless specific action is taken, messages need not be seen again. This secondary file is called mbox and is normally located in HOME directory. You can save messages in other files with names you specify. You can access a secondary file using the -f option. You can then read or otherwise process messages in the secondary file, using the same commands you use for the primary mailbox. When you access a secondary file with the -f option, that file is considered the current mailbox.

## Options

On the command line, options start with a dash (-). Any other arguments are taken as destinations (recipients). If you specify no recipients, mailx tries to read messages from the mailbox.

- -bcc Set the blind copy list to bcc. Enclose bcc in quotes if it contains more than one name.
- -B Do not buffer standard input or standard output.
- -cc Set the carbon copy list to cc. Enclose cc in quotes if it contains more than one name.
- -d Turn on debugging output (Neither particularly interesting nor recommended.)
- -e Test for the presence of mail. mailx prints nothing and exits with a successful return code if there is mail to read.
- -f [file] Read messages from file instead of mailbox. If you specify no file, use the mbox.
- -f [+folder] Use the folder in the folder directory (same as the folder command). The name of this directory is listed in the folder variable.
- -F Record the message in a file named after the first recipient. Override the record variable if set.
- -h number The number of network hops made so far. This option is provided for network software to avoid infinite delivery loops. This option and its argument are passed to the delivery program.
- -H Print header summary only.
- -i Ignore interrupts.
- -I Include the newsgroup and article header lines when printing mail messages. This option requires that you specify the -f option.
- -n not initialize from the system default mailx.rc or Mail.rc file.
- -N not print initial header summary.
- -r address Use as the return address when invoking the delivery program. Disable all commands. This option and its argument are passed to the delivery program.
- -s subject Set the Subject header field to subject. You must enclose subject in quotes if it contains embedded space.
- -t Scan the input for To:, Cc: and Bcc: fields. Ignore any recipients on the command line.
- -T file Record message ID and article header lines in file after the message is read. This option also sets the -I option.
- -u user Read user's mailbox. This option is effective only if user's mailbox is not protected.

## mailx, mail, Mail 769

- -U Convert UUCP-style addresses to Internet standards. Override the conv environment variable.
- -V Pass the -v flag to sendmail(1M).
- -V Print the mailx version number and exit.
- -- Interpret tilde escapes in the input even if not reading from a TTY.

## Operands

- recipient Address of message.

## Usage

## Starting Mail

At startup time, mailx escapes the system startup file /etc/mail/mailx.rc. If invoked as mail or Mail, the system startup file /etc/mail/Mail.rc is used instead.

The system startup file sets up initial display options and alias lists assigns values to some internal variables. These variables are flagged and valued parameters that are cleared by the set and unset commands. See "Internal Variables" on page 781. If mailx is started with the -n option, the mail commands do not execute the system startup file.

Regular commands are legal inside startup file except for the following commands: !, Copy, edit, followup, Followup, hold, preserve, reply, shell, and visual. When the startup file contains an error, the remaining lines are ignored.

After executing the system file, the mail commands execute the optional personal file $HOME/.mailrc, which you can use to override the values of the internal variables as set by the system startup file.

Many administrators include the following commands in the system startup files (to be compatible with post Solaris behavior), but these commands do not meet standards requirements for mailx.

```
unset appendletter
unset replyall
unset pipeignore
```

To get standard behavior for mailx, either use the -n option or include the following commands in a personal startup file.

```
unset appendletter
set replyall
set pipeignore
```
