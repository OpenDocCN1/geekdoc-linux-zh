
## Stylesheets

**h l**

Adds the link's URL at point to the bookmark file.

**h v**

Converts the bookmark file to HTML and displays it with W3.

**h a**

You are prompted for a regular expression. Type one in the minibuffer, and the bookmarks that match the expression are displayed. This is a handy way to find particular bookmarks in a large bookmark file.

**h u**

Lets you use Tab completion to jump to a bookmarked location. Type in a few letters of a bookmark's name (not the URL) and press Tab to insert the remainder of the name.

**h r**

Renames a bookmark. You might end up with bookmark names that are too long or that aren't good identifiers, such as index.html. This command also uses Tab completion. Type in a portion of the bookmark you want to rename, complete it by pressing the Tab key, and type the new name in the minibuffer when prompted.

These are the default bookmark key commands. If you have turned on Netscape or Lynx emulation, you can view the new keybindings by pressing Ctrl-h b.

## Using Netscape's Bookmark File

W3 can load an external bookmark file and make it available on the bookmark menu, but you need to use a certain amount of caution when doing this. A typical Netscape bookmark file has hundreds of entries. The Emacs menu system has a difficult time displaying a large number of items in a readable and navigable fashion. W3 has trouble rendering many table-heavy Web sites, so it makes sense to keep a separate bookmark file consisting of sites that W3 can handle.

Netscape uses HTML as the file format for its bookmark file. Not all of the bookmark commands just mentioned work with this type of file—another reason to maintain W3's bookmarks separately.

## Stylesheets

W3's display of HTML documents can be controlled through the use of Cascading Style Sheets (CSS). These are text files written with a particular syntax that CSS-enabled browsers interpret in order to control different attributes of an HTML file, such as fonts, colors, and text alignment. Stylesheets can exist both on the server that hosts an HTML file and on the machine running the browser. The point of using stylesheets is to separate the presentation attributes from the HTML file itself and to give both the viewer and the author a measure of control over how a page is displayed. The ratio between the influences of the viewer's and the author's stylesheets can be varied. The “cascading” of stylesheets is a metaphor for how multiple stylesheets can affect the ultimate presentation of the HTML file.

> W3 has the distinction of being the first web browser to include stylesheet support. Cascading Style Sheets were proposed as a standard long before the big-name browsers began to support the protocol.

The W3 distribution includes a sample stylesheet in the /etc directory called default.css. In the XEmacs package, it is named /etc/w3/stylesheet in the main package directory.

Here are a few sample entries from that file that give you a taste of CSS syntax:

```
/*
** Hypertext link coloring
*/
a:link    { color: #FF0000 }
a:visited { color: #B22222 }
a:active  { color: #FF0000 }

/* W3-specific section for Emacs versions which
** can only display one size of font at a time
*/
@media unifont {
h1,h2,h3,
h4,h5,h6 { text-decoration: underline; }

	h1 { color: rgb(0,255,255); }  // cyan
	h2 { color: rgb(70,130,180); } // steelblue
	h3 { color: rgb(106,90,205); } // slateblue
	h4 { color: rgb(135,206,235); } // skyblue
	h5 { color: rgb(0,0,128); }    // navy
	h6 { color: rgb(173,216,230); } // lightblue

	strong,em { color: red        }
	dfn { font-style: italic       }
	s,strike { color: green        }
}
```

Several chapters of the W3 Info manual are devoted to the nuts and bolts of stylesheets. You will find ample detail that is outside the scope of this book. You can get a feel for how stylesheets work by copying the W3 sample stylesheet to `~/w3/default.css` and letting W3 know that this file is the one to use. Do this by pressing M-x and typing `customize-group`

At the minibuffer prompt, type

w3-files

A buffer similar to Figure 20.3 appears. The setting to change is **Default Stylesheet**. Type in the entry field the path and file name of the sample file.

Save the changes by selecting **Save For Future Sessions** from the State button's menu.

Before starting W3, load your new stylesheet into an Emacs session and read through it. The color specifications can be in any of three formats: RGB number triplets, colors named in the X11 `rgb.txt` file, or 8-bit truncated RGB. All three formats are used in the example just shown.

As a first CSS experiment, try changing some of the colors in the file so that they show up well against your Emacs background color. The X11 application `xcolsel` is a handy tool for browsing the available colors and finding their names in various formats.

![](img/c8827ea52a0796def3f6891892ed9d3a_434_0.png)

The relative sizes of the different headers can be changed if you are using XEmacs (and possibly Emacs 21). Don't make too many changes at once so that you will be able to track down any mistakes.

Sections of the file that seem obscure are explained in the Stylesheet Info chapters.

After you have saved your changes, load a local HTML file by pressing M-x and typing

`w3-open-local`

The changes you made should be visible in the W3 buffer. If they aren't, check over the file for errors.

One thing to keep in mind is that W3 reads its configuration files the first time it is started in an Emacs session. You can shut down W3 by pressing q, edit a configuration file or stylesheet, and then restart W3, and the changes won't take effect. W3 seems to hold its configuration variables in memory for the duration of an Emacs session. This means that you need to shut down and restart Emacs when you want W3 to notice any changes you have made to its configuration.

## Security

W3 was designed with security in mind. You can install an external SSL (Secure Sockets Layer) program, and W3 will encrypt HTTP connections through an SSL channel. Cookies are files that many servers would like to leave on your hard drive that might contain password or identification information. You can disable all cookies or limit them to certain trusted servers.

## Using SSL

In order to use W3's SSL capabilities, you must install an external program. The only one that is currently supported is SSLeay version 0.6.6 or later. The current status of SSLeay is that it has been orphaned by its original developers. The code was adopted by a new project known as OpenSSL, which is under active development as an open source replacement for SSLeay. W3 doesn't have direct support for OpenSSL, but with a little scripting, this disadvantage can be circumvented.

A warning: What follows are some suggestions for an SSL W3 approach that has worked for some people, but it likely will require some tinkering to get it to work on your system. Some background reading will help. You can find references and links on the OpenSSL Web site at http://www.openssl.org.

The W3 Info manual can also provide further help.

Start out by creating a shell script named emacs-ssl:

```
#!/bin/sh
exec 2>/dev/null
exec openssl "$@"
```

This script starts openssl with all error messages directed to /dev/null so that W3 won't become confused by them. Make sure you make the script executable, and then move it to /usr/local/bin or another binary directory on your path.

The next step is to change the values of several W3-SSL variables. The easiest way to do this is with Customize.

### SSL Variables

Bring up a Customize buffer for SSL by pressing M-x and typing

```
customize-group
```

Respond to the prompt with

```
ssl
```

The resulting buffer, shown in Figure 20.4, lets you set such variables as the SSL certificate directory and the command-line options for the SSL program.

![](img/c8827ea52a0796def3f6891892ed9d3a_436_0.png)
