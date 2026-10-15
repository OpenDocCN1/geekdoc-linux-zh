
要使用 Netscape 访问 Web，请调用一个`minicli`窗口（参见第 8 章“访问网络”中的“Mini Command Line”）并输入`netscape`。你也可以从应用程序开始菜单下的 Applications 中访问 Netscape Communicator。几秒钟后，你会看到 Netscape 的一些面板，告诉你它正在为你创建配置文件以及放置缓存文件的位置。

![](img/edf072a03d4de1f8f4a13465ac79e7fb_95_0.png)

Netscape 对`www.yahoo.com`网站的描绘。请注意信息的呈现方式与前一图不同。

Previous Table of Contents Next

# SPIDER KILLER

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

## Complete Idiot's Guide to Linux

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

`Somehost.somedomain.com` is the fully qualified name of the machine you want to connect to. If that machine supports anonymous FTP, connections for which you don’t need a login and password, `KFM` will display the contents available at that location. To navigate, use `KFM` as if it was your local hard disk. You can copy files between your local machine and the server or from the server to your local machine by dragging and dropping files between `KFM` windows (see the next figure).

![](img/edf072a03d4de1f8f4a13465ac79e7fb_96_0.png)

To FTP a file using `KFM`, type the URL for the FTP site and browse for the file you want. Then click and drag the file to your desktop or to another `KFM` window focused to your local computer.

Because some files you transfer will be large, the speed of the copy will be much slower than you normally experience. But don’t despair— the file will be transmitted across the wire.

### BROWSE BY TOPIC

If the server doesn’t allow anonymous connections, you’ll need to specify your login name, like this:

`ftp://user@somehost.somedomain.com`

`user` is your user name, followed by an at symbol (`@`), then followed by the fully qualified name of the machine. When you enter FTP URLs like this, more advanced programs raise a panel that asks you for your password.

You can also enter your password right in the URL; however, I don’t recommend that you do this, as the password might be displayed for other people to see in the URL. `KFM` removes the password from the URL when you have connected. To supply your password on the URL, enter it like this:

`ftp://user:password@somehost.somedomain.com`

The username and password are separated by a colon (`:`), like this:

`ftp://me:mypassword@ftp.netscape.com`

The same technique for accessing files using FTP can be used with a browser such as Netscape Navigator. To access the site, enter the URL, and you are delivered. Instead of clicking and dragging to move files across the network, just right-click on the link and choose the `Save Link As` command from the context-sensitive menu that is displayed. Use the Save panel that is displayed to navigate your way to the location where you want to save the file.

## Email
