
You can use the du (short for disk usage) command to determine the amount of disk space used by a directory. Because you are interested in the disk usage for the entire directory in kilobytes, you need to use the -s (short for sum) and -k (short for kilobytes) options. The output of the du -sk command looks like the following:

```
$ du -sk /home/ranga/pub
4922 /home/ranga/pub
```

The size of the directory in kilobytes is listed in the first column. This function uses awk to retrieve this number.

```
# Name: getSpaceUsed
# Desc: output the space used for a directory
# Args: $1 -> The directory to check

getSpaceUsed () {
  if [ -d $1 ] ; then
    du -sk $1 | awk '{ print $1; }'
    return $?
  fi
  return 1
}
```

This function is almost as simple as getSpaceFree. It first determines whether it was given an argument. If no argument was given, it displays an error message and returns. Otherwise, it determines whether the first argument is a directory. If it is not, an error message is displayed and the function returns.

This function is quite simple; if the first argument, $1, is a directory, it executes du to determine the disk usage and then retrieves that value using awk:

```
du -sk '$1' | awk '{ print $1; }'
```

If the first argument is not a directory, the function returns 1, indicating failure.

The following example illustrates the use of this function:

```
getSpaceUsed /usr/local
```

The output is similar to the following (provided the directory /usr/local exists on your system):

```
15164
```

The number returned is in kilobytes, which in this case translates to about 15.1MB.

Often, you will want to compare the output of this function to some value. For example, the following example determines whether more than 10,000KB is used by the directory /var/tmp:

/var/tmp:
#!/bin/sh
#HOME/lib/libTYP52.sh

if [ "`getSpaceUsed /var/tmp`" -gt 10000 ] ; then
printWARNING "You're using too much space!"
fi

## Obtaining a Process ID by its Process Name

One of the difficulties with the ps command is that it is difficult to obtain the process ID (PID) of a command by specifying its process name. This capability is essential in scripts that start and stop processes. The next function in the library provides this capability.

```
# Name: getPID
# Desc: Outputs a list of process id matching $1
# Args: $1 -> the command name to look for

getPID() {
    if [ $# -lt 1 ] ; then
        return 1
    fi

    PSOPTS="-ef"
    /bin/ps $PSOPTS | grep "$1" | grep -v grep | awk '{ print $2; }'
}
```

As you can see, this function is a set of filters for the output of the command /bin/ps -ef. The first grep command looks for all lines that match the first argument. As an example, executing this on the command line produces output similar to the following:

```
$ /bin/ps -ef | grep sshd
```

Here you are looking for all the lines that contain the word sshd. The output might be similar to the following:

```
root 1449 1 8 12:23:06 ? 0:02 /opt/bin/sshd
ranga 1451 944 5 12:23:08 pts/0 0:00 grep sshd
```

As you can see, the output contains two lines. The first one contains the process ID of the command that you are looking for, but the second contains the process ID of the grep command that you executed. In order to ignore such lines, the command grep -v grep is used in the pipeline. Finally, awk extracts the process ID, which is stored in the second column of the output of ps. If more than one process has the requested name, this function displays each process ID.

Readers who are using Linux or BSD systems have to change this function in order for it to run properly. The value of the variable PSOPTS should be set to -auxw instead of -ef on these systems. In Chapter 23, you will see how to incorporate these changes into the function so that it runs without modification under any version of UNIX.

The following command illustrates the use of getPID:

```
getPID httpd
```

The output of this command is a list of process IDs, similar to the following:

- 330
- 331
- 332
- 333
- 334

## Getting a User's Numeric User ID

Some shell scripts need to determine whether a user has sufficient permissions to execute commands. For example, a startup script might need to run as root (UID 0) to modify system files correctly.

A user's ID can be checked by using the id command. The default for this command is to output information about the current user:

```
$ id
uid=500(ranga) gid=100(users) groups=100(users),101(ftpadmin)
```

If a username is supplied as an argument, the id command outputs information for that user:

```
$ id vathsa
uid=501(vathsa) gid=100(users) groups=100(users)
```

This chapter's function supports both modes.

```
# Name: getUID
# Desc: outputs a numeric user id
# Args: $1 -> a user name (optional)
```

```
getUID() {
  id $1 | sed -e 's/.*uid=//' -e 's/(.*//'
}
```

This function executes the id command and then uses sed to filter all the unimportant information.

When getUID is executed by itself

getUID

the output is similar to the following:

500

When the function is called with a username

getUID vathsa

the output is similar to the following:

501

Usually you need to compare this output to some known UID as follows:

```
#!/bin/sh
. $HOME/lib/sh/libTYP52.sh

if [ "`getUID`" -gt 100 ] ; then
printERROR 'You do not have sufficient privileges.'
exit 1
fi
```

Here the output of the getUID function is checked to see whether it is greater than 100.

## Summary

In this chapter you examined libraries of functions. Libraries can simplify your scripts by providing a shared interface for common scripting tasks. You also examined several functions in a library. By using and improving these implementations, you can avoid having to reinvent the wheel when faced with a particular problem.

## Questions

- 1. Write a function named toLower that converts its arguments to all lowercase and outputs the converted string to STDOUT. (HINT: Use tr .)
- 2. Write a function named toUpper that converts its arguments to all uppercase and outputs the converted string to STDOUT. (HINT: Use tr.)
- 3. Write a function called isSpaceAvailable to check whether a directory contains a certain amount of disk space.
The function should accept two arguments. The first one indicates the directory to check, and the second one indicates the amount of space to check. The function should return 1 if both arguments are not supplied or if the first argument is not a directory.

If sufficient space is present, your function should return 0. This enables you to use it as follows:

```
if isSpaceAvailable /usr/local 20000 ; then
: # perform some action
fi
```

(HINT: Use the function getSpaceFree.)
- 4. Modify your isSpaceAvailable function to accept an optional third argument that specifies the units of the amount space to check.

The default should remain in kilobytes, but you should support m or mb indicating megabytes and g or gb indicating gigabytes. If some other units are given, assume that the user meant kilobytes.

(The following conversion factors apply to this problem: 1 megabyte equals 1024 kilobytes, and 1 gigabyte equals 1024 megabytes.)

(HINT: Use the bc command.)
- 5. Write a function called isUserRoot that determines whether the ID of a user is equal to 0. If no user is given, it should determine whether the ID of the current user is root. (HINT: Use getUID.)

## Terms

**Executable Code** The part of the script that consists of all the commands in the script outside of the function definitions.

**Library** A repository of functions that can be accessed by shell scripts.

## Hour 22

### Problem Solving with Shell Scripts

In Chapter 21, “Problem Solving with Functions,” you examined several useful functions that can be used in shell scripts. In this chapter, you will learn about two shell scripts that demonstrate how you can use shell scripts to solve everyday problems.

These scripts illustrate how the tools covered in previous chapters can be used to create new re-usable tools. For each script, the chapter first describes the motivations for its development, followed by some design issues. Then it presents the script along with a discussion of the script’s flow.

This chapter examines two scripts related to the following topics:

- Startup scripts
- Maintaining an address book

![](img/3def70414996f811615f713b2077a154_374_0.png)
