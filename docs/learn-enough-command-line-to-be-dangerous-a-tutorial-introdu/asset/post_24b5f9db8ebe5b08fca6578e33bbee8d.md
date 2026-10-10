
**Listing 5:** The result of editing a longer command-line command.

```
$ echo "From fairest creatures we desire increase,"
```

I usually move around the command line with a combination of `Ctrl-A`, `Ctrl-E`, and right & left arrow keys, but for longer commands Option-click can be a big help. (I also frequently change my mind about the exact command I’m typing, in which case I usually find that hitting `Ctrl-U` and starting over again is the fastest way to proceed.)

# Exercises

- 1. Using the up arrow, print to the screen the strings “fee”, “fie”, “foe”, and “fum” without retyping `echo` each time.
- 2. Starting with the line in Listing 4, use any combination of `Ctrl-A`, `Ctrl-E`, arrow keys, or Option-click to change the occurrences of the short *s* to the archaic *long s* “ſ” in order to match the appearance of the original (Figure 10). In other words, the argument to `echo` should read “FRom faireft creatures we defire increase,”. *Hint:* It’s unlikely that your keyboard can produce “ſ” natively, so either copy it from the text of this tutorial or Google for it and copy it from the Internet.

# 1.5 Cleaning up

When using the command line, sometimes it’s convenient to be able to clean up by clearing the screen, which we can do with `clear`:

```
$ clear
```

A keyboard shortcut for this is `Ctrl-L`.

Similarly, when we are done with a terminal window (or tab) and are ready to exit, we can use the `exit` command:

| Command | Description | Example |
|---|---|---|
| `echo <string>` | Print string to screen | `$ echo hello` |
| `man <command>` | Display manual page for command | `$ man echo` |
| `Ctrl-C` | Get out of trouble | `$ tail^C` |
| `Ctrl-A` | Move to beginning of line | |
| `Ctrl-E` | Move to end of line | |
| `Ctrl-U` | Delete to beginning of line | |
| `Option-click` | Move cursor to location clicked | |
| `Up & down arrow` | Scroll through previous commands | |
| `clear` or `Ctrl-L` | Clear screen | `$ clear` |
| `exit` or `Ctrl-D` | Exit terminal | `$ exit` |

*Table 1: Important commands from Section 1.*

```
$ exit
```

A keyboard shortcut for this is **Ctrl-D**.

# Exercises

- 1. Clear the contents of the current tab.
- 2. Open a new tab, execute `echo 'hello'`, and then exit.

# 1.6 Summary

Important commands from this section are summarized in Table 1.

# Exercises

- 1. Write a command to print the string **Use** `"man echo"`, *including* the quotes; i.e., take care not to print out **Use** `man echo` instead. *Hint:* Use double quotes in the inner string, and wrap the whole thing in single quotes.
- 2. By running `man sleep`, figure out how to make the terminal “sleep” for 5 seconds, and execute the command to do so. After waiting the requisite 5 seconds, execute the command to sleep for 5000 seconds, realize that’s well over an hour, and then use the instructions from Box 4 to get out of trouble.

# 2 Manipulating files

Because this is a command-line tutorial, we’re not going to assume any familiarity with programs designed to edit text. (Such programs, called *text editors*, are the subject of the next tutorial in the sequence, *Learn Enough™ Text Editor to Be Dangerous*.) This means that we’ll need to create files by hand at the command line. But this is a feature, not a bug (Box 6), because learning to create files at the command line is a valuable skill in itself.

**Box 6. Learning to speak “geek”**

One important part of learning software development is becoming familiar with the hacker, nerd, and geek culture from which much of it springs. For example, the phrase “It’s not a bug, it’s a feature” is a common way of recasting a seeming flaw as a *virtue*. As the Urban Dictionary *puts it*:

**It’s not a bug, it’s a feature**  
Excuse made by software developers when they try to convince the user that a flaw in their program is actually what it’s supposed to be doing.

The *Jargon File*, which includes an *enormous* and entertaining *lexicon* of *hacker* terms, expands on this theme in its entry on *feature*:

Undocumented feature is a common, allegedly humorous euphemism for a *bug*. There’s a related joke that is sometimes referred to as the

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_26_0.png)

*Figure 11: It’s not a bug, it’s a feature.*

> “one-question geek test”. You say to someone “I saw a Volkswagen Beetle today with a vanity license plate that read FEATURE”. If he/she laughs, he/she is a *geek*.
>
> The joke here is that, because “bug” is a common slang term for a Volkswagen Beetle, a Beetle with the vanity plate FEATURE is a real-life manifestation of “It’s not a bug, it’s a feature” (Figure 11).

## 2.1 Redirecting and appending

Let’s pick up (more or less) where we left off in Section 1, with an **echo** command to print out the first line of Shakespeare’s first sonnet (Listing 4):

```
$ echo "From fairest creatures we desire increase,"
From fairest creatures we desire increase,
```

Our task now is to create a file containing this line. Even without the benefit of a text editor, it is possible to do this using the *redirect operator* `>`:

```
$ echo "From fairest creatures we desire increase," > sonnet_1.txt
```

(Recall that you can use up arrow to retrieve the previous command rather than typing it from scratch.) Here the right angle bracket `>` takes the string output from **echo** and redirects its contents to a file called **sonnet_1.txt**.

How can we tell if the redirect worked? We’ll learn some more advanced command-line tools for inspecting files in Section 3, but for now we’ll use the **cat** command, which simply dumps the contents of the file to the screen:

```
$ cat sonnet_1.txt
From fairest creatures we desire increase,
```

The name **cat** is short for “**c**oncate**n**ate”, which is a hint that it can be used to combine the contents of multiple files, but the usage above (to dump the contents of a single file) is extremely common. Think of **cat** as a “quick-and-dirty” way to view the contents of a particular file (Figure 12).[^11]

In order to add the second line of the sonnet (in modernized spelling), we can use the *append operator* `>>` as follows:

[^11]: Image retrieved from https://www.flickr.com/photos/tiffanyday/4076289864 on 2015-07-22

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_28_0.png)

Figure 12: Viewing a file with **cat**.

```
$ echo "That thereby beauty's Rose might never die," >> sonnet_1.txt
```

This just adds the line to the end of the given file. As before, we can see the result using cat:

```
$ cat sonnet_1.txt
From fairest creatures we desire increase,
That thereby beauty's Rose might never die,
```

(To get to this command, I hope you just hit up arrow twice instead of retyping it. If so, you're definitely getting the hang of this.) The result above shows that the double right angle bracket >> appended the string from echo to the file sonnet_1.txt as expected.

Modernized treatments of the Sonnets sometimes emend Rose to rose (thereby obscuring the likely meaning), and we can make a second file following this convention using two more calls to echo:

```
$ echo "From fairest creatures we desire increase," > sonnet_1_lower_case.txt
$ echo "That thereby beauty's rose might never die," >> sonnet_1_lower_case.txt
```

In order to facilitate the comparison of files that are similar but not identical, Unix systems come with the helpful diff command:

```
$ diff sonnet_1.txt sonnet_1_lower_case.txt
< That thereby beauty's Rose might never die,
---
> That thereby beauty's rose might never die,
```

When discussing computer files, diff is frequently employed both as a noun ("What's the diff between those files?") and as a verb ("You should diff the files to see what changed."). As with many technical terms, this sometimes bleeds over into common usage, such as "Diff present ideas against those of various past cultures, and see what you get."[^12]
