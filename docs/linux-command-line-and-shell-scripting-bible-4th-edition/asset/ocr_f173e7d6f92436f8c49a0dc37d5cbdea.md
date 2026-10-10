Instead of having to write separate if-then statements, you can use an alternative version of the else section called elsif. The elif continues an else section with another if-then statement:

```
if command1
then
commands
elif command2
then
more commands
fi
```

The elif statement line provides another command to evaluate, similar to the original if statement line. If the exit status code from the elif command is zero, Bash executes the commands in the second then statement section. Using this method of nesting provides cleaner code with an easier-to-follow logic flow:

```
$ cat test5.sh
#!/bin/bash
# testing nested ifs - using elif
#
testuser=NoSuchUser
#
if grep $testuser /etc/passwd
then	echo "The user $testuser account exists on this system."
echo "The user $testuser has a directory," 
		echo "even though $testuser doesn't have an account."
fi
echo "We are outside the nested if statements."
$ . /test5.sh
/home/NoSuchUser/
The user NoSuchUser has a directory, even though NoSuchUser doesn't have an account.
We are outside the nested if statements.
$
```

The problem with this script is that if the account is gone as well as the directory, you get no notifications of these facts. You can fix this problem, and even take the script a step further by having it check for