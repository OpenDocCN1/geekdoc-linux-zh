4. How about a quick gauge of how many users are on the system?

% who | wc -l
12

5. How many accounts are on your computer?

% cat /etc/passwd | wc -l
3877

The command is a great example of the simplest of commands, combined in a sophisticated pipeline, can be very powerful.

# Task 8.3: Removing Extraneous Lines Using uniq

Sometimes you're looking at a file, you'll notice that there are duplicate entries, either blank lines or, perhaps, lines of repeated information. To clean up these files and shrink their size at the same time, you can use the uniq command, which lists each unique line in the file.

Well, it is sort of lists each unique line in the file. What uniq really compares each line it reads with the previous line. If the lines are the same, uniq does not list the second line. You can use flags with uniq to get specific results: -u lists only lines that are not repeated, -d lists only lines that are repeated (the exact opposite of -u), and -c adds a count of how many times each occurred.

+   1. If you use uniq on a file that doesn't have any common lines, uniq has no effect.

| uniq testme keyptime.pie |
| Archives/ | bnr/ src/ |
| Infold/ | bitnet.mailing-lines.2 temp/ |
| News/ | drop.test.htq testme |

+   2. A trick using the cat command that lists the contents of each file sequentially, even if you specify the same file and over again, so you can easily build a file with lines of:

```
% cat testme testme > newest
```

Examine newest to verify that it contains three copies of testme, one after the other. (Try using wc.)

+   3. Now you have a file with duplicate lines. Will uniq realize these files have duplicate lines? Use wc to find out:

```
% wc newest
12 36 363
% uniq newest | wc
12 36 363
```