
in the /etc/passwd file.

The second interesting line is this one:

```
IFS=":" read user pw uid gid name home shell <<< "$file_info"
```

The line consists of three parts: a variable assignment, a read command with a list of variable names as arguments, and a strange new redirection operator. We’ll look at the variable assignment first.

The shell allows one or more variable assignments to take place immediately before a command. These assignments alter the environment for the command that follows. The effect of the assignment is temporary; only changing the environment for the duration of the command. In our case, the value of IFS is changed to a colon character. Alternately, we could have coded it this way:

```
OLD_IFS="$IFS"
IFS=":"
read user pw uid gid name home shell <<< "$file_info"
IFS="$OLD_IFS"
```

where we store the value of IFS, assign a new value, perform the read command, then restore IFS to its original value. Clearly, placing the variable assignment in front of the command is a more concise way of doing the same thing.

The <<< operator indicates a here string. A here string is like a here document, only shorter, consisting of a single string. In our example, the line of data from the /etc/passwd file is fed to the standard input of the read command. We might wonder why this rather oblique method was chosen rather than:

```
echo "$file_info" | IFS=":" read user pw uid gid name home shell
```

Well, there’s a reason...

## You Can’t Pipe read

While the read command normally takes input from standard input, you cannot do this:

```
echo "foo" | read
```

We would expect this to work, but it does not. The command will appear to succeed but the REPLY variable will always be empty. Why is this?

The explanation has to do with the way the shell handles pipelines. In bash and other shells such as sh, pipelines create subshells. These are copies of the shell and its environment which are used to execute the command in the pipeline. In our example above, read is executed in a subshell.

Subshells in Unix-like systems create copies of the environment for the processes to use while they execute. When the processes finishes the copy of the environment is destroyed. This means that a subshell can never alter the environment of its parent process. read assigns variables, which then become part of the environment. In the example above, read assigns the value “foo” to the variable REPLY in its subshell’s environment, but when the command exits, the subshell and its environment are destroyed, and the effect of the assignment is lost.

Using here strings is one way to work around this behavior. Another method is discussed in Chapter 37.

## Validating Input

With our new ability to have keyboard input comes an additional programming challenge, validating input. Very often the difference between a well-written program and a poorly written one is in the program’s ability to deal with the unexpected. Frequently, the unexpected appears in the form of bad input. We’ve done a little of this with our evaluation programs in the previous chapter, where we checked the value of integers and screened out empty values and non-numeric characters. It is important to perform these kinds of programming checks every time a program receives input, to guard against invalid data. This is especially important for programs that are shared by multiple users. Omitting these safeguards in the interests of economy might be excused if a program is to be used once and only by the author to perform some special task. Even then, if the program performs dangerous tasks such as deleting files, it would be wise to include data validation, just in case.

Here we have an example program that validates various kinds of input:

```
#!/bin/bash

# read-validate: validate input

invalid_input () {
    echo "Invalid input  $REPLY" >&2
    exit 1
}
```

```
read -p "Enter a single item > "

# input is empty (invalid)
[[ -z $REPLY ]] && invalid_input

# input is multiple items (invalid)
(( $(echo $REPLY | wc -w) > 1 )) && invalid_input

# is input a valid filename?
if [[ $REPLY =~ ^[-[:alnum:]_]+$ ]]; then
    echo "$REPLY" is a valid filename."
    if [[ -e $REPLY ]]; then
        echo "And file '$REPLY' exists."
    else
        echo "However, file '$REPLY' does not exist."
    fi

    # is input a floating point number?
    if [[ $REPLY =~ ^-?[[:digit:]]+\.[[:digit:]]+$ ]]; then
        echo "$REPLY" is a floating point number."
    else
        echo "$REPLY" is not a floating point number."
    fi

    # is input an integer?
    if [[ $REPLY =~ ^-?[[:digit:]]+$ ]]; then
        echo "$REPLY" is an integer."
    else
        echo "$REPLY" is not an integer."
    fi
else
    echo "The string '$REPLY' is not a valid filename."
fi
```

This script prompts the user to enter an item. The item is subsequently analyzed to determine its contents. As we can see, the script makes use of many of the concepts that we have covered thus far, including shell functions, [[ ]], (( )), the control operator &&, and if, as well as a healthy dose of regular expressions.

## Menus

A common type of interactivity is called menu-driven. In menu-driven programs, the user is presented with a list of choices and is asked to choose one. For example, we could imagine a program that presented the following:

```
Please Select:
```
