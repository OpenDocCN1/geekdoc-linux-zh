This folder contains the source code for the `tmake` utility that translates platform-independent project description files into platform-dependent makefiles or Microsoft projects. Building `tmake` is just as easy as building Qt.

```
./Distribution/RedHat-6.1/static
./Distribution/RedHat-6.1/shared
```

These folders contain prebuilt copies of the Qt Free Edition source for RedHat Linux Version 6.1, with the egcs-1.1.2 compiler. This is (arguably) the most common Linux distribution, but it will still behave correctly on many other Linux distributions.

I provided both dedicated static-linkage and dedicated dynamic-linkage builds. Which method you choose to use depends greatly on your end-user environment.

```
./Book/Examples/chap2
./Book/Examples/chap3
./Book/Examples/chap4
./Book/Examples/chap5
./Book/Examples/chap7
./Book/Examples/chap8
```

As you may have guessed, these folders contain the examples from the book. Some of the examples have been altered to provide “demo” capabilities. If you wish to use them in an application, you will need to either rip out the main() function definitions or enclose them within a conditional compile.

```
./Binaries/Windows/examples
```

While a Pro license is required to build Qt for Windows platforms, it may help Windows users to see the examples that come with the Qt distribution execute in a Windows environment. For that reason, the executable forms of the Qt examples are provided in this folder.

```
./Extras
```

This folder contains some useful classes and HTML documentation that I've written over the years. You are encouraged to improve on these classes and to share those improvements—but remember to give credit where credit is due.

It is important to note that the SpinTime widget, a weekend kludge that works very well, contains chunks of code that are taken directly from the Qt QSpinBox widget, and are therefore the property of Trolltech and subject to their generous licensing. It is reproduced in SpinTime by their kind permission. I will eventually rewrite the widget to support QString, QDateTime, and internationalization of the display format—a task that would already be complete had I not been busy writing a book.