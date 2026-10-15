```
/* Map the window on the screen */
xcb_map_window (c, win);

/* Make sure commands are sent before we pause, so window is shown */
xcb_flush (c);

pause ();   /* hold client */
/* Cleanup */
xcb_disconnect(c);
return 0;
}
```

# EXERCISE 22.21

What basic component of an X Windows client application is missing from the preceding program, and particularly what aspect or part of that component? How do you close the window without using the KDE4 window manager kill button?

# 22.4.4.2.2 XCB Example Program 2ndxcbdraw.c Objective: Draw a rectangular box in a window

Code:

```
#include <stdlib.h>
#include <stdio.h>
#include <xcb/xcb.h>
int
main ()
{
    xcb_connection_t    *c;
    xcb_screen_t        *screen;
    xcb_drawable_t      win;
    xcb_gcontext_t      foreground;
    xcb_generic_event_t *e;
    uint32_t            mask = 0;
    uint32_t            values[2];

    /* geometric objects */
    xcb_rectangle_t     rectangles[] = {
        { 10, 50, 40, 20 },
        { 80, 50, 10, 40 }};

    /* Initialization */
    /* Open the connection to the X server */
    c = xcb_connect (NULL, NULL);
```