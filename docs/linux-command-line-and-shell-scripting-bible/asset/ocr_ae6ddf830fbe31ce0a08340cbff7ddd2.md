The -s option prevents the data entered in the read command from being displayed on the monitor (actually, the data is displayed, but the read command sets the text color to the same as the background color). Here's an example of using the -s option in a script:

```
$ cat test27
#!/bin/bash
# hiding input data from the monitor

read -s p "Enter your password: " pass
echo
echo "Is your password really $pass?"
$ ./test27
Enter your password:
Is your password really T3stling?
$
```

The data typed at the input prompt doesn't appear on the monitor but is assigned to the variable just for use in the script.

# Reading from a file

Finally, you can also use the read command to read data stored in a file on the Linux system. Each call to the read command reads a single line of text from the file. When there are no more lines left in file, the read command will exit with a non-zero exit status.

The tricky part of this is getting the data from the file to the read command. The most common method for doing this is to pipe the result of the cat command of the file directly to a while command that contains the read command. Here's an example of how to do this:

```
$ cat test28
#!/bin/bash
# reading data from a file
```

```
count=1
cat test | while read line
do
	echo "Line $count: $line"
	count=$[$count + 1]
done
	echo "Finished processing the file"
$ cat test
The quick brown dog jumps over the lazy dog.
This is a test, this is only a test.
0 Romeo Romeo, Romeo! wherefore art thou Romeo?
$ ./test28
Line 1: The quick brown dog jumps over the lazy dog.
Line 2: This is a test, this is only a test.
```