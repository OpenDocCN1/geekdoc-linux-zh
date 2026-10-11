# ### Table A.1  Perl Functions (continued)

| Function | Description |
| :------- | :---------- |
| `unlink` | `unlink(LIST)`\n`unlink LIST`\n`unlink`\nRemoves a LIST of files. Returns the number of files deleted. Without an argument, unlinks the value stored in $\_. See unlink(2). |
| `unpack` | `unpack(TEMPLATE, EXPR)`\nUnpacks a string representing a structure and expands it to an array value, returning the array value, using TEMPLATE to get the order and type of values. Reverse of pack. |
| `unshift` | `unshift(LIST)`\n`unshift`\nPrepends LIST to the beginning of an array. Returns the number of elements in the new array. |
| `untie` | `untie VARIABLE`\nBreaks the binding (unties) between a variable and the package it is tied to. Opposite of tie. |
| `use` | `use MODULE VERSION LIST`\n`use MODULE LIST`\n`use MODULE`\n`use MODULE()`\n`use pragma`\nA compiler directive that imports subroutines and variables from MODULE into the current package. VERSION is the current version number of Perl. LIST consists of specific names of the variables and subroutines the current package will import. Use empty parameters if you don't want to import anything into your namespace. The -m and -M flags can be used at the command line instead of use. Pragmas are a special kind of module that can affect the behavior for a block of statements at compile time. Three common pragmas are *integer*, *subs*, and *strict*. |
| `utime` | `utime(LIST)`\n`utime LIST`\nChanges the access and modification times on a list of files. The first two elements of LIST are the numerical access and modification times. |
| `values` | `values(%ASSOC_ARRAY)`\n`values ASSOC_ARRAY`\nReturns an array consisting of all the values in an associative array, ASSOC_ARRAY, in random order. |