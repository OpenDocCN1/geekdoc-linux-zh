Although **cat** is officially a tool for combining files, it’s also commonly used to display the contents of a short file. If you type only one filename as an option, **cat** displays that file. This is a great way to review short files; but for long files, you’re better off using a full-fledged pager command, such as **more** or **less**.

You can add options to have **cat** perform minor modifications to the files as it combines them:

+   - **Display line ends**: If you want to see where lines end, add the `-E` or `--show-ends` option. The result is a dollar sign ($) at the end of each line.
+   - **Number lines**: The `-n` or `--number` option adds line numbers to the beginning of every line. The `-b` or `--number-nonblank` option is similar, but it numbers only lines that contain text.
+   - **Minimize blank lines**: The `-s` or `--squeeze-blank` option compresses groups of blank lines down to a single blank line.
+   - **Display special characters**: The `-T` or `--show-tabs` option displays tab characters as `^I`. The `-v` or `--show-nonprinting` option displays most control and other special characters using caret (^) and M- notations.

The **tac** command is similar to **cat**, but it reverses the order of lines in the output.

# ## Joining Files by Field with join

The **join** command combines two files by matching the contents of specified fields within the files. Fields are typically space-separated entries on a line, although you can specify another character as the field separator with the `-t *char*` option, where *char* is the character you want to use. You can cause **join** to ignore case when performing comparisons by using the `-i` option.

The effect of **join** may best be understood through a demonstration. Consider Listings 1.1 and 1.2, which contain data on telephone numbers—Listing 1.1 shows the names associated with those numbers, and Listing 1.2 shows whether the numbers are listed or unlisted.

```
Listing 1.1: Demonstration File Containing Telephone Numbers and Names
```
555-2397  Beckett, Barry
555-5116  Carter, Gertrude
555-7929  Jones, Theresa
555-9871  Orwell, Samuel
```
```

```
Listing 1.2: Demonstration File Containing Telephone Number Listing Status
```
555-2397 unlisted
555-5116 listed
555-7929 listed
555-9871 unlisted
```
```