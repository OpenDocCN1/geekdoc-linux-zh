# Tutorial

# Linux essentials

![](bbox=[0.06, 0.14, 0.18, 0.24])

# John Gowers

is a University tutor in Programming and Computer Science. He likes to install Linux on every device he can get his hands on, and uses terminal commands and shell scripts on a daily basis.

# Resources

Most of the tools we will be using in this tutorial are standard on any Linux distribution. But you might need to install the wget command.

# First steps: Using pipelines, grep and cat in the terminal

Getting to grips with the Linux terminal can be daunting, but once it's mastered you'll find yourself much more productive

If you're a Linux user, you've probably used the terminal before, even if only once or twice, and you might have dived into the world of shell scripting; the terminal is at the heart of Linux. While we should celebrate the fact that it's now possible to do so much in a Linux system without touching the terminal, it remains the case that if you master the terminal and shell scripting, you will have unlocked a powerful tool that can make you more productive and give you greater control over your computer. There's a bigger learning curve when it comes to using the terminal than with a graphical user interface, but it is no harder than learning a programming language, and you will find that the effort is well worth it.

In this tutorial series, we will be exploring ways in which you can use shell scripting and the terminal to improve your workflow and to automate routine tasks. We shall start with the most basic material and build up quickly to more advanced topics.

The first step towards becoming a terminal master is to open the terminal on your system. You do this in different ways on different distributions, and we can't give comprehensive instructions here. Look for an application called 'Terminal' or 'Console' or something similar and open it. If you see a window with a prompt and a blinking cursor as in Figure 1, then you've done it right.

To use the terminal, we type commands at the blinking prompt and press Enter. Try typing pwd and pressing Enter. This command will show you the file path for the working directory that your terminal is currently living in. Now type ls and press Enter. You should see a list of all the files in that directory. Last, we'll use the echo command to send a greeting. echo is a command that will print your chosen line of text back to the terminal:

```
$ echo 'Hello, world!'
Hello, world!
```

If all seems to be working correctly, let's get started!

# Navigating in the terminal.

To get started in the terminal, we'll create a new directory (folder) to experiment in. The Linux command for creating

![](bbox=[0.2, 0.59, 0.95, 0.99])