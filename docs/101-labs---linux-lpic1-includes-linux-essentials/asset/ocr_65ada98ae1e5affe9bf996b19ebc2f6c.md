
# LAB 67

Customize or Write Simple Scripts: Miscellaneous Tools

## Lab Objective

Learn about more useful scripting commands, such as `read`, `seq`, and `exec`.

## Lab Purpose

In this lab, you will learn how to read input to a script with `read`, print a sequence of numbers with `seq`, and replace the current shell with `exec`.

## Lab Tool

Ubuntu 18.04 (or another distro of your choice)

## Lab Topology

A single Linux machine, or virtual machine

## Lab Walkthrough

### Task 1

Open the Terminal and run:

```
read -p "What is your name? " name
<type your name>
echo $name
```

This is a simple use of `read`, but it can also be used to read from file descriptors rather than standard input. See the man page for more info.

### Task 2

`seq` is another command that's fairly straightforward to understand. Run the following:

```
seq 5
seq 3 5
seq 0 2 5
seq 0 0.5 5
```
