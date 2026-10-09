Use of `"$@"`  The `who` script uses a **for** statement to loop through the command-line arguments. In this script the implied use of `"$@"` in the **for** loop is particularly beneficial because it causes the **for** loop to treat an argument that contains a **SPACE** as a single argument. This example encloses *Marilou Smith* in quotation marks, which causes the shell to pass it to the script as a single argument. Then the implied `"$@"` in the **for** statement causes the shell to regenerate the quoted argument *Marilou Smith* so that it is again treated as a single argument.

*mawk*  For each command-line argument, `who` searches the */etc/passwd* file. Inside the **for** loop, the `mawk` utility extracts the first ($1) and fifth ($5) fields from each line in */etc/passwd*. The `-F:` option causes `mawk` to use a colon (:) as a field separator when it reads */etc/passwd*, allowing it to break each line into fields. The `mawk` command sets and uses the $1 and $5 arguments; they are included within single quotation marks and are not interpreted by the shell. Do not confuse these arguments with positional parameters, which correspond to command-line arguments. The first and fifth fields are sent to `grep` (page 166) via a pipe. The `grep` utility searches for *Sid* (to which the shell has assigned the value of a command-line argument) in its input. The `-i` option causes `grep` to ignore case as it searches; `grep` displays each line in its input that contains *Sid*.

At the end of a line  An interesting syntactical exception that *bash* makes for the pipe symbol (|) appears on the line with the `mawk` command: You do not have to quote a **NEWLINE** that immediately follows a pipe symbol (that is, a pipe symbol that is the last character on a line) to keep the **NEWLINE** from executing a command. Try giving the command **who |** and pressing **RETURN**. The shell displays a secondary prompt. If you then enter **sort** followed by another **RETURN**, you see a sorted *who* list. The pipe works even though a **NEWLINE** follows the pipe symbol.

# while

The **while** control structure has the following syntax:

```
while *test-command*
    do
        *commands*
    done
```

As long as the *test-command* (Figure 27-5) returns a *true* exit status, the **while** structure continues to execute the series of *commands* delimited by the **do** and **done** statements. Before each loop through the *commands*, the structure executes the *test-command*. When the exit status of the *test-command* is *false*, the structure passes control to the statement after the **done** statement.

*test builtin*  The following shell script first initializes the *number* variable to zero. The **test** builtin then determines whether *number* is less than 10. The script uses **test** with the `-lt` argument to perform a numerical test. For numerical comparisons, you must use `-ne` (not equal), `-eq` (equal), `-gt` (greater than), `-ge` (greater than or equal to), `-lt` (less than), or `-le` (less than or equal to). For string comparisons, use `=` (equal) or `!=` (not equal) when you are working with **test**. In this example, **test** has an exit status of 0 (*true*) as long as *number* is less than 10. As long as **test** returns *true*, the structure