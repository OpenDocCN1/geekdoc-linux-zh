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

# 12.6.3 The while Statement

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