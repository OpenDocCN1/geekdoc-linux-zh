The machine is the name of the machine on which the X server is running. It might be blank if the server is running on the local machine.

The `dispNum` is a number specifying the display number.

# Background Material

It is possible to have more than one display on a given machine. For example, under Linux, you can run two completely separate X servers in different virtual consoles. One would be display 0 and the other display 1.

The `screenNum` is the screen number. A multheaded display can have more than one machine.

On my network, I’m running a terminal on the machine *shvey* and the X server on *shishi*. The display for the client on *shvey* is called *shishi:0.0*. You can specify the display when you start an X Client with the -display option, but usually you set the DISPLAY environment variable to the display’s name. The startup process for X automatically sets the variable correctly for local clients.

# Window Managers

Another design feature of X is that it provides mechanism, not policy. That is, the core X system provides a mechanism for drawing windows, rendering text, and handling mouse and keyboard events. It does not specify how windows should look, what a particular mouse click should do, or which keystrokes do what. For example, X does not specify which keystrokes open or close windows, minimize them, and so on.

The policy or look-and-feel of the interface is left up to the window manager. The window manager is an ordinary X client that with has special powers. It draws decorative frames around windows, draws any required buttons, and provides means for users to resize, move, open, and close windows.

Figure 4.1 illustrates the X architecture. The figure shows an X server running on the local workstation. There are two local X clients connected to the server, as well as a window manager. In addition, there is a remote X client that is connected from another machine.