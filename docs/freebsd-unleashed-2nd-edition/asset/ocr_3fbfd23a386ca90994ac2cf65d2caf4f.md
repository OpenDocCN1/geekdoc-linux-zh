# Mail Transfer Agents (MTAs) and Mail User Agents (MUAs)

The schematic diagram for an e-mail message's path from one person to another is shown in Figure 24.1. Whether the user is on a dial-up connection from a remote site or sitting at the console on the mail server itself, the path the message takes is the same: From the user's input into the Mail User Agent (commonly known as an *e-mail client program*), the message moves into the sending SMTP server's message queue, where the Mail Transfer Agent (MTA; for example, Sendmail) pulls it out as soon as a connection to the receiving SMTP server becomes available and transmits it. (Because this process transmits a message that doesn't originate or terminate on the SMTP server machine itself, this step is known as *relaying*.) On the remote system, the MTA places the received message into the recipient's mailbox, where it can be read online with a server-side Mail User Agent (MUA) or downloaded to a client-side MUA through POP3.

![](bbox=[0.25, 0.38, 0.85, 0.73])

**FIGURE 24.1** Diagram of an e-mail message's path from one user to another, showing the roles of MUAs and MTAs.

As a FreeBSD administrator, you'll be interested in the way Sendmail operates as an MTA, both in sender (relay) and receiver roles. This section also discusses MUA programs—both the local kind that users run on the FreeBSD machine and the remote kind that operate by uploading and downloading messages. You learn how these programs interact with the “holding areas” of the MTAs: the message queue and the user mailboxes.