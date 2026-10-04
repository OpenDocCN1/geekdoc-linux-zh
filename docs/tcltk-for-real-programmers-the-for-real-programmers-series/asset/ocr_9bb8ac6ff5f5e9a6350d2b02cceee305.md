# Procedure Techniques

One key to writing modular code is dividing large programs into smaller subroutines. Tcl supports the common programming concept of subroutines—procedures that accept a given number of arguments and return one or more values. Tcl also supports procedures with variable numbers of arguments and procedures with arguments that have default values. The Tcl interpreter also allows scripts to rename procedures or create new procedures while the script is running.

This chapter will discuss:

+   - Defining the arguments to procedures.
- Renaming and deleting procedures.
- Examining a procedure's body and arguments.
- Performing Tcl variable and command substitutions upon a string.
- Constructing and evaluating command lines within a script.
- Turning a set of procedures and data into an object.

The last example in this chapter will show how to extend the Tree example from Chapter 5 into a tree object.