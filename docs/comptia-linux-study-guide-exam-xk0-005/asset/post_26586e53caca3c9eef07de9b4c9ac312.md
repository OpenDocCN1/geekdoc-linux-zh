
Explain the type of data you can access from within a shell script. The Bash shell provides access to environment variables, which contain information about the shell environment the script is running in. You can obtain information about the system as well as the user account that's running the shell script. The shell script also has access to positional variables, which allow you to pass data to the shell script from the command line when you run the shell script.

Describe how you can manipulate output data from a command before you use it in another command within a shell script. Command substitution allows you to redirect the output of a command to a user variable in your shell script. You can then use standard Linux text processing commands to manipulate the data, such as sort it or extract data records from it, before redirecting the variable data to another command.

Describe how the Bash shell performs mathematical operations. The Bash shell uses the `$[ ]` symbol to define mathematical equations to process. The Bash shell can only perform integer math, so this capability is somewhat limited.

Explain the different methods for implementing logic within a Bash shell script. The Bash shell supports both `if` statements and the `case` statement. They both allow you to perform a test on a numerical value, a string value, or a file and then run a block of commands based on the outcome of the test.

## Review Questions

1. What character or characters make up the shebang used in Linux to define the shell used for a shell script?
   - A. `>>`
   - B. `#!`
   - C. `|`
   - D. `>`
   - E. `2>`

2. Henry needs to store the output from his script into a new log file that he can read later. What character or characters should he use to do that?
   - A. `>>`
   - B. `#!`
   - C. `|`
   - D. `>`
   - E. `2>`

3. Jasmine has created a new Bash shell script and wants to run it from the command line. What `chmod` permissions should she assign to the file to run it as a shell script?
   - A. 644
   - B. `u+r`
   - C. `u+x`
   - D. `u+w`
   - E. `u=wr`

4. What environment variable contains the username of the user who started the shell?
   - A. `$USER`
   - B. `$UID`
   - C. `$HOME`
   - D. `$BASH`
   - E. `$1`

5. Zuri is writing a Bash shell script and needs to assign a number to a variable. How should he do that?
   - A. `var1=$(10)`
   - B. `var1 = 10`
   - C. `var1=10`
   - D. `var1="10"`
   - E. `var1=`10`

6. Cameron is writing a Bash shell script and needs to test if a file exists and that it's a file. What line of code should he write to do that?
   - A. `if [ -e file ]`
   - B. `if [ -f file ]`
   - C. `if [ -d file ]`
   - D. `if [ -x file ]`
   - E. `if [ -w file ]`

7. What character or combination of characters do you use to redirect the output of one command to another command?
   - A. `>>`
   - B. `#!`
   - C. `|`
   - D. `>`
   - E. `2>`

8. Christina is creating a Bash shell script and wants to make the script return a value of 2 if it fails. What statement should she add to do that?
   - A. `#!`
   - B. `$?`
   - C. `$1`
   - D. `exit`
   - E. `while`

9. What command should you use to perform a command substitution to assign the output of a command to a variable in your shell script?
   - A. `>`
   - B. `>>`
   - C. `$[ ]`
   - D. `|`
   - E. `$()`

10. What command should you use to perform a mathematical operation in your shell script?
    - A. `>`
    - B. `>>`
    - C. `$[ ]`
    - D. `|`
    - E. `$()`

# Chapter 26

# Automating Jobs

![](img/c0a399aca0d18f8822d714ad0a173123_792_0.png)

Objective 1.4: Given a scenario, configure and use the appropriate processes and services.

![](img/c0a399aca0d18f8822d714ad0a173123_793_0.png)

As you begin building shell scripts, you’ll probably start to wonder how to run and control them on your Linux system. So far in this book, we’ve only run commands and scripts directly from the command-line interface in real-time mode. This isn’t the only way to run scripts in Linux. There are quite a few other options available for running your shell scripts on Linux systems. This chapter examines different ways you can use to get your scripts started. Also, sometimes you might run into the problem of a script that gets stuck in a loop and you need to figure out how to get it to stop without having to turn off your Linux system. This chapter also examines the different ways you can control how and when your shell script runs on your system.

## Running Scripts in Background Mode

