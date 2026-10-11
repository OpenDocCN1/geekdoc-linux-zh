
## FORMAT

```
do (Block) while (Expression); 
do (Block) until (Expression);
```

## EXAMPLE 7.13

(The Script)

```
use warnings;
my $x = 1;
do {
    print "$x ";
    $x++;
} while ($x <= 10); # Test after the do block has executed
print "\n";

$y = 1;
do {
    print "$y ";
    $y++;
} until ($y > 10);
```

(Output)

```
1 2 3 4 5 6 7 8 9 10
1 2 3 4 5 6 7 8 9 10
```

## EXPLANATION

- 1. The scalar `$x` is assigned the value 1.
- 2. The `do/while` loop statement starts.
- 3. The block of statements is executed before the expression within the `while` loop is tested.
- 4. The scalar `$x` is incremented once.
- 5. The conditional expression following the `while` is evaluated. If true, the block of statements is executed again, and so on.
- 6. The scalar `$y` is assigned the value 1.
- 7. The `do/until` loop statement starts.
- 8. The block of statements is executed.
- 9. The scalar `$y` is incremented once.
- 10. The conditional expression following the `until` is evaluated. If false, the block of statements is executed again, and so on.

## EXAMPLE 7.14

```
1    use warnings;
2    my $n=0;
3    do {
4        print $n++ == 0?"Anybody out there? ": "Anybody out there yet?";
5        chomp($input = <STDIN>);
6        $input = lc $input;
7        sleep 1;
8    } until ( $input eq "yes" );
9    print "Welcome home!\n";
```

Output:
Anybody out there? No
Anybody out there yet? not yet
Anybody out there yet? yup
Anybody out there yet? Yes
Welcome home!

## EXPLANATION

- 1. Initialize `$n` to zero.
- 2-5. The first time in the loop, `$n` will evaluate to zero and the program prints "Anybody out there?". Because this is a post increment `++`, `$n` will be incremented after it is evaluated, and therafter `$n` will be greater than 0. "Anybody out there yet?" will be displayed until the value of `$input` equals the string "yes". The builtin `sleep` function causes the program to pause for one second.
- 6. The expression in the `until` loop is tested and if it tests false, the `do` block will be executed again.

### 7.3.4 The for Loop (The Three-Part Loop)

The *for* statement is like the *for* loop in C. The *for* keyword is followed by three expressions separated by semicolons and enclosed within parentheses. You can omit any or all of the expressions, but not the two semicolons. The first expression is used to set the initial value of variables, the second expression is used to test whether the loop should continue or stop, and the third expression updates the loop variables. See Figure 7.4.

![](img/8556abcb353c0991f12099420ec28735_225_0.png)

Figure 7.4 How the three-part for loop works.

### FORMAT

```
for (Expression1;Expression2;Expression3) {Block}
```

The above format is equivalent to the following `while` statement:

```
Expression1;
while (Expression2)
    {Block; Expression3};
```

### EXAMPLE 7.15

(The Script)

```
use warnings;
1 for (my $i=0; $i<10; $i++){ # Initialize, test, and increment $i
      print "$i";
  }
3 print "\nOut of the loop.\n";
```

(Output)

```
2 0 1 2 3 4 5 6 7 8 9
3 Out of the loop.
```

### EXPLANATION

- 1. The *for* loop contains three expressions. In the first expression, the scalar *$i* is assigned the value 0. This statement is executed just once. The second expression tests whether *$i* is less than 10, and if so, the block statements are executed (that is, the value of *$i* is printed). The last expression increments the value of *$i* by 1. The second expression is again tested, and the block is executed, *$i* is incremented, and so on, until the test evaluates to false.
- 2. The value of *$i* is printed each time through the loop.

### EXAMPLE 7.16

(The Script)

```
use warnings;
# Initialization, test, and increment, decrement of
# counters is done in one step.
1 for (my $count=1, my $beers=10, my $remain=$beers,
      my $where="on the shelf";
      $count <= $beers; $count++, $remain--)
{
2 if ($remain == 1){
      print "$remain bottle of beer $where $where = ";
  }
  else {
      print "$remain bottles of beer $where $where.";
  }
  print " Take one down and pass it all around.\n";
  print "Now ", $beers - $count, " bottles of beer $where!\n";
  if ($count == 10) {print "Party's over.\n";}
}
```

(Output)

