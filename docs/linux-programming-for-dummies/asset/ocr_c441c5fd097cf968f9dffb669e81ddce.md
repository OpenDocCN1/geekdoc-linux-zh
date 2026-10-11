# Problems with Sending Arguments

![](bbox=[0.08, 0.18, 0.16, 0.26])

Two common problems can occur whenever anyone sends your program or subprogram arguments: Someone can send you the wrong number of arguments or the wrong kind of arguments.

# The wrong number of arguments

You can plan to receive a fixed number of arguments, but nothing forces someone to send you the correct number. Suppose that your program expects the following two arguments:

```
```bash
#!/bin/bash
echo "First Name: $1"
echo "Last Name: $2"
```
```

Now suppose that someone supplies only one of those arguments, as follows:

```
$ displayname Bob
```

Your program is still telling your computer to use the second data item that it expects to pass to the program — in this case, the phantom data.

# The wrong kind of argument

Your program depends on someone else to pass it the correct information. If this person isn't dependable, your program experiences problems. Say that someone calls your program and sends the following information:

```
$ nanegame car: truck
```

Your program assumes that the information is just what it's looking for in the following example:

```
```bash
#!/bin/bash
echo "First Name: $1"
echo "Last Name: $2"
```
```

But that information isn't what your program expects and your program is using incorrect information. So who's going to get the blame for the problem? The person using your program or the programmer? (Who, you? Why, it's not your fault . . . is it?) You have no easy way to avoid this situation or the blame (except by not answering the phone if the user calls to complain). As long as you note in the documentation of your program that the user needs to enter specific kinds of information at the command prompt as the program runs,