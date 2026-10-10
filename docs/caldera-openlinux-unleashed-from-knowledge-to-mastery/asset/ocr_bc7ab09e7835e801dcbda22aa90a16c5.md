# Note

Under the standard Caldera setup, KDE runs in virtual console 8. There's nothing useful in virtual console 7, but virtual consoles 1–6 offer full login sessions. If you're in a text-mode virtual console, you can use Alt+Fn to switch consoles. In an X Window session, you need to use Ctrl+Alt+Fn. It's easier to use Ctrl+Alt+Fn everywhere because it doesn't hurt in a text-mode console.

# Typing Shortcuts

The problem with a command-line interface is that it involves a lot of typing, and people tend to minimize the amount of typing they do. This means that they name files with names like frpt9899 rather than fiscal-report-1998-99.txt. Graphical interfaces reduce the problem because files are often selected from a graphical dialog, eliminating the need to type their names.

# Filename Completion

With modern shells, there is no excuse for taking typing shortcuts. Let's create four files named a-long-filename, b-long-filename, b-long-again, and c-what-i-mean. Create an empty test directory and change to it. Then type:

```
```
$ cat < /dev/null > a-long-filename
$ cat < /dev/null > b-long-filename
$ cat < /dev/null > b-long-again
$ cat < /dev/null > c-what-i-mean
```
```

(Recall our discussion concerning /dev/null in the “Discarding Output” section.)

Now, let’s say we want to use cat to filter a-long-filename. At the command prompt, type cat a and then press Tab. The shell fills in the whole filename a-long-filename for you.

How did this work? The shell examined the partial command line and determined that you were looking for a file whose name began with a. It scanned the directory, found the only possible file that would match, and completed the name for you.

What if you start with cat b and then press Tab? In this case, the shell fills in as far as b-long-, and the terminal beeps. The shell knows you’re looking for a file starting with b, but there is more than one possibility. It completes up to the longest common stem and then beeps.