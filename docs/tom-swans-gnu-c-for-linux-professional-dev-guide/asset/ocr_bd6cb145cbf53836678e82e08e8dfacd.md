# MAIN APPLICATION

A V program’s engine is its main application object. This object initializes the program using a class constructor and starts the program’s ball rolling. The application class destructor performs any clean-up duties such as debugging the client from the X server. Every V application must have one and only one main application object.

To create the application object, derive an application class from VApp and fill in a few member functions. Listing 29.1 shows the generated main application class declaration (with myapp.cpp as the author for reformatting the code and removing some extraneous comments to save space).

```
```cpp
#include <v/vapp.h>
#include <v/vawinfo.h>

class myApp : public VApp {
    friend int AppMain(int, char**); // allow AppMain access
public:
    myApp(char* name, int sdi = 0, int h = 0, int w = 0);
    virtual ~myApp();
    // Routines derived from VApp that are normally overridden
    virtual VWindow* NewAppWin(VWindow* win, char* name,
        int w, int h, VAppWinInfo* winInfo);
    virtual void Exit(void);
    virtual int CloseAppWin(VWindow*);
    virtual void AppCommand(VWindow* win,
        int itemVal, int itemVal, CmdType type);
    virtual void Key(VWindow* v, VKey, unsigned int);
protected:
private:
    myCmdWindow* myCmdWin; // Pointer to first window instance
};
```
```

The VApp class is declared in V3’s vapp.h header file. Include that header and also vawinfo.h in your program’s main application file. The second header declares a class, vAppWinInfo, which apparently has little practical value but is included for backward compatibility with earlier V releases (see the online documentation for more about this class).

Derive your application class from VApp as shown in the listing. You can name your class as you like, but for clarity it should end with App. The first item in the derived class is a friend function declaration for AppMain(), giving that function access to myApp’s private and protected declarations. AppMain() is the equivalent of a C or C++ program’s main() function. V applications are totally object-oriented, and they use objects to construct and destroy the application. A V application does not have a main() function.

The other declarations in the myApp class override various member functions from the VApp base class. Depending on your needs, you might add or subtract from the generated functions—but these are typically needed in most applications. You can add other declarations to the class’s protected section, which is empty by default. A single private data member defines a pointer to an object of the myCmdWindow class discussed in the next section.