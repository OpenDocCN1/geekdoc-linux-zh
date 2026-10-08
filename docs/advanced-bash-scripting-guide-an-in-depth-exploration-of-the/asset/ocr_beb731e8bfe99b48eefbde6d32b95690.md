# Advanced Bash-Scripting Guide

Arithmetic operators

+   - combination operators, C-style

+= =* = /= %==

> In certain contexts, += can also function as a string concatenation operator.

Arrays

+   - Associative arrays

+   more efficient than conventional arrays
- Bracket notation
- Concatenating, example script
- Copying
- Declaring

+   declare -a array_name
- Embedded arrays
- Empty arrays, empty elements, example script
- Indirect references
- Initialization

```
array=( element1 element2 ... elementN)
```

Example script

+   Using command substitution
- Loading a file into an array
- Multidimensional, simulating
- Nesting and embedding
- Notation and usage
- Number of elements in

```
${#array_name[@]}
```

+   ${#array_name[*]}
- Operations
- Passing an array to a function
- As return value from a function
- Special properties, example script
- String operations, example script
- unset deletes array elements

Arrow keys, detecting

ASCII

+   - Definition

Appendix T. ASCII Table