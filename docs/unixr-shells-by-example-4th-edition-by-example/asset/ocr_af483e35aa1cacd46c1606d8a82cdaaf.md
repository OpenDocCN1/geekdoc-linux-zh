# EXPLANATION

1 The subscript in array name is a user-defined variable, x. The ++ indicates a numeric context. Awk initializes x to 0 and increments x by 1 after (post-increment operator) it is used. The value of the second field is assigned to each element of the name array. In the END block, the for loop is used to loop through the array, printing the value that was stored there, starting at subscript 0. Because the subscript is just a key, it does not have to start at 0. It can start at any value, either a number or a string.

2 The awk variable NR contains the number of the current record. By using NR as a subscript, the value of the third field is assigned to each element of the array for each record. At the end, the for loop will loop through the array, printing out the values that were stored there.

The Special-for Loop. The special-for loop is used to read through an associative array in cases where the for loop is not practical; that is, when strings are used as subscripts or the subscripts are not consecutive numbers. The special-for loop uses the subscript as a key into the value associated with it.

# FORMAT

```
{for(item in arrayname){
print arrayname[item]
}
}
```

# EXAMPLE 6.136

(The Input File)
% cat db
1 Tom Jones
2 Mary Adams
3 Sally Chang
4 Billy Black
5 Tom Savage
6 Tom Chung
7 Reggie Steel
8 Tommy Tucker

(The Command Line, for Loop)
1 % nawk '/^Tom/{name[NR]=$1};\
END{for(i = 1; i <= NR; i++) print name[i]}' db
Tom

Tom
Tom

Tommy