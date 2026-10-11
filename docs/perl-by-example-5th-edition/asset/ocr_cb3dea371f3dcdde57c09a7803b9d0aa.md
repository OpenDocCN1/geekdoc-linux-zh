# EXAMPLE 14.13 (CONTINUED)

```
5      *(Output)*
5      Paint the flower red.
5      Paint the sky blue.
          < Data::Dumper Output>
10     $VAR1 = sub {
           my $object = shift();
           print "Paint the $object $color.\n";
         };
         $VAR2 = sub {
           my $object = shift();
           print "Paint the $object $color.\n";
         };
```

# EXPLANATION

+   1  The paint() subroutine is defined.
+   2  The lexical scalar $color is assigned the value shifted from the @_ array.
+   3  The value in $ref is assigned an anonymous subroutine.
+   4  The anonymous subroutine takes one argument from the @_ array. In this example, the value of $object will be “flower” the first time this subroutine is called, and “sky” the next time.
+   5  Here is where we see a closure in action. The lexical variable $color is still in scope. The lexical variable $color doesn't go out of scope even after the subroutine called paint() is called and exited, because the anonymous subroutine still needs it. $color is still available here even though the paint() function was called and exited.
+   6  The paint() subroutine returns a reference to the anonymous subroutine. The reference looks like this: CODE(0x100804ee8)). The reference forms the closure; it keeps the lexical variables, in this case $color, around until no longer being referenced.
+   7  The paint() subroutine is called twice with different arguments. Each time paint() is called, Perl creates a new lexical scalar, $color, with its own value. The $color variable gets wrapped up in the closure that is returned. So $p1 encloses one $color, which is initialized to “red”, and $p2 encloses a totally different $color, initialized to “blue”. You can see that these variables get their own addresses, by printing $color each time the function paint() is called to produce:
+      SCALAR(0x7f947382d880)
+      SCALAR(0x7f947382dc40)
+   8, 9  $p1 and $p2 are references to the anonymous subroutine defined on line 3. They have formed a “closure” around the variable $color defined in paint() and will have access to their own copy of that variable until it is no longer being referenced.
+   10 We can use Data::Dumper to display the values of the code references, but unless we set the $Data::Dumper::Deparse variable to 1, the contents of an anonymous subroutine will be printed as DUMMY. Data::Dumper displays the contents of the anonymous subroutine.