
## LAB 13

# Searching and Extracting Data from Files: Pipes and Redirection

Lab Objective:

Learn how to use pipes and redirect input and output in `Bash`.

Lab Purpose:

`Bash` has two commonly-used features, known as pipes and I/O redirection, that make life easier when using `Linux`. In this lab, you will learn how to make use of these powerful features.

Lab Tool:

`Ubuntu 18.04` (or another distro of your choice)

Lab Topology:

A single `Linux` machine, or virtual machine

Lab Walkthrough:

### Task 1

Open the Terminal application and run:

```bash
mkdir lab13

cd lab13

echo "hello world" > hello

cat hello
```

You just redirected the output from your `echo` command into the `hello` file. The `>` is a shortcut; the proper version of this would be `1>`, where `1` is called a file descriptor, which references the standard output.

### Task 2

Now run:

```bash
ls nonexistent 2>> hello

cat hello
```
