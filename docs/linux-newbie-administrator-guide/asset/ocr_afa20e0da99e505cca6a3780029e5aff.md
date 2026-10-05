which will return you to the previous shell.

The shell for each user is specified as the last field in the the password file /etc/passwd. If you really wanted to change it, edit (as root) this file and replace the "/bin/bash" with the shell of your choice.

# 3.5.2 How do I write a simple shell script?

Create a text (ASCII) file that is to contain the shell script. For example, I would use the pico editor to write a script that runs the tar with all the parameters usually necessary to uncompress a tarball downloaded from the Internet (I never seem to remember the untar options). I decided to call my script "untar":

pico untar

Since the file "untar" did not exist in my current directory, it was created by the pico editor. Now, I type in the content of my script:

```
#!/bin/bash
echo this is the script file $0
echo untarring the file $1
# this calls tar with options -xvzf (extract, verbose, filter
through gzip, input filename)
tar -xvzf $1
```

I save the file with <Ctrl>o and exit with <Ctrl>x

The first line of the script, starting with "#!" (called-bang), is special--it tells the shell what program should be used to interpret the script. In the example, the script is to interpreted by the bash shell /bin/bash . The first line must start with #! or the script will never run (the file will be interpreted as just a text file). Other lines starting with # are comments for the author (readers, users) of the shell and are totally ignored by the computer.

The $0, $1, $2 ... in my script are the parameters passed to my script. For example, if I ran a script "myscript" with seven parameters like this:

```
myscript a b c d e f g
```

then $0 would be inside "myscript" as having the value "myscript", $1 would have the value "a", $2 would be "b", $3 would be "c", etc.

On the second and third line of my example script, the command echo prints on the screen everything that follows on the line, expanding $0 and $1 to the values of the parameters passed to the script. The fourth line is a comment written to myself to remain me what I was trying to achieve, just in case I ever had to modify my script. The fifth line performs the actual work.