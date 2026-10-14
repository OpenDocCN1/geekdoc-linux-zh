# FORWARD AND BOUNCE

The F command lets you forward messages to other users. The message composition screen appears as usual, with the forwarded message pasted into the message text area. You can add your own comments before sending.

The B command will “bounce” a message to another user with no opportunity to add comments. If the recipient’s mail system complies with standards, it will appear as if the message came from the original sender— not from you. This is handy when you get mail that was obviously meant for someone else and you want to quietly redirect it.

# EXPORT AND PIPE

The E command will export a message to a file in your home directory. This is useful if someone sends you a file that you want to save and edit, or if you receive a uencoded or encrypted message. (See Chapter 11, “Compression, Encoding, and Encryption,” for more on decoding and decryption.)

The | (vertical bar) command will pipe a message directly to any command or program. For example, you could use this feature to pipe a message to a program that strips off mail headers and formats notes for printing.

# ATTACHMENTS

Pine has excellent support for attached files. You can attach a binary file such as a program, image, or word processor document to an outgoing message using the CTRL-J command while the cursor is on the Attachment: line in the message composition screen. Pine encodes the attached file using MIME (Multi-purpose Internet Mail Enhancements), which is a widely used standard understood by most modern email programs.

Pine can also decode incoming MIME-attached files and either save them to disk or automatically launch the appropriate viewer tools. I used Pine to send Microsoft Word files back and forth to my publisher in the course of writing this book.

# ROLES

Pine allows you to play different roles, depending on who you are replying to. For example, if you are replying to a message addressed to