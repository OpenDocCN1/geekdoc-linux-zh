The last thing I found in the `README` file was that a bit of configuration needed to be done. I added a `MANPATH` variable to my `$HOME/.bashrc` to identify the location of man pages on my computer to be searched by the `whichman` utility. The line I added looked like this:

```
```
export
MANPATH=/usr/share/man:/usr/man/man1:/usr/X11R6/man:/usr/share/doc/samba-2.2.3a/docs
```
```

In case you are wondering, `whichman`, `ftwhich`, and `ftf` are commands that you can use to search for man pages. They can be used to find several locations of a man page, man pages that are close to the name you enter, or man pages that are located beneath a point in the directory structure, respectively.

# ## Running X Window Applications

Setting up and configuring the X Window System to your liking is the hard part. By comparison, using X to run applications is relatively easy. If you have used Microsoft Windows operating systems, you already know the most basic ways of running an application from a graphical desktop. X, however, provides a much more flexible environment for running native Linux applications.

> **CROSS-REFERENCE:** See Chapter 3 for information on setting up an X desktop.

# ### Starting applications from a menu

To run applications on your own desktop, most X window managers provide a menu, similar to the Microsoft Start menu, to display and select X applications. Applications are usually organized in categories. From the `GNOME` or `KDE` desktops in Fedora Core, open the red hat menu, select the category, and then select the application to run. Figure 5-1 shows an example of the Fedora Core Applications menu and the Sound & Video submenu.