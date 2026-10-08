# mailx, mail, Mail 773

file [file]

folder [file]

Quit from the current file of messages, and read in the specified file.
The following special characters are recognized when used as file names.
% is the current mailbox.
%user is the mailbox for user.
# is the previous mail file.
+file is the named file in the folder directory (listed in the folder variable).

With no arguments, print the name of the current mail file and the number of messages and characters it contains.

+   folders: Print the names of the files in the directory set by the folder variable ("Internal Variables" on page 781).

+   followup [message]: Respond to a message, recording the response in a file whose name is derived from the author of the message. Override the record variable if set. If the replyall variable is set, reverse the actions of followup and followup. See also the followup, Save, and Copy commands, outfolder in "Internal Variables" on page 781, and "Starting Mail" on page 769.

+   from [message-list]: Respond to the first message in the message-list, sending the message to the author of each message in the message-list. Using the subject line from the first message, record the response in a file whose name is derived from the author of the first message. If the replyall variable is set, reverse the actions of followup and followup. See also the followup, Save, and Copy commands, outfolder in "Internal Variables" on page 781, and "Starting Mail" on page 769.

+   group alias name... Print the header summary for the specified messages. If you specify messages, print the header summary for the current message.

+   alias name... Declare an alias for the given names. The names are substituted when used as a recipient. Useful in the mailrc file.

+   headers [message]: Print the page of headers that include the specified file. The screen variable sets the number of headers per page (see "Internal Variables" on page 781). Also see the z command.