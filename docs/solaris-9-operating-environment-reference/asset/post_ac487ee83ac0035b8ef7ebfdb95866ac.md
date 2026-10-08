
# 760

# mail, rmail

# Operands

recipient A user login name.

# Usage

largefile(5) for the description of the behavior of mail and rmail when encountering files greater than or equal to 2 Gbytes (2**31 bytes).

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of mail: LC_TYPE, LC_MESSAGES, and NLSPATH.

- Determine the time zone used with date and time strings.

# Exit Status

- 0 Successful completion when the user had mail.
- 1 The user had no mail or an initialization error occurred.
- >1 An error occurred after initialization.

# Files

```
dead.letter Unifiable text.
/etc/passwd Used to identify sender and locate recipients.
$HOME/mbox Saved mail.
$MAIL Variable containing path name of mail file.
/tmp/ma* Temporary file.
/tmp/MLDBG* Debug trace file.
/var/mail/*.lock Lock for mail directory.
/var/mail/: saved Directory for holding temp files to prevent loss of data in the event of a system crash.
/var/mail/user Incoming mail for user; that is, the mail file.
```

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcsu |

# Also

chmod(1), csh(1), login(1), mailx(1), vacation(1), ucp(1), uencode(1C), attributes(5), environ(5), largefile(5)

# mailcompat 761

Solaris Advanced User's Guide

# mailcompat — Provide Compatibility for Solaris Mailbox

# Format

/usr/bin/mailcompat

# Description

The mailcompat command provides SunOS 4.x compatibility for the Solaris mailbox format. You typically run run mailcompat to be able to read mail on a workstation running 4.x when your mail server is Solaris.

Enabling mailcompat creates an entry in an existing .forward file in your home directory. If the .forward file does not exist, mailcompat creates it. Disabling mailcompat removes the entry from the .forward file, if this was the only entry, removes the entire file.

To execute mailcompat, log in to the Solaris mail server and enter mailcompat on the command line. Answer the queries provided by the program.

# Usage

See large(5) for the description of the behavior of mailcompat when encountering files greater than or equal to 2 Gbytes (2**31 bytes).

# Examples

The following example enables the mailcompat feature and displays the contents of the .forward file.

```
castle$ mailcompat
This program can be used to store your mail in a format
 you can read with SunOS 4.X based mail readers
To enable the mailcompat feature a .forward file is created.
Would you like to enable the mailcompat feature? y
Mailcompat feature ENABLE.Run mailcompat with no arguments to remove it
castle$ .forward
"/usr/bin/mailcompat winsor"
castle$$
```

The following example disables the mailcompat feature for user winsor.

```
castle$ mailcompat
This program can be used to store your mail in a format
y you can read with SunOS 4.X based mail readers
You have a .forward file in your home directory containing:
"/usr/bin/mailcompat winsor"
Would you like to remove it and disable the mailcompat feature? y
Back to normal reception of mail.
castle$$
```

# Files

~/.forward List of recipients for forwarding messages.

# 762

# mailp

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUMwcsu |

# See Also

mailx(1), attributes(5), largefile(5)

# mailp — Ends to the mp Text to PDL Pretty Print Printer

# Synopsis

```
/bin/mailp [options] filename...
/bin/newsp [options] filename...
/bin/digestp [options] filename...
/bin/filep [options] filename...
/bin/filofaxp [options] filename...
/bin/franklin [options] filename...
/bin/timemamp [options] filename...
/bin/timesysp [options] filename...
```

# Description

The mailp command, new in the Solaris 8 Operating Environment, is a front end to the mp(1) program. The mailp command has different names to various mp options, as described below:

- mailp Print mail messages.
newsp Print USET articles.
digestp Print USenet digest files.
filep Print ordinary ASCII files.
ofilaxp Print in Filofax personal organizer format.
franklin Print in Franklin Planner personal organizer format.
timeman Print in Time Manager personal organizer format.
timesysp Print in Time/System International personal organizer format.

mailp and the associated programs read each file name in sequence and generate a prettified version of the contents. If you provide no file-name arguments, mailp works in the following two ways:

- With the -D option, it acts as an X print server client to produce the PDL of the target printer and spool it.
- With the -d or -P option, it generates and spools PostScript output.

# mailp

# 763

# Options

- -d printer Send output to the named printer. Otherwise, send output to the printer named in the PDL the PR environment variable.

- -D Generate the output for the target printer, and spool it to the printer.

- -F Instead of printing the name of the recipient of the mail article, the top header displays the name of the sender of the mail article. This option is useful for people with their own personal printer.

- -h Disabled banner printing. Most of the information that typically appears on the banner sheet is output in the mp banners.

- -1 Format output in landscape mode, and print two pages of text sheet of paper.

- -P printer Same as the -d option. For backward compatibility, the -P option—which spoools the PDL directly to the target printer in mp(1)—produces PostScript when used in mailp.

- -s subject Use as the new subject for the printout. When printing ordinary ASCII files that have been specified on the command line, the subject defaults to the name of each file.

# Operands

- filename The name of the file to be read.

# Environment Variables

If you do not specify the -d, -D, or -P option, mailp uses the PRINTER variable to determine the printer to receive the output from mp(1) program. If PRINTER variable is not found, the default destination is PostScript.

# Exit Status

- 0 Successful completion.
1 An error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWmp |

# See Also

- mp(1), attributes(5)

# mailq — Print the Mail Queue

Synopsis
/usr/bin/mailq [-q subarg] [-v]

Description
mailq displays a summary of the mail messages queued for future delivery.
The first line displayed for each mail message shows the internal identifier used on this host for the message, the size of the message in bytes, the date and time the message was accepted into the queue, and the envelope sender of the message.
The second line of the display shows the error message that remained in the queue. This line is not displayed if the message is being processed for the first time.
Mailq command used to be identical to sendmail -bp. Starting in the Solaris 9 release, it checks for the authorization attribute, solaris.mail.mailq. If the check for the invoking user succeeds, sendmail -bp is executed with the remaining argument vector. Otherwise, an error message is printed. This authorization attribute is, by default, enabled for all users. You can disable it by modifying the Solaris User entry in prof_attr(4).

# Options

- -qp[time] Similar to -qtime, except instead of periodically forking a child to process the queue, sendmail forks a single persistent child for each queue that alternates between processing the queue and sleeping. Specify the sleep time as the argument. The process always sleeps at least 5 seconds if the queue was empty in the previous queue. New in the Solaris 9 release.

- -qf Process saved messages in the queue once and not fork( ) but run in the foreground. New in the Solaris 9 release.

- -qG name Process jobs only in the queue called name.

- -q[!]I Limit processed jobs to those containing substr as a substring of the queue ID. Specify ! to negate the substr argument. New in the Solaris 9 release.

- -q[!]R Limit processed jobs to those containing substr as a substring of one of the recipients. Specify ! to negate the substr argument. New in the Solaris 9 release.

- -q[!]S Limit processed jobs to those containing substr as a substring of the sender. Specify ! to negate the substr argument. New in the Solaris 9 release.
