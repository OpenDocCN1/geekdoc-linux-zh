
## ### Listing 1.4: Script Demonstrating Assignment and Use of Variables

For instance, consider Listing 1.4, which displays the current IP address of the computer on which it runs. This script uses the variable $ip, which is extracted from the output of `ifconfig` using `grep` and `cut` commands. (The trailing backslash on the second line of the script indicates that the following line is a continuation of the preceding line.) When assigning a value to a variable from the output of a command, that command should be enclosed in back-quote characters (`'`), which appear on the same key as the tilde (`~`) on most keyboards. These are *not* ordinary single quotes, which appear on the same key as the regular quote character (`'`) on most keyboards.

```shell
#!/bin/sh
ip=`ifconfig eth0 | grep inet | cut -f 2 -d " ' ")`
echo 'Your IP address is $ip'
```

Listing 1.4 relies on the networking command `ifconfig`, which is described in more detail in Phase 6. You can type `ifconfig` by itself to see what its output includes. The second line of Listing 1.4 uses `grep` and `cut` to isolate the IP address from the rest of the `ifconfig` output.

Scripts like Listing 1.4, which obtain information from running one or more commands, are useful in configuring features that rely on system-specific information or information that varies with time. You might use a similar approach to obtain the current hostname (using the `hostname` command), the current time (using `date`), the total time the computer's been running (using `uptime`), free disk space (using `df`), and so on. When combined with conditional expressions (described shortly), variables become even more powerful because then your script can perform one action when one condition is met and another in some other case. For instance, a script that installs software could check free disk space and abort the installation if there's not enough disk space available.

One special type of variable was mentioned earlier in this chapter: environment variables. Environment variables are assigned and accessed just like shell script variables. The difference is that the script or command that sets an environment variable uses the `export` command to make the value of the variable accessible to programs launched from the shell or shell script that made the assignment. Environment variables are most often set in shell startup scripts, but the scripts you use can access them. For instance, if your script calls X programs, it might check for the presence of a valid $DISPLAY environment variable and abort if it finds this variable isn't set. By convention, environment variable names are all uppercase, whereas non-environment shell script variables are all lowercase or mixed case.

## ## Using Conditional Expressions

Scripting languages support several types of *conditional expressions*. These enable a script to perform one of several actions contingent on some condition—typically the value of a variable. One common command that uses conditional expressions is `if`, which allows the system to take one of two actions depending on whether some condition is true. The `if` keyword's conditional expression appears in brackets after the `if` keyword and can take many forms. For instance, `-f` *file* is true if *file* exists and is a regular file; `-s` *file* is true if *file* exists and has a size greater than 0; and `string1 = string2` is true if the two strings have the same values.

To better understand the use of conditionals, consider the following code fragment:

```
if [ -s /tmp/tmpstuff ]
then
	echo "/tmp/tmpstuff found; aborting!"
	exit
fi
```

This fragment causes the script to exit if the file /tmp/tmpstuff is present. The then keyword marks the beginning of a series of lines that execute only if the conditional is true, and fi (if backwards) marks the end of the if block. Such code might be useful if the script creates and then later deletes this file, since its presence indicates that a previous run of the script didn't succeed or is still working.

An alternative form for a conditional expression uses the test keyword rather than square brackets around the conditional:

```
if test -s /tmp/tmpstuff
```

You can also test a command's return value by using the command as the condition:

```
if [ command ]
then
	additional-commands
fi
```

In this example, the additional-commands will be run only if command completes successfully. If command returns an error code, the additional-commands won't be run.

Conditional expressions are sometimes used in loops as well. Loops are structures that tell the script to perform the same task repeatedly until some condition is met (or until some condition is no longer met). For instance, Listing 1.5 shows a loop that plays all the .wav audio files in a directory.

## **Listing 1.5:** A Script That Executes a Command on Every Matching File in a Directory

```
#!/bin/bash
for d in `ls *.wav` ;
do play $d ;
done
```

The for loop as used here executes once for every item in the list generated by ls *.wav. Each of those items (filenames) is assigned in turn to the $d variable and so is passed to the play command.

Another form of loop is the while loop, which executes for as long as its condition is true. The basic type of this loop type is like this:

```
while [ condition ]
do
    commands
done
```

