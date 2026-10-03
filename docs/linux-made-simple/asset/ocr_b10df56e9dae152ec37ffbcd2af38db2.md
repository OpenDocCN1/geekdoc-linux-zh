want to do a quick Wikipedia check, or search the Gentoo documentation for the USE flags required to make your login manager work. In this case, something such as Lynx or Links (in text mode) is all you need. However, many web pages don't render terribly well; Lynx doesn't support CSS or JavaScript, for instance, and while Links does support JavaScript, it might not help much in text mode. Links does, however, have a graphical mode which makes use of a framebuffer. In this mode frames, tables and images are supported, but don't worry – it can't do Flash.

The lightest web browser for X is the fltk-based Dillo, which manages to squeeze both substantial CSS support and tabbed browsing into its tiny footprint. Its lack of JavaScript support and history-keeping can be seen as security features. Cookies are supported, but turned off by default. Likewise basic SSL transactions, although users are warned that this support is very much in an alpha state. Luakit (GTK+) and dwb both use the Webkit engine to provide standards-compliant rendering with thoroughly minimal interfaces. They both rely rather heavily on keyboard shortcuts and are

> “Dillo squeezes tabbed browsing into its tiny footprint”

both thoroughly extensible. More conventional Webkit-based browsers include Midori (GTK+) and QupZilla (Qt).

# Email clients

Mutt is a terminal-based email client that's been around since the mid-90s. It supports IMAP, SMTP, SSL, GPG and third-party plug-ins. Of course, there are some keyboard shortcuts to learn, and if you want to look at your mail offline you'll need to set up offlineimap (IMAP) or getmail (POP). Mutt uses the external text editor of your choosing, and you can make a sort of address book using aliases, or use the purpose-built Abook application. Back in 1991, the Pine email client was released, but source code was only available for UNIX. Pine was pretty easy to learn, and came bundled with a simple-but-powerful text editor called Pico. The GNU Nano editor we all know and love is a clone of this. The Apache-licensed Alpine (Alternatively Licensed Pine) was released in 2007 and although it is no longer under active development, a project

called Re-alpine sought to continue it. The latest release of Re-alpine was in mid-2013.

On the graphical front we have Sylpheed and its slightly more featureful fork Claws Mail, both of which use GTK+2 and support various plug-ins. Sylpheed does almost everything you need and absolutely nothing more. Claws Mail, meanwhile, offers support for spam filtering, GPG and can render HTML mail through Webkit. If you like Qt and IMAP, then you should have a look at Troidy* which supports HTML mail (through Webkit) and has been designed to be as gentle as possible with respect to resource usage.

# Music players

MPD (Music Player Daemon) is a superb program that will maintain a database of your music collection and play tracks in response to commands from a (possibly remote) client program, of which there are many. It is incredibly lightweight, which means it's possible to use it with a ncurses-based console client such as ncurses (or the even more confusingly named ncmpcpp) without your CPU even noticing. MPD isn't shy of features; it plays anything the FFmpeg library understands (in other words, anything), Spotify and SoundCloud playlists are supported, and all manner of plug-ins are available. If you just want a simple ncurses music player, then your first stop should be Cmus or Herrie.

There are graphical clients for MPD, too, such as Xfmpc for XFCE and Gimmix, but development seems to have dried up on most of the other GTK+ ones. On the Qt front, all we were able to come up with was Cantata. In terms of standalone applications, there is the superbly-titled Deadbeef, which uses GTK+2 or 3 and not much else, yet supports all manner of formats, tag editing, gapless playback and has many plug-ins available.

Slightly larger, but far from overweight, is the mighty Audacious, which you can make look like Winamp/XMMS. Similarly, for Qt check out Qmmp. Speaking of XMMS, XMMS2 is a client/server project that aims to continue the legacy of its hugely popular predecessor. Clients catering to all tastes are available: https://xmms2.org/wiki/Clientlist.

# Image viewers and editors

You can view pictures at the console, and all you need to use is Lars Solberg's Shellpic. It's written in Python, only depends

![](bbox=[0.15, 0.67, 0.59, 0.88])

![](bbox=[0.6, 0.67, 0.93, 0.88])

Terminator running shellpic, links and mc. You could have done much more governating this way, Arnold.

The Dillo browser does a great job at rendering http://dillo.org; YMMV works for other sites.