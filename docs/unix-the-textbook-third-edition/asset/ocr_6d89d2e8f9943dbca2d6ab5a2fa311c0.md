has a more complex data structure and API than Xlib. Qt uses the object-oriented client programming paradigm with attendant data structures and classes, and is coded in C++.

Application code for Xlib or XCB is written in C or C++ and compiled using any of the available C/C++ compilers on the system.

When programming in C++ for Qt, that library has its own facilities to compile, link, and assemble a client application and place it in the context of a Qt project, as shown in Section 22.4.5, “Using the Qt Toolkit.”

# 22.4.2 Xlib versus XCB

The reason we include examples of Xlib and XCB client programs is that they are the two official C libraries for the X Window protocol. Xlib, the predecessor of XCB, was the original X client library, and was the only official X client library until the introduction of XCB.

The two libraries are based upon very different approaches: Xlib is a layer further from the X protocol that uses a traditional and programmer-friendly C API, whereas XCB is a very thin layer on top of the X protocol that does not have a transparent and friendly API.

As you can see from our presentation on both Xlib and XCB, the documentation that exists currently for XCB is far less friendly, complete, and descriptive. These two aspects of XCB, documentation and user-friendliness, are a function of its closer relationship with the complex data structure implementation of the X protocol itself.

In practice, the difference in organizing schemes is most evident in how the two libraries handle the fundamental asynchronous event-request model between server and client of the X protocol itself. Xlib attempts to implement the asynchronous X protocol behind a mixed synchronous and asynchronous API, whereas the XCB API is asynchronous.

For example, to lookup the attributes (e.g., size and position) of a window, you would write the following code using Xlib:

```
XWindowAttributes attrs;
XGetWindowAttributes(display, window, &attrs);
/* Execute some code */
```

The Xlib call to XGetWindowAttributes() in the client-side program sends a request to the X server and blocks until it receives a reply from the X server. This is a synchronous request-event sequence.

The following is the code for the same thing in XCB:

```
xcb_get_window_attributes_cookie_t cookie = xcb_get_window_attributes(connection, window);
/*Execute other code while waiting for the reply from the server*/
 xcb_get_window_attributes_reply_t* reply = xcb_get_window_attributes_reply(connection, cookie, NULLptr);
/*Execute some code based on the reply*/
```