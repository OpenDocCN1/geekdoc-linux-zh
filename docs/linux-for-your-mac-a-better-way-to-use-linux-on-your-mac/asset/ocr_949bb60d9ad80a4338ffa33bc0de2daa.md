![](bbox=[0.23, 0.08, 0.97, 0.4])

Figure 8.4  *The x11x client displays characters in X11 fonts.*

Want to use a really big cursor during your X sessions? Browse to the site, http://www.linuxdoc.org/HOWTO/mini/X-Big-Cursor.html and read the X Big Cursor-HOWTO to find out how!

# ### Changing Pointer Buttons

If you use a three-button mouse but are left-handed, remap the mouse buttons using the `xmodmap` client. Use `xmodmap` and its `-e` and `pointer` options like this:

```
`# xmodmap -e "pointer = 3 2 1"`
```

After you press Enter, the buttons will be reversed.

# ## Using X11 on a Network

X was built from the ground up to work over a network. As you learn more about using Linux and the X Window System, you will find newer, faster, and more efficient ways to work over a network. This section introduces a few basic ideas you can use if you use a Macintosh running Linux on a network.

Most PC users sit down at their computers, then launch and run programs from the computer’s hard drive. This is the only way to use Linux and X if the computer is not attached to a network. However, if the computer is on a network, you can log in at another computer on the network to do work.