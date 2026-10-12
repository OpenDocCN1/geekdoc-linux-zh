
## Using Mozilla Mail

![](img/9f89727199836b0f871f1745838aa8b2_374_0.png)

### Composing and sending messages

To send an e-mail message, you either write a new message or reply to a message you are reading. The general steps for sending an e-mail message are as follows:

1. To reply to a message, click the Reply or Reply All button on the toolbar as you are reading the message. To write a new message, click the Compose button on the toolbar. To forward a message, click the Forward button.
   A message composition window appears (as shown in Figure 1-9).
2. In the message composition window, fill in the subject line and type your message.
   The message can include links to Web sites and images. To insert any of these items, choose Insert➔Link or Insert➔Image from the menu.
3. If you're creating a new message or forwarding a message, type the e-mail addresses of the recipients.
   To select addresses from the Address Book, click the Address button on the toolbar. Your Address Book opens, from which you can select the addresses.
4. When you're done composing the message, click the Send button.
   Mozilla Mail asks whether you want to send the message in HTML format or plain text or both.
5. Select a format and then click Send to send the message.
   If you inserted images and Web links and you know the recipient can read HTML mail, be sure to select HTML format; otherwise, choose plain text.

![](img/9f89727199836b0f871f1745838aa8b2_375_0.png)

TIP
If you want to complete a message later, click **Save** in the message composition window and then close the window. Mozilla Mail saves the message in the Drafts folder. When you're ready to work on that message again, go to the Drafts folder and then double-click the saved message to open it.

## Instant Messaging with Gaim

You can use Gaim to keep in touch with all of your buddies on AOL Instant Messenger (*or AIM*, as it's commonly known). If you use AOL's AIM, you'll be right at home with Gaim, a client for the AOL AIM service. You need an AOL AIM screen name to use Gaim.

Start Gaim by choosing **Main Menu\*\* Internet\*\*\* Messaging Client** from the GNOME desktop. The initial Gaim window appears (see Figure 1-10).

If you've used AIM before, you already have a screen name. Just type it in, enter the password, and then click the **Sign On** button. Gaim logs you in and opens the standard Buddy List window. The Buddy List is initially empty. To add buddies, select Buddies:C Add a Buddy. In the Add Buddy window that appears, enter the screen name of the buddy and click Add. To create a new group, choose Buddies:C Add a Group. Type the name of the new group in the Add Group window that appears and then click Add.

![](img/9f89727199836b0f871f1745838aa8b2_376_0.png)

**Figure 1-10:** Sign on to AIM with Gaim.

If any of your buddies are online, their names show up in the Buddy List window. To send a message to a buddy, double-click the name and a message window pops up. If someone sends you a message, a message window pops up with the message and you can begin conversing in that window.

Well, if you know AIM, you know what to do: Have fun IMing with Gaim!

# Chapter 2: Using the Web

## In This Chapter

- Discovering the World Wide Web
- Understanding a URL
- Checking out Web servers and Web browsers
- Web browsing with Mozilla
- Creating Web pages with Mozilla Composer

I suspect you already know about the Web, but did you know that the Web, or more formally the World Wide Web, made the Internet what it is today? The Internet was around for quite a while, but it did not reach the masses until the Web came along in 1993.

Before the Web came along, you had to use arcane UNIX commands to download and use files, which was simply too complicated for most of us. With the Web, however, anyone can enjoy the benefits of the Internet by using a Web browser—a graphical application that downloads and displays Web documents. A click of the mouse is all you need to go from reading a document from your company Web site to downloading a video clip from across the country.

In this chapter, I briefly describe the Web and introduce Mozilla—the primary Web browser (and, for that matter, mail and newsreader, too) in Fedora Core. I also briefly discuss how you can create your own Web pages.

## Discovering the World Wide Web

If you have used a file server at work, you know the convenience of sharing files. You can use the word processor on your desktop to get to any document on the shared server.

Now imagine a word processor that enables you to open and view a document that resides on any computer on the Internet. You can view the document in its full glory, with formatted text and graphics. If the document makes a reference to another document (possibly residing on yet another computer), you can open that linked document by clicking the reference. That kind of easy access to distributed documents is essentially what the World Wide Web provides.

![](img/9f89727199836b0f871f1745838aa8b2_378_0.png)

Of course, the documents have to be in a standard format, so that any computer (with the appropriate Web browser software) can access and interpret the document. And a standard protocol is necessary for transferring Web documents from one system to another.

The standard Web document format is *HyperText Markup Language* (HTML), and the standard protocol for exchanging Web documents is *HyperText Transfer Protocol* (HTTP). HTML documents are text files and don’t depend on any specific operating system, so they work on any system from Windows and Mac to any type of UNIX and Linux.

![](img/9f89727199836b0f871f1745838aa8b2_378_1.png)

A *Web server* is software that provides HTML documents to any client that makes the appropriate HTTP requests. A *Web browser* is the client software that actually downloads an HTML document from a Web server and displays the contents graphically.

### Like a giant spider’s web

The World Wide Web is the combination of the Web servers and the HTML documents that the servers offer. When you look at the Web in this way, the Web is like a giant book whose pages are scattered throughout the Internet. You use a Web browser running on your computer to view the pages — the pages are connected like a giant spider’s web, with the documents everywhere (shown in Figure 2-1).

![](img/9f89727199836b0f871f1745838aa8b2_378_2.png)

Imagine that the Web pages — HTML documents — are linked by network connections that resemble a giant spider’s web, so you can see why the Web is called “the Web.” The “World Wide” part comes from the fact that the Web pages are scattered around the world.

## Links and URLs

Like the pages of real books, Web pages contain text and graphics. Unlike real books, however, Web pages can include multimedia, such as video clips, sound, and links to other Web pages that can actually take you to those Web pages.

The *links* in a Web page are references to other Web pages that you can follow to go from one page to another. The Web browser typically displays these links as underlined text (in a different color) or as images. Each link is like an instruction to you — something like, “For more information, please consult Chapter 4,” that you might find in a real book. In a Web page, all you have to do is click the link; the Web browser brings up the referenced page, even though that document may actually reside on a far-away computer somewhere on the Internet.

![](img/9f89727199836b0f871f1745838aa8b2_379_0.png)

The links in a Web page are referred to as *hypertext* links because when you click a link, the Web browser jumps to the Web page referenced by that link.

This arrangement brings up a question. In a real book, you might ask the reader to go to a specific chapter or page in the book. How does a *hypertext* link indicate the location of the referenced Web page? In the World Wide Web, each Web page has a special name, called a *Uniform Resource Locator* (URL). A URL uniquely specifies the location of a file on a computer. Figure 2-2 shows the parts of a URL.

![](img/9f89727199836b0f871f1745838aa8b2_379_1.png)