There are times when running a shell script directly from the command-line interface is inconvenient. Some scripts can take a long time to process, and you may not want to tie up the command-line interface waiting. While the script is running, you can’t do anything else in your terminal session. Fortunately, there’s a simple solution to that problem. The following sections describe how to run your scripts in background mode on your Linux system.

### Running in the Background

Running a shell script in background mode is a fairly easy thing to do. To run a shell script in background mode from the command-line interface, just place an ampersand symbol after the command:

```text
$ ./test1.sh &
[1] 19555
$ This is a test program
Loop #1
Loop #2

$ ls -l
total 8
-rwxr--r-- 1 rich rich 219 Feb 26 19:27 test1.sh
$ Loop #3
```

When you place the ampersand symbol after a command, it separates the command from the Bash shell and runs it as a separate background process on the system. The first thing that displays is the line `[1] 19555`.

The number in the square brackets is the *job number* the shell assigns to the background process. The shell assigns each process started a unique job number. The next number is the process ID (PID) the Linux system itself assigns to the process. So every process running in a shell has a unique job number, and every process running on the Linux system has a unique PID.

As soon as the system displays these items, a new command-line interface prompt appears. You are returned to the shell, and the command you executed runs safely in background mode.

At this point, you can enter new commands at the prompt (as shown in the example). However, while the background process is still running, it still uses your terminal monitor for output messages. You'll notice from the example that the output from the `test1.sh` script appears in the output intermixed with any other commands that are run from the shell.

When the background process finishes, it displays a message on the terminal:

`[1]+ Done ./test1.sh`

This shows the job number and the status of the job (Done), along with the command used to start the job.

### Running Multiple Background Jobs

You can start any number of background jobs at the same time from the command-line prompt:

```text
$ ./test1.sh &
[1] 19582
$ This is the test1 program output
Test 1 Loop #1 output
$ ./test2.sh &
[2] 19597
$ This is the test2 program output
Test 2 Loop #1 output
$ ./test3.sh &
[3] 19612
$ This is the test3 program output
Test 3 Loop #1 output
Test 1 Loop #2 output
Test 2 Loop #2 output
Test 3 Loop #2 output
```

Each time you start a new job, the shell assigns it a new job number, and the Linux system assigns it a new PID. You can see that all of the scripts are running by using the `ps` command:

```text
$ ps au
USER     PID %CPU %MEM   VSZ   RSS TTY      STAT START     TIME COMMAND
rich 19498 0.0 1.2 2688 1628 pts/0 S 11:38 0:00 -bash
rich 19582 0.0 0.9 2276 1180 pts/0 S 11:55 0:00 /bin/bash ./test3.sh
rich 19597 0.1 0.9 2276 1180 pts/0 S 11:55 0:00 /bin/bash ./test2.sh
rich 19612 0.1 0.9 2276 1180 pts/0 S 11:55 0:00 /bin/bash ./test1.sh
rich 19639 0.0 0.4 1564 552  pts/0 S 11:56 0:00 sleep 10
rich 19640 0.0 0.4 1564 552  pts/0 S 11:56 0:00 sleep 10
rich 19641 0.0 0.4 1564 552  pts/0 S 11:56 0:00 sleep 10
rich 19642 0.0 0.5 2588 744  pts/0 R 11:56 0:00 ps au
$
```

Each of the background processes you start appears in the `ps` command output listing of running processes. If all of the processes display output in your terminal session, things can get pretty messy pretty quickly. Fortunately, there's a simple way to solve that problem, which we'll discuss in the next section.

**WARNING** You need to be careful when using background processes from a terminal session. Notice in the output from the `ps` command that each of the background processes is tied to the terminal session (`pts/0`) terminal. If the terminal session exits, the background process also exits. Some terminal emulators warn you if you have any running background processes associated with the terminal, while others don't. If you want your script to continue running in background mode after you've logged off the console, there's something else you need to do. The next section discusses that process.

### Running Scripts without a Console

There will be times when you want to start a shell script from a terminal session and then let the script run in background mode until it finishes, even if you exit the terminal session. You can do this by using the `nohup` command.

The `nohup` command runs another command blocking any `SIGHUP` signals that are sent to the process. This prevents the process from exiting when you exit your terminal session (`nohup` is short for "no hangup").
