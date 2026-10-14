
To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

# Online Help via /usr/doc

Linux stores many documentation and supplemental information files in /usr/doc. This directory is littered with a series of directories named after the program or tool to which they belong. Inside each you will typically find a README file containing some last-minute information about the program and frequently asked questions (FAQs) to features or issues with the program. This information is in addition to any documentation that you might find through man or other documentation readers.

The online help in the /usr/doc directory also contains some of the most important general Linux information on your computer:

- The Linux Installation and Getting Started Guide—This is a "getting started" manual for Linux beginners created by the Linux Documentation Project. The Linux Documentation Project is an initiative to create a complete set of online manuals for Linux computers.
- The Linux System Administrator’s Guide—This manual is about UNIX system administration and was created by the Linux Documentation Project.
- The Linux Network Administrator’s Guide—This manual describes how to use Linux in network environments and how to administer large, Linux-based networks. This manual was also created by the Linux Documentation Project.
- Other feature texts created by authors at the Linux Documentation Project.

• HOWTO documents—These feature guides on how to accomplish certain advanced tasks, such as configuring software or some interesting networking tool.

These documents are located in /usr/doc/html, but they are stored in HTML format, which means that you won’t want to read them with a pager like less. You can access them in two ways, depending on whether you are in a KDE (X) session or a console. In a KDE session, launch Netscape Navigator to view the online manuals. The actual URL is file:/usr/doc/html/index.html; as shipped, Navigator is configured to open a link to this page by default. If you are working from a console, start the text-based Lynx browser by typing “lynx” at the command line. Lynx is also configured to go to this page by default.

In addition to using Navigator and Lynx, if you are in KDE, you can type the URL into KFM’s URL location field, and KFM will display the documentation for you.

# More about HOWTO documents

Most standard Linux distributions include HOWTO documents. These documents explain how to do many things, like how to set up a DNS server in your box and how to configure a sound card. Most of these documents are written by fellow users or the developer of a tool as a help to the Linux community.

Many of these documents are invaluable. However, most are too long (the average document is about 60 pages long!) and tend to include a lot of peripheral information. This could present some difficulty to users who are new to Linux; their background level is not the same as that of a hacker. But this is what you get. In a free OS, it’s not too easy to come by a good technical writer who can distill what you need to know from what is nice to know.

The HOWTO documents on OpenLinux 1.3 systems can be found by visiting the online documentation URL in /usr/doc, as we discussed in the previous section.

# Mini HOWTOs

The mini HOWTO is similar in spirit to a HOWTO document; however, mini HOWTOs tend to be more free-form and shorter. HOWTO documents follow certain formatting standards that don’t bind mini-HOWTOs.

Mini HOWTOs can be found in the HOWTO index page on your OpenLinux 1.3 computer, and are designated by the word “Mini” somewhere in the title.

# LDP—Linux Documentation Project

The LDP is probably the most useful and most helpful online information about Linux. The LDP’s goal is to create reliable documentation for Linux, covering installation, kernel development, kernel information, network administration, system administration, and user guides. The authors at the LDP make sure that the documentation distributed with Linux is accurate and up-to-date.

Some of the manuals developed by LDP are available online in your system, as we’ve already discussed. Others are available through the Internet. If you have Internet access, you can view the latest documentation at http://sunsite.unc.edu/LDP.

In addition to providing online manuals and HOWTO documents, the LDP is responsible for maintaining a number of FAQ (Frequently Asked Questions) documents about Linux. These can be found at the LDP homepage on the Internet.

# Reading Compressed Documentation: zless

Occasionally, you may encounter compressed documents in /usr/doc or other help areas on your Linux computer. Compressed documents can be identified because they end with one of the following filename extensions: .gz, .z, or .Z.

When you encounter a compressed document on your Linux computer, you will either need to decompress it before reading it or use a special utility that can peek into compressed documents.

zless is a tool that allows you to view compressed text files (filenames ending in a .gz, .z, or .Z) with the less pager. If the zless command is not available, you can achieve the same by using zcat and less in a pipe:

```
zcat filename | less
```

To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

# Info Pages

A lot of developers are starting to use GNU's info to write documentation. The GNU info system uses hypertext to relate different pieces of information. The goal of info is to make reading a documentation page easier by proving a way to jump between different sections of the documentation.

The concept is similar to using a Web browser. To read documentation, you use the info command followed by the name of the tool you are interested in. If you don't provide a tool name, info will show you a list of all the commands it knows about and some entry points to the info documentation itself. The following figure shows a screen in info.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_170_0.png)

The info program.

The basic commands for moving in info are listed in Table 15.2.

# Table 15.2 Info Commands

| Key | Description |
| --- | ----------- |
| Space | Page down |
| Backspace | Page up |
| b | Beginning of the page |
| ? | Help |
| n | Next node |
| u | Previous node |
| l | Last node |
| u | Up |
| m | Menu (type menu name or ? for a list of options) |
| Ctrl+g | Cancel current operation (or menu) |
| f | Cross reference (type cross reference name or ? for a list of options) |
| d | Show a directory of all the documents info knows about |

Each page in an info document is called a node. A node can contain menus and cross-references. Menus are related nodes within the same document. Cross-references are nodes typically located in a different document.

The easiest way to learn how to use info is to go through its interactive tutorial. To access the tutorial, enter info at the command prompt, and type h to follow instructions. On Emacs you can enter info by typing Ctrl+h i.

# Usenet: Internet Newsgroups

If you have access to the Internet and newsgroups, there are many places where you can find information about Linux. The groups are organized according to topics. People all over the Internet post questions and answers to groups that fancy their interests.

There are thousands of newsgroups for all topics and interests. But with the aid of a good reader such as Netscape Communicator's Colabra, included with OpenLinux 1.3, you can cruise through several postings until you find what you want. (Do a man -k news to find console-capable news tools installed in your system.)

Some newsgroups are moderated. A moderated group has a posting reviewed by the group's maintainer, who then decides if your post merits distribution.

Usenet newsgroups are full of noise, because a lot of users post blindly without doing their own research into the problem. If you have looked at all the resources mentioned in this chapter and you still don't have a solution to the problem, it probably is a valid question.

When posting a question, it is always a good idea to put the version and distribution of your software, and then the tool that you are having a problem with (include version information). Sometimes different software versions can determine what the correct answer is to your question. Be brief but descriptive, and only ask one question per message.

Some of the Linux groups follow:

- comp.os.linux.advocacy—A newsgroup dedicated to flame on why Linux is better than other OSs.
