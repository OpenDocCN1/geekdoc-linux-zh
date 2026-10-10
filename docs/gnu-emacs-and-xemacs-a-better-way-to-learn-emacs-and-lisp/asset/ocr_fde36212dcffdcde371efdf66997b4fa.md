The mode is also useful for those who read the Project Gutenberg public-domain texts. I’ve found that I’m much more likely to look up a word if I can do it quickly with a single key command.

# Emacs CD and MP3 Players

Plenty of command-line music players are available for Linux. This section focuses on Emacs interfaces for the mpg123 MP3 player and the cda and cdcd music CD players. These Emacs music modes aren’t as fancy as the stand-alone X11 players such as gcd and xmcdd, but if you use Emacs a lot and don’t mind sacrificing a portion of one of your Emacs frames, they can be quite convenient. X11 players can become buried behind stacks of windows or might be in another virtual desktop. It is distracting to shufﬂe through a complicated screen layout when all you need is to ﬁnd the player’s controls. An Emacs music player is just another buffer and can be accessed from the Buffers menu.

# A CD Interface

Matthew Hodges wrote cdi.el, a versatile CD-playing mode that displays the track, artist, and disc names in a narrow window and offers the expected commands for the various playing operations. Both of the command-line players support look up CDs (if you are on the Internet) by accessing a CD database server and pulling down the title, artist, and track information for current and future use.

cdi.el is a single-ﬁle package that can be dropped into your site-lisp directory. These two lines in your ~/.emacs ﬁle enable the extension:

```
(require 'cdi)
(global-set-key [(control c) (z)] 'cdi-start)
```

The second line is optional and could be set to any convenient and available binding. If you don’t choose to assign a keybinding, pressing M-x and typing

```
cdi-start
```

will start a new cdi session.

The Cdi interface is a short window with the disc, track, and elapsed time displayed at the top.

While the Cdi window has focus, press Ctrl-h b (the bindings help key), and a window similar to the top one in Figure 15.6 will appear. This mode assigns mnemonic keys such as p for play/pause and > for next track.