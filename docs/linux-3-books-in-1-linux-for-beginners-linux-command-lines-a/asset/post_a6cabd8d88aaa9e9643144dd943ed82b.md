
The startup sequence is responsible for bringing the Linux operating system to a usable state for an end-user so that they can log in and start using the system for their tasks.

## Systemd

Systemd is called the mother of all processes in the Linux operating system. It is responsible for initiating the Linux operating system and bring it to a usable state. Before the systemd service was developed, the same task was performed by the init service, but systemd has many more functions compared to init, such as initiating and managing system service, mounting file systems, etc.

The first task for systemd is to mount all the file systems that are defined in the configuration file located at /etc/fstab. systemd also has access to all the other configuration files stored in /etc. systemd brings the system into a state or target as defined in the file stored at /etc/systemd/system/default.target. If it is a desktop, the default target is usually the graphical.target. If it is a Linux server, the default target is usually the multi-user.target.

Targets and services are units of the systemd service. The configuration file for a target defines the dependencies of that particular target. These dependencies are initiated by systemd. The dependencies refer to services needed to run the Linux operating system based on the initialized target. When systemd loads all the target's dependencies, it can be said that the system is up and running or that the system is running at that particular target level.

The startup sequence has two checkpoints, sysinit.target and basic.target. It is a fact that systemd starts services simultaneously, but some services need to be initiated before other services. A checkpoint is passed only when all the services and targets for that particular checkpoint have been initiated successfully.

The sysinit.target checkpoint is reached only after all its services and targets have been initiated. The sysinit.target has multiple dependencies, and these are initiated parallely within sysinit.target.

The sysinit.target first starts all the low-level services that are needed to reach the basic.target. The basic.target then initiates some additional services to reach the next target.

Once both these checkpoints have been reached successfully, the system can move to the **graphical.target** or **multi-user.target**. But note that the Linux system can reach the multi-user.target even before the dependencies of the graphical.target have been initiated.

You will see a text-based login prompt if the default target is set to multi-user.target. This target is commonly used by Linux servers that have Linux installed on them without any graphical interface. If you have installed Linux on a personal desktop and have included the GNOME desktop along with the installation, the default target will be the graphical.target. In such a case, you will be presented with a graphical interface to login into the Linux desktop.

This is where the startup sequence concludes. You can simply enter your username and password on the text-based login prompt or the graphical interface login screen to start using your Linux system.

Every modern-day Linux operating system functions with GRUB2 and systemd as its core components. Both these components work together to load the Linux kernel, start the services, and make the Linux system usable for any end-user.

# Chapter Eleven

## Introduction to Shell Scripting

The open-source programming language developed for Linux is known as Shell Scripting. Simply put, shell scripting is a series of individual Linux commands put together to be executed automatically. A shell script may have a single line of code or multiple lines of code that are stored in a single file such that a user does not need to type them manually every time they need to perform a specific task.

We will introduce you to the basics of shell scripting in this chapter, and we will also briefly discuss some advanced concepts of shell scripting. This chapter will serve as a launchpad for you into the world of shell scripting.

## Writing a Shell Script

You can use a text editor to write a shell script. Linux has a set of inbuilt text editors such as nano, vi, and vim. You can use any of these to start writing a shell script. One thing you need to ensure is that the files you create for your shell script are executable. You can make any file executable by running the following command on the filename.

```bash
$ chmod a+x filename.sh
```

And then, you just need to store the file in a location that is easily accessible by the Linux operating system.

The following steps go into the creation of a shell script.

- 1. Create a new file using the text editor of your choice. Save the script file with a .sh extension.
- 2. The first line of your script file should always be #!/bin/sh
- 3. Type in some Linux commands.
- 4. Save the file as filename.sh
- 5. Use the following command on the Linux shell to execute your script.

```bash
bash filename.sh
```

#! is known as a shebang operator. It tells the script the location of the interpreter of the Linux system. When you type the first line in your shell script as #!/bin/sh the Linux operating system knows that the interpreter to execute the script is located at /bin/sh

Let us create a simple shell script.

```bash
#!/bin/sh
ls
```

Save this script as list.sh

You can run this script using the following command on the shell.

```bash
[student@desktop ~]$ bash list.sh
```

Documents Movies Books Pictures

The result of this script is the `ls` function that lists down the contents of a directory.

## Commenting Your Script

Commenting is used in every programming language, and shell scripting is no exception to it. You can use the following syntax to add comments to your shell script.

```bash
#this is a comment
```

If we take the above script as an example, you can add a comment to it as follows.

```bash
#!/bin/sh
#this is my first script
```

## ls

You can also add comments as multiple lines to your shell script. You can do so by placing your comments between `:'` and `'`.

Consider the example below.

```bash
#!/bin/bash
:'
  This script calculates
  the square of 5.
'
((area=5*5))
echo $area
```

So the string between `:'` and `'` that is this script calculates the square of 5 is commented out from the script.

## Shell Variables

Variables in any programming language are used to store data in the form of characters and numbers. Shell scripts also support variables that store data that can be accessed by the Linux shell.

For instance, the simple example below shows a variable that stores some data and then prints it.

```bash
variable ="Hello"
echo $variable
```

Let us look at another example of a shell script that uses variables.

```bash
#!/bin/sh
echo "what is your name?"
read name
echo "How do you do, $name?"
read remark
echo "I am $remark too!"
```

## How Does This Script Work?

When you run this script, the system will print the question, “what is your name?”

You will then see that the system is expecting input from you. If you type Mark, the string Mark is then stored in the variable **name**. In the next line of code, the script uses the name provided to ask the next question, “How do you do Mark?” where the variable **name** gets replaced by the string entered by you earlier. The system again expects the answer to this question as input from you. When you type it, it is again stored in another variable called **remark**. So if your answer is “fine,” the script will replace the variable **remark** with your string in the next line of code and print the output as “I am fine too!”

## More Shell Scripting Examples

### Hello World

The first program everyone types to learn a new programming language is often Hello World. It is a simple program that will print the output as “Hello World.” Use a text editor like nano or vim and create a file named helloworld.sh and type the following lines of code in it.

```bash
#!/bin/bash

echo "Hello World"
```

Save the file and change the permission for the file to make it executable.

```bash
$ chmod a+x hello-world.sh
```

Now run one of the following commands to run your script.

```bash
$ bash hello-world.sh
```
