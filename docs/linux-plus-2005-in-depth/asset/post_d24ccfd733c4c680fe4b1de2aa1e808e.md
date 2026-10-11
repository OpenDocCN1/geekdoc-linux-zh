
## The if Construct

The most common type of decision construct is known as the `if` construct; the syntax of the `if` construct is shown next:

```bash
if this is true
   then
      do these commands
   elif this is true
   then
      do these commands
   else
      do these commands
   fi
```

Some common rules govern `if` constructs:

- 1. `elif` (else if) and `else` statements are optional.
- 2. You can have an unlimited number of `elif` statements.
- 3. The *do these commands* section can consist of multiple commands, one per line.
- 4. The *do these commands* section is typically indented from the left-hand side of the text file for readability, but does not need to be.
- 5. The end of the statement must be a backward “`if`” (`fi`).
- 6. The *this is true* part of the `if` syntax shown earlier can be a command or a test statement:
    - Commands return true if they perform their function properly.
    - Test statements are enclosed within square brackets `[ ]` or prefixed by the word “test” and used to test certain conditions on the system.

An example of using a basic `if` construct to ensure that the /etc/hosts file is only copied to the /etc/sample directory if that directory could be created successfully is shown in the following output:

```bash
[root@server1 root]# cat testmkdir
#!/bin/bash
if mkdir /etc/sample
then
    cp /etc/hosts /etc/sample
    echo "The hosts file was successfully copied to /etc/sample"
else
    echo "The /etc/sample directory could not be created."
fi
```

```bash
[root@server1 root]# chmod a+x testmkdir
[root@server1 root]# ./testmkdir
The hosts file was successfully copied to /etc/sample
[root@server1 root]#
```

In the preceding output, the `mkdir /etc/sample` command is always run; if it runs successfully, the shell script proceeds to the `cp /etc/hosts /etc/sample` and `echo "The hosts file was successfully copied to /etc/sample"` commands. If the `mkdir /etc/sample` command was unsuccessful, the shell script skips ahead and executes the `echo "The /etc/sample directory could not be created."` command. If there were more lines of text following the `fi` in the preceding shell script, they are executed after the `if` construct regardless of its outcome.

Often, it is useful to use the `if` construct to alter the flow of the program given input from the user. Recall the `myscript` shell script used earlier:

```bash
[root@server1 root]# cat myscript
#!/bin/bash
echo -e "Today's date is: \c"
date
echo -e "\nThe people logged into the system include:"
who
echo -e "\nthe contents of the / directory are:"
ls -F /
[root@server1 root]#
```

To ask the user whether to display the contents of the `/` directory, you could use the following `if` construct in the `myscript` file:

```bash
[root@server1 root]# cat myscript
#!/bin/bash
echo -e "Today's date is: \c"
date
echo -e "\nThe people logged into the system include:"
who
echo -e "\nWould you like to see the contents of /?(y/n)...\)\c"
read ANSWER
if [ $ANSWER = "y" ]
then
    echo -e "\nthe contents of the / directory are:"
    ls -F /
fi
[root@server1 root]# ./myscript
Today's date is: Sat Jun  4 09:13:31 EDT 2005

The people logged into the system include:
root  pts/0  Jun  1 08:44 (3.0.0.2)
```

Would you like to see the contents of /? (y/n) -> **y**

The contents of the / directory are:

```
bin/    etc/     lib/    mnt/    root/    sys/    udev/
boot/   home/    lost+found/    opt/    sbin/    tftpboot/   usr/
dev/    initrd/   misc/    proc/    selinux/   tmp/    var/
[root@server1 root]# _
```

Notice from the preceding output that the test statement `[ $ANSWER = "y" ]` is used to test whether the contents of the `ANSWER` variable are equal to the letter “y.” Any other character in this variable causes this **test statement** to return false and the directory listing is then skipped altogether. The type of comparison used previously is called a string comparison because two values are compared for strings of characters; it is indicated by the operator of the test statement, which is the equal sign (`=`) in this example. Table 8-5 shows a list of common operators used in test statements and their definitions.

> **NOTE**
>
> The test statement `[ $ANSWER = "y" ]` is equivalent to the test statement `test $ANSWER = "y"`.
>
> It is important to ensure that there is a space character after the beginning square bracket and before the ending square bracket; otherwise, the test statement produces an error.

**Table 8-5 Common test statements**

