```
$ echo There are $(60*60*24*365) seconds in a non-leap year.
There are 31536000 seconds in a non-leap year.
```

The next example uses wc, cut, arithmetic expansion, and command substitution (page 362) to estimate the number of pages required to print the contents of the file **letter.txt**. The output of the wc (word count) utility used with the -l option is the number of lines in the file, in columns (character positions) 1 through 4, followed by a SPACE and the name of the file (the first command following). The cut utility with the -c1-4 option extracts the first four columns.

```
$ wc -l letter.txt
351 letter.txt
$ wc -l letter.txt | cut -c1-4
351
```

The dollar sign and single parenthesis instruct the shell to perform command substitution; the dollar sign and double parentheses indicate arithmetic expansion:

```
$ echo $( ($(wc -l letter.txt | cut -c1-4)/66 + 1))
6
```

The preceding example sends standard output from wc to standard input of cut via a pipe. Because of command substitution, the output of both commands replaces the commands between the $( and the matching ) on the command line. Arithmetic expansion then divides this number by 66, the number of lines on a page. A 1 is added because the integer division results in any remainder being discarded.

# Fewer dollar signs ($)

> When you use variables within $( ( and )), the dollar signs that precede individual variable references are optional:

```
$ x=23  y=37
$ echo $((${x + 3*$y}))
157
$ echo $((2*x + 3*$y))
157
```

Another way to get the same result without using cut is to redirect the input to wc instead of having wc get its input from a file you name on the command line. When you redirect its input, wc does not display the name of the file:

```
$ wc -l < letter.txt
351
```

It is common practice to assign the result of arithmetic expansion to a variable:

```
$ numpages=$( ($(wc -l < letter.txt)/66 + 1))
```

> The let builtin evaluates arithmetic expressions just as the $(( )) syntax does. The following command is equivalent to the preceding one:

```
$ let "numpages=$((wc -l < letter.txt)/66 + 1)"
```