
# Key Concept

Navigating through the information is fairly straightforward. The spacebar scrolls down one screen and the Delete key scrolls back one screen. You can jump forward to the next topic by typing n and jump back by typing p. Typing l will return you to your last location.

The info utility provides much the same information as the man pages; however, it is usually easier to understand. The spacebar scrolls up and the Delete key scrolls down. Type n for the next topic and p for the previous one. Typing q will quit.

# HOWTOs

Linux HOWTOs are detailed documents that describe the methods of performing tasks in Linux. For example, you may need to find out how to configure a piece of hardware or how to complete a simple task such as printing a document.

A HOWTO document usually covers a complex subject and as such tends to be rather long. Less complex subjects such as LILO and printing are covered in mini HOWTOs.

Versions (usually compressed) of HOWTOs are usually installed in the /usr/doc/HOWTO directories. Check online to find the latest version(s).

You can download the latest version of a HOWTO via ftp (from ftp://sunsite.unc.edu/pub/Linux/docs/HOWTO or one of its mirrors). They also can be browsed via HTML from several sites, including http://sunsite.unc.edu/LDP/HOWTO/ or http://www.linuxdoc.org/HOWTO/.

Mirror sites can be located by consulting http://sunsite.unc.edu/LDP/mirrors.htm. These documents are also available in several different languages.

# Key Concept

HOWTOs are written by users to describe how they solved a problem. They are easier to use than man pages and info and cover different topics. Because HOWTOs are frequently updated and new ones published, you should periodically verify that you have the latest versions.

HOWTOs are easier to understand than using man pages or info and frequently address issues that are not discussed in other locations. They include topics that other users have researched and published that would be useful to other users.

For example, are you trying to run the game Quake on Linux? Checking the man pages and info does not help. However, there is a HOWTO that tells you how to do it.

# FAQ

FAQs (Frequently Asked Questions) is a collection of documents that are intended to be read in conjunction with the HOWTO documents. They are written in a question-and-answer format, addressing those questions that users ask most often.

FAQs are available in HTML, PostScript, and text formats. Copies of the FAQs in all three formats are usually installed in the /usr/doc/FAQ directory by almost all distributions. Check online to find the latest version(s) at http://linuxdoc.org/FAQ/.

# Program Documentation

Text files that provide more information about specific programs can be found in /usr/doc in subdirectories named for the program and version number. These provide information on installation, configuration, and use of the application. You can usually read them with either less or more.

In addition, applications usually install a manual page that discusses how to use the program. These are found by using the man command discussed earlier in this chapter.

# Internet Resources

As you know, all the source code for Linux is available on the Internet for download. Linux documentation is also online in many locations. The primary source of information related to Linux is the Linux Documentation Project at http://metalab.unc.edu/LDP/. Here you’ll find all the HOWTOs, mini-HOWTOs, and FAQs. This site also provides the ability to search all of the material from one place.

The Linux Documentation Project also has made available several guides that cover specific topics ranging from the kernel to network administration. They are available from http://sunsite.unc.edu/LDP. Available guides include

- The Linux Documentation Project Manifesto, by Matt Welsh
- Installation and Getting Started Guide, by Matt Welsh
- The Linux Kernel, by David Rusling
- The Linux Kernel Hackers’ Guide, by Michael K. Johnson
- The Linux Kernel Module Programming Guide, version 1.1.0 by Ori Pomerantz
- The Network Administrator's Guide, by Olaf Kirch
- The Linux System Administrators' Guide, by Lars Wirzenius
- The Linux Users' Guide, by Larry Greenfield
- The Linux Programmer's Guide, by Sven Goldt, Sven van der Meer, Scott Burgett, and Matt Welsh

A more recent project to make Linux documentation more user-friendly is under way by Linuxnewbie.org (http://www.linuxnewbie.org/). Their goal is to create user-friendly documents out of existing HOWTOs, FAQs, and other resources.

# Newsgroups

A wealth of information is available via many Usenet newsgroups. The *comp.os.linux.announce* newsgroup is a moderated group that contains up-to-date information about software updates, new ports, user group meetings, and commercial products. Submissions to this group should be emailed to linux-announce@news.ornl.gov.

*comp.os.linux.answers* contains all the FAQs, HOWTOs, and other important documentation. HOWTOs are posted near the beginning of the month. You then can use the NestoHOWTO program available from `http://sunsite.munc.edu/pub/Linux/system/news/misc/` to assemble the posts.

Other groups worth reading are in the *comp.os.linux.\** hierarchy. Often, you can have a problem that is not in a HOWTO or FAQ but is answered in one of the following newsgroups:

- comp.os.linux.setup
- comp.os.linux.hardware
- comp.os.linux.networking
- comp.os.linux.x
- comp.os.linux.development.apps
- comp.os.linux.development.system
- comp.os.linux.advocacy
- comp.os.linux.misc

Most newsgroups are archived at `http://www.deja.com` and `http://www.altavista.com` where you can search postings relevant to a specific topic or forum.

# Mailing Lists

Several mailing lists are available on the subject of Linux. Some of these are generic while others apply to a specific distribution.

You can join a mailing list mirror of `comp.os.linux.announce` by sending email to `Linux-Announce-Request@NEWS-DIGESTS.MIT.EDU` with the word `subscribe` in the body of the message. Sending an empty message to the same address will get you help on using the mailing list (including instructions on how to leave).

There are several Linux mailing lists hosted at `majordomo@vger.rutgers.edu`. Send a message with the word `lists` in the body to find out what lists are available. Sending a message with the word `help` will get you instructions for subscribing and unsubscribing to the lists. Most of these lists are technical and are not intended for new users' questions.

Be sure to follow the rules of Net etiquette. Don't pose a question to a newsgroup or mailing list until after you have researched it. Often your question has already been posed and answered. Check the documentation (HOWTOs, FAQs, and man pages) first, then check the archives at `http://www.deja.com/` before you post.

If you do post, include as much relevant information about your system and your problem as possible, such as general information on the version(s) of your software and a brief summary of your hardware configuration. Learn to appreciate the value of hacking your system, and how to fix problems yourself.

# Searching for Information

There are many other ways to find information about commands when you need help. Some of the most frequently used commands are `whereis`, `whatis`, `which`, and `apropos`.

# whereis

The `whereis` command is used to find files but also will show you the location of the file's binary, source files, and any associated manual pages. One limitation of `whereis` is that the search is limited to known directories that are coded into the program. Its syntax is

```
whereis [options] filename
```

If you wanted to see where to find `passwd` or its related man pages, you would type

```
whereis  passwd

passwd: /usr/bin/passwd /etc/passwd /etc/passwd.OLD /usr/man/man1/passwd.l
/usr/man/man5/passwd.5
```
