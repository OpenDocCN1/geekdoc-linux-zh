# Reusing an Expressions Value

Returning to the price list of fruits, say that we want to change the list to reflect that the prices are in dollars by appending the $ character in front of each of the prices. By using the following expression, we can match all the lines that end with a price:

```
/ *([0-9][0-9]?)\..[0-9][0-9]/
```

The problem is replacing the existing price with a price that is preceded by the $ character. It seems as though we would need to write a separate s command for each line in the file. Fortunately, the s command provides the & operator, which enables us to reuse the matched string from pattern1 in pattern2.

We can reuse the price that was matched as follows:

```
$ sed 's/*([0-9][0-9]?)\..[0-9][0-9]*/\$&/' fruit_prices.txt
Fruit      Price/lbs
Banana     $0.89
Peach      $0.79
Kiwi       $1.50
Pineapple  $1.22
Apple      $0.99
```

# Using Multiple sed Commands

As you can see from the last example, we were able to update the prices, but Peach remains misspelled as Paech. In order to perform both changes, you will have to perform more than one sed command on the file. This can be accomplished in one of two ways:

+   - Perform the first change and then update the file. Perform the second change command and then update the file.
+   - Perform both changes using a single sed command and then update the file.

As you can guess, the second method is much more efficient and less prone to error because the file is updated only once. You can perform both changes using a single sed command as follows:

```
sed -e 'cmd1'... -e 'cmdN' files
```

Here cmd1 ... cmdN are sed commands of the type discussed previously. Each command is applied to every line in each of the files specified by files.

We can perform both updates using either of the following commands:

```
$ sed -e 's/Paech/Peach/' -e 's/*([0-9][0-9]?)\..[0-9][0-9]*/\$&/' fruit_prices.txt
$ sed -e 's/*([0-9][0-9]?)\..[0-9][0-9]*/\$&/' -e 's/Paech/Peach/' fruit_prices.txt
```