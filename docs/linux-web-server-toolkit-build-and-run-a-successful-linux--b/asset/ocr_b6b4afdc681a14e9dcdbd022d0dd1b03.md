# Chapter 3: Choosing Your Software

With so many Linux CD-ROMs available in the back of books and as shrink-wrapped products with no documentation, you might wonder what use the manual is. Linux – is true of all UNIX systems – is a very complex system if you want to understand it completely or make it perform to its utmost. Reading the documentation that comes with your Linux system can guide you through the myriad of functionality that the system has to offer. That includes OpenLinux. This book focuses on creating a Web server, but you can use Linux for many other things that are described in the user manuals that accompany the full product from Caldera.

Apart from the installation instructions, which really ought to be in a printed manual, you should also inquire about how much online documentation is included with a Linux system. Most I've seen several thousand pages, often taken from the Linux Documentation Project (a free software type of documentation) and the Linux HOWTO documents on specific topics such as setting up a PPP connection or printing in Linux.

# Choosing Web Server Features

Once you have your Linux distribution selected and installed (Appendix A explains how to install the included OpenLinux Lite CD-ROM), you can choose your Web server software. To review a little, the Web server is the program that runs on your Linux operating system to accept requests from Web clients (browsers such as Netscape Navigator), process these requests, and return the information over the Internet or an organizational intranet. A Web server is also called an HTTP server or HTTP daemon–a UNIX name for a background program or process. The protocols and terms are defined at length in the next chapter.

As you select a Web server, you should consider the factors mentioned in the paragraphs that follow. Consider which factors are most important to you based on your organizational goals and concerns. You can use Table 3-2 to decide if a Web server other than the included Apache server would best serve your needs, either immediately or as your Site grows and develops.

# Web Server Features

The features outlined in the following paragraphs are those that you should consider as you choose Web server software. Everyone would like to have the best of everything, but compromises are always in order. You give speed for a more stable product, you give up security to get a free Web server, and so forth.

# SPEED

Speed refers to both how quickly the Web server program can respond to a request from a Web client (latency), and the number of requests that can be handled at one time (throughput capacity). Responding quickly to numerous client requests involves many facets, the least of which is how efficient the Web server