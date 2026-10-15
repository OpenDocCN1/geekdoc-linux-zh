
```
exit 1
else
    directory="$1"    # If one command line argument and it is a
                        # directory, prepare to perform the task
fi
# Get file count in the given directory; for empty directory,
# display a
# message and quit.
file_count=`ls $directory | wc -w`  # Get count of files in the
                                    # directory
if [ $file_count -eq 0 ]            # If no files, display error
                                    # message
then
    echo "$directory: Empty directory."
    exit 0
fi
# For each file in the directory specified, add the file size
# to the running total. The more command is used to output file
# names one per line so can read command can be used to read
# file names.
sum=0 # Running sum initialized to 0.
ls "$directory" | more |
while read file
do
    file="$directory"/"$file"  # Store the relative path name for
                                  # each file
    if [ -f "$file" ]            # If it is an ordinary file
    then # then
        set -- `ls -l "$file"`  # Set command line arguments
        sum=`expr $sum + $5`      # Add file size to the running
                                  # total.
    fi
# Code to decrement the file_count variable and display the
# final sum if the last file has been processed.
if [ "$file_count" -gt 1 ] # Are more files left? If so,
                            # continue.
then
    file_count=`expr $file_count - 1`
else
# Spell out the current directory
if [ "$directory" = "." ]
then
    directory="your current directory"
fi
echo "The size of all ordinary files in $directory is $sum bytes."
```
```
fi
done
exit 0
$ 
$ pwd
/home/sarwar/unix3e/ch13
$ ./fs /bin
Usage: ./fs [directory name]
$ ./fs unix3e
unix3e: File does not exist
$ ./fs ~/unix3e
The size of all ordinary files in /home/sarwar/unix3e is 0 bytes.
$ ./fs ..
The size of all ordinary files in .. is 0 bytes.
$ ./fs .
The size of all ordinary files in your current directory is 4716 bytes.
$ ./fs /
The size of all ordinary files in / is 10238 bytes.
$ ./fs /bin
The size of all ordinary files in /bin is 1635367 bytes.
$ ./fs dir1
dir1: Empty directory.
$
```

## EXERCISE 13.1

Create the addall script in your directory and run it with the first 10 numbers in the Fibonacci series. What is the result? Does the program produce the correct result? If you are not familiar with the Fibonacci series, browse through the following website: http://en.wikipedia.org/wiki/Fibonacci_number.

## 13.3 THE HERE DOCUMENT

The here document feature of the Bourne shell allows you to redirect standard input of a command in a script and attach it to data within the script, wrapped in a particular format, as will be explained. Obviously, this feature works with commands that take input from standard input. The feature is used mainly to display menus, although there are some other important uses of this feature. The advantage of maintaining data within the script is that it eliminates extra file operations such as open and read that would be required if the

data was maintained in a separate file. The result is a much faster program. The following is a brief description of the here document.

### SYNTAX

```
command << [-] input_marker
... input data ...
input_marker
```

Purpose: To execute command with its input coming from the here document—data between the input start and end markers input_marker

The input_marker is a string that you choose to wrap the input data in for command. The closing marker must be on a line by itself and cannot be surrounded by any spaces. The command and variable substitutions are performed before the here document data is directed to stdin of the command. Quotes can be used to prevent these substitutions or to enclose any quotes in the here document. input_marker can be enclosed in quotes to prevent any substitutions in the entire document, as in:

```
command << 'Marker'
...
'Marker'
```

A hyphen (-) after << can be used to remove leading tabs (not spaces) from the lines in the here document and the marker that ends the here document. This feature allows the here document and the delimiting marker to conform to the indentation of the script. The following session illustrates this point:

```
while [ ... ] do
grep ... <<- DIRECTORY
    John Doe ...
    ...
    Art Pohn ... DIRECTORY
...
done
```

One last, but very important point: output and error redirections of the command that uses the here document must be specified in the command line, not following the marker that ends the here document. The same is true of connecting the standard output of the command with other commands via a pipeline, as shown in the following session. Note that the grep ... <<- DIRECTORY 2> errorfile | sort command can be replaced by (grep ... 2> errorfile | sort) <<- DIRECTORY.

```
while [ ... ] do
    grep ... <<- DIRECTORY 2> errorfile | sort John Doe ...
```
