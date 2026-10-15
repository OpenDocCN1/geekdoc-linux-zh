
## 6.20 Arrays

Arrays in awk are called associative arrays because the subscripts can be either numbers or strings. The subscript is often called the key and is associated with the value assigned to the corresponding array element. The keys and values are stored internally in a table where a hashing algorithm is applied to the value of the key in question. Due to the techniques used for hashing, the array elements are not stored in a sequential order, and when the contents of the array are displayed, they may not be in the order you expected.

An array, like a variable, is created by using it, and awk can infer whether it is used to store numbers or strings. Array elements are initialized with numeric value zero and string value null, depending on the context. You do not have to declare the size of an awk array. Awk arrays are used to collect information from records and may be used for accumulating totals, counting words, tracking the number of times a pattern occurred, and so forth.

### 6.20.1 Subscripts for Associative Arrays

Using Variables As Array Indexes. [See Example 6.135 for a demonstration.

### EXAMPLE 6.135

(The Input File)
% cat employees
Tom Jones      4424   5/12/66    543354
Mary Adams     5346   11/4/63    28765
Sally Chang    1654   7/22/54    658000
Billy Black    1683   9/23/44    336500

(The Command Line)
1 % awk '{name[++i]=$2};END{for(i=0; i<NR; i++) print i, name[i]}' employees
0 Jones
1 Adams
2 Chang
3 Black

2 % awk '{id[NR]=$3};END{for(x = 1; x <= NR; x++) print id[x]}' employees
4424
5346
1654
1683

### EXPLANATION

1 The subscript in array name is a user-defined variable, x. The ++ indicates a numeric context. Awk initializes x to 0 and increments x by 1 after (post-increment operator) it is used. The value of the second field is assigned to each element of the name array. In the END block, the for loop is used to loop through the array, printing the value that was stored there, starting at subscript 0. Because the subscript is just a key, it does not have to start at 0. It can start at any value, either a number or a string.

2 The awk variable NR contains the number of the current record. By using NR as a subscript, the value of the third field is assigned to each element of the array for each record. At the end, the for loop will loop through the array, printing out the values that were stored there.

The Special-for Loop. The special-for loop is used to read through an associative array in cases where the for loop is not practical; that is, when strings are used as subscripts or the subscripts are not consecutive numbers. The special-for loop uses the subscript as a key into the value associated with it.

### FORMAT

```
{for(item in arrayname){
print arrayname[item]
}
}
```

### EXAMPLE 6.136

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

### EXAMPLE 6.136 (CONTINUED)

```
(The Command Line, Special-for Loop)
2 % nawk '/Tom/{name[NR]=$1;}
END{for(i in name){print name[i]}}' db
Tom
Tommy
Tom
Tom
```

### EXPLANATION

- 1 If the regular expression Tom is matched against an input line, the name array is assigned a value. The NR value, the number of the current record, will be used as an index in the name array. Each time Tom is matched on a line, the name array is assigned the value of $1, the first field. When the END block is reached, the name array consists of four elements: name[1], name[5], name[6], and name[8]. Therefore, when printing the values for the name array with the traditional for loop, the values for indexes 2, 3, 4, and 7 are null.
- 2 The special-for loop iterates through the array, printing only values where there was a subscript associated with that value. The order of the printout is random because of the way the associative arrays are stored (hashed).

Using Strings As Array Subscripts. A subscript may consist of a variable containing a string or literal string. If the string is a literal, it must be enclosed in double quotes.

### EXAMPLE 6.137

```
(The Input File)
% cat datafile3
tom
mary
sean
tom
mary
mary
bob
mary
alex
```

```
(The Script)
# awk.sc script
1 /tom/ { count["tom"]++ }
2 /mary/ { count["mary"]++ }
3 END{print "There are " count["tom"] " Toms in the file and " count["mary"] " Marys in the file."}
```
