![](bbox=[0.28, 0.08, 0.68, 0.66])

FIGURE 12.5 Semantics of the while statement.

<Ctrl+C> would also do the trick, unless the process is designed to ignore <Ctrl+C>. In that case, you need to put the process in the background by pressing <Ctrl+Z> and use the kill -9 command to terminate it. See Chapter 10 for details on processes.

The script in the while_demo file shows a simple use of the while loop. When you run this script, the secretcode variable is initialized to agent007 and you are prompted to make a guess. Your guess is stored in a local variable yourguess. If your guess is not agent007, the condition for the while loop is true and the commands between do and done are executed. This program displays a message tactfully informing you of your failure and prompts you for another guess. Your guess is again stored in the yourguess variable, and the condition for the loop is tested. This process continues until you enter agent007 as your guess. At which time, the condition for the loop becomes false and the control comes out of the while statement. The echo command following done executes, congratulating you for being part of a great gene pool!

```
$ cat while_demo
#!/bin/sh
secretcode=agent007
echo "Guess the code!"
echo -e "Enter your guess: \c"
read yourguess
```