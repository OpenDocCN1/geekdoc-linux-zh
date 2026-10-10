
## mount iso988 /dev/rom /dev/cdrom

As the sample shows, you are mounting three kinds of information. “iso988”, “/dev/rom”, and “/dev/cdrom”.

Apart from finding and mounting a file, you have the option to change a file’s size. This is done due to the occurrence of a file’s fragmentation.

Since files become inefficient during fragmentation, changing a file’s size allows the allocation of files. Consequently, the system becomes more stable.

You are introduced to the commands “truncate” and “fallocate”. Both commands allow you to create a file with a preferred size.

Sample:

```
# truncate -s 19MB mop1.txt
# fallocate -l 19000000 mop2.txt
# ls -ls mop.txt
0 -rw-rw-r-- 2 trs trs 19000000 Aug 12 02:44 mop1.txt
14819 -rw-rw-r-- 2 trs trs 19000000 Aug 12 02:45 mop2.txt
```

As the sample shows, you created a “19MB” file called “mop” on “Aug 12”.

## CHAPTER 4. Basic Shell Programming

In this chapter, we will dive into one of the hacker's secrets weapons that are scripting. There is quite a small difference between programmers and hackers. Programmers use scripting to build systems whereas hackers use scripting to exploit systems. Without creating their scripts, a novice hacker can never become a professional Hacker but will remain as a script kiddie who just uses other tools to crack systems. Thus, scripting knowledge is a must in the checklist for anyone trying to master hacking. To help you out this chapter will introduce a lot of bash scripting concepts with real-world coding examples. Let's have fun with some scripting now!

First of all, we need to know about the shell in detail.

### What is a Shell?

A shell is that cursor you observe when you first connect to a server using a password or when you make yourself connected to a system using remote desktop tools like SSH. In other words, if you want it to look solely from a programming point of view you would be delighted because it acts just as an interpreter between the user and system just like how an operating system does.

But it just sends the input advises from the user to the Linux kernel and sends the output that is the result back to the system user.

### Types of shell

There are types of shells that exist according to the Linux official documents. Out of both the first one stands for a GUI whereas the second one stands for CLI.

There are a lot of shells that have been manufactured with the Distro's like Bourne shell, C shell, korne shell, and Bash shell.

Out of all different types of shells that are present bash shell is one of the most famous that ever existed. It is pre-installed in almost all the famous Linux Distro's. It also acts as an interceptive language that helps the Linux kernel understand the instructions we are giving logically.

### How does the bash shell work?

There are two types of modes that one can work shell with. Out of which one is an interactive mode and the other is a script mode.

- a) Interactive mode

In this mode, the Linux user can enter the functions or the bash code one by one and wait until the result is given. If there is an error in the middle the user cannot proceed further. It just works interactively like in an old handheld video game.

- b) Script mode

In this mode first of all the bash code will be written in a text file and then will make to run the script file using the command-line interface. While using this mode the user can get all the results that he was looking for all at once. Hackers need to be more perfect in script mode because it will be easy to exploit systems fast using this way. However, programmers that are who create systems will prefer interactive mode more.

Before knowing more about the grammatical structure of the shell it would be better if we have a good overview of the advantages of the shell.

### Advantages of the shell

- 1) It is very easy to learn inline programming languages that differ a lot in both execution and implementation.
- 2) It has a lot of help documents that will help the hackers to rectify the errors as soon as possible.
- 3) It has an added advantage because it is an explanatory language. That is, it need not be compiled before running. So, hackers can easily cross-check the code before trying to implement it on the victim’s system.

Apart from this shell is also fast and works efficiently. Due to all these reasons, hackers should mandatorily learn about the implementation of the shell.

Let’s go!

## First shell script

Let us create a shell script of the name sample.sh. create a shell script using the following command.

```
cat sample.sh
```

Location of the shell program

```
echo "This is very regressive"
```

Now we will explain this in detail. Line by line.

- a) #! This represents the starting of a shell script that we are trying to write.
- b) If it starts with only a hash # then it is called a comment. Comments are annotations that are used to make it easy for reference or for other users that want to look at the code. It may seem unnecessary to write comments for small shell scripts. But it is a good practice to start writing comments.
- c) echo is a shell default command that lets the interpreter display the content that is written.

Here to run the shell you need to use the following command:

```
bash sample.sh
```

And then the output will appear

For this example, the output is as follows:

```
This is very regressive
```

There is also another feature that will let you run the script with additional permissions. As we discussed earlier Linux has a set of permissions and if you don't provide with necessary permissions the script may not run perfectly. So, to provide permission use the following command

Debugging is one of the most important programming tasks. Even hackers need to be perfect at this because wrong debugging of code may result in bad adaptation of the task.

### Debugging the shell scripts

Normally when you enter a wrong default command in the script such as shown below in the code.

```
vulnerhost @ example: echo 7898
```

This code will not run and show an error as shown below

```
the echo command is not found
```

This is exactly what debugging is. Debugging features informs the user about the errors in the script.

There are also a lot of shell debugging tools that perform the tasks we do in a command-line interface. Tools like bashdb are famous for this. This section will help hackers understand the basics of shell programming effectively. Let's go!

## Built-in Shell Commands

Before entering into a deep discussion about the built-in commands it is important to know that these built-in commands cannot be used as variable names. Variables are an important functionality of shell programming that helps to define things.

Linux provides a command called type that will let you cross-check whether a command is a built-in command or not.

The command works as follows:

```
type echo
```

The output is as follows:

```
echo is a built-in shell
```

Another example,

```
type trump
```

The output is as follows:

```
Trump is not a built-in shell
```

Also, remember that two dots that is (**) is used to determine the successful working or execution of the script. Here are the in-built commands we are going to discuss in detail.

### 1) Alias

Normally Linux commands are a little trickier to type. I suppose you have to type echo every time it may be difficult. For this reason, you can use an alias to give shortcut for a command.

Below we describe the command that needs to be entered to make alias work.

```
example@ linuxwar : Alias groupecho
```

However, it should be remembered that aliases work only until the shell environment is open. That is if the shell is exited there is no way to access it again. Also, the alias functions are stored in the bashrc directory of the user environment. Aliases are an easy way to increase productivity. Hackers use a lot of aliases to make deciphering the script a lot trickier.

### 2) Unalias

As you might have guessed already unalias is used to delete the alias systems that are present. By using this command, you can delete any alias command that you have created before.

Below is the command that will let us understand how it works:

```
example@ linuxwar : unalias groupecho
```

You can also use -a to delete all the aliases that are present at once.
However, as we said before ending a shell environment will delete all the aliases that are present but using unalias will help you to delete things while you are still scripting.

### 3) bg, fg, jobs

A lot of shellcode is done in interactive mode. Sometimes when you are trying to exploit a system you need to perform various tasks at once. These tasks are called jobs in Linux terms. So for everyone's convenience jobs are divided into two types. The first one is a foreground job where we can see the procedure that is going on. The classic example of foreground jobs is the installation of system programs. You can't handle other jobs while doing foreground jobs.
