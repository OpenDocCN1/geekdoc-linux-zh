# Chapter 12. Writing a Tcl Extension

# 12.3.3 demoCmd.c

The demoCmd.c file is where most of your extension code will exist. For small extensions this file will contain all the code that implements your package functionality.

The Demo_CmdFromObj function introduces a couple of new Tcl library functions.

The Tcl_GetIndexFromObj function searches a list of words for a target word. This function will return the index of the word that either matches the target word or a unique abbreviation of the target word. This function is used in this example to extract a subcommand from a list of valid subcommands.

**Syntax: int Tcl_GetIndexFromObj (interp, objPtr, tblPtr, flags, indexPtr)**

+   - Tcl_GetIndexFromObj sets indexPtr to the offset into tablePtr of the entry that matches the string representation of the data in objPtr. An item in tblPtr is defined as a match if it is either an exact match to a string or a unique abbreviation for a string in the table.

This function returns TCL_ERROR if no match can be found. If Tcl_GetIndexFromObj fails, it will set an error message in the interpreter's result object.

+   - interp: A pointer to the Tcl interpreter

+   - tablePtr: A pointer to a NULL-terminated list of strings to be searched for a match.

+   - msg: A string that will be included in an error message to explain what was being looked up if Tcl_GetIndexFromObj fails. The error message will resemble

```
bad msg "string": must be tableStrings
```

+   - msg: The string defined in the msg argument

+   - string: The string representation of the data in objPtr