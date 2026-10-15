
the file extension .cpp—for example, exercise1.cpp, which contains Qt client application program code.

Step 1: At the shell prompt, type qmake-qt4 -project.

Step 2: At the shell prompt, type qmake-qt4.

Step 3: At the shell prompt, type make.

Step 4: In the directory you will now have five files: exercise1.cpp, Makefile, exercise1.o, qtprogs1.pro, and qtprogs1.

Step 5: At the shell prompt, type ./qtprogs1.

Step 6: The graphics contained in the Qt program you entered into exercise1.cpp are now shown on the screen. Use the kill window button to close this Qt window.

## 22.4.5.2 Qt Examples

Here is the simplest Qt client application program you can enter. Notice how much shorter it is than the XCB or Xlib code shown in the preceding sections. Follow the instruction steps in Section 22.4.5.1 to create the program and execute it.

## Qt EXERCISE 22.1: SIMPLEST Qt PROGRAM

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

## Qt EXERCISE 22.2: SIMPLE Qt PROGRAM WITH A GUI

```
4       int main(int argv, char **args)
5       {
6           QApplication app(argv, args);
7
8       QTextEdit textEdit;
9       textEdit.show();
10
11      return app.exec();
12      }
```

Dialog of explanation and description:

Lines 1 and 2 include the header files for QApplication and QTextEdit, which are the two classes that Qt uses. Qt is an object-oriented programming language that uses C++ class and object descriptions and functionality. All Qt classes have a header file named after them.

Line 4 declares the variables and opens the program.

Line 6 creates a QApplication object. This object manages application-wide resources and is necessary to run any Qt program that has a GUI. It needs argv and args because Qt accepts a few command line arguments for this object.

Line 8 creates a QTextEdit object. A text edit is a visual element in the GUI. In Qt, we call such elements widgets, short for window gadgets. Examples of other Qt widgets are scroll bars, labels, spin boxes, sliders, and radio buttons. A widget can also be a container for other widgets, a dialog area, or a main application window.

Line 9 shows the text edit on the screen in its own window frame. Since widgets also function as containers (for instance QMainWindow, which has toolbars, menus, a status bar, and a few other widgets), it is possible to show a single widget in its own window. Widgets are not visible by default; the function show() makes the widget visible.

Line 11 makes the QApplication object enter its event loop, similar to XCB and Xlib client application programs. When a Qt client application is running, events are generated and sent to the widgets of the application. Examples of events, as seen in XCB and Xlib, are mouse button presses, mouse cursor movements, and key strokes pressed on the keyboard. When you type text in the text edit widget, it receives key press events and responds by drawing the text that was typed.

## Qt EXERCISE 22.3: ADDING A QUIT BUTTON

In a real application, you would usually create more than one widget to allow a rich and varied dialog between client application data-generating code and Qt code. We will now show a simple example of a QPushButton beneath the text edit window created in Qt

Exercise 22.2. The button will exit the QTextEdit application when pushed (i.e., clicked on with the mouse). Again, disregard the line numbers shown, since they are only used to reference the code in the dialog that follows the code.
Here is the code.

```
1   #include <QtGui>
2
3   int main(int argv, char **args)
4   {
5       QApplication app(argv, args);
6
7       QTextEdit *textEdit = new QTextEdit;
8       QPushButton *quitButton = new QPushButton("&Quit");
9
10      QObject::connect(quitButton, SIGNAL(clicked()), qApp,
11                      SLOT(quit()));
12
13      QVBoxLayout *layout = new QVBoxLayout;
14      layout->addWidget(textEdit);
15      layout->addWidget(quitButton);
16
17      QWidget window;
18      window.setLayout(layout);
19
20      window.show();
21
22      return app.exec();
23  }
```

Dialog of explanation and description:

Line 1 includes QtGui, which contains all of Qt’s GUI classes.

Lines 7 and 8 create two pointer objects to be used to reference the classes of objects below.

The next line illustrates probably the most important Qt call.

Line 10 uses Qt’s signals and slots mechanism to make the application exit when the Quit button is pushed. A slot is a function that can be invoked at run time using its name (as a literal string). A signal is a function that when called will invoke slots registered with it; we call that to connect the slot to the signal and to emit the signal. So, quit() is a slot of QApplication that exits the application; clicked() is a signal that QPushButton emits when it is pushed.

As a programming reminder for C++, :: is called the (binary) scope resolution operator. By using the scope resolution operator, you can address member functions outside of
