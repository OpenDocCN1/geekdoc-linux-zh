in the output file. The bash shell automatically gives error messages a higher priority than the standard output. This allows you to view the error messages together, rather than scattered throughout the output file.

# Redirecting Output in Scripts

You can use the STDOUT and STDERR file descriptors to produce output in multiple locations by redirecting the appropriate file descriptors. There are two methods for redirecting output in the script:

+   - Temporarily redirecting each line
- Permanently redirecting all commands in the script

The following sections describe each of these methods work.

# Temporary redirections

If you want to purposely generate error messages in your script, you can redirect an individual output line to STDERR. All you need to do is use the output redirection symbol to redirect the output to the STDERR file descriptor. When you redirect to a file descriptor, you must precede the file descriptor number with an ampersand sign (&):

```
echo "This is an error message" >&2
```

This line displays the text wherever the STDERR file descriptor for the script is pointing, instead of the normal STDOUT. Here's an example of a script that uses this feature:

```
$ cat test8
!/bin/bash
# testing STDERR messages
```

```
echo "This is an error" >&2
echo "This is normal output"
$
```

If you run the script as normal, you won't notice any difference:

```
$ ./test8
This is an error
This is normal output
$
```

Remember, by default Linux directs the STDERR output to STDOUT. However, if you redirect STDERR, any text directed to STDERR in the script will be redirected:

```
$ ./test8 2> test9
This is normal output
```