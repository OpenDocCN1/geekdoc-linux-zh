
UNIX has several tools for other phases of a software life cycle, but a discussion of them is outside the scope of this textbook.

## QUESTIONS AND PROBLEMS

1. What are the differences between compiled and interpreted languages? Give three examples of each.

2. Give one application area each for assembly and high-level languages.

3. Write the steps that a compiler performs on a source program in order to produce an executable file. State the purpose of each step. Be precise.

4. What are the -o, -l, and -xO options of the cc command used for? Give an example command line for each and describe what it does.

5. Give the compiler commands to create an executable called prog from C source files myprog.c and misc.c. Assume that misc.c uses some functions in the math library. What is the purpose of each command?

6. What are the three steps of the program development process? What are the main tasks performed at each step? Write the names of UNIX tools that can be used for these tasks.

7. Give a shell command that can be used to determine the LOC in the program stored in the scheduler.c file.

8. Write advantages and disadvantages of automating the recompilation and relinking process by using the make utility, as opposed to manually doing this task.

9. Consider the following makefile and answer the questions that follow.

```
CC = cc
OPTIONS = -xO4 -o
OBJECTS = main.o stack.o misc.o
SOURCES = main.c stack.c misc.c
HEADERS = main.h stack.h misc.h
polish: main.c $(OBJECTS)
	$(CC) $(OPTIONS) power $(OBJECTS) -lm
main.o: main.c main.h misc.h
stack.o: stack.c stack.h misc.h
misc.o: misc.c misc.h
```

List the following:
a. Names of macros
b. Names of targets
c. Files that each target is dependent on
d. Commands for constructing the targets named in part (b)

10. For the makefile in Problem 9, give the dependency tree for the software.

11. What commands are executed for the main.o, stack.o, and misc.o targets? How do you know?

12. For the makefile in Problem 9, what happens if you run the make command on your system? Show the output of the command.

13. Use the nm command to determine the size of the select call in the socket library (/usr/lib/libsocket.a). What is the size of the code for the call?

14. Give the command line for determining the library that contains the function strcmp. What is the size of this function?

15. What would happen if you tried to check out the same file again using Git/GitHub? Why?

16. Create a three-branch repository of commits exactly like Figure 17.16. Use any number of text files that you modify between commits on the three branches. Keep the default name for the branch master, but name the other two branches test and dev, as seen in Figure 17.16.

17. Create a three-branch repository of commits exactly like Figure 17.17. Use any number of text files that you modify between commits on the three branches. Keep the default name for the branch master, but name the other two branches test and dev, as seen in Figure 17.17.

![](img/02e070097d401d3bf7de4bf1c470b267_818_0.png)

FIGURE 17.16 Sample three-branch repository of commits.

![](img/02e070097d401d3bf7de4bf1c470b267_818_1.png)

FIGURE 17.17 Sample three-branch repository of commits.

18. As an alternative to using git pull in Example 17.5 to obtain the source code for this book from the listed GitHub repository (https://github.com/bobk48/unix textbook3), use the git clone command, as shown in Example 17.4, from your home directory on your UNIX system. What will be the name of the repository directory created by Git on your local machine that contains the source code files?

19. Before doing this problem, go through all of the material in Chapter 24 on the Zettabyte File System, including the in-chapter exercises and problems. Then, in your own words, describe the differences and similarities between Git, GitHub, and ZFS. For example, the commands zfs snapshot and git commit are very similar. In what way do they differ? In your opinion, is it possible to use the commands zpool and zfs to achieve the same or similar results as using Git and GitHub? What other UNIX commands would be needed to augment the ZFS file system commands to attain results that are similar to Git and GitHub functions, commands, and capabilities?

20. The following code is meant to prompt you for integer input from the keyboard, read your input, and display it on the screen. The program compiles with one warning, but it doesn't work properly. Use the gdb utility to find the bugs in the program. What are they? Fix the bugs, recompile the program, and execute it to be sure that the corrected version works. Show the working version of the program.

```
#include <stdio.h>

#define PROMPT "Enter an integer: " void get_input (char *, int *);
int main ()
{
    int user_input;
    get_input(PROMPT, user_input);
    (void) printf("You entered: %d.\n", user_input);
}

void get_input(char *prompt, int *ival)
{
    (void) printf("%s", prompt);
    scanf ("%d", &ival);
}
```

21. What does the time sh command line do when executed under the C shell?

22. Give the command line to redirect the output of the /usr/bin/time polish command to a file called polish_output. Assume that you are using the Bourne shell.
