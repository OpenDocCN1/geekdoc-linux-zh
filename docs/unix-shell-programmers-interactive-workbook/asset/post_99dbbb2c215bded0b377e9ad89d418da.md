
## 532 Lab 11.3: Intercepting and Generating Traps

e) What happened when you pressed Ctrl-C?

Now run the following two commands:

```
tt1 &
kill -INT %1
```

f) Does the trap handler affect signal handling for the script?

You can clear the setup for a condition (or a list of conditions) by entering trap command with a dash in the position where the handler goes, followed by the condition name(s) that you want to restore to default operation.

Enter the following sequence of commands:

```
trap
trap - INT
trap
```

g) What did the three trap commands do?

Now create a new version of our test program for this exercise, called tt2, that looks like the following:

```
# test-trap 2
trap 'print "$0: Resetting"; sleep 30' INT
trap 'print "$0: Exit Trap' EXIT
```

```
sleep 30
print "$0: Exiting Normally"
```

Run the program in the foreground and press Ctrl-C as it runs.

- h) What happens each time you press Ctrl-C?

Now run the program in the background and enter the following sequence of commands:

```
tt2 &
kill -INT %1
kill -USR1 %1
```

- i) What printed when the program terminated?

We won't work with ERR or KEYBD conditions here. You should be able to see how to use the ERR condition based on the examples you have done so far. The KEYBD condition is used to customize your interactive environment, but we are focusing our attention on programming the shell rather than using it interactively.

You can find tips for customizing your interactive environment, including an example of how to use the KEYBD trap, at the companion website for this book, located at:

![](img/694fa9f0320e707804a4c650b96a09b4_552_0.png)

```
http://www.php.net/phpinteractive/
```

## 11.3.2 USE THE DEBUG TRAP

We will end this lab with an introduction to the shell's debugging features. For the small pieces of code we have been using to introduce the shell's features, you really don't need to use these features, but as you progress to larger and larger scripts and functions, you will find them invaluable.

Before we look at the DEBUG trap condition, we need to introduce the debug trap option that is always available to you. Enter the following commands in a script named tt3:

```
# trap-test 3
set -x
print This is the first command in this script
print This is the second command in this script
print This is the last command in this script > /dev/null
```

- a) What happened when you executed tt3?

Now create another script named tt4 that looks like the following:

```
# test-trap 4
function showVars {
print Variable values are: X=$X Y=$Y Z=$Z
}
trap showVars DEBUG
nX=abc Y=cba Z=bac
X=hello
Y=greetings!
Z=Farewell
```

- b) What happened when you executed tt4?

As you might guess, you can combine the shell's xtrace option with the DEBUG trap condition to see the commands being executed, as well as whatever debugging information you want to display with your trap handler.

## LAB 11.3 ANSWERS

![](img/694fa9f0320e707804a4c650b96a09b4_554_0.png)

This section gives you some suggested answers to the questions in LAB 11.3, with discussion related to those answers. Your answers may vary, but the most important thing is whether or not your answer works. Use this discussion to analyze differences between your answers and those presented here.

If you have alternative answers to the questions in this exercise, you are encouraged to post your answers and to discuss them at the companion web site for this book, located at:

http://www.phpptr.com/phpptrinteractive/

## 11.3.1 ANSWERS

- a) What was displayed when you ran the kill command?
Answer: Your interaction should look like the following:
```
[11035]: tt1 &
[1] 328
[11036]: kill -INT %1           tt1 &
[1] +
[11037]:
```
Line 11035 starts the tt1 command running in the background, then the kill command sends an INT signal to the job, causing it to terminate immediately, just as it was running in the foreground and you pressed Ctrl-C. Note that the program does not print its “Normal Termination” message.

- b) What does delivering these three types of signals do when they are delivered to a process?
Answer: Your interaction should look like the following:

