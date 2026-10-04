# Chapter 12. Writing a Tcl Extension

* in this function and no other function is called.
  */

```
if (returnStruct != NULL) {
    returnValue = returnStruct->object;
    result = returnStruct->status;
    free (returnStruct);
}
```

/* 12
  Set the return value and return the status
  */

```
if (returnValue != NULL) {
    Tcl_SetObjResult(interp, returnValue);
}
return result;
```

+   1. This array of strings will be passed to the Tcl_GetIndexFromObj function that will identify a valid subcommand from this list.

+   2. These #defines create a set of textual identifiers for the positions of the subcommands in the list. They will be used in a switch command in the main code to select which function to call to implement the subcommands.

+   3. The cmdDefinition structure is one that I prefer. It is not part of the official Tcl coding standards. It is strongly recommended that functions check their arguments and return a usage message if the arguments do not least match the expected count. This can be done in each function that implements a subcommand, or in the function that implements the main command. I prefer to use this to define the maximum and minimum number of arguments expected and the error message to return if the number of arguments received is not within that range.

+   4. There is a #define macro used to define debugprt in demoint.h. This will reference the demoDebugPrint global variable. This is not part of the official Tcl coding standards. I find it convenient to use printf for some levels of debugging.

+   5. This is the standard header for a C function in a Tcl extension, recommended in the Tcl/Tk Engineering Manual.