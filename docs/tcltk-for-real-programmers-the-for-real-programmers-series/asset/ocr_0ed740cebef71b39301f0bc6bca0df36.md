# 12.3 An Example

3. There are some conventions that Microsoft VC++ demands for code that will be dynamically loaded. If your extension will need to compile only on Unix or Macintosh, you may delete this section and simplify the function prototypes.

4. The CmdReturn structure is not a part of the Tcl standard. I use it to allow functions that implement subcommands to return both a status and a Tcl_Obj to the function that implements the primary command. The status field may be assigned the value TCL_OK or TCL_ERROR. The object field may be NULL if the function has no return or a pointer to a Tcl Object.

If you find another convention more suited to your needs, feel free to use that instead.

5. The function prototypes for the functions in the source code files. All of the functions defined in the source code files should also be defined here.

# 12.3.2 demoInit.c

The demoInit.c file is one of the required files in an extension. At a minimum this file must define the Demo_Init function, as shown (and discussed) next:

Example 12.3.2-1

```
demoInit.c
#include "demoInt.h"

/* CVS Revision Tag */
#define DEMOINIT_REVISION $Revision: 1.2 $
/*
----------------------------------------------------------------------
* Demo_Init
*
* Called from demoAppInit() if this is a standalone
* shell, r when the package is loaded if compiled
* into a binary package.
*
```