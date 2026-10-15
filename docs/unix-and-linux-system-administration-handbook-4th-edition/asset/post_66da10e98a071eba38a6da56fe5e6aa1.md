
## Input and output

The echo command is crude but easy. For more control over your output, use **printf**. It is a bit less convenient because you must explicitly put newlines where you want them (use “\n”), but it gives you the option to use tabs and enhanced number formatting in your output. Compare the output from the following two commands.

```sh
$ echo "\taa\tbb\tcc\n"
\taa\tbb\tcc\n
$ printf "aa\tbb\tcc\n"
    aa  bb  cc
```

Some systems have OS-level **echo** and **printf** commands, usually in **/bin** and **/usr/bin**, respectively. Although the commands and the shell built-ins are similar, they may diverge subtly in their specifics, especially in the case of **printf**. Either adhere to **bash**’s syntax or call the external **printf** with a full pathname.

You can use the **read** command to prompt for input. Here’s an example:

```bash
#!/bin/bash

echo -n "Enter your name: "
read user_name

if [ -n "$user_name" ]; then
    echo "Hello $user_name!"
    exit 0
else
    echo "You did not tell me your name!"
    exit 1
fi
```

The **-n** in the **echo** command suppresses the usual newline, but you could also have used **printf** here. We cover the if statement’s syntax shortly, but its effect should be obvious here. The **-n** in the if statement evaluates to true if its string argument is not null. Here’s what the script looks like when run:

```text
$ sh readexample
Enter your name: Ron
Hello Ron!
```

## Command-line arguments and functions

Command-line arguments to a script become variables whose names are numbers. $1 is the first command-line argument, $2 is the second, and so on. $0 is the name by which the script was invoked. That could be something strange such as **../bin/example.sh**, so it’s not a fixed value.

The variable $# contains the number of command-line arguments that were supplied, and the variable $* contains all the arguments at once. Neither of these variables includes or counts $0.

If you call a script without arguments or with inappropriate arguments, the script should print a short usage message to remind you how to use it. The example script below accepts two arguments, validates that the arguments are both directories, and displays them. If the arguments are invalid, the script prints a usage message and exits with a nonzero return code. If the caller of the script checks the return code, it will know that this script failed to execute correctly.

```bash
#!/bin/bash

function show_usage {
  echo "Usage: $0 source_dir dest_dir"
  exit 1
}

# Main program starts here
if [ $# -ne 2 ]; then
  show_usage
else # There are two arguments
  if [ -d $1 ]; then
    source_dir=$1
  else
    echo 'Invalid source directory'
    show_usage
  fi
  if [ -d $2 ]; then
    dest_dir=$2
  else
    echo 'Invalid destination directory'
    show_usage
  fi
fi

printf "Source directory is ${source_dir}\n"
printf "Destination directory is ${dest_dir}\n"
```

We created a separate show_usage function to print the usage message. If the script were later updated to accept additional arguments, the usage message would only have to be changed in one place.

```text
$ mkdir aaa bbb
$ sh showusage aaa bbb
Source directory is aaa
Destination directory is bbb
$ sh showusage foo bar
Invalid source directory
Usage: showusage source_dir dest_dir
```

5. Note that the error messages and usage message go to standard output. Shouldn't they go to standard error instead? That would in fact be more correct, but since this script isn't intended for use as a filter, the distinction is less important.

Arguments to **bash functions** are treated much like command-line arguments. The first argument becomes $1, and so on. As you can see in the example above, $0 remains the name of the script.

To make the previous example a bit more robust, we could make the `show_usage` routine accept an error code as an argument. That would allow a more definitive code to be returned for each different type of failure. The next code excerpt shows how that might look.

```bash
function show_usage {
    echo "Usage: $0 source_dir dest_dir"
    if [ $# -eq 0 ]; then
        exit 99 # Exit with arbitrary nonzero return code
    else
        exit $1
    fi
}
```

In this version of the routine, the argument is optional. Within a function, $# tells you how many arguments were passed in. The script exits with code 99 if no more-specific code is provided. But a specific value, for example,

```text
show_usage 5
```

makes the script exit with that code after printing the usage message. (The shell variable $? contains the exit status of the last command executed, whether used inside a script or at the command line.)

The analogy between functions and commands is strong in **bash**. You can define useful functions in your `~/.bash_profile` file and then use them on the command line as if they were commands. For example, if your site has standardized on network port 7988 for the SSH protocol (a form of “security through obscurity”), you might define

```bash
function ssh {
    /usr/bin/ssh -p 7988 $*
}
```

in your `~/.bash_profile` to make sure ssh is always run with the option **-p 7988**.

Like many shells, bash has an alias mechanism that can reproduce this limited example even more concisely, but functions are more general and more powerful. Forgo aliases and use functions.

## Variable scope

Variables are global within a script, but functions can create their own local variables with a local declaration. Consider the following code.
