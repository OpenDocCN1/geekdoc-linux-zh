
## XTERM TRICKS THAT MAKE LIFE EASIER

### Xterm Enhancements

Every version of the X Window System comes with at least the minimum version of Xterm. Plus, many vendors include their own custom terminal window that takes advantage of some of the specifics of their system. SCO, for example, includes scoterm with its Open Desktop package, and HP includes a couple of different versions of hpterm with its systems: one for VUE, their "Visual User Environment," an all encompassing desktop environment based on X; and another for those running just the X Window System. Each of these add specific features that enhance the overall look and feel of the basic Xterm, but we'll stick to just the basic Xterm here. Most of the third-party enhanced Xterms accept the same command-line parameters as the basic version, in addition to any that control the specifics of their own implementation. The basic result of typing Xterm & is pretty boring, so let's spruce it up. You can control the fonts, colors, and all sorts of other stuff.

### Can I change the colors of Xterm to make it easier on the eyes?

Absolutely. Colors are a very personal and individual thing, but here's a combination that works for us.

```
/usr/bin/X11/Xterm -fg white -bg MidnightBlue &
```

This gives you white text on a dark blue background. Of course, we know someone who finds this look far too middle class, and opts instead for

```
/usr/bin/X11/Xterm -fg yellow -bg purple &
```

But then he's just a bit on the outer edges on most questions.

### How can I get a list of color possibilities?

Use showrgb. This will print out a list of colors that are defined in your system. Even if your system doesn't have the showrgb program, you can still see this list. Just use vi (in its read-only mode, so you don't accidentally mess something up). Type in:

```
view /usr/lib/X11/rgb.txt
```

This will give you a look at the default color database that your system uses. Pick any colors you want from here for your Xterm colors. But don't forget to enclose the color name in quotes if the name includes any spaces.

> Warning: When you type in your Xterm color selections, don't forget to enclose the color name in quotes if the name includes any spaces. A two-word color without quotes will confuse UNIX and cause the command to fail.

### Is it possible to change the title on my Xterm?

Yes. You can even have your Xterm tell you where you are and who you are logged in as by adding this information to the title bar of the Xterm. The only catch is, this information is static, so if you use the window to log into another, remote machine, it won't be accurate. But we find it useful nonetheless, since it tells us where we started from. Use the -T option like this:

```
Xterm -T "$(hostname):$LOGNAME -- $(date +%X)" &
```

This will put your hostname, login name, and time the window was started all in the title bar.

### Is there a way I can change the font in my Xterm to make it easier to read?

Of course. The older we get, the bigger the fonts have to be. We know young programmers with six or eight Xterm windows open on their screen, each one with tiny little fonts. For them, this may be OK, but we like something just a bit larger and easier on the eyes. So we use one of the larger standard fonts for our Xterm:

/usr/bin/X11/Xterm -fn 10x20 &

This makes for a large enough window to actually see what you're doing. Of course, if you're running on a display with a lower resolution than our 1280 x 1024, or you have good enough eyes and want to squeeze the window size down a bit, try

```
/usr/bin/X11/Xterm -fn 8x13 &
```

This should give something small enough for most purposes. A good middle choice is the "9 x 15" font. But examine the other choices on your system. Each vendor's implementation of X includes different fonts, so you may have some additional choices.

### How can I see which fonts are available?

Use **xlsfonts**. This program, if run with no options, will send a complete list of all the fonts you have available on your system to standard output. To limit this list, you can add the **-fn pattern** option to the command line, or pipe the whole thing through **grep** to see a more limited list.

### Can I see ahead of time what a font will look like, and what characters are available for it?

Yes. **xfd -fn fontname** will show you all the characters for that font, as well as give you far more information about each individual character than you are likely to need.

### Is there a way I can add scrollbars to my Xterm to make it easy to scroll back through text?

Certainly. In fact, we're sure this will quickly become your standard Xterm. You can add scrollbars to the standard Xterm by using the command-line option **-sb**, which will put a simple scrollbar on the left side of the window like the one in Figure 8-1.
