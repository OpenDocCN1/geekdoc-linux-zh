```
$ perl sort4.pl
22 188 44 2 12
2 12 22 44 188
188 44 22 12 2
```

# SUBROUTINES

All variables are package variables (page 1045) unless you use the my function to define them to be lexical variables (page 1045). Lexical variables defined in a subroutine are local to that subroutine.

The following program includes a main part and a subroutine named add(). This program uses the variables named $one, $two, and $ans, all of which are package variables. They are available to both the main program and the subroutine. The call to the subroutine does not pass values to the subroutine and the subroutine returns no values. This setup is not typical: It demonstrates that all variables are package variables unless you use my to declare them to be lexical variables.

The subroutine1.pl program assigns values to two variables and calls a subroutine. The subroutine adds the values of the two variables and assigns the result to another variable. The main part of the program displays the result.

```
$ cat subroutine1.pl
$one = 1;
$two = 2;
add();
print "Answer is $ans\n";

sub add {
    $ans = $one + $two
}

$ perl subroutine1.pl
Answer is 3
```

The next example is similar to the previous one, except the subroutine takes advantage of a return statement to return a value to the main program. The program assigns the value returned by the subroutine to the variable $ans and displays that value. Again, all variables are package variables.

```
$ cat subroutine2.pl
$one = 1;
$two = 2;
$ans = add();
print "Answer is $ans\n";

sub add {
    return ($one + $two)
}

$ perl subroutine2.pl
Answer is 3
```