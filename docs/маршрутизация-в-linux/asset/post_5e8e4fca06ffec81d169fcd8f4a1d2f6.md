
## Tell Us What You Think

As the reader of this book, you are the most important critic and commentator. We value your opinion and want to know what we’re doing right, what we could do better, what areas you’d like to see us publish in, and any other words of wisdom you’re willing to pass our way.

As Associate Publisher at New Riders Publishing, I welcome your comments. You can fax, email, or write me directly to let me know what you did or didn’t like about this book—as well as what we can do to make our books stronger.

> Please note that I cannot help you with technical problems related to the topic of this book, and that due to the high volume of mail I receive, I might not be able to reply to every message.

When you write, please be sure to include this book’s title and author as well as your name and phone or fax number. I will carefully review your comments and share them with the author and editors who worked on the book.

Fax: 317-581-4663
Email: stephanie.wall@newriders.com
Mail: Stephanie Wall
Associate Publisher
New Riders Publishing
201 West 103rd Street
Indianapolis, IN 46290 USA

## Introduction

In the Linux world, when we talk about routing we're usually just referring to utilizing the route command to set up some nice, simple data delivery information. A Linux box is capable of so much more. With the proper setup and tuning, you can build a stable and efficient router for your network and its subnets. Linux Routing gives you the background and techniques you need to choose the appropriate routing protocol(s), configure the routing daemon(s), add security and obfuscation to protect your data and machines, fine tune the kernel for this very task-specific setup, and even monitor your traffic and adjust it to make it more efficient.

## What’s Inside?

Because so many Linux administrators haven't had to tackle the ins and outs of routing protocols, multicasting, IPv4's classless addressing possibilities, and more, this book begins with a thorough discussion of much background information that you must understand before you can easily proceed with the rest. To this end, we've broken this book into Parts for simpler navigation:

- Part I, "Routing Basics," contains Chapters 1 through 4.
- Part II, "Linux Routing Issues and Technologies," contains Chapters 5 through 15.
- Part III, "Appendixes," contains Appendix A and B.

From there, it's the individual chapters that are of interest, so let's take a look.

## Chapter 1, "Unicast Protocols"

As the saying goes, it's usually best to begin at the beginning. The unicast routing protocols contain some of the oldest Internet protocols that are still in use. This chapter introduces an example network used throughout Part I to give you a consistent framework to compare and contrast how these protocols work—and how they work is covered in detail. Specifically, it covers static routing and the protocols: RIP version 1 (RIP-1), RIP version 2 (RIP-2), and OSPF version 2.

## Chapter 2, "Multicast Protocols"

Not everyone is content to stick with unicast. This chapter covers the most popular multicast routing protocols. Once again, we use the example network to discuss how each of these works so that you have a solid framework from which to decide which of these you want to implement. Specifically, this chapter covers the multicasting features of RIP-2, plus the following multicast protocols: DVMRP, MOSPF, PIM-DM, and PIM-SM.

## Chapter 3, “Introduction to Border Routing Protocols”

While the previous two chapters focus on what you’re doing in your own little part of the world, there has to be a way as well for your networks to talk to others. Without such a method there would be no Internet. This chapter focuses on both unicast and multicast protocols where implementations are available for Linux use. These protocols are: EGP, BGP, BGMP, and MSDP.

## Chapter 4, “IPv4 and IPv6 Addressing”

Many Linux aficionados know the standard ins and outs of IPv4 addressing. This chapter begins with a thorough look at IPv4 subnetting for those who have never had to learn the math behind it and have just used certain set solutions in the past. Then, we move into new territory. The next item is IPv4 Classless InterDomain Routing (CIDR), which allows you to break up your addressing space without sticking to class A, B, and C boundaries.

Finally, it’s time to get familiar with IPv6 before the transition takes you by surprise. We take a look at the basics of working with this addressing system so you’ll know how to recognize types of addresses, break IPv6 addresses down into their hexadecimal components, and more.

## Chapter 5, “Inside the Unicast Kernel 2.2.x Daemons”

There are a fair number of daemons available for routing in Linux. If we were to have covered them all in depth, then that would have filled the entire book. So in this chapter, we take a look in great detail at good old routed and the public version of gated. Here you’ll learn not only about these daemons, but everything there is to know about configuring them. When it comes to gated, this means you’ll learn how to set it up for all of the unicast protocols that you’ve learned about so far. Pointers to the other potential routing daemons are included.

## Chapter 6, “Inside the Multicast Kernel 2.2.x Daemons”

Multicasting data is a growing movement, but it has not yet reached the mainstream proportion that its proponents would like. This chapter covers two different multicasting daemons available for Linux. One of these is mrouted, which is typically used to connect to the MBONE—the multicast backbone—because it implements the DVMRP protocol; and the other is pim6d, which is used for most other multicast applications because it supports the PIM-SM protocol.
