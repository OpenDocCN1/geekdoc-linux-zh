
# CHAPTER 7 THE SHELL

![](img/45ff4cd21497435daa35084a84b95d07_294_0.png)

**Figure 7-4** By default, standard input comes from the keyboard and standard output goes to the screen

*Standard input* is a place that a program gets information from. As with standard output the program never “knows” where the information comes from. Following-sections explain how to redirect standard input to a command so that it comes from an ordinary file instead of the keyboard (the default).

In addition to standard input and standard output, a running program normally has a place to send error messages: *standard error*. Refer to page 297 for more information on working with standard error.

# THE SCREEN AS A FILE

Chapter 6 introduced ordinary files, directory files, and soft links. Linux has an additional type of file: *device file*. A device file resides in the Linux structure, usually in the */dev* directory, and represents a peripheral device, such as a screen, printer, or disk drive.

The device name that the utility displays after your username is the filename of your screen. For example, when displays the device name *pts/4*, the pathname of your screen is */dev/pts/4*. When you work with multiple windows, each has its own device name. You can also use thetty to display the name of the device that you give the command from. Although you would not normally have occasion to do so, you can read and write to this file as though it were a text file. Writing to it displays what you write on the screen; reading from it reads what you enter on the keyboard.

When you first log in, the shell directs standard output of your commands to the device file that represents the screen (Figure 7-4). Directing output in this manner causes it to appear on the screen. The shell also directs standard input to come from the same file, so that your commands receive as input anything you type on the keyboard.

# STANDARD INPUT and STANDARD OUTPUT

```
$ cat
This is a line of text.
This is a line of text.
Cat keeps copying lines of text
Cat keeps copying lines of text
util you press CONTROL-D at the beginning
until you press CONTROL-D at the beginning
of a line.
of a line.
$
```

**Figure 7-5** The cat utility provides a good example of the keyboard and standard function as standard input and standard output, respectively.

When you use it, it copies a file to standard output. Because the shell directs standard output to the screen, cat displays the file on the screen.

Up to point cat has taken its input from the filename (argument) you specify on the command line. When you do not give cat an argument (that is, when you give the command line followed immediately by RETURN), cat takes its input from standard input. Thus, when called without an argument, cat copies input to standard output, one line at a time.

To see how cat works, type cat and press RETURN in the shell prompt. Nothing happens. Enter a line of text and press RETURN. The same line appears just under the one you entered. The cat utility is working. Because the shell associates cat's standard input with the keyboard and cat's standard output with the screen, when you type a line of text cat copies the text from standard input (the keyboard) to standard output (screen). Figure 7-5 shows this example.

The cat utility keeps copying text until you enter CONTROL-D on a line by. Pressing CONTROL-D sends an EOF (end of file) signal to cat to indicate that it has reached the end of standard input and there is no more text for it to copy. The cat finishes execution and returns control to the shell, which displays a prompt.

# REDIRECTION

The term redirection encompasses the various ways you can cause the shell to alter where standard input of a command comes from and standard output goes to. By default the shell associates standard input and standard output of a command with the keyboard and the screen. You can cause the shell to redirect standard input or standard output of any command by associating the input or output with a command or file other than the device file representing the keyboard or the screen. This section demonstrates how to redirect input from and to output text files and utilities.

# 246 CHAPTER 7 THE SHELL

![](img/45ff4cd21497435daa35084a84b95d07_296_0.png)

Figure 7-6 Redirecting standard output

# REDIRECTING STANDARD OUTPUT

The redirect output symbol (>) instructs the shell to redirect the output of a command to the specified file instead of it to the screen (Figure 7-6). The format of a command line that redirects output is

```
command [arguments] > filename
```

where command is an executable program (such as an application program or a utility), arguments are optional arguments, and filename is the name of the ordinary file the shell redirects output to.

7-7 uses cat to demonstrate output redirection. This figure contrasts with Figure 7-5, where standard input and standard output are associated with the keyboard and screen. The redirect output symbol on the command line causes the shell to associate cat's standard output with the sample.txt file specified on the command line.

