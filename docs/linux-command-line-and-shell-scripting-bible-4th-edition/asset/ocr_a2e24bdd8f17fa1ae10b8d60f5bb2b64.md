directory.

> **NOTE**
> 
> The pipe command (|) used in this example redirects the output of the du command to the sort command. That's discussed in more detail in Chapter 11, “Basic Script Building.”

# ### Searching for data

Often in a large file, you have to look for a specific line of data buried somewhere in the middle of the file. Instead of manually scrolling through the entire file, you can let the grep command search for you. The command-line format for the grep command is

```
grep [options] pattern [file]
```

The grep command searches either the input or the file you specify for lines that contain characters that match the specified pattern. The output from grep is the lines that contain the matching pattern. Here are two simple examples of using the grep command with the filel file used in the “Sorting Data” section:

```
$ grep three file1
three
$ grep t file1
two
three
$
```

The first example searches the file filel for text matching the pattern three. The grep command produces the line that contains the matching pattern. The next example searches the file filel for the text matching the pattern t. In this case, two lines matched the specified pattern, and both are displayed. Because of the popularity of the grep command, it has undergone lots of development changes over its lifetime. Many features have been