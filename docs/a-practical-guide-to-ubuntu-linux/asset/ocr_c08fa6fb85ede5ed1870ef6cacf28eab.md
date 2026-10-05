```
$ perl sort4.pl
22 188 44 2 12
2 12 22 44 188
188 44 22 12 2
```

# SUBROUTINES

All variables are package variables (page 1045) unless you use the my function to define them to be lexical variables (page 1045). Lexical variables defined in a subroutine are local to that subroutine.

The following program includes a main part and a subroutine add(). The program uses the variables named Some, $two, and $ans, all of which package variables: They are available to both the main program and the subroutine. The call to the subroutine does not pass values to the subroutine and the subroutine returns no values. This style is not typical: It demonstrates that all variables are package variables unless you use my to declare them to lexical variables.

The subroutine1.pl assigns values to two variables and calls a subroutine. The subroutine assigns the values of the two variables and assigns the result to another variable. The main part of the program displays the result.

```
$ cat subroutine1.pl
Sone = 1;
$two = 2;
add();
print "Answer is $ans\n";
```

```
sub add {
$ans =Sone + $two
}
```

```
$ perl subroutine1.pl
Answer is 3
```

The next example is similar to the previous one, except the subroutine takes advantage of a return statement to return a value to the main program. The program assigns the value returned by the subroutine to the variable $Ans and displays the value. Again, all variables are package variables.

```
$ cat subroutine2.pl
Sone = 1;
$two = 2;
$ans = add();
print "Answer is $ans\n";
```

```
sub add {
return ($Some + $two)
}
```

```
$ perl subroutine2.pl
Answer is 3
```