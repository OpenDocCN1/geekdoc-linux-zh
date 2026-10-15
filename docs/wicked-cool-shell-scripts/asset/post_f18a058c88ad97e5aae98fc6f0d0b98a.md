
# The Code

```
#!/bin/bash
# open2--A smart wrapper for the cool OS X 'open' command
# to make it even more useful. By default, 'open' launches the
# appropriate application for a specified file or directory
# based on the Aqua bindings, and it has a limited ability to
# launch applications if they're in the /Applications dir.
#
# First, whatever argument we're given, try it directly.

if ! open "$@" >/dev/null 2>&1 ; then
if ! open -a "$@" >/dev/null 2>&1 ; then
# More than one arg? Don't know how to deal with it--quit.
if [ $# -gt 1 ] ; then
echo "open: More than one program not supported" >&2
exit 1
else
case $(echo $1 | tr '[:upper:]' '[:lower:]') in
activ*|cpu ) app="Activity Monitor" ;;
addr* ) app="Address Book" ;;
chat ) app="Messages" ;;
dvd ) app="DVD Player" ;;
excel ) app="Microsoft Excel" ;;
info* ) app="System Information" ;;
prefs ) app="System Preferences" ;;
qt|quicktime ) app="QuickTime Player" ;;
word ) app="Microsoft Word" ;;
* ) echo "open: Don't know what to do with $1" >&2
exit 1
esac
echo "You asked for $1 but I think you mean $app." >&2
open -a "$app"
fi
fi
fi

exit 0
```

Listing 11-7: The open2 script

# How It Works

This script revolves around the zero and nonzero return codes, with the open program having a zero return code upon success and a nonzero return code upon failure ①

If the supplied argument is not a filename, the first conditional fails, and the script tests whether the supplied argument is a valid application name by adding a. If the second conditional fails, the script uses a case statement ② to test for common "nicknames" that people use to refer to popular applications.

It even offers a friendly message when it matches a nickname, just before launching the named application.

```
$ open2 excel
You asked for excel but I think you mean Microsoft Excel.
```

# Running the Script

The open2 script expects one or more filenames or application names to be specified on the command line.

# The Results

Without this wrapper, an attempt to open the application Microsoft Word fails.

```
$ open "Microsoft Word"
The file /Users/taylor/Desktop//Microsoft Word does not exist.
```

Rather than a scary error message, though it occurred only because the user did not supply the -a flag. The same invocation with the open2 script shows that it is no longer necessary to remember the -a flag:

```
$ open2 "Microsoft Word"
$
```

No output is good: the application launched and ready to use. In addition, the series of nicknames for common OS X applications means that while open -a word definitely won't work, open2 word works just fine.

# Hacking the Script

This script could be considerably more useful if the nickname list were tailored to your specific needs or the needs of your user community. That should be easily accomplished!

# 12

# SHELL SCRIPT FUN AND GAMES

![](img/4ffb1cc24a1b24b49254839643abedb2_304_0.png)

Up to this point, we've focused on serious uses of shell scripts to improve your interaction with your system and make the system more flexible and powerful. But there's another side to shell scripts that's worth exploring: games.

Don't worry—we're not proposing that you write Fallout 4 as a shell script. There just happen to be some simple games that are easily and informatively written as shell scripts. And wouldn't you rather learn how to debug shell scripts with something fun than with some utility for suspending user accounts or analyzing Apache error logs?

For some of the scripts, you'll need files from the book's resources, found at http://www.nostarch.com/uccs2/, so download that file now if you haven't already.

# TWO QUICK TRICKS

Here are two quick examples up front to show you what we mean. First off, old-school Usenet users know about rot13, a simple mechanism whereby off-color jokes and obscene text are obscured to make them a bit less easily read. It's a substitution cipher, and it's remarkably simple to accomplish in Unix.

To rot13 something, feed it through tr.

```
tr '[a-zA-Z]' '[n-za-mN-ZA-M]'
```

Here's an example:

```
$ echo "So two people walk into a bar..." | tr '[a-zA-Z]' '[n-za-mN-ZA-M]'
Fb gjb crbcyr jnyx vagb n one...
```

To unwrap it, apply the same transform:

```
$ echo 'Fb gjb crbcyr jnyx vagb n one...' | tr '[a-zA-Z]' '[n-za-mN-ZA-M]'
So two people walk into a bar...
```

A famous substitution cipher of this nature is associated with the movie 2001: A Space Odyssey. Remember the computer's name? Check it out:

```
$ echo HAL | tr '[a-zA-Z]' '[b-zaB-ZA]'
IBM
```

Another short example is a palindrome checker. Enter something you believe is a palindrome, and the code will test it.

```
testit="$echo $0 | sed 's/[^[:alpha:]]//g' | tr '[:upper:]' '[:lower:]'"
backward="$echo $testit | rev"
```

```
if [ "$testit" = "$backward" ] ; then
echo "$0 is a palindrome"
else
echo "$0 is not a palindrome"
fi
```

A palindrome is a word that's identical forward and backward, so the first step is to remove all non-alphabetic characters and ensure that all letters are lowercase. Then the Unix utility rev reverses the letters in a line of input. If the forward and backward versions are the same, we've got a palindrome; if they differ, we don't.

The games in this chapter are only a bit more complex, but all will prove fun and worth adding to your system.
