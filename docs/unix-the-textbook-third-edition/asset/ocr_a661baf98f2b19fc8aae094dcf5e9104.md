echo command following done executes, congratulating you for being part of a great gene pool!

```
% cat while_demo
#!/bin/csh
set secretcode = agent007
echo "Guess the code!"
echo -n "Enter your guess: "
set yourguess = `head -1`
while ("$secretcode" != "$yourguess")
    echo Good guess but wrong. Try again!
    echo -n "Enter your guess: "
    set yourguess = `head -1`
end
echo "Wow! You are a genius!!"
exit 0
% ./while_demo
Guess the code!
Enter your guess: star wars
Good guess but wrong. Try again!
Enter your guess: columbo
Good guess but wrong. Try again!
Enter your guess: agent007
Wow! You are a genius!!
%
```

# 14.7.4 The break, continue, and goto Commands

The break and continue commands can be used to interrupt the sequential execution of the loop body. The break command transfers control to the command following end, thus terminating the loop prematurely. A good programming use of the break command is to transfer control out of a nested loop. The continue command transfers control to end, which results in the evaluation of the loop condition again, hence continuation of the loop. In both cases, the commands in the loop body following these statements are not executed. Thus they are typically part of a conditional statement such as an if statement.

The goto command can be used to transfer control to any location in the script. The following is a brief description of the command.

```
SYNTAX
goto label

Purpose: To execute the command at the label
```

The goto command transfers control to the command at label:, a tag for the command. The use of goto is considered a bad programming practice because it makes debugging of programs a daunting task. For this reason, we do not recommend its use, with