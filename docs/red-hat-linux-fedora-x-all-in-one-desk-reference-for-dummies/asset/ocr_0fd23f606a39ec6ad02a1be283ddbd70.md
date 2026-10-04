# Writing Shell Scripts

To combine the split files back into a single file, use the cat command as follows:

```
cat part.?? > hugefile.tar
```

# Writing Shell Scripts

If you have used MS-DOS, you may remember MS-DOS batch files. These are text files with MS-DOS commands. Similarly, shell scripts are also text files with a bunch of shell commands.

If you aren't a programmer, you may feel apprehensive about programming. But shell programming can be as simple as storing a few commands in a file. Right now you can't write complex shell scripts, but you can certainly try out a simple shell script.

To try your at a little shell programming, type the following at the shell prompt exactly as shown and then press Ctrl+D when you're:

```
cd
cat > /bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

The cat command changes the current directory to your home directory. Then the cat command displays whatever you type; in this case, I'm sending the output to a file named simple. After you press Ctrl-D, the cat command ends and you see the shell prompt again. What you have created is a file named simple that contains the following script:

```
/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

The first line commands Linux to run the Bash program (its name is /bin/bash). The shell then reads the rest of the lines in the script.

Just as most Linux commands accept command-line options, a Bash script also accepts command-line options. Inside the script, you can refer to the options as $1, $2, and so on. The special name $0 refers to the name of the script itself.