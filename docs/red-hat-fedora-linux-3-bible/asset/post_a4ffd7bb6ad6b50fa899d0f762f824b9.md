
## Chapter 9: Tools for Using the Internet and the Web

The Advanced Preferences can be used to fine-tune your Web browsing experience, as well as specify what content you open can and can't do on your computer. Here are some Advanced Preferences that might interest you:

- **Scripts & Plugins** — The Web content you choose can try to open, move, resize, raise and lower windows. It can request to change your images, status bar text, or bits of information stored in what are called *cookies*. These preferences let you restrict what the content you request can do.

- **Cache** — By default, the most recent 4MB of Web pages you visit are stored in RAM and the most recent 50MB of pages you visit are stored on your hard disk. If a page is not out-of-date, caching makes it possible to return to a page quickly, without needing to reload from the original Web server. Cache preferences let you change how much information is cached and where hard disk cache is located. Other cache preferences let you clear all memory and disk cache immediately.

- **Proxies** — If you have direct access to the Internet, you don't need to change any proxy settings. However, if you need to access the Internet via a proxy server, you can identify the location of that server (or servers) here. To access the Web via proxy servers, you must explicitly identify the proxy server to use for each type of content you request (HTTP, SSL, FTP, Gopher, and SOCKS).

- **HTTP Networking** — If you are using a proxy server, that proxy server may require that you make HTTP requests using either HTTP/1.0 or HTTP/1.1 standards (1.1 is the default).

- **Software Installation** — When a request for Web content results in that content trying to install software on your computer, you can either allow that to happen (with prompting) or not allow any software updates, based on how this preference is set.

- **Mouse Wheel** — If your mouse has a wheel, you can change how Mozilla behaves when you use that wheel. By default, the mouse wheel scrolls a line at a time.

- **DOM Inspector** — Turn this on to check the structure of a Web page (for debugging). This is very useful if you need to create Web pages, especially dynamic Web pages.

### Adding helper apps

Although the main type of content provided by Web pages is HTML, many other content types can be displayed, played, or presented by a Web browser. Most additional data encountered by Mozilla is handled in one of two ways: plug-ins or helper apps.

Plug-ins are self-contained programs that allow data to play within the Mozilla window. A helper app can be any program that is available on your Red Hat Linux system. It is up to you to identify the plug-in or helper app to launch when a certain type of data is encountered.

Mozilla determines what helper app or plug-in to launch based on the following criteria:

- **Suffixes** — If the browser is reading a file that has a particular suffix attached to the filename (such as exe for an application or gz for a compressed zip file), it can use that suffix to determine the file’s contents. When a file’s suffix matches a suffix configured for a particular helper app or plug-in, the helper app or plug-in is used to play or display the data.

- **MIME type** — Because data may come to the browser in a stream or have no suffix, Mozilla can use the MIME type attached to the data to determine which plug-in or helper app to use. (MIME stands for Multipurpose Internet Mail Extensions.)

You can add your own helper app to automatically handle a particular type of data in your browser. Here’s how:

1. Choose **Edit → Preferences**. The Mozilla Preferences window appears.
2. Select Helper Applications under the Navigator category.
3. Click **New Type**. A dialog box appears that enables you to add information about the helper app and the data that it can handle.
4. Type in a description of the data, the MIME type, and the file suffixes (if any) on files that contain that type of data.

> NOTE: When you add the suffix, don’t include the dot.

5. Choose an application to handle the data type. If the application needs a Terminal window to run, type **xterm -e**, followed by the command line you need to enter. This executes the command in an xterm window, reading in data as needed.
6. Click **OK** when you are done.

The next time you open data in Mozilla of the type you just added, a pop-up window will ask you if you want to use the application you just entered to open the data.

### Adding plug-ins

There are not many plug-ins available for use in the version of Mozilla that comes with Fedora Core. To see a list of plug-ins associated with your Mozilla browser, choose **Help → About Plug-ins**. You will probably see one plug-in: MozPlugger. If MozPlugger isn’t installed, you can install it from the DVD that comes with this book. MozPlugger (`http://erik.hube.net/plugger.html`) is a multimedia plug-in that handles AVI, SGI-movie, TIFF, DL, IFF-anim, MIDI, Soundtracker, AU, WAV, and Comdodere 64 audio files by relying on external programs to play the data. Recently, MozPlugger has also added support for displaying a variety of Microsoft office productivity file types.

Here is a list of some free plug-ins available for Mozilla that work with Fedora Core.

- **Adobe Acrobat Plug-in** (www.adobe.com/support/downloads) — Displays files in Adobe Systems’ PDF (Portable Document Format) format.
- **Cult3D Plug-in** (www.cult3d.com) — Displays high-quality, interactive real-time 3D images on the Web. This plug-in is from Cycore Computers. (Click Download to find the plug-in. There is a cult3d RPM available that requires tailoring to work in Mozilla.)
- **DjVu Plug-in** (djvu.sourceforge.net) — Displays images in DjVu image compression technology. This plug-in is from AT&T.
- **Real Audio** (www.real.com) — Plays Real Audio and Video content. (To use the Real Plug plug-in in Mozilla, you need the RealPlayer and realplay-plugin RPMs, available by searching rpmfind.net.)
- **Macromedia Flash Player** (www.macromedia.com) — Displays multimedia vector graphics and animation. This plug-in is from Macromedia, Inc. Flash Player is available for Fedora Core, but Macromedia’s Shockwave plug-in is not yet available for Linux.

More plug-ins may be added in the future for use with Fedora Core. Mozilla now offers a great new Web site for getting plug-ins for Linux that run in Mozilla: http://pluginbox.mozdev.org/linux.html. The site contains links to download plug-ins and instructions for installing them.

When you download a plug-in, follow the instructions that come with the plug-in for installing it. If the plug-in comes in an RPM file, install it as you would install any other software package in Red Hat Linux (`rpm -Uvh *package*`). Otherwise, just copy the plug-in file (a .so file) to the system plug-in directory (probably `/usr/lib/mozilla/plugins`) or `/usr/lib/mozilla/plugins`. When you restart Mozilla, the plug-ins will automatically be picked up from those locations.

> NOTE: The CrossOver Plugin is a commercial product that lets you use many Windows plug-ins in Mozilla. See the section “Adding a CrossOver Plugin” later in this chapter for details.

### Using Mozilla Navigator controls

If you have used a Web browser before, the controls are probably as you might expect: location box, forward and back buttons, file and edit menus, and so on. There are a few controls with Mozilla, however, that you might not be used to seeing. Here are some examples:

- Using the sidebar — Press the F9 function key to toggle the sidebar on and off. Click a What's Related, Search, Bookmarks, or History tab (or add your own tab as described earlier). Add your own bookmarks, return to pages from your history list, or search for Web content.
- Sending Web Content — You can send an e-mail containing either the current Web page (File → Send Page) or the URL of the current Web page (File → Send Link) to selected recipients.
- Searching the Internet — You can search the Internet for a keyword phrase in many different ways. Choose Tools → Search the Web to open a Netscape Web site that lets
