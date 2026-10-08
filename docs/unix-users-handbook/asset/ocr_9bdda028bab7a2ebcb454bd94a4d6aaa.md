# # Shell Functions

As you write shell programs, you will notice that there are certain sets of commands appear in many places within a program. For example, several times in a script, you may check user input and issue an appropriate message if input is invalid. It can be tedious to type the same lines of code in your program numerous times. It can be a nuisance if you later want to change these lines.

Instead, you can you put these commands into a shell function. Functions look and act like a new command that can be used inside the script. Here’s an example of a basic shell function:

```
# This is a function that may be called from anywhere within
# the program. It displays a standard usage error message
# and then exits the program.

print_usage()
{
	echo "Usage:"
	echo "To trash files: $0 [-i] files_to_trash..."
	echo "Display trashed files: $0 -d" -to_trash...
	echo "Remove all trashed files: $0 -rm"
	echo "Print this message: $0 -help"
	exit 1
}
```

**print_usage** is now a new command in your shell program. You can use it anywhere in this script.

Shell functions also have their own set of positional parameters ($1-$9, $#, and $*), so you can pass them arguments just like any other command. The only nuance is that $0 represents the name of the shell program, not the name of the function.

Earlier, we talked about arguments. When you type the name of the shell script, you can supply arguments that are saved in the variables $1 through $9. The first ten words on the command line are