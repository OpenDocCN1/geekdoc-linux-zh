codes. The first 32 characters in the ASCII coding scheme are used to transmit commands to Teletype-like devices. Some of these codes are familiar (tab, backspace, line feed, and carriage return), while others are not (null, end-of-transmission, and acknowledge).

Table 7-2 lists some of the common backslash escape sequences.

Table 7-2: Backslash Escape Sequences

| Escape sequence | Meaning |
|---|---|
| \a | Bell (an alert that causes the computer to beep) |
| \b | Backspace |
| \n | Newline; on Unix-like systems, this produces a line feed |
| \r | Carriage return |
| \t | Tab |

The idea behind this representation using the backslash originated in the C programming language and has been adopted by many others, including the shell.

Adding the -e option to echo will enable interpretation of escape sequences. You can also place them inside $' '. Here, using the sleep command, a simple program that just waits for the specified number of seconds and then exits, we can create a primitive countdown timer:

```
sleep 10; echo -e "Time's up\a"
```

We could also do this:

```
sleep 10; echo "Time's up" $'\a'
```

# Summing Up