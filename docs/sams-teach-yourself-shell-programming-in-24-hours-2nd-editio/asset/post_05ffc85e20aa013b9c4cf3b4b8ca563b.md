
```
echo hpux ;;
AIX)
    echo aix ;;
*)
    echo unknown ;;
}
```

As you can see, this function is not very complicated. It checks the output of uname -s and looks for a match. In the case of SunOS, it also checks the output of uname -r to determine whether the operating system is Solaris or SunOS.

In many cases, you need to tailor the options of a command, such as ps or df, for a particular system in order to obtain the desired output from that command. In such cases, you need the capability to 'ask' whether the operating system is of a certain type:

```
isOS() {
    if [ $# -lt 1 ] ; then
        echo "ERROR: Insufficient Arguments." >&2
        return 1
    fi
    REG=`echo $1 | tr '[A-Z]' '[a-z]'`
    if [ "$REG" = "`getOSName`" ] ; then return 0 ; fi
    return 1
}
```

This function compares its first argument to the output of the function getOSName and returns 0 (true) if they are the same; otherwise, it returns 1 (false).

Using this function, it is possible to write if statements similar to the following:

```
if isOS hpux ; then
    # HP-UX specific commands here
elif isOS solaris ; then
    # Solaris specific commands here
else
    # generic unix commands here
fi
```

![](img/3def70414996f811615f713b2077a154_410_0.png)

> The reason that the isOS function does not directly check the value of $1, but uses the variable REG instead, is to allow for greater flexibility on the part of the function's user. For example, this implementation allows any of the following to be used to check whether a system is running Linux:
> isOS LINUX
> isOS Linux
> isOS linux

## Techniques for Increasing Portability

There are two common techniques to increase the portability of a shell script between different versions of UNIX:

- Conditional execution
- Abstraction

Conditional execution alters the execution of a script based on the system type, whereas abstraction retains the same basic flow of the script by placing the conditional statements within functions.

### Conditional Execution

A script that uses conditional execution for portability contains an if statement at the beginning that sets several variables indicating the set of commands to use on a particular platform. This section looks at two common cases in which conditional execution is used:

- Determining the remote shell command
- Determining the proper method of using the echo command in prompts

The first case illustrates setting a variable based on the operating system type. The second case illustrates setting variables based on the behavior of a command (echo) on a particular system.

### Executing Remote Commands

A common use of conditional execution is found in scripts that need to execute commands on remote systems. On most versions of UNIX, you can use the rsh (remote shell) command to execute commands on a remote system. Unfortunately, this command is not available on all versions of UNIX. On HP-UX, for example, rsh is available but it is not the remote shell program—it is the restricted shell program. On HP-UX, you need to use the command remsh to execute commands on a remote system.

A script that needs to execute commands on a remote system might have an if statement of the following form at its beginning:

```
if SystemIs HP_UX ; then
RCMD=remsh
else
RCMD=rsh
fi
```

After the variable $RCMD is set, remote commands can execute as follows:

```
"$RCMD" host command
```

Here, host is the hostname of the remote system, and command is the command to execute.

### Problems with the echo Command in Prompts

Most programs that need to prompt the users need to be able to print a prompt that is not terminated by a newline. In Chapter 5, "Input and Output," there were several problems with using the \c escape sequence of the echo command to do this. The workaround was to use the /bin/echo command.

Although this works for UNIX versions based on System V, on some BSD-based systems this does not work. You need to specify the -n option to echo instead. By using the following shell script, you can create a shell function, echo_prompt, to display a prompt reliably across all versions of echo:

```
_ECHO=/bin/echo
_N="-n"
_O="-c"
ECHOTEST=`$_ECHO "hello \c"`
if [ "$ECHOTEST" = "hello \c" ] ; then
  _N="-n"
  _O=""
fi
export _ECHO _N _O
echo_prompt() { $_ECHO $_N "$*" $_O ; }
```

