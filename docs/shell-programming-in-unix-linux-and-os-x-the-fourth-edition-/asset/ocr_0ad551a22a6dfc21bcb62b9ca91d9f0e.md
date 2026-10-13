```
```text
$ vi newmemo

you have mail
$ mail
From steve Wed Aug 28 17:44:46 EDT 2002
sandy has logged on

?d
$
```
```

*Work continues*

Of course, we could have written `waitfor` to accept the -m option as either the first or second argument, but that’s not how traditional Unix syntax works: all options are expected to precede any other types of arguments on the command line.

Also note that the old version of `waitfor` could have been executed as follows:

```
```sh
$ waitfor sandy | mail steve &
[1] 5522
$
```
```

to achieve the same result as adding the -m option, but it’s considerably less elegant.

The program always sends mail to steve as it’s written now, which isn’t particularly useful if someone else wants to run it. A better way is to determine the user running the program and then send them the mail if they specify the -m option. But how do you do that? One way is to execute the who command with the am i options and get the user name that comes back. You can then use cut to extract the username from the who output and use that name as the recipient of the mail.

All of this can be done in the last if command of waitfor if it’s changed to read as shown:

```
```sh
if [ "$#" -eq 1 ]
then
        echo "$user has logged on"
else
        runner=$(who am i | cut -cl-8)
        echo "$user has logged on" | mail $recipient
fi
```
```

Now the program can be run by anyone, and the mail notification will be sent to the correct recipient.

# More on Loops

# Breaking Out of a Loop

Sometimes program logic dictates an immediate exit from a loop statement. To exit from the loop but not from the program, use the break command:

```
```sh
break
```
```