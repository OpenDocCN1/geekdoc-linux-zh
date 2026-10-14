
## Customizing Your mailx Session

You can customize your mailx session permanently by including in your .mailrc file any of the settings described in Table D-1. See the unset command in Appendix F for information about temporary settings.

### Table D-1: Variables for Customizing Your mailx Session

| Variable | Type | Description |
|---|---|---|
| allnet | Binary | Treats all network names with the same login name the same. |
| append | Binary | Saves messages in your mbox file in the order of arrival; the earliest message is the first message in the file. When this variable is unset, messages are saved in reverse order; the first message in the file is the most recent. The mailx program runs faster if append is set. |
| ask | Binary | Prompts you for a subject line when you send a message. Enter a blank line to send a message with no subject. |
| askcc | Binary | Prompts you for carbon-copy recipients for each message you send. |
| autoprint | Binary | Automatically displays the next message when you delete the current message. When autoprint is unset, mailx does not display the next message when you delete a message. In either case, the next message becomes your new current message. |
| bang | String | Enables the special-case treatment of the exclamation point (!) in escape command lines as in vi. |
| cmd | String | Lets the user specify the default command to be used when using the vertical bar or pipe (\|) command. |
| conv | String | Lets the user specify how to convert UUCP style addresses for sendmail. |
| crt | Numeric | For use with a video display (CRT) terminal. Reads your mail one screenful at a time using the more program. The value tells mailx how many lines of the message to display before invoking the pager. For example: `set crt=20` |
| DEAD | String | Lets the user specify a different location for `dead.letter`. A dead letter will be written to `$HOME/dead.letter` by default. |
| debug | Binary | Displays debugging information. |
| dot | Binary | Interprets a period on a line by itself to be the end of a message. Do not unset `dot` and also set `ignoreeof`. |
| EDITOR | String | Specifies the pathname for the text editor to be used when you use the edit command or the `~e` escape. For example: `set EDITOR=/usr/ucb/ex`. If your terminal is a CRT terminal, you can specify a screen editor for this variable. See the VISUAL variable later in this table. |
| escape | String | Lets you specify the escape character (the character that starts an escape command when you are in the middle of writing a message). The default is the tilde (`~`). You must specify a single character. |
| excode | String | Lets the user specify the locale to be used when doing character conversion on outgoing mail messages. |
| folder | String | Specifies the directory for storing mail folders. A name beginning with a slash, such as `/usr/users/hale`, is an absolute pathname. A name without an initial slash is a pathname relative to your home directory. For example, the command `set folder=folder` indicates the directory `/usr/users/hale/folder`. |
| gonext | Binary | If set, entering a Return by itself causes the next mail message to be displayed. If not set, the current message is displayed again. |
| header | Binary | Prints the message header of messages when mailx is invoked. |
| hold | Binary | Prevents messages from being moved to your mbox file after you read them. Messages you have read are held in your system mailbox. |
| ignore | Binary | Ignores Ctrl/C interrupts, echoing them as "at" signs (@). This variable is different from the ignore command described in Appendix F. |
| ignoreeof | Binary | Ignores Ctrl/D as the end of an outgoing message. Do not set ignoreeof and also unset dot. |
| indentprefix | String | Lets the user specify a string to be inserted at the beginning of each line of text of a mail message that was included using the `~m` command. |
| keep | Binary | Lets mailx truncate your system mailbox instead of deleting it when it is empty. This is useful if you have set special permissions on your system mailbox for security reasons. If keep is unset, your system mailbox is deleted when it becomes empty; the next time it is created, you must reestablish your desired permissions. |
| keepsave | Binary | Prevents deletion of saved messages when you quit mail. Usually, the mailx program marks messages when you save them in other files or folders, and then deletes them from your system mailbox when you leave mailx. Setting keepsave makes mailx leave these messages in your system mailbox. |
| lang | String | Lets the user specify the locale to be used for displaying the mail message. |
