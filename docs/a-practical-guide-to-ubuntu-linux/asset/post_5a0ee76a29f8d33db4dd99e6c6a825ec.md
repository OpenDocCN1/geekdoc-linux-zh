
As programs to read netnews articles have been ported to non-UNIX and non-Linux systems, the community of netnews users has become highly diversified. In the UNIX tradition, categories of netnews groups are structured hierarchically. The top level includes such designations as comp (computer-related), misc (miscellaneous), rec (recreation), sci (science), soc (social issues), and talk (ongoing discussions). Usually at least one regional category is at the top level, such as ba (San Francisco Bay Area), and includes information about local events. New categories are continually added to more than 30,000 newsgroups. The names of newsgroups resemble domain names are read from left to right (like Linux filenames): comp.os.unix.misc, comp.lang.c, misc.jobs.offered, rec.ski, sci.med, soc.singles, and talk.politics are but a few examples.

A great deal of useful information is available on Usenet, but need patience and perseverance to find what you are looking for. You can ask a question, and someone from halfway around the world answer it. Before posing a simple question and causing it to appear on thousands of systems around the world, however, first ask yourself whether you can get help in a less invasive way. Try the following:

- Refer to the man pages and info.
- Look through the files in /usr/share/doc.
- Ask the system administrator or another user for help.
- All of the popular newsgroups have FAQs (lists of frequently asked questions). Consult these lists and see whether your question has been answered. FAQs are periodically posted to the newsgroups; in addition, all the FAQs are archived at sites around the Internet, including Google groups (groups.google.com).
- Because someone has probably asked the same question earlier, search the netnews archives for an answer. Try looking at groups.google.com, which has a complete netnews archive.
- Use a search engine to find an answer. One good way to get help is to search on an error message.
- Review support documents at help.ubuntu.com.
- Contact an Ubuntu Linux users' group.

Post a query to the worldwide Usenet community as a resort. If you are stuck on a Linux question and cannot find any other help, try submitting it to one of the newsgroups:

- comp.os.linux.misc
- alt.os.linux
- comp.os.linux.networking
- comp.os.linux.security
- comp.os.linux.setup

One way to find out new tools and services is to use Usenet news. The comp.os.linux hierarchy is of particular interest to Linux users; for example, news about newly released software for Linux is posted to comp.os.linux.announce. People often announce the availability of free software there, with instructions on how to get a copy for your use using anonymous FTP (page 694). Other tools to help you find resources, old and new, exist on the network; see Appendix B.

## WWW: World Wide Web

The World Wide Web (WWW, W3, or the Web) provides a unified, interconnected interface to the vast amount of information stored on computers over the world. The idea that spawned the World Wide Web came from the mind of Tim Berners-Lee (w3.org/People/Berners-Lee) of the European Particle Physics Laboratory (CERN) in response to a need to improve communications throughout the high-energy physics community. The first-generation solution consisted of a program named Enquire, short for Entire Within Everything (the name of a book from Berners-Lee's childhood), which he created in 1980 on a NeXT computer and which supported links between named nodes. Not until 1989 was the concept proposed as a global hypertext project to be known as the World Wide Web. In 1990, Berners-Lee wrote a proposal for a hypertext project which eventually produced HTML (Hypertext Markup Language), the common language of the Web. The World Web program became available on the Internet in the summer of 1991. By designing the tools to work with existing protocols, such as FTP and gopher, the researchers who created the Web produced a system that is generally useful for many types of information and across many types of hardware and operating systems.

The WWW is another example of the client/server paradigm. You use a WWW client, or browser, to retrieve and display information on a server that may be located anywhere on your local network or the Internet. WWW clients can interact with many types of servers. For example, you can use a WWW client to contact a remote FTP server and display the list of files it offers for anonymous FTP. Most commonly you use a WWW client to contact a WWW server, which offers support for the special features of the World Wide Web that are described in the remainder of this chapter.

The power of the Web derives from its use of hypertext, a way to navigate through information by following cross-references (linked links) from one piece of information to another. To use the Web, you need to run interactive network applications. The first GUI for browsing the Web was a tool named Mosaic, which was released in February 1993. Designed at the National Center for Supercomputer Applications at the University of Illinois, its introduction sparked a dramatic increase in the number of users of the World Wide Web. Marc Andreessen, who participated in the Mosaic project at the University of Illinois, later co-founded Netscape Communications with the founder of Silicon Graphics, Jim Clark. The created Netscape Navigator, a Web client program that was designed to perform better and support more features than the Mosaic browser. Netscape enjoyed immense success and has become a popular choice for exploring the Wide Web. Important for Linux users is the fact that its inception Netscape has provided versions of its tools that run on Linux. Also, Netscape created Mozilla (mozilla.org) as an open-source browser project.

These browsers provide GUIs that allow you to listen to sounds, watch Web events or live news reports, and display pictures as well, giving you access to hypermedia. A picture on your screen may be a link to more detailed, nonverbal information, such as a copy of the picture at a higher resolution or a short animation. If your system can produce audio output, you can listen to audio clips that have been linked to a document.

## URL: UNIFORM RESOURCE LOCATOR

Consider the URL http://www.w3.org/Consortium/siteindex. The first component in the URL indicates the type of resource, in this case http (HTTP-Hyper Transfer Protocol). Other valid resource names, such as https (HTTPS-secure HTTP) and ftp (FTP-File Transfer Protocol), represent information available on the Web using other protocols. Next come a colon and double slash (/). Frequently the // string is omitted from a URL in print, and unless you need to enter it to reach the URL. The next element is the full name of the host that acts as the server for the information (www.w3.org/). The rest of the URL consists of a relative pathname to the file that contains the information (Consortium/servlet). If you enter a URL in the location bar of a Web browser, the Web server returns a frequently, HTML (page 112) file.

By convention many sites identify their WWW servers by prefixing a host or domain name with WWW. For example, you can reach the Web server at the New Jersey Institute of Technology at www.njit.edu. When you use a browser to explore the World Wide Web, you may never need to enter a URL. However, as more information is published in hypertext text, you cannot find but URLs everywhere—not just online email messages and Usenet articles, but also in newspapers, advertisements, and on product labels.

## BROWSERS

Mozilla (mozilla.org) is the open-source counterpart to Netscape. Mozilla, which was first released in March 1998, was based on Netscape 4. Since then, Mozilla has been under continuous development by employees of Netscape (a division of AOL) and other companies and contributors from the community. Firefox is the Web browser component of Mozilla. KDE includes Konquer, an all-purpose file manager and Web browser. Other browsers include Epiphany (projects.gnome.org/epiphany) and Opera (www.opera.com). Although each Web browser is unique, all of them allow you to move about the Internet, viewing HTML documents, listening to sounds, and retrieving files. If you do not
