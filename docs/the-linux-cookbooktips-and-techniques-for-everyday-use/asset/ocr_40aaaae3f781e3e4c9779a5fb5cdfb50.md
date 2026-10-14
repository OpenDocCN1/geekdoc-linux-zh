# 32.4 Browsing the Web in Emacs

-localhost Disable URLs that point to remote hosts--useful for using lynx to read HTML- or text-format documentation in `/usr/doc` and other local documents while not connected to the Internet.

-nolist Disable the annotated link list in dumps.

-number_links Number links both in dumps and normal browse mode.

-partial Display partial pages while downloading.

-pauth=user:pass Use a username of user and password of pass for protected proxy servers.

-underscore Output italicized text like _this_ in dumps.

-use_mouse Use mouse in an xterm.

-version Output lynx version and exit.

-vikeys Enable vi-style key bindings for movement.

-width=integer Format dumps to a width of integer columns (default 80).

@sf(Debian): `w3-el-e20`
@sf(WWW): ftp://ftp.cs.indiana.edu/pub/elisp/w3/

Bill Perry's Emacs/W3, as its name implies, is a Web browser for Emacs (giving you, as Bill says, one less reason to leave the editor). Its features are many---just about the only things it lacks that you may miss are SSL support (although this is coming) and JavaScript and Java support (well, you may not miss it, but it will make those sites that require their use a bit hard to use). It can handle frames, tables, stylesheets, and many other HTML features.

+   - To start W3 in Emacs, type:

```
M-x w3 RET
```

To open a URL in a new buffer, type C-o and, in the minibuffers, give the URL to open (leaving this blank visits the Emacs/W3 home page). Middle-click a link to follow it, opening the URL in a new buffer.

+   - To open the URL http://gnuscape.org/ type:

```
C-o http://gnuscape.org/ RET
```

+   - To open the URL of the Emacs/W3 home page, type:

```
C-o RET
```