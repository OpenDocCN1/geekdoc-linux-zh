
```
then
    echo -n "$user:   "
    grep "^""echo $user:":" /etc/passwd | cut -f5 -d':'
fi
done
exit 0
$ ./user_info dheckman ghacker sarwar
dheckman:  Dennis R. Heckman
ghacker:   George Hacker
sarwar:    Syed Mansoor Sarwar
$
```

## 12.6.3 The while Statement

The while statement, also known as the while loop, allows repeated execution of a block of code based on the condition of an expression. The following is a brief description of the statement.

```
SYNTAX
while expression
do
    command-list
done

Purpose: To execute commands in command-list as long as expression evaluates to true
```

The expression is evaluated and, if the result of this evaluation is true, the commands in command-list are executed and expression is evaluated again. This sequence of expression evaluation and execution of command-list, known as one iteration, is repeated until the expression evaluates to false. At that time, control comes out of the while statement and the statement following done is executed. Figure 12.5 depicts the semantics of the while statement.

The variables and/or conditions in the expression that result in a true value must be correctly manipulated in the commands in command-list for well-behaved loops—that is, loops that eventually terminate and allow execution of the rest of the code in a script. Loops in which the expression always evaluates to true are known as nonterminating, or infinite, loops. Infinite loops, usually a result of poor design and/or programming, are undesirable because they continuously use CPU time without accomplishing any useful task. However, some applications do require infinite loops. For example, all the servers for Internet services such as the HTTP service (which allows us to browse webpages on the Internet) are programs that run indefinitely, waiting for client requests. In case of the HTTP service, for example, the client requests come through Web browsers (i.e., HTTP clients) such as Mozilla Firefox. Once a server has received a client request, it processes it, sends a response to the client, and waits for another client request. The only way to terminate a process with an infinite loop is to kill it by using the kill command. Or, if the process is running in the foreground, pressing

![](img/02e070097d401d3bf7de4bf1c470b267_522_0.png)

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

```
while [ "$secretcode" != "$yourguess" ]
do
	echo "Good guess but wrong. Try again!"
	echo -e "Enter your guess: \c"
	read yourguess
done
echo "Wow! You are a genius!!"
exit 0
$ ./while_demo
Guess the code!
Enter your guess: star wars
Good guess but wrong. Try again! Enter your guess: columbo
Good guess but wrong. Try again! Enter your guess: agent007
Wow! You are a genius!!
$
```

## 12.6.4 The until Statement

The syntax of the until statement is similar to that of the while statement, but its semantics are different. Whereas in the while statement the loop body executes as long as the expression evaluates to true, in the until statement the loop body executes as long as the expression evaluates to false. The following is a brief description of the statement.

```
SYNTAX
until expression
do
	command-list
done

Purpose: To execute commands in command-list as long as expression evaluates to false
```

Figure 12.6 illustrates the semantics of the until statement. The code in the until_demo file performs the same task that the script in the while_demo file does (see Section 12.6.3), but it uses the until statement instead of the while statement. Thus, the code between do and done (the loop body) is executed for as long as your guess is not agent007.

```
$ cat until_demo
#!/bin/sh
secretcode=agent007
echo "Guess the code!"
echo -n "Enter your guess: "
read yourguess
until [ "$secretcode" = "$yourguess" ]
do
echo "Good guess but wrong. Try again!"
echo -n "Enter your guess: "
```
