```
$ cat subroutine4.pl
$one = 1;
$two = 2;
$ans = addplusone($one, $two);
print "Answer is $ans\n";
sub addplusone {
    return ($_[0] + $_[1] + 2);
}

$ perl subroutine4.pl
Answer is 5
```

The final example in this section presents a more typical Perl subroutine. The subroutine max() can be called with any number of numeric arguments and returns the value of the largest argument. It uses the **shift** function to assign to **$biggest** the value of the first argument the subroutine was called with and to shift the rest of the arguments. After using **shift**, argument number 2 becomes argument number 1 ($8), argument 3 becomes argument 2 (**$4**), and argument 4 becomes argument 3 (**$2**). Next, **foreach** loops over the remaining arguments (**@_**). Each time through the foreach block, Perl assigns to **$_** the value of each of the arguments, in order. The **$biggest** variable is assigned the value of **$_** if **$_** is bigger than **$biggest**. When **max()** finishes going through its arguments, **$biggest** holds the maximum value, which **max()** returns.

```
$ cat subroutine5.pl
$ans = max (16, 8, 64, 2);
print "Maximum value is $ans\n";

sub max {
    my $biggest = shift;   # Assign first and shift the rest of the arguments to max()
    foreach (@_) {
        $biggest = $_ if $_ > $biggest;
    }
    return ($biggest);
}

$ perl subroutine5.pl
Maximum value is 64
```

# ## **REGULAR EXPRESSIONS**

Appendix A defines and discusses regular expressions as you can use them in many Linux utilities. All of the material in Appendix A applies to Perl, except as noted. In addition to the facilities described in Appendix A, Perl offers regular expression features that allow you to perform more complex string processing. This section reviews some of the regular expressions covered in Appendix A and describes some of the additional features of regular expressions available in Perl. It also introduces the syntax Perl uses for working with regular expressions.