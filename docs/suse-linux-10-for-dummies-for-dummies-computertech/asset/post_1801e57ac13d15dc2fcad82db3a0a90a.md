
This runs the uname command with three options -s, -r, and -v (these can be combined as -srv, as this example shows). The -s option causes uname to print the name of the kernel, -r prints the kernel release number, and -v prints the kernel version number. The command generates the following output on one of my Linux systems:

```text
Linux 2.6.13-8-default #1 Tue Sep 6 12:59:22 UTC 2005
```

In this case, the system is running Linux kernel version 2.6.13.

To read a file, use the more command. Here’s an example that displays the contents of the /etc/passwd file:

```text
more /etc/passwd

root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/bin/bash
daemon:x:2:2:Daemon:/sbin:/bin/bash
lp:x:4:7:Printing daemon:/var/spool/lpd:/bin/bash
... lines deleted ...
```

To see a list of all the programs currently running on the system, use the ps command, like this:

```text
ps ax
```

The ps command takes many options, and you can provide these options without the usual dash (-) prefix. This example uses the a and x options — the a option lists all processes that you are running, and the x option displays all the rest of the processes. The net result is that ps ax prints a list of all processes running on the system, as shown in the following sample output:

```text
  PID TTY          STAT     TIME COMMAND
    1 ?             S       0:01 init [5]
    2 ?             SN      0:10 [ksoftirqd/0]
    3 ?             S<      0:00 [events/0]
    4 ?             S<      0:00 [khelper]
    9 ?             S<      0:00 [kthread]
   19 ?             S<      0:00 [kacpid]
   75 ?             S<      0:02 [kblockd/0]
... lines deleted ...
```

Amazing how many programs can run on a system even when only you are logged in as a user, isn’t it?

As you can guess, you can do everything from a shell prompt, but it does take some getting used to.

## Shutting Down

When you’re ready to shut down Linux, you must do so in an orderly manner. Even if you’re the sole user of a SUSE Linux PC, several other programs are usually running in the background. Also, operating systems such as Linux try to optimize the way that they write data to the hard drive. Because hard drive access is relatively slow (compared with the time needed to access memory locations), data generally is held in memory and written to the hard drive in large chunks. Therefore, if you simply turn off the power, you run the risk that some files aren’t updated properly.

Any user (you don’t even have to be logged in) can shut down the system from the desktop or from the graphical login screen. In KDE, choose Main Menu→Log Out. In GNOME, choose Desktop→Log Out. A dialog box appears (Figure 3-8 shows the example from the KDE desktop), providing the options for restarting or turning off the system, or simply logging out. To shut down the system, simply select Turn Off Computer (or Shut Down in GNOME), and click OK. The system then shuts down in an orderly manner.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_67_0.png)

**Figure 3-8:** Shutting down your SUSE Linux system from the KDE desktop.

If you are at the graphical login screen, you can shut down the system by selecting the shutdown option from the menus available at the login screen.

As the system shuts down, you see text messages about processes being shut down. You may be surprised at how many processes exist, even when no one is explicitly running any programs on the system. If your system does not automatically power off on shutdown, you can manually turn off the power.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_68_0.png)

Note that shutting down or rebooting the system may not require root access or even the need to log in to the system. This is why it’s important to make sure that physical access to the console is protected adequately so that anyone who wants to cannot simply walk up to the console and shut down your system.

## Chapter 4

## Taking Stock of What’s New in SUSE

### In This Chapter

- Discovering the Internet applications
- Introducing the office applications
- Exploring the multimedia applications
- Reviewing the images and graphics applications

SUSE Linux comes with a whole lot of applications. All you have to do is look at the menus on the GUI desktops to see what I mean. Often you find more than one application of the same type. For example, in the KDE desktop, you can take your pick from two Web browsers — Firefox and Konqueror.

Depending on the desktop — KDE or GNOME — that you installed by following the steps outlined in Chapter 2, you get a different set of applications. Both desktops include the OpenOffice.org office application suite with a word processor, spreadsheet, presentation software, and more. You find many choices for CD players and multimedia players, not to mention the games, utility programs, and useful tools, such as a digital camera and image-editing applications.

In this chapter, I provide a quick listing of some common SUSE Linux applications. After you get familiar with these applications, you can explore them further and use them when you need them. I cover many of these applications in greater detail in Chapters 8 through 14.

