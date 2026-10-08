
# Chapter 9: Migrating from Windows Systems

- *DOC, XLS, PPT*: You can use the OpenOffice.org tools to open the files that are created by Microsoft Office applications. Microsoft's new XML-oriented DOCX, XLSX, and related formats are only supported by OpenOffice.org version 3.0 (and greater) tools.
- PDF files: Ubuntu uses the Evince application to display PDF files. This application does not enable you to edit PDF files, or edit forms, and so on. Most Ubuntu applications enable you to create PDF files by selecting the "Print to File" option and specifying PDF output. The pdfedit application, which can be found in the Ubuntu repositories, can be used to edit existing PDF files.

As you can see, this list could go on forever. For a summary of the Linux applications that are equivalent to Windows applications, see sites such as the following:

- Linux Alternatives Project: www.linuxalt.com
- Linux Application Finder: www.linuxappinder.com/alternatives
- Linux equivalents to Windows software: www.linuxlinks.com/article/2007070111340544/Equivalents.html
- Linux software equivalent to Windows software: http://wiki.linuxquestions.org/wiki/Linux_software_equivalent_to_Windows_software
- Table of Equivalents/Replacements/Alternatives of Windows software in Linux: www.linuxrsp.org/win-lin-soft/table-eng.html

In addition to these Linux-specific sites, the Open Source Alternatives site (www.osalt.com) lists equivalent applications for Windows software that run on other open source operating systems (including Linux, of course).

For information about using emulation, virtualization, and similar techniques to enable you to run actual Windows software on your Ubuntu system, see Chapter 24, "Using Virtual Machines and Emulators." Yes, it can be done!

# Summary

The wealth of software available for Linux makes it quite conceivable to make Ubuntu your daily operating system—the one where you get all of your work done. But about browser favorites/bookmarks, and data files that you have accumulated on your existing Windows or Mac OS systems? This chapter explained different ways of migrating e-mail and browser settings from a Microsoft Windows or Mac OS system to an Ubuntu system, to facilitate migration, identified some tasks that you should do before doing your final backups, and discussed critical locations where applications such as Internet Explorer, Outlook, and Outlook Express store their data. It also discussed other considerations for complete migration to an Ubuntu system, such as making sure that you can find applications that will enable you to work with your existing data files.

Constant connectivity and interaction is almost an expectation today, and even classic software such as e-mail is viewed as being too slow and not interactive enough for many people. The next chapter discusses instant messaging on Ubuntu, which enables you to hold virtual conversations with friends regardless of their location—just like texting from your desktop!

# CHAPTER 10

## Sending and Receiving Instant Messages

E-mail has revolutionized how people communicate today. E-mail is the carrier of most business communications, replacing paper memos, faxes, and most information-sharing meetings, and enabling geographically disparate offices and personnel to keep in touch and know what each is doing. E-mail has revolutionized personalized communications. Thanks to e-mail, I've been able to maintain friendships that would otherwise have atrophied because I'm not the best letter writer or snail mail user. I can send e-mail at any time, from any computer, and know that it will be waiting for the recipient after a very short time.

"Waiting for the recipient," identifies a key shortcut of e-mail and a key advantage of instant messaging—the "instant" part. E-mail was designed as an asynchronous communications mechanism and does a great job at that. I can send e-mail and respond at your convenience. Unfortunately, "your convenience" isn't always good enough. If I have an extra ticket to a baseball game that starts in a few hours, I need to know whether you want it now. If you send an instant message to someone you are usually alerted that a new message has come in—you don't have to wait for them to get around to checking their mail.

A related issue is that e-mail isn't really convenience-oriented. If I send e-mail with several questions, I can respond to your e-mail at the top or inters your responses, a back-and-forth exchange of conversational messages quickly gets hard to read, at best.

Instant messaging, in which you can open a direct connection between one or more people and either send a single message or have an online conversation, has been around for a while, but is still increasing in popularity as both a personal and business communication mechanism. This

### IN THIS CHAPTER
- Instant messaging history
- Getting an IM account
- Using Empathy on Ubuntu
- Using Pidgin on Ubuntu
- Using IRC
- Other IM clients
- Troubleshooting

# Part II: Ubuntu for Desktop Users

chapter provides a little background on instant messaging, explains what you need to do in order to participate in instant messaging, discusses the most popular instant messaging clients on Ubuntu systems (Empathy, the new one; and Pidgin, the former and still-popular one), discusses Internet Relay Chat, and provides some tips on resolving instant messaging problems.

## Instant Messaging Overview

Believe it or not, people were actually online even before the Internet. Bulletin-board systems (commonly referred to as BBs) were a popular early personal computing phenomenon, consisting of computers running specialized, multi-user software that users could connect to using a modem, and on which users could read and send both public and private messages using a terminal-based interface. Many BBs also supported inter-BBS email by forwarding messages from one system to another using modems and forwarding networks such as FidoNet). Commercial dial-up/BBS services such as America Online (AOL), CompuServe, Prodigy, and many others provided centralized locations where people could share resources and, importantly, instant communicate with each other in shared areas, commonly referred to as chat rooms, conferences, or echoes (FidoNet), or online forums. As the availability, popularity, and amount of content on the Internet increased in the early 1990s, the reason for these centralized services became less important—after all, you could contact anyone via email and access the entire Internet, why bother limiting yourself to a single online community? The entire planet is your potential community.

As discussed in the introduction to this chapter, e-mail is cool but inherently messaging-oriented rather than conversation-oriented. UNIX and UNIX-like systems have had real-time communication software, starting with the `write` command in the original research edition of UNIX, which enabled you to immediately send a one-way message to another user on the terminal or other device that they used. Enhanced versions of the write command, such as Orville Write—`http://unixappa.com/write.html`—supported multi-user and multi-way communication, but were not part of the standard UNIX distribution.

Early UNIX also provided the talk command, which enabled you to have real-time text conversations between two users by splitting your terminal window into two sessions in which you could exchange messages back and forth. (I'm told the first version intermingled text as both users typed, but I'm not quite that old). I remember using the talk command in the early 1990s to help an acquaintance in Australia debug some problems that I was having with one of my machines, while I sat in my office in Pittsburgh. Good times...

Outside the UNIX-only universe, the increased availability of the Internet led to the development of many cross-platform and admittedly friendlier instant communication mechanisms. The idea of a shared, instant communication area is always attractive for its immediacy. Internet-based instant communication was born in 1988 with the creation of IRC (Internet Relay Chat), written by Jarkko Oikainen (www.ircnet.org/History/jarkko.html). IRC, in wide use today, enables instant communication between users by providing IRC channels (like chat rooms) that users connect to, at which point their messages are seen by anyone on the
