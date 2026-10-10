# Introduction to Linux

In the above example, if you type "a" after the first two characters and hit Tab again, no other possibilities are left, and the shell completes the directory name, without you having to type the string "rthere":

```
your_prompt> cd starthere
```

Of course, you’ll still have to hit Enter to accept this choice.

In the same example, if you type "u", and then hit Tab, the shell will add the "ff" for you, but then it protests again, because multiple choices are possible. If you type Tab Tab again, you’ll see the choices; if you type one or more characters that make the choice unambiguous to the system, and Tab again, or Enter when you’ve reach the end of the file name that you want to choose, the shell completes the file name and changes you into that directory - if indeed it is a directory name.

This works for all file names that are arguments to commands.

The same goes for command name completion. Typing l s and then hitting the Tab key twice, lists all the commands in your PATH (see Section 3.2.1) that start with these two characters:

```
your_prompt> l s
ls                lsdev             lspci             lsraid            lsw
lsattr            lsmod             lspnp             ls1616toppm
```

# 2.3  Getting help

# 2.3.1 Be warned

GNU/Linux is all about becoming more self-reliant. And as usual with this system, there are several ways to achieve the goal. A common way of getting help is finding someone who knows, and however patient and peace-loving the Linux-using community will be, almost everybody will expect you to have tried one or more of the methods in this section before asking them, and the ways in which this viewpoint is expressed may be rather harsh if you prove not to have followed this basic rule.

# 2.3.2 The man pages

A lot of beginning users fear the man (manual) pages, because they are an overwhelming source of documentation. They are, however, very structured, as you will see from the example below on: man man.

Reading man pages is usually done in a terminal window when in graphical mode, or just in text mode if you prefer it. Type the command like this at the prompt, followed by Enter: