
![](img/12d790664598bbf390261087fbe55bbc_83_0.png)

Of course, your e-mail settings will be different from any other user’s. However, to assist you in following along, this text used the author’s e-mail settings as an example. This also will help should you want to e-mail the author. The first screen asks you to enter your full name and your e-mail address. You also can connect to a signature file. A signature file can be either a text document or an HTML document that contains a signature block you would like to appear at the bottom of all of your outgoing e-mails. This screen is shown in Figure 4.29.

![](img/12d790664598bbf390261087fbe55bbc_83_1.png)

The next screen asks you to enter information about your incoming e-mail servers. The e-mail server is a machine at your ISP or in your company that handles incoming and outgoing e-mail. The overwhelming majority of e-mail servers use Post Office Protocol (POP) for incoming e-mail, and it usually works on port 110. POP is simply the protocol that computers use to receive e-mail. Some computers use a protocol called IMAP. Conversely, all computers use Simple Mail Transfer Protocol (SMTP) to send e-mail, and that protocol works on port 25. You will find that there is a protocol for every type of communication between one computer and another. The e-mail server screen is seen in Figure 4.30. The screens for setting up your SMTP server and POP server are identical.

![](img/12d790664598bbf390261087fbe55bbc_84_0.png)

**Figure 4.30**: Your incoming e-mail server.

The next screen, shown in **Figure 4.31**, asks your preferences regarding checking e-mail. You are asked to indicate how often you want to check for new e-mail and whether to leave a copy on the server. This means that even after you read your e-mail, it is still on the server. This is usually preferred by people who might check their e-mail from more than one machine. If you leave the e-mail on the server, you can access it from any e-mail client on any machine. Of course, if you get a large volume of e-mail, this volume might exceed limits that your ISP or network administrator has set on your e-mail inbox.

![](img/12d790664598bbf390261087fbe55bbc_84_1.png)

**Figure 4.31**: Preferences for receiving e-mail.

The following screen, shown in **Figure 4.32**, is to set up your outgoing e-mail. Recall that we previously mentioned that e-mail is sent using SMTP, which usually works on port 25.

![](img/12d790664598bbf390261087fbe55bbc_85_0.png)

The next two screens have you enter your e-mail address and select your time zone. You are now ready to start using the Evolution e-mail client. In fact, you will be taken to the main e-mail client screen, shown in Figure 4.33. In the future, when you launch the e-mail client, you will go directly to this screen.

![](img/12d790664598bbf390261087fbe55bbc_85_1.png)

You can see that using Evolution for your e-mail client will be no more difficult that using Microsoft Outlook® or Outlook Express®. In fact, the initial setup is considered easier by many people. This is just one of many alternative applications that were mentioned in previous chapters.

There is an option you may have noticed, called Leave messages on server. This is just a little check box that you either check or uncheck. It simply directs the e-mail software to leave the e-mail on the server, even after you have read it. If you intend to check your e-mail from more than one PC or e-mail client, then you may wish to leave the e-mail on the server. If you don't, then when you log on with another e-mail program, you won't see any of your e-mails. You might think they are gone! However, they were simply downloaded by the e-mail client Evolution.

Note The option of whether or not to leave e-mail on the server is hardly unique to Evolution. You are likely to find that option somewhere in almost any e-mail client program you may choose to use.

< Day Day Up >

PREV

NEXT

# Summary

This chapter took you through the fundamentals of administering and configuring your Linux PC. You have seen how to get connected to the Internet, how to configure your browser, and how to configure your e-mail. These are critical tasks because most people are particularly interested in Internet access.

In addition to establishing Internet access, you have also seen how to configure your desktop preferences, the look and feel for your desktop, and how to set up and use the multiple desktop feature of KDE. You have also been shown where to find hardware settings.

# Review Questions

- 1. What are the three most common means of Internet connection?
- 2. How many different desktops does KDE provide, by default?
- 3. Under desktop settings, what does the common background setting do?
- 4. What is the rule of thumb for changing hardware settings?
- 5. What is the default browser for KDE?
- 6. What drop-down menu do you select in Mozilla to set up your Internet connection settings?
- 7. What is the default e-mail client for KDE?
- 8. Favorites in Internet Explorer are called what in Mozilla?

# Answers

- 1. Modem, Ethernet, and cable/DSL
- 2. Four
- 3. It forces all the various desktops to use the same background.
- 4. If you do not know what it is, do not touch it!
- 5. Mozilla
- 6. Edit
- 7. Evolution
- 8. Bookmarks

# Chapter 5: Using KDE for Everything You Used to Do in Windows

# Overview

# In This Chapter

- Text Editors
- Calculators
- Paint Programs and Screen Capture
- The File Manager
- Accessibility
- Other Office Applications

# Introduction

