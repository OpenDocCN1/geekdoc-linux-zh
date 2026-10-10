The script uses the exec command to redirect file descriptor 3 to an alternative file location. When the script executes the echo statements, they display on STDOUT as you would expect. However, the echo statements that you redirect to file descriptor 3 go to the alternative file. This allows you to keep normal output for the monitor and redirect special information to files, such as log files.
You can also use the exec command to append data to an existing file instead of creating a new file:

exec 3>>test13out

Now the output is appended to the test13out file instead of creating a new file.

# Redirecting file descriptors

Here's the trick to help you bring back a redirected file descriptor. You can assign an alternative file descriptor to a standard file descriptor, and vice versa. This means that you can redirect the original location of STDOUT to an alternative file descriptor and then redirect that file descriptor back to STDOUT. This might sound somewhat complicated, but in practice it's fairly straightforward. This example will clear things up for you:

```
$ cat test14
#!/bin/bash
# storing STDOUT, then coming back to it
exec 3>&1
exec 1>test14out

echo "This should store in the output file"
echo "along with this line."

exec 1>&3

echo "Now things should be back to normal"
$ . ./test14
Now things should be back to normal
$ cat test14out
This should store in the output file
along with this line.
```