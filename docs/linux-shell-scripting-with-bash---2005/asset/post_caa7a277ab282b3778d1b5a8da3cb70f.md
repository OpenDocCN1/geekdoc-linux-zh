
A well-structured Bash script can be divided into five sections:

-   The header
-   Global declarations
-   Sanity checks
-   The main script
-   Cleanup

Each of these sections plays an important role in the design of a script. Next, you take a look at the previous example and see how you can improve it by examining each of the sections.

## The Header

The header defines what kind of script this is, who wrote it, what version it is, and what assumptions or shell options Bash uses.

The very first line of a script is the *header line*. This line begins with `#!` at the top of the script, flush with the left margin. This character combination identifies the kind of script. Linux uses this information to start the right program to run the script. For Bash scripts, this line is the absolute pathname indicating where the Bash interpreter resides. On most Linux distributions, the first header line is as follows

```bash
#!/bin/bash
```

If you don't know the location of the Bash shell, use the Linux `whereis` command to find it:

```bash
$ whereis bash
bash: /bin/bash
```

The beginning of a typical script looks like this

```bash
#!/bin/bash
#
# Flush disks if nobody is on the computer
#
# Ken O. Burch
# CVS: $Header$

shopt -s -o nounset
```

The Bash header line is followed by comments describing the purpose of the script and who wrote it. The *CVS* line is explained in Chapter 8, “Debugging and Version Control.” The `shopt -s -o nounset` command detects some spelling mistakes by reporting undefined variables.

## Global Declarations

All declarations that apply to the entirety of the script should occur at the top of the script, beneath the header. By placing *global declarations* in one place, you make it easy for someone to refer to them while reading the script.

```bash
# Global Declarations
declare -rx SCRIPT=${0##*/}         # SCRIPT is the name of this script
declare -rx who="/usr/bin/who"       # the who command - man 1 who
declare -rx sync="/bin/sync"         # the sync command - man 1 sync
declare -rx wc="/usr/bin/wc"         # the wc command - man 1 wc
```

## Sanity Checks

The next section, *sanity checks*, protects the script from unexpected changes in the computer. Normally, when a command runs at the command prompt, Bash searches several directories for the command you want to run. If it can't find the command, perhaps because of a spelling mistake, Bash reports an error. This kind of behavior is good for working interactively with Bash because it saves time and any mistakes are easily corrected with a few keystrokes.

Scripts, on the other hand, run without any human supervision. Before a script executes any statements, it needs to verify that all the necessary files are accessible. All required commands should be executable and stored in the expected locations. These checks are sometimes called *sanity checks* because they do not let the script begin its main task unless the computer is in a known, or "sane," state. This is especially important with operating systems such as Linux that are highly customizable: What is true on one computer might not be true on another.

Another way of putting it is that Bash relies on runtime error checking. Most errors are only caught when the faulty statement executes. Checking for dangerous situations early in the script prevents the script from failing in the middle of a task, otherwise making it difficult to determine where the script left off and what needs to be done to continue.

Sometimes system administrators unintentionally delete or change the accessibility of a file, making it unavailable to a script. Other times, changes in the environment can change which commands are executed. Malicious computer users have also been known to tamper with a person's login profile so that the commands you think you are running are not the ones you are actually using.

In the case of the sample script, you need to verify that the commands you need are where they're supposed to be and are available to the script.

```bash
# Sanity checks
if test -z "$BASH" ; then
    printf "$SCRIPT:$LINENO: please run this script with the BASH shell\n" >&2
    exit 192
fi
if test ! -x "$who" ; then
    printf "$SCRIPT:$LINENO: the command $who is not available - aborting\n" >&2
    exit 192
fi
if test ! -x "$sync" ; then
    printf "$SCRIPT:$LINENO: the command $sync is not available - aborting\n" >&2
    exit 192
fi
if test ! -x "$wc" ; then
    printf "$SCRIPT:$LINENO: the command $wc is not available - aborting\n" >&2
    exit 192
fi
```

