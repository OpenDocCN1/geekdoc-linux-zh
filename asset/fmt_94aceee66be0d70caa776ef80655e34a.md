
# PARAMETERS AND VARIABLES

Shell variables were introduced on page 312. This section adds to the previous coverage with a discussion of array variables, global versus local variables, special and positional parameters, and expansion of null and unset variables.

## ARRAY VARIABLES

The Bourne Shell supports one-dimensional array variables. The subscripts are integers with zero-based indexing (i.e., the first element of the array has the subscript `(0)`). The following format declares and assigns values to an array:

```
name=(element1 element2 ...)
```

The following example assigns four values to the array:

```bash
$ NAMES=(max helen sam zach)
```

You reference a single element of an array as follows:

```
$ echo ${NAMES[2]}
```

The subscripts [`*` and `@`] both extract the entire array but work differently when used within double quotation marks. An `@` produces an array that is a duplicate of the original array; `*` produces a single element of an (or a plain variable) that holds all the elements of the array separated by the first character in `IFS` (normally a space). In the following example, the array `A` is filled with `NAMES` using `*`, and `B` is filled using `@`. The `declare` builtin uses the `-a` option displays the values of the array (and reminds you that bash uses zero-based indexing):

```
$ declare -a ${NAMES[0]}
$ declare -b ${NAMES[0]}
declare - A='${NAMES[0]=max helen sam zach'
declare - B='${[0]=max" [1]=helen" [2]=sam" [3]=zach"
declare -a NAMES='${*}=max" [1]=helen" [2]=sam" [3]=zach"
```
