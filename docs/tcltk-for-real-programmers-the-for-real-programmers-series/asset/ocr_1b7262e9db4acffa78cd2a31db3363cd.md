# Chapter 12. Writing a Tcl Extension

```
return(returnStructPtr);
)
```

+   1. This code implements the equivalent of set arrayName (Index) Value.
2. This section of code implements the equivalent of
 arrayName(alpha) NewValue.
The value assigned to returnObjPtr is a pointer to valueObjPtr,
because there is no extra processing attached to the valueObjPtr variable.
3. Note that you should use the Tcl_DecrRefCount function to free Tcl
objects. Do not use the free function.
4. The valueObjPtr is also created in this function. A pointer to this object
will be returned by the Tcl_ObjSetVar2 call, but the reference count for
this object is not incremented.

Since this object is being returned as the returnObjPtr, the reference
count should not be decremented. If a pointer to this object is passed to
Tcl_DecrRefCount, the object will be destroyed, and returnObjPtr will
point to a nonexistent object. When the Tcl interpreter tries to process
then nonexistent object, it will not do anything pleasant.

# 12.4 Complex Data

If you need to handle complex data (such as a structure) in your extension,
here are some options.

+   1. You can define the structure in your Tcl script as a list of values and pass
 to extension code to parse into a structure.
2. You can use an associative array in the Tcl script, where each index into
the associative array is a field in the structure.
3. You can create a function that will accept the values for a structure in
list or array format, parse them into a structure, place that structure in a
hash table, and return a key to the Tcl script for future use.

The following code snippet shows how a Tcl associative array can be used
to pass a structure into a C code extension. The code expects to be
with the name of an array that has the appropriate indices set. The indices
of the array must have the same names as the fields of the structure.