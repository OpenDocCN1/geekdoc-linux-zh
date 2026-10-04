
# Chapter 12. Writing a Tcl Extension

Whether you are building a new tcl or a loadable binary package, and whether you are linking to an existing library or are writing your own functions, the steps to follow are the same. This chapter will describe the components of an extension, step through creating a Tcl extension, discuss how to move data between the Tcl interpreter and your C language functions, and discuss how to handle complex data such as structures.

In Tcl 8.0 a major modification was introduced to the Tcl internals. Prior to this (Tcl 7.3, 7.4, 7.5, and 7.6), all data was stored internally as a string. When a script needed to perform a math operation, the data was converted from string to native format (integer, long, float, double, etc.), the operation was performed, and then the native data was converted back to a string to be returned to the script. This procedure caused scripts to run rather slowly.

With Tcl revision 8.0 and later, the data is stored internally in a Tcl_Obj structure. The Tcl_Obj structure contains a string representation of the data and a native representation of the data. The two representations are kept in sync in a lazy manner; the native and string representations are calculated when needed and retained as long as they are valid.

This change to the Tcl interpreter helped speed up the Tcl interpreter, but it causes some problems for extension writers. Most of the Tcl library functions that interface with data now come in two forms, one to deal with old-style string data and one to deal with new-style Tcl_Obj data.

If you are writing a new extension, you can use all of the new Tcl_Obj-oriented commands (which have the word obj in their names). If you need to link with an earlier version of Tcl (for instance, if you need to use an extension that exists only for Tcl 7.5), you will need to use the older version of the commands.

This chapter will cover both sets of commands. If you don't need to be able to link with an older version of Tcl, it is recommended that you use the Tcl_Obj objects for your data and the Tcl_Obj API to interface with the interpreter.

## 12.1 Overview

This section will provide an overview of how to construct an extension, first from the functional viewpoint of what functionality is required in an extension and how the parts work together and then from the structural viewpoint of how the pieces should be assembled.

### 12.1.1 Functional Overview of an Extension

An extension must perform these actions:

- Initialize any persistent data structures.
- Register new commands in the Tcl interpreter.
- Accept data from the Tcl interpreter.
- Process the new commands.
- Return results to the calling scripts.
- Return status to the calling scripts.

Your extension must include an initialization function that will be called by the Tcl interpreter when the extension is loaded into the interpreter. The code that performs the initialization will depend on your application.

The interface between the Tcl library and an extension is provided by several functions. On Windows systems these are documented under the **Tcl Library Procedures** entry in the *Tcl Help* menu. On Unix systems, they are documented in files named Tcl_*.3 in the doc directory. On the Macintosh these functions are documented under the **HTML DOCS** folder. Read those entries for more details on these commands.

### 12.1.2 Data Types

The interface to the Tcl library includes several data types that are specific to Tcl. The ones we'll be dealing with:

- Tcl_Interp * A pointer to a Tcl interpreter state structure.
- Tcl_ObjCmdProc * a pointer to a function that will accept Tcl objects as arguments.
- Tcl_CmdProc * a pointer to a function that will accept strings as arguments.
- ClientData a one-word value that is passed to functions but is never used by the Tcl interpreter. This allows functions to use data that is specific to the application, not the interpreter. For instance, this argument could be used to pass a pointer to a database record, or a window object, or a C++ this pointer.

### 12.1.3 Registering New Commands with the Interpreter

You register a new command with the Tcl interpreter by calling a function that will insert the name of the new command into the Tcl hash table and associate that name with a pointer to a function that will implement the command.

There are two functions that can be invoked to register a new command with the Tcl interpreter. One will register the new command as a function that can use Tcl objects, and the other will register the new command as a function that requires string arguments. Extensions that are to be linked with versions of Tcl more recent than 8.0 should create Tcl object-based functions rather than string-based functions.

```
Syntax: int Tcl_CreateObjCommand (interp, cmdName, func, clientData, deleteFunc)
Syntax: int Tcl_CreateCommand (interp, cmdName, func, clientData, deleteFunc)
```

Tcl_CreateObjCommand these functions register a new command with the Tcl interpreter. These actions are performed within the Tcl interpreter:

- Register cmdName with the Tcl interpreter.
- Define clientData data for the command.
- Define the function to call when the command is evaluated.
- Define the command to call when the command is destroyed.

Tcl_CreateCommand

This is the pre-8.0 version of this command. It will still work with 8.0 and newer but uses Tcl_ObjCommand.

Tcl_Interp

This is a pointer to the Tcl interpreter. It is required by all commands that need to interact with the interpreter state.

char *cmdName

The name of the new command, as a NULL-terminated string.

Tcl_ObjCmdProc *func

The function to call when cmdName is encountered in script.

ClientData

A value that will be passed to func which is on most machines the size of a pointer. You can allocate memory and use this pointer to pass an arbitrarily large data structure to func.

Tcl_CmdProc *deleteFunc

A pointer to a function to call when the command is deleted. If the command has some persistent data associated with it, this function should free that memory. If you have no special processing, set this pointer to NULL, and the Tcl interpreter will not register a deletion procedure.

These commands will return TCL_OK to indicate success or TCL_ERROR to indicate a failure. These are defined in the file tcl.h, which should be included in your source.

### 12.1.4 Transferring Data from a Tcl Script to a Language Extension

When a command is evaluated the interpreter needs to pass data from the script to the function. The Tcl interpreter handles this with a technique similar to that used by the C language for receiving command line parameters. The function that implements the C command receives an integer argument count and an array of pointers to the Tcl script arguments.

For example, if you register a command foo with the interpreter as Tcl_CreateObjCommand(interp, "foo", fooCmd, NULL, NULL); and later write a script command foo one two then fooCmd will be passed an argument count of 4 and an argument list that contains one, 1, two, and 2.

The prototype for the C function that implements the Tcl command will take one of these two forms:
Syntax: int func(clientData, interp, objc, objv)
Syntax: int func(clientData, interp, argc, argv)
