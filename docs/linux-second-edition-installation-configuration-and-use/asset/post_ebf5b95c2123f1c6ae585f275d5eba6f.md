
# 328 GOING INTERNET WITH LINUX

NAVIGATOR | APPLICATIONS. Figure 9.9 illustrates the configuration for display of PostScript files.

![](img/b30873dd3d753687a59253fb9ad26a0b_355_0.png)

Figure 9.9 Netscape Communicator configuration.

### Images
If you do not want images to be transferred automatically, deactivate AUTOMATICALLY LOAD IMAGES IN THE ADVANCED category. Now that much less data needs to be transmitted, documents are displayed faster. If you want to view an image, simply click on the icon displayed as a placeholder. By clicking the IMAGES button, all the images of the document are downloaded.

### Java, JavaScript
Java and JavaScript are two programming languages for executing programs that can be integrated into WWW documents. If you wish to deactivate Java and/or JavaScript for security reasons, you can do this via options of the ADVANCED category.

### Cache/Proxy
The Communicator manages a local cache for the most recently downloaded documents. Cache parameters can be set in the ADVANCED|CACHE category. If you have enough space on your hard disk, increase the disk cache! If your Internet provider manages a proxy cache, you should enter its address in the ADVANCED|PROXIES category CONFIGURATION.

# WORLD WIDE WEB (WWW) 329

### Smart Browsing
Since version 4.5, the Communicator has a new feature: when you click on the WHAT'S RELATED button, the program offers you a selection of comparable Web pages. However, this function is not controversial. To make it work, Netscape stores a list of all Web pages you visit (and this is not done locally, but on a server of the Netscape Corporation). From a data protection point of view, this is at least a dubious procedure. If you have reservations about it, you can easily deactivate this function in the category NAVIGATORSSMART BROWSING.

# Problems

### Lock file
You may however receive this warning even if Netscape is currently not running at all. In this case, if you did not exit Netscape properly when you used it (crash), ~/.netscape/lock has not been deleted. In this case, you will have to delete the file manually:

```bash
rm ~/.netscape/lock
```

There is only rarely any reason to start Netscape more than once. First, you can open any number of windows with [Alt+N]. Second, you can display a new document in a running Netscape instance with the command netscape -remote "openUrl address".

### talkback
Since version 4.5, the program talkback is supplied together with Netscape. This program occasionally establishes a connection to Netscape's company server, and supplies the company with feedback about utilization and potential difficulties of Netscape. In particular, the program is started automatically when there is a problem with the execution of Netscape.

> Whether this uninvited and mostly even unnoticed behavior is desirable from a data protection point of view will be left open. The real problem is of a different kind: talkback in the worst case lead to a complete loss of keyboard and mouse control – and then only the reset button returns (which will result in the loss of all unsaved data and, if you are unlucky, in a faulty file system).

Therefore, you should deactivate talkback for your own good. To do this, you need to start the program. It is located in a subdirectory of the Netscape directory, in SuSE in /opt/netscape.

```bash
/opt/netscape/talkback/talkback
```

### Arena
Now you execute SETTINGS. This puts an end to all the Talkback hubbub.

Arena was the first freely available and reasonably user-friendly Web browser for X. In comparison with other WWW browsers, arena is limited to the absolute minimum; the program is capable of displaying documents at various levels of scaling (Zoom) and of following cross-references contained in them. More cannot be said: further functions are not provided (not even the management of a bookmark list). Arena is controlled through an easily understandable button bar and, apart from the cursor keys, no keyboard shortcuts exist.

For reading online documentation and for first experiments with the WWW, Arena is certainly sufficient. The program has the additional advantage that screens are built up quite quickly and memory consumption is limited. However, it cannot offer the comfort and stability of Netscape.

### kfm (KDE file manager)
The program kfm is not only a file manager but also a quite adequate Web browser. Its operation is problem-free. Configuration is carried out with OPTIONS|CONFIGURE BROWSER.... (see also page 500).

![](img/b30873dd3d753687a59253fb9ad26a0b_357_0.png)

Figure 9.10 Reading HTML files with kfm.

Please note that in kfm, WWW addresses have to be entered in full, that is with the preceding characters http://. Netscape fills addresses automatically, whereas kfm interprets addresses without http:// as file names.

# WORLD WIDE WEB (WWW) 331

### Lynx
Lynx has one big advantage over WWW browsers: the program runs in text mode. This advantage is seen by many users as a disadvantage; because many features of the WWW obviously get lost (text attributes, pictures). On the other hand, Lynx is very easy on memory consumption and computing capacity, and it does not require X installation.

![](img/b30873dd3d753687a59253fb9ad26a0b_358_0.png)

Figure 9.11 Lynx – reading HTML files in text mode.

Handling Lynx is simple: usually, the program is started by passing it a WWW address or the name of an HTML file. Lynx loads the document and displays the page. Subsequently, the following keyboard shortcuts apply:

| Key | Action |
| :--- | :--- |
| PgUp | cursor one/down |
| PgDn | cursor two/down |
| ⇧ | cursor to previous/next |
| ← | follow cross-reference |
| → | back to document |
| Backspace | show list of documents |
| J | search for text in current document |
| A | insert reference to document |
| D | transfer document |
| E | start editor |
| G | enter WWW address |
| K | display all available shortcuts |
| O | set options |
| V | display bookmark list |

# GOING INTERNET WITH LINUX

Lynx can also be started by passing it a directory: the program displays a list of all files and subdirectories which can be selected in the same way as cross-references. Recent versions of Lynx displaying headings and links in different colors (With the left button, you follow a link; the right button takes you to the previous page.) These features can be activated with the options --color and --use-mouse.

Lynx has yet another function: the program can be used as an ASCII converter, and converts HTML documents into readable text file. The following command illustrates this:

```bash
lynx -dump source.html target.txt
```

Lynx has an extensive man. Lynx -help gives an overview of all command options. During operation, [K] can be used to display a list of all commands. Help is called with [H] or [?] - however, the help texts are read over the Internet. If you use Lynx for reading local files only and you have no network connection, you can use this function.

### Surfing offline (WWWle)
Usually, Web documents can be read "online," that while your computer is connected (via PPP) to the Internet. The WWWle program seems to promise the opposite but cannot work miracles. Nevertheless, the program is extremely useful:

- It manages a cache which stores all WWW documents that have been read. You can read all these documents without problems at a later date, even if you are not connected to the Internet at the time. (In principle, this corresponds to the "offline" mode of Internet Explorer.)
- When you click offline on links of documents that are not locally available at the moment, WWWle marks the document. Whenever a new Internet connection is established, all earmarked documents are transmitted at once. Afterwards, the connection can be terminated.
- Reading single documents is often unsatisfying. With WWWle, you can therefore mark whole groups of documents (which are connected from a starting page via links) for transmission. Any link depth can be specified.

WWWle can do much more than is explained here. You should read the extensive online documentation, and check the WWWle-Homepage: http://www.gedanken.demon.co.uk/wwoffle/