# Redirecting output can destroy a file

caution Use caution when you redirect output to a file. If the file exists, the shell will overwrite its contents. For more information see the tip “Redirecting output can destroy a file II” on page 249.

After giving the command and typing the text shown in Figure 7-7, the sample.txt file contains the text you entered. You can use cat with an example of sample.txt to display this file. The next section shows another way to use cat to display the file.

Figure 7-7 shows that redirecting standard output from cat is a handy way to create a file without using an editor. The drawback is that once you enter a line and press RETURN, you cannot edit the text. While you are entering a line, the erase and kill keys work to delete text. This procedure is useful for creating short, simple files.

Figure 7-8 shows how to use cat and the redirect output symbol to concatenate (join one after the other—the derivation of the cat utility) several files into

```
$ cat > sample.txt
This text is being entered at the keyboard and
cat is copying it to a file.
Press CONTROL-D to indicate the
end of file.
CONTROL-D
$
```

**Figure 7-7** cat with its output redirected

larger file. The first three commands display the contents of three files: stationery, tape, and pens. The next command shows cat with three filenames as arguments. When you call it with more than one filename, cat copies the files, one at a time, to standard output. This command shows that supply_orders contains the contents of.

# REDIRECTING STANDARD INPUT

Just as you can redirect standard output, so can redirect standard input. The redirect input symbol (<) instructs you to redirect a command from the specified file instead of the keyboard (Figure 7-9). The format of a command line that redirects input is

```
command [arguments] < filename
```

where command is an executable program (such as an application program or a utility), arguments are optional arguments, and filename is the name of the ordinary file the shell redirects input from.

| stationery |
| :--- |
| tape |
| pens |

$ cat < supply_orders

**Figure 7-9** Redirecting standard input

The cat utility provides a good example of the keyboard and standard function as standard input and standard output, respectively.

When you use it, it copies a file to standard output. Because the shell directs standard output to the screen, cat displays the file on the screen.

Up to point cat has taken its input from the filename (argument) you specify on the command line. When you do not give cat an argument (that is, when you give the command line followed immediately by RETURN), cat takes its input from standard input. Thus, when called without an argument, cat copies input to standard output, one line at a time.

To see how cat works, type cat and press RETURN in the shell prompt. Nothing happens. Enter a line of text and press RETURN. The same line appears just under the one you entered. The cat utility is working. Because the shell associates cat's standard input with the keyboard and cat's standard output with the screen, when you type a line of text cat copies the text from standard input (the keyboard) to standard output (screen). Figure 7-5 shows this example.

The cat utility keeps copying text until you enter CONTROL-D on a line by. Pressing CONTROL-D sends an EOF (end of file) signal to cat to indicate that it has reached the end of standard input and there is no more text for it to copy. The cat finishes execution and returns control to the shell, which displays a prompt.

![](img/45ff4cd21497435daa35084a84b95d07_298_0.png)

**Figure 7-8** Using cat to catenate files

The cat utility is a member of class of Linux utilities that function in this manner. Other members of this class include sort, grep, and Perl. These utilities first examine the command line that you call. If you include a filename on the command line, the utility takes its input from the file you specify. If you do not specify a filename, the utility takes its input from standard input. It is the utility or program—not the shell or operating system—that functions in this manner.

# noclober: AVOIDS OVERWRITING FILES

The shell provides the noclober feature that prevents overwriting a file using redirection. Enable this feature by setting noclober using the command -o noclober. The same command with +o sets noclober. With noclober set, if you redirect to an existing file, the shell displays an error message and does not execute the command. The following example creates a file using touch, sets noclober, and attempts to redirect the output from echo to the newly created file, uses theber, and performs the redirection

```
$ touch tmp
$ -o noclober
$ echo "hi there" > tmp
bash tmp: cannot overwrite existing file
$ +o noclober
$ echo "hi there" > tmp
```

You can override noclober by putting a pipe symbol after the redirect symbol (>). In the following example, the user creates a file by redirecting the output of date.