The until loop is similar in form, but it continues execution for as long as its condition is false—that is, until the condition becomes true.

## ## Using Functions

A function is a part of a script that performs a specific sub-task and that can be called by name from other parts of the script. Functions are defined by placing parentheses after the function name and enclosing the lines that make up the function within curly braces:

```
myfn() {
    commands
}
```

The keyword function may optionally precede the function name. In either event, the function is called by name as if it were an ordinary internal or external command.

Functions are very useful in helping to create modular scripts. For instance, if your script needs to perform half a dozen distinct computations, you might place each computation in a function and then call them all in sequence. Listing 1.6 demonstrates the use of functions in a simple program that copies a file but aborts with an error message if the target file already exists. This script accepts a target and a destination filename and must pass those filenames to the functions.

## **Listing 1.6: A Script Demonstrating the Use of Functions**

```bash
#!/bin/bash

doit() {
    cp $1 $2
}

function check() {
    if [ -s $2 ]
    then
        echo 'Target file exists! Exiting!'
        exit
    fi
}

check $1 $2
doit $1 $2
```

If you enter Listing 1.6 and call it **safercp**, you might use it like this, assuming the file `original.txt` exists and `dest.txt` does not:

```
$ ./safercp original.txt dest.txt
$ ./safercp original.txt dest.txt
Target file exists! Exiting!
```

The first run of the command succeeded because `dest.txt` did not exist. When the command was run a second time, though, the destination file did exist, so the program terminated with the error message.

Note that the functions are not run directly and in the order in which they appear in the script. They’re run only when called in the main body of the script (which in Listing 1.6 consists of just two lines, each corresponding to one function call).

## # Criteria for Completion

To complete this task, you must have created five scripts to perform the five tasks outlined earlier. I recommend that you try some simple variants on these tasks so that you create scripts that perform other tasks—for instance, you might modify Listing 1.5 so that it displays graphics files in a directory rather than plays audio files.

# Phase 2: Managing Hardware and the Kernel

![](img/f430a19bdf014c43ad7c2d594afd5b21_79_0.png)

![](img/f430a19bdf014c43ad7c2d594afd5b21_80_0.png)

Linux software requires hardware to be useful, and managing that hardware requires its own set of street smarts. Phase 2 focuses on this topic, beginning with low-level hardware configuration in the Basic Input/Output System (BIOS) and resolving hardware conflicts. This phase then moves on to Linux utilities for identifying and configuring your hardware, and particularly the Universal Serial Bus (USB), hard disk, and power management subsystems. The kernel is a critical part of the hardware equation, so this phase looks at configuring and compiling the kernel. Finally, this phase concludes with three tasks related to the X Window System (or X for short), Linux's GUI environment.

![](img/f430a19bdf014c43ad7c2d594afd5b21_80_1.png)

> This phase maps to portions of the ComptIA Linux+ objective 6 and to portions of the LPIC objectives 101, 105, and 110.

## # Task 2.1: Set BIOS Options

The BIOS is a low-level set of software functions that were designed in the 1980s to simplify the creation of OSs such as Microsoft's original Disk Operating System (DOS). The BIOS would handle functions such as keyboard input, screen output, and even low-level disk input/output. Over the years, as computers and OSs grew in complexity, the BIOS became less and less important in handling these I/O tasks. Nonetheless, the BIOS remains important because it controls the computer's initial boot sequence and hardware initialization. If the BIOS doesn't know your hard disk exists, or if it configures your hard disk incorrectly, the computer won't boot. Improper BIOS settings can also cause unreliable operation, clocks that are set incorrectly, an inability to access on-board hardware devices, and other problems. Thus, care should be taken when setting BIOS options, and checking these options is a wise precaution whenever putting a new computer into operation.

### ## Scenario

You've just assembled a new computer from parts. Before booting it and attempting to install Linux, you want to check its BIOS options to see that they're sensible. You should pay particular attention to the disk options and to the system clock setting. When assembling a computer from parts, you are responsible for setting basic BIOS options. When you buy a preassembled computer, in theory the BIOS should be set correctly; however, errors do sometimes appear, so checking the BIOS options is a sensible precaution. The clock is likely to need adjustment even with a store-bought computer.
