runlevel such as A for data and B for fax. When you know which you need, you simply spawn the appropriate one from one of the following command lines:

```
telinit A
telinit B
```

The appropriate getty is put on the line until the first call is received. When the caller terminates the connection, the getty drops because, by definition, on demand will not respawn.

> > **Note:** The previous example is just a contrived example. For fax and data capability, use mgetty.

The other two letters, S and 0, are special. As noted earlier, S brings your system to maintenance mode and is the same as changing runlevel to runlevel 1. The Q is used to tell init to reread inittab. The inittab file can be changed as often as required, but will only be read under certain circumstances:

+   - One of its processes dies. (Do you need to respawn another?)
+   - On a powerfail signal from a power daemon (or the command line)
+   - When told to change runlevel by `telinit`

The Q argument tells init, “I’ve changed something, please reread the inittab.”

# # THE INITTAB FILE FROM TOP TO BOTTOM

Within the actual inittab, lines beginning with a # sign are disabled and left as examples or explanatory remarks, or as examples for possible future use. Be sure to read the comments throughout. These comments might give you a hint as to how to effectively customize inittab. Most programs, such as mgetty or fax, which were meant to run from inittab come with examples in their documentation showing how to implement them.

Because you already know how to read a line (`id:runlevel:action:process`), here’s a look at what each line does:

+   - `id:5:initdefault:`
+   
+     The first line of interest is the default runlevel line. As you’ll see later, this is what determines whether you boot into a graphical screen or a command-line terminal. This must never be set to 0 or 6.
+   
+   - `s0::sysinit:/bin/bash -c 'C=/sbin/booterd; [ -x $C ] && $C'`
+     `s1::sysinit:/bin/bash -c 'C=/etc/rc.d/rc.modules; [ -x $C ] && $C default'`
+     `s2::sysinit:/bin/bash -c 'C=/etc/rc.d/rc.serial; [ -x $C ] && $C'`
+     `bw::bootwait:/etc/rc.d/rc.boot`
+   
+     Just below the default runlevel line, you’ll see the system initialization script calls. Line ID s0, which calls booterd, is one of two programs that handles the Lizard boot screen (as long as the vga = 274 has not been removed from /etc/grub/menu.lst or /etc/lilo.conf). Line ID s0 loads the default modules listed in /etc/modules/defaults via