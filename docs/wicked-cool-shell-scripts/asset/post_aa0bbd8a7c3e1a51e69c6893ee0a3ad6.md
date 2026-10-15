
```
if [ ! -d ${HOME:?"You need to have your HOME set to your home directory"} ]
then
    echo "** HOME set to $HOME, but it's not a directory."
    errors=$(($errors + 1))
fi

# Our first interesting test: Are all the paths in PATH valid?

oldIFS=$IFS; IFS=":"   # IFS is the field separator. We'll change to ':'.

for directory in $PATH
do
    if [ ! -d $directory ] ; then
        echo "** PATH contains invalid directory $directory."
        errors=$(($errors + 1))
    fi
done

IFS=$oldIFS            # Restore value for rest of script.

# The following variables should each be a fully qualified path,
#   but they may be either undefined or a progname. Add additional
# # variables as necessary for your site and user community.

validate "EDITOR" $EDITOR
validate "MAILER" $MAILER
validate "PAGER" $PAGER

# And, finally, a different ending depending on whether errors > 0

if [ $errors -gt 0 ] ; then
    echo "Errors encountered. Please notify sysadmin for help."
else
    echo "Your environment checks out fine."
fi

exit 0
```

> Listing 5-21: The validator script

## How It Works

The tests performed by this script aren't overly complex. To check that all the directories in PATH are valid, the code steps through each directory to ensure that it exists ⑥. Notice that the internal field separator (IFS) had to be changed to a colon at ⑤ so that the script would properly step through all of the PATH directories. By convention, the PATH variable uses a colon to separate each of its directories:

```
$ echo $PATH
/bin:/sbin:/usr/bin:/sw/bin:/usr/X11R6/bin:/usr/local/mybin
```

To validate: the environment variable values are valid, the validate() function ② first checks whether each value begins with a /. If it does, the function checks whether the variable is an executable. If it doesn’t begin with a /, the script calls the in_path() function imported from the library we started with Script #1 on page 11 ① to see whether the program is found in one of the directories in the current PATH.

The most unusual aspects of this script are its use of default values within some of the conditionals and its use of variable slicing. Its use of default values in the conditionals is exemplified by the line at ③. The notation ${varname:?'errorMessage'} can be read as "If varname exists, substitute its value; otherwise, fail with the error errorMessage."

The variable-slicing notation ${varvalue%${varvalue%?}} used at ③ is the POSIX substring function, and it produces only the first character of the variable varvalue. In this script, it’s used to tell whether an environment variable has a fully qualified filename (one starting with / and specifying the path to the binary).

If your version of Unix/Linux doesn’t support either of these notations, they can be replaced in a straightforward fashion. For example, instead of ${SHELL:?'No Shell'}, you could substitute the following:

```
if [ -z "$SHELL" ] ; then
echo "No Shell" >&2; exit 1
fi
```

And instead of {varvalue%${varvalue%?}}, you could use this code to accomplish the same result:

```
$(echo $varvalue | cut -c1)
```

## Running the Script

This is code that users can run to check their own environment. There are no starting arguments, as Listing 5-22 shows.

## The Results

```
$ validator
** PATH contains invalid directory /usr/local/mylbin.
** MAILER set to /usr/local/bin/elm, but I cannot find executable.
Errors encountered. Please notify sysadmin for help.
```

Listing 5-22: Testing the validator script

## #44 Cleaning Up After Guests Leave

Although many sites disable the guest user for security reasons, others do have a guest account (often with a trivially guessable password) to allow clients or people from other departments to access the network. It’s a useful

account, but there's one big problem: with multiple people sharing the same account, it's easy for someone to leave things messed up for the next user—maybe they were experimenting with commands, editing .rc files, adding subdirectories, or so forth.

This script in Listing 5-23 addresses the problem by cleaning up the account space each time a user logs out of the guest account. It deletes any newly created files or subdirectories, removes all dotfiles, and rebuilds the official account files, copies of which are stored in a read-only archive tucked away in the guest account's .template directory.

## The Code

```
#!/bin/bash

# fixguest--Cleans up the guest account during the logout process

# Don't trust environment variables: reference read-only sources.
iam=$(id -un)
myhome="$(grep "^$iam:" /etc/passwd | cut -d: -f6)"

# *** Do NOT run this script on a regular user account!

if [ "$iam" != "guest" ] ; then
echo "Error: you really don't want to run fixguest on this account." >&2
exit 1
fi

if [ ! -d $myhome/.template ] ; then
echo "$0: no template directory found for rebuilding." >&2
exit 1
fi

# Remove all files and directories in the home account.

cd $myhome

rm -rf * $(find . -name "[.-a-zA-Z0-9]*" -print)

# Now the only thing present should be the .template directory.

cp -Rp .template/* .
exit 0
```

Listing 5-23: The fixguest script
