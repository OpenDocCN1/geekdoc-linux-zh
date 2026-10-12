# ## 17.6 X window system

The X window system (it’s a window system called “X,” not a system called “X Window”) is the base on which all Linux graphical workstations are built. It is also available for almost every UNIX platform, and many others too, including Windows and Macintosh, and many handheld computers and PDAs (personal digital assistants). On some systems, especially Windows, it is a chargeable extra, usually supplied by third-party vendors.

The current (and only foreseeable) version of X is X11.

![](bbox=[0.16, 0.24, 0.9, 0.51])

Figure 17.11 Unique features of the X window system

As window systems go, X has some unique features, illustrated in Figure 17.11:

+   - it is a client/server system, from the ground up
+   - the *display server* (or *X server*) controls the graphics display, keyboard, and mouse
+   - the *client* is the application program that:
+     - sends *requests* to the server to draw lines and characters on-screen
+     - receives *events* from the server, containing mouse movements/clicks, and keyboard input

In other words, the server is on the workstation you’re sitting at, and the client is the application that may be running locally on the same workstation, or remotely on another machine on the network. You can think of it as the client sending pictures of its windows across the network, to be displayed on the server’s screen. (The terminology seems backward compared with, for example, file servers and Web servers, where the server part is remote. However, if you remember that the server is something that provides a service and accepts requests from clients to do things – display graphics in this case – it makes sense.)

+   - there’s no difference between a local client application and a remote one. Both of them use exactly the same protocol; the requests and events travel over the wire in one case and via a local inter-process communication method in the other