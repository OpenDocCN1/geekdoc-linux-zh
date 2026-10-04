# Using Lists and Arrays

This chapter will demonstrate how lists and arrays can be used to group data into constructs similar to structures, linked lists, and trees. The first examples will show how lists can be used to group data in ordered and unordered formats. The next section will discuss using associative arrays instead of structures, and the final set of examples will show how associative arrays and naming conventions can be used to create a tree-structured container object.

Tcl has been accused of being unsuited for serious programming tasks because of the simplicity of its data types. Whereas C++ has integers, floats, pointers, structs, and classes, Tcl has just strings, lists, and associative arrays. These simple constructs are usually sufficient. This chapter will demonstrate some techniques for using Tcl data constructs in place of the more traditional structs, linked lists, etc.

For some applications, such as dealing with an interface to a relational database management system (RDBMS), the Tcl data constructs are more suited to the interface than a C structure. Tcl handles an empty return from a database query more intuitively than some other languages.