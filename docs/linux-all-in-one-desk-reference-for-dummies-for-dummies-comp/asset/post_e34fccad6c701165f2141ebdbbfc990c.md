
![](img/11709a8f88c8cd03868a929dc94c0e2b_351_0.png)

Figure 1-7: The initial KMail window

![](img/11709a8f88c8cd03868a929dc94c0e2b_351_1.png)

Figure 1-8: Configure e-mail accounts in the Configure KMail window.

To set up the incoming mail information, click Add on the Receiving tab, and select the mail protocol, such as POP3 or IMAP. Your ISP would have told you what protocol to use. (Typically, it’s POP3 or IMAP.) Then enter the mail server’s name (for example, mail.concast.net) as well as the username and password of your ISP account.

After the e-mail account information is set up, you can start using KMail. The user interface is intuitive and similar to other mail readers such as Thunderbird and Evolution. KMail periodically checks and downloads messages from your incoming mail accounts. You can view messages as they arrive in your Inbox.

## Instant Messaging in Linux

There are two major IM clients in Linux. In GNOME desktops, you can use Gaim, whereas Kopete is designed to work well on KDE desktops. I briefly describe both IM clients in the following sections.

### Using Gaim

You can use Gaim to keep in touch with all of your contacts on many different IM services, such as AIM, ICQ, Yahoo!, MSN, Gadu-Gadu, and Jabber. If you use any of the IM services, you’ll be right at home with Gaim.

![](img/11709a8f88c8cd03868a929dc94c0e2b_352_0.png)

In Fedora Core, start Gaim by choosing Applications → Internet → Messaging Client from the GNOME desktop. You can start Gaim in a similar manner from GNOME desktops in other distributions. The initial Gaim window appears together with an Accounts window, as shown in Figure 1-9.

![](img/11709a8f88c8cd03868a929dc94c0e2b_352_1.png)

**Figure 1-9:** Manage all of your IM accounts in this window.

Start by setting up your messaging accounts in the Accounts window. Click the Add button and fill in the requested information in the Add Account window, as shown in Figure 1-10. You have to select the protocol for your IM service. For example, the protocol for AIM is AIM/Icq. Other protocol choices include Gadu-Gadu, Jabber, MSN, and Yahoo!.

![](img/11709a8f88c8cd03868a929dc94c0e2b_353_0.png)

Figure 1-10: Enter information about each IM account.

After you enter account information, the Accounts window shows all currently defined accounts. You can then select an account from the Gaim main window and click Sign On, as shown in Figure 1-11.

![](img/11709a8f88c8cd03868a929dc94c0e2b_353_1.png)

Figure 1-11: Sign on to AIM with Gaim.

After Gaim logs you in, it opens the standard Buddy List window. (See Figure 1-12.)

![](img/11709a8f88c8cd03868a929dc94c0e2b_354_0.png)

Figure 1-12: A buddy list window in Gaim.

To add buddies, choose Buddies → Add Buddy. In the Add Buddy window that appears, enter the screen name of the buddy and click Add. To create a new group, choose Buddies → Add Group. Type the name of the new group in the Add Group window that appears and then click Add.

If any of your buddies are online, their names show up in the Buddy List window. To send a message to a buddy, double-click the name and a message window pops up. If someone sends you a message, a message window pops up with the message and you can begin conversing in that window.

### Using Kopete

Kopete — the KDE IM client — enables you to connect to many messaging services including AIM, IRC, MSN Messenger, Yahoo!, Gadu-Gadu, and SMS.

You can start Kopete by choosing Chat or Instant Messaging in the applications menu in Debian, SUSE, and Xandros.

When you first run Kopete, you get the Configure Kopete window (see Figure 1-13), where you can enter information about your IM and other messaging service accounts.

For example, to add your AIM account information, click New and then answer and respond to the prompts from the Account Wizard. The first step is to select your messaging service. (See Figure 1-14.)

