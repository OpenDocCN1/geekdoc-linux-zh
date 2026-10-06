to your message; and Subject:, for entering the subject of your message. After completing the fields in the header, you can compose your mail message using the built-in pine editor. (Help is available to learn the editor commands.)

If you are in the middle of composing a message and to finish it later, you can select Postpone. The pine utility stores the message in the folder named postponed-msgs, and the next time you run pine, it gives you the opportunity to continue with the postponed message.

# Reading Messages

If you simply want to read your mail, the easiest way is to use the -i option on the command line. This option takes you directly to the Message Index screen (Figure 3-19 on page 92), where a list of message headers is displayed. The highlighted message is the current message; you can highlight any other message by using the control characters in the screen menu.

Another way to read messages in pine is to select Message Index from the Main menu. This is appropriate if you plan to remain in the mail after reading your incoming messages.

By default each message header contains the following fields:

| flags | message-# | date-sent | from-name | size | [subject] |
|---|---|---|---|---||
| A | | | | You have replied to the mail message. |
| D | | | | You have marked the message for deletion. |
| N | | | | The message is new. |
| + | | | | The message was sent directly to you (that is, not, a carbon copy). | |
| * | | | | You have marked the message as important. |

The first field lists the possible flags for each message (Table III-26).

Once you have read a mail message, you can reply to the message, forward it to another person, save it in a folder, or export to a file. If you do not to keep a message, you can also select Delete to mark the message for deletion; the message is not deleted until you give the Expunge command or terminate your pine session. Exporting a message to a file automatically marks that message for deletion. To mark a message as important (*), set the pine variable enable-flag-cmd.