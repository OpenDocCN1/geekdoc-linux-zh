# uniq

Syntax: `uniq [-c] filename`

The `uniq` command compares adjacent lines and displays only one unique line. When used with the `-c` option, `uniq` counts the number of occurrences. A file that has the contents

```
```
a
a
a
b
a
```
```

produces the following result when used with `uniq`:

```
```
uniq test.txt
a
b
a
```
```

Notice how the adjacent `a`'s were removed but not all `a`'s in the file. This is an important detail to remember when using `uniq`. If you want to find all the unique lines in a file called `test.txt`, run the following command:

```
```bash
sort test.txt | uniq
```
```

This command sorts the `test.txt` file and puts all the similar lines next to each other, allowing `uniq` to display only the unique lines. For example, suppose you want to find out quickly how many unique visitors came to your Web site. Run the following command:

```
```bash
awk '{print $1}' access.log | sort | uniq
```
```

This displays the unique IP addresses in a CLF log file, which is what Apache Web server uses.

# vi

The `vi` program is a powerful, full-screen text editor that can almost certainly be found on all Unix systems because of its size and capabilities. `vi` does not require much in the way of resources to utilize its features. In