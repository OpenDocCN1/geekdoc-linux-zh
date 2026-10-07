
# Contents xx

## Chapter 17 Using Server APIs. . . . . . . . . . . . . . 411
What Are APIs?.. . . . . . . . . . . . . . . . . . . . 411
Introduction to the Apache API . . . . . . . . . . . . . . . . . . 412
Introduction to the Netscape API . . . . . . . . . . . . . . . . . . 413
Using APIs to Your Advantage . . . . . . . . . . . . . . . . . 414
Programming with the Apache API . . . . . . . . . . . . . . . . . 415
Programming with the Netscape API . . . . . . . . . . . . . . . . . 416
Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 419

## Chapter 18 Web Security Issues and Internet Firewalls.. . . . . 421
A Summary of Security Issues . . . . . . . . . . . . . . . . . 421
Brute Force Attacks . . . . . . . . . . . . . . . . . . . . . . 422
Keyboard Readers. . . . . . . . . . . . . . . . . . . . . . . 422
Packet Sniffers . . . . . . . . . . . . . . . . . . . . . . . 423
Human Error . . . . . . . . . . . . . . . . . . . . . . . . . 424
Web Server Security Issues . . . . . . . . . . . . . . . . 424
A Security Checklist . . . . . . . . . . . . . . . . . . . . . 426
Adding a Firewall to Your Network . . . . . . . . . . . . . 427
Protocol Routing Firewalls. . . . . . . . . . . . . . . . . 428
Using Application-Level Firewalls . . . . . . . . . . . . 431
Using Firewalls. . . . . . . . . . . . . . . . . . . . . . . 431
Learning More About Firewalls . . . . . . . . . . . . . . . 431
Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . 432

## Chapter 19 Maintaining Your Web Pages . . . . . . . . . . . 433
Recognizing Potential Problems. . . . . . . . . . . . . . . . 433
Implementing Maintenance Processes. . . . . . . . . . . . . . . 434
Using Spell Checking Tools. . . . . . . . . . . . . . . . . . . . . . . 437
Professional Tools . . . . . . . . . . . . . . . . . . . . . 437
Ispell . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 438
Using HTML Validation Tools . . . . . . . . . . . . . . . . 439
Finding the Right HTML Validation Tools . . . . . . . . . . . . . 440
A Good Link Checker (and it's Free) . . . . . . . . . . . . . . 442
Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . 443

## Chapter 20 Backups and Disaster Recovery . . . . . . . . . . . 445
Determining Your Level of Need. . . . . . . . . . . . . . . . 445
How Important Is Your Web Site . . . . . . . . . . . . . . . . 445
Possible Web Server Problems . . . . . . . . . . . . . . . . 446
Preparing a Disaster Plan . . . . . . . . . . . . . . . . . 447
Simple Disaster Plan. . . . . . . . . . . . . . . . . . 447
Complex Disaster Plan. . . . . . . . . . . . . . . . . . 448
Implementing Your Plan . . . . . . . . . . . . . . . . . 449

# Linux Web Server Toolkit

Backing Up Your Web Server ................................................... 449
Types of Backups ............................................................ 449
Utilities to Back Up Your Server.............................................. 451
Summary ............................................................................ 453

# Chapter 21

Upgrading Linux Kernels and Software Packages ................................................ 455
Tracking Updates of the Linux Kernel....................................................... 455
Remaking the Linux Kernel ................................................................... 456
Using the make Utility ...................................................................... 456
Creating a New Linux Kernel.................................................................. 457
Working with New Packages...................................................................... 459
Adding New Packages .......................................................................... 460
Upgrading Existing Packages ................................................................... 461
Adding Security Patches ........................................................................ 462
Summary ........................................................................................ 462

# Appendix A: What's on the CD-ROM ................................................................... 465
# Index ............................................................................................ 471
# End-User License Agreement ................................................................... 497
# CD-ROM Installation Instructions .............................................................. 502

# Part I

## Planning Your Web Server

The first four chapters of this book provide vital background information on the Web, Web servers, and Linux. You'll learn the history and benefits of Linux, as well as how to create a plan for your site and define a presence on the Web and how to choose a Linux distribution as well as server software, based on your requirements. The last chapter in Part I discusses the Internet, the Web, and UNIX and how they are related, and includes an introduction to the graphical interfaces of Linux.

![](img/e01f1106dd2902613fa07890c8baa7e6_29_0.png)

# Chapter 1

## Planning Your Web Site

THE FACT THAT YOU purchased this book means not only that you (or someone else) have already decided your company needs a Web site, but that the decision has been made to allocate resources for a full-fledged Web server. A Web server is any computer that stores Web pages and responds to browser requests using Internet protocol, such as TCP/IP, and the HTTP protocol.

This chapter should bolster your confidence and, it's hoped, address some basic questions you may still have about this burgeoning phenomenon we call the Web. It also gives you some facts to pass on to those less enthusiastic than yourself.

The topics covered in this chapter include the following:

- The Web explodes
- Why have a Web site?
- What makes a good Web site?
- What makes a bad Web site?
- Defining your Web presence
- Creating a plan for your site
- Legal considerations

Chapter 2 begins the discussion of Linux, and why it makes an ideal Web server platform.

## The Web Explodes

It's pretty amazing to think of how fast the Web has grown. It's been like microwaves or fax machines—just about everyone I can't imagine how to live without the Web. Suddenly, it seems as though everyone wants to be surfing the Web and even to have their own page or site. In 1994, there was a What's New page to which everyone submitted URLs for their pages and servers. I really enjoyed reviewing these lists to see the growing diversity of content that people were putting on the Web. The list seemed to grow exponentially, and I started seeing Web servers from all over the world.
