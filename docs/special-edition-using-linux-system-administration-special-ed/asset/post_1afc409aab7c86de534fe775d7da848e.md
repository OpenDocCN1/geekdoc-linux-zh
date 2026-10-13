
## TILDE/ESCAPES

A summary of the tilde escapes follows. These are used when composing messages to perform special functions. Tilde escapes are only recognized at the beginning of lines. The name *tilde escape* is somewhat of a misnomer because the actual escape character can be set by the option `escape`.

- `~! command`—Execute the indicated shell command, and then return to the message.
- `~b name ...`—Add the given names to the list of carbon copy recipients but do not make the names visible in the Cc: line ("blind" carbon copy).
- `~c name ...`—Add the given names to the list of carbon copy recipients.
- `~d`—Read the file `dead.letter` from your home directory into the message.
- `~e`—Invoke the text editor on the message collected so far. After the editing session is finished, you can continue appending text to the message.
- `~f messages`—Read the named messages into the message being sent. If no messages are specified, read in the current message. Message headers currently being ignored (by the ignore or retain command) are not included.
- `~F messages`—Identical to `~f` except all message headers are included.
- `~h`—Edit the message header fields by typing each one in turn and allowing the user to append text to the end or modify the field by using the current terminal erase and kill characters.
- `~m messages`—Read the named messages into the message being sent, indented by a tab or by the value of `indentprefix`. If no messages are specified, read the current message. Message headers currently being ignored (by the ignore or retain command) are not included.
- `~M messages`—Identical to `~m` except all message headers are included.
- `~p`—Print out the message collected so far, prefaced by the message header fields.
- `~q`—Abort the message being sent, copying the message to `dead.letter` in your home directory if `save` is set.
- `~r filename`—Read the named file into the message.
- `~s string`—Cause the named string to become the current subject field.
- `~t name ...`—Add the given names to the direct recipient list.
- `~v`—Invoke an alternate editor (defined by the VISUAL option) on the message collected so far. Usually, the alternate editor will be a screen editor. After you quit the editor, you can resume appending text to the end of your message.
- `~w filename`—Write the message onto the named file.
- `~| command`—Pipe the message through the command as a filter. If the command gives no output or terminates abnormally, retain the original text of the message. The command `fmt(1)` is often used as command to re-justify the message.
- `~ mail-command`—Execute the given mail command. Not all commands, however, are allowed.
- `~ string`—Insert the string of text in the message prefaced by a single `~`. If you have changed the escape character then you should double that character in order to send it.

## MAIL OPTIONS

Options are controlled through set and unset commands. Options can be either binary, in which case it is only significant to see whether they are set; or string, in which case the actual value is of interest. Binary options include the following:

- `append`—Causes messages saved in mbox to be appended to the end rather than prepended. This should always be set (perhaps in `/etc/mail.rc`).
- `ask, asksub`—Causes mail to prompt you for the subject of each message you send. If you respond with simply a newline, no subject field will be sent.
- `askcc`—Causes you to be prompted for additional carbon copy recipients at the end of each message. Responding with a newline indicates your satisfaction with the current list.
- `askbcc`—Causes you to be prompted for additional blind carbon copy recipients at the end of each message. Responding with a newline indicates your satisfaction with the current list.
- `autoprint`—Causes the delete command to behave like dp, thus, after deleting a message, the next one will be typed automatically.
- `debug`—Setting the binary option debug is the same as specifying `-d` on the command line and causes mail to output all sorts of information useful for debugging mail.
- `dot`—The binary option dot causes mail to interpret a period alone on a line as the terminator of a message you are sending.
- `hold`—This option is used to hold messages in the system mailbox by default.
- `ignore`—Causes interrupt signals from your terminal to be ignored and echoed as `@s`.
- `ignoreof`—An option related to dot is ignoreof, which makes mail refuse to accept a control-d as the end of a message. Ignoreof also applies to mail command mode.
- `metoo`—Usually, when a group is expanded that contains the sender, the sender is removed from the expansion. Setting this option causes the sender to be included in the group.
- `noheader`—Setting the option noheader is the same as giving the `-N` flag on the command line.
- `nosave`—Normally, when you abort a message with two RUBOUT (erase or delete) mail copies the partial letter to the file `dead.letter` in your home directory. Setting the binary option nosave prevents this.
- `replyall`—Reverses the sense of reply and Reply commands.
- `quiet`—Suppresses the printing of the version when first invoked.
- **searchedheaders**—If this option is set, a message-list specifier in the form `/x:y` will expand to all messages containing the substring `y` in the header field `x`. The `x` string search is case insensitive.
- **verbose**—Setting the option verbose is the same as using the `-v` flag on the command line. When mail runs in verbose mode, the actual delivery of messages is displayed on the user's terminal.