The first four chapters of this book took you through the fundamentals of Linux. At this point, you should have a solid grasp of essential Linux terminology, know how to install Linux, and know how to do some basic configuration of your system. These are the essential functions you will need in order to progress with Linux. The Linux terminology is critical to being able to understand Linux articles and books, use online tutorials, or simply communicate with other Linux users. The capability to install and configure a system is absolutely essential to being able to use that system. However, these are not the things that most users do on a day-to-day basis. You generally install Linux on a PC only one time. You will usually only change the system’s configuration when some pressing need arises, such as if you change your hardware or a person with different requirements will use the machine. This brings us to this chapter. In this chapter, we will explore some basic, common tasks that most people will use on a frequent basis.

This chapter will show you how the most commonly used functions in Windows can be accomplished in Linux. The point is to take those common functions you formerly accomplished in Windows and translate them into Linux. We will walk through many of the basic tasks that typical users will do. This should take you to the point that you can start using Linux productively. The tasks we will examine will include using basic text editors to write documents, finding calculators, using a contact manager, and screen captures. In most cases, we will discuss briefly how the task is done in Windows and then show you how to accomplish the same task in Linux.

The applications and utilities we will deal with in this chapter come with the KDE user interface. If you will recall from Chapter 2, “Installing Linux,” during the installation process you were asked to select the KDE interface as your default mode of using Linux. KDE has a similar feel to Windows, so it should be no surprise that KDE offers a number of applications that are quite similar to Windows applications. This chapter will review the use of some of the more common of these utilities.

# Text Editors

The first question we should address is, what is a text editor? A text editor is a program that enables you to enter text, alter it, and save it. In short, it is a program that enables you to edit text. To quote from a popular online Unix help page, www.gw.com/UNIXhelp/editors, “you will often want to create a text file and then change its content in some way. A text editor is a program that has been designed especially for this purpose.” Text editors enable you to enter text and change the content. They generally don’t have advanced formatting or processing capabilities that you find in word processors. A simplified definition might be that a text editor is a very simple word processor. Linux is not limited to text editors. In fact, there are several complete word processors and office suites available for Linux. You can choose from Star Office, Open Office, Corel Word Perfect, and others. All of these are comparable with Microsoft Word. We will look at Open Office extensively later in this book. In fact, several chapters are devoted to Open Office. However, you may be used to having access to simpler text editors that you use for smaller, less demanding tasks. In Windows, you can go to Start, choose Programs (in Windows 2000 or 98 it was Programs, in Windows XP , it is All Programs), then select Accessories, and you immediately have access to both Microsoft Notepad and WordPad. Notepad is a very limited text editor. With Notepad you can essentially type in plain text with no formatting options. You can then either save the file or print it. WordPad, while not as feature rich as most commercially available word processors, does include basic word processing features. It is more than adequate for most simple word processing tasks. Simplified word processing applications such as Notepad and WordPad often are called text editors. The difference between a text editor and a word processor is the additional tools available in a word processor. However, there is no accepted demarcation line that indicates when some application is considered a word processor, versus when it is considered a text editor. Some purists would comment that a text editor is entirely separate from a word processor, and at one time that would have been accurate. However, more and more text editors are adding enhanced formatting to their capabilities, and more and more simplified word processors are being released. This has caused the line between text editor and word processor to be blurred considerably.

Now that we have discussed what a text editor is and mentioned some text editors found in Windows, you might be wondering if Linux also has some text editor applications for you to use. The answer is a resounding yes. In fact, when using the KDE graphical interface, you have a few different text editors to choose from.

We also have mentioned that Linux ships with full-fledged word processors. This might lead you to ask why would you use a text editor? There actually are several reasons. The first is that if you want a very simple tool to just type in text, a word processor might have more complexity than the situation warrants, especially if you are not overly familiar with that word processor. Text editors also are useful when you want to enter text that has no formatting at all. If you enter your own HTML code for Web pages, code for compilers, or just shell scripts (which we will do in Chapter 21, “Advanced Shell Functions”), then you need text with no formatting at all. Many word processors add formatting that may cause problems when you attempt to use the resulting text as a script or in a compiler. Finally, these text editors are so common in the Linux world that it would be a glaring omission not to introduce you to them.

Now you know what a text editor is, and you know some of the reasons why you might use one. We will now take a look at a few of the more common text editors you have access to in Linux.

# Kate

The KDE interface comes with a text editor called *Kate*. Other graphical interfaces (such as GNOME) may have a very similar application called simply *Text Editor*. Whatever your distribution of Linux calls it, it is found in the same place and functions pretty much the same. Kate is a very simple text editor that enables you to enter text and to save that file to some location. It does not enable you to alter fonts or do any type of formatting. With Kate, you cannot align text, insert images, or draw tables and graphs. Kate is limited to entering plain text and saving or printing that text. It is quite a bit like Microsoft Notepad in that regard. To launch Kate, you would to go the K (recall that we mentioned earlier that depending on your distribution, you might have a capital K in the lower left-hand corner of your taskbar, or a red hat), find Accessories and select Kate (or select Text Editor). You should then see something very much like what is seen in Figure 5.1. Enter your text, then select File from the drop-down menu and Save As. You will then be able to save your file with any valid name you want, in any location you choose.
