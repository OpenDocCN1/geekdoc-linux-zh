d [msg-list] delete Deletes the messages in the msg-list from your mailbox. Without msg-list it deletes the current message.

or x Exits from mail without changing your mailbox. If you deleted any messages during this session with mail, they are not removed from your mailbox.

h header Displays a list of headers. Refer to the z command (following) if you want to scroll the list of headers.

m name Sends a message to name. Using this command is similar to calling mail with name from the command line.

p [msg-list] preserve preserve Preserves messages in the msg-list in your mailbox. Use this command after you have read a message but do not want to remove it from your mailbox. Refer to the q command.

q quit Exits from mail, saving in your mbox files that you did and not delete and leaving in your mailbox messages that you have not read. You can use the pre command to force mail to leave a message in your mailbox even though you have read it.

r [message] reply Replies to a message. This command copies the subject line of the message and addresses a reply to the person who sent you the message. Everyone gets a copy of the original message also gets a copy of the new message. The r command puts mail in Input mode so you can compose a message.

R [message] reply Replies to a message. This command is like the r command, but it sends a reply only to the person who sent you the message.

s [msg-list, filename] save Saves the messages in msg-list in filename. When you use this command, mail does not save msg-list in your mbox when you exit from mail with the q command. This command appends to filename if it already exists; otherwise, it creates it.

set See the introduction to the following section, "The Mail Environment," for a description of this command. You can give the set command in response to a mail prompt, set is typically used in .mailrc.

t [msg-list] Displays the messages in the msg-list. This command is a synonym for p.

top [msg-list] Displays the top few lines of the specified messages.

u [msg-list] undelete Restores the specified messages. You can restore a deleted message only if you have not quit from mail since you deleted the message.

unset Like the command set, this command modifies the mail environment. This command can be given in response to the mail prompt to remove the value of an environment variable, but it is usually given in .mailrc. See the following section for an envi.