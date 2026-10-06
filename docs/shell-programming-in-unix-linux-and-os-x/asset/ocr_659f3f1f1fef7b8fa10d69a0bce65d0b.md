$ mycp prog1 prog2    Simple case
$ mycp prog1 bin      Copy into directory
bin/prog1 already exists; (yes/no)? yes

# A Final Version of mycp

The last modification to mycp makes the program virtually equivalent to the standard Linux
 command by allowing a variable number of arguments. Recall that with the standard
command any number of files can precede the name of a directory, as in
c prog1 prog2 greetings bin

To modify mycp to accept any number of files in a similar format, you can use this approach:

+   1. Get each argument but the last from the command line and store it in the shell variable
elist.
2. Store the last argument in the variable to.
3. If $to is not a directory, test the argument count as there must be exactly two arguments.
4. If $to is a directory, for each file in $filelist, check whether the file already exists in
t destination directory. If it doesn't, add the filename to the variable copylist. If the answer is yes,
it it exists, ask the user whether the file should be overwritten.
add the filename to copylist.
5. If copylist is non-null, copy the files in it to $to.

If this algorithm seems a bit fuzzy, the program and a detailed explanation will help clear
tings up. Note the modified command usage message.

```
$ cat mycp
#
# Copy a file -- final version
#
```

```
numargs=$#    # save this for later use
filelist=
copylist=

#
# Process the arguments, storing all but the last in filelist
#
while [ "$#" -gt 1 ]; do
  filelist="$filelist $1"
  shift
```