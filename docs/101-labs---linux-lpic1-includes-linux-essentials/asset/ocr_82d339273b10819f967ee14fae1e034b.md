
# LAB 46

## Use Streams, Pipes, and Redirects: Redirection and File Descriptors

**Lab Objective:**

Learn how to redirect input and output in Bash.

**Lab Purpose:**

Bash has a commonly-used feature, known as I/O redirection, that makes life easier when using Linux. In this lab, you will learn how to make use of this powerful feature.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1

Open the `Terminal` application and run:

```bash
mkdir lab46

cd lab46

echo "hello world" > hello

cat hello
```

You just redirected the output from your `echo` command into the `hello` file. The `>` is a shortcut; the proper version of this would be `1>`, where `1` is called a *file descriptor*, which references the *standard output*.

### Task 2

Now run:

```bash
ls nonexistent 2>> hello

cat hello
```
