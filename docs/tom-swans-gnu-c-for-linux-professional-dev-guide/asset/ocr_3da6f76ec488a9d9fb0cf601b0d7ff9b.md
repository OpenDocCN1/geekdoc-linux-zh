# LISTING 30.2 VWELCOME.CPP

```
#include "cmdwin.h"    // Include command window header
#include "app.h"       // Include application module header

// Construct the application object
static TWelcomeApp WelcomeApp(APPNAME);

// Main function
int AppMain(int argc, char* argv[])
{
    theApp->NewAppWin(0, TITLE, 325, 50);
    return 0;
}
```

The application object is a global, static variable of a class derived from vApp. In this case, I name the application class TWelcomeApp and the global object WelcomeApp. APPNAME is a string constant that represents the application name. TITLE is the window title string.

Function AppMain() resembles the main() function in a conventional program. It has argc and argv parameters for using any command-line options, although the sample program ignores these variables. Inside AppMain(), the first statement calls the NewAppWin() member function for an object addressed by theApp. This is a global V pointer that addresses the main application object— in this case, WelcomeApp. The four arguments passed to NewAppWin() are as follows:

+   - 0 This is a null window* pointer value, but it could address an existing window (perhaps of the derived class vCmdWindow) if for some reason you want to create that object before initializing the application.
+   - TITLE This is a standard C-style, null-terminated string that represents the window title. Because V is based on widgets (at least in UNIX and Linux), you can count on the window title appearing atop its frame, unlike in pure Xlib programming, which gives no similar guarantee.
+   - 325 This is a suggested width in pixels for the window frame.
+   - 50 This is a suggested height in pixels for the window frame.

There are two main reasons for using theApp pointer instead of the object directly. First, many other modules need to refer to this critical object, and second, in a larger program, you might define the application object in a separate module perhaps to hide it from view. In any case, you can always use theApp to address the main application object.

# Note

> Because of the way the X server, client applications, and the window manager work, you can't count on AppMain() returning. However, you can count on the main application object's class destructor being called before control returns to the process that started your client program. This means that your main application object always gets one last opportunity to perform critical tasks just before a program ends—saving a file, for example.