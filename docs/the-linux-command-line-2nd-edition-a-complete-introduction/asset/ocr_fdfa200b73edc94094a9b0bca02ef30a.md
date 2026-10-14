the command is a more concise way of doing the same thing.

The <<< operator indicates a here string. A here string is like a here document, only shorter, consisting of a single string. In our example, the line of data from the /etc/passwd file is fed to the standard input of the read command. We might wonder why this rather oblique method was chosen rather than:

```
echo "$file_info" | IFS=":" read user pw uid gid name home shell
```

Well, there’s a reason...

# You Can’t Pipe read

While the read command normally takes input from standard input, you cannot do this:
echo "foo" | read
We would expect this to work, but it does not. The command will appear to succeed but the REPLY variable will always be empty. Why is this?
The explanation has to do with the way the shell handles pipelines. In bash (and other shells such as sh), pipelines create subshells. These are copies of the shell and its environment which are used to execute the command in the pipeline. In our example above, read is executed in a subshell.
Subshells in Unix-like systems create copies of the environment for the processes to use while they execute. When the processes finishes the copy of the environment is destroyed. This means that a subshell can never alter the environment of its parent process. read assigns variables, which then become part of the environment. In the example above, read assigns the value “foo” to the variable REPLY in its subshell’s environment, but when the command exits, the subshell and its environment are destroyed, and the effect of the assignment is lost.
Using here strings is one way to work around this behavior. Another method is discussed in Chapter 36.

# Validating Input

With our new ability to have keyboard input comes an additional programming challenge, validating input. Very often the difference between a well-written program and a poorly written one lies in the program’s ability to deal with the unexpected. Frequently, the unexpected appears in the form of bad input. We’ve done a little of this with our evaluation programs in the previous chapter, where we checked the values of integers and screened out empty values and non-numeric characters. It is important to perform these kinds of programming checks every time a program receives input, to guard against invalid data. This is especially important for programs that are shared by multiple users. Omitting