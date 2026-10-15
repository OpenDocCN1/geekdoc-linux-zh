# EXAMPLE 12.14 (CONTINUED)

```
3 $ print $? 
0
# Success
4 $ test $name = Tom
5 $ print $? 
0
# Success
6 $ test $name != Tom
$ print $? 
1
# Failure
7 $ [ $name = Tom ]
# Brackets instead of the test command
8 $ print $? 
0
9 $ [[ $name = [Tc]?m ]]
# New ksh test command
10 $ print $? 
0
```

# EXPLANATION

1 The string Tom is assigned to the variable name.

2 The grep command will search for string Tom in datafile, and if successful in its search, will display the line found.

3 The ? variable, accessed by $?, contains the exit status of the last command executed, in this case, the exit status of grep. If grep is successful in finding the string Tom, it will return an exit status of 0. The grep command was successful.

4 The test command is used to evaluate strings and numbers, and to perform file testing. It returns an exit status of 0 if the expression is true, and an exit status of 1 if the expression fails. There must be spaces surrounding the equal sign.

5 The value of name is tested to see if it is equal to Tom. The test command returns an exit status of 0, meaning that $name does evaluate to Tom.

6 The value of name is tested to see if it is equal to Tom. The test command returns an exit status of 1, meaning that name is not equal to Tom.

7 The brackets are an alternate notation for the test command. There must be spaces after the first bracket. The expression is tested to see if $name evaluates to the string Tom.

8 The exit status of the test is 0. The test was successful because $name is equal to Tom.

9 The new Korn shell test command, [[, is used. The new test allows shell meta-character expansion. If the variable matches Tom, tom, Tim, tim, and so on, the test will return a successful status, 0.

10 The variable name did match a string beginning with T or t and ending in m, resulting in a successful exit status ($?) of 0.