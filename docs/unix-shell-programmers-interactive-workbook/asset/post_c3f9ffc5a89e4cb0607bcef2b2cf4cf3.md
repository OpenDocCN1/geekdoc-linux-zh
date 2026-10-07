
## 230 Lab 5.1: Parameters

Use single quotes where you want to prevent the shell from evaluating what look like variable references, use either single or double quotes where you want the shell to preserve spaces inside a parameter, and use double quotes where you want the shell to do variable substitution.

## 5.1.4 ANSWERS

Run this command from the command line to print the values of the three special variables #, @, and *:

```
print $$: $: $*
```

- a) Is the variable # defined? How many parameters were passed to ksh when it started running?

Answer: Yes, # is defined, and its value is 0. Your interaction should look like the following:

```
[5028]: print $$: $: $*
0 :
[5029]:
```

Note the colon ( : ) immediately after the 0 in the output. That tells us the zero is the value of # rather than one of the other parameters, which are both empty strings. (Note the position of the colons in the print command line.)

Use a set command to set the positional parameters to the message, My name is "Your Name." Use quotes so your first and last name, separated by five spaces, will be one parameter value.

Print the values of the special variables #, @, and *. (Use separate print commands.)

- b) What are the values of the three variables now?

Answer: # is 4, and the four arguments are "My", "name", "is", and "Your Name." Your interaction should look like the following:

```
[5029]: set -- My name is "Your Name."
[5030]: print $$
```

```
[5031]: print "$@"
My name is Your Name.
[5032]: print "$*",
```

## Chapter 5: Parameters

My name is Your Name. [5033]:

This question confirms that the set command can be used to give values to positional parameter variables that you can reference #, @, and *.

![](img/694fa9f0320e707804a4c650b96a09b4_250_0.png)

You should know how the output would have been different if you did not put quotes around $@ and $* in the print command. If not, you need to review the previous exercise.

![](img/694fa9f0320e707804a4c650b96a09b4_250_1.png)

Putting a double dash after the set command name is a good habit to get into so you won't get tripped up when the first parameter looks like an option parameter.

Now run s513 as a parameter and again using $*. Do not put any quotes in your command line.

- c) How many positional parameter variables are passed in both cases, and what are their values?

Answer: Both @@ and $* are passed as five arguments, the words My, name, Your, and Name. Your interaction should look like the following:
[5033]: s513 $@
# is 5
$@ is My name is Your Name
$* is My name is Your Name
[5034]: s513 $**
# is 5
$@ is My name is Your Name
$* is My name is Your Name
[5035]:

The value of variable 4 for the command line has been split into two values when passed to the script. Note also that the five spaces between Your and Name have been reduced to one.

Finally, to see the difference between @ and *, repeat the last two commands, but put $@ and $* inside double quotes. Note the number of parameters passed and how the spaces between your first and last names are handled.

## Lab 5.1: Parameters

- d) What is the difference between these two special variables?

Answer: The difference is that a reference to @@ inside double quotes is passed as separated arguments, but a reference to $* inside double quotes is passed as a single argument.

Your interaction should look like the following:

```
[5035]: s513 "@"
$# is 4
$@ My name is Your Name
$* My name is Your Name
[5036]: s513 "$*"
$# is 1
$@ is My name is Your Name
$* is My name is Your Name
[5037]:
```

Now "@" is passed as four variables, but "*" is passed as one variable. The spaces inside parameter 4 are preserved in both cases.

> Summary: If you want to pass positional parameters to a script with embedded spaces preserved, put double quotes around the references to @ and *. If you want to preserve embedded spaces and pass the positional parameters as separate values, use "$@", but if you want to pass a single parameter containing all the positional parameters, use "*$". You will find this distinction most useful when you are using loops, which will be covered in Chapter 8, "Loops".

![](img/694fa9f0320e707804a4c650b96a09b4_251_0.png)

## 5.1.5 ANSWERS

