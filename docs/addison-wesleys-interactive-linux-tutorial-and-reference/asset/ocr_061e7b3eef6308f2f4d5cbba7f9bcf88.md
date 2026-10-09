In the next module of the CBT course, *Linux Tools*, we cover yet another function of the `cat` command: When combined with *redirection*, `cat` can be used to create text files directly from your keyboard. We introduce this function of `cat` at this point, however, so that you can create the files you will need to complete the exercises in this *Try It Live!* section.

When you enter text or commands at your keyboard, whatever you have typed is *input*. Input normally becomes *output* of some sort. Linux expects to send the output from your keyboard, *standard input*, to your monitor screen, *standard output*. In simpler terms, the system expects to take what you type and send it to your screen. That's why keyboard and monitor are referred to as *standard input* and *standard output*, respectively.

There are times when you want to change where the output is heading—you want to *redirect* it. There are many ways for this redirection to occur. We're going to use it here in one of its simplest forms.

Before we begin to create these files for our later exercises, we will experiment a bit with one simple option we have in creating these files: when to use `<Enter>`.

+   4. Create the first temporary file.
+       a. Type `cat > tempfile1`
+       Note that there is a space both before and after the redirection symbol, `>`.
+       b. Press `<Enter>`
+       c. Type: `This is tempfile1.`
+       d. Press `<Ctrl-D>`
+       <Ctrl-D> tells the system, “My input is complete. Create the file.”

+   5. Now take a look at `tempfile1`.
+       a. Type `cat tempfile1`
+       b. Press `<Enter>`
+       Your screen will look similar to Figure 6-2.

```
$ `cat tempfile1`
`This is tempfile1.$` |
```

**Figure 6-2 Shell Prompt Next to Text of *tempfile1***