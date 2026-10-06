# TABLE 1.2 Common redirection operators

| Redirection operator | Effect |
| --- | --- |
| > | Creates a new file containing standard output. If the specified file exists, it's overwritten. |
| >> | Appends standard output to the existing file. If the specified file doesn't exist, it's created. |
| 2> | Creates a new file containing standard error. If the specified file exists, it's overwritten. |
| 2>> | Appends standard error to the existing file. If the specified file doesn't exist, it's created. |
| & | Creates a new file containing both standard output and standard error. If the specified file exists, it's overwritten. |
| < | Sends the contents of the specified file to be used as standard input. |
| << | Accepts text on the following lines as standard input. |
| <> | Causes the specified file to be used for both standard input and standard output. |

Most of these redirectors deal with output, both because there are two types of output (standard output and standard error) and you will be concerned with what to do in case you specify a file that already exists. The most important input redirector is <, which takes the specified file's contents as standard input.

![](bbox=[0.137, 0.683, 0.215, 0.737])

A common trick is to redirect standard output or standard error to /dev/null. This file is a device that's connected to nothing; it's used when you want to rid of data. For instance, if the program is generating too many error messages, you can type whine 2> /dev/null to run it and discard its error messages.

One operator that requires elaboration is <<. This operator implements a here document, which takes text from the following lines as standard input. Chances you won't use this redirect on the command line, though; the following lines are standard input, so there's no need to redirect them. Rather, you might use this command as part of a script in order to pass data to an interactive program. Unlike redirection operators,