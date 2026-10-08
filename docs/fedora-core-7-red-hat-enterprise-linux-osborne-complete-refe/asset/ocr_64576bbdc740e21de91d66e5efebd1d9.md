The standard input piped into a command can be more carefully controlled with the standard input argument (`-`). When you use the dash as an argument for a command, it represents the standard input.

# # Redirecting and Piping the Standard Error: `>`, `2>`

When you execute commands, an error could possibly occur. You may give the wrong number of arguments, or some kind of system error could take place. When an error occurs, the system issues an error message. Usually such error messages are displayed on the screen, along with the standard output. Linux distinguishes between standard output and error messages, however. Error messages are placed in yet another standard byte stream, called the *standard error*. In the next example, the `cat` command is given as its argument the name of a file that does not exist, `myintro`. In this case, the `cat` command simply issues an error:

```
```
$ cat myintro
cat : myintro not found
$
```
```

Because error messages are in a separate data stream from the standard output, error messages still appear on the screen for you to see even if you have redirected the standard output to a file. In the next example, the standard output of the `cat` command is redirected to the file `mydata`. However, the standard error, containing the error messages, is still directed to the screen.

```
```
$ cat myintro > mydata
cat : myintro not found
$
```
```

You can redirect the standard error, as you can the standard output. This means you can save your error messages in a file for future reference. This is helpful if you need a record of the error messages. Like the standard output, the standard error has the screen device for its default destination. However, you can redirect the standard error to any file or device you choose using special redirection operators. In this case, the error messages will not be displayed on the screen.

Redirection of the standard error relies on a special feature of shell redirection. You can reference all the standard byte streams in redirection operations with numbers. The numbers 0, 1, and 2 reference the standard input, standard output, and standard error, respectively. By default, an output redirection, `>`, operates on the standard output, 1. You can modify the output redirection to operate on the standard error, however, by preceding the output redirection operator with the number 2. In the next example, the `cat` command again will generate an error. The error message is redirected to the standard byte stream represented by the number 2, the standard error.

```
```
$ cat nodata 2> myerrors
$ cat myerrors
cat : nodata not found
$
```
```