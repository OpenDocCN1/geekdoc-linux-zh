```
1 #include <QtGui>
2
3
4 int main (int argc, char *args)
5 {
6 QApplication app (argv, args);
7
8 QTextEdit *textEdit= new QTextEdit;
9 QPushButtom *quitButtom= new QPushButton ("&Quit");
10
11 QObject::connect (quitButtom, SIGNAL(clicked() ), qApp, SLOT(quit()));
12
13 QVBoxLayout *layout= new QVBoxLayout;
14 layout->addWidget (textEdit);
15 layout->addWidget (quitButtom);
16
17 QWidget window;
18 window.setLayout (layout);
19
20 window.show();
21
22 return app.exec();
23
```

# **Listing 11.1**

Text edit program.

Make a subfolder under your home directory, and create the program shown in Listing 11.1. To build the program, run the following commands:

```
qmake-project
qmake
make
```

The first command creates a *project* file with the extension .pro. This contains some elementary information about the project. The second command creates a rather elaborate makefile, and the last command builds the target.

# **QT Designer**

Yes, you can build elaborate GUIs by manually programming as we just did, but there is a better way. *QT* has a graphical design tool called *Qt Designer* that allows you to design in a what-you-see-is-what-you-get environment, and generates the code for you.

There are a couple of ways to start Qt Designer. In a command shell, enter designer -qt4. In CentOS 7 it is also available from the *Application Launcher* under Development > Qt4.