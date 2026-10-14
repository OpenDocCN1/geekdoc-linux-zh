# 32.2.4 Replying to Mail

Use reply (or just r) to reply to a message. This makes a new mail message, sent from you to the sender and all recipients of a mail in your inbox. With no arguments, it replies to the current message, such as the last message you read; you can also give a message number as an argument to reply to that message number.

⇒ Here are two ways to use this.

+   - To reply to the current message, type:
+     & reply [RET]
+   - To reply to message number 14, type:
+     & r 14 [RET]

When you reply to a mail, use the keyboard commands for composing your message as described in Recipe 32.1.5 [Composing Mail], page 616.

# 32.2.5 Saving Mail to a File

Use save (or just s) to save a message to a file. By default, it works on the current message, but you can specify a number or a range, as well. Give the name of the file to save to as an argument; if the file exists, the mail will be appended.

⇒ Here are some ways to use this.

+   - To save the current message to a new file called saved-mail, type:
+     & s saved-mail [RET]
+   - To save messages 18 through 24 to a new file called conference-reflections.2004, type:
+     & save 18-24 conference-reflections.2004 [RET]
+   - To save messages two through seven to a new file called correspondence, type:
+     & save 2-7 correspondence [RET]
+   - To save the current message to a new file called conference-ideas, type:
+     & save conference-ideas [RET]
+   - To append message 214 to an existing file called saved-mail, type:
+     & save 214 saved-mail [RET]