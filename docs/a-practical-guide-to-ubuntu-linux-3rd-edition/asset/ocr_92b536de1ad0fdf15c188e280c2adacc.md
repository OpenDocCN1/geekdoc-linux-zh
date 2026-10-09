```
$ . /while1.pl
Good morning.
1. Good morning.
Today is Monday.
2. Today is Monday.
CONTROL-C

2 lines entered.
```

In the preceding example, $count keeps track of the number of lines the user enters. Putting the ++ increment operator before a variable (++$count, called a preincrement operator) increments the variable before Perl evaluates it. Alternatively, you could initialize $count to 1 and increment it with $count++ (postincrement), but then in the final print statement $count would equal one more than the number of lines entered.

$. The $. variable keeps track of the number of lines of input a program has read. Using $, you can rewrite the previous example as follows:

```
$ cat while4.pl
#!/usr/bin/perl -w
while ($line = <>) {
  print $., ". $line";
}
print "\n\nlines entered.\n";
```

$_ Frequently you can simplify Perl code by using the $_ variable. You can use $_ many places in a Perl program—think of $_ as meaning it, the object of what you are doing. It is the default operand for many operations. For example, the following section of code processes a line using the $line variable. It reads a line into $line, removes any trailing NEWLINE using chomp (page 1067), and checks whether a regular expression matches $line.

```
while (my $line = <>) {
  chomp $line;
  if ($line =~ /regex/) ...
```

You can rewrite this code by using $_ to replace $line:

```
while (my $_ = <>) {
  chomp $_;
  if ($_ =~ /regex/) ...
```

Because $_ is the default operand in each of these instances, you can also omit $_ altogether:

```
while (<>) {   # read into $_
  chomp;       # chomp $_
  if (/regex/) ...   # if $_ matches regex
```