## The Main Script

When you have verified that the system is sane, the script can proceed to do its work.

```bash
# Flush disks if nobody is on the computer
USERS=`who | wc -l`
if [ $USERS -eq 0 ] ; then
    sync
fi
```

## Cleanup

Finally, the script needs to clean up after itself. Any temporary files should be deleted, and the script returns a status code to the person or program running the script. In this case, there are no files to clean up. More complex scripts might use a variable to keep track of that status code returned by a failed command.

By placing the cleanup section at the end of the program, there is one unique place to perform your housekeeping tasks, as opposed to duplicating them throughout the script.

```bash
exit 0 # all is well
```

The completed script looks like Listing 4.2.

## Listing 4.2 flush.sh

```bash
#!/bin/bash
# Flush disks if nobody is on the computer
# Ken O. Burch
# CVS: $Header$

shopt -s -o nounset

# Global Declarations

declare -rx SCRIPT=${0##*/}          # SCRIPT is the name of this script

declare -rx who="/usr/bin/who"       # the who command - man 1 who
declare -rx sync="/bin/sync"         # the sync command - man 1 sync
declare -rx wc="/usr/bin/wc"         # the wc command - man 1 wc

# Sanity checks

if test -z "${BASH}" ; then
       printf "${SCRIPT}:${LINENO}: please run this script with the BASH shell\n" >&2
       exit 192
fi
if test ! -x "$who" ; then
       printf "${SCRIPT}:${LINENO}: the command $who is not available - aborting\n" >&2
       exit 192
fi
if test ! -x "$sync" ; then
       printf "${SCRIPT}:${LINENO}: the command $sync is not available - \
aborting\n" >&2
       exit 192
fi
if test ! -x "$wc" ; then
       printf "${SCRIPT}:${LINENO}: the command $wc is not available - aborting\n" >&2
       exit 192
fi

# Flush disks if nobody is on the computer

USERS=`$who | $wc -l`
if [ ${USERS} -eq 0 ] ; then
       $sync
fi

# Cleanup

exit 0 # all is well
```

This script is much longer than the four-line script that introduced this section. In general, the longer the main script, the less overhead imposed by the lines in a well-behaved script. This new script is much more secure and reliable than a script containing only the main script.

## Stopping a Script

The `logout` command, which ends an interactive login session, cannot be used to stop a script. (After all, a script is not a login session.) Instead, Bash provides two built-in commands for terminating a script.

As seen previously, the `exit` command unconditionally stops a script. `exit` can include a status code to return to the caller of the script. A status code of `0` indicates no error. If the status code is omitted, the status of the last command executed by the script is returned. As a result, it's always best to supply an exit status.

```bash
exit 0 # all is well
```

A script automatically stops when it reaches its end as if there was an implicit `exit` typed there, but the `exit` status is the status of the last command executed.

The `suspend` command likewise unconditionally stops a script. However, unlike `exit`, execution is suspended until the script is signaled to wake up and resume the next statement after the `suspend` command.

```bash
suspend # wait until notified otherwise
```

This command is discussed in more detail later in Chapter 10, “Job Control and Signals.”

There is also a Linux utility called `sleep`. Sleep suspends the script for a specific number of seconds after which it wakes up and resumes the next statement after the `sleep` command.

```bash
sleep 5 # wait for 5 seconds
```

Sleep is useful for placing pauses in the script, enabling the user to read what's been displayed so far. Sleep isn't suitable for synchronizing events, however, because how long a particular program runs on the computer often depends on the system load, number of users, hardware upgrades, and other factors outside of the script's control.

## Reading Keyboard Input

The built-in `read` command stops the script and waits for the user to type something from the keyboard. The text typed is assigned to the variable that accompanies the `read` command.

```bash
print "Archive files for how many days? "
read ARCHIVE_DAYS
```