![](img/11709a8f88c8cd03868a929dc94c0e2b_354_1.png)

## Book IV

### Chapter 1

#### E-Mailing and IMing in Linux

![](img/11709a8f88c8cd03868a929dc94c0e2b_355_0.png)

Figure 1-13: Enter information about your messaging accounts in this window.

Select the appropriate messaging service, such as AIM if you use AOL’s instant messaging service. Then provide the AIM screen name and the password.

![](img/11709a8f88c8cd03868a929dc94c0e2b_355_1.png)

Figure 1-14: Select your messaging service in this window.

After you set up your messaging service accounts, the Account Wizard closes and you get the regular Kopete window. To sign on with your messaging services and begin using Kopete, click the Connect button — the leftmost button on the toolbar — in the Kopete window. (See Figure 1-15.)

![](img/11709a8f88c8cd03868a929dc94c0e2b_356_0.png)

**Figure 1-15:** Viewing a buddy list in Kopete.

Click the magnifying-glass icon to see your buddies. You see a solid smiley face icon for buddies who are online. Right-click an online buddy and select Start Chat from the menu to start chatting. Choose File ➪ Add Contact to add more contacts.

Well, if you know AIM, you know what to do: Have fun IMing with Kopete!

## Chapter 2: Browsing the Web

### In This Chapter

- Discovering the World Wide Web
- Understanding a URL
- Checking out Web servers and Web browsers
- Taking stock of Web browsers for Linux
- Web browsing with Mozilla Firefox

I suspect you already know about the Web, but did you know that the Web (or more formally, the World Wide Web) made the Internet what it is today? The Internet has been around for quite a while, but it didn't reach the masses until the Web came along in 1993.

Before the Web came along, you had to use arcane UNIX commands to download and use files, which was simply too complicated for most of us. With the Web, however, anyone can enjoy the benefits of the Internet by using a Web browser — a graphical application that downloads and displays Web documents. A click of the mouse is all you need to go from reading a document from your company Web site to downloading a video clip from across the country.

In this chapter, I briefly describe the Web and introduce Mozilla Firefox — the primary Web browser (and, for that matter, mail and newsreader, too) in most Linux distributions. I also briefly discuss how you can create your own Web pages.

> KDE desktops often use Konqueror as the Web browser, but after you have used one Web browser, you can easily use any other Web browser.

### Discovering the World Wide Web

If you have used a file server at work, you know the convenience of sharing files. You can use the word processor on your desktop to get to any document on the shared server.

Now imagine a word processor that enables you to open and view a document that resides on any computer on the Internet. You can view the document in its full glory, with formatted text and graphics. If the document makes a reference to another document (possibly residing on yet another computer), you can open that linked document by clicking the reference. That kind of easy access to distributed documents is essentially what the World Wide Web provides.

Of course, the documents have to be in a standard format, so that any computer (with the appropriate Web browser software) can access and interpret the document. And a standard protocol is necessary for transferring Web documents from one system to another.

- **TECHNICAL STUFF**
  The standard Web document format is *HyperText Markup Language* (HTML), and the standard protocol for exchanging Web documents is *HyperText Transfer Protocol* (HTTP). HTML documents are text files and don't depend on any specific operating system, so they work on any system from Windows and Mac to any type of UNIX and Linux.

- **REMEMBER**
  A *Web server* is software that provides HTML documents to any client that makes the appropriate HTTP requests. A *Web browser* is the client software that actually downloads an HTML document from a Web server and displays the contents graphically.

### Like a giant spider's web

The World Wide Web is the combination of the Web servers and the HTML documents that the servers offer. When you look at the Web in this way, the Web is like a giant book whose pages are scattered throughout the Internet. You use a Web browser running on your computer to view the pages — the pages are connected like a giant spider's web, with the documents everywhere, as illustrated in Figure 2-1.

![](img/11709a8f88c8cd03868a929dc94c0e2b_359_0.png)
