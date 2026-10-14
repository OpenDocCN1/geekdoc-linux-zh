

- Composer 图标—点击打开文本编辑器
dlike application you can use for designing your own Web pages.

要使用 Netscape 访问 Web，请调用一个 minicli 窗口（参见第 8 章“访问网络”中的“Mini Command Line”）并输入 `netscape`。你也可以从应用程序开始菜单下的 Applications 中访问 Netscape Communicator。几秒钟后，你会看到 Netscape 的一些面板，告诉你它正在为你创建配置文件以及放置缓存文件的位置。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_95_0.png)

Netscape 对 www.yahoo.com 网站的描绘。请注意信息的呈现方式与前一图不同。

Previous Table of Contents Next

## SPIDER KILLER

## spider catcher

- HOME
- ACCOUNT INFO
- SUBSCRIBE
- LOGIN
- SEARCH
- MY ITKNOWLEDGE
- FAQ
- SITEMAP
- CONTACT US

## SEARCH ITKNOWLEDGE

To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Bookmark it

Search this book:

- Previous
- Table of Contents
- Next

## FTP

FTP (File Transfer Protocol) is a protocol used to move files between computers. FTP under KDE is very simple: To go to a site, just enter an FTP URL in the location bar of a KFM window, like this:

```
ftp://somehost.somedomain.com
```

Somehost.somedomain.com is the fully qualified name of the machine you want to connect to. If that machine supports anonymous FTP, connections for which you don’t need a login and password, KFM will display the contents available at that location. To navigate, use KFM as if it was your local hard disk. You can copy files between your local machine and the server or from the server to your local machine by dragging and dropping files between KFM windows (see the next figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_96_0.png)

To FTP a file using KFM, type the URL for the FTP site and browse for the file you want. Then click and drag the file to your desktop or to another KFM window focused to your local computer.

Because some files you transfer will be large, the speed of the copy will be much slower than you normally experience. But don’t despair— the file will be transmitted across the wire.

## BROWSE BY TOPIC

If the server doesn’t allow anonymous connections, you’ll need to specify your login name, like this:

ftp://user@somehost.somedomain.com

user is your user name, followed by an at symbol (@), then followed by the fully qualified name of the machine. When you enter FTP URLs like this, more advanced programs raise a panel that asks you for your password.

You can also enter your password right in the URL; however, I don’t recommend that you do this, as the password might be displayed for other people to see in the URL. KFM removes the password from the URL when you have connected. To supply your password on the URL, enter it like this:

ftp://user:password@somehost.somedomain.com

The username and password are separated by a colon (:), like this:

ftp://me:mypassword@ftp.netscape.com

The same technique for accessing files using FTP can be used with a browser such as Netscape Navigator. To access the site, enter the URL, and you are delivered. Instead of clicking and dragging to move files across the network, just right-click on the link and choose the Save Link As command from the context-sensitive menu that is displayed. Use the Save panel that is displayed to navigate your way to the location where you want to save the file.

## Email

KDE provides an email program called kmail that you can use to read and write email messages. Although this program gets the job done, I am a little partial toward Netscape Messenger, as it provides more features than kmail. One nice feature of kmail over Netscape Messenger, however, is that kmail can manage multiple email accounts for you. Netscape allows you to set up multiple remote IMAP mailboxes but only a single POP mail account. Most users have several POP mailboxes. IMAP, though more powerful and useful to power users, is not as popular between ISPs. I also like having a spell-checker accessible right from the application, as Netscape Messenger offers. At the time of this writing, kmail doesn’t allow me to spell-check my messages. In this section, you will learn how to set up Netscape Messenger to handle your email.

Techno Talk: POP and IMAP? What’s that?

IMAP and POP are two different protocols used to access your email.

IMAP stands for Interactive Message Access Protocol. It allows you to manipulate and organize a remote mailbox as if it were local to your computer—and it does it without the need to transfer your entire mailbox to your computer. This is cool because your mailbox is then centralized on the network. No matter what computer you use and where you are, your entire mailbox is accessible. Many ISPs don’t like giving IMAP mailboxes, because users tend to collect copious amounts of email. For example, yours truly has an 80MB mailbox—yeah, there are things I should delete. But then again, disk space is cheap.

POP, which stands for Post Office Protocol, is a much simpler interface to

your mailbox. It doesn’t allow you to organize your inbox in any way, but it allows you to download your messages to a local mailbox for reading.

The process of setting up your email reader is very similar for most email applications. You will need to know the following:

- Your email address
- The type of email account that you have (IMAP or POP)
- The username and password needed to access your account
- The name of the machine where your incoming mail is stored
- The name for the SMTP (outgoing) mail server

Previous Table of Contents Next

To access the contents, click the chapter and section titles.

# Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Configuring Your Identity for Netscape Messenger

In the identity panel, you provide information that will be included in your email, such as your “real” name and your email address (see following figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_99_0.png)

Identity panel in Netscape Preferences.

## Configuring Your Mail Server

The next step in configuring your email program is to configure your mail servers so that Messenger can receive and send your email (see the following figure). Information to be entered here includes:

- Name of your email account (don’t put a domain name on it).
- Name of mail server that sends your mail (SMTP).
- Name of mail server that stores email sent to you.
- Type of mail server. If it’s a POP account, check whether if you want to leave incoming messages on the server (Otherwise messages are deleted from your ISP’s server after they are downloaded. If it’s an IMAP server, your mailboxes are kept on the server.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_100_0.png)

Messenger’s Mail Server Configuration panel stores information about sending and receiving your email.

## Reading Email

After configuring your identity and mail server settings, Messenger is ready to send and receive email. To start a Messenger session, choose the Messenger Mailbox command under the Communicator menu in a Navigator window. Messenger displays four main areas (from top to bottom):

- Menus and buttons—Access to commands and functions
- Mailboxes—Access to separate mailboxes
- Mailbox contents
- Message body

See the following figure for a description of the most important buttons and areas.

Different buttons in the Messenger window include:

- Get Msg—Click to download new messages.
- New Msg—Click to compose a new message.
- Reply—Click to reply to sender of the current message.
- Forward—Click to send a copy of the current message to another person.
- Delete—Click to delete the message from your mailbox.

You can also organize your messages into different boxes. To select a different message box, click the Inbox menu.

![](img/edf072a03d4de1f8f4a13465ac79e7fb_100_1.png)

The Netscape Messenger window.

## Composing an Email Message

Sending email is just as easy as reading email. To send a message, click the New Msg button (see the previous figure). This will present you with a window where you can compose and address an email message like the one shown in the following figure. When done composing a message, click Send Now to forward your email message to your mail server for delivery.

