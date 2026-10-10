keys.el file presents you with a simple list of your keybindings. No longer will you need to page through a large .emacs file, looking for a particular keybinding.

# Edit and Then Re-Byte-Compile

If you have byte-compiled .emacs, don't forget to repeat the process if you make any changes to the original .el file. Emacs always loads the speedier byte-compiled .elc files rather than the human-readable .el files, so any changes you make will not take effect until byte-compilation is repeated.

# A Little Reassurance

If this account of broken .emacs files and malformed Lisp statements sounds daunting, take heart. The usual method of customizing Emacs with Lisp is slowly incremental, and dealing with a single problem at a time isn't really much work. As time permits, you will eventually develop an initialization file that smooths your work.

A custom in the Emacs community is very helpful to the newcomer. The vast majority of Emacs add-on packages include a section of commented-out installation instructions at the beginning of the primary Lisp file. These instructions nearly always include several lines of Lisp code that can be copied and pasted into an .emacs file. These lines are necessary for the proper usage of the package. The programmers who write these packages primarily write them for their own use, but when other people begin using them, the impulse to fix bugs and develop the package further seems to increase. One way to encourage this is to make the package accessible to new users. Sometimes a package ends up serving an entire community of users, many of whom contribute patches and bug reports, thus enhancing the package for everyone. The Gnus news-and-mail reader, maintained by Lars Magne Ingebrigtsen, is a perfect example. Over the past several years, this very complex and featureful extension to Emacs has gained enough adherents to merit a Usenet newsgroup of its own, ntp://gnus.emacs.gnus.

# Trying out the Sample Files

On the CD-ROM that accompanies this book there are several sample .emacs files located in the directory /lisp/samples. These files are meant for experimentation and would need to be adapted to your system in order to actually be useful. Look at them as a source of Lisp snippets that can be copied and pasted into your personal file.