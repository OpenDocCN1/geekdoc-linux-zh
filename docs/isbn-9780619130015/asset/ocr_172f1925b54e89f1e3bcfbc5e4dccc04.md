![](bbox=[0.15, 0.07, 0.75, 0.41])

Figure 9-12: Output of perlcom.p

The first line of each program tells the shell program to run either the awk program or the Perl program and pass the statements in the file to the program for execution. Both programs also use the pound sign (#) to specify a comment line. Further, the pattern-matching code is the same in both programs. That is where the similarities end.

The -f option in the awk program tells the shell that the program is being called with a script file that contains the awk commands. Recall that awk contains more built-in commands to read lines from the file. All awk needs is the pattern-matching conditions to select the lines. The reading of the file, in awk, is implied as shown in this code.

```
/^#|&& !/^#!\t{++line_count}

```

Awk also uses BEGIN and END to control when commands execute. All statements in a BEGIN block execute before the input file is read. All statements in an END block execute after all the contents of the input file have been read. This program only needs the END pattern.

In the Perl program, the code:

```
$filein = $ARGV[0];

```

takes the name of the file on the command line (ARGV[0]) and places it in a variable so it can be referenced later. The filename originally stored in ARGV[0] from the command line is destroyed during the while loop.

```
while (<>)

```

The <> symbol is called the diamond operator. Once the file is opened, you can access its data using the diamond operator. Each time it is called, it returns the next line from the file.