I mention only the default applications installed with each GUI desktop — GNOME and KDE. You can, however, use YaST to find and install many more applications. Chapter 17 provides an overview of YaST.

![](img/b7e91b81e0d84c8a5261ee14a48991b2_69_0.png)

## Discovering the Internet Applications

Internet applications are for doing tasks such as browsing the Web, reading and sending e-mail, reading newsgroups, and downloading files. From your SUSE desktop — both KDE and GNOME — you can get to these applications by selecting the Internet menu from the Main menu.

You get different sets of default Internet applications depending on whether you installed the KDE or GNOME desktop. Table 4-1 lists the default Internet applications for GNOME and KDE desktops.

I describe the Internet applications in detail in Chapters 8 through 11.

| Application Category | GNOME Desktop | KDE Desktop |
|---|---|---|
| Chat (instant messaging) | GAIM, Gnome Jabber, Xchat | Kopete |
| Web browser | Firefox, Mozilla, Epiphany | Konqueror |
| E-mail | Novell Evolution | KMail |
| News reader | Pan | KNode |
| RSS feed reader | Blam | Akregator |
| Videoconference and IP telephone | GnomeMeeting, Linphone | KPhone, Linphone |

Here’s what you can do with these applications:

- **Chat (instant messaging)** applications enable you to communicate with other people on the Internet — it’s like a phone call with many people at the same time, only you type your messages instead of speaking. America Online (AOL) provides a popular instant messaging (IM) service called AIM. With the chat applications in SUSE, you can talk to people on many different IM services such as AIM, ICQ, and Microsoft's MSN. On the GNOME desktop, you have a choice of several IM applications such as GAIM, Gnome Jabber, and XChat. On the KDE desktop, use Kopete for your IM needs.

- **Web browsing** applications are, well, for browsing the Web. On the GNOME desktop, you can take your pick from three Web browsers — Mozilla, Epiphany, and the up-and-coming Firefox with its reputation as the “faster, better Web browser.”

- **E-mail applications** are for sending and receiving electronic mail. You need an e-mail account with an ISP to use these applications. If you use the GNOME desktop, your best bet for an e-mail inbox is Novell Evolution — a multipurpose application that integrates e-mail, calendaring, to-do lists, and contact management in a single application. On the KDE desktop, your e-mail client is KMail.

- **News readers** enable you to read Usenet newsgroups, which are like bulletin boards where people post messages. Anyone can read and respond to the messages. Like e-mail, you need access to your ISP’s server to read newsgroups. The GNOME desktop provides the Pan news reader; on KDE, use the KNode application to read newsgroups.

- **RSS feed readers** enable you to subscribe to the content of Web sites and blogs that are made available in Really Simple Syndication (RSS) format. The RSS format, which is a dialect of XML (extensible markup language), is used for syndicating — gathering and making available — content of Web sites, primarily news-oriented sites and blogs. RSS-formatted content is called an RSS feed, and an RSS-aware program can check the feed periodically for changes, download new items, and make them available to the user. KDE comes with the Akregator RSS feed reader. GNOME uses the Blam RSS reader from Imendio AB, a small European company.

- **Videoconference and IP telephone applications** are for making phone calls and running videoconferences (think of videoconferences as “picture phones” where you can see and be seen by other participants as you talk). The GNOME desktop includes the GnomeMeeting videoconferencing application. GnomeMeeting conforms to a standard called H.323, which means it can work with other H.323-compliant videoconferencing software such as Microsoft Netmeeting. Besides GnomeMeeting, the GNOME desktop also includes Linphone for making voice calls over the Internet. The KDE desktop includes both KPhone and Linphone IP telephony applications. KPhone and Linphone conform to the Session Initiation Protocol (SIP), which is widely used for voice over IP telephone calls.

## Introducing the Office Applications

By *office applications*, I mean software for word processing, spreadsheets, presentations (briefing slides), calendars, and managing contacts. You can, of course, think of the Internet applications — at least e-mail and Web browser — as office applications as well, but I am differentiating between the applications that need the Internet to work versus the ones you may use on stand-alone PCs.

Regardless of your desktop — KDE or GNOME — OpenOffice.org is the primary office application suite in SUSE Linux. OpenOffice.org includes several
