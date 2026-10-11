# EXAMPLE 10.5 (CONTINUED)

```
(The Script)

```perl
use warnings;
# Open a file with a filehandle
open(my $fh, "<", "datebook") || die "Can't open datebook: $!\n";
while(my $line = <$fh>) { # Each line, in turn, is assigned to $line
    print "$line" if $line =~ /Lori/i;
}
close($fh);
```

(Output)

```
Lori Gortz
```
```

# EXPLANATION

+   1. The *datebook* file is opened for reading.
+   2. When the *while* loop is entered, a line is read from the file and stored in the scalar `$line`.
+   3. The value of the scalar `$line` is printed if it contains the pattern *Lori*, and *Lori* is at the beginning of the line.
+   4. When the closing brace is reached, control goes back to line 2, and another line is read from the file. The loop ends when the file has no more lines.
+   5. The file is closed by closing the filehandle.

**“Slurping” a File into an Array.** When assigning input from a file to an array, Perl takes each line (ending in \n) as an element of the array, “slurping” up each line of the file and adding it to the array until end of file is reached.

# EXAMPLE 10.6

```
(The Script)

```perl
use warnings;
# Open a file with a filehandle
open(my $fh, "<", "datebook") || die "Can't open datebook: $!\n";
@lines = <$fh>;      # Contents of the entire file are printed
print "\nThe datebook file contains ", scalar @lines,
      " lines of text.\n";
close($fh);
```

(Output)

```
The datebook file contains 7 lines of text.
```
```