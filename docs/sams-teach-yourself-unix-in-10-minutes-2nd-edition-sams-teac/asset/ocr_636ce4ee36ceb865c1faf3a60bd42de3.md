# The more Command

All you need to do to use more is to type the command followed by the file or files you want to display. This command is similar to cat. The tricky part is memorizing which one to use and having that knowledge at your fingertips when you need it. Let's take a look at the more command in action:

```
>more hosts.allow
(Output removed)
```

For this command you will need to have a file that is long enough to scroll off your screen and warrants the use of the command. If you type in the wrong command, or you specify a file that is not long enough to scroll off the screen, more will more or less nothing for you. (Pun intended.)

When you use the more command with a long file, you immediately see something new on your terminal screen. On the bottom left of the screen, you will see the more command in action:

+   - More -- (53%)

Fifty-three percent is what you have seen and the rest is still needs to be seen. You know from the percentage how many pages you are dealing-with. If you had 25%, then it's three or four pages of output to view.

Pressing the Spacebar will bring you to the next page. You can use the q on the keyboard to quit the program, or Ctrl+z will also stop the more command if you want to break the sequence of using it. Using s on the keyboard will skip one line at a time and is helpful if you want to scroll through your output line by line, instead of page by.

In this section we looked at how to use more to page through your output. Using cat showed you contents of a file, but you had little control over being able to view large files and this is where the more command is useful. Now, let's take a look at the less command, which is a new version of the more command. So you can do more with less!