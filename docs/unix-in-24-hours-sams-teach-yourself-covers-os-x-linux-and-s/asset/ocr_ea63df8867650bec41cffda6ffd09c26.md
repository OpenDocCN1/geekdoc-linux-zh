```
Whenever any reference (however slight) is made here to the condition of the Danish people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add something to the popular and picturesque means of "dickens.note" 28 lines, 1123 characters
```

Processes and jobs in Unix have many aspects, particularly regarding the level of control offered by the shell. The rest of this hour explains how to exploit these capabilities to make your work easier and faster.

# Task 15.2: Foreground/Background and Unix Programs

Now that you know how to suspend programs (freezing them in their tracks), it’s time to learn how to allow them to keep running in the background (by using the bg command) while you’re doing something else and how to have programs start in the background by using the & suffix.

In the first hour, you learned that one of the distinguishing characteristics of Unix is that it’s a true multitasking operating system. It is capable of running hundreds of programs at the same time. This applies to any program from a simple command-line utility to a full-screen persistent application. If you want to save a couple of man pages to a file, for example, you can run those processes in the background while you are working on something else.

Once a job is stopped, you can enter fg to restart it as the program you’re working with. (The fg command takes its name from foreground, which refers to the program that your display and keyboard are working with.) If the process will continue without any output to the screen and without any requirement for input, you can use bg to move it into the background, where it runs until it is done. If the program needs to write to the screen or read from the keyboard, the system will stop its execution automatically and inform you. You then can use fg to bring the program into the foreground to continue running.

# Tip

If you find that running background jobs are still writing information to your screen, try using the shell command stty tostop prior to starting the command as a solution.

You can also use job control to start multiple programs and then use the fg command, with the job ID as an argument, to start the job you want to work with. Not entering the job ID will bring the most recently stopped job back to the foreground. If your system takes a long time to start big applications (such as emacs or vi), this could save you lots of time.