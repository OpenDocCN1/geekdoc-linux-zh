# 12.3 An Example

# tableStrings

The strings defined in tablePtr

flags

The flags argument allows the calling code to define what matches are acceptable. If this flag is TCL_EXACT, only exact matches will be returned, rather than allowing abbreviations.

indexPtr

A pointer to the integer that will receive the index of the matching field.

demoCmd.c file contains the C functions that are called when demo commands are evaluated in the Tcl script. In a larger package with several commands, this file would contain several entry points.

# Example 12.3.3-1

# demoCmd.c

```
#include "demoInt.h"

/* 1
* Define the sub commands
*
* These strings define the subcommands that the demo command
* supports.
*
* To add a new subcommand, add the new subcommand string,
* #define, and entry in cmdDefinition.
*
* Note: Order is important.
*
* These are the subcommands that will be recognized
*/
static char *subcommands[] = {
    "create", "set", "get", "debug", "destroy", NULL;
}

/* 2
* These #defines define the positions of the subcommands.
* You can use enum if you are certain your compiler will
* provide the same numbers as this.
*/
```