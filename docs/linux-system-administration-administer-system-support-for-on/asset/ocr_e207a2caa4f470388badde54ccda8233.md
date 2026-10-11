focusing on the TCP/IP network protocol. I have two practical reasons for doing so: (1) if your system includes data communications, you're likely to encounter TCP/IP, and (2) TCP/IP and is a clear illustration of how a network protocol works.

# ## TCP/IP Overview

TCP/IP (Transmission Control Protocol/Internet Protocol) is the main networking protocol used for communicating over the Internet. As it happens, TCP/IP is native to UNIX – which means it's native to Slackware Linux. As a Linux system administrator, you'll probably find that a handy feature when you connect your system to the Internet (if not other networks).

# ## Using the TCP Model

The TCP model is similar to the OSI model, but it's easier to remember because it uses fewer layers. TCP combines OSI layers 5, 6, and 7 – the Session, Presentation, and Application Layers, respectively – into its own Application Layer. OSI layers 1 and 2 – Physical and Data, respectively into its Physical Layer. Table 11-2 demonstrates the TCP model.

![](bbox=[0.07, 0.5, 0.14, 0.59])

If you're called upon to remember a particular TCP layer and don't have a chart handy, the following mnemonic device may help: **A** (**A**pplication) **T**iger **T** (**T**ransport) **N**ever (**N**etwork) **P**outs (**P**hysical).

# TABLE 11-2 THE TCP MODEL

| Number | Layer | Example |
| :--- | :--- | :--- |
| 4 | Application | ping, ftp, ssh, lynx |
| 3 | Transport | TCP, UDP |
| 2 | Network | IP address |
| 1 | Physical | Cables, Network Interface Cards, MAC address |

When your Linux system makes a connection to another machine (through ssh, for example), you use the command-line interface (at the Application Layer). Next,