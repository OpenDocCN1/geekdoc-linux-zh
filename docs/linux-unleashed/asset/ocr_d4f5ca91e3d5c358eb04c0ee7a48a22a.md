> **NOTE**

When defining aliases, there can be no spaces on either side of the equal sign. The quotation marks are only necessary if the command within them contains spaces or other special characters.

If you enter the *alias* command without any arguments, it prints all of the aliases that are already defined to the screen. There is a way to make sure that all of your *alias* commands get executed each time you start *pdKsh*. This is done by using an initialization file, which we will discuss later in this chapter in the “Customizing *pdKsh*” section.

# ## Input Redirection

Input redirection is used to change the source of input for a command. Typically, when a command is entered in *pdKsh*, the command expects some kind of input in order to do its job. Some of the simpler commands must get all of the information that they need passed to them on the command line. The *rm* command, for example, requires you to tell it on the command line which files you want to delete; if you do not specify any files, it issues a prompt telling you to enter *rm -h* for help.

Other commands require more elaborate input than a simple directory name. The input for these commands is typically found in a file. For example, the *wc* (word count) command counts the number of characters, words, and lines in the input that was given to it. If you enter the *wc* command with a filename as an argument, *wc* returns the number of characters, words, and lines that are contained in that file. An example of this is:

```
```
wc test
11 2 1
```
```

Another way to accomplish passing the contents of the *test* file to *wc* as input is to change (or redirect) the input of the *wc* command from the terminal to the *test* file. This results in the same output. The `<` character is used by *pdKsh* to redirect the input to the current command from the file following the character. So, redirecting *wc*’s input from the terminal to the *test* file is done by entering the following command:

```
```
wc < test
11 2 1
```
```

Input redirection is not used too often because most commands that require input from a file have an option to specify a filename on the command line. There are times, however, when you come across a program that does not accept a filename as an input parameter, and yet the input that you want to give to the command exists in a file. Whenever this situation occurs, you can use input redirection to get around the problem.