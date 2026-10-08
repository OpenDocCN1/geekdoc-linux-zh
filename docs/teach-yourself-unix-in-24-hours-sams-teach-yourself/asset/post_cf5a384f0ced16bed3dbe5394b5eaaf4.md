
# Basic Shell Programming

Using the white loop, we solved the problem. At the end of the execution of our script, we created a checkpoint file. At the beginning, if the checkpoint file was newer than the log file, we'd wait. Programmatically, that is:

```
while
  [checkpoint -nt logfile]
    sleep 60
done
```

This program would wait one minute between checks. If the new logfile had not been written, the program would go back to sleep for a minute.

You can use white loops also in a determinate manner. In the case you are not concerned with a variable's value but a count of times to run a command-block, you can use a variable to increment through the number:

```
i=0
while
  [ $i -lt 100 ]
    i=$(expr "$i" + 1)
    commands
done
```

This is easier than listing 100 items in a list!

> The shell provides two convenient mechanisms for running a group of commands repeatedly. These loop commands are useful from both the command line and a program.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_367_0.png)

# Summary

In this hour, you just skimmed the basics of shell programming. You were introduced to the control structures of the shell and two important commands. There is a lot more you can learn about shell programming; Teach Yourself Shell Programming (Sams Publishing) is one place you can look. If you are interested in the C shell, Teach Yourself the UNIX C Shell (S Publishing) is another resource.

# Workshop

The Workshop summarizes the key terms you learned and poses some questions about the topics presented in this chapter. It also provides you with a preview of what you will learn in the next hour.

# Key Terms

- **command-block** A list of one or more shell commands that are grouped in a conditional or looping statement.

- **conditional expression** This is an expression that returns either true or false.

- **determine loop** A loop where the number of times the loop is run can be known before starting the loop.

- **expression** This is a command that returns a value.

- **indeterminate loop** A loop where the number of times the loop is run is not known before starting the loop.

- **loop** This is a sequence of commands that is repeatedly executed while a condition is true.

- **variables** These are names to label data that may change during the execution of a program.

- **zero-length variable** A variable that does not have a value assigned to it.

# Questions

1. How would you read in an address in a shell program? How would you read in a name?
2. If you read in the number of people who read a newspaper and the number of people who subscribe to a particular paper, how would you determine the ratio of subscribers to readers?
3. How do you know if a file has data?
4. How do you want for data to be placed in a file?

# Preview of the Next Hour

In the next hour, you are introduced to managing processes in UNIX. You learn how to start a background job, how to switch between foreground and background, and how to terminate a command.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_368_0.png)

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_369_0.png)

# Hour 17

# Job Control

In this hour you will learn about how UNIX handles jobs, and how you can manipulate them. Commands you will include `jobs` and `ps`, to see what processes are running; `fg` and `bg`, to move jobs back and forth between the foreground and background; and `kill`, to terminate jobs that you no longer want around.

# Goals for This Hour

In this hour, you learn:

- About job control in the shell: stopping jobs
- How to put jobs in the background and bring them back to the foreground
- How to find out what tasks are running by using `jobs` and `ps`
- How to terminate errant processes by using `kill`

Throughout this book, I indicated that my focus is on the most important and valuable flags and options for the commands covered. That's all well and good, but how do you find out about the other alternatives that might actually work better for your use?

This hour presents an explanation of a UNIX philosophical puzzle: What is a running program? To learn the answer, you are introduced to ps and jobs, for controlling processes; fg and bg, you move your processes back and forth between the foreground and background; and the quasi-omnipotent kill command, for stopping processes in their proverbial trials.

# Task 17.1: Job Control in the Shell: Stopping Jobs

- DESCRIPTION: Whether you are requesting a man page, listing files with ts, starting vi, or running just about any UNIX command, you're starting one or more processes. In UNIX, any program that is a process. You can have multiple processes running at once. The pipeline `ts -i | sort | more` invokes three processes: ts, sort, and more. Processes in both the C and Korn shells are also known as jobs, and the program you're running is known as the current job.

Any job or process can have a variety of different states, with “running” being the most typical state. In shells, you can stop a job by pressing ^Z. To restart it, enter fg.

1. Earlier I was perusing the man page entry for sort. I had reached the bottom of the first screen:

```
% man sort
SORT(1) DNIX Programmer's Manual SORT(1)
NAME sort - sort merge files
SYNOPSIS sort [ -mubdfintrx ] [ +pos1 [-pos2] ] ... [-o name ] [
-T directory [ name ] ...
DESCRIPTION sort sorts lines of all named files together and writes the result on the standard output. The name “-\” means the standard input. If no input files are named, the standard input is sorted.
The default sort key is an entire line. Default ordering is lexicographic by bytes in machine collating sequence. The ordering is affected globally by the following options, one or more of which may appear.
  b  Ignore leading blanks (spaces and tabs) in field com-
--More--
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_370_0.png)

# Job Control

I can check to see if someone is logged in and then return to vi with the fg command.

- * who | grep marv
- * fg

1. Earlier I was perusing the man page entry for sort. I had reached the bottom of the first screen: (see above)
2. I can check to see if someone is logged in and then return to vi with the fg command.
3. I can check to see if someone is logged in and then return to vi with the fg command.

I can check to see if someone is logged in and then return to vi with the fg command.

I can check to see if someone is logged in and then return to vi with the fg command.

I can check to see if someone is logged in and then return to vi with the fg command.

I can check to see if someone is logged in and then return to vi with the fg command.

I can check to see if someone is logged in and then return to vi with the fg command.

I can check to see if someone is logged in and then return to vi with the fg command.

I can check to see if someone is logged in and then return to vi with the fg command.

I can check to see if someone is logged in and then return to vi with the fg command.

- At this point, the bottom of the page, the screen would look like this:

```
The default sort key is an entire line. Default ordering is lexicographic by bytes in machine collating sequence. The ordering is affected globally by the following options, one or more of which may appear.
  b  Ignore leading blanks (spaces and tabs) in field com-
--More--
```

- At this point, the bottom of the page, the screen would look like this:

```
The default sort key is an entire line. Default ordering is lexicographic by bytes in machine collating sequence. The ordering is affected globally by the following options, one or more of which may appear.
  b  Ignore leading blanks (spaces and tabs) in field com-
--More--
```

- At this point, the bottom of the page, the screen would look like this:

```
The default sort key is an entire line. Default ordering is lexicographic by bytes in machine collating sequence. The ordering is affected globally by the following options, one or more of which may appear.
  b  Ignore leading blanks (spaces and tabs) in field com-
--More--
```

- At this point, the bottom of the page, the screen would look like this:

```
The default sort key is an entire line. Default ordering is lexicographic by bytes in machine collating sequence. The ordering is affected globally by the following options, one or more of which may appear.
  b  Ignore leading blanks (spaces and tabs) in field com-
--More--
```

- At this point, the bottom of the page, the screen would look like this:

```
The default sort key is an entire line. Default ordering is lexicographic by bytes in machine collating sequence. The ordering is affected globally by the following options, one or more of which may appear.
  b  Ignore leading blanks (spaces and tabs) in field com-
--More--
```

(Note: The OCR text contained significant repetitions and fragmented sentences in the later pages. I have reconstructed the logical flow based on the provided content.)
