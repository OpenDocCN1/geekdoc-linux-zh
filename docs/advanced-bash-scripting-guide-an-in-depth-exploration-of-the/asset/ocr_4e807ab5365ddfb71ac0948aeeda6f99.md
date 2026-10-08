# Advanced Bash-Scripting Guide

```
# Within double-quotes, the behavior of Glob-Pattern references
## depends on the setting of IFS (Input Field Separator).
## Within double-quotes, All-Elements-Of references behave the same.
```

```
# Specifying only name of a variable holding a string refers
## to all elements (characters) of a string.
```

```
# To specify an element (character) of a string,
## the Extended-Syntax reference notation (see below) MAY be used.
```

```
# Specifying only the name of a Bash array references
## the subscript zero element,
## NOT the FIRST DEFINED nor FIRST WITH CONTENTS element.
```

```
# Additional qualification is needed to reference other elements,
## which means that the reference MUST be written in Extended-Syntax.
## The general form is: ${name[subscript].
```

```
# The string forms may also be used: ${name[:subscript]}
## for Bash-Arrays when referencing the subscript zero element.
```

```
# Bash-Arrays are implemented internally as linked lists,
## not as a fixed area of storage as in some programming languages.
```

```
# Characteristics of Bash arrays (Bash-Arrays):
```

```
# If not otherwise specified, Bash-Arrays begin with
## subscript number zero. Literally: [0]
## This is called zero-based indexing.
```

```
# If not otherwise specified, Bash-Arrays are subscript packed
## (sequential subscripts without subscript gaps).
```

```
# Negative subscripts are not allowed.
```

```
# Elements of a Bash-Array need not all be of the same type.
```

```
# Elements of a Bash-Array may be undefined (null reference).
## That is, a Bash-Array may be "sparse sparse."
```

```
# Elements of a Bash-Array may be defined and empty (null contents).
```

```
# Elements of a Bash-Array may contain:
## A whole number as a 32-bit (or larger) integer
## A string
## A string formatted so that it appears to be a function name
## with optional arguments
```

```
# Defined elements of a Bash-Array may be undefined (unset).
## That is, a subscript packed Bash-Array may be changed
```

Appendix A. Contributed Scripts