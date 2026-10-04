# Chapter 12. Writing a Tcl Extension

#  12.3.4 demoDemo.c

demoDemo.c file has the functions that implement the subcommands of the demo command. The naming convention is that the first demo indicates this is part of the demo package, and the second Demo indicates that this file implements the demo command. If there were a foo command in this demo package, it would be implemented in the file demoFoo.c.

Most of these functions will be called from demoCond.c. the Demo_InitHashTable function, which is called from Demo_Init. This function is included in this file to allow the hash table pointer (demo_hashtbl) to be a static global and keep all references to it within this file.

# 12.3.4.1 Demo_InitHashTable

This function simply initializes the Tcl hash table and defines the keys to be NULL-terminated strings.

Example: 12.3.4.1-1

```
Demo_InitHashTable
#include "demoInit.h"
static Tcl_HashTable *hashtblPtr;
extern int demoDebugPrint;
```

```
/*------------------------------------
* void Demo_InitHashTable () --
* Initialize a hash table.
* If your application does not need a hash table, this may be
ndeleted.
*
```

+   * Arguments
NONE

+   * Results
Initializes the hash table to accept STRING keys

+   * Side Effects:
None