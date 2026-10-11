name=(element1 element2 ...)

The following example assigns four values to the array NAMES:

```
$ NAMES=(max helen sam zach)
```

You reference a single element of an array as follows:

```
$ echo ${NAMES[2]}
sam
```

The subscripts [*] and [@] both extract the entire array but work differently when used within double quotation marks. An @ produces an array that is a duplicate of the original array; an * produces a single element of an array (or a plain variable) that holds all the elements of the array separated by the first character in IFS (normally a SPACE). In the following example, the array A is filled with the elements of the NAMES variable using an *, and B is filled using an @. The declare builtin with the -a option displays the values of the arrays (and reminds you that bash uses zero-based indexing for arrays):

```
$ A=("${NAMES[*]}")
$ B=("${NAMES[@]}")
```

```
$ declare -a
declare -a A=("max helen sam zach")
declare -a B=([0]="max" [1]="helen" [2]="sam" [3]="zach")
...
declare -a NAMES=([0]="max" [1]="helen" [2]="sam" [3]="zach")
```

From the output of declare, you can see that NAMES and B have multiple elements. In contrast, A, which was assigned its value with an * within double quotation marks, has only one element: A has all its elements enclosed between double quotation marks.

In the next example, echo attempts to display element 1 of array A. Nothing is displayed because A has only one element and that element has an index of 0. Element 0 of array A holds all four names. Element 1 of B holds the second item in the array and element 0 holds the first item.

```
$ echo ${A[1]}

$ echo ${A[0]}
max helen sam zach
$ echo ${B[1]}
helen
$ echo ${B[0]}
max
```

You can apply the ${#name[*]} operator to array variables, returning the number of elements in the array:

```
$ echo ${#NAMES[*]}
4
```