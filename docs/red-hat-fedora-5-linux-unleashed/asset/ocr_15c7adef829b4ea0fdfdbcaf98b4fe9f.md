+   
+   - `joe`—Joe's Own Editor, a text editor, which can be used to emulate other editors
+   - `mcEdit`—A DOS-like text editor for UNIX-like systems
+   - `nano`—A simple text editor similar to the `pico` text editor included with the `pine` email program
+   - `sed`—A stream editor usually used in shell scripts (discussed in Chapter 15)
+   - `vim`—An improved, compatible version of the `vi` text editor (which we call `vi` in the rest of this chapter because it has a symbolic link named `vi` and a symbolically linked manual page)
+   

Note that not all text editors described here are *screen-oriented*; editors such as `ed` and `sed` work on a line-by-line basis, or a stream of text, and do not support movement of a cursor on the screen. Some of the text editors for the X Window System, which provide a graphical interface such as menu bars, buttons, scrollbars and so on, are

+   
+   - `gedit`—A GUI text editor for GNOME
+   - `kate`—A simple KDE text editor
+   - `kedit`—A simple KDE text editor
+   - `nedit`—A programming text editor
+   - `karate`—A simple KDe text editor
+   

A good reason to learn how to use a text-based editor, such as `vi`, is that system maintenance and recovery operations generally never take place during X Window sessions (negating the use of a GUI editor). Many larger, more complex and capable editors do not work when Linux is booted to its single-user or maintenance mode. See Chapter 15 for more information about how Fedora boots. If anything does go wrong with your system, you probably won't be able to get into the X Window system, making knowledge and experience of using both the command line and text editors such as `vi` important. Make a point of opening some of the editors and playing around with them; you never know, you might just thank me someday!

Another reason to learn how to use a text-based editor under the Linux console mode is so that you can edit text files through dial-up or network shell sessions because many servers do not host graphical desktops.

# ## Working with `vi`

The editor found on nearly every UNIX and Linux system is, without a doubt, the `vi` editor, originally written by Bill Joy. This simple-to-use but incredibly capable editor features a somewhat cryptic command set, but you can put it to use with only a few commands. Although more experienced UNIX and Linux users continue to use `vi` extensively during computing sessions, many newer users might prefer learning an easier-to-use text editor such as `pico` or GNU `nano`. Die-hard GNU fans and programmers definitely use `emacs`.