
# vacation

# 1513

You have a message file in /export/home/winsor/.vacation.msg.
Would you like to see it? n
Would you like to edit it? n
You have a .forward file in your home directory containing:
Winsor, /usr/bin/vacation winsor
Would you like to remove it and disable the vacation feature? y
Back to normal reception of mail.

# Additional Configuration

Starting with the Solaris 8 release, vacation provides the -a, -f, -j, -m, -s, and -t
configuration options that are not part of the installation. See "Options."

![](img/185d23104c385dfb6a62d64cc96b8997_1542_0.png)

# Options

- -I

Clear the .vacation.pag and .vacation.dir files. If you do not
specific the flag and provide a username argument, vacation reads
the first line from the standard input (for a From line, no colon). If
absent, it produces an error message.

Use the following configuration options on the .forward file, on the command
line. For example, \username, "/usr/bin/vacation -tim username" repeats replies
to the sender every minute.

- -a alias

Indicate that alias is one of the valid aliases for the user running
vacation so that mail addressed to that alias generates a reply.

- -f file

Use instead of .vacation as the basename for the database file.
Do check whether the recipient appears in the To: or Cc: line.

![](img/185d23104c385dfb6a62d64cc96b8997_1542_1.png)

- -j

- -m file

Use instead of .vacation.msg as the message to send for the
reply.

![](img/185d23104c385dfb6a62d64cc96b8997_1542_2.png)

- -s sender

Reply to sender instead of the value read from the UNIX line: of
the incoming message.

Change the interval between repeat replies to the same sender.
default is 1 week. A trailing s, m, h, d, or w to seconds, minutes,
hours, days, or weeks.

# Usage

The .vacation.msg file should include a header with at least a Subject: line.
it should not include a From: or a To line. For example:

Subject: I am on vacation
am on vacation until March 8. If you have an urgent issue, please
contact my manager.
--Janice

If you include the string SUBJECT in the .vacation.msg file, it is replaced with
the subject of the original message when the reply is sent. For example, the following
.vacation.msg file includes the subject of the message in the reply.

Subject: I am on vacation
I on vacation until March 8.

![](img/185d23104c385dfb6a62d64cc96b8997_1542_4.png)

# 1514

I will read your mail regarding "$SUBJECT" when I return. If you have an urgent issue, please contact my manager.
--Janice

# Files

~/.forward

Contains a line of the following format that is used to forward the message in the .vacation.msg file. \username, \|/usr/bin/vacation username

~/.vacation.msg

Contains the message that is sent in response to incoming mail.

~/.vacation.pag

Stores a list of senders when vacation is enabled. You cannot view this file directly with a text editor.

~/.vacation.dir

Stores a list of senders when vacation is enabled. You cannot view this file directly with a text editor.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNWcsu |

# See Also

vi(1), sendmail(1M), getusershell(3C), dbm(3UCB), aliases(4), shells(4), attributes(5)

# val — Validate an SCCS File

# Synopsis

```
/usr/ccs/bin/val [-s] [-m name] [-rsid] [-y type] s.filename.
```

# Description

See sccs-val(1).

# vax 1515

# vax — Get Processor Type Truth Value

# Synopsis

/usr/bin/vax

# Description

See machidi(1).

# vc — Version Control

# Synopsis

```
/usr/ccs/bin/vc [-a] [-t] [-cchar] [-s] [keyword=value... keyword=value]
```

# Description

Note — This command is obsolete and will be removed in the next release.

The vc copies lines from the standard input to the standard output, using arguments and control statements from the standard input. In a copy operation, user-declared keywords can be replaced by their string value when they appear in plain text and/or control statements.

The copying of lines from the standard input to the standard output is conditional, based on (in control statements) of keyword values specified in control statements or vc control commands.

A control statement is a single line beginning with a control character, except as modified by the -t key. The default control character is colon (:) as modified by the -c key. Input lines with a backslash (\ followed by a control character are not control lines and are copied to the standard output with the backslash removed. Lines beginning with a backslash followed by a noncontrol character are copied in their entirety.

A keyword is composed of nine or fewer alphanumerics; the first must be alphabetic. A value is any ASCII text that can be created with etc; a numeric value which is an unsigned string of digits. Keyword values may not contain blanks or Tabs. Keywords are replaced whenever a keyword surrounded by control characters is encountered in a version control statement. The -a key letter forces replacement of keywords in all lines of text. You can include an unintended control character in a value by replacing with \. If a literal \ is desired, you must precede it with \.

# Options

- -a Force replacement of keywords surrounded by control characters with their assigned value in all text lines and not just in vc statements.

- -cchar Specify a control character to be used in place of the colon (:) default.

# 1516

- -s Silence warning messages (not error) that are normally printed on the
diagnostic output.

- -t Ignore all characters from the beginning of a line up to including
the Tab character for the purpose of detecting a control statement.
If a control statement is found, discard all characters up to
including the Tab.

vc recognizes the following version control statements.
:asg keyword=value

Assign values to keywords. An asg statement overrides the assignment
for the corresponding keyword on the vc command line and all previous
asg statements for that keyword. Keywords that are declared but are
not assigned values have null values.

:dcl keyword, ..., keyword
Declare keywords. All keywords must be declared.

:if condition
:end Skip lines of the standard input. If condition is true, copy all lines
between the statement and the matching statement to the
standard output. If condition is false, discard all intervening lines,
including control statements. Note that intervening statements and
matching statements are recognized.

The syntax of condition is:

```
cond ::= "not" <or>
or ::= <and> | "||" <and>
and ::= <exp> | "&&" <exp>
exp ::= "(" <cond> ")" | <op> <value>
op ::= "=" | "!=" | "<" | ">"
value ::= ASCII string
```

The available operators and their meanings are:

- = Equal.
- != Not equal.
- & AND.
- | OR.
- > Greater than.
- < Less than.

You can use not only after an if. When not is present, it inverts
value of the entity. > and < operate only on integer values (for example, :02 > 12 is false).
All other operators take strings as arguments (for example, :12 != 12 is true).

The precedence of the operators (from highest to lowest) is:

- = ! >=
- & |

You can use parentheses to alter the order of precedence.
Separate values from operators or parentheses by at least one blank or Tab.

```
::text    Replace keywords on lines that are copied to the standard output.
Remove the leading control characters and replace keywords
surrounded by control characters in text with their value before
copying the line to the output. This action is independent of the -a
key letter.
```

```
:on      Turn on or off keyword replacement on all lines.
:off     Change the control character to char.
```

```
:msg message    Print message on the diagnostic output.
```

```
:err message    Print message followed by ERROR: err statement on line .. (915)
on the diagnostic output. Halt execution, and return an exit code of 1.```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| :--- | :--- |
| Availability | SUNwprot |

# See Also

edit(1), attributes(5)

# edit – Screen-Oriented Visual Display Editor Based on ex

# Synopsis

```
/usr/bin/edit - [-s] [-l] [-L] [-R] [-r [filename]] [-S] [-t tag]
[-v] [-V] [-x] [-wn] [-C] +command [-c command] filename...
/usr/xpg4/bin/edit - [-s] [-l] [-L] [-R] [-r [filename]] [-S]
[-t tag] [-v] [-V] [-wn] [-C] +command [-c command] filename...
/usr/bin/edit - [-s] [-l] [-L] [-R] [-r [filename]] [-t tag][-
[-v] [-V] [-x] [-wn] +command [-c command] filename...
/usr/xpg4/bin/edit - [-s] [-l] [-L] [-R] [-r [filename]] [-t tag]
[-v] [-V] [-x] [-wn] * help
```
