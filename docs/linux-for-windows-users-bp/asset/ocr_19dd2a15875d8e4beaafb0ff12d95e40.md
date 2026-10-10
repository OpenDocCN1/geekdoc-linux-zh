# 2  Command Line

a list of the files in a directory that start with “Fig”, this command would list them:

**Fig\***

if you needed to know which files started with “Fig” had two characters and then ended with “.gif”, this command would do the job:

**Fig??\.gif**

when using the question mark wildcard bear in mind that it will only work in the number of question marks matches up with the number of characters in the filename. For instance, the previous example with three “Fig12.gif” all right, but it would not match with “Fig1.gif” or “Fig100.gif”. These would both be catered for by this command:

**Fig*.gif**

there is a third wildcard in Linux, which is the square bracket. In MS-DOS the third wildcard has the same effect, but to know a pair of square brackets ([ ]). Suppose you wanted to know which files called “fig6a.gif”, “fig6b.gif” and “fig6c.gif”. You could search for specifically for these files using the square brackets:

**fig6[abc].gif**

under most circumstances there is probably no point in using the square brackets, but they can be useful in circumstances where the other wildcards would not be specific enough.

# Copying files

files are copied using the cp command, which must specify the file to be copied and its destination directory. The copy retains the filename of the original. This example would copy the file called “test” from the current directory to the /root directory:

**cp test /root**

This assumes that the file called “test” is in the current directory. If the source file is in the current directory the full path must be supplied in addition to the filename, as in this example:

**cp /bin/test /root**

Use “.” as the destination directory if you wish to copy a file from another directory to the current directory. This command would copy the file called “test” in the /bin directory into the current directory:

**cp /bin/test .**

The name of the file can be changed during the copy operation, and it is just a matter of giving the new file name when specifying the destination in the file called “nice” in the /bin directory is copied to the current directory as the file called “bad”. Of course, if “bad” was a directory, the file would be copied into this directory under its original name.

**cp /bin/nice /bad**

It is possible to copy several files from one directory to another by specifying several source files in the cp command. This command will copy the files called “test” and “test1” from the current directory to the /root directory:

**cp test test1 /root**

Rather than copying a file you can simply move it using the mv instruction. This operates in much the same way as the cp command, but the original file is deleted. This command would copy the file called temp in the /usr directory to the /usr/temp/:

**mv /usr/temp / ./**

This version of the command has the same effect, but the moved file is renamed “hello” during the move.

**mv /usr/temp /hello**

If a complete directory or even a directory structure must be copied, the mv or cp can test with the “-R” option argument. This example would copy all the directories and files in the /usr directory as a subdirectory of the current directory. The directory and file names remain unaltered.

**cp -R /usr/test_ ./**

An entire directory or directory structure can be moved using the mv command, and the -r modifier is not needed. This command has the same effect as the previous example, but the original directory structure is removed.

**mv /usr/test ./**

There would seem to be no Linux equivalent to the MS-DOS diskcopy command, and Linux is less disc oriented than MS-DOS. The contents of a disc are copied to another disc by rundiskcopy means of course.