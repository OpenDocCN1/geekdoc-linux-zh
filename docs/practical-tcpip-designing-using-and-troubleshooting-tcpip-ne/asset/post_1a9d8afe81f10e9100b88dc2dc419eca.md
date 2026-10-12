
26.10 Configure the PC's dial-up default gateway and other routing 680

26.11 Dial-up PC connecting to HQ's network 682

26.12 Miscellaneous 684

Summary 686

## 27 VPN – virtual private networking 691

27.1 What VPN is and why you want it 692

27.2 IPsec – the IP security protocol 694

27.3 IPsec concepts – manual keying 696

27.4 IPsec manual keying example 698

27.5 VPN implementation details 700

27.6 IKE – Internet Key Exchange (automated keying) 702

27.7 IKE example 704

27.8 Protecting dial-up VPN 706

27.9 VPN troubleshooting 708

27.10 Building a test network for VPN 710

Summary 712

## Epilog 719

## Appendices 721

1 Layers, the protocol stack, and network reference models 722

2 RFCs and Internet standards 726

3 Ethernet Hubs and switches 731

4 `tcpdump` command summary 736

5 `tcpdump` man page in full 741

6 Making network settings permanent – Debian Linux 766

7 UTP and null-modem wiring 776

8 Windows-NT `route` command manpage 778

9 Example of working network diagram 779

10 Our on-site toolkit 780

11 `nslookup` man page in full 781

12 `host` man page summary 788

13 Base64 encoding 792

14 Nested MIME attachments 794

15 Example of an IMAP session 796

16 Installing `ethereal`; `ethereal` field names 798

17 HTTP/1.1 server response codes 802

18 IP Protocol numbers 804

19 `nc (netcat)` man page in full 805

20 Controlling network services 808

21 NetBIOS names 815

22 DNS and NetBIOS name resolution order in Windows 818

23 Windows name resolution worksheet 822

24 The BROWSTAT command 824

25 Worksheet for testing a new Internet connection 828

26 Organizing your software downloads 830

## Index 833

## Preface

This book is based on practical experience with TCP/IP networks and has evolved from our in-house and public training course materials. For several years our company has concentrated on installing firewalls and e-mail systems, and in that time we’ve found that there’s a small kernel of knowledge that you need to get your network up and running quickly, and to make it run efficiently. We’ve noticed that many IT professionals in charge of their organization’s computing understand their applications and high-level systems fully (in the old days they were called “data-processing specialists”) but have a lot of trouble with the basic underlying networks. Another reason for writing this book is for training our own consultancy and services staff. For a relatively inexperienced engineer, going on-site to install a customer’s network or firewall can be daunting: you’re working under time pressure, on an unfamiliar network, and so many things can go wrong. You can never foresee all possible problems, so the best way to prepare people is to give them a problem-solving “methodology” – an understanding of how to analyze problems, and break them down into manageable bits – and a good set of tools that let you see exactly what’s happening. We’ve found this is a great way to build up people’s skills and confidence. (Our customers have been pleased with it, too.)

The book distills out the essentials you need in practice. There are hundreds of large books and manufacturers’ manuals about TCP/IP, but it’s hard to find what you really need. There is so much information that newcomers are swamped with detail they don’t need, and explanations they can’t understand because they don’t have the context to relate them to.

By contrast, this book:

- tells you *how* to build your network
- starts with a simple two-machine network and goes on to a full network connected to the Internet with a firewall and internal routers, and DNS and e-mail servers
- explains the software tools you need to diagnose problems and to understand how your network is operating
- explains *why* you would want to do things, as well as *how* to do them
- includes practical troubleshooting and diagnostic techniques that you can apply just about everywhere, so you can solve problems in your own network and in systems configured by others
- assumes things will go wrong rather than work first time. We explain error messages and other symptoms, and then how to get over problems. We’ve found this is great for the confidence of our own engineers out on-site because they know they’ll be able to fix any errors they make, and we hope it will help you too. (Just a typo in an IP address can cause a system to fail, and as we network people live in a veritable sea of IP and Ethernet numbers, it’s easy to make mistakes, especially when you’re working on someone else’s network. So we have to show you how to identify and fix these errors.)
- ties together the various networking components so you view a network as a whole, not just disjointed pieces. As we cover Linux® and Windows® operating systems, and how they relate, the book is relevant to just about everybody
- can be used as the basis for a course of self-study or a taught training course.

