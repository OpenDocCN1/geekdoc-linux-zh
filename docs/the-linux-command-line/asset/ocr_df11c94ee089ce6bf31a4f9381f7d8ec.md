accept standard input in addition to command line arguments. We only touched on them briefly then, but now we will take a closer look at how they can be used to perform text processing.

# cat

The cat program has a number of interesting options. Many of them are used to help better visualize text content. One example is the -A option, which is used to display non-printing characters in the text. There are times when we want to know if control characters are embedded in our otherwise visible text. The most common of these are tab characters (as opposed to spaces) and carriage returns, often present as end-of-line characters in MS-DOS style text files. Another common situation is a file containing lines of text with trailing spaces.

Let’s create a test file using cat as a primitive word processor. To do this, we’ll just enter the command cat (along with specifying a file for redirected output) and type our text, followed by Enter to properly end the line, then Ctrl-d, to indicate to cat that we have reached end-of-file. In this example, we enter a leading tab character and follow the line with some trailing spaces:

```
[me@linuxbox ~]$ cat > foo.txt
    The quick brown fox jumped over the lazy dog.
[me@linuxbox ~]$
```

Next, we will use cat with the -A option to display the text:

```
[me@linuxbox ~]$ cat -A foo.txt
^IThe quick brown fox jumped over the lazy dog.  $
[me@linuxbox ~]$
```

As we can see in the results, the tab character in our text is represented by ^I. This is a common notation that means “Control-I” which, as it turns out, is the same as a tab character. We also see that a $ appears at the true end of the line, indicating that our text contains trailing spaces.