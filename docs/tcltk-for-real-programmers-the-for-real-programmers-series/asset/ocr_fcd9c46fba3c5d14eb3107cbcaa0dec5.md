# 2.1 The tclsh and wish interpreters

If there are any arguments after the script name, those arguments will be ignored by the tclsh or wish interpreter and passed directly to the script for evaluation.

# 2.1.2 Starting tclsh or wish under Unix

Under Unix, you start tclsh as you would start any other program: type tclsh at a shell prompt. Be certain the directory containing the tclsh you want to invoke is in $PATH.

```
/usr/local/bin/tclsh ?scriptName? ?scriptArguments
or
wish ?options? ?scriptName? ?scriptArguments
```

When tclsh or wish interpreter starts, it loads several Tcl script files to define certain commands. The location for these files is defined when the interpreters are installed. If the interpreters are moved without being reinstalled, or the supply file directories become unreachable, you may get an error message resembling the following when you try to run tclsh:

```
application-specific initialization failed:
Can't find a usable init.tcl in the following directories:
/usr/local/lib/tcl18.0 /usr/local/lib/tcl18.0
/usr/tcl18.0/library /usr/local/library
This probably means that Tcl wasn't installed properly.
```

or when you try to run wish:

```
Application initialization failed:
Can't find a usable init.tcl in the following directories:
/usr/local/lib/tk8.0 /usr/local/lib/tk8.0 /usr/local/lib/tk8.0
/usr/local/lib/tk8.0/library /usr/local/library /usr/tk8.0/library
/usr/tk8.0/library
This probably means that Tk wasn't installed properly.
```

If this happens, you should reinstall Tcl/Tk, or restore the init.tcl other files to one of the directories listed in the default search paths. Alternatively, you can find the appropriate init.tcl and define the environment variable TCL_LIBRARY as that directory. The default location of init.tcl can be overridden by setting the environment variable.