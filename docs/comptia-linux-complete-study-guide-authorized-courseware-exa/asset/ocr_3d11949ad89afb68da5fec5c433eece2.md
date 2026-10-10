```
if [ -s $2 ]
then
echo "Target file exists! Exiting!"
exit
fi
)
check $1 $2
doit $1 $2
```

If you enter Listing 9.6 and call it safercp, you can use it like this, assuming the file original.txt exists and dest.txt doesn’t:

```
$ ./safercp original.txt dest.txt
$ ./safercp original.txt dest.txt
Target file exists! Exiting!
```

The first run of the command succeeded because dest.txt didn’t exist. When the command was run a second time, though, the destination file did exist, so the program terminated with the error message.

Note that the functions aren’t run directly and in the order in which they appear in the script. They’re run only when called in the main body of the script (which in Listing 9.6 consists of just two lines, each corresponding to one function call).

Shell scripts are useful tools, and creating them effectively requires practice. Exercise 9.2 begins your exploration of shell scripts, but in the long run, you’ll need to learn to design your own shell scripts by doing more than copying examples from a book.

# EXERCISE 9.2

# Creating a Simple Script

This exercise presents a shell script that gives you the option of reading every text file (with a name ending in .txt) in the current directory with less. To begin with this script, follow these steps:

+   1. Log into the Linux system as a normal user.

+   2. Launch an xterm from the desktop environment’s menu system, if you used a GUI login method.

+   3. Start an editor, and tell it to edit a file called testscript.

+   4. Type the following lines into the editor:

```
#!/bin/bash
for file in `ls *.txt` ; do
echo -n 'Display $file? '
```