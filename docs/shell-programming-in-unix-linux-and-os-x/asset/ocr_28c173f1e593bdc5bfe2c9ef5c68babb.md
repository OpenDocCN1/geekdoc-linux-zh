enclosed inside a pair of curly braces, and the whole element is preceded by a dollar sign.
Sounds complicated? It's not:

```
$ echo ${array[0]}
hello
$ echo ${array[1]}
some text
$ echo ${array[2]}
/users/steve/memos
$ echo $array
hello
$
```

As you can see from the preceding example, if no subscript is specified, element zero is used.
If you forget the curly braces when performing the substitution, nothing breaks, it just produces a result that's not what you expect:

```
$ echo ${array[1]}
hello
$
```

The value of array is substituted (hello—the value of array[0]) and then echoed along [1]. (Note that the shell does filename substitution after variable substitution, the shell would attempt to match the pattern hello[1] against the files in your current directory).

The construct [* can be used as a subscript to produce all the elements of an array on the command line, with each element separated by a space.

```
$ echo ${array[*]}
hello some text /users/steve/memos
$
```

The construct ${#array[*]} is used to find out the number of elements in array.

```
$ echo ${#array[*]}
3
$
```

The number reported is the actual number of elements stored within array elements, not the largest subscript used to store an element inside the array.

```
$ array[10]=foo
$ echo ${#array[*]}
hello some text /users/steve/memos foo
$ echo ${#array[*]}
4
$
```

An array that has noncontiguous values is known as a sparse array, in case you've ever heard that phrase before.

You can declare an array of integers by specifying the array name to typeset -i:

```
typeset -i data
```