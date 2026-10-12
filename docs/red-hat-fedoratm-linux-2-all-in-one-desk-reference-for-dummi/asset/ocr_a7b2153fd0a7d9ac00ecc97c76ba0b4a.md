# **Saving command output in a file**

To save the output of a command in a file, redirect the standard output to a file. For example, type `cd` to change to your home directory and then type the following command:

```
grep typedef /usr/include/* > typedef.out
```

This command searches through all files in the `/usr/include` directory for the occurrence of the text `typedef` — and then saves the output in a file called `typedef.out`. The greater-than sign (>) redirects `stdout` to a file. This command also illustrates another feature of Bash. When you use an asterisk (*), Bash replaces the asterisk with a list of all filenames in the specified directory. Thus, `/usr/include/*` means *all the files in the* `/usr/include` directory.

![](bbox=[0.13, 0.4, 0.22, 0.46])

If you want to append a command’s output to the end of an existing file instead of saving the output in a new file, use two greater-than signs (>>) like this:

```
command >> filename
```

# **Saving error messages in a file**

Sometimes you type a command and it generates a whole lot of error messages that scroll by so fast you can’t tell what’s going on. One way to see all the error messages is to save the error messages in a file so that you can see what the heck happened. You can do that by redirecting `stderr` to a file.

For example, type the following command:

```
find / -name COPYING -print 2> finderr
```

This command looks throughout the file system for files named `COPYING`, but saves all the error messages in the `finderr` file. The number `2` followed by the greater-than sign (2>) redirects `stderr` to a file.

![](bbox=[0.13, 0.81, 0.22, 0.87])

If you want to simply discard the error messages instead of saving them in a file, use `/dev/null` as the filename, like this:

```
find / -name COPYING -print 2> /dev/null
```

![](bbox=[0.13, 0.87, 0.22, 0.94])

That `/dev/null` is a special file — often called the *bit bucket* and sometimes glorified as the *Great Bit Bucket in the Sky* — that simply discards whatever it receives. So now you know what they mean when you hear phrases such as, “Your mail probably ended up in the bit bucket.”