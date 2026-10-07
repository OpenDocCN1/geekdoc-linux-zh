# Understanding E-Mail Protocols

The simplest e-mail exchange between computers involves just two computers and a single protocol (probably SMTP). In this scenario, one composes an e-mail message and issues a command that causes the e-mail software to connect to the destination system and transmit the message. The recipient computer then holds the message in a local mail queue, and the addresse reads the message using a mail program on the recipient computer.

Most mail transfers on the Internet today are more complex, however. They typically involve several transfers, which are illustrated in Figure 17.1. These steps are as follows:

+   1. The sender composes a message using an MUA on one computer (let's call it frank@example.com). Depending on the MUA, the mail may be sent immediately or queued locally. A recipient address (let's susan@express.gov) is included in the message.

+   2. At some point, franklin connects to a mail server for its domain (let's call osgood.example.com) and sends the e-mail. In this transfer, franklin uses SMTP and functions as a client to osgood's server.

+   3. Unless the recipient's local is local, osgood uses the Domain Name System (DNS) to look up the computer that functions as the mail server for the recipient domain (express.gov). This may be a computer that goes by the same name, or it may be a different computer (such as pony.express.gov).

+   4. Once osgood has the address of the recipient system, osgood connects to that system using SMTP and transfers the e-mail. In this transfer, unlike in step 2, osgood is the client; pony.express is the server.

+   5. pony goes into a queue on a railroad, associated with the recipient (susan). Sooner or later, susan uses another computer (say, air.express.gov) to connect to railroad and retrieve mail. This transfer is likely to use POP or IMAP. Here, railroad is the server, air is the client.

+   6. The message goes into a queue on a railroad, associated with the recipient (susan). Sooner or later, susan uses another computer (say, air.express.gov) to connect to railroad and retrieve mail. This transfer is likely to use POP or IMAP. Here, railroad is the server, air is the client.

+   7. susan reads her e-mail on air, using an MUA. If she wants to reply, she can do so, initiating a series of actions similar to those outlined here; The e-mail might not pass through the same computers, though; an organization can configure different systems to function as incoming and outgoing mail servers.

The details of an e-mail transfer may range from a simple two-computer situation up to the full set of steps described above, and potentially even more. Precisely what operations

![](bbox=[0.935, 0.715, 0.985, 0.835])