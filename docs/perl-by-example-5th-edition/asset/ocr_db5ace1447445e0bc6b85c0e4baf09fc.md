![](bbox=[0.07, 0.07, 0.71, 0.15])

**Figure 7.3** How the until loop works.

# FORMAT

```
until (Expression) {Block}
```

# EXAMPLE 7.11

```
(The Script)
use warnings;
1 $num=0;                 # initialize
2 until ($num == 10){
      # Test expression; loop quits when expression is true or 1
3    print "$num ";
4    $num++;      # Update the loop variable $num; increment $num
5 }
6 print "\nOut of the loop.\n";

(Output)
3 0 1 2 3 4 5 6 7 8 9
6 Out of the loop.
```

# EXPLANATION

+   1. The scalar `$num` is initialized. The initialization takes place before entering the loop.
+   2. The test expression is evaluated. If the result is false, the block of statements in curly braces is executed. When `$num` is equal to 10, the loop exits.
+   3. The scalar `$num` is incremented. If not, the test expression would always yield a false value and the loop would never end.

# EXAMPLE 7.12

```
(The Script)
use warnings;
1 print "Are you o.k.? ";
2 chomp($answer=<STDIN>);
3 until ($answer eq "yes"){
4     sleep(1);
5    print "Are you o.k. yet? ";
6    chomp($answer=<STDIN>);
7 }
8 print "Glad to hear it!\n";
```