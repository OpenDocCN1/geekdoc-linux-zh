
## TABLE 22.8 Xlib Event Functions

| Xlib Function Name | Description |
|---|---|
| XNextEvent | Copies the first event from the event queue into the specified XEvent structure and then removes it from the queue |
| XLookupString | Translates a key event to a KeySym and a string |
| XSetForeground | Sets the foreground attributes of a given GC |
| XDrawString | Draws text characters in a given drawable |
| XSetStandardProperties | Provides a means by which simple applications set the most essential properties with a single call |
| XSelectInput | Requests that the X server report the events associated with the specified event mask |
| XCreateGC | Creates and returns a GC; can be used with any destination drawable with the same root and depth as the specified drawable |
| XSetBackground | Sets the background attributes of a given GC |
| XClearWindow | Clears the entire area in the specified window |
| XMapRaised | Maps the window and all of its subwindows that have had map requests and raises the window to the top of the stack |
| XFreeGC | Destroys the specified GC as well as all the associated storage |
| XDestroyWindow | Destroys the specified window as well as all of its subwindows and causes the X server to generate a DestroyNotify event for each window |
| XCloseDisplay | Closes the connection to the X server for the display specified in the display structure and destroys all windows and resource IDs |
| XClearWindow | Clears the entire area in the specified window |

```
Window win;
GC gc;
/* X routines */
void init_x();
void close_x();
void redraw();
main () {

/*Initialization*/

    XEvent event; /* declare the XEvent */
    KeySym key;   /* KeyPress Events */
    char text[256];   /* char buffer for KeyPress Events */
    init_x();

/* Start the Event-Request Loop*/
    while(1) {
        /* get the next event.
           We set the mask for events that we want detected
        */
        XNextEvent(dis, &event);
        if (event.type==Expose && event.xexpose.count==0) {
/* the window was exposed redraw it! */
    redraw();
}
if (event.type==KeyPress&&
    XLookupString(&event.xkey,text,255,&key,0)==1) {
/* use the XLookupString routine to convert the event KeyPress data into regular text.
*/
    if (text[0]=='q') {
        close_x();
    }
    printf("You pressed the %c key\n",text[0]);
}
if (event.type==ButtonPress) {
/* report where the mouse Button was Pressed */
    int x=event.xbutton.x;
    y=event.xbutton.y;
    strcpy(text,"UNIX Rocks");
    XSetForeground(dis,gc,rand()%event.xbutton.x%255);
    XDrawString(dis,win,gc,x,y, text, strlen(text));
}
}
void init_x() {
/* Set the colors black and white */
    unsigned long black,white;

    dis=XOpenDisplay((char *)0);
    screen=DefaultScreen(dis);
    black=BlackPixel(dis,screen),
    white=WhitePixel(dis, screen);
    win=XCreateSimpleWindow(dis,DefaultRootWindow(dis),0,0,
        300, 300, 5,black, white);
    XSetStandardProperties(dis,win,"Report","E",None,NULL,0,NULL);
    XSelectInput(dis, win, ExposureMask|ButtonPressMask|KeyPressMask);
    gc=XCreateGC(dis, win, 0,0);
    XSetBackground(dis,gc,white);
    XSetForeground(dis,gc,black);
    XClearWindow(dis, win);
    XMapRaised(dis, win);
};

void close_x() {
XCloseDisplay(dis);
    exit(1);
};

void redraw() {
    XClearWindow(dis, win);
};
```

### 22.4.3.3.3 Xlib Example Program test1.c

Objective: Produce a simple window on the display that prints Hello, World! and draw a small filled-in rectangle in black. It may be closed by pressing <Ctrl+C>.

New functions called (Table 22.9):

Code:

```
/*
 * Simple Xlib application drawing a box in a window.
 */
#include <X11/Xlib.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void)
{
    Display *display;
    Window window;
    XEvent event;
    char *msg = "Hello, World!";
    int s;

    /*Initialization*/

    /* open connection with the server */
    display = XOpenDisplay(NULL);
    if (display == NULL)
    {
        fprintf(stderr, "Cannot open display\n");
        exit(1);
    }
    s = DefaultScreen(display);

    /* create window */
```

## TABLE 22.9 Xlib Drawing Function

| Xlib Function Name | Description |
|---|---|
| XFillRectangle | Fills the specified rectangle or rectangles as if a four-point FillPolygon protocol request were specified for each |
