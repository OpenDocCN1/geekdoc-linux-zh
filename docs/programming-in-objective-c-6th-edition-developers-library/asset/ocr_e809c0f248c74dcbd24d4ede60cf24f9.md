# Input and Output Operations with Files

So far, when a call was made to the $\texttt{\fbox{s}}$ function by one of the programs in this book, the data that was requested by the call was always read in from keyboard input by your program’s user. Similarly, all calls to the $\texttt{\fbox{p}}$ function resulted in the display of the desired information to your active window. To improve the utility of your programs, you need to be able to read data from, and write data to, files, which are covered in this section.

# Redirecting I/O to a File

Both read and write file operations can be easily performed under many operating systems, including Windows, Linux, and Unix, without anything special being done at all to the program. Type [Program 15.2](#), a very simple example that takes a number, then performs some very simple calculations on it.

**Program 15.2 A Simple Example**
[Click here to view code image](#)

```

```
/ #
main
{

```

```

Simple enough, but suppose you want to keep the results in a file. If you want to write the results from this program into a file called **r**, for example, all that you need to do under Unix or Windows if running from a command prompt is to redirect the output from the program into the file **r** by executing the program with the following command:

**p**

This command instructs the system to execute the program **p** but to redirect the output normally written to the command prompt into a file called results.txt instead. So, any values displayed by **p** do not appear in your window but are instead written into the file called **r**.

While [program 15.2](#) is interesting, it would be even more valuable to prompt the user to enter a number and then perform the calculations on the number and display the results. [Program 15.3](#) shows that slightly tweaked program.

**Program 15.3 A Simple, yet More Interactive, Example**
[Click here to view code image](#)