This script fragment uses the /bin/echo workaround as the base from which to construct the correct echo command. It checks the output of an echo command to determine whether the \c sequence is handled correctly. If it is not, the -n option is enabled.

After the appropriate values have been determined, the function echo_prompt is created using these values. This function enables you to reliably output prompts on every system.

## Abstraction

Abstraction is a technique used to hide the differences between the versions of UNIX inside shell functions. By doing this, the overall flow of a shell script is not affected. When a function is called, it makes a decision as to what commands to execute.

You will learn about two different examples of abstraction:

- Adapting the getSpaceFree function to run on HP-UX
- Adapting the getPID function to run on both BSD and System V

This section uses the functions getOSName and isOS, given earlier in this chapter.

### Adapting getSpaceFree for HP-UX

Recall the getSpaceFree function introduced in Chapter 21:

```
getSpaceFree() {
  if [ $# -lt 1 ] ; then
echo "ERROR: Insufficient Arguments." >&2
return 1
fi

DIR="$1"
if [ ! -d "$DIR" ] ; then
  DIR="/usr/bin/dirname $DIR"
fi

df -k "$DIR" | awk 'NR != 1 { print $4 ; }'
}
```

This function prints the amount of free space in a directory in kilobytes. Its output is used in the isSpaceAvailable function to determine whether there is enough space in a particular directory. Although this works for most systems (Solaris, Linux, BSD), it does not work on HP-UX systems because the output of df -k on HP-UX systems is quite different from other versions of UNIX.

```
$ df -k /usr/sbin
/usr  (/dev/vg00/lvol8  ) :  737344 total allocated Kb
                        368296 free allocated Kb
                        369048 used allocated Kb
                        50 % allocation used
```

To get the output in a format that is easier to parse, you need to use the command df -b instead:

```
$ df -b /usr/sbin
/usr  (/dev/vg00/lvol8  ) :  392808 Kbytes free
```

In order to use isSpaceAvailable on all systems, including HP-UX, you need to change the function getSpaceFree to take this into account. The modified version looks like the following:

```
getSpaceFree() {
  if [ $# -lt 1 ] ; then
    echo "ERROR: Insufficient Arguments." >&2
    return 1
  fi

  DIR="$1"
  if [ ! -d "$DIR" ] ; then
    DIR="/usr/bin/dirname $DIR"
  fi

  if isOS HPUX ; then
    df -b "$DIR" | awk '{ print $5 ; }'
  else
    df -k "$DIR" | awk 'NR != 1 { print $4 ; }'
  fi
}
```

Here, the isOS function is called in order to determine the command to execute.

### Adapting getPID for BSD

Recall the getPID function introduced in Chapter 21:

```
getPID() {
    if [ $# -lt 1 ]; then
        echo 'ERROR: Insufficient Arguments.' >&2
        return 1
    fi

    PSOPTS='-ef'
    /bin/ps $PSOPTS | grep "$1" | awk '/grep/ { next; } { print $2; }'
}
```

This function works correctly only on systems where the ps -ef command produces a listing of all running processes. On BSD systems and older Linux systems, you need to use the command

ps -auxw

to get the correct output. This command works correctly on BSD system but older Linux systems produce the following warning message:

> warning: '-...' deprecated; use 'ps -aux', not 'ps -auxw'

By using the getOSName function given earlier in this chapter, you can adapt the getPID function to work with the BSD, Linux, and System V versions of ps. The modified version of getPID is as follows:

```
getPID() {
    if [ $# -lt 1 ]; then
        echo 'ERROR: Insufficient Arguments.' >&2
        return 1
    fi

    case `getOSName` in
        bsd|sun|sunos|linux|darwin)
            PSOPTS='-auxw' ;;
        *)
            PSOPTS='-ef' ;;
    esac

    /bin/ps $PSOPTS 2>/dev/null | grep "$1" | \
    awk '/grep/ { next; } { print $2; }'
}
```
