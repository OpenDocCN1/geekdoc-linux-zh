Select all the lines in the RFI_Tel2 file that contain a plus sign ( + ):

```
$ grep '\+' RFI_Tel2<Enter>
```

# Other grep Commands: egrep and fgrep

We have already discussed how `grep` can be extremely useful when you have to extract text from a data stream, such as a text file. (Yes, `grep` can be used for other types of data streams, but this usage is not covered here.) The command’s functionality or performance for extracting text in particular situations is further enhanced by the `egrep` and `fgrep` commands.

# egrep: Searching for Alternates

The `grep` command itself cannot be used for the type of search request where you want to find all strings containing one item or another. The extended `grep` command, `egrep`, enables OR searches by letting you put a pipe symbol ( | ) between your specified alternate search expressions, as shown in Example 8.14. The `egrep` command also works with `grep`’s metacharacters and options. The `egrep` command is a little slower than a normal `grep`, mostly because it executes more than one `grep` process.

# Example 8.14 egrep

Lady Dulcinea wants to know how many 800 numbers the RFI has to pay for. She also wants to know whether RFI has any 900 numbers:

```
$ egrep '800|900' RFI_Tel3<Enter>
Emergencies - +34 91 800 09 87
Human Resources - +34 91 900 55 87
```

Although she is not sure why the human resources department has a 900 number, she is satisfied that the emergencies number is an 800 number.

# Faster Searching for Fixed Strings with fgrep

The `fgrep` command is similar to `grep` but does not provide the regular expression capability. Instead, you are limited to searching for fixed text strings, as shown in Example 8.15. This command enables you to use the