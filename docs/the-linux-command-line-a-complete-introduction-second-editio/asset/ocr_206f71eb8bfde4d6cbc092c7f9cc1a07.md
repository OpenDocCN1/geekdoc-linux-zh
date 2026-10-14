We can restore the original prompt at any time during our terminal session by simply reversing the process.

```
[me@linuxbox ~]$ PS1="$ps1_old"
```

Now that we are ready to proceed, let’s see what happens if we have an empty prompt string.

```
[me@linuxbox ~]$ PS1=
```

If we assign nothing to the prompt string, we get nothing. No prompt string at all! The prompt is still there but displays nothing, just as we asked it to do. Because this is kind of disconcerting to look at, we’ll replace it with a minimal prompt.

```
PS1="\$ "
```

That’s better. At least now we can see what we are doing. Notice the trailing space within the double quotes. This provides the space between the dollar sign and the cursor when the prompt is displayed.

Let’s add a bell to our prompt.

```
$ PS1="\[\a\]\$ "
```

Now we should hear a beep each time the prompt is displayed, though some systems disable this “feature.” This could get annoying, but it might be useful if we needed notification when an especially long-running command has been executed. Note that we included the \[ and \] sequences. Since the ASCII bell (\a) does not “print,” that is, it does not move the cursor, we need to tell bash so it can correctly determine the length of the prompt.

Next, let’s try to make an informative prompt with some hostname and time-of-day information.

```
$ PS1="\A \h \$ "
17:33 linuxbox $
```