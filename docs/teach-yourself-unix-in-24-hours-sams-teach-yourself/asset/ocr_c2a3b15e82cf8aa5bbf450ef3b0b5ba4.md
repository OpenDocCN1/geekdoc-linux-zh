They're the same. Remember, the uniq command removes duplicate lines only if they're adjacent.

4. Create a file that has duplicate lines:

```
% tail -1 testme > lastline
% cat lastline lastline lastline > newtest2
% cat newtest2
News/ drop.text.hx testme
News/ drop.text.hx testme
News/ drop.text.hx testme
News/ drop.text.hx testme
```

Now you can see what uniq does:

+   - uniq newtest2
News/ drop.text.hx testme

5. Obtain a count of the number of occurrences of each line in the file. The -c flag does that job:

+   - uniq -c newtest2
4 News/ drop.text.hx testme

This shows that line occurs four times in the file. Lines that are unique have no number prefix.

6. You also see what the -d and -u flags do, and how they have exactly opposite actions:

+   - uniq -d newtest2
News/ drop.text.hx testme
% uniq -u newtest2
%

Why did the -u flag list nothing? The answer is that the -u flag tells uniq to list only those lines that are not repeated in the file. Because the only line in the file is repeated four times, there's nothing to display.

Given this example, you probably think uniq is of marginal value, you will find that it's uncommon for files to have many blank lines scattered throughout the text. The uniq command is a fast, easy, and powerful way to clean up such files.

# Task 8.4: Sorting Information in a File Using sort

Whereas it is useful at the end of a pipeline of commands, uniq is a filter, a program that is really designed to be tucked in the middle of a pipeline. Filters, of course, can be placed anywhere in a line, anywhere enables them to help direct uniq to. The common characteristic of UNIX filters is that they can read from standard input, process it in one manner, and leave the results in standard output. With file redirection, standard input and output are also files. To do this, you can either specify the filenames to the command (usually input only) or use the file-redirection symbols learned earlier in this hour (<, >, >>).

![](bbox=[0.062, 0.886, 0.145, 0.966])