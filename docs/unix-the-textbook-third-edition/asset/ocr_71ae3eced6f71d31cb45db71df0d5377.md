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