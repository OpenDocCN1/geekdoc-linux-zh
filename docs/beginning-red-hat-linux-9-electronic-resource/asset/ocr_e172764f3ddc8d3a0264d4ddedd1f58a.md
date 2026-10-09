```
###+
### End of main program, subroutines follow ...
###-
```

We start out by defining a set of constants – variables whose values will not change over the life of the program – using the our command. The our command allows us to define variables that have a global scope; can be accessed in subroutines. By using a constant, as opposed to a literal value, we can change its value easily without having to search and replace various instances of the actual value throughout the program.

One of the constants you should take note of is $FILESYSTEM, a data type that we have not seen so far. It is an associative array, commonly referred to as a hash, but is very different than a regular array. You can think of a hash as an array that is indexed by an alphanumeric key, rather than an ordered number. And each hash element has two scalar components: the key and an associated value. In this application, we are using a hash to associate file systems with their corresponding disk usage thresholds. For example, we can access the threshold value for the /home1 file system by using the following syntax:

```
$home = $FILESYSTEMS{ '/home1' };
```

After initialization, we proceed to use a pipe to interact with the df system command, which, in turn, produces and returns a disk usage report. Then, we iterate through each line of the report and extract the usage percentage and file system name with a regular expression. Based on the regex dissection that we performed in the previous section, can you understand this expression? We start our search toward the end of the input string, looking for one or more numerical digits followed by a percent sign. The numerical value will be stored in $1 and represents the usage percentage. Then, we match one or more whitespace characters and proceed to extract and save the remaining portion of the string in $2; this is the file system name. The trailing $ metacharacter allows us to anchor a regex to the end of the string.

Only if the line of input matches the regex do we proceed with the rest of the code. For each file system, we check to see if it exists in the hash and if the usage value exceeds the specified threshold. And only in that case, we print a diagnostic message and invoke the process_filesystem subroutine to process each user's individual directory.

We can use subroutines, also known as functions, methods and procedures, to make our code more modular. By placing a block of code that performs a distinct operation or set of operations in its own unique “container,” we can keep the program clean, easy to understand, and possibly more efficient. Let’s look at this subroutine.

```
###+
### Subroutines
###-
```