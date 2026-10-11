
# Figure 15.1A: Error message 404.

If the response is that the request was OK and the server is processing it, then the server will respond by sending the appropriate HTML document to the Web browser that was requesting that document. The browser then loads that document into memory and displays it in the browser. The basic process of sending and receiving requests between a Web browser, your ISP, and a Web server is diagrammed in Figure 15.1b.

![](img/12d790664598bbf390261087fbe55bbc_327_1.png)

# Figure 15.1B: The process.

There are a number of codes that a Web server can send back to a browser. Some of the more common codes are listed in Table 15.1. It is important that you remember two facts. The first is that these error codes are the same regardless of the browser making the request or the Web server answering the request. An Internet Explorer browser connecting to a Microsoft Internet Information Server® Web server will get the same codes that a Mozilla browser connecting to an Apache Web server will get. The second fact to keep in mind is that the browser will not display some codes to you. For example, if the code indicates that the Web page was found and is being sent, then that code will not be displayed. Usually your browser will only display those codes that indicate an error of some type has occurred.

# Table 15.1: HTTP Return Codes

| Code | Meaning |
| :--- | :--- |
| 101 | This is an indication that the browser has asked to switch protocols (maybe to download a file, so it is switching to FTP) and the server is agreeing. |
| 200 | This is just an OK message. |
| 202 | The request has been accepted. |
| 301 | The page has been moved and you are being redirected to the new address. |
| 401 | The browser is not authorized to do whatever it is attempting. |
| 404 | The requested file could not be found. |
| 504 | Server timed out. |

Some of these response codes you would never see. The browser would process them. Some, like 401, 404, and 504, you will probably see at some point in your Web surfing. It is not necessary for you to commit this list to memory. What is important is that you understand what is going on in the background when you use your Web browser to visit some Web site. Messages are being sent from your browser to the server. On the server end, some software is listening in to port 80 for standard browser requests and then responding. That is the essence of a Web server. Now keep in mind that commercial Web servers are generally run on very high-end computers with backup hard drives, lots of memory, and lots of processor power. However, you can certainly run a Web site from your personal computer. It just won’t be able to handle thousands of visitors every day.

This leads us to the Web server software. There are several programs available that will listen on port 80 and respond to HTTP requests. Some are easier to use than others. Also, some work on one operating system but not another. The two most commonly used are Microsoft’s Internet Information Server, commonly called IIS, and the Apache Web Server from www.apache.org. Since IIS is strictly for Windows, we will devote much of this chapter to Apache.

**Note** You can go to www.netcraft.org and type in any Web site’s address. It will then tell you what kind of Web server that Web site is using.

## The Apache Web Server

Apache is a full-featured robust Web server that is available, free of charge, for Unix, Linux, and even for Windows. This software is completely open source and is free to download from www.apache.org. It also ships with Red Hat Linux. The fact that it is included in the Red Hat installation makes it ideal for our purposes. The Apache Project is a collaborative software development project whose aim is to produce a robust, professional-level, full-featured HTTP (Web) server. The project is managed by a group of volunteers located around the world, using the Internet and the Web to communicate. These volunteers are known as the Apache Group. It is important to realize that the entire process is done by volunteers donating their time and expertise. In addition, hundreds of Apache users have contributed ideas to the project.

### Apache History

Before we delve into the intricacies of working with Apache, it might be a good idea to explore its history just a little. In February 1995, the most popular server software on the Web was an HTTP daemon developed by Rob McCool at the National Center for Supercomputing Applications, University of Illinois, Urbana-Champaign. Recall that a daemon is just a program that runs in the background without interaction from the user sitting at the computer. In Windows these are called services. Unfortunately, development of that Web server stalled after Mr. McCool left NCSA in 1994. However, since it was open source, many Webmasters developed their own extensions to the Web server as they were needed. A small group of these Webmasters decided that they should coordinate their efforts into a standard release of the software. Brian Behlendorf and Cliff Skolnick put together a mailing list and set up a server to hold extensions written by the core development team. At that point these eight core contributors formed the foundation of the original Apache Group. The names of these individuals are

- Brian Behlendorf
- Roy T. Fielding
- Rob Hartill
- David Robinson
- Cliff Skolnick
- Randy Terbush
- Robert S. Thau
- Andrew Wilson

They started with Version 1.3 of the NCSA Web server as a base and then added all of the published bug fixes and enhancements they could find. Apache was an immediate success. Webmasters loved the price: free! And developers loved the open source concept. This enabled any competent programmer to make modifications and submit them for release as part of the next version of Apache.

Apache exists today for a few rather simple reasons. It is a robust, professional-grade Web server that is free of charge. Apache was originally available only for Unix-based systems, but has since been ported to Windows. This brings us to one last but very humorous point in the history of Apache, the name. Some people seem to think the name is derived from the Native American tribe, but this is not true. Since this Web server was originally the work of several different developers patched together, it was called A-Patchy-Server. This name eventually morphed into Apache Server.

### How to Set Up Apache

If you have Red Hat Linux, then Apache comes with it. And if you followed the instructions in Chapter 2, then it is already installed on your system. However, in case you are not sure, remember that you can go to the Start menu, select System Tools, and choose Packages to see if it is installed. You can add it if it's not already installed.

Now we are going to need to modify a few files. To find them it would be best to use the File Manager, so your next step is to launch that application. If you will recall, when we first discussed File Manager, you where admonished to spend some time getting comfortable with it, as it would be used later in this book. If you still don't feel comfortable with the File Manager, take the following steps slowly, consulting the images provided in this chapter to ensure that you are on the right track.

You will need to first find the /etc/httpd/conf directory. Use the File Manager to locate the etc directory, then open it. Within that directory you will find a subdirectory named httpd. Then you look under that directory for yet another subdirectory named conf. Browse through this until you find the httpd.conf file. When you find it, right-click on it and open it with Text Editor. This directory and file are shown in Figure 15.2.

![](img/12d790664598bbf390261087fbe55bbc_330_0.png)

**Note** Do not double-click on the file. If you do that, the document will be opened in a read-only mode, and you won't be able to make any changes. Recall that many applications, including the File Manager, work like a Web browser. If you double-click on a file, it will open like a Web page, for viewing only.

You will see that this is a large text file with a lot of information in it. You may even feel a bit overwhelmed. There are dozens of settings available in this file. However, most of them are not required for basic Web server operation. These settings are important for advanced Web server operations that are beyond the scope of this book. Entire books have been written on Apache, and you would need to consult such a book to go deeper into Apache. There are only a few settings in this that you even care about. The most important is ServerName. Follow these steps and you can have your server running.

**Note** It will only be accessible from your machine. This is a test mode to see if the Apache server itself works properly. If all goes well, we will go back and change a few things to make it accessible from the entire Internet. Also note that the ServerName setting is sometimes commented out with a pound symbol in front of it. Delete the pound symbol.

1. Set the ServerName = localhost. This is shown in Figure 15.3.
