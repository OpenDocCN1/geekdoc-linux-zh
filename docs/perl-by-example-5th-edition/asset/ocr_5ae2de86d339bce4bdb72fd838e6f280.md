# EXAMPLE 10.38 (CONTINUED)

```
(The Script)
```
#!/usr/bin/env perl
use warnings;
# Scriptname: grab.pl
# Program will behave like grep -- will search for a pattern
# in any number of files.
1 if ( scalar @ARGV < 2) {die "Usage: $0 pattern filename(s) \n"}
2 my $pattern = shift; # implicitly shifts @ARGV
3 while(my $line=<ARGV>){
      print "$ARGV: $line" if $line =~ /$pattern/i;
    close(ARGV) if eof;
}
```

(Output)
```
$ grab.pl
1 Usage: grab.pl pattern filenames(s)
2 $ grab.pl 'norma' db
db:5: Norma Cord
3 $ grab.pl 'Sir Lancelot' db
db:4: Sir Lancelot
4 $ grab.pl '...' db
db:1: Tori Gortz
5 $ grab.pl 'Steve d*'
databaseb.master:12: Johann Erickson:Stevensville, Montana
datafile:8: Steven Daniels:496-456-5676:83755:11/12/56:20300
db:1: Steve Blenheim
```

```

# EXPLANATION

+   1. If there are no command-line arguments, the die function is executed. $0 is the current Perl script name.
+   2. The first argument is shifted from the @ARGV array. This should be the pattern that will be searched for.
+   3. Since the first argument was shifted off the @ARGV array and assigned to the scalar $pattern, the remaining arguments passed in from the command line are opened in turn to the ARGV filehandle. When the while loop is entered, a line is read and assigned to $line.
+   4. The ARGV scalar holds the name of the file that is currently being processed. The $ variable holds the current line number. If the value in $pattern is matched, the filename where it was found, the number of the line where the pattern was found, and the line itself are printed. The i after the last delimiter in the pattern turns off case sensitivity.
+   5. When the file being processed reaches the end of file (EOF), the ARGV filehandle is closed. This causes the $. variable to be reset. If ARGV is not closed explicitly here, the $. variable will continue to increment and not be set back to 1 when the next file is read.