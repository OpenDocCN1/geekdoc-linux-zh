# Chapter 12. Writing a Tcl Extension

This may not be a pointer to newValPtr if events triggered by accessing the newValPtr modify the contents of newValPtr. This can occur if you are using the trace command to observe a variable. See the discussion on using trace in Section 15.1 and read about the trace command in your online help to see how this can happen.

Tcl_ObjGetVar2

Returns a Tcl object containing a value identified by the string values in id1Ptr and id2Ptr.

Tcl_SetVar2

Creates or modifies a script variable. The value of the referenced variable will be set to newstring. This function returns a char * pointer to the new value.

This function is for use with versions of Tcl older than 8.0.

Tcl_GetVar2

Returns the string value for the variable or array reference identified by the string values in name1 and name2.

This function is for use with versions of Tcl older than 8.0.

Tcl_Interp *interp

A pointer to the Tcl interpreter.

Tcl_Obj *id1Ptr

An object that contains the name of a Tcl variable. This may be either a simple variable or an array name.

Tcl_Obj *id2Ptr

If this is not NULL, it contains the index of an array variable. If this is not NULL, then id1Ptr must contain the name of an array variable.

char *name1

A string that references either a simple Tcl string variable or the name of an associative array.

char *name2

If this is not NULL, it is the index of an array variable. If this is not NULL, then name1 must contain the name of an array variable.