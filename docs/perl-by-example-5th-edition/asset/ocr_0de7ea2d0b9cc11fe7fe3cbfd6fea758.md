# EXAMPLE 10.33 (CONTINUED)

(Output)
Sun Feb 18 14:12:44 PST 2014

# EXPLANATION

+   1.  The user-defined pipe handle $INPIPE will be used to pipe the output from the command as input to Perl. The output of a UNIX *date* command will be used as input by your Perl script via the *INPIPE* pipe handle. Windows users, use *date /t*.
+   2.  The scalar $today will receive its input from the *INPIPE* pipe handle; in other words, Perl reads from *INPIPE*.
+   3.  The value of the UNIX *date* command was assigned to $today and is displayed.
+   4.  After you have finished using the pipe handle, use the close function to close it. This guarantees that the command will complete before the script exits. If you don't close the pipe handle, the output may not be flushed properly.
+   5.  This format became available in version 5.6. It allows you to create lexically scoped pipe handles which will be closed when the handle goes out of scope.
+   6.  Now Perl reads from the pipe, storing the output of the UNIX *date* command in $today.

![](bbox=[0.0, 0.5, 0.8, 0.78])

# EXAMPLE 10.34

(The Script)

```
use warnings;
open(LISTDIR, "ls \*" ) or
die "PIPE failed $!\n";  # See next example for Windows
while( $filename = <LISTDIR> ) {
    print $filename;
}
```