```
[11037]: tt1 &
[1] 281
[11038]: kill -USR1 %1
[1] + User 1 tt1 &
[11039]: tt1 &
[1] 328
[11040]: kill -HUP %1
[11041]: tt1 &
[1] 349
[11042]: kill -CHLD %1
[11043]: /home/user/bin/tt1 Completed Normally
```
On line 11043, the prompt string was printed, then after 30 seconds, the “Completed Normally” message printed, leaving the cursor at the beginning of the line. When I pressed the Enter key, the last two lines printed.
```
[1] + tt1
[11043]:
```
The USR1 and HUP signals cause the program to terminate abruptly (without printing its “Normal Termination” message). In addition, the shell displays the “full name” of the signal that caused the job to terminate, telling that the job is finished. The HUP signal was originally designed to tell a program when a user’s dial connection has been lost (“hangup”) but now is often used to tell long-running programs that they should reinitialize. USR1 and USR2 signals are provided for any use you might make of. However, unless you create a trap handler for these or other signal types, the default behavior is to terminate the process which they are sent.

The CHLD signal is an example of a signal that, by default, does not cause the process receiving it to be terminated. As the interaction with tt on line 11042 shows, sending this signal has no effect on the program, which continues to run and finally prints its “Normal Completion” message. This signal is automatically delivered to a process any time one of its child processes terminates. For example, if you run a program in the background, your interactive shell receives this signal when the job finishes. Internally, that’s how the shell knows when it is time to print its “Done” message for the job.

- c) What did you observe?
Answer: Your interaction should look like the following:

```
[11043]: tt1 &
[1] 282
[11044]: kill -STOP %1
[1] + Stopped (SIGSTOP) tt1 &
[11045]: kill -CONT %1
[11046]: /home/user/bin/tt1 Completed Normally
[1] + tt1
[11046]:
```
The sequence of events here was basically the same as in the previous example. The difference is that the total time between lines 11043 and 11046 (the one above) was 30 seconds, the time I waited between entering lines 11044 and 11045.

The range of features implemented using UNIX signals is broad. This example shows that the STOP and CONT (continue) signals, as their names imply, start and stop a process execution. We'll concentrate on the ones that are most useful in constructing shell scripts here.

- d) What happens if you press Ctrl-C in response to the shell's command prompt?
Answer: You get another prompt string.

The point of mentioning this is that according to normal UNIX signal processing, pressing Ctrl-C while the shell is executing its code to read a command line from you should cause the shell process to terminate. Clearly, there is some way to override the shell's default behavior, and that's where the shell's trap command comes in. The shell establishes the equivalent of what we are about to look for itself by making machine-language calls to the operating system to control how signals are handled.

- e) What happened when you pressed Ctrl-C?
Answer: Your interaction should look like the following:

```
[11046]: trap "print INT occurred."
[11047]: INT occurred.
[11048]: INT occurred.
```

![](img/694fa9f0320e707804a4c650b96a09b4_556_0.png)

```
[11048]: helloINT occurred.
[11048]:
```
Here we used the trap command to establish a trap handler that prints "INT occurred" whenever the INT signal is delivered to our interactive shell process. Normally, you will do this sort of thing inside a script, as you will see below, but the trap command can be used at any level of your session.

On line 11048 I typed "hello" before pressing Ctrl-C, and that partially completed command line was discarded by the shell, and it reissued the prompt string for command 11048.

- f) Does the trap handler affect signal handling for the script?
Answer: Your interaction should look the same as your interaction for Question a. Enter the trap command at the command prompt has no effect on signal processing for a command that runs as a subprocess.

If a process wants to manage signals it has to do it itself. The way in which signals are handled in one process does not affect the way they are handled by other processes. (If you are familiar with the UNIX systems' programming, note that this is different from the behavior of the fork() system call.)

- g) What did the three trap commands do?
Answer: The first and last ones print a list of trap handlers that are set. The middle one clears the trap handler for INT

Your interaction should look something like this:

```
[11048]: trap
trap - 'print INT occurred.' INT
trap - 'eval "${Keytable[${sh.edchar}]}\' KEYBD
[11049]: trap - INT
[11050]: trap
trap - 'eval "${Keytable[${sh.edchar}]}\' KEYBD
[11051]:
```
Line 11048 shows that I had two trap handlers set when I issued the trap command, the one for INT that we entered earlier in this exercise, plus one for KEYBD that was set when I logged into the system. Entering the
