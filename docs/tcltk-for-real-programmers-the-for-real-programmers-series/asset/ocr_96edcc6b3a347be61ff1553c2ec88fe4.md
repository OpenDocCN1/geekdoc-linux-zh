# 7.2 Packages

If the procedure is not defined in any known package, then the Tcl interpreter reports an error. If the command can be acquired by loading a package, the interpreter does so and evaluates the command line that caused the error again (presumably successfully).

The Tcl interpreter will search the index files in the directories listed in the global variable `auto_path`. The `auto_path` variable is defined in the `init.tcl` script, which is loaded when a Tcl or Tk interpreter is started.

This section will discuss how to generate the index files and how to add your package directories to the list of index files to be searched.

Note that when you create an index for a package that has procedures defined within a namespace, only the procedure names listed in a namespace export command will be indexed.

# 7.2.2 Internal Details: The Files and Variables Used with Packages

These files and global variables are used to find and load a package.

`auto_path` global variable `auto_path` variable contains a list of the directories that should be searched for package index files.

The `auto_path` variable is defined in the `init.tcl` script, which is loaded when a `tclsh` interpreter is started.

On Unix systems, `init.tcl` will probably be found in `/usr/local/lib/tcl18.0` or some variant, depending on your installation and the revision number of your `tclsh`. On Windows systems, `init.tcl` is stored in `\Program Files\Tcl\lib\tcl18.0`, or some variant depending again on your version of Tcl and the base directory in which you installed the Tcl interpreter.