You end up with a working network, you understand what is happening at a detailed level, and you gain the ability to diagnose and fix problems, and to identify bugs in the software you're using.

We cover networking from the bottom up, in small chunks. We have found that when you're learning, if you break things down into small pieces and examine one in isolation without the complication of other factors, it's much easier to understand. Then you can go and tie all the pieces together when you understand them. Consequently, some of our topic sections are brief (but non-trivial).

### Intended audience

- technical staff, technical managers, or technical sales
- consultancy and services staff installing or managing customer networks
- people using TCP/IP networks every day ...
- who are managing and building networks, or ...
- who are responsible for an organization's applications and systems as a whole
- people building TCP/IP networks at home
- anyone connecting to the Internet
- students at any level studying computer networks

### Background

This book was inspired by Richard Stevens' TCP/IP Illustrated Volume 1. Stevens gives a wonderful explanation of how the TCP/IP protocols operate, and to some extent how they evolved. To get a theoretical understanding of TCP/IP, we've found no better book. But Stevens is primarily explanatory, not practical. His approach is to explain TCP/IP by showing you the packets on the wire. We also look at the packets, but:

- we use it as a diagnostic technique
- we expect you to do it as well, not just look at our pictures.

Our book differs in other ways too. As well as explaining how the protocols work in practice, we cover:

- how to set up test networks so you can experiment with the protocols
- techniques for exploring what's happening
- debugging tools and techniques
- a different balance between the various topics. For example, Stevens devotes about a page to how routing works; we do three chapters. He devotes long chapters to TCP internals such as sliding windows, slow start, etc. which we don't even mention. Our guiding

principle has been “do we need to know this in our day-to-day work?” If not, we either omit it or relegate it to the Notes sections or an appendix if it gives an interesting insight into what we’re doing. However, the core knowledge we give you will always allow you to go forward and explore these other, more exotic areas if you need to.

We don't assume you are as familiar or experienced with networking as Stevens does, nor do we assume programming (or significant experience with binary arithmetic). With our book, you learn by doing as well as reading.

### What this book isn’t

The book does not attempt to describe the theoretical foundation of networking; the books by Stevens and Comer and many others already do this superbly and we strongly recommend them. We don't cover world-wide enterprise-scale Microsoft networks, Internet backbone router configuration, OSPF, BGP, and ATM and other ISP-level topics: 99% of the population never needs that stuff. Nor do we cover the nitty-gritty system administration of individual server packages (e.g. “how to configure sendmail or Exchange”) because there are so many of them and there are lots of books dedicated to them. Instead, we concentrate on the network aspects of the system.

### The operating systems that we cover

We use Linux® and Windows-NT® in equal depth, and occasionally mention Windows-95/98 and Windows-2000 (“Win-2K”) and Windows XP. When we say Windows-NT we generally mean Windows NT Server, especially when dealing with routing. At a user and general networking level, Windows NT Workstation contains most of the same tools, and you configure it the same way as NT Server.

The examples in the text are based on Debian Linux, but only because that's what we've been using in-house for years. Everything we cover applies to other versions of Linux as well, although there may be the usual slight differences in where a particular command or file is located. We've deliberately isolated the Linux system-specific configuration details into a single appendix (Appendix 6), and a Red-Hat equivalent of this is available on our Web site.

We don't use any GUI-based Linux tools, because:

- in real life, you'll often have to work with servers and routers that don't have any GUI and frequently may not even have a screen
- using the command-line keeps you very close to the guts of the thing, so you really understand what's happening
- the command-line tools are available with minor differences on other versions of UNIX. The GUI-based tools aren’t.

Once you understand the command-line tools, using the particular GUI tool on your platform will be child's play.

We sort of assume that you have both Linux and Win-NT available, if only because we often take the line of least resistance and use whatever is easiest initially.
