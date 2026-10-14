
## INTER-CLIENT COMMUNICATION

Atoms are the only reliable method for one client to communicate with another. Although you might be tempted to use other techniques, keep in mind that, in a networked environment, two clients must run on physically separated machines, possibly of different types. It isn’t safe to use temporary files even for inter-client communications. Instead, consider using atom properties to transmit information. If the atom is associated with the root window, then you can be sure it is available to all clients running on the user’s X server.

One of the best and easiest ways to pass information between clients is to use one of the eight cut buffers provided by the X server. A cut buffer—otherwise known as the Clipboard—is an atom property with the names XA_CUT_BUFFER0 through XA_CUT_BUFFER7. Most clients use the first cut buffer to transfer text information between them. Listing 28.4, xcut.cpp, demonstrates how a client can be notified when this cut buffer changes and also how to retrieve the buffer’s contents.

```
Listing 28.4  X CUT.CPP (PARTIAL)

// Specify the types of events we want to receive
//
XSelectInput(display, win,
ExposureMask | KeyPressMask | PropertyChangeMask );
XSelectInput(display, DefaultRootWindow(display),
PropertyChangeMask);

// The event loop
//
bool done = false;
XEvent event;
int nbytes = 0;
char *s = NULL;
while (!done) {
```

### LISTING 28.4 CONTINUED

```
XNextEvent(display, &event);
switch (event.type) {
case Expose:
    cout << "Expose event received" << endl;
    break;
case PropertyNotify:
    cout << "PropertyNotify event" << endl;
    s = XFetchBytes(display, &bytes);
    if (s != NULL && nbytes > 0) {
        cout << "Property changed: " << s << endl;
        XFree(s);
    }
    break;
case KeyPress:
    cout << "Keypress detected" << endl;
    done = true;  // Exit on any keypress
    break;
}
```

For a client to be notified that a cut buffer has been changed, it is necessary to specify the PropertyChangeMask for the root window. The root window owns the cut buffer atoms, so adding PropertyChangeMask to our window's events is alone not sufficient. Apparently, it doesn't hurt to select this event mask for the root and client windows, and this seems to ensure that the event is generated initially when the window comes into being. But if you don't want to do that, you may delete PropertyChangeMask from the first call to XSelectInput().

### Note

> You don't have to elect notification of a change to a cut buffer. Alternatively, you can access a cut buffer using the same techniques shown here in response to another type of event—for example, a mouse button click or a keypress. You might, however, want to use PropertyChangeMask to set a flag that indicates information is newly available in a cut buffer. Typically, a client does this to enable a Paste menu command or button, often called a Yank command in UNIX.

The switch case for the PropertyNotify event is selected when the user causes data to be inserted into the cut buffer. The program calls XFetchBytes() to retrieve the information—this always uses the first buffer identified as XA_CUT_BUFFER0. To use the other cut buffers, you can call the similar XFetchBuffer() function. To insert data into a buffer, call XStoreBytes() or XStoreBuffer().

Always call XFree() as shown in the sample program to delete string data returned by XFetchBytes() or XFetchBuffer(). This is a copy of the information held in the server, so deleting it does not prevent it from being used again.

## LINE AND FILL STYLES

All graphics output in an X client application takes place in reference to a graphics context, or GC. This and the preceding two chapters show numerous examples of creating and using simple GCs, but this section explains some other more advanced features that you will undoubtedly want to use. With a GC, you can select the style of lines and also set a pixmap pattern to use for filled objects such as arcs and rectangles.

### LINE WIDTH AND STYLE

The X server is capable of drawing lines in any practical width and in a variety of styles. Line styles affect not only straight lines but also the outlines of other shapes, so these concepts come into play in nearly every graphics program. Listing 28.5, xdash.cpp, shows the easiest way to create solid and dashed lines. The program also shows one way to change the width of dashes—an obscure feature that is neither obvious nor well explained in many tutorials. Figure 28.3 shows the program’s window. (The third line’s background color might or might not be visible on this page, but it should be a pale yellow onscreen.)

### Figure 28.3

Sample xdash.cpp window showing three line styles: LineSolid, LineOnOffDash, and LineDoubleDash.

![](img/6eab91cc30158075ed10d0cabbac9029_732_0.png)

### LISTING 28.5 XDASH.CPP (PARTIAL)

```
// Create a graphics context for our window
//
XGCValues gc_values;
unsigned long gc_mask = GCDashList;
gc_values.dashes = 24; // Width of dashes and spaces
GC gc = XCreateGC(display, win, gc_mask, &gc_values);

// Paint lines in different styles
void PaintLines(Window win, GC gc,
    int winWidth, int winHeight)
{
    int x1, y1, x2, y2;
    unsigned int lineWidth = 8;

    x1 = 0;
    y1 = lineWidth * 6;
    x2 = winWidth;
    y2 = y1;

    XSetForeground(display, gc, colors[0]);
```
