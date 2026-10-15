# Table 2.1 C and TC Shell Syntax and Constructs (continued)

|  |  |
|---|---|
| Wildcards | There are some characters that are evaluated by the shell in a special way. They are called shell metacharacters or "wildcards." These characters are neither numbers nor letters. For example, the *, ?, and [ ] are used for filename expansion. The ! is the history character, the <, >, >>, &, and | symbols are used for standard I/O redirection and pipes. To prevent these characters from being interpreted by the shell they must be quoted with a backslash or quote marks.

**EXAMPLE**

`rm *; ls ??; cat file[1-3]; !!`
`echo "How are you?"`
`echo Oh boy!` |
| Displaying output | To print output to the screen, the echo command is used. Wildcards must be escaped with either a backslash or matching quotes.

**EXAMPLE**

`echo "Hello to you!!"` |
| Local variables | Local variables are in scope for the current shell. When a script ends or the shell exits, they are no longer available; i.e., they go out of scope. Local variables are set and assigned values.

**EXAMPLE**

`set variable_name = value`
`set name = "Tom Jones"` |
| Global variables | Global variables are called environment variables. They are set for the currently running shell and are available to any process spawned from that shell. They go out of scope when the script ends or the shell where they are defined exits.

**EXAMPLE**

`setenv VARIABLE_NAME value`
`setenv PRINTER Shakespeare` |
| Extracting values from variables | To extract the value from variables, a dollar sign is used.

**EXAMPLE**

`echo $variable_name`
`echo $name`
`echo $PRINTER` |
| Reading user input | The special variable $ < reads a line of input from the user and assigns it to a variable.

**EXAMPLE**

`echo "What is your name?"`
`set name = $ <` |