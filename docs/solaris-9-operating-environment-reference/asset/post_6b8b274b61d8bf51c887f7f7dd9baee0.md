
# 784

# mailx, mail, Mail

record=file

Record all outgoing mail in file. Disabled by default. See also folder. Note that mailx does not lock your record file. So, if you use a record file and send two or more messages simultaneously, lines from the messages may be interleaved in the record file.

Reverse the effect of the reply and Reply and followup commands. Although set by default, replyall is frequently used in the system startup file. See flipl for "Starting Mail" on page 769.

replyall

Enable saving of messages in deadletter on interrupt or delivery error. See DEAD in "Environment Variables" for page 785 for a description of this file. Enabled by default.

save

Set the number of lines in a full screen of headers for the headers command. number must be a positive number. The default is set according to baud rate or window size. With a baud rate less than 1200, defaults to 5; if the baud rate is exactly 1200, it defaults to 10. If you are in a window, number defaults to the default window size minus 4. Otherwise, the default is 20.

screen=number

Alternative command for delivering messages. Note that, in addition to the expected list of recipients, mail also passes the -i and -m options to command. Because these options are not appropriate for other commands, you may have to use a shell script that strips them from the arguments before invoking the desired command. Default is /usr/bin/mail.

sendmail=shell-command

Wait for background mailer to finish before returning. Disabled by default.

sendwait

Show the sender's real name (if known) in the message header of the mail address. Disabled by default, showname is set in /etc/mail/mailx.rc system startup file for mailx.

showname

When displaying the header summary and the message is from you, print the recipient's name instead of the author's name.

showto

Insert the variable into the text of a message when the -a (autograph) command is used. No default (see also ~i in "Tilde Escapes" on page 779).

sign=string

Insert the variable into the text of a message when the ~A command is used. No default (see also ~i in "Tilde Escapes" on page 779).

Sign=string

Set the number of lines of header to print with the top command. Default is 5.

toplines=number

# mailx, mail, Mail

verbose Invoke sendmail(IM) with the -v flag.

Use the translate program to translate mail addresses. The program receives mail addresses as arguments. It produces, on the standard output, lines containing the following data, in this order:

- The postmark for the sender (see the postmark variable).
- Translated mail addresses, one per line, corresponding to the program's arguments. Each translated address replaces the corresponding address in the mail message sent.
- A line containing only y or n. If the line contains y, you are asked to confirm that the message should be sent.

The translate program is invoked for each mail message to be sent. The program exits with a non-zero exit status or fails to produce output, the message is not sent.

# Usage

See large(5) for the description of the behavior of mailx when encountering files greater than or equal to 2 Gbytes (2*31 bytes).

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of mailx: HOME, LANG, LC_TYPE, LC_TIME, LC_MESSAGES, NLPATH, and TERM.

- DEAD The name of the file used to save partial letters in case of untimely interrupt. Default is $HOME/dead.letter.
- EDITOR The command to run when the edit or -e command is used. Default is edit(1).
- LISTER The command (and options) to use when listing the contents of the folder directory. The default is ls(1).
- MAIL The name of the initial mailbox file to read (in lieu of standard system mailbox). The default is /var/mail/username.
- MAILRC The name of the startup file. Default is $HOME/.mailrc.
- MAILX_HEAD Include the specified string at the beginning of the body of each message that is sent.
- MAILX_TAIL Include the specified string at the end of the body of each message that is sent.
- MBOX The name of the file in which to save messages that have been read. The exit command overrides this function, as does saving the message explicitly in another file. Default is $HOME/mbox.
- PAGER The command to use as a filter for paginating output. You can also use this variable to specify the options to be used. Default is pg(1), or if bsdcompat variable is set, the default is more(1). See "Internal Variables" on page 781.
- SHELL The name of a preferred command interpreter. Default is sh(1).
- VISUAL The name of a preferred screen editor. Default is vi(1).

# 786

# Exit Status

When you specify the -e option, the exit values are returned:

- 0 Mail was found.
- >0 Mail was not found or an error occurred.

Otherwise, the following exit values are returned:

- 0 Successful completion. Note that this status implies that all messages were sent, but it gives no assurances that any of them were actually delivered.
- >0 An error occurred.

# Files

```
$HOME/.mailrc
  Personal startup file.
$HOME/.mbox  Secondary storage file.
$HOME/.mailock
  Lock file to prevent multiple writers of system mailbox.
/etc/mail/mailx.rc
  Optional system startup file for mailx only.
/etc/mail/Mail.rc
  BSD compatibility systemwide startup file for /usr/ucb/mail and
/tmp/R[emqs]*
  Temporary files.
/usr/share/lib/mailx/mailx.help*
  Help message files.
/var/mail/*  Post office directory.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNWcsu |

# See Also

echo(1), ed(1), ex(1), fmt(1), lp(1), ls(1), mailx(1), mailcompat(1),
more(1), newaliases(1), pg(1), sh(1), vacation(1), vi(1), biff(1B),
uucp(1C), sendmail(1M), aliases(4), passwd(4), attributes(5), environ(5),
largefile(5), standards(5)

# make

# make — Maintain, Update, and Regenerate Related Programs and Files

# Synopsis

```
/usr/ccs/bin/make [-dd] [-D] [-DD] [-e] [-i] [-k] [-n] [-p] [-P]
[-q] [-r] [-s] [-t] [-V] [-f makefile]...[-K statefile]...
[target] (macro=value)
/usr/xg4/bin/make [-d] [-dd] [-DD] [-i] [-k] [-n] [-p] [-P]
[-q] [-r] [-s] [-t] [-V] [-f makefile]...[target] (macro=value)
```

Description
You use the make command
 makefile to specify a list of dependencies from source files and the target
application. The make command uses make to determine the minimum
compilation needed to rebuild the application. make uses file-system modification
dates to determine which files are newer than their dependencies. Then, make rebuilds the
modules and reconstructs the application.

The make command executes a list of shell commands associated with each target,
makefile contains entries that
describe how to bring a target up-date with its dependencies. Because each
dependence is a target, it has dependencies of its own. Targets, dependencies, and
subdependencies constitute a tree structure that make traces when deciding whether
ot rebuild a target.

The make command recursively checks each target against its dependencies,
beginning with the first entry in
makefileif you specify no target on
t line. If after processing all of its dependencies, a target file is either
molder than any of its dependencies, make rebuilds it. Optionally, with this
version of make, you can treat a target as an out-of-date when the commands used to
have changed since the last time the target was built.

To build a target, make executes the list of commands, called a rule. You can list
this explicitly in the target's makefile, or it can be supplied implicitly by
make.

If you specify no target on the command line, make uses the first target defined in
makefile.
A target has no makefile or if it has no rule, make tries to drive a rule by
each of the following methods, until a suitable rule is found. Each method is
desescribed under “Reading Makefiles and the Environment” on page 789.

- 1. Pattern matching rules.
- 2. Implicit rules read from a user-supplied makefile.
- 3. Standard implicit rules (also known as suffix rules), typically read in the file
/usr/share/lib/make/make.rules.
- 4. SCCS retrieval. make retrieves the most recent version from the SCCS history file
(if any). See the description of the .SCCS_GET: special-function target for details.
- 5. The rule from the .DEFAULT: target entry if there is an entry in the
makefile.
- 6. If the target has no makeentry for a target, and if no rule can be derived for
building, and if no file by name is present, make issues an error message and halts.
