
# mailx, mail, Mail 775

more [message-list]
page [message-list]

Print the specified messages. If crt is set, page through the messages that are longer than the number of lines specified by the crt variable, using the command specified by the PAGER variable. The default command is pg(1), or if the bsdcompat variable is set, the default is more(i). See "Environment Variables" on page 785. Same as the print and type commands.

More [message-list]
Page [message-list]

Print the specified messages on the screen, including all header fields. Override suppression of fields by the ignore command. Same as the print and Type commands.

new [message-list]
new [message-list]
unread [message-list]
unread [message-list]

Mark each message in a message list as not having been read.

next [message]

Go to the next message matching message. If you do not supply message, find the next message that was not deleted or saved. If you specify a message-list, the first valid message in the list is the only one used. This command is useful for jumping to the next message from a specific user because, otherwise, the name would be taken as a command in the absence of a real command. See the discussion of message-list above for a description of possible message specifications.

pipe [message-list] [shell-command]
| [message-list] [shell-command]

Pipe the message through the given shell-command. Treat the message as if it were read. If you specify no arguments, pipe the message through the command specified by the value of the cmd variable. If the page variable is set, insert a formfeed character after each message (see "Internal Variables" on page 781).

preserve [message-list]
hold [message-list]

Preserve the specified messages in the mailbox.

print [message-list]
type [message-list]

Print the specified messages. If crt is set, page through the messages that are longer than the number of lines specified by the crt variable, using the command specified by the PAGER variable. The default command is pg(1), or if the bsdcompat variable is set, the default is more(1). See "Environment Variables" on page 785. Same as the print and page commands.

```
Print [message-list]
Type [message-list]
```

Print the specified messages on the screen, including all header fields.
Override suppression of fields by the ignore command. Same as the More and Page commands.

```
put [file]
put [message-list] file
```

Save the specified message in the given file. Use the same conventions as the print command for which header fields are ignored.

```
Put [file]
Put [message-list] file
```

Save the specified message in the given file. Override suppression of fields by the ignore command.

quit
Exit from mailx, storing messages that were read in bbox and unread as the mailbox. Delete messages that have been explicitly saved in a file unless the keepsave variable is set.

```
reply [message-list]
respond [message-list]
replysender [message-list]
```

Send a response to the author of each message in the message-list. Take the subject line from the first message. If record is set to a file, add a copy of the reply to that file. If the replyall variable is set, reverse the actions of Reply/Respond and reply/respond. replysender command is not affected by the replyall variable but sends each reply only to the sender of each message. See "Starting Mail" on page 769.

```
reply [message]
Respond [message]
replyall [message]
```

Reply to the specified message, including all other recipients of that message. If the variable record is set to a file, add a copy of the reply to that. If the replyall variable is set, reverse the actions of Reply/Respond and reply/respond. The replyall command is not affected by the replyall variable but always sends the reply to all recipients of the message. See "Starting Mail" on page 769.

retain
Add the list of header fields named to the retained list. Show only the header fields in the retain list when you run a terminal when you print a message. Suppress all other header fields. Override any list of ignored fields specified by the ignore command. You can use the Type and Print commands to print a message in its entirety. If you execute retain with no arguments, it lists the current set of retained fields.

# mailx, mail, Mail 777

Save [message-list]

Save the specified messages in a file whose name is derived from the author of the first message. The name of the file is taken to be the author's name with all network addressing stripped off. See also the Copy, followup, and Followup commands, and outfolder in "Internal Variables" on page 781.

save [file]

save [message-list] file
Save the specified messages in the given file. Create the file if it does not exist. The file defaults to mbox. Delete the message from the mailbox when mailx terminates keepsave is set (see also "Internal Variables" on page 781 and the exit and quit commands).

set

set variable
set variable=string

Define a variable. To assign a value to variable, separate the variable name from the value by an equal sign (=). Do not follow the equal sign with a space. You can give a value, string, or numeric value. To embed the value in quotes. With no arguments, set all defined variables and any values they might have. See "Internal Variables" on page 781.

shell
Invoke an interactive shell. See also SHELL in "Environment Variables" on page 785.

size [message-list]

Print the size in characters of the specified messages.

source file
Read commands from the given file and return to command mode.

top [message-list]

Print the top few lines of the specified messages. If the toplines variable is set, take it as the number of lines to print (see "Internal Variables" on page 781). The default is 5.

touch [message-list]

Print the specified messages. If any message in message-list is not saved in a file, on normal termination, put it in the mbox or in the file specified in the MBOX environment variable. See exit and quit.

Type [message-list]
Print [message-list]

Print the specified messages on the screen, including all header fields. Override suppression of fields by the ignore command.

# 778

type [message-list]
print [message-list]

Print the specified messages. If crt is set, use the command specified by the PAGER variable to page through the messages that are longer than the number of lines specified by the crt variable. The default command is pg(1).

unalias [alias]...
ungroup [alias]...

Remove the definitions of the specified aliases.

undelete [message-list]

Restore the specified deleted messages. Restore only messages deleted in the current mail session. If autoprint is set, print the last message of those restored (see "Internal Variables" on page 781).

undiscard [header-field...]
unignore [header-field...]

Remove the specified header fields from the list being ignored. If you specify no header fields, remove all header fields from the list being ignored.

unread [message-list]
Unread [message-list]

Same as the new command.

unretain [header-field...]

Remove the specified header fields from the list being retained. If you specify no header fields, remove all header fields from the list being retained.

unset variable...

Erase the specified variables. If the variable was imported from the environment (that is, an environment variable or exported shell variable), you cannot unset it from mailx.

version [message-list]

Print the current version and release date of the mailx command.

visual [message-list]

Edit the given messages with a screen editor. Put each message in a temporary file, and invoke the program named by the VISUAL variable to edit it (see "Environment Variables" on page 785). Note that the default visual editor is vi.

write [message-list] file

Write the given messages on the specified file, minus the header and trailing blank line. Otherwise, equivalent to the save command.

xit

Exit from mailx, without changing the mailbox. Save no messages in the mbox (see also quit).

exit
