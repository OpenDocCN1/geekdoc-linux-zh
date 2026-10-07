+   A for loop cycles through a number of values comparing them to a variable or a constant. When the list has been exhausted, the loop ends. A simple for loop looks like this:

```
#set the maximum length to 0
$maxlength= 0 ;
#cycle through each length and compare it to the maxlength
foreach (keys %in) {
    $maxlength= length if length > $maxlength;
}
#increment the maxlength variable
$maxlength++;
```

+   A while loop continues to cycle through performing whatever function is contained therein until the while statement is no longer true. A simple while loop looks like this:

```
while ($variable <= 3) {
    change_variable;
}
```

There are several ways to initiate a Perl script. First, you may call the Perl interpreter with the script name as an argument, like so:

```
$usr/bin/perl scriptname
```

You may also cat the script into the Perl interpreter, like this:

```
Scat scriptname | perl
```

Unfortunately, both of these initiation methods require that you know that this particular command is a Perl script and not a Python script, Bash script, or compiled executable. It is far easier, given the number of commands available on a Linux system, to execute the Perl script by using the script name as a program executable. Your shell facilitates this if you have set the permissions string to make the script executable and have included an interpreter line in the following format as the first line of the script:

```
#!usr/bin/perl [optional arguments]
```