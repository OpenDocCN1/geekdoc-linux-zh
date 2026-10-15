
free(reply);

The function xcb_get_window_attributes sends the request to the X server, and returns immediately without waiting for the reply. This is an asynchronous request–event sequence. The client program must call xcb_get_window_attributes_reply to block on the reply.

The advantage of the asynchronous approach is gained when we need to retrieve the attributes of multiple windows at the same time. Using XCB, we can make multiple requests to the X server at once and then wait for multiple replies. With Xlib, we have to wait for the response to each request before we can send the next one. XCB only blocks for one round-trip network latency period, compared to multiple latency period waits with Xlib.

To be fully asynchronous, the XCB approach leads to a more complex data structure approach, and a less programmer-friendly API. The preceding Xlib code looks like your average C library call; the XCB code has a more complex data structure implementation.

XCB is fully asynchronous, whereas Xlib is not fully synchronous. Xlib has a mixture of synchronous and asynchronous APIs. Functions that do not return values (e.g., XResizeWindow, which changes the size of a window) are asynchronous, while functions that return values (e.g., XGetGeometry, which returns the size and position of a window) are synchronous. Here is a quote from Volume 1 of the *Xlib Programming Manual* dealing with Xlib’s synchronicity:

> Buffering
> 
> Xlib saves up requests instead of sending them to the server immediately, so that the client program can continue running instead of waiting to gain access to the network after every Xlib call. This is possible because most Xlib calls do not require immediate action by the server. This grouping of requests by the client before sending them over the network also increases the performance of most networks, because it makes the network transactions longer and less numerous, reducing the total overhead involved.

## 22.4.3 Xlib

In this section, we give programming examples using Xlib. It would be useful for you to compare the complexity of the code given here with the code given for XCB programming in the following section. Also, compare the extent documentation for Xlib to the documentation available for XCB.

### 22.4.3.1 Basic Xlib Theoretical Consideration

Xlib operates on the client–server model, which can be directly contrasted to the traditional networking model of those components. Essentially, the client–server model used for Xlib reverses the role of client and server assumed in the networking model. Below, we give you a practical introduction to programming in the Xlib model.

### 22.4.3.2 Compiling an Xlib Client Application Program

Be aware that, on a PC-BSD system, you may have to download and install the GNU C compiler (either version 47 or the latest version available) for the following example programs to run, if that has not already been done by your system administrator. If you are the system administrator, you can do this for yourself by using the procedures in the AppCafe in PC-BSD or by using the repository in Solaris.

On our PC-BSD system, we used the following compiler command with the options and arguments shown. On Solaris, you can substitute gcc for gcc47.

```
gcc47 input_file.c -o output_file -lX11
```

Here, input_file.c is the name of your C source code file and output_file is the name of the executable program.

### 22.4.3.3 Sample Xlib Client Application Programs

The following are three elementary sample Xlib programs. Each is preceded by a statement of what the program does and a table listing the X Window functions called along with a description of what the functions do. To get more information about the function calls—for example, what their specific argument list data structure and contents are—consult the online documentation for Xlib given at the end of this chapter.

### 22.4.3.3.1 Xlib Example Program test2.c Objective: Draw a black 500×500 pixel window, surrounded by the window manager decorations for whatever window manager you have running on your system. Then, after five seconds, the window will disappear.

Functions called (Table 22.7):

Code:

```
/*Standard includes*/
#include <stdio.h>
#include <stdlib.h>
#include <X11/Xlib.h>
#include <X11/Xutil.h>
#include <X11/Xos.h>
#include <X11/Xatom.h>
#include <X11/keysym.h>
/*Variable and pointer declarations*/
Display *dis;
```

# TABLE 22.7 Xlib Display Functions

| Xlib Function Name | Description |
|---|---|
| XOpenDisplay | Returns a display structure that serves as a connection to the X server |
| XCreateSimpleWindow | Creates an unmapped InputOutput subwindow for a specified parent window |
| XMapWindow | Maps the window and all its subwindows |
| XFlush | Flushes the output buffer |