## OPTION STRING VALUES

- **EDITOR**—Pathname of the text editor to use in the edit command and `~e` escape. If not defined, a default editor is used.
- **LISTER**—Pathname of the directory lister to use in the folders command. Default is `/bin/ls`.
- **PAGER**—Pathname of the program to use in the more command or when crt variable is set. The default paginator more(1) is used if this option is not defined.
- **SHELL**—Pathname of the shell to use in the `!` command and the `~!` escape. A default shell is used if this option is not defined.
- **VISUAL**—Pathname of the text editor to use in the visual command and `~v` escape.
- **crt**—The valued option crt is used as a threshold to determine how long a message must be before PAGER is used to read it. If crt is set without a value, the height of the terminal screen stored in the system is used to compute the threshold (see stty(1)).
- **escape**—If defined, the first character of this option gives the character to use in the place of `~` to denote escapes.
- **folder**—The name of the directory to use for storing folders of messages. If this name begins with a `/`, mail considers it to be an absolute pathname; otherwise, the folder directory is found relative to your home directory.
- **MBOX**—The name of the mbox file. It can be the name of a folder. The default is mbox in the user's home directory.
- **record**—If defined, gives the pathname of the file used to record all outgoing mail. If not defined, outgoing mail is not so saved.
- **indentprefix**—String used by the `~m` tilde escape for indenting messages, in place of the normal tab character (`^I`). Be sure to quote the value if it contains spaces or tabs.
- **toplines**—If defined, gives the number of lines of a message to be printed out with the `top` command; normally, the first five lines are printed.

## ENVIRONMENT

mail utilizes the HOME and USER environment variables.

## FILES

- `/var/spool/mail/*`—Post office
- `~/mbox`—User’s old mail
- `~/.mailrc`—File giving initial mail commands
- `/tmp/*`—Temporary files
- `/usr/lib/mail.*.help`—Help files
- `/etc/mail.rc`—System initialization file

## SEE ALSO

fmt(1), newaliases(1), vacation(1), aliases(5), mailaddr(7), sendmail(8) and 'The Mail Reference Manual'.

## HISTORY

A mail command appeared in AT&T System v6. This man page is derived from 'The Mail Reference Manual' originally written by Kurt Shoens.

## BUGS

Some flags are not documented here. Most are not useful to the general user.

## MAN

### NAME

`man`—Format and display the online manual pages.

`manpath`—Determine user's search path for man pages.

### SYNOPSIS

```
man [-acdfhKkTwW] [-m system] [-p string] [-C config_file] [-M path] [-P pager]
↪ [-S section_list] [section] name ...
```

### DESCRIPTION

man formats and displays the online manual pages. This version knows about the MANPATH and (MAN)PAGER environment variables, so you can have your own set(s) of personal man pages and choose whatever program you want to display the formatted pages. If section is specified, man only looks in that section of the manual. You can also specify the order to search the sections for entries and which preprocessors to run on the source files using command-line options or environment variables. If name contains a / then it is first tried as a filename, so that you can do man ./foo.5 or even man /cd/foo/bar.1.gz.

### OPTIONS

- `-C config_file`—Specify the man.conf file to use; the default is /etc/man.config. (See man.conf(5).)
