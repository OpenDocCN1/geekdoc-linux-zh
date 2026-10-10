there aren't any spaces between the assignment equal sign and the command substitution character. Here's an example of creating a variable using the output from a normal shell command:

```
```
$ cat test5
#!/bin/bash
testing=$(date)
echo "The date and time are: " $testing
$
```
```

The variable testing receives the output from the date command, and it is used in the echo statement to display it. Running the shell script produces the following output:

```
```
$ chmod u+x test5
$ ./test5
The date and time are: Mon Jun 01 15:45:25 EDT 2020
$
```
```

That's not all that exciting in this example (you could just as easily put the command in the echo statement), but once you capture the command output in a variable, you can do anything with it.

Here's a popular example of how command substitution is employed to capture the current date and use it to create a unique filename in a script:

```
```
#!/bin/bash
# copy the /usr/bin directory listing to a log file
today=$(date +%y%m%d)
ls /usr/bin -al> log.$today
```
```

The today variable is assigned the output of a formatted date command. This is a common technique used to extract date information for log filenames. The +%y%m%d format instructs the date command to display the date as a two-digit year, month, and day:

```
```
$ date +%y%m%d
200601
$
```
```

The script assigns the value to a variable, which is then used as part of a filename. The file itself contains the redirected output (discussed later in the “Redirecting Input and Output” section) of a directory listing. After running the script, you should see a new file in your