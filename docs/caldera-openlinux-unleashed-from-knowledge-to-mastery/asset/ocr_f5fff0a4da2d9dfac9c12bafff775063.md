whatis is useful to determine what mysteriously named programs do. For example, Caldera OpenLinux comes with a program called ldd (in /usr/bin):

```
$ whatis ldd
  ldd (1) - print shared library dependencies
```

Note that you can type man 1 ldd for more information.

# Background Material

whatis is not likely to work for KDE programs, unfortunately. KDE has its own HTML-based help system and does not include man pages for most applications. In my opinion, this is regrettable.

+   * man -a item searches all manual pages for item. As you may recall, some items are both commands and system calls (for example, chown(1) and chown(2)). If you don't specify a section, man just displays the first manual page it finds. To see all the manual pages for chown, use
+   
+       ```bash
+       $ man -a chown
+       ```
+   
+       After you finish reading chown(1), man shows the pages for chown(2).

+   * man -K keyword looks for keyword in the body of all each system man pages. This process is very slow and likely to produce huge amounts of useless information.
+   
+       But if you're desperate, you can try it.

Of course, man has many more options. To read more about these option, type the following:

```
$ man man
```

This will take to the man page for man.

# info

As the GNU project developed, its leaders invented a new documentation system called Texinfo. For its time, the system was powerful and innovative. With a single source file, Texinfo authors could generate both high-quality typeset documentation (using Donald Knuth's TeX program) and hyper-linked online documentation. The online viewer is (traditionally) character-based, making Texinfo seem rather archaic compared to modern HTML-based help systems. Still, Texinfo is very powerful and most of the GNU utilities are documented using it.