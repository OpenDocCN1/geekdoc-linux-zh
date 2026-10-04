
# Chapter 14. Programming Tools

## 14.3.2 Graphic Debuggers

There are several GUI-oriented debuggers available for Tcl, ranging from the commercial debugger from Scriptics to freeware offerings.

### 14.3.2.1 Tuba

- Language: Tcl/C++
- Primary Site: http://www.doitnow.com/~iliad/Tcl/tuba/
- Contact: iliad@doitnow.com
- Tcl Revision Supported: Tcl: 8.0-8.1 Tk: 8.0-8.1
- Supported Platforms: Unix, Windows NT, Windows 95

This package uses multiple windows to display the code being debugged; allow the user to display and modify variable contents; step into or through procedures; and set breakpoints by line, procedure, or when a variable is set. The GUI is very friendly and includes balloon popups to describe the tool buttons.

Tuba includes an extended update command and some parsing code to enable it to control the code being debugged. These functions are written in both C++ and Tcl. The Tcl code and the C++ libraries have the same functionality, but the compiled code runs much faster. If you cannot compile the C++ libraries, the Tcl libraries are acceptably fast.

The first image to follow shows the main window and file selection window. The second image shows the source code window with a variable monitor window displayed on top of it.

### 14.3.2.2 TdChoose/TdDebug

- Language: Tcl
- Primary Site: http://www.neosoft.com
- Contact: david.dougherty@amd.com

14.3 Debugging

![](img/fdcc2919568b5c9f5301d5a1e8d7_590_0.png) Tuba v2.1

![](img/fdcc2919568b5c9f5301d5a1e8d7_590_1.png) Hit breakpoint on /usr/src/Tcl/dummy/test.tcl

Chapter 14. Programming Tools

Tcl Revision Supported: Tcl: 7.3-8.0 Tk: 3.6-8.0
Supported Platforms: Unix

The TdDebug package (originally developed by Gregor Schmid) is unique in that it can be attached to an already running wish program. This is useful when you have a program that's running for several days and suddenly goes into a strange state and needs to be examined. With TdChoose you choose the wish interpreter you want to debug and then select the procedures you wish to observe. Tcl commands are added to your code to invoke the debug window once a selected procedure is entered. A search field makes it easy to select procedures in large programs.

While the debugger is controlling your application, you can step through the procedure, insert breakpoints, or continue execution with a user-specified delay. The debugger updates variables window and displays the result as each line is evaluated. You can also enter a line of Tcl code to evaluate in the program's current scope. This line of code can modify variables, change program flow, etc.

TdDebug supports an extensive configuration file that lets you define colors and highlighting various useful controls for the appearance and detail of the information in the debug window. Additional features are available if the wish interpreter contains Tix or BL extensions.

The following images show a portion of a debugging session for a GUI that calculates the mean value from a list of numbers.

Example 14.3.2-1 Script

```tcl
proc addList {lst} {
    set total 0
    foreach num $lst {
        set total [expr $total + $num]
    }
    return total
}
```

```tcl
proc mean {lst} {
  set sum [addList $lst]
  set count [length $lst]
  set mean [expr $sum / $count]
  return $mean
}
```

```tcl
set lst [list 2 4 6 8]
entry .list -textvar lst
label .mean -textvar mean
button .go -text Calculate -command {mean $lst}
pack .list
pack .mean
pack .go
```

The application debugged is displayed in the upper left corner. The upper right-hand corner shows the TChoose window which allows the user to select the application to debug and which procedures within that examination. The window labeled TDebug-Backtrace shows the current stack. The window labeled TDebug-Widget-Hierarchy shows the names and types of this application's widgets.

The bottom window shows the code currently evaluated and the values of the local variables. I typed the command in the Eval entry to initialize the total variable to a bogus value, as shown in the Variables scrollbox.

### 14.3.2.3 TclPro Debugger

| Language | Tcl |
|---|---|
| Primary Site | http://www.scriptics.com |
| Contact | sales@scriptics.com |
| Tcl Revision Supported | Tcl: 7.6-8.0 Tk: 4.2-8.0 |
| Supported Platforms | Unix, Windows NT, Windows 95 |

![](img/fdcc2919568b5c9f5301d5a1e8d7_593_0.png)

The TclPro Debugger is part of the TclPro development suite. TclPro Debugger can be used to debug local, embedded, and remote applications written in either straight Tcl or extended Tcl.

When a program is loaded into TclPro Debugger, it is checked for correctness. If TclPro Debugger finds a syntax error, it will display a window with a description of the error and mark the offending line in the main window.

14.3 Debugging

The main window of the TclPro Debugger displays the contents of the local variables, the stack, the code being evaluated, and the visible breakpoints. You can open other windows to display all breakpoints, display variables being watched, select procedures to display in the main window, or enter commands that can be evaluated at different procedure scopes in the stack.

TclPro Debug supports stepping into, over, or out of Tcl procedures; setting breakpoints on lines of Tcl code; setting variable breakpoints that stop execution when a variable is set; viewing variable data; and viewing the Tcl stack.

When the evaluation is halted at a breakpoint you can step up and down through the Tcl call stack to examine the program state. TclPro Debug also displays the "hidden" stack levels such as the uplevel that occurs when the script associated with a button is evaluated.

In order to use the debugger with remote or embedded applications, you must add a small amount of initialization code to your application. Once this is done, a remote application can be debugged just like a local application.

The following image shows TclPro Debug examining the application shown in Example 14.3.2-1. Line 4 is currently evaluated, and there is a breakpoint set at line 10. The Stack Frame display in the main window shows that this procedure was entered from a button press. The display in the Eval window shows the variable being set to 4 before the loop started.

Chapter 14. Programming Tools

![](img/fdcc2919568b5c9f5301d5a1e8d7_595_0.png)

## 14.4 GUI Generators

If you are developing a GUI-intensive application, you can spend a lot of time rearranging the widgets to get the appearance you want. Natively, you can use one of the GUI generator programs to create a GUI skeleton that you can populate with your application code.

Again, there are other GUI builders available. You should check the Neosoft archives or lang.tcl to see if other generators may suit your needs better than these.

### 14.4.1 SpecTcl

| Language | Tcl |
|---|---|
| Primary Site | http://sun.script.com/products/spec-tcl.html |
| Contact | Not officially supported |
| Tcl Revision Supported | Tcl: 7.6-8.1 Tk: 4.2-8.1 |
| Supported Platforms | Unix, Windows NT, Windows 95, Mac |

SpecTcl can generate the "skeleton" of a GUI program. It lets you position any of the standard Tcl widgets within a grid, test the appearance of the GUI, and save the GUI description and the Tcl (or Java) code.

Double clicking on a widget within SpecTcl will open a window that displays all of a widget's properties and allows you to modify them.
