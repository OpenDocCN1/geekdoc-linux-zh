# Table 2.2 Bourne Shell Syntax and Constructs (continued)

|  |  |
|---|---|---|
| Wildcards | There are some characters that are evaluated by the shell in a special way. They are called shell metacharacters or "wildcards". These characters are neither numbers nor letters. For example, the *, ?, and [ ] are used for filename expansion. The <, >, 2>, >>, and | symbols are used for standard I/O redirection and pipes. To prevent these characters from being interpreted by the shell they must be quoted.

**EXAMPLE**
Filename expansion:
rm *; ls ??; cat file[1-3];

Quotes protect metacharacter:
echo "How are you?" |
| Displaying output | To print output to the screen, the echo command is used. Wildcards must be escaped with either a backslash or matching quotes.

**EXAMPLE**
echo "what is your name?" |
| Local variables | Local variables are in scope for the current shell. When a script ends, they are no longer available; i.e., they go out of scope. Local variables are set and assigned values.

**EXAMPLE**
variable_name=value
name="John Doe"
x=5 |
| Global variables | Global variables are called environment variables. They are set for the currently running shell and any process spawned from that shell. They go out of scope when the script ends.

**EXAMPLE**
VARIABLE_NAME=value
export VARIABLE_NAME

PATH=/bin:/usr/bin:.
export PATH |
| Extracting values from variables | To extract the value from variables, a dollar sign is used.

**EXAMPLE**
echo $variable_name
echo $name
echo $PATH |