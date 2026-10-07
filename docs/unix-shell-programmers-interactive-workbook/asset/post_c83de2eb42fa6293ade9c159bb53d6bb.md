
# Chapter 11: I/O and TRAP Processing 519

c) What would have happened if you had created a function with these commands and run it, or had run the commands from the shell prompt, or dotted the script?
Answer: You would have been logged out from your KornShell session!

In all three situations listed, the exec command would have caused your interactive shell process to be replaced by the ls command, and when it terminated, you would have been logged out. When it finishes generating its output, the ls command internally does the equivalent of the shell's exit command, logging you off the system.

Self-Review Question 1 shows a somewhat more realistic way that you might make use of the exec command in a script.

## 11.2.2 ANSWERS

```
exec 3 file1
exec 4> file2
while read -ru3
do
    print -u4 "$REPLY"
done
exec 3<&-
exec 4<&-
```

a) What do the first two exec commands do?
Answer: They open file1 for reading and file2 for writing.

Although these look like commands to redirect I/O for the exec command, they do it for the program that runs exec. That is, if you run commands from the command line (*from an interactive shell*), they open fds 3 and 4 for the interactive shell you are running, but if you do them from inside a script, they take effect for the code inside the script. Doting a script or running a function with these commands in them would have the same effect as entering execs from the command line.

## 520 Lab 11.2: The exec Command

Inside a script the standard I/O fds (0, 1, and 2) will be copies of those in effect in your interactive shell, but all fds greater than number 2 will be closed. However, all the interactive shell's fds will still be open when control returns to it.

![](img/694fa9f0320e707804a4c650b96a09b4_539_0.png)

- b) What do the last two lines do?
Answer: They close the two fds that were opened by the first command lines.

LAB 11.2

Closing files when you are finished with them is a good thing to do, although failing to do so will generally not have much effect on your life. Doing so prevents your program from doing more reads or prints using the fd until it is opened again. You saw that m&n is the syntax for connecting fd m to the same file or device as fd n in Lab 2.3, "Redirect Input and Output." Now you can see that using a dash (&-) for n means that fd m gets closed and cannot be used for I/O.

- c) What does the -ru3 on the read command accomplish?
Answer: It makes the command read from the first input file.

The -r part says to treat backslashes ( \ ) at the ends of lines as normal characters rather than line continuation. The u3 part says to read from fd 3. You could have typed this as -r -u3, if you prefer. It's always a good idea to use -r when you read from a file; line continuation is really designed for interactive use.

![](img/694fa9f0320e707804a4c650b96a09b4_539_1.png)

- d) What do the quotes around REPLY accomplish?
Answer: They preserve the spacing in the lines being printed.

The IFS variable was set to the empty string before entering the loop so that no token splitting is done by the read commands inside the loop, and the print commands used to prevent the spacing from being lost in the output. The value of IFS is restored to its default value after copying, so that the read command asking for the next file name will do token splitting as required. (Wait, the text says "token splitting as required").

# Chapter 11: I/O and TRAP Processing 521

Don't try to use these commands to copy anything but text files. Reading and printing non-ASCII characters will almost lead to unpredictable results.

![](img/694fa9f0320e707804a4c650b96a09b4_540_0.png)

- e) What is inefficient about the second version compared with the first?
Answer: In the second version, shell commands are executed for every line of the input file, whereas the cp command executes no commands.

Shell commands, even built-ins such as read and print, almost always take longer to execute than the equivalent machine instructions inside a binary. The reason for using a shell program to read a file is that you can do something special with its contents. If you can, use the external commands that came with your system, such as cp, mv, grep, sort, uniq, head, and tail.

![](img/694fa9f0320e707804a4c650b96a09b4_540_1.png)

- f) What are four things the user could use to cause this script to stop?
Answer: q, Ctrl-D, or Ctrl-C.

The program checks whether the user types a q on the command line and exits the outer while loop. Because the outer while loop continues as long as the read command returns true, the user can press Ctrl-D (or Ctrl-Z on DOS/Windows systems, whatever the user has set as the end-file character) to indicate end of input. Finally, if the user types Ctrl-C (or whatever the interrupt character is on the system), the program will terminate abruptly.

- g) What is the purpose of the print command at the end of the script?
Answer: It positions the cursor properly in the case the user presses Ctrl-D. Because the cursor does not move to the start of a new line in this case, the script does a print command if execution gets past the end of the outer while loop.

## 522 Lab 11.2: The exec Command

h) What happens if the user enters the name of a nonexistent file for either of the files to shuffle?
Answer: The shell will print an error message, as in the following interaction:

```
shuffle
Name two files that you want to shuffle: x y
shuffle: x: cannot open such file or directory
```

In this example, there was no file x in my working directory, the error message was printed as soon as the exec 3< command was reached, and the script terminated immediately. The exec 4< command was not reached in this case (it would have failed too, I didn't have a file y), nor were any of the other commands in the script. So "name of a nonexistent file" would have been the thing that you mentioned in your answer f.

- i) What happens if the user enters the name of a file that already exists as the output file?
Answer: It would have been overwritten.

Even if the user had the interactive shell's noclobber option before running the script, the file would have been overwritten because the shell resets almost all of its options whenever it starts a script. The exceptions are the emacs and vi options, so the user can use his/her preferences for command line editing when responding to read commands, and the trackall option which means the shell will remember where it finds external commands while running the script.

![](img/694fa9f0320e707804a4c650b96a09b4_541_0.png)

Be aware of this feature of the shell when writing scripts. Users don't like to be surprised. The first Test Your Thinking question at the end of this chapter deals with this matter further.

i) What happens if the user enters the name of one of the input files as the name of the output file? (Hint: Don't try this on a file that you care keeping!)
Answer: The file gets truncated to zero bytes.

```
if grep "^${USER?:"Unable to determine user"}" /etc/passwd > /dev/null
then print "You have a local account on this system."
else print "You have a network account for accessing this system."
fi
```

Lab 11.2: The exec Command

b) What does this if statement do, and why is the output of the grep command redirected to /dev/null?
Answer: It uses grep to look for the user's name in the /etc/password file, discarding the output of the grep command, then prints a message based on the value of the return code from the grep command.

The basic idea is here that we want to use the grep command to see whether a file contains a string, but we are not interested in seeing the line that grep prints if it finds the string, so we throw by redirecting the output of the grep command to /dev/null. The grep command will have an exit code of true (0) if it finds the string, and false (1) if it does not, so the if statement prints the message if the user's name is found in the local /etc/passwd file, and the second message if not.

```
print "Hey, pay attention to me!" > /dev/tty
insist > /dev/null 2>&1
```

b) What does the I/O redirection on the command line do?
Answer: It forces the standard output from the script, both stdout and stderr, to be discarded.

The insist command line redirects both stdout and stderr to /dev/null, which means that the user wants to discard all output that would normally be written to the screen.

c) Did the "pay attention" message print on the screen?
Answer: Yes, it did.

The script still manages to show its message because it writes to the device directly without using an fd.

img/694fa9f0320e707804a4c650b96a09b4_543_0.png)

Reading and writing /dev/tty can be a useful capability, but don't use it because you think you know better than the user the user "should" do. If the user redirects all output away from the screen, your program should normally honor that setting.

Most often, this feature is used when you temporarily close one of the standard I/O fds inside a script, then want to restore the standard I/O.
