then select **Contents**. When you are finished, click the **File** menu and select **Close** or **Quit**.

+   • To leave KDE altogether, use the **KDE Start** button and select **Logout**. You are returned to the Linux command-line prompt.

+   15. At the command line, invoke the help option for *mount*. How does Linux respond? Pay special attention to the options that Linux says can be used with *mount*.

+   16. Try to invoke *mount* but deliberately use an incorrect option. How does Linux respond?

+   17. Display the system’s date.

```
```
$ date<Enter>
```
```

+   18. Display a count of the number of lines in the */etc/passwd* file.

```
```
$ wc -1 /etc/passwd<Enter>
```
```

+   19. Display the entire calendar for the year 2002.

```
```
$ cal 2002<Enter>
```
```

Now, try displaying it with the addition of `| more`.

```
```
$ cal 2002 | more<Enter>
```
```

+   20. Display the month of September for the year 1752.

```
```
$ cal 9 1752<Enter>
```
```

Do you notice anything peculiar about September?

+   21. Display the month of August for the year 1999 and then for the year 99.

```
```
$ cal 8 1999<Enter>
$ cal 8 99<Enter>
```
```