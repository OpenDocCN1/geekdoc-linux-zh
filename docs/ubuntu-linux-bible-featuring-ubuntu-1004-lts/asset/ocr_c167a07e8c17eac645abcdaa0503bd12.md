# Chapter 7: Managing E-Mail and Personal Information with Evolution

FIGURE 7-6
Options for handling incoming mail from a POP server

![](bbox=[0.068, 0.166, 0.458, 0.506])

Many of the options for interacting with an incoming mail server are specific to the type of server that you're connecting to. For example, Figure 7-7 shows the configuration options available when communicating with an IMAP server.

There are many more options for configuring Evolution's interaction with an IMAP server than with a POP server. Because IMAP servers maintain a master repository for your e-mail, Evolution's IMAP Configuration panel offers options for how to connect to the server (such as through a custom command that provides a secure tunnel), how to interact with the mail folders on the IMAP server (both your personal folder and public ones to which you may have access), whether to synchronize your local mail folder with those on the server (giving you a local copy of all your mail), and whether mail filters and general junk mail (spam) processing should occur against your master mailboxes or I'll discuss mail filters and junk mail handling in the section "Filtering Incoming Mail" in this chapter. If you're configuring Evolution to interact with an IMAP server, I suggest activating both the "Apply filters" and "Check new messages" options for now. You can always turn them off, and selecting these options initially will ensure that Mail Filters work as expected, and will also help get rid of some of the spam that plague e-mail users today.

After you configure how Evolution interacts with your incoming mail server when you read your mail, regardless of the type of incoming mail server you're using, you need to configure how Evolution actually sends mail. Click Forward to proceed to the panel shown in Figure 7-8.