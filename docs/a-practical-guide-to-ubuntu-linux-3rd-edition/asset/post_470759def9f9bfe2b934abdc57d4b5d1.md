
![](img/2344fc4a798f29dca9e8b5ed7288171a_296_0.png)

Figure 7-6 Redirecting standard output

## REDIRECTING STANDARD OUTPUT

The *redirect output* symbol (>) instructs the shell to redirect the output of a command to the specified file instead of to the screen (Figure 7-6). The format of a command line that redirects output is

```
command [arguments] > filename
```

where *command* is any executable program (such as an application program or a utility), *arguments* are optional arguments, and *filename* is the name of the ordinary file the shell redirects the output to.

Figure 7-7 uses cat to demonstrate output redirection. This figure contrasts with Figure 7-5, where standard input *and* standard output are associated with the keyboard and screen. The input in Figure 7-7 comes from the keyboard. The redirect output symbol on the command line causes the shell to associate cat’s standard output with the *sample.txt* file specified on the command line.

### Redirecting output can destroy a file!

> Use caution when you redirect output to a file. If the file exists, the shell will overwrite it and destroy its contents. For more information see the tip “Redirecting output can destroy a file!” on page 249.

After giving the command and typing the text shown in Figure 7-7, the *sample.txt* file contains the text you entered. You can use cat with an argument of *sample.txt* to display this file. The next section shows another way to use cat to display the file.

Figure 7-7 shows that redirecting standard output from cat is a handy way to create a file without using an editor. The drawback is that once you enter a line and press RETURN, you cannot edit the text. While you are entering a line, the erase and kill keys work to delete text. This procedure is useful for creating short, simple files.

Figure 7-8 shows how to use cat and the redirect output symbol to *concatenate* (join one after the other—the derivation of the name of the cat utility) several files into one larger file. The first three commands display the contents of three files: stationery, tape, and pens. The next command shows cat with three filenames as arguments. When you call it with more than one filename, cat copies the files, one at a time, to standard output. This command redirects standard output to the file supply_orders. The final cat command shows that supply_orders contains the contents of all three of the original files.

![](img/2344fc4a798f29dca9e8b5ed7288171a_297_0.png)

Figure 7-7 cat with its output redirected

## Redirecting Standard Input

Just as you can redirect standard output, so you can redirect standard input. The redirect input symbol (<) instructs the shell to redirect a command's input to come from the specified file instead of from the keyboard (Figure 7-9, next page). The format of a command line that redirects input is

```
command [arguments] < filename
```

where command is any executable program (such as an application program or a utility), arguments are optional arguments, and filename is the name of the ordinary file the shell redirects the input from.

![](img/2344fc4a798f29dca9e8b5ed7288171a_297_1.png)

Figure 7-8 Using cat to catenate files

![](img/2344fc4a798f29dca9e8b5ed7288171a_298_0.png)

Figure 7-9 Redirecting standard input

Figure 7-10 shows cat with its input redirected from the `supply_orders` file created in Figure 7-8 and standard output going to the screen. This setup causes cat to display the sample file on the screen. The system automatically supplies an EOF signal at the end of an ordinary file.

- Utilities that take input from a file or standard input

Giving a cat command with input redirected from a file yields the same result as giving a cat command with the filename as an argument. The cat utility is a member of a class of Linux utilities that function in this manner. Other members of this class of utilities include lp, sort, grep, and Perl. These utilities first examine the command line that you call them with. If you include a filename on the command line, the utility takes its input from the file you specify. If you do not specify a filename, the utility takes its input from standard input. It is the utility or program—not the shell or operating system—that functions in this manner.

## noclobber: AVOIDS Overwriting Files

The shell provides the noclobber feature that prevents overwriting a file using redirection. Enable this feature by setting noclobber using the command set -o noclobber. The same command with +o unsets noclobber. With noclobber set, if you redirect output to an existing file, the shell displays an error message and does not execute the command. The following example creates a file using touch, sets noclobber, attempts to redirect the output from echo to the newly created file, unsets noclobber, and performs the same redirection:

