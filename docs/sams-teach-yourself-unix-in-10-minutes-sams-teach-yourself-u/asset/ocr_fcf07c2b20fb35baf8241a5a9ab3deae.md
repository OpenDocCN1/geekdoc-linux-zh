There are many other window managers, and a variety will most likely be available to you for use on your machine. After you've investigated your options, you can start building a custom environment that feels and behaves exactly as you want it to.

Remember, it is the window manager that provides user-interface features such as title bars. If you find yourself facing a screen which looks like Figure 3.2 (windows missing title bars, no scroll bars, no icons) it is because there is no window manager running; it either hasn't started for some reason, or it has crashed. You can try starting a window manager by typing twm—if there is a terminal window open that is accepting keyboard input (directing keyboard input to a particular window is also a window manager function). If not, you'll need to exit the X Windows environment and modify your startup files to start the window manager of your choice immediately after starting the X server.

![](bbox=[0.12, 0.58, 0.9, 0.92])

Figure 3.2 This X Windows session has lost its window manager.