| Test Statement | Returns true if: |
| :--- | :--- |
| `[ A = B ]` | String A is equal to String B. |
| `[ A != B ]` | String A is not equal to String B. |
| `[ A -eq B ]` | A is numerically equal to B. |
| `[ A -ne B ]` | A is numerically not equal to B. |
| `[ A -lt B ]` | A is numerically less than B. |
| `[ A -gt B ]` | A is numerically greater than B. |
| `[ A -le B ]` | A is numerically less than or equal to B. |
| `[ A -ge B ]` | A is numerically greater than or equal to B. |
| `[ -r A ]` | A is a file/directory that exists and is readable (r permission). |
| `[ -w A ]` | A is a file/directory that exists and is writable (w permission). |
| `[ -x A ]` | A is a file/directory that exists and is executable (x permission). |
| `[ -f A ]` | A is a file that exists. |
| `[ -d A ]` | A is a directory that exists. |

You can also combine any test statement together with another test statement using the special comparison operators `-o` (OR) and `-a` (AND) or reverse the meaning of a test statement with the `!` (NOT) operator; examples of using these operators in test statements are listed in Table 8-6.

> **NOTE**
>
> There can be several `-o`, `-a`, and `!` operators in one test statement.

**Table 8-6 Special operators in test statements**

| Test Statement | Returns true if: |
| :--- | :--- |
| `[ A = B -o C = D ]` | String A is equal to String B OR String C is equal to String D. |
| `[ A = B -a C = D ]` | String A is equal to String B AND String C is equal to String D. |
| `[ ! A = B ]` | String A is NOT equal to String B. |

Considering the `myscript` shell script, you can proceed with the directory listing if the user enters "y" or "Y" in the following example:

```bash
[root@server1 root]# cat myscript
#!/bin/bash
echo -e "Today's date is: \c"
date
echo -e "\nThe people logged into the system include:"
who
echo -e "\nWould you like to see the contents of /?([y/n]->)\c"
read ANSWER
if [ $ANSWER = "y" -o $ANSWER = "Y" ]
then
    echo -e "\nThe contents of the / directory are:"
    ls -F /
fi
```

```bash
[root@server1 root]# ./myscript
Today's date is: Sat Jun  4 09:13:31 EDT 2005

The people logged into the system include:
root    pts/0      Jun  1 08:44 (3.0.0.2)

Would you like to see the contents of /?(y/n) -> Y

The contents of the / directory are:
bin/     etc/     lib/      mnt/     root/    sys/       udev/
boot/    home/    lost+found/  opt/     sbin/    tftpboot/  usr/
dev/     initrd/  misc/     proc/    selinux/ tmp/       var/
[root@server1 root]# _
```

## The case Construct

The `if` construct used earlier is well suited for a limited number of choices. But consider the `myscript` example used earlier, this time with several `elif` statements to perform different tasks based on the user input:

```bash
[root@server1 root]# cat myscript
#!/bin/bash
echo -e "What would you like to see?
Todays date (d)
Currently logged in users (u)
The contents of the / directory (r)"

Enter your choice(d/u/r)->c"
read ANSWER
if [ $ANSWER = "d" -o $ANSWER = "D" ]
then
    echo -e "Today's date is: \c"
    date
elif [ $ANSWER = "u" -o $ANSWER = "U" ]
then
    echo -e "\nThe people logged into the system include:"
    who
elif [ $ANSWER = "r" -o $ANSWER = "R" ]
then
    echo -e "\nThe contents of the / directory are:"
    ls -F /
fi
[root@server1 root]# _
```

```bash
[root@server1 root]# ./myscript
What would you like to see?
Todays date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice(d/u/r/)-> d
Today’s date is: Sat Jun  4 11:10:03 EDT 2005
[root@server1 root]# _
```

The preceding shell script becomes increasingly difficult to read as the number of choices available increases. Thus, when presenting several choices, it is commonplace to use a `case` construct. The syntax of the `case` construct is shown next:

```bash
case variable in
    pattern1 ) do this
              ;;
    pattern2 ) do this
              ;;
    pattern3 ) do this
              ;;
esac
```

The `case` statement compares the value of a variable with several different patterns of text or numbers. If there is a match, the commands to the right of the pattern are executed (*do this* in the preceding syntax). As with the *if* construct, the *case* construct must be ended by a backward “case” (*esac*).

An example that simplifies the previous `myscript` example by using the `case` construct is shown in the following output:

```bash
[root@server1 root]# cat myscript
#!/bin/bash

echo -e "What would you like to see?
Todays date (d)
Currently logged in users (u)
The contents of the / directory (r)

Enter your choice(d/u/r/->)c*"
read ANSWER

case $ANSWER in
    d | D )  echo -e "\nToday’s date is: \c"
              date
              ;;
```
