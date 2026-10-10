
objectives, subroutines, and expected outputs were of the script itself (sometimes the comments are as important as the script commands themselves)

Thus, a *shell script* is a collection of system commands stored in a text file that the shell reads and executes in sequence. A script can enable you to do anything that you could normally do from the shell prompt. Therefore, in its simplest form, it will contain at least one Linux/UNIX command, as shown in Example 13.1. When the shell processes a shell script, it reads the script file one command at a time, parses the commands, and sends them to the operating system for execution. The commands are executed in turn, just as if you had typed them at the terminal command line.

You can execute any Linux command in a shell script. In fact, some shell features that you can use in a script cannot be accessed at the command line. They are built-in facilities that enable more complicated functions to be performed.

Meanwhile, you can use any Linux/UNIX text editor to create a shell script.

## Example 13.1 Using the cat Command to Create a Simple Shell Script

Lady Molinera wants to execute the *date* command, but she does not want to enter it on the command line every time she wants to invoke it. So, she creates a shell script called *script1* using the *cat* command as her text editor:

```
$ cat > script1<Enter>
$ date<Enter>
<Ctrl>-d
```

## Example 13.2 Creating a Simple Shell Script with vi

Lady Molinera also likes to keep close track of her directory contents. She wants to execute *date*, *pwd*, and *ls -l* periodically but does not want to enter the commands at the command line one after the other every time. So, with vi, she creates another shell script called *script2* to handle this function:

```
$ vi script2<Enter>
i
date
pwd
ls -l
:wq
```

## Example 13.3 Creating the Same Simple Shell Script with cat and ;

Lady Molinera could have used cat to create script2, too. There is really no difference between the scripts created with vi and the syntax shown next. You will come across (and use, likely) several styles of script creation when reviewing others' shell scripts. Here, the Lady creates script3, which does the same as script2 with cat:

```
$ cat > script3<Enter>
date;pwd;ls -l<Enter>
<Ctrl>-d
```

# Executing Shell Scripts

Before executing a shell script, you have to determine two things:

- Can the users access the script file?
- How will the script be executed? Are the permissions on the shell script file set so the script can be executed in the manner you intended?

## Can Users Access the Script File?

In order for users to be able to execute the script file, they have to be able to access it. If they cannot, then naturally they will never be able to execute it.

One way to make it accessible is to put the script file in a directory to which there is a path. So, try to make sure its directory is listed in the PATH environment variable: yours, your group's, or everyone's. If there is no path to the directory, then whoever tries to invoke it will get a message from Linux similar to the following:

```
bash: script1: No such file or directory
```

If the shell script cannot be located in the user's path, then they will have to provide a directory path to the script (relative or absolute) when they execute it.

### Executing the Shell Script

There are two basic ways to execute a shell script:

- Use the `bash` command (if you are in the bash shell; otherwise, you use the respective shell execution command).
- Make the script file an executable file all its own. That way, the user only has to use its name to execute it.

#### Using the *bash* (or Equivalent) Command to Execute the Script File

If the script's permissions are not set as executable, you can still execute the script, but you have to use the `bash` command. In this case, no one needs the `x` (in other words, execute) permission on the file—not even the owner. `bash` will take care of it. Later in this chapter, we will show you what is actually happening when scripts are executed in this manner from a process standpoint.

##### **Example 13.4 Using the *bash* Command to Execute a Shell Script**

Here, Lady Molinera executes her `script2` script by using the `bash` command:

```bash
$ bash script2
Sat Jul 28 13:45:25 MDT 2001
/home/molinera
total 12
-rwxrwxr-x  1 molinera knights3  110 Jul 14 12:47 apples
drwxr-xr-x  2 molinera knights3 4096 Jul 4  12:36 Desktop
-rw-rw-r--  1 molinera knights3    8 Jul 25 13:24 script1
-rw-rw-r--  1 molinera knights3   15 Jul 25 13:36 script2
```

Note that in this example, you presumed one of two things: 1) that the script file is in the same directory as Lady Molinera (which the response actually substantiates), or 2) that the script file could have been somewhere in the directories defined by the Lady's `PATH` variable.

