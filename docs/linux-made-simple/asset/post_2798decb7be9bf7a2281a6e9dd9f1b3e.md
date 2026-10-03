
![](img/57f4a2d286909b0a84c8ecfefbbe15f2_97_0.png)

## Software | Light apps

## Low resource applications

Got an old PC? Then we offer you this smorgasbord of lightweight applications that won't eat up all your memory.

We've covered a few lightweight Linux distros (see page 84), but the plethora of pint-sized applications out there deserves attention, too. For the vast majority of all your other Linuxing, there are some small yet perfectly formed programs that do everything you need, and do so without pulling in a truckload of dependencies and eating all your memory.

If you're really serious about resource usage, you should consider using console applications. This can be daunting at first, but once you learn the requisite quota of magic keystrokes and break out of the clicking-and-dragging mindset, you'll be surprised how much more efficient you can be.

Furthermore, in so doing you'll look much cooler. If you still don't want to go down that road, there are plenty of slimline graphical applications worth considering.

### File managers

Files are important, so a functional file manager is vital. Our first suggestion, then, is somewhat controversial – don't bother with one. Or, more precisely, be your own file manager. With some basic shell-fu, you can do all manner of balletic moving and systematic renaming, and with tab-completion you can obviate the problem of typing long filenames.

If you do crave a purpose-built file manager, but are happy with a terminal-based one, then your first stop should be Midnight Commander – sorry, GNU Midnight Commander. This is an Orthodox File Manager (OFM) offering a dual pane view with a command terminal in the style of the classic Norton Commander. It's pretty intuitive: [Tab] moves between panes, and the actions performed by Function keys are helpfully shown at the bottom. You can even use the mouse and open files in their native applications (via xdg-open) if you run it in an X session. Midnight Commander also has a native viewer and editor (hex and ascii), can open archives natively, can browse FTP sites and windows shares, and comes with some lovely themes. If you want something a little more advanced, then direct your attention to vifm, which features ‘vi-like keybindings’. As such, we shall say no more about it.

Moving on to graphical species, we’ll begin with SpaceFM. This offers a multi-panel tabbed interface and its own virtual filesystem, and it is highly customisable beyond recognition. It can be built for GTK+2 or 3 and works seamlessly with the dependency-light Udevil device-mounting program, so you’re spared asking yourself, “What is this, 2004?” when you’re prompted for the root password in order to mount a USB stick. SpaceFM can even manage desktop icons, which may appeal to you if you’re using a standalone window manager, or may be irrelevant if you consider desktop icons to be a relic from 1995.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_98_0.png)

SpaceFM, a lightweight file manager running in Gnome 3.

SpaceFM was forked from the venerable PcManFM back in the HAL days. The latter is the default file manager in Raspbian and LXDE and differs mainly in its reliance on the Gnome VFS (and hence the Udisks2 framework) for mounting of drives, shares and whatnot. If you don’t mind installing a bunch of Gnome 2 libs and want an OFM, then Gnome Commander is probably a worthy candidate. If you are a KDE person with similar desires, then try Krusader.

### The Suckless and KISS philosophies

Growing frustrated with the seemingly inexorable bloat of core tools and libraries, a community of motivated hackers have established http://suckless.org. This collective aims to produce software based on the key principles of simplicity, clarity and frugality – “software that sucks less”, to use their own words. The project is geared towards more advanced users, because this group is generally the most frustrated by the aforementioned symptoms. The collective’s efforts to date include, but are far from limited to: the dwm window manager, the dmenu menuing system, the Surf web browser and st, a simple terminal. On their website you’ll find a list of software that “rocks”, some of which is included in this article. Also, you’ll find lists of software, and assumptions made by software, that are deemed to “suck”. The more general KISS (Keep It Simple, Stupid) ideology, oft-uttered on the Arch Linux wiki but apropos to so many situations in life, aims for simplicity, eschews unnecessary complexity and strives for elegance through minimality. In terms of software, this speaks to the underlying UNIX ethos of small tools that do one thing and do it well. One can equally see it encompassing those applications (particularly graphical ones) that avoid over-worked interfaces, unnecessary features and pull in myriad software and library dependencies.

### Terminal emulators/multiplexers

If you’re using a desktop environment, then chances are you’re satisfied with the terminal program provided therein. But there are alternatives, some of them rather good.

Of particular note is rxvt-unicode, which builds on the venerable Rxvt with features such as unicode support, transparency (pseudo and true) and support for Xft fonts. It supports Perl extensions which can provide clickable URLs and a tabbed interface, although that relies on GTK+2. Somewhat uniquely, it’s built around a client server model, so once the daemon is loaded, opening terminal windows is both swift and memory-light.

If you want to be really minimal, then you should use st (Simple Terminal) from http://suckless.org, but it might come as a surprise that there’s no scrollback buffer, and that you have to edit a file to make the [Del] key work in Bash.

Next, we have the GTK-based Lilyterm, Sakura and EvilVte. Lilyterm works best with GTK+2, Sakura only with 3, and EvilVte can work with either 2 or 3. All three have very few dependencies besides the venerable Gnome VTE library and offer tabs, transparency and unicode support.

