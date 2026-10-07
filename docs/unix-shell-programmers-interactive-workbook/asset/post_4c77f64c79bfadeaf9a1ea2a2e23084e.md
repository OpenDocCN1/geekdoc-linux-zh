
## Chapter 2: Command Syntax 107

You could try to deal with this problem using 1>>out3 2>>out3 or 1>out3 2>out3, but those won't work either. This entire, complex topic can be summarized in the following Tip:

> Don't try to use separate redirections to send information from two fds to one file

## 2.3.4 ANSWERS

- a) Why must there be no space between the 2 and the >

Answer: Consider this command:
`cat out 2 >out2`

This would copy the files named out and 2 (because 2 is a valid file name) to out2. 

> If you find files with names like 1 or 2 in a directory, it probably means someone made typing errors when they were trying to redirect fds. But you never know, they might be real files, so double-check before deleting them!

- b) Why must there be no space between the > and the ampersand?

Answer: Consider this command:
`cat out 2> &out2`

Under this, you have to “think like the shell.” When it sees the 2> token, it knows the next thing must be the name of the file you want stderr redirected to, but the next thing it sees is the ampersand, which is its “background job” indicator, which you will cover in the next lab. That doesn't make any sense, and it issues an error message saying the sand was “unexpected.” The cat command never gets run.

## 108 Lab 2.3: Command Syntax

The shell uses spaces to tell it how to divide the parts of a command line into syntactic elements. If you want to link fds, the fd number, the >, and the ampersand must all be a single syntactic element with no spaces within it.

![](img/694fa9f0320e707804a4c650b96a09b4_127_0.png)

- c) Why there be a space between the ampersand and the 1?
Answer: There is no ambiguity. Once the shell sees 2&, it knows that the next thing has to be an fd number, and it doesn't matter whether there is a space before it or not.

Pay attention to where spaces are required, where they are optional, where they are prohibited in command lines. These are all common sources of syntax errors.

![](img/694fa9f0320e707804a4c650b96a09b4_127_1.png)

- d) What is the difference between the following two commands:
`cat out1 out2 >out3 2& > 1`
`cat out1 out2 2& > 1 out3`

Answer: The first command redirects stdout (fd 1) to out3, and then redirects stderr to the same place as fd 1 (i.e., to out3 also). The second one redirects stderr to the same place as fd 1, which is still connected to your screen, then it redirects-out to the file out3. The net effect of the second command is the same as the following command:
`cat out1 out2 > out3`

Remember the left-to-right order that the shell uses to process redirection symbols. The fd association is done in left-to-right order, just like all other redirection operations.

## 2.3.5 ANSWERS

- a) What effect did the exclamation mark after the word document have?
Answer: It had no effect; it is part of the content of the here document.

The marker symbol can appear inside the here document, but when it is the only thing on a line, it marks the end of the here document.

## LAB 2.3

## Chapter 2: Command Syntax 109

- b) Modify the example so it uses a dot as the symbol marking the end of the here document.

Answer: Your interaction should look something like the following:

```
$ cat <<.
> This here document is two lines long.
> Here is a dot: It is not the dot that ends this doc.
>
```

This here document is two lines long.
Here is a dot: . It is not the dot that ends this doc.
$

![](img/694fa9f0320e707804a4c650b96a09b4_128_0.png)

Again, you put the marker symbol inside the here document, but when it appears alone on a line, it marks the end of the document.

The > symbols on the second, third, and fourth lines prompt the shell when it is waiting for you to type parts of a command that extend to multiple lines on the screen.

As this shows, you can use a dot without problems, but there are other punctuation marks you cannot use. For example, you can't use > symbol because that would look like output redirection to the shell, and you will get a syntax error.

- c) Can you use the word the as the marker?
Answer: Yes you can, as the following shows:

```
$ cat << the
> time is now
> So words work fine as terminators too.
> the
```

Note that the first line starts with the marker symbol, but has more characters on the same line, so it doesn't terminate the here document. You can use just anything as the termination symbol for here documents, unless it looks like a syntax element to the shell, such as redirection. For clarity, it's best to use something that won't be confusing to the person reading your script.

## 110 Lab 2.3: Command Syntax

Common symbols used to end documents include the word END (using capital letters makes it stand out) or exclamation marks (!!!). It's a good idea to pick one symbol and use it for all the documents you write. The consistency will help you and the people who read your code to spot your use of documents easily.

![](img/694fa9f0320e707804a4c650b96a09b4_129_0.png)

Three signs (+++) might seem like a good termination symbol for documents because it's easy to spot, but that tells many shells to go into interactive mode!![](img/694fa9f0320e707804a4c650b96a09b4_129_1.png) Type a cat command with a here document for stdin, and redirect stdout to a file.

- d) What does the command do?
Answer: It copies the here document to the file. Your interaction should look like the following:

```
$ rm -f out
$ cat << !!! > out
> This is here.
> That is there.
> Never shall meet.
> !!!
$ more out
This is here.
That is there.
Never shall meet.
$
```

This example shows the syntax for using both << and other redirection for a single command, but it is not the kind of thing you would normally do in interactive mode. Here documents are used almost exclusively inside scripts and functions.

## LAB 2.3

## LAB 2.3 SELF-REVIEW QUESTIONS

To test your progress, you should be able to answer the following questions.

- 1) What does fd stand for?
a) file directory
b) file descriptor
c) format directive
d) free distribution
e) future domain

- 2) Aside from potential differences in readability, it does not matter in what order you put input redirection, output redirection, and the command name in the command.
a) True
b) False

- 3) What happens if you specify output redirection more than once for the same command?
a) None of the redirections have any effect except the first one.
b) None of the redirections have any effect except the last one.
c) All the files are created, but only the first is written to.
d) All the files are created, but only the last is written to.
e) The shell prints a syntax error message.

- 4) Which of the following has everything to do with I/O redirection:
a) The command being executed.
b) The shell.
c) The operating system.
d) The network. (Hint: not this answer!)

- 5) Which of the following commands redirect stdout? (There may be more than one answer).
a) cat a_file_b_file 2> error.log
b) cat > a_file b_file
c) print hello 3> there
d) print hello 1> there
e) print hello > there

## 112 Lab 2.3: Command Syntax

- 6) Which cat command writes both stdout and stderr to a file named out?
a) cat a b > out 2>&1
b) cat a b > out 2>&1
c) cat a b 2>&1 out
d) cat a b 2>&1 out
e) cat a 2 >&1 out

- 7) Which of the following is not a valid marker symbol for a here document?
a) !!!
b) +END+
c) >out
d) END
e) +++

- 8) Which of the following commands might fail if noclobber is set?
a) print hello |cat
b) print hello > out
c) print hello >| out
d) cat < out
e) print Not this one!

Quiz answers appear in Appendix A, Section 2.4.

## CHAPTER 2

## TEST YOUR THINKING

![](img/694fa9f0320e707804a4c650b96a09b4_132_0.png)

The projects in this section are meant to have you utilize all of the skills that you have acquired throughout this chapter. The answers to these projects can be found at the companion web site to this book, located at:

http://www.phptr.com/phptrinteractive/
Visit the web site periodically to share and discuss your answers.

- 1) Write a syntax synopsis for the sort command. There are several versions of sort available on different UNIX systems. Write your synopsis for the one that has the following options and parameters:

Options b, c, d, f, i, m, M, n, r, and u do not take arguments.
The following options take the arguments indicated:

```
k       keydef
o      output
t       char
T       directory
z       recsz
```

The option y takes an optional argument called kmem.
Any number of file names, possibly none, are positional parameters.
