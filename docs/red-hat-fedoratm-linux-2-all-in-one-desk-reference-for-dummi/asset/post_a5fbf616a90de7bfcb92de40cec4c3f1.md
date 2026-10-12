
# Web servers and Web browsers

As Figure 2-2 shows, a URL has the following parts:

- **Protocol:** Name of the protocol that the Web browser uses to access the data from the file the URL specifies. In Figure 2-2, the protocol is `http://`, which means that the URL specifies the location of a Web page. Here are some of the common protocol types and their meanings:
    - `file://` means the URL is pointing to a local file. You can use this URL to view HTML files without having to connect to the Internet. For example, `file:///var/www/html/index.html` opens the file `/var/www/html/index.html` from your Fedora Core system.
    - `ftp://` means you can download a file using the File Transfer Protocol (FTP). For example, `ftp://ftp.purdue.edu/pub/uns/NASA/nasa.jpg` refers to the image file `nasa.jpg` from the `/pub/uns/NASA` directory of the FTP server `ftp.purdue.edu`. If you want to access a specific user account via FTP, use a URL in the following form: `ftp://username:password@ftp.somesite.com/` with the username and password embedded in the URL (note that the password is in plain text and not secure).
    - `http://` means the file is downloaded using the HyperText Transfer Protocol (HTTP). This protocol is the well-known format of URLs for all Web sites, such as `http://fedora.redhat.com` for the Fedora Project’s home page. If the URL does not have a filename, the Web server sends a default HTML file named `index.html` (that’s the default filename for the popular UNIX-based Apache Web servers; Microsoft Windows Web servers use a different default filename).
    - `https://` specifies that the file is accessed through a Secure Sockets Layer (SSL) connection—a protocol designed by Netscape Communications for encrypted data transfers across the Internet. This form of URL is typically used when the Web browser sends sensitive information (such as credit card number, username, and password) to a Web server. For example, a URL such as `https://some.site.com/secure/takeorder.html` may display an HTML form that requests credit card information and other personal information (such as name, address, and phone number).
    - `mailto:` specifies an e-mail address you can use to send an e-mail message. This URL opens your e-mail program from where you can send the message. For example, `mailto:webmaster@someplace.com` refers to the Webmaster at the host `someplace.com`.
    - `news://` specifies a newsgroup you can read by means of the Network News Transfer Protocol (NNTP). For example, `news://news.md.comcast.giganews.com/comp.os.linux.setup` accesses the `comp.os.linux.setup` newsgroup at the news server `news.md.comcast.giganews.com`. If you have a default news server configured for the Web browser, you can omit the news server’s name and use the URL `news:comp.os.linux.setup` to access the newsgroup.

- **Domain name:** Contains the fully qualified domain name of the computer that has the file this URL specifies. You can also provide an IP address in this field. The domain name is not case sensitive.
- **Port:** Port number that is being used by the protocol listed in the first part of the URL. This part of the URL is optional; all protocols have default ports. The default port for HTTP, for example, is 80. If a site configures the Web server to listen to a different port, the URL has to include the port number.
- **Directory path:** Directory path of the file being referred to in the URL. For Web pages, this field is the directory path of the HTML file. The directory path is case sensitive.
- **Filename:** Name of the file. For Web pages, the filename typically ends with `.html`. If you omit the filename, the Web server returns a default file (often named `index.html`). The filename is case sensitive.
- **HTML anchor:** Optional part of the URL that makes the Web browser jump to a specific location in the file. If this part starts with a question mark (?) instead of a hash mark (#), the browser takes the text following the question mark to be a query. The Web server returns information based on such queries.

The Web server serves up the Web pages, and the Web browser downloads them and displays them to the user. That’s pretty much the story with these two cooperating software packages that make the Web work.

In a typical scenario, the user sits in front of a computer that’s connected to the Internet and runs a Web browser. When the user clicks a link or types a URL into the Web browser, the browser connects to the Web server and requests a document from the server. The Web server sends the document (usually in HTML format) and ends the connection. The Web browser interprets and displays the HTML document with text and graphics. Figure 2-3 illustrates this typical scenario of a user browsing the Web.

### 356 Web Browsing in Fedora Core

![](img/9f89727199836b0f871f1745838aa8b2_382_0.png)

The Web browser's connection to the Web server ends after the server sends the document. When the user browses through the downloaded document and clicks another hypertext link, the Web browser again connects to the Web server named in the hypertext link, downloads the document, ends the connection, and displays the new document. That's how the user can move from one document to another with ease.

A Web browser can do more than simply "talk" HTTP with the Web server — in fact, Web browsers can also download documents using **FTP** and many have integrated mail and newsreaders as well.

## Web Browsing in Fedora Core

Web browsing is fun because many of today's Web pages are so full of graphics and multimedia. Then there's the element of surprise — you can click a link and end up at unexpected Web pages. Links are the most curious (and useful) aspect of the Web. You can start at a page that shows today's weather and a click later, you can be reading this week's issue of *Time* magazine.

To browse the Web, all you need is a Web browser and an Internet connection. I assume that you’ve already taken care of the Internet connection, so all you need to know are the Web browsers in Fedora Core.

# Checking out the Web browsers in Fedora Core

Fedora Core comes with the Mozilla Web browser. Mozilla is an open-source version of Netscape Communicator, and it is the primary Web browser in Fedora Core.

Fedora Core includes several other Web browsers. I briefly mention the other browsers, but I focus on Mozilla in the rest of the discussions. Here are the major Web browsers that come with Fedora Core:

- **Mozilla**: The reincarnation of that old workhorse — Netscape Communicator — only better. Includes mail and a newsreader. The Web browser is called the Mozilla Navigator, or simply Navigator (just as it was in Netscape Communicator).
- **Epiphany**: The GNOME Web browser that uses parts of the Mozilla code to draw the Web pages, but has a simpler user interface than Mozilla. Epiphany is not installed by default, but it’s on the DVD included with this book. If you can’t find Epiphany on the DVD, you can download it from www.gnome.org/projects/epiphany/.
- **Konqueror**: The KDE Web browser that also doubles as a file manager and a universal viewer.

In addition to these three, many other applications are capable of downloading and displaying Web pages.

# Starting Mozilla

From the GNOME desktop, you can start Mozilla in one of two ways:

- Click the Web Browser icon (the earth and mouse) on the GNOME or KDE panel.
- Choose Main Menu > Internet > Mozilla Web Browser from GNOME.

When Mozilla starts, it displays a browser window with a default home page (the main Web page on a Web server is known as the *home page*). You can configure Mozilla to use a different Web page as the default home page.

# Learning Mozilla’s user interface

Figure 2-4 shows a Web page from a U.S. government Web site (www.gao.gov), as well as the main elements of the Mozilla browser window.