Use set to give the values red, white, and blue to positional parameter variables through 3. Print $$ and @$, run the shift command, and print $$ and @$ again. Repeat the shift and print commands three more times.

- a) What happens to variable 1 each time you run shift?

Answer: Variable 1, containing the left-most parameter, is discarded and replaced by the value of the next parameter to the right each time.

Your interaction should look like the following:

```
[5037]: set red white blue
[5038]: print $$: @$
```

## Chapter 5: Parameters 233

```
3: red white blue
[5039]: shift
[5040]: print #: $@
2: white blue
[5041]: shift
[5042]: print #: $@
1: blue
[5043]: shift
[5044]: print #: $@
0
[5045]:
```

Command number 5037 assigns the values red, white, and blue to positional parameter variables 1, 2, and 3. Then the print command on line 5038 confirms that there are three variables with the values specified. The first shift command on line 5039 removes red, leaving two parameters, white and blue, as the print command on line 5040 confirms. At this point, the value of variable 1 is white, and the red value has lost.

Set the positional parameters to the seven colors of the rainbow in the order red, orange, yellow, green, blue, indigo, and violet. Use a single shift command to get rid of red, orange, yellow, and then print what's left.

- b) What commands did you use, and what was the result?

Answer: The four colors green, blue, indigo, and violet should remain after running the following commands.
[5045]: set red orange yellow green blue indigo violet
[5046]: shift 3
[5047]: print $@
green blue indigo violet
[5048]:

The set command replaces all parameter variables with the seven values shown and sets the special variable # to 7. Shifting away three variables (line 5046) leaves the four shown by the print command.

- c) What happens if you try to shift away more variables than there are?

Answer: The shell reports a "bad number" error, as the following illustrates:
[5048]: shift 5
ksh: shift: bad number
[5049]:

## 234 Lab 5.1: Parameters

[5050]: print $$: $@
[5051]:

You can shift all variables away, but not more than there are. Line 5050 shows that # is now empty.

## 5.1 SELF-REVIEW QUESTIONS

To test your progress, you should be able to answer the following:

- 1) What would be the value of # when the following line is:
myfunc
a) The empty string.
b) 0
c) 1
d) 2
e) 5

- 2) Assume myfunc is defined in a file named ~/fun/myfunc, what happens the first time you run myfunc?
a) The shell prints a "not found" message.
b) The shell executes ~/bin/myfunc.
c) The shell executes ~/fun/myfunc.
d) The shell executes ~/fun/myfunc then executes the defined function.
e) The shell executes ~/bin/myfunc then executes ~/fun/myfunc.

## Chapter 5: Parameters 235

- 3) Again assuming myfunc is defined in a file named ~/fun/myfunc, what happens the second time you run myfunc?
a) Nothing, because the shell knows it has already executed this file.
b) Nothing, because the shell knows it has already executed this function.
c) Nothing, because the shell knows it has already executed ~/bin/myfunc.
d) The shell executes ~/fun/myfunc then executes the defined function.
e) The shell executes the already-defined function, myfunc.

- 4) After running myfunc the first time, you can modify or delete ~/fun/myfunc and the shell will continue to use the definition it found the first time you ran it.
a) True
b) False

- 5) What is the difference between "@" and "*" as a parameter to a command?
a) There is no difference because they are in quotes.
b) The positional parameters will be passed as separate values using "@", but will be passed as a single value using "*".
c) The positional parameters will be passed as separate values using "*", but will be passed as a single value using "@".
d) "@" reverses the order of the parameters, but "*" does not.
e) "*" reverses the order of the parameters, but "@" does not.

- 6) What is the difference between $@ and $* as a parameter to a command?
a) There is no difference because neither is in quotes.
b) The positional parameters will be passed as separate values using $@, but will be passed as a single value using $.*
c) The positional parameters will be passed as separate values using $*, but will be passed as a single value using $@.
d) $@ reverses the order of the parameters, but $* does not.
e) $* reverses the order of the parameters, but $@ does not.