To check her PATH environment variable value(s), let’s have Lady Molinera echo her PATH:

```
$ echo $PATH
/usr/local/bin::bin:/usr/bin:/usr/X11R6/bin:../home/molinera/bin:
```

## Making Shell Script Files Executable

The alternative (the preferred alternative, really) for script execution relies on the owner of the shell script file making that an “executable” by using the chmod command (we discussed chmod in Chapter 6, “Linux File Permissions”). Users of the shell script file must have both read and execute permissions for the shell script file. Why? The answer is, because the shell needs to open the script file to read the commands within it. If you give “group” the execute permission, however, you need not give it to “others” and vice versa (although if someone is in “group,” he or she is probably in “others,” too). You can be selective.

The owner can use either of the following two syntax formats:

```
$ chmod ugo+rx scriptfilename<Enter>
```

Or

```
$ chmod 755 scriptfilename<Enter>
```

Or

```
$ chmod +x script2<Enter>
```

In those three examples, “execute” permission is given to everybody. We could have narrowed the permissions somewhat to “ug+rx” or “754” for just the “same group” members or just “u+x” or “744” so that the owner is the only one who can execute it like that.

At any rate, after you complete the previous step(s), the designated user(s) can invoke the script2 shell script as if it were an ordinary command (in other words, without bash or any other shell execution command) as follows:

```
$ script2<Enter>
```

Similar to executing with the `bash` command, later in this chapter we will show you what is actually happening from a process standpoint when scripts are executed in this manner.

### **Example 13.5 Using the bash Command to Execute a Shell Script**

Lady Molinera wants to make her `script2` file executable so that she can execute it without relying on the shell execution commands all the time. Plus, she would like to make `script2` available to others in her group for their convenience, too. Here is how she does both at once:

```
$ chmod 754 script2<Enter>
```

She can now invoke it in the following manner:

```
$ script2<Enter>
Wed Jul 25 13:54:25 MDT 2001
/home/molinera
total 12
-rwxrwxr-x 1 molinera knights3 110 Jul 14 12:47 apples
drwxr-x 2 molinera knights3 4096 Jul 4 12:36 Desktop
-rw-rw-r-- 1 molinera knights3 8 Jul 25 13:24 script1
-rwxr-xr-- 1 molinera knights3 15 Jul 25 13:36 script2
```

Before we move on, see how the permission bits were changed on `script2`?

## Shell Script Invocation from a Process Standpoint: Three Options

We have already seen the results of two of the following three options for invoking shell scripts. Here are all three:

- Invoking shell scripts by using the `bash` command
- Invoking shell scripts that are executable
- Invoking shell scripts inside the current shell

Basically, all three methods seem to create the same results. But they might cause the shell(s) to behave differently. To illustrate, we will use Lady Molinera's very simple `script1` file created in Example 13.1.

### Option 1: Invoking Scripts by Using the bash Command

When a shell script like `script1` is invoked with bash, a bash subshell is invoked by the login -bash shell to execute the shell script file.

That other bash subshell runs as a child to the parent login shell. When that subshell has finished executing the commands in the `script1` file, it terminates and control is passed back to the parent login -bash shell.

#### Example 13.6 Processes Invoked When the bash Command Executes a Shell Script

The only way that we can really demonstrate this behavior is to

- Identify and echo the current shell's `PID`.
- Ask `script1`, as it is being executed, to `echo` back the `PID` of the shell in which it is actually being executed.

To do so, we have asked Lady Molinera to modify her `script1` to echo the current subshell's `PID` as it runs. The script now looks like the following (the `echo $$` will display the `PID` of the subshell that actually invokes `script1`):

```
$ cat script1<Enter>
date
echo $$
```

Before running the script, she displays the current shell's `PID` to demonstrate that it is different from the subshell in which the script will eventually execute:

```
$ echo $$<Enter>
2393
$ bash script1<Enter>
Wed Jul 25 14:35:59 MDT 2001
2413
```
