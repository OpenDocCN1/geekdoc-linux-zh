This statement closes file descriptor 3, preventing it from being used any more in the script.
Here's an example of what happens when you try to use a closed file descriptor:

```
$ cat badtest
!/bin/bash
# testing closing file descriptors
\exec 3>test17file

echo "This is a test line of data" >&3
\exec 3>&-

echo "This won't work" >&3
$.badtest
./badtest: 3: Bad file descriptor
$
```

Once you close the file descriptor, you can't write any data to it in your script or the shell produces an error message.

There's yet another thing to be careful of when closing file descriptors. If you open the output file line on your script, the shell replaces the existing file with a new file. This means that if you output any data, it will overwrite the existing file. Here's an example of this problem:

```
$ cat test17
!/bin/bash
# testing closing file descriptors

exec 3>test17file
echo "This is a test line of data" >&3
exec 3>&-

cat test17file

exec 3>test17file
echo "This'll be bad" >&3
$.test17
This is a test line of data`
$ cat test17file
This'll be bad
$
```

After sending a data string to the test17file and closing the file descriptor, the script uses the cat command to display the contents of the file. So far, so good. Next, the script reopens the output file and sends another data string to it. When you display the contents of the output file, all you'll see the second data string. The shell overwrite the original output file.