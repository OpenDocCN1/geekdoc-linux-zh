# 10.3 Passing Arguments

339

# EXAMPLE 10.40

```
(The Text File: emp.names)
Steve Blenheim
Getty Boop
Igor Chesvky
Norma Cord
Jon DeLoach
Karen Ewich

(In Script)
use warnings;
1 open ( my $fh,"<", "emp.names" ) || die "Can't open emp.names: $!";
2 while(<$fh>){
3   print if (/Norma…eof);  # … is the range operator
   }

(Output)
Norma Cord
Jonathan DeLoach
Karen Ewich
```

# EXPLANATION

1 The file emp.names is opened via the $fh filehandle.
2 The while loop reads a line at a time from the filehandle $fh.
3 When the line containing the regular expression Norma is reached, that line and all lines in the range from Norma until eof (the end of file) are printed.

# EXAMPLE 10.41

```
(The Text Files)
$ cat file1
abc
def
ghi

$ cat file2
1234
5678
9101112

(The Script)
#!/usr/bin/env perl
use warnings;
# eof.p script
1 while(<>){
2   print "$_";
3 if (eof){
4   print "-" x 30, "\n";
   close (ARGV);
```