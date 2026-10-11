# Appendix D

# Linux Programming Exercises

Now you actually must put your knowledge to use to solve the exercises in this appendix. But don't fear! This task is an open-book activity—and I provide the answers right after the question. You can peek if you want.

Note: I group the exercises by chapter, but not all the chapters have corresponding exercises.

# Chapter 3: Writing Your First Linux Program

+   1. How do you start the vi text editor?

Type vi, following it by the name of the file that you want to create or modify, as follows:

```
vi myfile
```

+   2. What is the first line in a bash shell program?

```
#!/bin/bash
```

+   3. What is the second instruction you want to give the computer in most programs that you write?

```
clear
```

This command clears the screen of characters that are left from the preceding program.

+   4. Write a program that displays the name Bob Smith on-screen.

```
#!/bin/bashecho "Bob Smith"
```

+   5. Make a program that you name myprogram into an executable program.

```
chmod 777 myprogram
```