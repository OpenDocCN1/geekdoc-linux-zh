# mail

**Purpose:** Send email to local and remote users.

**Usage syntax:** `mail [OPTIONS] [ADDRESS]`

![](bbox=[0.13, 0.23, 0.96, 0.29])

The **mail** command sends email messages. In the above example, a new email message is created and addressed to the specified recipient. After pressing enter, the mail client will prompt you for a subject for the message. Pressing enter again will start the body of the message. Pressing **CTRL + D** exits the mail client and sends the message.

> **Tip** Press **CTRL + C** *twice* to cancel editing and discard a mail message (without sending).

A text file can be substituted for the body of an email message. In the next example, the text in the `message.txt` file will be sent as the body of the message.

![](bbox=[0.13, 0.63, 0.92, 0.66])

Common usage examples:

+   - `mail` Check for new email
+   - `mail [ADDRESS]` Start a new message to the specified address
+   - `mail [ADDRESS] < [FILE]` Use the specified file as the message body
+   - `mail -s "[SUBJECT]" \ [ADDRESS]` Specify a message subject on the command line