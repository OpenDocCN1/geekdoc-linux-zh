![](bbox=[0.08, 0.11, 0.72, 0.56])

> **FIGURE 6.12**
> 
> *Example of STDIN* 
> *redirection.*$^4$

To combine the data and error, use either this:
`some_program > data_and_errors.txt 2>&1`
or this shortcut:
`some_program &> data_and_errors.txt`

To send the output from one program into the input of another, you *could* use a convoluted combination of `>` and `<;` but UNIX provides the *pipe* command, `|`, which is much easier. The pipe works like this:
`some_command | another_command`

For example, you can list the running processes, and then search the list for all instances of Firefox:
`ps -A | grep firefox`

If you are of the sort who likes to have your cake and eat it too, the *tee* command will duplicate a stream and send one copy to the display and another to a file. It’s used with the *pipe* command:
`ls -al | tee directory.txt`