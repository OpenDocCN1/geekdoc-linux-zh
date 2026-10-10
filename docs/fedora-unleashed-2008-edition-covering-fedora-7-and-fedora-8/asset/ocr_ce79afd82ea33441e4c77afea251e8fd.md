# # CHAPTER 21
# Handling Electronic Mail

E mail is still the dominant form of communication over the Internet. It is fast, free, and very easy to use. However, much of what goes on behind the scenes is extremely complicated and would appear scary to anyone who does not know much about how email is handled. Fedora comes equipped with a number of powerful applications to help you build anything from a small email server right through to large servers handling thousands of messages.

This chapter shows you how to configure Fedora to act as an email server. We look at the options available in Fedora, as well as the pros and cons of each one. You will also learn how mail is handled in Linux, and to a lesser extent, UNIX.

# ## How Email Is Sent and Received

Email is transmitted as plain text across networks around the world using *SMTP* (*Simple Mail Transfer Protocol*). As the name implies, the protocol itself is fairly basic, and it has been extended to add further authentication and error reporting/messaging to satisfy the growing demands of modern email. *Mail transfer agents*, or *MTAs*, work in the background, transferring email from server to server, allowing emails to be sent all over the world. You might have come across such *MIA* software such as Sendmail, Postfix, Fetchmail, Exim, or Qmail.

SMTP enables each computer through which the email passes to forward it in the right direction to the final destination. When you consider that there are millions of email servers across the world, you have to marvel at how simple it all seems.

# IN THIS CHAPTER

+   How Email Is Sent and Received
+   Basic Sendmail Configuration and Operation
+   Introducing Postfix
+   Using Fetchmail to Retrieve Mail
+   Choosing a Mail Delivery Agent
+   Mail Daemons
+   Alternatives to Microsoft Exchange Server
+   Reference