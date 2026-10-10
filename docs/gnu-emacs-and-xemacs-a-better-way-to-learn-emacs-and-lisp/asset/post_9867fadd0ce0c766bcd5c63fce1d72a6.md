
## Conclusion

This chapter, short as it is, should give you a head start on editing remote files. After you get it set up with your own passwords, ange-ftp is a straightforward package, transparent enough in use that you can easily take it for granted.

The next chapter introduces W3, the sole Web browser of the text-editor world.

## Chapter 20: Web-Browsing with W3

Installing and Setting up W3
Images, XEmacs, and GNU Emacs
Basic Commands
Stylesheets
Security
Masquerading
Downloading Files
Asynchronous Operation
Caching Web Sites

![Image](img/c8827ea52a0796def3f6891892ed9d3a_426_0.png)

Some years ago, an Emacs hacker named Bill Perry had a quixotic idea. What if Emacs could be used as a Web browser? After all, Web pages are ASCII text documents; even the HTML tagging is composed of ASCII characters. What about the images? At the time (the early '90s), XEmacs was just beginning to be able to display images, so that was one possibility. The proposed Emacs browser could also be run strictly in text mode like the Lynx browser, which would let GNU Emacs users use this fantasticized Emacs extension. A challenging project, to be sure, that would end up pushing the limits of what can be demanded of an interpreted language like Emacs-Lisp.

Perry plugged away at the project for several years. He was kept busy with W3, because this Emacs extension occupied an unstable area: the shifting ground between the two slowly-evolving versions of Emacs on the one side and the fractically mutating nature of HTML in the mid-to-late '90s on the other.

How did it turn out? Considering the difficulties inherent in the project, remarkably well. It's far from perfect; W3 can be slow to render Web pages, and due to the single-threaded nature of Emacs, it can cause Emacs to "zone out" if there are network slowdowns.

On the plus side, here are some of W3's hard-won features:

- It renders inline images well (on XEmacs and presumably Emacs 21).
- Stylesheets are well-supported.
- It has SSL encryption (with helper applications).
- It supports bookmarks and caching.

It won't replace Netscape or Mozilla, but W3 can be useful at times. Gnus makes good use of W3 when displaying HTML mail or newsgroup messages. It also can be handy for reading HTML files on your hard disk.

### Installing and Setting up W3

XEmacs users can install a preconfigured package that should be ready to go. GNU Emacs doesn't include W3, so you have to install it from source, which isn't that difficult. The W3 source archive is much like those of Gnus and VM; because it includes a configure script that generates a custom makefile. A copy of the W3 archive can be found on this book's CD-ROM in the directory /cdrom/packages/w3.

If you would like to specify a particular directory for W3's byte-compiled Lisp files, run the configure script with this command:

```
configure --with-lispdir="/path"/W3 --with-emacs
```

Substitute the path to your site-lisp directory (the recommended location) for *path* in this command. If your Emacs (for whatever reason) isn't called *emacs* or isn't in your executable path, substitute the name and the path (if needed) for *emacs*.

Running *make* and then *make install* should be all you need to do.

*W3* makes use of several configuration files, some of which are automatically generated and then saved in the directory *~/.w3*. You can change the way *W3* works either by editing the files there or by accessing the *W3 Customize Group* buffer and changing the settings.

### Images, XEmacs, and GNU Emacs

*W3*, shown in Figure 20.1, was one of the first Emacs extensions to take advantage of the built-in XEmacs image-rendering support. Users of GNU Emacs were denied this *W3* feature until the release of *Emacs 21*, a significant event in Emacs history. *W3* in its current released version doesn't work with *Emacs 21*, but the fixes are in the *W3 CVS* tree, which will eventually become a new version. This chapter focuses on *W3* usage with XEmacs, but the usage and configuration details should be applicable to GNU Emacs when the code situation stabilizes.

![Figure 20.1](img/c8827ea52a0796def3f6891892ed9d3a_428_0.png)

*Figure 20.1 W3 Displaying the W3 Home Page*

**NOTE**

Emacs 21 hadn’t yet been released while this book was being written, but the release seemed so imminent that it will probably be available by the time you read this.

### Turning off Image Display

Even if you are running an image-enabled Emacs, there might be good reasons to disable W3’s image loading. W3 is slower than browsers such as Netscape and Opera and shouldn’t be considered as a replacement graphical browser. With image loading turned off, W3 does a respectable job, similar to Lynx but with more-advanced page formatting. The W3 Options menu, shown in Figure 20.2, lets you turn off automatic image loading. Selecting the final item on the menu saves the current state of the listed options to an initialization file named ~/.w3/profile.

### MIME Support

W3 is aware of the standard locations where it can expect to find a system’s mailcap and mime-types files. Many Web browsers refer to these files to find a way to present a file to the user. The mime-types file (often /etc/mime.types) lists various file suffixes and which MIME-type the suffix indicates. Here are a couple of lines from a typical mime-types file:

```
audio/x-pn-realaudio     ra rm ram
application/x-httpd-php3  php3
```

The mailcap file (~/.mailcap or /etc/mailcap) maps files that have been identified as having a certain MIME type to corresponding programs that know how to handle such files. Here is a mailcap line that corresponds to the first mime-type line just shown:

```
audio/x-pn-realaudio:/usr/local/RealPlayer7/realplay "*"
```

![Figure 20.2](img/c8827ea52a0796def3f6891892ed9d3a_429_0.png)

This line associates the RealPlayer program with files that have been identified in the mime-types files as being of the audio/x-pn-realaudio type.

### Basic Commands

There are two ways to start W3. The first is to press M-x and type

```
w3
```

W3 starts up and attempts to load the default home page, the W3 home site at Indiana University. If you aren't connected to the Net, W3 naturally won't be able to find the page. Pressing Ctrl-g aborts the search. If you want to be able to start W3 without being Net-connected, you can change the default page to a local HTML file on your hard disk. You can change the setting by pressing M-x and typing

```
customize-group
```

Respond to the minibuffer prompt by typing

```
w3-files
```

One of the items in the resulting Customize buffer will be w3-default-homepage. You can type any valid URL in the item's text entry field. Don't forget to select "Save for Future Sessions" from the State menu when you are finished.

You can also start W3 by pointing it directly to a local HTML file by pressing M-x and typing

```
w3-open-local
```

You are queried for a file name in the minibuffer.

W3 provides a great number of key commands, but you need to learn only a few to be able to quickly navigate Web sites:

| Key/Command | Description |
| :--- | :--- |
| Spacebar and Backspace | Scroll forward and backward through a page (Page Up and Page Down work too). |
| Enter | Follows the link at point (the middle mouse button also does this). |
| B | Returns to the previous page. A cached copy is used if you have turned on the disk cache. |
| F | Goes forward to the next page. |
| r | Reloads the page (g also does this). |
| Tab | Moves point to the next text entry field (such as a form). |
| Shift-Tab | Moves to the previous text entry field. |
| Ctrl-o | Prompts you for a Web site’s URL. |
| o | Prompts you for a local HTML file. |
| s | Displays the HTML source for the current buffer. |

There are many other key commands, but these are the ones you will need the most. Press Ctrl-l h to see a complete list.

To help Netscape and Lynx users adapt easily to W3, Bill Perry included emulation keybindings. These two commands replace the default keybinding with bindings similar to either of the two browsers:

```
M-x turn-on-netscape-emulation
M-x turn-on-lynx-emulation
```

These commands allow you to try out the new keybindings, but if you decide you want to use one of these emulations in every W3 session, you probably don’t want to type the command each time W3 starts up. One solution to this is to insert this line in your ~/.w3/profile file:

```
(setq-default w3-netscape-emulation-minor-mode t)
```

Substitute lynx for netscape in this line if you prefer.

### Bookmarks

By default, W3 recognizes the file ~/.mosaic-hotlist-default as its bookmarks file. You probably don’t use Mosaic, the early precursor of Netscape, so you probably don’t have such a file. If you select Add bookmark from the Bookmark menu while visiting a Web site, that site’s URL is added to that bookmark file. If it doesn’t exist, it is created.

If you would rather use a different bookmark file, you can specify it in the ~/.w3/ profile file with a line like this:

```
(setq-default w3-hotlist-file "file:///[path]/file.html")
```

There are several keybindings (as well as menu items) for working with bookmarks:

| Key/Command | Description |
| :--- | :--- |
| h i | Adds the current page to the default bookmark file. This command uses the buffer name as an identifier (this is what you see on the bookmark menu). If you want to give the bookmark another name, press Ctrl-l u and type new-name before typing i i. |
