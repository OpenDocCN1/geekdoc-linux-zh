# The Mechanics of Using the Tcl and Tk Interpreters

The first step in learning a new computer language is learning to run the interpreter/compiler and create simple executable programs. This chapter will describe:

+   - Mechanics of starting the interpreters.
- Starting tclsh and wish scripts in the interactive mode.
- Exiting the interpreter.
- Running tclsh and wish scripts from files.

# 2.1 The tclsh and wish Interpreters

The Tcl/Tk package is distributed with two script interpreters, tclsh and wish. Tclsh is a text-oriented interpreter that includes the core commands. It's useful for applications that don't require a GUI. Wish is the windowing shell; it includes the core Tcl interpreter with all the commands that tclsh supports and the Tk graphics extensions.