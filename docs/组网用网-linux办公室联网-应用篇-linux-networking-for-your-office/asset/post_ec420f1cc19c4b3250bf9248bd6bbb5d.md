
You might have other reasons to use X's networking features. The flexibility of X's design allows you to use remote access in ways that might be important to you but that might not be easy for others (such as X's designers) to predict.

## Using an X Server

In X parlance, the server handles the display of information for the client, which is an application program of some variety. When you aren't sitting at the console, this results in some potentially confusing terminology because the server is the system at which you're sitting, whereas the client is the computer whose resources you want to access. This terminology is exactly backward from what most people expect because the server is usually the distant machine with the resources you want to use. To understand this terminology, though, you should look at it from the point of view of the application program. When you use a word processor on a Macintosh and want to save a file to a distant system, the word processor must access the resources on that distant system. When you use an X-based Linux word processor in a networked environment, though, the word processor must make requests of distant resources merely to display your document—from the program's point of view, the display at which you're staring really is a server. The same is true when you use a standalone Linux system, except that X runs on the same system as the application program. In this case, you still run an X server program, but it happens to run on the same computer as the applications.

## Examples of X Server Software

Many programs exist for handling X displays on various operating systems. The following are some examples:

- XFree86—XFree86 comes with all major Linux distributions, and is capable of handling the display of applications from a distant system. You can therefore use one Linux computer as a remote X display for another Linux computer. XFree86 is also available on assorted non-Linux platforms, including many UNIX flavors and OS/2. You can find out more from the XFree86 Web site, http://www.xfree86.org.
- Metro-X—This is a commercial X server for Linux and various UNIX flavors. It replaces the server component of XFree86. In some cases Metro-X may run faster than XFree86 or support hardware that XFree86 doesn't support. In other cases XFree86 is the superior product. For more information, check out http://www.metrolink.com.
- Accelerated-X—Accelerated-X is another commercial X server for Linux, FreeBSD, and Solaris. Similar comments apply to Accelerated-X as apply to Metro-X. You can find more information at http://www.xig.com.

## Tip

In general, the commercial Linux X servers provide support for newer hardware than does XFree86, for a variety of reasons. For older hardware, there's usually less reason to use a commercial server. Each of these three systems, though, has its own strengths, so you might want to check their Web sites just to see what you are—and aren't—missing.

- X servers for UNIX—Most commercial UNIXes come with their own X servers. Such systems should not have difficulty running Linux programs remotely.
- MI/X—This is an inexpensive X server for Windows and MacOS. You can obtain a 15-day sample version of the program to see if it suits your needs. For more information, see http://www.microimages.com/mix for the Windows version, or http://www.microimages.com/freestuf/mix/macindex.htm for the Macintosh version.
- X-Win32—This is another commercial X server for Windows systems. A demo version (with a two-hour time limit per session) is included on the CD-ROM that accompanies this book, in the same -extras/X directory, or you can obtain a demo version from http://www.starnet.com.
- Exceed—Yet another approach to an X server for Windows is Exceed. You can learn more from http://www.hummingbird.com/products/nc/exceed/index.html, where you can order a demo CD.
- eXodus—This is a commercial X server for the Macintosh. You can obtain more information or download a demo version from http://www.wpine.com.

The details of operation of each of these products differ, though the X servers for UNIX and Linux tend to operate very similarly to one another. On Windows and MacOS, the programs can use one of three methods of operation (most of the programs allow you to select from among at least two of these):

- Rootless with native GUI—The X server can use the native GUI as its window manager. This makes X programs look very much like programs in the host OS, at least at first glance. Figure 19.1 demonstrates this approach, as demonstrated by X-Win32.
