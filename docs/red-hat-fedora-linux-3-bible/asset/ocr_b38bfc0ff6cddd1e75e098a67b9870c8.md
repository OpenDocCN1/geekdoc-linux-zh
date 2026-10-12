# Chapter 9: Tools for Using the Internet and the Web

The Advanced Preferences can be used to fine-tune your Web browsing experience, as well as specify what content you open can and can't do on your computer. Here are some Advanced Preferences that might interest you:

+   - **Scripts & Plugins** — The Web content you choose can try to open, move, resize, raise and lower windows. It can request to change your images, status bar text, or bits of information stored in what are called *cookies*. These preferences let you restrict what the content you request can do.

+   - **Cache** — By default, the most recent 4MB of Web pages you visit are stored in RAM and the most recent 50MB of pages you visit are stored on your hard disk. If a page is not out-of-date, caching makes it possible to return to a page quickly, without needing to reload from the original Web server. Cache preferences let you change how much information is cached and where hard disk cache is located. Other cache preferences let you clear all memory and disk cache immediately.

+   - **Proxies** — If you have direct access to the Internet, you don't need to change any proxy settings. However, if you need to access the Internet via a proxy server, you can identify the location of that server (or servers) here. To access the Web via proxy servers, you must explicitly identify the proxy server to use for each type of content you request (HTTP, SSL, FTP, Gopher, and SOCKS).

+   - **HTTP Networking** — If you are using a proxy server, that proxy server may require that you make HTTP requests using either HTTP/1.0 or HTTP/1.1 standards (1.1 is the default).

+   - **Software Installation** — When a request for Web content results in that content trying to install software on your computer, you can either allow that to happen (with prompting) or not allow any software updates, based on how this preference is set.

+   - **Mouse Wheel** — If your mouse has a wheel, you can change how Mozilla behaves when you use that wheel. By default, the mouse wheel scrolls a line at a time.

+   - **DOM Inspector** — Turn this on to check the structure of a Web page (for debugging). This is very useful if you need to create Web pages, especially dynamic Web pages.

# Adding helper apps

Although the main type of content provided by Web pages is HTML, many other content types can be displayed, played, or presented by a Web browser. Most additional data encountered by Mozilla is handled in one of two ways: plug-ins or helper apps.

Plug-ins are self-contained programs that allow data to play within the Mozilla window. A helper app can be any program that is available on your Red Hat Linux system. It is up to you to identify the plug-in or helper app to launch when a certain type of data is encountered.

Mozilla determines what helper app or plug-in to launch based on the following criteria:

+   - **Suffixes** — If the browser is reading a file that has a particular suffix attached to the filename (such as exe for an application or gz for a compressed zip file), it can use that