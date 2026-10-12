2. Next, type **hello** followed by the name of the server you're pretending to be. Using the host name of the machine you're working on is probably not a bad idea. Whether any checking is done on this value will depend entirely on the paranoia of the server you're connecting to. If you use the name of the machine you're connecting from, you shouldn't have any problems.
`helo my-hostname.my-domain-name.com`

3. Enter the **mail from:** now. Remember from the previous section that this identifies the sender of the message. If you're dealing with a properly paranoid mail server, this value should at least be a valid e-mail address. You can use your own e-mail address here.
`mail from: myself@my-domain-name.com`

4. Now enter the e-mail address of the recipient, after the **rcpt to:** command. This will again be your own e-mail address for this test.
`rcpt to: myself@my-domain-name.com`

5. Next comes the **data** command:
`data`

6. Finally we get to the meat of the e-mail. If you want this message to actually be readable with standard mail software, you'll need to have proper headers. Start with entering the simple headers shown here:
`From: myself@my-domain-name.com`
`To: myself@my-domain-name.com`
`Subject: Project 13-1`

7. Enter a blank line to separate the headers from the body of the message.

8. Type any message body that you like; then enter a period on a line by itself to end the message.
`This is really cool. I can test my mail servers just like this.`
`.`

8. Type **quit** to close the connection.

9. Fire up your favorite mail reader and see if your message arrived.

# Project Summary

This project not only gave you a real-world example of an SMTP session, but illustrates a simple method for testing your mail servers if you're experiencing problems. Hopefully you'll have the restraint necessary not to misuse this ability next April first.