
The output shows that the original login -bash shell has a PID of 2393 and that script1, when executed, returned the date and a PID of 2413. This concept is very important to remember. In this case, PID 2413 is a child of PID 2393.

Figure 13.1 illustrates that the login shell called -bash opens another bash subshell to run script1, and the date command itself will run in yet another subshell. All of the subshells exist only for the time it takes to run their respective commands. Also, when they are finished, control is passed back to the login -bash shell, which has been asleep while the subshells performed their functions.

## Option 2: Invoking Scripts by Making Them Executable

When script1 is made to be executable on its own and then invoked, a bash subshell is invoked again by the login -bash shell to execute the shell script file (basically the same process as Option 1 when the bash command was used).

The only difference is—and this fact is probably obvious to you by now—that the shell script has been flagged as executable. Then you can execute the script directly, like such:

![](img/cae5c706c216875d12d4b7d28144cc71_425_0.png)

**Figure 13.1** Invoking shell scripts by using the bash command.

```
$ script1<Enter>
Wed Jul 25 15:07:51 MDT 2001
```

As illustrated in Figure 13.2, invoking script1 on its own in the login shell invokes another bash subshell that runs as a child to the login shell. When that subshell has finished executing the commands in the script1 file, it terminates and control is passed back to the parent login -bash shell.

### Example 13.7 Processes the Shell Script Invoked Itself

We will demonstrate this behavior in a manner identical to Option 1 (Example 13.6):

- Identify and echo the current shell's PID.
- Ask script1, as it is being executed, to echo back the PID of the shell in which it is actually being executed.

Using $ chmod 775<Enter>, Lady Molinera has now made script1 executable. Its long listing now looks like the following:

```
$ ls -l script1<Enter>
-rwxrwxr-x 1 molinera knights3 13 Jul 14 15:10 script1
```

Before running the script, she again displays the current shell's PID to demonstrate that it is different from the subshell in which the script will eventually execute:

```
$ echo $$<Enter>
2393
$ bash script1<Enter>
Wed Jul 25 14:35:59 MDT 2001
2443
```

This output shows that the original login -bash shell has a PID of 2393 and that script1, when executed, returned the date and a PID of 2443. Again, this concept is important to remember. PID 2443 is the child of PID 2393 this time.

Figure 13.2 illustrates that the login shell called -bash opens another bash subshell to run script1 and that the date command itself will run in yet another subshell. When they were finished, control was passed back to the login -bash shell, which was asleep while the subshells performed their functions.

![](img/cae5c706c216875d12d4b7d28144cc71_427_0.png)

Figure 13.2 Invoking shell scripts that are executable.

## Option 3: Invoking Scripts in the Same Shell

It is possible to force shell scripts to execute in the current shell instead of opening all the other subshells. You perform this task by altering the syntax to what is shown here:

```
$ . scriptfilename<Enter>
```

or

```
$ source script1<Enter>
```

In the first syntax example, the "." denotes “in the current shell.” The process will ultimately resemble that shown in Figure 13.3.

### Example 13.8 Invoking Scripts in the Same Shell

Freston tells Lady Molinera that she can save a few CPU cycles and some nanoseconds if she forces her script1 to execute in the same shell she is in now. But to prove it, he has her check her shell’s PID’s again, just like she did for Options 1 and 2.

```
$ echo $$
2393
$ . script1
Wed Jul 25 15:55:28 MDT 2001
2393
```

She executed script1 by running it with a “.” in front of it. Remember, the “.” means, “Do this in the current shell.” The original shell returned a PID of 2393, and the shell script also returned a current PID of 2393. The alternative syntax to the “.” is “source.” These two methods are the same, and Figure 13.3 illustrates both of them.

```
$ echo $$
2393
$ source script1
Wed Jul 25 16:05:53 MDT 2001
2393
```

### Example 13.9 Changing .bash_profiles “On the Fly”

Where else do you think this method could be useful? Assume that Freston has just made changes to his hidden .bash_profile file. Using the “.” or source, he can make the shell re-execute his user profile without him having to log out and log in again. After he has made the changes to the file itself, all he has to do is type either of the following:

```
$ . .bash_profile<Enter>
```

or

```
$ source .bash_profile<Enter>
```

![](img/cae5c706c216875d12d4b7d28144cc71_428_0.png)

Figure 13.3. Invoking shell scripts inside the current shell.

## Creating Scripts: Some Practical Examples

