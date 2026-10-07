> character is used for output redirection. The following command redirects the standard input of the cat command to the .cshrc file:

```
cat < .cshrc
```

In practice, input redirection isn't used very often because most commands that require input from a file support passing the filename as an argument to the command.

Output redirection is used much more frequently. The following command redirects the standard output of the cat command to the file named cshenv (which has the effect of storing the contents of the .cshrc and .login files in one file named cshenv):

```
cat .cshrc .login > cshenv
```

> **CAUTION**

The file to which output is being redirected is created if it does not exist and is overwritten without warning if it already exists.

# ## Pipelines

tosh pipelines, just like bash and pdksh pipelines, are a way to string together a series of Linux commands. This means that the output from the first command in the pipeline is used as the input to the second command in the pipeline. The output from the second command in the pipeline is used as input to the third command in the pipeline, and so on. The output from the last command in the pipeline is the output that the user actually sees. This output is displayed to the screen (or put into a file if output redirection was specified on the command line).

You can tell tosh to create a pipeline by typing two or more commands separated by the | character. The following command illustrates an example of using a tosh pipeline:

```
cat file1 file2 | wc -l
```

The cat command in this pipeline appends file2 to the end of file1 and passes the resulting file to the wc command. The wc command prints to the screen the total number of lines contained in the resulting file.