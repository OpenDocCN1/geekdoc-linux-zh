ready to open a window). The second line only displays when you exit the program. Of course, if your program crashes or ceases operation in some other abrupt fashion, the second line never displays.

External processes or devices use the event queue to send information to your program. The queue is read-only, so if your program needs to talk to other programs or to devices it has to use some other method.

There are several different types of events. A number of them are of no real consequence to an application because the underlying GTK+ event handler does most of the work. For example, if a window becomes unobscured, an event arrives specifying that window must be redrawn completely or partially. But there normally is no need for the application to bother with it because GTK+ takes care of it. However, there are circumstances in which you may want to have more information about the incoming events. For example, if your application uses input from the mouse to draw lines on the screen, you need to know where the mouse is located and whether a button is being held down. This information is all included with the event and is passed to your callback functions.

# The Sequence of Dispatching Events

An event happens (such as a key being pressed on the keyboard) and your program reacts. There may be several programs running at the same time, so a process needs to decide which process is to receive information about the event and a mechanism needs to get it there. The following steps are a high-level overview of the process.

+   Step 1: The mouse pointer is moved around the display and a button is pressed. This causes a hardware interrupt.

+   Step 2: The software driver for the mouse fields the interrupt and packages the information in the standard form for the system. The information includes the x and y location of the mouse click and which button was pressed. The driver then passes the information on to the process that registered with it — in the case of X, it is the window manager.

+   Step 3: The window manager has the job of positioning all the windows on the display and determining the stacking order (which windows are obscured by other windows). Using this geographic information, the window manager determines which window just received the mouse click. With the keyboard, the process is a little different because there is no on-screen location information. There is one window that has the focus, and that window receives all keystrokes.