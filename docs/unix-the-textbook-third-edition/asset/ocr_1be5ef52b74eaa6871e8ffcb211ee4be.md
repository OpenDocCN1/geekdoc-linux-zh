arguments can be referenced by using the names $argv[number] where number may assume values 0, 1, 2, and so on, with $argv[0] referring to the program (or command) name. The positional parameters may also be specified by using the $number or ${number} notation, such as $0, $1, $2, and so on, or ${0}, ${1}, ${2}, and so on. The curly braces are used to isolate number from the character(s) that may follow. If a positional argument referenced in your script is not passed as an argument, it is initialized to a value of null. However, while displaying such arguments, the $number notation works fine, but the $argv[number] notation results in an error message, argv: Subscript out of range., which simply means that you are indexing the argv array for an element that does not exist. You can use the names $#argv or $# to refer to the total number of arguments passed in an execution of the script. The names $argv[*], argv, or $* refer to the values of all of the arguments. The names $argv[0] and $0 refer to the name of the script file (i.e., the command name). In the following session, we use the shell script in the cmdargs_demo file to show how you can use these variables.

```
% cat cmdargs_demo
#!/bin/csh
echo "The command name is $0."
echo "The number of command line arguments is $#argv."
echo "-n "The values of the command line arguments are: "
echo "$1 $2 $3 $4 $5 $6 $7 $8 $9 $10 $11 $12"
echo "Another way to display command line arguments is: $argv[*]"
echo "Yet another is: $*"
exit 0
% ./cmdargs_demo 1 2 3 4 5 6 7 8 9 10 11 12
The command name is cmdargs_demo.
The number of command line arguments is 12.
The values of the command line arguments are: 1 2 3 4 5 6 7 8 9 10 11 12
Another way to display command line arguments is: 1 2 3 4 5 6 7 8 9 10 11 12
Yet another is: 1 2 3 4 5 6 7 8 9 10 11 12
% ./cmdargs_demo One Two 3 Four 5 6
The command name is cmdargs_demo.
The number of command line arguments is 6.
The values of the command line arguments are: One Two 3 Four 5 6
Another way to display command line arguments is: One Two 3 Four 5 6
Yet another is: One Two 3 Four 5 6
%
```

The C shell maintains as many as command line arguments at a time as the command line length allows. You can write scripts that handle command line arguments one at a time, by shifting the arguments left by one argument. To do so, use the shift command. By default, this command shifts the command line arguments to the left by one position, moving $argv[2] to $argv[1], $argv[3] become $argv[2], and so on. The