
```
find ~ -print
```

We can use find to delete files that meet certain criteria. For example, to delete files that have the file extension “.BAK” (which is often used to designate backup files), we could use this command:

```
find ~ -type f -name '*.BAK' -delete
```

In this example, every file in the user’s home directory (and its subdirectories) is searched for filenames ending in .BAK. When they are found, they are deleted.

> Warning: It should go without saying that you should use extreme caution when using the -delete action. Always test the command first by substituting the -print action for -delete to confirm the search results.

Before we go on, let’s take another look at how the logical operators affect actions. Consider the following command:

```
find ~ -type f -name '*.BAK' -print
```

As we have seen, this command will look for every regular file (-type f) whose name ends with .BAK (-name '*.BAK') and will output the relative pathname of each matching file to standard output (-print). However, the reason the command performs the way it does is determined by the logical relationships between each of the tests and actions. Remember, there is, by default, an implied -and relationship between each test and action. We could also express the command this way to make the logical relationships easier to see:

```
find ~ -type f -and -name '*.BAK' -and -print
```

With our command fully expressed, let’s look at how the logical operators affect its execution:

| Test/Action | Is Performed Only If... |
| -print | -type f and -name '*.BAK' are true |

In this example, we search for files with names starting with the string “foo” and execute the command ls -l each time one is found. Using the -ok action prompts the user before the ls command is executed.

## Improving Efficiency

When the -exec action is used, it launches a new instance of the specified command each time a matching file is found. There are times when we might prefer to combine all of the search results and launch a single instance of the command. For example, rather than executing the commands like this:

```
ls -l file1
```

```
ls -l file2
```

we may prefer to execute it this way:

```
ls -l file1 file2
```

thus causing the command to be executed only one time rather than multiple times. There are two ways we can do this. The traditional way, using the external command xargs and the alternate way, using a new feature in find itself. We’ll talk about the alternate way first.

By changing the trailing semicolon character to a plus sign, we activate the ability of find to combine the results of the search into an argument list for a single execution of the desired command. Going back to our example, this:

```
find ~ -type f -name 'foo*' -exec ls -l '{}' ';'
-rwxr-xr-x 1 me me 224 2007-10-29 18:44 /home/me/bin/foo
-rw-r--r-- 1 me me 0 2008-09-19 12:53 /home/me/foo.txt
```

will execute ls each time a matching file is found. By changing the command to:

```
find ~ -type f -name 'foo*' -exec ls -l '{}' +
-rwxr-xr-x 1 me me 224 2007-10-29 18:44 /home/me/bin/foo
-rw-r--r-- 1 me me 0 2008-09-19 12:53 /home/me/foo.txt
```

we get the same results, but the system only has to execute the ls command once.

## xargs

The xargs command performs an interesting function. It accepts input from standard input and converts it into an argument list for a specified command. With our example, we would use it like this:

```
find ~ -type f -name 'foo*' -print | xargs ls -l
-rw-xr-xr-x 1 me me 224 2007-10-29 18:44 /home/me/bin/foo
-rw-r--r-- 1 me me 0 2008-09-19 12:53 /home/me/foo.txt
```

Here we see the output of the find command piped into xargs which, in turn, constructs an argument list for ls command and then executes it.

Note: While the number of arguments that can be placed into a command line is quite large, it's not unlimited. It is possible to create commands that are too long for the shell to accept. When a command line exceeds the maximum length supported by the system, xargs executes the specified command with the maximum number of arguments possible and then repeats this process until standard input is exhausted. To see the maximum size of the command line, execute xargs with the --show-limits option.

## Dealing With Funny Filenames

Unix-like systems allow embedded spaces (and even newlines!) in filenames. This causes problems for programs like xargs that construct argument lists for other programs. An embedded space will be treated as a delimiter and the resulting command will interpret each space-separated word as a separate argument. To overcome this, find and xarg allow the optional use of a null character as argument separator. A null character is defined in ASCII as the character represented by the number zero (as opposed to, for example, the space character, which is defined in ASCII as the character represented by the number 32). The find command provides the action -print0, which produces null separated output, and the xargs command has the --null option, which accepts null separated input. Here's an example:

```
find ~ -iname '*.jpg' -print0 | xargs --null ls -l
```

Using this technique, we can ensure that all files, even those containing embedded spaces in their names, are handled correctly.
