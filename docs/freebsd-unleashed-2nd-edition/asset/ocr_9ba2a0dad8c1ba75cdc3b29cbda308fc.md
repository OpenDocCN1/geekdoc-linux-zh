Other wildcards supported by case include ?, which works the same way it does in the shell (as you saw in Chapter 7), and the pipe character (|), which allows case to accept a range of options. For example, Y | y) will accept either Y or y as a match for a test. You can also enclose multiple characters in brackets to match a range of characters. For example, [Yy]|[Ee]|[Ss]) will accept either y or yes as a match in any combination of upper- or lowercase letters.

# CGI Programming

You've probably seen Web sites that have features such as random quotes that display on the page at each load or a random picture that changes each time the page is reloaded. The program presented previously that used case to display the quotes is one way to do this. This is called a CGI program, and it is a way for the Web server to run external programs and then send the output of those programs over the Internet to a browser. Chapter 25, "Configuring a Web Server," covers more of CGI programming.

# Logical AND/OR Conditionals

Using logical AND/OR conditionals are basically a short-hand way of doing if statements in some cases. They use the exit status of the first command to determine whether to run the second command. Here's an example:

```
tar cvfz backup.tar.gz documents/2000/ & & rm -r documents/2000
```

This command basically says, "If the first operation is successful, perform the second operation. If the first operation is not successful, do not perform the second operation." In other words, "You have to perform A and B. If A cannot be performed, do not perform B." In this case, it will attempt to archive all the files in the directory documents/2000 into a file called backup.tar.gz. If the archive operation is successful (the tar command exits with 0), the operation after && will also be performed, which removes the directory documents/2000. If the archive operation is unsuccessful (the tar command exits with some number other than 0), the operation after && will not be performed (obviously, we do not want to remove the directory if we were unable to successfully archive it).

The || is the OR operator. It basically says, "If you cannot perform A, perform B. But do not perform B if A is successful." Here is an example:

```
tar cvfz backup.tar.gz documents/2000/ || echo "Archive operation failed."
```

In this case, if the archive operation is successful (tar exits with 0), the statement after || will not be executed. If, however, the archive operation fails (tar returns an exit status other than 0), the statement after || will be executed, and an error message will be printed to the screen.