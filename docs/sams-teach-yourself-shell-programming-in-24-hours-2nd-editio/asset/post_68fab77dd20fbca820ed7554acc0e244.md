
![](img/3def70414996f811615f713b2077a154_272_0.png)

> In order to match \, you can escape it using itself: \\.

## Useful Regular Expressions

Table 16.3 provides some useful regular expressions.

TABLE 16.3 Some Useful Regular Expressions

| String Type | Expression |
|---|---|
| Blank lines | /^$/ |
| An entire line | /^.*$/ |
| One or more spaces | / +/ |
| HTML (or XML) tag sets | /<[^>]+>/ |
| Valid URLs | /[a-zA-Z][a-zA-Z0-9+.-]*:\/\/[a-zA-Z0-9][a-zA-Z0-9.-]*\.[a-zA-Z]{2,}/ |
| Formatted dollar amounts | /[$][0-9]+(\.[0-9]{2})?/ |

## Using sed

sed is a stream editor that performs a set of actions on every line of its input. This allows sed to be used as a filter. The basic syntax of a sed command is

`sed 'script' files`

Here files is a list of one or more files, and script is one or more commands of the form

`/pattern/ action`

where pattern is a regular expression and action is one of the commands given in Table 16.4. If pattern is omitted, action is performed for every line of input.

TABLE 16.4 Some of the Actions Available in sed

| Action | Description |
|---|---|
| p | Prints the line (p as in print) |
| d | Deletes the line (d as in delete) |
| s | Substitutes one expression with another (s as in substitute) |

### Printing Lines

Let's start with the simplest feature available in sed—printing a line that matches an expression.

The following is a price list for a small fruit market:

```
$ cat fruit_prices.txt
Fruit    Price/lbs
Banana   0.89
Peach    0.79
Kiwi     1.50
Pineapple 1.29
Apple    0.99
Mango    2.20
```

This file lists the name of a fruit and its price per pound. Most of the following examples assume that this list is stored in the file fruit_prices.txt.

To start with, let's print out a list of those fruits that cost less than $1 per pound. We will need to use the sed command p:

```
/pattern/p
```

Here pattern is a regular expression.

Let's try the following sed command:

```
$ sed '/ 0.[0-9][0-9]$/p' fruit_prices.txt
```

This will print all the lines that match the expression:

```
/ 0.[0-9][0-9]$/
```

This expression specifies that only lines ending in prices such as 0.89 and 0.99 should be printed. The leading 0 ensures that lines ending in prices such as 2.20 or 10.10 are not printed.

Looking at the output,

```
Fruit    Price/lbs
Banana   0.89
Banana   0.89
Peach    0.79
Peach    0.79
Kiwi     1.50
Pineapple 1.29
Apple    0.99
Apple    0.99
Mango    2.20
```

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

### Deleting Lines

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

Next, we use sed to delete the lines starting with Mango or mango from the temporary file. Then the output of the sed command is redirected into the file fruit_prices.txt.

We used cat to show us that the update was successful:

| Fruit | Price/lbs |
| Banana | 0.89 |
| Paech | 0.79 |
| Kiwi | 1.50 |
| Pineapple | 1.29 |
| Apple | 0.99 |

Now that we know that the update happened correctly, we can remove the temporary file as follows:

```
$ rm fruit_prices.txt.$$
```

### Performing Substitutions

By now you might have noticed that Peach is misspelled as Paech in our file. We can fix this by substituting Paech with the correct spelling using the sed command s:

```
/pattern1/s/pattern2/pattern3/
```

Here pattern1, pattern2, and pattern3 are regular expressions. The s command replaces pattern2 with pattern3 on any line that matches pattern1.

Frequently pattern1 is omitted, so you see the s command used as follows:

```
s/pattern2/pattern3/
```

If pattern1 is omitted, the s command is executed for every input line.

To fix the spelling of Paech, you can use the following sed command:

```
$ sed 's/Paech/Peach/' fruit_prices.txt
```

Now the output resembles the following:

| Fruit | Price/lbs |
| Banana | 0.89 |
| Peach | 0.79 |
| Kiwi | 1.50 |
| Pineapple | 1.29 |
| Apple | 0.99 |

You did not have to specify the -n option to sed to obtain the desired output. The s command is similar to the d command in that it tells sed to modify its normal output.

### Common Errors

A common error with the s command is forgetting one or more of the / characters. For example, say that you were to issue the following command:

```
$ sed 's/Peach/Peach' fruit_prices.txt
```

An error message similar to the following is produced:

```
sed: command garbled: s/Peach/Peach
```

This error message illustrates the standard style for sed error messages:

```
sed: command garbled: command
```

sed just repeats the command and states that it could not understand it. No additional error messages or information are produced, so you have to determine what went wrong yourself.

### Performing Global Substitutions

In the last example, you just needed to fix a single misspelling on a single line. Sometime you might need to perform multiple corrections. As an example, take a look at the following file:

```
$ cat nash.txt
```

things that are equal to the same thing are equal to each other

In this file, the word equal is misspelled as eqal. You can try to fix this using the s command as follows:

```
$ sed 's/eqal/equal/' nash.txt
```

things that are equal to the same thing are equal to each other

As you can see, the first misspelling was fixed, but the second one was not. This is the default behavior of the s command: It only performs one substitution on a line. To perform more than one substitution, we need to use the g (as in global) operator:

/pattern1/s/pattern2/pattern3/g

The g operator tells the s command to substitute every occurrence of pattern2 with pattern3 on lines matching pattern1. If pattern1 is omitted, every line of input is operated on.

In this case, we need to use the g operator as follows:

```
$ sed 's/eqal/equal/g' nash.txt
```

### Reusing an Expressions Value

Returning to the price list of fruits, say that we want to change the list to reflect that the prices are in dollars by appending the $ character in front of each of the prices. By using the following expression, we can match all the lines that end with a price:

/ *([0-9][0-9]?)\.[0-9][0-9]/

The problem is replacing the existing price with a price that is preceded by the $ character. It seems as though we would need to write a separate s command for each line in the file. Fortunately, the s command provides the & operator, which enables us to reuse the matched string from pattern1 in pattern2.

We can reuse the price that was matched as follows:

```
$ sed 's/ *([0-9][0-9]?)\.[0-9][0-9]/\$&/' fruit_prices.txt
Fruit      Price/lbs
Banana     $0.89
Peach      $0.79
Kiwi       $1.50
Pineapple  $1.29
Apple      $0.99
```

### Using Multiple sed Commands

As you can see from the last example, we were able to update the prices, but Peach remains misspelled as Paech. In order to perform both changes, you will have to perform more than one sed command on the file. This can be accomplished in one of two ways:

- Perform the first change and then update the file. Perform the second change command and then update the file.
- Perform both changes using a single sed command and then update the file.

As you can guess, the second method is much more efficient and less prone to error because the file is updated only once. You can perform both changes using a single sed command as follows:

```
sed -e 'cmd1'... -e 'cmdN' files
```

Here cmd1 ... cmdN are sed commands of the type discussed previously. Each command is applied to every line in each of the files specified by files.

We can perform both updates using either of the following commands:

```
$ sed -e 's/Paech/Peach/' -e 's/ *([0-9][0-9]?)\.[0-9][0-9]/\$&/' fruit_prices.txt
$ sed -e 's/ *([0-9][0-9]?)\.[0-9][0-9]/\$&/' -e 's/Paech/Peach/' fruit_prices.txt