```
10 bottles of beer on the shelf on the shelf. Take one down and pass it all around.
Now 9 bottles of beer on the shelf!
9 bottles of beer on the shelf on the shelf. Take one down and pass it all around.
Now 8 bottles of beer on the shelf!
8 bottles of beer on the shelf on the shelf. Take one down and pass it all around.
Now 7 bottles of beer on the shelf!
< continues >
2 bottles of beer on the shelf on the shelf. Take one down and pass it all around.
Now 1 bottle of beer on the shelf!
1 bottle of beer on the shelf on the shelf. Take one down and pass it all around.
Now 0 bottles of beer on the shelf!
Party's over.
```

### EXPLANATION

- 1. The initialization of all scalars is done in the first expression of the *for* loop. Each initialization is separated by a comma, or the expression is terminated with a semicolon. The first expression is executed only once, when the loop starts. The second expression is the test. If it evaluates to true, the statements in the block are executed. After the last statement in the block is executed, the third expression is evaluated. The control is then passed to the second expression in the *for* loop, and so on.
- 2. The block is executed if the second expression in the *for* loop is evaluated as true.
- 3. This statement will be tested and, if the condition is true, the statement will be executed and control will go to the third expression within the *for* loop, incrementing *$count* for the last time.

### 7.3.5 The *foreach* (*for*) Loop

If you need to iterate through an array or hash such as a list of files, IP or email addresses, keys, values from a hash, and so forth, then the *foreach* loop, as its name implies, is a control structure designed just for you.

The *foreach* loop (a synonym for *for*) iterates over each element in the parenthesized list or an array, aliasing each element of the list to a scalar variable, one after the other, until the end of the list.

The *VARIABLE* is local to the *foreach* block. It will regain its former value when the loop is exited. Any changes made when assigning values to *VARIABLE* will, in turn, affect the individual elements of the array. If *VARIABLE* is not present, the *$_* special scalar variable is implicitly used.

### FORMAT

```
foreach VARIABLE {LIST} {BLOCK}
for {LIST} {BLOCK}
```

### EXAMPLE 7.17

(The Script)

```
use warnings;
1 foreach my $pal {'Tom', 'Dick', 'Harry', 'Pete'} {
2     print "Hi $pal\n";
     }
```

(Output)

```
2 Hi Tom!
Hi Dick!
Hi Harry!
Hi Pete!
```

### EXPLANATION

- 1. The `foreach` is followed by the scalar `$pal` and a list of names. `$pal` points to each name in the list, starting with `Tom`. You can think of `$pal` as an alias, or reference, for each item in the list. Each time the loop is entered, `$pal` goes to the next item in the list and gets that value. So, for example, after `Tom`, `Dick` is fetched, then `Harry`, and so on until all list items have been used, at which time the loop exits.
- 2. Each time through the loop, the value referenced by `$pal` is printed. (See Figure 7.5.)

![](img/8556abcb353c0991f12099420ec28735_228_0.png)

Figure 7.5 *The foreach loop.*

### EXAMPLE 7.18

(The Script)

```
use warnings;
1 foreach my $hour {1 .. 24} { # The range operator is used here
2     if ($hour > 0 && $hour < 12) {print "Good-morning.\n";}
3     elsif ($hour == 12) {print "Happy Lunch.\n";}
4     elsif ($hour > 12 && $hour < 17) {print "Good afternoon.\n";}
5     else {print "Good-night.\n";}
6     }
```

(Output)

```
2
Good-morning.
Good-morning.
Good-morning.
Good-morning.
Good-morning.
Good-morning.
Good-morning.
Good-morning.
Good-morning.
Good-morning.
Good-morning.
3
Happy Lunch.
4
Good afternoon.
Good afternoon.
Good afternoon.
Good afternoon.
5
Good-night.
Good-night.
Good-night.
Good-night.
Good-night.
Good-night.
Good-night.
Good-night.
```

The list `(1 .. 24)` is a range of list items starting with 1 and ending with 24. Each of those values is referenced in turn by the scalar `$hour`. The block is executed, and the next item in the list is assigned to `$hour`, and so on.

The scalar `$hour` is tested, and if the value is greater than 0 and less than 12, the `print` statement is executed.

If the previous `elsif` statement is false, this statement is tested. If the scalar `$hour` is equal to 12, the `print` statement is executed.

If the previous `elsif` statement is false, this statement is tested. If the scalar `$hour` is greater than 12 and less than 17, the `print` statement is executed.

If all of the previous statements are false, the `else`, or default statement, is executed.
