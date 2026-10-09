
# LAB 47

# Use Streams, Pipes, and Redirects: Pipes

**Lab Objective:**

Learn how to use pipes in Bash to use the output of one command as the input of another.

**Lab Purpose:**

Bash has a commonly-used feature, known as pipes, that makes life easier when using Linux. In this lab, you will learn how to make use of this powerful feature.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

***Task 1:***

Pipes (`|`) let you use the output of a command as the input to another command. In many situations (but not all), `|` and `<<` are kind of a reverse of one another. For example, the output of...

```
echo "hello
world" | grep e
```

... is identical to the output of...

```
grep e << "hello
world"
```

Try to predict the output of the following command string before you run it (see **Answer 1** below):

```
grep non hello | cut -d: -f3
```
