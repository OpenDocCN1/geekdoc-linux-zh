When you type your own -exec parameters, be sure to include a space before \;.
Otherwise, you might see an error such as missing argument to `-exec`.

Do you see now why some people think the find command is scary? Many people learn just enough about find to be able to use it in a very basic way, but hopefully you will see how much it can do if you give it a chance.

# Searches for a String in Input with grep

The grep command, like find, is an incredibly powerful search tool in the right hands. Unlike find, though, grep processes any text, whether in files, or just in standard input.

The basic usage of grep is this:

```
grep "some text" *
```

That searches all files in the current directory (but not subdirectories) for the string some text and prints matching lines along with the name of the file. To enable recursive searching in subdirectories, use the -r parameter, like this:

```
grep -r "some text" *
```

Each time a string is matched within a file, the filename and the match are printed. If a file contains multiple matches, each of the matches is printed. You can alter this behavior with the -l parameter (lowercase L), which forces grep to print the name of each file that contains at least one match, without printing the matching text. If a file contains more than one match, it is still printed only once. Alternatively, the -c parameter prints each filename that was searched and includes the number of matches at the end, even if there were no matches.

You have a lot of control when specifying the pattern to search for. You can, as we did previously, specify a simple string like some text, or you can invert that search by specifying the -v parameter. For example, this returns all the lines of the file myfile.txt that do not contain the word hello:

```
grep -v "hello" myfile.txt
```

You can also use regular expressions for your search term. For example, you can search myfile.txt for all references to cat, sat, or mat with this command:

```
grep "[cms]at" myfile.txt
```

Adding the -i parameter to that removes case sensitivity, matching Cat, CAT, MaT, and so on:

```
grep -i "[cms]at" myfile.txt
```

The output can also be controlled to some extent with the -n and --color parameters. The first tells grep to print the line number for each match, which is where it appears in