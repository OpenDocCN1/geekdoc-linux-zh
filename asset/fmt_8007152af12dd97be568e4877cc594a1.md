
# LAB 16

# Turning Commands into a Script: Scripting Practice

**Lab Objective:**

Use what you already know to write a simple shell script, from scratch.

**Lab Purpose:**

Scripting with `Bash` is a daily task by many professional Linux administrators. When a task is repetitive, you don't want to be typing the same list of commands over and over; you want to create a script, and perhaps also schedule that script to run automatically.

**Lab Tool:**

`Ubuntu 18.04` (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

*Task 1:*

Open the Terminal application, and run your favorite text editor, such as `vi` or `nano`. (If you have never used `vi` or `vim`, then `nano` is strongly recommended.)

You may wish to reference Lab 15 if you have not already done so. Your goal is to write a script which accepts one argument—a number—and prints out two numbers at a time such that:

+ The first number counts down from the argument to 0
+ The second number counts up from 0 to the argument

Example:

```
. /foo.sh 100
100 0
99 1
98 2
...
```
