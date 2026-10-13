we find that the lines for fruit with prices less than a dollar are printed twice, whereas lines for fruit with prices greater than a dollar are printed only once. This demonstrates the default behavior of sed—it prints every input line to the output. To avoid this behavior, we can specify the -n option to sed as follows:

```
$ sed -n '/0.[0-9][0-9]$/p' fruit_prices.txt
```

This changes the output as follows:

```
Banana 0.89
Peach 0.79
Apple 0.99
```

# Deleting Lines

Say that we run out of mangos and thus need to delete them from the list. To accomplish this task, we can use the sed command d:

```
/pattern/d
```

Here pattern is a regular expression.

We can use the following sed command:

```
$ sed '/^[Mm]ango/d' fruit_prices.txt
```

This command deletes lines that start with the words mango or Mango. The output is as follows:
Fruit Price/lbs
Banana 0.89
Peach 0.79
Kiwi 1.50
Pineapple 1.29
Apple 0.99

Notice that you did not have to specify the -n option to sed to get the correct output. The p command tells sed to produce additional output, whereas the d command tells sed to modify the regular output.

Although you have modified the output and have verified that it is correct, the file still needs to be updated. You can do this with the help of the shell:
$ mv fruit_prices.txt fruit_prices.txt.$$
$ sed '/^[Mm]ango/d' fruit_prices.txt.$$ > fruit_prices.txt
$ cat fruit_prices.txt

First, we rename the file fruit_prices.txt to fruit_prices.txt.$$. Recall that the value of the variable $$ is the process ID of the current shell. Appending the value of $$ to the end of a file is a commonly used method for creating temporary files with unique names.