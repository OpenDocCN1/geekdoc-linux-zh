To select a font server, add entries in the following form to the FontPath entry in the Files section:

```
transport/hostname:port
```

Generally this will be something like the following:

```
tcp/myserver:7100
```

In this example, tcp is the protocol, which is the usual protocol for fonts. myserver is your font server, and 7100 is the port. This is the normal font server port.

For more information on setting up a font server, see the xfs man page.

# ## LOADING AND QUERYING RESOURCES

Generally, resource definitions are put in a file called ~/.Xresources. If you want to update your resources after you’ve logged in, update this file and run the following:

```
$ xrdb -merge ~/.Xresources
```

If you want to see what resources are currently in use, run this:

```
$ xrdb -query
```

![](bbox=[0.0, 0.488, 0.075, 0.891])

# # PROJECT: AUTO-SHRINKING XTERM

Most people just use X resources to make simple modifications to colors or fonts. Even then, they generally just copy the X resources from another user without ever really understanding what the resources are doing. In this short project, we’ll investigate an interesting set of resources in xterm: Translations.

Translations in xterm enable you to execute certain actions in response to events. Often these events are key presses or mouse clicks (a good way to build macros), but there are other events such as when the mouse enters or leaves the window.

Say you want the xterm to shrink whenever the mouse leaves its and then grow when the mouse enters. This way, you could have many xterms on the screen and could somewhat watch what they were doing without having them take over your entire desktop. This can be very handy when you have a lot of compilations going on. You might want to watch them all to see when one completes, but you don’t really care what the output looks like most of the time.

To get this effect, you can instruct xterm to change its font in response to mouse actions. The following X resource would do this:

```
shrinkerterm*VT100.Translations: <EnterWindow>: set-vt-font(d)  \n\
                              <LeaveWindow>: set-vt-font(l)  \n
```