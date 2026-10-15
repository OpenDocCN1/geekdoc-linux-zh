# FORMAT

```
if ! { (command) } then
```

# EXAMPLE 10.23

```
1  if ! { `ypmatch $user passwd >& /dev/null` } then
2    echo $user is not a user here.
    exit 1
3  endif
```

# EXPLANATION

1 The ypmatch command is used to search the NIS passwd file, if you are using a network. If the command succeeds in finding the user ($user) in the passwd file, the expression evaluates to be true. The exclamation point (!) preceding the expression NOTs or complements the expression; that is, makes it false if it is true, and vice versa.

2 If the expression is not true, the user is not found and this line is executed.

3 The endif ends this if block.

# 10.6.14 The goto

A goto allows you to jump to some label in the program and start execution at that point. Although gotos are frowned on by many programmers, they are sometimes useful for breaking out of nested loops.

# EXAMPLE 10.24

```
(The Script)
#!/bin/csh -f
startover:
1  echo "What was your grade?"
   set grade = $<
3  if ( "$grade" < 0 || "$grade" > 100 ) then
4    echo "Illegal grade"
5  goto startover
endif
if ( $grade >= 89 ) then
  echo "A for the genius!"
else if ( $grade >= 79 ) then
  .. < Program continues >
```

# EXPLANATION

1 The label is a user-defined word with a colon appended. The label is called start-over. During execution of the program, the label is ignored by the shell, unless the shell is explicitly directed to go to the label.