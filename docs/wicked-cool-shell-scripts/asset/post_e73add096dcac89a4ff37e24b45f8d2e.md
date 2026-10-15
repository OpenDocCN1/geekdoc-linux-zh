
## Listing 1-1: The inpath shell script functions

```bash
elif ! in_path $var "$PATH" ; then
    return 2
fi
fi
}
```

As stated in Chapter 0, we recommend that you create a new directory called scripts in your home directory, and then add that fully qualified directory name to your PATH variable. Use echo $PATH to see your current PATH and edit the contents of your login script (.login, .profile, .bashrc, or .bash_profile, depending on the shell) to modify your PATH appropriately. See "Configuring Your Login Script" on page 4 for more details.

> **NOTE**
>
> If you are listing files in the terminal with the ls command, some special files, like .bashrc or .bash_profile, may not show up at first. This is because files that start with a period, as .bashrc does, are considered "hidden" by the filesystem. (This turned out to be a bit of a bug-turned-feature very early on in Unix.) To list all the files in a directory, including the hidden ones, use the -a argument with ls.

Definitely worth mentioning again is the assumption that you're running bash as your shell for all these scripts. Note that this script explicitly sets the first line (called the shebang) to call /bin/bash. Many systems also support a /usr/bin/env bash shebang setting as the runtime for the script.

> **A NOTE ON COMMENTS**
>
> We wrestled with whether to include a detailed explanation of how each script works. In some cases, we'll provide an explanation of a tricky coding segment after the code, but in general we'll use code comments to explain, in context, what's happening. Look for lines that begin with the # symbol or, sometimes, anything that appears after the # on a line of code.
>
> Since you'll doubtless find yourself reading other people's scripts (other than ours, of course!), it's useful to practice figuring out what the heck is going on in a script by reading the comments. Commenting is also an excellent habit to get into when writing scripts of your own, to help you define what you seek to accomplish in specific blocks of code.

### How It Works

The key to getting checkForCmdInPath to work is for it to be able to differentiate between variables that contain just the program name (like echo) and variables that contain a full directory path plus the filename (like /bin/echo). It does this by examining the first character of the given value to see whether it's a /; hence, we have the need to isolate the first character from the rest of the variable value.

Note that the variable-slicing syntax ${var:0:1} at ① is a shorthand notation that lets you specify substrings in a string, starting from an offset and continuing up to the given length (returning the entire rest of the string if no length is provided). The expression ${var:10}, for example, will return the remaining value of $var starting from the 10th character, while ${var:10:5} constrains the substring to just the characters between positions 10 and 15, inclusive. You can see what we mean here:

```bash
$ var="something wicked this way comes..."
$ echo ${var:10}
wicked this way comes...
$ echo ${var:10:6}
wicked
$
```

In Listing 1-1, the syntax is just used to see whether the specified path has a leading slash. Once we have determined whether the path passed to the script starts with a leading slash, we check if we can actually find the path on the filesystem. If the path begins with a /, we assume the path given is an absolute path and check whether it exists using the -x bash operator ②. Otherwise, we pass the value to our inpath function ③ to see whether the value can be found in any of the directories set in our default PATH.

### Running the Script

To run this script as a stand-alone program, we first need to append a short block of commands to the very end of the file. These commands will do the basic work of actually getting user input and passing it to the function we wrote, as shown here.

```bash
if [ $# -ne 1 ]; then
echo "Usage: $0 command" >&2
exit 1
fi

checkForCmdInPath "$1"
case $? in
  0 ) echo "$1 found in PATH"      ;;
  1 ) echo "$1 not found or not executable"  ;;
  2 ) echo "$1 not found in PATH"  ;;
esac

exit 0
```

Once you've added the code, you can invoke the script directly, as shown next in "The Results." Make sure to remove or comment out this additional code when you're done with the script, however, so it can be included as a library function later without messing things up.
