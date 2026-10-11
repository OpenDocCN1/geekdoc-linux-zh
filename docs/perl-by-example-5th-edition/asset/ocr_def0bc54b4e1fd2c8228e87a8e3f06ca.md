# EXAMPLE 16.62

```
(Command Line)
1 $ perl -e 'while(glob("p??? [1-5]*")) { print "$_\n";}'
perl
perl2
perl3
perl4
perl5
```

```
(In Script)
2 while ( glob("p??? [1-5]*")) {
3   print "$_\n";
}
```

```
(Output)
3 perl
   perl2
   perl3
   perl4
   perl5
```

# EXPLANATION

+   1.  At the command line, the glob function will \`glob\' onto any files in the current working directory whose name begins with a p, followed by any three characters (???), followed by any number between 1 and 5 ([1-5]). Each filename that matches the expression is assigned to $\_, and then printed.
+   2.  This time, glob is being used in a script. The behavior is the same as in the first example.
+   3.  The expanded filenames are printed.

# 16.4 Error Handling

There are a number of occasions when a system call can fail; for example, when you try to open a file that doesn't exist or remove a directory when it still contains files or when you try to read from a file for which you do not have read permission. Although we have used the die function in earlier examples, now we will go into more detail about error handling and functions you can use to handle errors. The functions are the die function, the warn function, and the eval function.

+   - Use the die function to quit the Perl script if a command or filehandle fails.
+   - The warn function is like the die function, but it does not exit the script.
+   - The eval function has multiple uses, but it is used primarily for exception handling.