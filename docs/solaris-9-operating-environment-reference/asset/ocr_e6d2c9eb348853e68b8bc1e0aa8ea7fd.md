# mailx, mail, Mail 777

Save [message-list]

Save the specified messages in a file whose name is derived from the author of the first message. The name of the file is taken to be the author's name with all network addressing stripped off. See also the Copy, followup, and Followup commands, and outfolder in "Internal Variables" on page 781.

save [file]

save [message-list] file\Save the specified messages in the given file. Create the file if it does not exist. The file defaults to mbox. Delete the message from the mailbox when mailx terminates keepsave is set (see also "Internal Variables" on page 781 and the exit and quit commands).

set

set variable
set variable=string

Define a variable. To assign a value to variable, separate the variable name from the value by an equal sign (=). Do not follow the equal sign with a space. You can give a null, string, or numeric value. To embed characters within a value, enclose the value in quotes.

With no arguments, set displays all defined variables and any values they might have. See "Internal Variables" on page 781 for a description of all predefined mail variables.

shell
Invoke an interactive shell. See also SHELL in "Environment Variables" on page 785.

size [message-list]

Print the size in characters of the specified messages.

source file
Read commands from the given file and return to command mode.

top [message-list]

Print the top few lines of the specified messages. If the toplines variable is set, take it as the number of lines to print (see "Internal Variables" on page 781). The default is 5.

touch [message-list]

Print the specified messages. If any message in message-list is not specifically saved in a file, on normal termination, put it in the mbox or in the file specified in the MBOX environment variable. See exit and quit.

Type [message-list]
Print [message-list]

Print the specified messages on the screen, including all header fields. Override suppression of fields by the ignore command.