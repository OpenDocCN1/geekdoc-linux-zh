# How Email Is Sent and Received

smtp.lion.org  smtp.cheetah.org

![](bbox=[0.31157, 0.11932999999999999, 0.68843, 0.25335])

**FIGURE 19.1** A simple example of how email is successfully processed and sent to its destination.

+   1. user1@lion.org composes and sends an email message to user2@cheetah.org.
2. The MTA at lion.org receives user1's email message and queues it for delivery behind any other messages that are also waiting to go out.

+   3. The MTA at lion.org contacts the MTA at cheetah.org on port 25. After cheetah acknowledges the connection, the MTA at lion.org sends the mail message. After cheetah.org accepts and acknowledges receipt of the message, the connection is closed.
4. The MTA at cheetah.org places the mail message into user2's incoming mailbox, user2 is notified that she has new the mail the next time she goes on.

Of course, several things can go wrong during this process:
If user2 doesn't exist at cheetah.org? In this case, the MTA at cheetah.org will reject the email and notify the MTA at lion.org of the problem. The MTA at lion.org will then generate an email message and send it to user1@lion.org, informing her that no user2 exists at cheetah.org (or perhaps just silently discard the message and give the sender no indication of the problem, depending on how the server is configured).
What happens if cheetah.org doesn't respond to lion.org's connection attempts? (Perhaps the server is down for maintenance.) The MTA at lion.org notifies the server that the initial delivery attempt has failed. Further attempts will be made at intervals decided by server administrator until the deadline is reached, and the sender be notified that the mail is undeliverable.