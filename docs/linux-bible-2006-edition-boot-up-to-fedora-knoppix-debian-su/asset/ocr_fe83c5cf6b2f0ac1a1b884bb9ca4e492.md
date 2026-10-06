# 674 Part V ♦ Running Servers

+   * **Local IPC — Inter-process communications are often used instead of SMTP when transferring a message between programs within a system.

Upon receiving a message, the MTA places it in a queue to be processed by MDA (Mail Delivery Agent). Mail Delivery Agents come into two varieties:

+   * **Local MDAs**, which deliver messages to mailboxes on the local server. Simple versions copy messages directly to a specified mailbox, while complex implementations can alter delivery parameters based on user-specified rules.

+   * **Remote MDAs**, which deliver messages over the network to remote servers. Full remote MDAs use DNS (Domain Name System) to determine the exchange hosts for recipient addresses and to deliver the best one for each. Simple remote MDAs (sometimes called "null clients") forward messages to a central server to continue the process. Most remote MDAs are capable of both method and will act as the administrator that performs the configuration.

![](bbox=[0.117, 0.423, 0.176, 0.513])

You will see then the term MTA in reference to the software that performs both MTA and MDA functions. This is a carry-over from older designs that did not separate the functions and is still fairly accurate the fact that most server implementations include a minimum of an MTA, remote MDA, and basic local MDA.

When a message reaches its destination server, it is written to the mailbox by the local MDA. From that point, the message can be viewed by the user using one of three methods:

+   * **Direct access to the mailbox** — An MUA (Mail User Agent) with access to the mailbox file, directly or through a network file system, can read messages from the disk and display them for the user. This is generally a console or Web mail application running on the server.

+   * **Downloaded to a workstation for local viewing** — Most users use POP3 (Post Office Protocol, version 3) to download messages to their local computer and view them in applications such as Evolution or Balsa. By default, messages are removed from the server during this process (similar to when you get your "snail mail" from the mailbox).

+   * **Accessed intermittently over the network** — Most clients also support viewing messages while they are still on the server, through IMAP (Internet Message Access Protocol). Unlike POP3, this protocol enables users to access multiple folders on their servers and allows them to access their messages from anywhere. However, this also creates a heavier burden on the server because it must process (and store) everything the user decides to keep. Most