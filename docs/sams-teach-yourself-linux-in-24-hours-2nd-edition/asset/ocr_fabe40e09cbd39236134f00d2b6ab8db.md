# FIGURE 13.1

The Lynx text-only Web browser is a compact, efficient program you can use to quickly browse Web pages without waiting for graphics to load.

![](bbox=[0.38, 0.17, 0.9, 0.55])

You can also use the Lynx browser to retrieve files without browsing. By using this approach, you can automatically research or get information on a regular basis:

```
# lynx http://www.yahoo.com/headlines/news -dump >news.raw
```

In this example, the content of the Web page is downloaded by the lynx command and then redirected to the file news.raw. Lynx also downloads files just like other browsers if you press the Enter key while your cursor has a file or link highlighted. The basic navigation keys for this browser are the cursors (to scroll up and down the current page, to go back to a previous page, or forward to the next), the Enter key (to load a link), and the Tab key (to go to the next link). To get help while using Lynx, type the question mark (?) key.

# Exploring Netscape Communicator

The Netscape Communicator Web browser, by Netscape Communications (soon to merge with America Online), is one of the most popular browsers for all computer systems. You can find a copy installed on your system that is specifically configured for OpenLinux (see Figure 13.4).

Netscape, like most well-behaved X11 clients, uses several X11 Toolkit options. For example, if you don't like the large initial window, you can specify a smaller starting window using geometric settings.

> See Hour 7, "Using the X Window System," for a discussion of X11 toolkit options, such as geometry settings.