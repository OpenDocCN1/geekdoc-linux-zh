There is nothing intrinsically wrong with these two lines, as long as the directory named in the variable, dir_name, exists. But what happens if it does not? In that case, the cd command fails and the script continues to the next line and deletes the files in the current working directory. Not the desired outcome at all! The hapless administrator destroyed an important part of the server because of this design decision.

Let's look at some ways this design could be improved. First, it might be wise to make the execution of rm contingent on the success of cd:

```
cd $dir_name && rm *
```

This way, if the cd command fails, the rm command is not carried out. This is better, but still leaves open the possibility that the variable, dir_name, is unset or empty, which would result in the files in the user's home directory being deleted. This could also be avoided by checking to see that dir_name actually contains the name of an existing directory:

```
[[-d $dir_name ]] && cd $dir_name && rm *
```

Often, it is best to terminate the script with an error when an situation such as the one above occurs:

```
# Delete files in directory $dir_name
if [[ ! -d "$dir_name" ]]; then
  echo "No such directory: '$dir_name'" >&2
  exit 1
fi
if ! cd $dir_name; then
  echo "Cannot cd to '$dir_name'" >&2
  exit 1
fi
if ! rm *; then
  echo "File deletion failed. Check results" >&2
  exit 1
fi
```

Here, we check both the name, to see that it is that of an existing directory, and the success of the cd command. If either fails, a descriptive error message is sent to standard error and the script terminates with an exit status of one to indicate a failure.