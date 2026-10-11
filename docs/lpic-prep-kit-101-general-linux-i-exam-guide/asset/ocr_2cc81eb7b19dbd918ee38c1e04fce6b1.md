The syntax for sed is

```
sed [-n] [-e command] [-f command_file] filename [>newfile]
```

We will look at each of the options in this section.

Chapter 4 discussed using sed to search for text in a file; however, it can do much more than that. sed commands can be entered at the command line, as in the following:

```
sed s/term1/term2/ FileName
```

More commonly, however, you will use a file containing the commands in conjunction with sed, as in the following:

```
sed -f ConfFile FileName
```

where ConfFile contains the command

```
s/term1/term2
```

One of the simplest sed commands is substitution. In the previous example, sed replaces the first occurrence of the first term in each line with the second term. If term1 occurs more than once in a line, only the first occurrence is replaced. To replace every occurrence of term1 with term2, you would use g at the end, as in

```
s/term1/term2/g
```

The g tells sed to perform a global search and replace. You can limit the replacement to a specific occurrence by specifying which occurrence you want to act upon, as in the following:

```
s$3/term1/term2/
```

This would replace only the third occurrence of term1 with term2. You also can designate specific lines to process by referring to the line by number:

```
1s/term1/term2/  1,3s/term1/term2/
```

The first example will process only line 1, whereas the second processes lines 1–3. Be sure to note the placement of the numbers. If the number is first, it denotes line number, but if it is after the s (command) then it denotes the number of its occurrence. The following is an example of this:

```
s$2/term1/term2/
```

This would replace the second occurrence of term1 with term2.