Terminals that slide down from the top of the screen à la Quake are popular too. These include Yakuake for KDE and Guake, which doesn’t require much besides VTE and the Python bindings for GTK+. There is also Tilda (the tilde key summoned the terminal in the original Quake), which doesn’t require these bindings. Having a terminal with a hotkey away is pretty useful, but sometimes you do need multiple windows, so this might not be a complete solution.

We should also mention Terminator (“the robot future of terminals”) here, since it enables the user to tile sessions in all manner of wild configurations.

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_98_1.png)

Remember also that you get a whole bunch of console terminals for free too (accessible via [Ctrl]+[Alt]+[Fn] keys). If you’re stuck at the console, you can use these as primitive tabs. Or you could up your game and get a terminal multiplexer such as tmux or screen.

These are mainly used for keeping remote programs running after logout, but can do much more – multiple sessions, scrollback buffers, copy and paste, awkward keyboard shortcuts, the list goes on.

> “If you want to be really minimal, then you should use st”

### Web browsers

Depending on what you’re doing, surfing from the console might be entirely reasonable – for example, if you simply want to do a quick Wikipedia check, or search the Gentoo documentation for the USE flags required to make your login manager work. In this case, something such as Lynx or Links (in text mode) is all you need. However, many web pages don't render terribly well; Lynx doesn't support CSS or JavaScript, for instance, and while Links does support JavaScript, it might not help much in text mode. Links does, however, have a graphical mode which makes use of a framebuffer. In this mode frames, tables and images are supported, but don't worry – it can't do Flash.

The lightest web browser for X is the fltk-based Dillo, which manages to squeeze both substantial CSS support and tabbed browsing into its tiny footprint. Its lack of JavaScript support and history-keeping can be seen as security features. Cookies are supported, but turned off by default. Likewise basic SSL transactions, although users are warned that this support is very much in an alpha state. Luakit (GTK+) and dwb both use the Webkit engine to provide standards-compliant rendering with thoroughly minimal interfaces. They both rely rather heavily on keyboard shortcuts and are both thoroughly extensible. More conventional Webkit-based browsers include Midori (GTK+) and QupZilla (Qt).

> “Dillo squeezes tabbed browsing into its tiny footprint”

### Email clients

Mutt is a terminal-based email client that's been around since the mid-90s. It supports IMAP, SMTP, SSL, GPG and third-party plug-ins. Of course, there are some keyboard shortcuts to learn, and if you want to look at your mail offline you'll need to set up offlineimap (IMAP) or getmail (POP). Mutt uses the external text editor of your choosing, and you can make a sort of address book using aliases, or use the purpose-built Abook application. Back in 1991, the Pine email client was released, but source code was only available for UNIX. Pine was pretty easy to learn, and came bundled with a simple-but-powerful text editor called Pico. The GNU Nano editor we all know and love is a clone of this. The Apache-licensed Alpine (Alternatively Licensed Pine) was released in 2007 and although it is no longer under active development, a project called Re-alpine sought to continue it. The latest release of Re-alpine was in mid-2013.

On the graphical front we have Sylpheed and its slightly more featureful fork Claws Mail, both of which use GTK+2 and support various plug-ins. Sylpheed does almost everything you need and absolutely nothing more. Claws Mail, meanwhile, offers support for spam filtering, GPG and can render HTML mail through Webkit. If you like Qt and IMAP, then you should have a look at Troidy* which supports HTML mail (through Webkit) and has been designed to be as gentle as possible with respect to resource usage.

### Music players

MPD (Music Player Daemon) is a superb program that will maintain a database of your music collection and play tracks in response to commands from a (possibly remote) client program, of which there are many. It is incredibly lightweight, which means it's possible to use it with a ncurses-based console client such as ncurses (or the even more confusingly named ncmpcpp) without your CPU even noticing. MPD isn't shy of features; it plays anything the FFmpeg library understands (in other words, anything), Spotify and SoundCloud playlists are supported, and all manner of plug-ins are available. If you just want a simple ncurses music player, then your first stop should be Cmus or Herrie.

There are graphical clients for MPD, too, such as Xfmpc for XFCE and Gimmix, but development seems to have dried up on most of the other GTK+ ones. On the Qt front, all we were able to come up with was Cantata. In terms of standalone applications, there is the superbly-titled Deadbeef, which uses GTK+2 or 3 and not much else, yet supports all manner of formats, tag editing, gapless playback and has many plug-ins available.

Slightly larger, but far from overweight, is the mighty Audacious, which you can make look like Winamp/XMMS. Similarly, for Qt check out Qmmp. Speaking of XMMS, XMMS2 is a client/server project that aims to continue the legacy of its hugely popular predecessor. Clients catering to all tastes are available: https://xmms2.org/wiki/Clientlist.

### Image viewers and editors

You can view pictures at the console, and all you need to use is Lars Solberg's Shellpic. It's written in Python, only depends

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_99_0.png)

![](img/57f4a2d286909b0a84c8ecfefbbe15f2_99_1.png)

Terminator running shellpic, links and mc. You could have done much more governing this way, Arnold.

The Dillo browser does a great job at rendering http://dillo.org; YMMV works for other sites.
