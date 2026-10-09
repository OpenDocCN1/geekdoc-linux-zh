Another form of data interchange is within groups. Shared messages depend on the TCP/IP protocols for broadcasting messages or isolating traffic. All computers in the same network segment can see these messages. Because routers do not pass foreign broadcast messages, the group messages are isolated in the destination segment. It tends to be more secure than the public form, but it is still subject to network snooping (within the same network segment). Intrusion is not as much of an issue because the segment typically assumes that you are among friends.

Private messages try to limit access to the information between the source and destination. They often have critical information to which external data prying can cause serious damage. Private messages require extra measures, both physical and logical, to ensure data security and integrity.

Another important message form that requires inclusion here is a special data form that distributes program execution to other sites. These commands include RPCs and direct commands (like those of `telnet`, `rlogin`, or `rsh`). The data's function demonstrates its difference from regular data. Regular data (or *inactive data*) only changes the meaning or its interpretation if corrupted. Distributed commands (or *active data*) change execution when corrupted and can even compromise host security. The Love Bug virus in Microsoft Outlook is an example of corrupted active data.

Of the different types of data interactions, active data presents the greatest security risk. If you are required to include remote instructions and commands, you must be careful to verify that the remote host is trusted.

# ## The Problem with the Internet

The Internet itself presents its own unique problems. Its very nature is the heart of the problem; it was designed in anarchy to solve the anarchy problem. You can find several stories of how the Internet was created, but the most relevant fact is that it was designed to circumvent the problem of nuclear explosion blackout. That is the reason that the paths from host to host are so dynamic.

No path through the system is really exact. You cannot say to the network system: "Take this packet through these routers to the destination." Each packet may even follow a different path. Your pipe may go in and out of enemy territory on the Internet.

# ## Everything Is Visible

When writing network programs, you must remember an important rule: The Internet cannot guarantee you a private channel. Like yelling a sell command on the New York Stock Exchange floor, everyone there can hear you. However, most of the time those who hear don't care and ignore the message. Other times, the room can have listeners that can intercept or even revise that message for ulterior motives.

Similarly, the message may move in and out of trusted zones. A *trusted zone* is a network that a company trusts to be safe. For example, two popular trusted zones are the AT&T and US Sprint backbones. Other major corporations buy into these networks through dedicated lines. They are trusted because the zones host company provides limited guarantee of privacy.

Corporations create or buy into trusted zones as part of their own network or intranet. The intranet is the corporation's own network system. When two more corporations collaborate and share information in a special network (which often happens to be the same physical medium), they form an *extranet*. Because each company must get information quickly from host to host, the boundaries defining Internet, intranet, and extranet are beginning to blur.