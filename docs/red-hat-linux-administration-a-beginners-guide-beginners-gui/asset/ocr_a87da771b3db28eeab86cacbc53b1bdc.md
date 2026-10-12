The Simple Mail Transfer Protocol (SMTP) is the accepted standard for mail transport across the Internet. Anyone who wants to have a mail server capable of sending and receiving mail across the Internet must be able to support it. Many internal networks have also taken to using SMTP for their private mail services because of its platform independence and availability across all popular operating systems.

In this module, we’ll first discuss the mechanics of SMTP as a protocol and its relationship to other mail-related protocols, such as the Post Office Protocol (POP) and the Internet Message Access Protocol (IMAP). Then we’ll discuss the Internet’s most popular mail server, Sendmail, as well as one of the more popular alternatives, Postfix. As part of our discussion, we’ll go over several popular configurations and conclude with some references to where you can get more information.

# 13.1 **Discovering the Mechanics of SMTP**

The SMTP protocol defines the method by which mail is sent from one host to another. That’s it. It does not define how the mail should be stored. It does not define how the mail should be picked up or displayed by the recipient. Nothing.

SMTP’s strength is its simplicity, and that is due to the dynamic nature of networks during the early 1980s. (The SMTP protocol was originally defined in 1982.) People were linking networks together with everything short of bubble gum and glue. SMTP was the first mail standard that was independent of the transport mechanism. This meant that people using TCP/IP networks could use the same format to send a message as someone using some other networking protocol.

SMTP is also independent of operating systems, which means each system can use its own style of storing mail without worrying about how senders of messages store their mail. You can draw parallels to how the phone system works: each phone service provider has its own independent accounting system; however, they all have agreed on a standard way to link their networks together so that calls can go from one network to another transparently.

# **Rudimentary SMTP Details**

Ever had a “friend” who sent you an e-mail on behalf of some government agency informing you that you owe taxes from the previous year, plus additional penalties? Somehow a message like this ends up in a lot of people’s mailboxes around April 1, better known as April Fool’s Day. Well, guess what? I’m going to show you how they did it. Even more fun, how you can do it yourself. (Not that I would advocate such behavior, of course.)

The purpose of this example is to show how the SMTP protocol sends a message from one host to another. After all, more important than learning how to forge an e-mail is learning how to troubleshoot mail-related problems. So in this example, you are acting as the sending host, and whichever machine you connect to is the receiving host.