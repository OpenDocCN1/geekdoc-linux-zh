# 2.3 Evaluating Tcl Script Files

5. You can write double Tcl programs as .bat files and evaluate them as filename.bat with a wrapper around the Tcl code:

```
::catch (};#\
@echo off
::catch (};#\
"@C:\tcl\bin\tclsh.exe" %0 %1
::catch (};#\
@goto eof
#your code here
#\
:eof
```

This is similar to the startup described for the Unix Tcl files.
The lines with leading double colons are viewed as labels by the bat file interpreter, while the Tcl interpreter evaluates them as commands in the global namespace.

These lines end with a comment followed by a backslash. The backslash is ignored by the bat file interpreter, which then executes the next line.
The Tcl interpreter treats the next line as a continuation of the previous comment and ignores it.

The catch command is discussed in Chapter 5, and namespaces are discussed in Chapter 6.

If you prefer to run your scripts by single word, i.e., filename.bat, you can change the line:
"@C:\tcl\bin\tclsh.exe" %0 %1 %2
to
"@C:\tcl\bin\tclsh.exe" %0.bat %1 %2

# 2.5 Evaluating a Tcl Script on the Mac

The concept of the executable script file doesn't really exist on the Mac.

If you wish to evaluate a previously written script on the Mac, you can select the Source entry from the File menu, and then select the file to execute.

Alternatively, you can type the command to source the script file at the % prompt. In this case, you must use the complete path:

```
source :demos:widget
```