![](bbox=[0.205, 0.08, 0.775, 0.415])

Figure 9-11: Output of awkcom.a

Now compare and contrast the awkcom.a program with this Perl program:

```
#!/usr/bin/perl
# program name: perlcom.p
# purpose: count the source file's comment lines

$filein = $ARGV[0];
while (<>)
{
    if (/^#/ && !/^#!/) {
        ++$line_count
    }
}
print ("File \"$filein\" has $line_count comment lines. \n"
);
```

Although the end results of both programs are very similar, you can see where the two programs differ. Awk uses an implicit while loop that automatically sends the entire contents of the file named on the command line to the pattern-matching and action part of the program. However, note that for the Perl program you need to build the while loop explicitly.