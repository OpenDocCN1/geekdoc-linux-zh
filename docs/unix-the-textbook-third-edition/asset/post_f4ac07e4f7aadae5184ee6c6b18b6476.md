
```python
try:
    #Getting search pattern from user and assigning it to a list
    pattern = raw_input("Enter the file pattern to search for:\n")
    #defining a 'find' string and assigning results to a variable
    commandString = "find " + pattern
    commandOutput = commands.getoutput(commandString)
    findResults = string.split(commandOutput, "\n")
    #output find results, along with permissions
    print "Files:"
    print commandOutput
    print "****************************"
    for file in findResults:
        mode=stat.S_IMODE(os.lstat(file)[stat.ST_MODE])
        print "\nPermissions for file ", file, ":"
        for level in "USR", "GRP", "OTH":
            for perm in "R", "W", "X":
                if mode & getattr(stat,"S_I"+perm+level):
                    print level, " has ", perm, " permission"
                else:
                    print level, " does NOT have ", perm, " permission"
except:
    print "Error - check your input of file matching pattern"
```

In summary, we used rsync to backup a file and directories from the hard drive to a USB thumb drive, to a remote host on the local network, and in a rolling scheme to a USB thumb drive. We have also illustrated a simple UNIX file maintenance command useful for system administration. In Chapter 23 we will explore more robust strategies and examples of how to back up user files and system files, and carry out common system administration chores using shell commands and Python code.

## 16.4.3 Graphical User Interface with Python and Tkinter Widgets

Up until this point in the chapter, we have interacted with Python in a text-based manner, where we typed commands into the Python shell, or into a text editor, and executed Python to view the output results as text. In this section, we will build a “widget”-based (widget is short for window gadget) GUI with Python, where we still create the Python code as text, but see the resulting output of the Python script in the form of widget graphics.

To accomplish this, we assume the following:

- 1. That you are using a GUI environment to interact with your UNIX system, such as KDE or Gnome. In our base UNIX system, PC-BSD, we installed the default KDE desktop environment when we installed the system. Thus, we have a GUI capability in Python.
- 2. That you have Python 2.7.9 on your PC-BSD, as we showed in Section 16.2.
- 3. That you are using a BSD-family UNIX, such as our base system, PC-BSD.
- 4. If you are using a Solaris-family UNIX system, such as Oracle Solaris or OpenIndiana, you can use the graphical version of the IPS package manager, as mentioned in Section 16.2, to update your Python installation to Python 2.7.X. Additionally, the Tkinter graphics package installation is already done for you if you upgrade to Python 2.7.X in Solaris using the IPS package manager. When you upgrade to Python 2.7.X in Solaris, to launch version 2.7.X of Python, you need to type python2.7 on the command line.

### 16.4.3.1 Obtaining Tkinter and Basic Widget Construction

The standard widget GUI package that works with Python is called Tkinter. For you to add widget GUI components and functionality to Python, you must be able to import the Tkinter package. You can easily test to see if your default Python system has the Tkinter package available. On the Python command line, type:

```
>>> import Tkinter
```

If you get an error message that the module does not exist, or some similar error message, then you must install the Tkinter package from the FreeBSD ports repository. Use the kickoff application launcher at the bottom left of the PC-BSD window, and under “Applications> System”, launch an XTerm window. In that window, type the following command as superuser:

```
% pkg install py27-tkinter
```

The pkg package manager may update itself to its latest release, and then, by typing y to assent to the installation of packages, Tkinter is installed in the proper directories. You can then import Tkinter as a module in Python.

Basically, there are two parts to Tkinter widget GUI script construction. The first part is constructing your widgets, using a set of universal constructor tools and the Tkinter widget module set. The second part is building your application program from Python code, that accomplishes what you want to do, and then “hooking” it to the widget constructors of the first part.

Tkinter widgets can be constructed to display and be hooked up to your Python application code, either using OOP, where the widgets are object instances of master classes of Tkinter widgets, or they can be constructed using a functional programming approach. We choose the latter approach because it is easier for beginners, even though in the last examples we present you should be able to see that OOP is an essential, but not mandatory, part of Tkinter GUI programming.

The general form of using a Tkinter widget is as follows.

```
>>> widget = Widget.method (master, option=value,
option=value,...)
```
