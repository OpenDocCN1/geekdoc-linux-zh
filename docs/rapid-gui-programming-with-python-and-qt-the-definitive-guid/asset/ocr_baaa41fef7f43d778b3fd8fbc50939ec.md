including Tcl/Tk. Once Python has been installed, the installer may ask you to reboot—you should do so before going on to install PyQt.

![](bbox=[0.14, 0.15, 0.48, 0.35])

![](bbox=[0.51, 0.15, 0.88, 0.35])

# **Figure A.3 The Python and PyQt installers on Windows**

Now you can install PyQt4 itself. Start up the PyQt installer by double-clicking **PyQt–gpl-4.2-Py2.5-Qt4.2.3.ex**, or whichever version of PyQt you downloaded. The installer’s first screen is shown on the right in Figure A.3. If you installed Python in a nonstandard location you must enter the correct location in the Choose Install Location screen—PyQt is installed as a Python extension, so its libraries are placed inside the Python directories. (For this reason, if you ever want to uninstall Python, you should uninstall PyQt first, then Python.)

PyQt is the last tool that must be installed to have everything set up and working. To test things, click Start→All Programs→PyQt GPL v4.2→Examples and Demos. This launches a PyQt version of the standard Qt demo application. From inside this application you can run many of the demo applications that are supplied with PyQt. The source code to the demos, and to many other PyQt examples, are normally installed in `C:\Program Files\PyQt4\examples`.

If you downloaded the book’s examples, you might like to unzip pyqtbook.zip in `c:` to get a `c:\pyqt` directory with all the book’s examples, along with model answers to the exercises, categorized by chapter. In the `c:\pyqt` directory itself you will find `mkpyqt.py` and `makepyqt.py`; these utilities are explained on page 207. If you want to try out any of the examples before reading the book, make sure that you run `makepyqt.py` first. (When you run `makepyqt.py`, set its path to `c:\pyqt`, check its Recurse checkbox, and then click the Build button. Now all the examples will be ready to run.)

That completes the installation for Windows, and is sufficient for PyQt GUI programming. But if you also want to write some console applications, or to sometimes run PyQt applications in a console (which can be useful for debugging), a few more steps will make this much more convenient.

Click Start→All Programs→Accessories→Windows Explorer. Once Windows Explorer is running, navigate to My Computer\Local Disk (C:)\Documents and Settings, and