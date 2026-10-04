
Structures appear in the file def.h, as follows:

```
#include <stdio.h>
#include <limits.h>
#include <signal.h>
#include <fcntl.h>

#define TRUE 1
#define FALSE 0
#define OKAY 1
#define ERROR 0
#define MAXLINE 200          /* Maximum length of input line */
#define MAXARG 20            /* Max number of args for each simple command */
#define PIPELINE 5           /* Max number of simple commands in a pipeline */
#define MAXNAME 100          /* Maximum length of i/o redirection filename */

char line[MAXLINE+1];               /* User typed input line */
char *lineptr;                      /* Pointer to current position in line[] */
char avline[MAXLINE+1];             /* Argv strings taken from line[] */
char *avptr;                        /* Pointer to current position in avline[] */
char infile[MAXNAME+1];             /* Input redirection filename */
char outfile[MAXNAME+1];            /* Output redirection filename */

int backgnd;                        /* TRUE if & ends pipeline else FALSE */
int lastpid;                        /* PID of last simple command in pipeline */
int append;                         /* TRUE for append redirection (>>) else FALSE */

struct cmd
{
    char *av[MAXARG];
    int infd;
    int outfd;
} cmdlin[PIPELINE];                /* Args and fds, one per simple command */
```

When you type a command line to the tiny shell in response to its prompt, the characters you enter are stored directly into the line[] array. Suppose you enter the command:

```
tsh: echo hello world
```

you already know that in order to execute this command the tiny shell needs to fork() a child process and then exec() the echo command in the child. As the echo command takes parameters it is necessary to extract them from the command line (in the line[] array) and parcel them up into an argv type data structure to pass into exec() (the execvp() system call in this case).

In the tiny shell, the separate words on the command line are extracted and stored as a set of separate strings in the avline[] array. Then for each simple command in

![](img/ad36c2db45661d7b3b68db09c8eea0a1_344_0.png)

Figure 20.1 Use of line[], avline[] and cmdlin[] arrays.

the command line an array of pointers is set up to point to the appropriate individual command line words for that command. The array of pointers is contained in the struct cmd structure, one of which is available for each simple command in the pipeline. This set of structures is itself stored as an array called cmdlin[].

Figure 20.1 is intended to illustrate this idea by showing the contents of the line[], avline[] and cmdlin[] arrays when the entered command pipeline is:

```
tsh: ls | wc -w
```

## 20.2 The Code

Having seen the basic data structures and their use let us now take a look through the code. The tiny shell has been designed in a basically top-down fashion and that is the order in which we'll work through it.

### 20.2.1 main Function

The top level design of any interpreter is basically a loop which just gets something to do and then goes away to do it. The tiny shell is no exception so that the main() function is particularly simple:

```
#include "def.h"

main(void)
{
    int i;

    initcold();

    for (;;)
    {
        initwarm();

        if (getline())
            if (i = parse())
                execute(i);
    }
}
```

The first thing that happens is that main() calls a one-off initialization function called initcold(). This is followed by an endless loop which repeatedly prints a prompt, gets lines of input, parses them to extract the simple commands and their parameters, and then executes each of the simple commands, dealing with I/O redirection and pipes as appropriate.

In detail, the body of the loop first calls initwarm() to initialize things for each input command line and display the tsh: prompt. This is followed by a call to getline(), which copies the user's command line into the line[] array and returns a non-zero value if the length of the entered line was less than MAXLINE.

If a non-zero value is returned by getline(), then the parse() function is called next. This function has the task of parsing the contents of the line[] array and extracting the relevant information from it. This includes the simple command names and their associated parameters, the input and output file names for any I/O redirection, and the pipeline background (&) operator, if specified.

Assuming there are no errors, the parse() function returns a positive value which is the number of simple commands in the input command pipeline. On error, parse() returns the value zero. If there have been no errors so far, then, finally, the execute() function is called with the count returned by parse() passed in as a parameter. The execute() function uses fork() and exec() to execute each of the simple commands in turn, creating pipes and opening I/O redirection files as required.

### 20.2.2 Initialization Functions

The contents of the initcold() initialization function are currently commented out so that the function actually does nothing. This is because the tiny shell has no built-in commands like the real shell. What this means is that shell commands like exit, which will terminate the real shell, cannot be used with the tiny shell in the same way. The easiest way to terminate the tiny shell is therefore to send it an interrupt (Ctrl-c) or quit (Ctrl-\ ) signal from the keyboard. Obviously, if the contents of initcold() were uncommented, then this would not be possible and the tiny shell would then be more difficult to terminate.

```
initcold(void)
{
/*
    signal(SIGINT, SIG_IGN);
    signal(SIGQUIT, SIG_IGN);
*/
}
```

```
initwarm(void)
{
    int i;

    backgnd = FALSE;
    lineptr = line;
    avptr = avline;
    infile[0] = '\0';
    outfile[0] = '\0';
    append = FALSE;

    for (i = 0; i<PIPELINE; ++i)
    {
        cmdlin[i].infd = 0;
        cmdlin[i].outfd = 1;
    }

    for (i = 3; i<OPEN_MAX; ++i)
        close(i);

    printf("tsh: ");
    fflush(stdout);
}
```

The initwarm() function is executed at the start of each iteration of the ‘get a command, execute a command’ loop. Essentially, it just initializes the global
variables, sets the infd and outfd file descriptors for each of the simple command structures in the cmdlin[] array to their default values, close()s all file descriptors other than the standard input, output and error output devices, and finally displays the tsh: prompt.

### 20.2.3 getline Function

```
getline(void)
{
    int i;

    for (i = 0; (line[i] = getchar())!='\n' && i<MAXLINE; ++i);

    if (i==MAXLINE)
    {
        fprintf(stderr, "Command line too long\n");
        return(ERROR);
    }

    line[i+1] = '\0';
    return(OKAY);
}
```

This function just takes characters from the standard input device and copies them into the line[] array, until either a newline (\n) character is encountered or MAXLINE number of characters have been entered, in which case the line[] array is full.

If MAXLINE characters have been entered then the function returns ERROR; otherwise a string terminator (\0) is added after the last character entered, and the OKAY value is returned instead.

### 20.2.4 parse Function

The syntax of a command pipeline looks as follows:

```
cmd [ < filename ] [ | cmd ]... [ or filename ] [ & ]
```

Here cmd means any simple command including its parameters, and or is either of the output redirection operators (> or >>). Square brackets are used to enclose optional items and the ellipses (...) mean that the preceding bracket contents may be repeated zero or more times.

Piecing it all together, what this says is that a tiny shell command pipeline starts with a simple command. This is then optionally followed by an input redirection
operator and its associated *filename*. This in turn can optionally and repeatedly be followed by a pipe operator and then another simple command. After the last simple command, which may also be the first if no pipes are used, an optional output redirection operator and its associated *filename* may be specified. Finally, the whole pipeline may optionally be set to run in the background by specifying the & operator.

The *parse()* function needs to make sure that the syntax of its input conforms to this specification, whilst at the same time extracting the tokens belonging to each simple command and the file names for any input or output redirection that might be specified.

```
parse(void)
{
    int i;

    /* 1 */
    command(0);

    /* 2 */
    if (check("<"))
        getname(infile);

    /* 3 */
    for (i = 1; i<PIPELINE; ++i)
        if (check("|"))
            command(i);
        else
            break;

    /* 4 */
    if (check(">"))
    {
        if (check(">"))
            append = TRUE;

        getname(outfile);
    }

    /* 5 */
    if (check("&"))
        backgnd = TRUE;

    /* 6 */
    if (check("\n"))
        return(i);
    else
    {
