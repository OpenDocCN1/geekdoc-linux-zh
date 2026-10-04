# 12.3 An Example

demo get Retrieves the value of an entry from the hash table and returns the string saved with that key.

key The key for the entry to return.

**Syntax:** demo destroy key

demo destroy Deletes an entry in the hash table.

key The key that identifies which entry to delete.

**Syntax:** demo set arrayName index

demo set An example of how to set the values in an associative array. It sets the index to the requested value and sets the index alpha of the array to the value NewValue. The index alpha and value NewValue are hardcoded in the procedure Demo_SetCmd.

This subcommand executes the C code equivalent of

```
set arrayName(index) Value
set arrayName(alpha) "NewValue"
```

The command will return the string "NewValue".

arrayName The name of a Tcl array. It need not exist before calling this subcommand.

index An index into the array. This index will have Value assigned to it.

Value The value to assign to `arrayName(index)`.

The demo extension is arranged in the style of a large package with many commands, to show how the functionality can be split across files and functions. It consists of these files:

demoInt.h This file has the definitions for the structures used by this extension and the function prototypes of the functions that are defined in demoInit.c, demoCmd.c, and demoDemo.c.