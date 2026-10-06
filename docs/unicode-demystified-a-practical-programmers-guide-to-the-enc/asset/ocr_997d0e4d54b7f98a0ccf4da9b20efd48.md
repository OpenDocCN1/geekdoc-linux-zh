# X Window System 195

The -- option (the -- option but preceded by -, as most options) starts separates options from the startx command itself from options to be passed to the X server. Any options that appear before the -- option are treated as options to the X server, which passes options after -- to the server.

The most common reason for starting a X server is to have a second display with a different number of bits allocated to each screen. (Refer to “Virtual Consoles” on page 193 for more information on how to switch to a virtual console for a second server.) Having more bits per pixel means that you can display more colors simultaneously. Most X servers for GNU/Linux default to 8 bits per pixel, which permits the use of any combination of 256 colors simultaneously. Starting an X server with 16 bits per pixel permits the use of any combination of 65,536 colors at the time. The number of bits per pixel you can depends on your computer graphics hardware and your X server. The most common values that are allowed are 8, 16, 24, and 32 bits per pixel. The following command starts a X server running at 16 bits per pixel.

```
$ startx --depth 16 :1 &
```

Of course, you can use 16 bits per pixel with your first X server as well:

```
$ startx --depth 16 &
```

| xhost Grants Access to a Display |

If you get an error message when you try to open a window on a remote display, you need to have the remote user run xhost to grant you access to the display. For example, if you are logged in on a system named kudos and you want to create a window on Alex's display, Alex needs to run the following command:

```
$ xhost +kudos
```

If Alex wants to allow anyone to create windows on his display, the following command line grants access to all hosts:

```
$ xhost +
```

If you frequently work with others over a network, you may find it convenient to add an xhost line to your .profile or .login file. Be selective about granting access to your X display with xhost; if you allow another machine to access your display, you may find that your work is often interrupted by others.

# Stopping the X Server

When you set up your .xinitrc file as described, terminating your window manager causes the X server to quit. How do you terminate your window manager depends on which window manager you are running and how it is configured. When X does