### Example 13.10 Exporting Variables and Values for Use with Scripts

The following script shows a variation on the classic Hello World script: Sancho is sending a greeting to his burro, Dapple (well, maybe one of the trainers will read it to him. Who knows?). We are going to use this simple script to illustrate the exporting of variables and how they can be accessed in subshells.

```
$ cat > hello<Enter>
1 #!/bin/bash
2 #This is a simple Hello World type of script
3 #
4 var1="Hi Dapple! Ready for our August journey?"
5 echo $var1
<Ctrl>-d
```

Now, to make the script executable,

```
$ chmod 755 hello<Enter>
```

When it is executed, the hello script will return the following:

```
$ hello<Enter>
Hi Dapple! Ready for our August journey?
```

The hello script has been listed with line numbers for reference. As we examine it, we will not mention all the lines. Actually, if you are using these scripts as example, leave the line numbers off.

Line 1, although it has a tic-tac-toe symbol, is actually a shell declaration (the ! ensures that). Putting a declaration in such as this one is considered proper practice, because you never know what shell the user will be in (and this addition guarantees that this script will execute in a bash shell environment).

Line 2 is a comment. It is also considered best practice to describe what the script does and sometimes so you contact for support. Quite often, these lines include information about script versioning in large environments.

Line 3 is a comment spacer line. This line makes scripting “easier on the eyes” (in other words, easier to create; easier to debug; easier to analyze; and even easier to copy).

Line 4 sets a user-defined variable called var1 to the text string “Hi Dapple! Ready for our August journey?”. When a variable is set inside the script, there will never be any question on what var1 is equal to.

Line 5 will echo the string to standard out, which is the terminal screen.

We will work with this example to demonstrate how to access variables outside the script. In the sample code coming up next, we will set another variable. But this time, it will be set outside the script in the current shell environment. The thing to note here is that it will not find the variable. This situation is intentional, and we will fix it in the next sample code:

```
$ cat >> hello<Enter>
<echo $var2<Enter>
<Ctrl>-d

$ var2="Yes I am. Let’s go!“<Enter>
$ echo $var2<Enter>
Yes I am. Let’s go!
$ cat hello<Enter>
#!/bin/bash
#
#This is a simple Hello World type of script
#
var1="Hi Dapple! Ready for our August journey?"
echo $var1
echo $var2
$ hello<Enter>
Hi Dapple! Ready for our August journey?
```

Notice that var2 did not display. The reason why is because the script executed in a subshell. The var2 variable, created in the parent login shell, was not exported to the child subshell. Therefore, the subshell did not have access to it. Let's fix that now by using the export feature.

```
$ export var2<Enter>
$ hello<Enter>
Hi Dapple! Ready for our August journey?
Yes I am. Let's go!
```

For this reason, many system administrators choose to set all their variables inside a script that needs them. In the event that you are in a situation where you are relying on a variable outside your shell, you should always conduct a test to see whether the variable is null or not before proceeding with whatever processing you wish to perform.

### Example 13.11 A Simple Backup Script

A more practical, but still simple, script would be a backup script. But first, let's look at Preston's private directory:

```
$ ls -l<Enter>
total 56
-rwxrwxr-x  1 freston knight84  110 Apr 14 12:47 monthly.rept
-rwxr-xr-x  2 freston knight84 4096 Jan  4 12:36 Desktop
-rwxrwxr-x  1 freston knight84  102 Mar 14 16:26 hello
-rwxrwxr-x  1 freston knight84   74 Jul 14 16:43 private_bu
-rwxrwxr-x  1 freston knight84   13 Jul 25 14:30 script1
-rwxr-xr-x  1 freston knight84   15 Jul 25 13:36 script2
-rw-rw-r--  1 freston knight84 2288 Jul 26 16:44 typescript
```

See if you can interpret what the following script does:

```
$ cat private_bu<Enter>
#!/bin/bash
BUF=$nightly/USER-backup-$(date +%Y%m%d).tgz
tar -cZf $BUF ~
```

The script is called private_bu, and let's say that its permissions are executable. The script is directed to run in a bash shell environment. A variable called BUF is set to a string that will represent the name of the backup file used by the tar command. The string for BUF will resolve another variable called $USER to Freston and will set the date with a specified format of year-month-day to keep the filename unique. The tar command will use this BUF variable to create the file inside a directory called nightly. Basically, Freston is creating a one-user backup file in a special directory.
