the file extension .cpp—for example, exercise1.cpp, which contains Qt client application program code.

Step 1: At the shell prompt, type qmake-qt4 -project.

Step 2: At the shell prompt, type qmake-qt4.

Step 3: At the shell prompt, type make.

Step 4. In the directory you will now have five files: exercise1.cpp, Makefile, exercise1.o, qtprogs1.pro, and qtprogs1.

Step 5: At the shell prompt, type ./qtprogs1.

Step 6: The graphics contained in the Qt program you entered into exercise1.cpp are now shown on the screen. Use the kill window button to close this Qt window.

# 22.4.5.2 Qt Examples

Here is the simplest Qt client application program you can enter. Notice how much shorter it is than the XCB or Xlib code shown in the preceding sections. Follow the instruction steps in Section 22.4.5.1 to create the program and execute it.

# Qt EXERCISE 22.1: SIMPLEST Qt PROGRAM

```
// helloWorld/main.cpp
#include <QApplication>
#include <QLabel>
int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    QLabel label("Hello World");
    label.show();
    return a.exec();
}
```

# Qt EXERCISE 22.2: SIMPLE Qt PROGRAM WITH A GUI