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

# Built-in Shell Commands

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