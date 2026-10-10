or GNOME, because the default menu button resides in the lower-left corner of the display. The value 132 is the difference between the virtual and physical screen size (900 minus 768).

As root, open your system's XF86Config file (found under the Red Hat or Mandrake Linux /etc/X11 directory), create your settings, and save the file. If you're running xdm, kdm, or gdm, you can kill the current X session, and X will restart with the new settings. If all goes well, you'll end up with a larger resolution, and your display will “pan,” or move, when the cursor hits a boundary that has more real estate. This is a great way to get a larger display if you need it!

The other display resolutions in the sample listing allow you to toggle between screen sizes on-the-fly. If you want to use this feature, your notebook's display must support each resolution, a companion modeline entry must exist in your XF86Config file, and you must have enabled toggling by commenting out the DontZoom entry in XF86Config's ServerFlags section:

```
# DontZoom
```

# The Fine Art of Tweaking Modelines

Modelines in your XF86Config are lines of text that define possible resolutions, along with associated graphics chip clock settings and resolutions for your LCD. XF86Re6 comes with a default XF86Config file named XF86Config.efg (found under the /usr/X11R6/lib/X11 directory) that provides many different default settings. Although most notebook users will find acceptable defaults that work well, you might need to create your own settings. Be careful! Using memory, monitor, resolution, clock, or frequency settings out of range could damage your display! Always be prepared to kill a test X session with Ctrl+Alt+Backspace when testing. The best approach is to browse the Linux laptop pages for the exact model of your laptop and to use any recommended settings. If you're still determined, first read Eric S. Raymond's Video Timings HOWTO (see the “Resource Information” section at the end of this chapter).

Toggling resolutions on a desktop PC with a normal keyboard is quite easy; press Ctrl+Alt+KeyPad++ (plus) or Ctrl+Alt+KeyPad− (minus). Performing this stunt on a notebook can be a little trickier, because few, if any, notebooks come with a separate keypad (although you can buy one that plugs into your PS2 port). Toggling resolutions on a notebook usually involves pressing Ctrl+Alt along with a special Fn key and then the + or − keypad keys (which are enabled when you use the NumLock key on your notebook's keyboard).