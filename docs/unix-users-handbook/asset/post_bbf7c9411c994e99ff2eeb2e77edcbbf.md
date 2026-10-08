
# CHAPTER 11

## Introduction to Shell Programming

### Shell Programming

There is much more to a shell than meets the eye. The shell is much more than the command line interpreter everyone is used to using. UNIX shells actually provide a powerful interpretive programming language as well.

In this chapter, we’ll cover **ksh** shell programming. I chose **ksh** because most **ksh** programming techniques work with the Bourne shell as well. There is a follow-on to **ksh** programming at the end of the chapter for **csh** because the **csh** employs many different programming techniques than the **ksh**.

We’ll cover most important **ksh** programming techniques. The climax of this chapter is a fairly sophisticated shell program to remove files and place them in a directory, rather than just permanently removing files from the system with **rm**. This program employs all the shell programming techniques covered in the chapter. This shell program, called **trash**, with some minor modifications, can be run in the Bourne shell as well.

The shell is one of the most powerful features on any UNIX system. If you can’t find the right command to accomplish a task, you can probably build it quite easily using a shell script.

The best way to learn shell programming is by example. There are many examples given in this chapter. Some serve no purpose other than to demonstrate the current topic. Most, however, are useful tools or parts of tools that you can easily expand and adapt into your environment. The examples provide easy-to-understand prompts and output messages. Most examples show what is needed to provide the functionality we are after. They do not do a great deal of error checking. From my experience, however, it only takes a few minutes to get a shell program to do what you want; it can take hours to handle every situation and every error condition. Therefore, these programs are not very dressed up (maybe a sport coat versus a tuxedo). I’m giving you what you need to know to build some useful tools for your environment. I hope that you will have enough knowledge and interest by the time we get to the end of this chapter to learn and do more.

Most of the examples in this chapter were performed on a Solaris system; however, shells are nearly identical going from one system to another so you should be able to get the programs in this chapter running on your system quickly.

### Steps to Create Shell Programs

When you craft a shell program, there are some initial steps you want to perform so that you have consistency among all of your programs. The following is a list of some important concepts to employ with your shell programs:

-   **1. Names of shell programs and their output** - You should give your shell programs and their output a meaningful name. If you call your shell programs *script1, script2* and so on these will not have any meaning for you and other potential users of the programs. If your shell program finds files of a particular type, then you can name the program *filefind* or some other descriptive name. Do the same with the output of shell programs. Don't call the output of a shell program *output1* if there is some descriptive name you can give it such as *filefind.out*. Also avoid naming shell programs and their output names that already exist. You may use commands such as **read** and **test**, so you may create confusion and conflicts if you were to give your program and their output the same names. The first shell program in this chapter shows today's date. If we were to name the program **date**, we would actually run the system **date** command as opposed to our shell program **date**. The reason is that in most cases, the system **date** command would be found before our shell program **date** file.
-   **2. Repository for shell programs** - If you plan to produce numerous shell programs, you may want to place them in a directory. You can have a directory in your home directory called **bin** or **shellprogs**, in which all programs are located. You can then update your path to include the directory name where your shell programs are located.
-   **3. Specify shell to execute program** - The very first line of the program specifies the shell to be used to execute the program. The path of the shell is preceded by `#!`, which is a "magic number" that indicates that the path of the shell is about to follow. The shell programs in this chapter use the **ksh** path.
-   **4. Formatting of shell programs** - Do not underestimate the importance of proper formatting to enhance the readability of shell programs. You should indent areas of the program to indicate that commands are part of a group. Indenting only three or four spaces is fine for groups of commands. You may also want to set autoindent in **vi** so that the next line starts at the same point as the previous line (try :set **ai** in **vi** to see how this technique works). You can break up long lines by placing a `\` at the end of one line and continue the command on the next line.
-   **5. Comments** - Include detailed comments in your shell program. You can write paragraphs of comments to describe what an upcoming section of your program will accomplish. These will help you understand your program when you look at it months or years after having originally created it as well as help others understand the program. No limit exists on the amount of comments you can include. Start comment lines with a `#` (pound sign).
-   **6. Make the shell program executable** – The **chmod** command covered in the chapters introducing various shells is used to make your program executable.

Following the previous list of recommendations will make creating and using shell programs more efficient. Now we need to cover the types of shell programs.

A shell program is simply a file containing a set of commands you wish to execute sequentially. The file needs to be set with execute permissions so that you can execute it just by typing the name of the script.

There are two basic forms of shell programs exist:

-   **1. Simple command files** – When you have a command line or set of command lines that you use over and over, you can use one simple command to execute them all.
-   **2. Structured programs** – The shell provides much more than the ability to “batch” together a series of commands. It has many of the features that any higher-level programming language contains:
    -   Variables for storing data
    -   Decision-making controls (the **if** and **case** commands)
    -   Looping abilities (the **for** and **while** loops)
    -   Function calls for modularity

Given these two basic forms you can build everything from simple command replacements to much larger and more complex data manipulation and system administration tools.

### ksh Programming

I have created a directory in my home directory called **shellprogs** to serve as a repository for my shell programs. In order to execute these programs without having to specify an absolute path, I have updated my path in **.profile** to include the following line:

```
export PATH=${PATH}:~/shellprogs
```

This adds /home/martyp/shellprogs to my path. After updating **.profile** you can log out and log in to update your path. You can issue the command below to confirm that your path has indeed been updated to include the directory in which you keep your shell programs:

```
martyp $ echo $PATH
/usr/bin:/usr/sbin:/etc:~/shellprogs
martyp $
```

Let's now go to the **shellprogs** directory and type a simple command file called **today**:

```
#!/bin/ksh
# This is a simple command file to display today's date.
echo "Today's date is"
date +%x
```

Before we look at each line in the program, let's run it to see the output:

```
martyp $ today
ksh: today: cannot execute
martyp $ ls -al
total 6
```

![](img/75f39fc91296b889c0653851accdfd46_722_0.png)

We could not execute **today** because the file was created without execute permissions, which we confirm by performing a long listing. We then add execute permission to the file with **chmod +x**, which is confirmed with the next long listing. We are then able to execute **today** and view its results.

The **umask** discussion in each of the earlier shell chapters describes the defaults for new files. Almost invariably, new files are created without execute permission; therefore, you will have to update the permissions on the file to include execute.

Let's now walk through this simple shell program and analyze each line.

```
#!/bin/ksh
```

The first line specifies that the **ksh** will be used. If you are using Bash, C shell, or any other shell, you would specify its location in this manner. Some systems have multiple versions of shells running on them. It may be that a shell has been updated since the last release and some users may want to maintain the old version of the shell. For this reason, you want to be sure that the absolute path you specify is indeed that of the shell you wish to use. Note that the **#!** must be the very first two characters in the file.

Normally, when you run a shell program, the system tries to execute commands using the same shell you are using for your interactive
