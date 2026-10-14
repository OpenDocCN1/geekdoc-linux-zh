# WINDOW CANVAS

Much of a window's visual activity is handled by painting graphics and text on a window's canvas. To provide for this, the application creates a window canvas object of a class derived from one of several that V provides.

In the sample generated application, the main window's canvas object is of a class named myCanvasPane, derived from the vCanvasPane base class. Listing 29.5 shows this class's declaration (edited for prime-time viewing here).

# LISTING 29.5 MYCVN.H (PARTIAL)

```
#include <v/vcanvas.h>

class myCanvasPane : public vCanvasPane {
public:
    myCanvasPane();
    virtual ~myCanvasPane();

    // Scrolling
    virtual void HPage(int shown, int top);
    virtual void VPage(int shown, int top);
    virtual void HScroll(int step);
    virtual void VScroll(int step);

    // Events
    virtual void MouseDown(int x, int y, int button);
    virtual void MouseUp(int x, int y, int button);
    virtual void MouseMove(int x, int y, int button);
    virtual void Redraw(int x, int y, int width, int height);
    virtual void Resize(int newW, int newH);
    ...
};
```

The myCanvasPane class declares the usual constructor and destructor, along with some member functions for scrolling and handling input and output events. To respond to the user clicking the mouse inside the window's canvas area, simply override the MouseDown() function and provide whatever programming you need.

Handle graphics similarly. To paint graphics in a window, override Redraw() and call the graphical output functions you need (more on this in Chapter 30). Don't be concerned at this stage with how to draw actual objects. Be aware only that Redraw() is where you add this code for a specific window. It is the V equivalent of an Xlib program's response to an Expose event. If the window needs repainting—for example, on being exposed by the user moving another window aside—V calls Redraw() as needed to update the window's canvas. The four parameters indicate the portion of the window that requires redrawing, but except for highly complex graphics, you can simply draw everything and ignore these values. The Resize() function corresponds with the Xlib ConfigureNotify event.