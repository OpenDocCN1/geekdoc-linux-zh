# ### Demonstrating the Sendmail MDA

To summarize, so far we’ve done two things:

+   - We’ve set up the Sendmail application as a mail server, capable of listening for incoming mail messages on 127.0.0.1, and filtering those messages into the correct mailbox so that the intended recipient can read them
+   - We’ve created some users, configure their mailboxes, and set up each user so that it can use the Evolution application as a mail client (to enable them to send messages and view the messages they’ve received

In a moment, we can begin to test all this – for example, by logging in as *kapils*, sending a message to *markm*, and then logging in as *mark* to check that the mail message safely arrived.

# ### Starting the POP3 Service

There’s one thing we must do before we can use Evolution to send a message: we must start the POP3 service. You can do this from the **Service Configuration** GUI (**Main Menu | System Settings | Server Settings | Services**). First, check the checkbox next to the **ipop3** entry in the list, and then check that the **xinetd** service is running.

> The **ipop3** service runs under the **xinetd** service, so if **xinetd** service is running and the **ipop3** service is enabled then the **ipop3** service will run too.

# ### Sending Mails

You’ve done the hard work; this last part is easy! Log onto one of your accounts (say, *kapils*), and launch the Evolution application by selecting **Main Menu | Internet | Evolution Email**. Then select **File | New | Mail Message**, and write a mail message to another account on the system:

![](bbox=[0.22, 0.58, 0.8, 0.83])

Click the **Send** button to send the message. You may be asked to provide your POP password; use the account’s system password.