```
$ touch tmp
$ set -o noclobber
$ echo "hi there" > tmp
bash: tmp: cannot overwrite existing file
$ set +o noclobber
$ echo "hi there" > tmp
```

You can override noclobber by putting a pipe symbol after the redirect symbol (>|). In the following example, the user creates a file by redirecting the output of date.

```
$ cat < supply_orders
2,000 sheets letterhead ordered:    10/7/10
1 box masking tape ordered:          10/14/10
5 boxes filament tape ordered:       10/28/10
12 doz. black pens ordered:          10/4/10
```

**Figure 7-10** *cat* with its input redirected

Next the user sets the **noclobber** variable and redirects output to the same file again. The shell displays an error message. Then the user places a pipe symbol after the redirect symbol and the shell allows the user to overwrite the file.

```
$ date > tmp2
$ set -o noclobber
$ date > tmp2
bash: a: cannot overwrite existing file
$ date >| tmp2
```

### Redirecting output can destroy a file!

Depending on which shell you are using and how the environment is set up, a command such as the following may yield undesired results:

```
$ cat orange pear > orange
cat: orange: input file is output file
```

Although **cat** displays an error message, the shell destroys the contents of the existing **orange** file. The new **orange** file will have the same contents as **pear** because the first action the shell takes when it sees the redirection symbol (>) is to remove the contents of the original **orange** file.

If you want to concatenate two files into one, use **cat** to put the two files into a temporary file and then use **mv** to rename this third file:

```
$ cat orange pear > temp
$ mv temp orange
```

What happens in the next example can be even worse. The user giving the command wants to search through files **a**, **b**, and **c** for the word **apple** and redirect the output from **grep** (page 166) to the file **a.output**. Unfortunately the user enters the filename as **a output**, omitting the period and inserting a **SPACE** in its place:

```
$ grep apple a b c > a output
grep: output: No such file or directory
```

The shell obediently removes the contents of **a** and then calls **grep**. The error message may take a moment to appear, giving you a sense that the command is running correctly. Even after you see the error message, it may take a while to realize that you have destroyed the contents of **a**.

## APPENDING STANDARD OUTPUT TO A FILE

The *append output symbol* (**>>**) causes the shell to add new information to the end of a file, leaving existing information intact. This symbol provides a convenient way of concatenating two files into one. The following commands demonstrate the action of the append output symbol. The second command accomplishes the catenation described in the preceding caution box:

![](img/2344fc4a798f29dca9e8b5ed7288171a_300_0.png)

Figure 7-11 Redirecting and appending output

![](img/2344fc4a798f29dca9e8b5ed7288171a_300_1.png)

The first command displays the contents of the orange file. The second command appends the contents of the pear file to the orange file. The final cat displays the result.

### Do not trust noclobber

Appending output is simpler than the two-step procedure described in the preceding caution box but you must be careful to include both greater-than signs. If you accidentally use only one and the noclobber feature is not set, the shell will overwrite the orange file. Even if you have the noclobber feature turned on, it is a good idea to keep backup copies of the files you are manipulating in case you make a mistake.

Although it protects you from overwriting a file using redirection, noclobber does not stop you from overwriting a file using cp or mv. These utilities include the -i (interactive) option that helps protect you from this type of mistake by verifying your intentions when you try to overwrite a file. For more information see the tip "cp can destroy a file" on page 164.

The next example shows how to create a file that contains the date and time (the output from date), followed by a list of who is logged in (the output from who). The first line in Figure 7-11 redirects the output from date to the file named whoson. Then cat displays the file. Next the example appends the output from who to the whoson file. Finally cat displays the file containing the output of both utilities.

## /dev/null: MAKING DATA DISAPPEAR

The /dev/null device is a data sink, commonly referred to as a bit bucket. You can redirect output that you do not want to keep or see to /dev/null and the output will disappear without a trace:
