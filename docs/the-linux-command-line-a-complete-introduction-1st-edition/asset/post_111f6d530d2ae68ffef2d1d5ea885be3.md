
# 13

# CUSTOMIZING THE PROMPT

In this chapter we will look at a seemingly trivial detail: our shell prompt. This examination will reveal some of the inner workings of the shell and the terminal emulator program itself.

Like so many things in Linux, the shell prompt is highly configurable, and while we have pretty much taken it for granted, the prompt is a really useful device once we learn how to control it.

## Anatomy of a Prompt

Our default prompt looks something like this:

```
[me@linuxbox ~]$
```

Notice that it contains our username, our hostname, and our current working directory, but how did it get that way? Very simply, it turns out. The prompt is defined by an environment variable named PS1 (short for prompt string 1). We can view the contents of PS1 with the echo command:

```
[me@linuxbox ~]$ echo $PS1
\u@\h \W\$
```

> Note: Don't worry if your results are not exactly the same as the example above. Every Linux distribution defines the prompt string a little differently, some quite exotically.

From the results, we can see that PS1 contains a few of the characters we see in our prompt, such as the square brackets, the @ sign, and the dollar sign, but the rest are a mystery. The astute among us will recognize these as backslash-escaped special characters like those we saw in Table 7-2. Table 13-1 is a partial list of the characters that the shell treats specially in the prompt string.

### Table 13-1: Escape Codes Used in Shell Prompts

| Sequence | Value Displayed |
|---|---|
| \a | ASCII bell. This makes the computer beep when it is encountered. |
| \d | Current date in day, month, date format; for example, 'Mon May 26' |
| \h | Hostname of the local machine minus the trailing domain name |
| \H | Full hostname |
| \j | Number of jobs running in the current shell session |
| \l | Name of the current terminal device |
| \n | A newline character |
| \r | A carriage return |
| \s | Name of the shell program |
| \t | Current time in 24-hour, hours:minutes::seconds format |
| \T | Current time in 12-hour format |
| \@ | Current time in 12-hour, AM/PM format |
| \A | Current time in 24-hour, hours:minutes format |
| \u | Username of the current user |
| \v | Version number of the shell |
| \V | Version and release numbers of the shell |
| \w | Name of the current working directory |

### Table 13-1 (continued)

| Sequence | Value Displayed |
|---|---|
| \w | Last part of the current working directory name |
| \! | History number of the current command |
| \# | Number of commands entered during this shell session |
| \$ | This displays a "$" character unless you have superuser privileges. In that case, it displays a "#" instead. |
| \[ | This signals the start of a series of one or more non-printing characters. It is used to embed non-printing control characters that manipulate the terminal emulator in some way, such as moving the cursor or changing text colors. |
| \] | This signals the end of a non-printing character sequence. |

## Trying Some Alternative Prompt Designs

With this list of special characters, we can change the prompt to see the effect. First, we’ll back up the existing string so we can restore it later. To do this, we will copy the existing string into another shell variable that we create ourselves:

```
[me@linuxbox ~]$ PS1_old="$PS1"
```

We create a new variable called PS1_old and assign the value of PS1 to it. We can verify that the string has been copied by using the echo command:

```
[me@linuxbox ~]$ echo $PS1_old
[\u@\h \W\$]
```

We can restore the original prompt at any time during our terminal session by simply reversing the process:

```
[me@linuxbox ~]$ PS1="$PS1_old"
```

Now that we are ready to proceed, let’s see what happens if we have an empty prompt string:

```
[me@linuxbox ~]$ PS1=
```

If we assign nothing to the prompt string, we get nothing. No prompt string at all! The prompt is still there but displays nothing, just as we asked it to. Since this is kind of disconcerting to look at, we’ll replace it with a minimal prompt:

```
PS1="^\$ "
```
