
## The read Command 191

to="$1"

```
#
# If less than two args, or if more than two args and last arg
# is not a directory, then issue an error message
#
if [ "$numargs" -lt 2 -o "$numargs" -gt 2 -a ! -d "$to" ]; then
    echo "Usage: mycp file1 file2"
    echo "mycp file(s) dir"
    exit 1
fi
```

```
#
# Sequence through each file in filelist
#
```

```
for from in $filelist ; do
#
# See if destination file is a directory
#
if [ -d "$to" ]; then
    tofile="$to/$(basename $from)"
else
    tofile="$to"

# Add file to copylist if file doesn't already exist
# or if user says it's okay to overwrite
#
if [ -e "$tofile" ]; then
    echo "$tofile already exists; overwrite (yes/no)? \c"
    read answer

    if [ "$answer" = "yes" ]; then
        copylist="$copylist $from"
    else
        copylist="$copylist $from"
    fi
fi
done
```

```bash
#
# Now do the copy -- first make sure there's something to copy
#
if [ -n "$copylist" ] ; then
    cp $copylist $to      # proceed with the copy
fi
$
```

Let's look at some sample output before delving into the code itself.

> See what's around

```
$ ls -c
bin    lu    names    prog1
prog2
$ ls bin
lu
nu
prog1
```

> And what's in bin?

```
$ mycp
Usage: mycp file1 file2
mycp file(s) dir
$ mycp names prog1 prog2
Usage: mycp file1 file2
mycp file(s) dir
$ mycp names prog2 lu bin
bin/prog1 already exists, overwrite (yes/no)? yes
bin/lu already exists, overwrite (yes/no)? no
$ ls -1 bin
```

> No arguments

```
total 5
-rw-r--r-- steve  543 Jul 19 14:10 lu
-rw-r--r-- steve  949 Jul 21 17:11 names
-rw-r--r-- steve  38 Jul 19 09:55 nu
-rw-r--r-- steve  498 Jul 21 17:11 prog1
-rw-r--r-- steve  498 Jul 21 17:11 prog2
$
```

> Legitimate use

> See what happened

In the last case, mycp was overwritten and lu wasn't, as per the user's request.

When the program starts, it saves the number of arguments in the variable numargs. This is done because the argument variables are changed later in the program by the shift command.

A loop is entered and executed as long as the number of arguments is greater than one. The purpose of this loop is to get the last argument on the line. While doing this, the loop clashes the other arguments into the shell variable filelist, which ultimately will contain a list of all the files to be copied.

```
filelist=$filelist $1
```

## The read Command 193

says to take the previous value of filelist, add on a space followed by the value of $1, and then store the result back into filelist. Then the shift command is executed to "move" all the arguments over by one. Eventually, $# will be equal to one, and the loop will be.

At that point, filelist will contain a space-delimited list of all the files to be copied, and $1 will contain the last argument, which is either the destination filename or directory.

To see this works, consider execution of the while loop when the command is executed as mycp names prog2 lu.

Figure 9.1 depicting the changing values of the variables through each iteration of the loop. The first line shows the state of the variables before the loop enters.

```
$ $1 $2 $3 $4 $5 filelist
5 names prog1 prog2 lu null
4 prog2 lu bin names
3 prog2 lu bin names prog1
2 lu bin names prog1 prog2
1 bin names prog1 prog2.lu
```

Figure 9.1 Processing command arguments

After the loop, the last argument contained in $1 is stored in the variable to. Next test is made to ensure that at least two arguments were typed on the command line, and if more than two were, that the last argument is a directory. If either condition is not satisfied, usage information is displayed to the user, and the program exits with a status of 1.

Following this, the for loop examines each file in the list to see whether it already exists in the destination directory. If it does, the user is prompted as before. If the user wants to overwrite the file—or if the file doesn't exist—the file is added to the shell variable copylist. The technique used here is the same used to accumulate the arguments inside filelist.

When the for loop, copylist contains a list of all the files to be copied. In an extreme case, notice that this can be null if the user decided not to overwrite any files and every file specified exists in the destination directory. Therefore a test is made to ensure copy is non-null, and if it is, the copy is performed.

Take some time to review the logic of the final version of mycp; it illustrates many of the features you've learned in this book. Some exercises at the end of this chapter will also test your understanding of this program.

## A Menu-Driven Phone Program

One useful thing about the read command is that it enables you to write menu-driven shell programs. As an example, let's return to the three book programs we wrote earlier, add, lu, and rem, and create what’s known as a wrapper, a program that makes other programs easier to use. This time we’ll create the wrapper program rolo ("rolo") short for Rolodex, just in case you remember a Rolodex is!

When invoked, rolo will display a list of choices to the user and execute the appropriate program depending on the selection after prompting for the necessary arguments:

```
$ rolo
#
# rolo - rolodex program to look up, add, and
#   remove people from the phone book
#
#
# Display menu
#
echo 'Would you like to:
1. Look up
2. Add to the phone book
3. Remove from the phone book
Please select one of the above (1-3): '
#
# Read and process selection
#
read choice
case "$choice" in
  1)
    # Look up
    lu "$choice"
    ;;
  2)
    # Add to the phone book
    add "$choice"
    ;;
  3)
    # Remove from the phone book
    rem "$choice"
    ;;
  *)
    echo "Bad choice"
    ;;
esac
#
```

## The read Command 195

Notice how a single echo is used to display the newlines. Then read gets the selection and stores it in variable choice. A case statement determines what choice was made. If choice 1 selected, the user wants to look up Note also the double quotes around name are necessary to ensure that more words typed in

When an invalid choice is entered, the program displays Bad choice and terminates. A friendly approach would be to loop around and again prompt the user to proper choice is made. This can be done by enclosing the entire program inside a loop that will be executed until a valid selection is made.

Another change to rolo reflects its most likely usage: Because the most common operation is looking someone up, there will be a tendency to avoid typing rolo, then making selection, then the desired name. Instead, it's a little easier to just type in

directly, let's give some command line arguments so it can also be used efficiently. By default any arguments are specified, rolo will assume a lookup requested and call lu directly, handling all the arguments along. If the user wants to perform a quick lookup, they can type rolo followed by the name. If they want to get the full menu interface, they type rolo offers just that alternative. The preceding two changes (looping until a valid choice is selected and doing a quick lookup) are added to version 2 of rolo:

```bash
$ cat rolo
#
# rolo - rolodex program to look up, add, and
#   remove people from the phone book -- version 2
#

# If arguments are supplied, then do a lookup
#
if [ "$#" -ne 0 ]; then
    lu "$@"
    exit
fi
validchoice="    # set it null
#
# Loop until a valid selection is made
#

until [ -n "$validchoice" ];
do
    #
    # Display menu
    #
    echo 'Would you like to:
1. Look up
2. Add to the phone book
3. Remove from the phone book
Please select one of the above (1-3): '
    read choice
    #
    # Read and process selection
    #
    case "$choice" in
      1)
        # Look up
        lu "$choice"
        ;;
      2)
        # Add to the phone book
        add "$choice"
        ;;
      3)
        # Remove from the phone book
        rem "$choice"
        ;;
      *)
        echo "Bad choice"
        ;;
    esac
done
#
```

## Chapter 9 Reading and Printing Data

Please select one of the above (1-3): 4

Bad choice
$
