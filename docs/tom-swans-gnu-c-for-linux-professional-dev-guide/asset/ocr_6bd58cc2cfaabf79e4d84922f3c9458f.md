# X WINDOWS

There are two types of X windows—input and output, and input only. Input and output windows are the most common because most windows display at least some type of visual response to user input. A button, for example, typically indicates visually that it has recognized a mouse click.

As a structure, a window possesses attributes that determine visual aspects such as the window’s border patterns, background color, size, and position. It’s important always to remember that these and other specifications are only “hints” to the X server about how a window should be displayed. The actual appearance, location, size, and other visual features of a window depend on the rules and regulations enforced by the window manager.

There are two ways to create windows. A simple window specifies only minimal attributes such as position, size, foreground, and background colors. Other attributes are inherited from the parent window. You can also create windows the “hard way” by specifying a structure and bit mask that provides any attributes you want to override from the parent. (Chapter 27, “Controlling Xlib Input and Output,” explains this technique.) However, regardless of how you create a window, depending on the window manager and the hardware’s limitations, the actual output might appear very differently from one display to another.

Using toolkits and widgets helps minimize those types of differences by providing useful standards for common components such as menu items, buttons, check boxes, dialogs, scrollbars, and other types of visual objects. Although such standards have been extremely lax in the history of X, the current Gnome project promises to provide better and more visually consistent components for creating and customizing a virtual desktop.

# THE GRAPHICS CONTEXT

All output requests take place in reference to a graphics context, or GC. The GC specifies parameters such as line width, a colormap, fill patterns, and other characteristics for many Xlib functions such as XDrawLine() and XFillRectangle(). The GC minimizes the number of arguments passed to Xlib functions, and thus has a positive effect on network traffic between the client application and X server. The GC also helps you maintain multiple configurations. For example, a program can create multiple GCs for a specific window and easily switch between them. The actual GC for a particular window resides in the X server and is referenced by a simple ID value provided to the client. This keeps GC references fast.

> Tip
> Some X servers can maintain only a limited number of GCs, and most X experts recommend creating as few as possible in client applications.

In most all cases, a client creates a GC after it creates an associated window. Every GC is tied specifically to a window, and it uses whatever attributes are assigned during the window’s creation (or reassigned later). There are numerous ways to create and initialize GCs, but in