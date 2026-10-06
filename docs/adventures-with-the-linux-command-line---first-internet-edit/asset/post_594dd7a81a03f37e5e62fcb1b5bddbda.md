
number of lines processed in the input stream (NR) divided by the page length and if the result is zero, and thus an even multiple.

AWK supports an expression's useful for testing membership in an array:

```
(var in array)
```

where var is an index value and array is an array variable. Using this expression tests if the var exists in the specified array. This method of testing for array membership avoids the problem of inadvertently creating the array by testing it with methods such as:

```
if (array[var] == "
```

When the test is attempted this way, the array element var is created, as AWK creates variables simply by their use. The (var in array) form is used, no variable is created.

To test for array membership in a multi-dimensional array, the following syntax is used:

```
(var,var2) in array
```

# for : expression ; expression ) statement

The loop in AWK closely resembles the one in the C programming language. The first expression is usually used to initialize a counter variable, the second defines when the loop is completed, and the third defines how the loop is incremented or advanced at each iteration. Here is a demonstration using a loop to print fields in reverse order:

```
ls -l | awk '{s=""; for (i=NF; i>0; i--) s=$i OFS; print s}'
```

In this example we create an empty string s, then begin a loop that starts with the number of fields in the current input line (i=NF) and counts down (--) until we reach the first field (i>0). Each iteration of the loop counts the current field and the output separator to be concatenated to the string s (s = s OFS). After the loop concludes, we print the resulting value of string s.

# for ( var in array )

AWK has a special flow control statement for traversing the indices of an array. Here is an example of what it does:

In this program, we have a single BEGIN action that performs the entire exercise without the need for an input stream. We create an array a and add 10 elements, containing the string "foo". Next, we use for (i in a) to loop through all the indexes in the array and print each index. It is important to note that the order of the arrays in memory is implementation dependent, meaning that it could be anything, we cannot rely on the results in any particular order. We'll look at how to address this problem little later.

# AWK

Even without sorted order, this type of loop is useful if we need to process every element in an array. For example, we could delete every element of an array like this:

```
for (i in a) delete a[i]
```

# while ( expression ) statement

do statement while ( expression )
The while and do loops in AWK are pretty straightforward. We determine a condition that must be maintained for the loop to continue. We can demonstrate this using our field reversal program (we'll type it out in multiple lines to make the logic easier to follow):

```
ls -l | awk {
s = ""
i = NF
while (i > 0) {
s = $i OFS
i--
}
print s
}
```

The do loop is similar to the while loop; however the do loop will always execute its statement at least once, whereas the while loop will only execute its statement if the initial condition is met.

# break
continue
next

The break, continue, and next keywords are used to "escape" from loops. break and continue behave like their corresponding commands in the shell. continue tells AWK to stop and continue with the next iteration of the current loop. break tells AWK to exit the current loop entirely. the next keyword tells AWK to skip the remainder of the current program and begin processing the next record of input.

# exit expression

As with the shell, we can tell AWK to exit and provide an optional expression that sets AWK's exit status.

# Regular Expressions

Regular expressions in AWK work like those in egrep, a topic we covered in Chapter 19 of TLCL. It is important to note that back references are not supported and that some versions of AWK (most notably awk versions prior to 1.3.4) do not support POSIX-character classes.

Regular expressions are most often used in patterns, but they are also used in some of the built-in variables as FS and RS, and they have various roles in the string functions which we will discuss shortly.

Let's try using some regular expressions to tell the different file types in our directory listing (we'll make clever use of an associative array too).

```
ls -l /usr/bin | awk '
$1 ~ /\[Regular Files\]/
$1 ~ /\[directories\]/
$1 ~ /\[Symbolic Links\]/
END (for (i in t) print "\t "" t[i])'
```

In this program, we use regular expressions to identify the first character of the first field and increment the corresponding element in array r. Since we can use strings as array indexes in AWK, we split out the file type as the index. This makes printing the results in the END action easy, as we only have to traverse the array with (i in t) to obtain both the name and the accumulated total for each type.

# Output Functions

print expr1, expr2, expr3,...

As we have seen, print accepts a comma-separated list of arguments. An argument can be any valid expression; however, if an expression contains a relational operator, the entire list must be enclosed in parentheses.

The commas are important, because they separate arguments. If omitted, AWK will output them without a space.

# printf(format, expr1, expr2, expr3...)

In AWK, printf is like the C function. It formats the output based on a string. Here is an example where we use printf to format columns:

```
awk '{printf "%-10s %5d\n", $1, $2}'
```

# Writing to Files and Pipelines

In addition to stdout, we can also output to files. To do this, we use the redirection operator. For example, to redirect output to a file we use:

```
awk '{print $0}' > file.txt
```

If we want to append to a file, we use the >> operator:

```
awk '{print $0}' >> file.txt
```

# Reading Data

As we have seen, awk processes data from standard input. However, we can also specify filenames on the command line:

```
awk '{print $0}' file1 file2
```

Knowing this, we can, for example, create a program that simulates wc:

```
awk '{chars += length($0); words} END {print NR, chars}' file1
```

This program has a couple of interesting features. First, length($0) does not count the newline character at the end of line, so we have to add them to make the character count out. The second feature is NR.

Even if we don't include filenames on the command line, we can tell AWK to read data from within a program. Normally we don't do this, but there are some cases where this might be hard. For example, if we wanted to insert one file inside another, we could use getline function. Here's an example that adds a header and footer to an existing body:

```
awk '
BEGIN {
    while (getline <"header.txt" > 0) {
        print $0
    }
}
END {
    while (getline <"footer.txt" > 0) {
        print $0
    }
}' body.txt > finished_file
```

getline is quite flexible and can be used in a variety of:

# getline

In its most basic form, getline reads the next record from the current input stream. $0, NF, NR, and FNR are set.

# getline var

Reads the next record from the current input stream and assigns its contents to the variable var. var, NR, and FNR are set.

# getline <file

Reading a record from file. $0 and NF are set. It's important to check for errors when reading from files. In the earlier example above, we specified a loop as follows:
while (getline <"header.txt" > 0)

As we can see, getline is reading from the file header.txt, but what does the “> 0" mean? The answer is that, like most functions, getline returns a value. A positive value means success, zero means EOF (end of file), and a negative value means some other file-related problem, such as file not found has occurred. If we did not check the return value, we might end up with an infinite loop.
