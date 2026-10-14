And that's it—a complete V application ready to fill with your own code. Before continuing to the next sections for a look at how to implement menus, toolbars, status bars, graphics, and other features, you might want to review the preceding discussion. As mentioned, all other sample programs in this chapter build on vWelcome's modules.

> Note
> Not counting comments and conditional directives, the total number of lines in vWelcome is about 110 versus 158 lines for the similar xWelcome Xlib application in Chapter 26, "Introducing X Programming." Even ignoring its pull-down menu and potential for other GUI elements, the V application's source code is about one-third smaller than the Xlib equivalent—another good example of how C++ classes and object-oriented programming can reduce complexity in software development.

# SOFTWARE DEVELOPMENT WITH V

As with most programming tools, after you learn how to get a V application up and running, you might wonder how to handle input and output. Because a V application is, of course, an X client, the same observations made for Xlib programming in Chapters 26 through 28 apply. However, instead of making requests to the X server and responding to server events, a V application uses two input and output techniques: responding to command events such as menu selections in a window's CommandWindow() function and overriding virtual member functions to handle specific actions such as mouse button clicks and cursor movements. The following sections show examples of both methods.

# GRAPHICS

All graphics output in a V application is made in reference to an object of the vDC class. The DC in this class name stands for "Device Context," but in Xlib programming, this is called a GC for "Graphics Context." No matter—DCs and GCs are conceptually the same, although a vDC object is much more convenient to create and use.

The vDC class provides for the characteristics of graphical output including colors, outline widths, and the pattern and color used in filled shapes. As a C++ class, vDC provides graphics functions for creating output. For example, if pDC is a pointer to a vDC object, a program can draw a line using the following statement:

```
pDC->DrawLine(x1, y1, x2, y2);
```

Although that's one way to draw graphics, another more common way is to call similarly named functions from a window's canvas object. Most windows own a canvas object of a class derived from vCanvasPane. By deriving a new class from that one and creating this object for a window, you provide a simple way to create graphical output. The next program demonstrates how to do this in a sketch application that lets you draw lines by clicking and dragging the mouse. The program also demonstrates how to respond to mouse button and movement events.