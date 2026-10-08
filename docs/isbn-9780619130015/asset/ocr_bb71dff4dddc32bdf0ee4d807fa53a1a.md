terminates. Two commands inside the while loop are enclosed within curly braces: print “$_” displays each record that is read in, and ++$line_count increments (counts) the records in the file. The last command, print (“File \$filein\”, has \$line_count lines. \n”) prints the name of the file (saved in \$filein) and the number of lines in the file.

Next, you learn how to open the file from within your program, as opposed to passing it on the command line. All files opened inside programs must be closed before the program terminates.

# To use Perl to open a file from within a program:

+   1.  Use the editor of your choice to create the file perread.p2.

+   2.  Enter this Perl program:

```
#!/usr/bin/perl
# program name: perread.p2
# purpose: Open disk file. Read and display the records in
#             the file. Count the number of records in the
#             file.

open (FILEIN, "students") || warn "Could not open students
file\n";
while (<FILEIN>)
{
    print "$_";
    ++$line_count;
}
print ("File \"students\" has \$line_count lines. \n");
close (FILEIN);
```

+   3.  Save the file and quit the editor.

+   4.  Give the file execute permission.

+   5.  Test the program by typing ./perread.p2 and then pressing Enter. Your screen should then display the contents of the students file, shown in Figure 9-14.