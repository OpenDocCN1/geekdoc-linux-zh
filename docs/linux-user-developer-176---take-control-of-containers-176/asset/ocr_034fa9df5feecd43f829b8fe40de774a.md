# file

**MODULE**
file

**MODULE SUMMARY**
File interface module.

**DESCRIPTION**

This module provides an interface to the file system.

On operating systems with thread support, file operations can be performed in threads of their own, allowing other Erlang processes to continue executing in parallel with the file operations. See command-line flag **+A** in `ez1(1)`. 

Regarding filename encoding, the Erlang VM can operate in two modes. The current mode can be queried using function `native_name_encoding/0`; it returns `latin1` or `utf8`.

In `latin1` mode, the Erlang VM does not change the encoding of filenames. In `utf8` mode, filenames can contain Unicode characters greater than 255 and the VM converts filenames back and forth to the native filename encoding (usually UTF-8, but UTF-16 on Windows).

The default mode depends on the operating system: Windows and MacOS X enforce consistent filename encoding and therefore the VM uses `utf8` mode.

On operating systems with transparent naming (for example, all Unix systems except MacOS X), default is `utf8` if the terminal supports UTF-8, otherwise `latin1`. The default can be overridden using `+fnl` (to force `latin1` mode) or `+fnu` (to force `utf8` mode) when starting `xerl(1)`. 

On operating systems with transparent naming, files can be inconsistently named, for example, some files are encoded in UTF-8 while others are encoded in ISO Latin-1. The concept of *raw filename* is introduced to handle file systems with inconsistent naming when running in `utf8` mode.

*A raw filename* is a filename specified as a binary. The Erlang VM does not translate a filename specified as a binary on systems with transparent naming.

When running in `utf8` mode, functions `list_dir/1` and `read_link/1` never return raw filenames. To return all filenames including raw filenames, use functions `list_dir_all/1` and

# Opening text files for reading

The following Erlang code opens a file that is identified by file for reading:

```
{ok, FD} = file:open(File, [read])
```

The use of `file:open()` is illustrated in `workText.erl`. Executing `lineByLine/1` from `workText.erl` generates the following kind of output:

```
1> c(workText).
[ok, workText]
2> workText:lineByLine("cmdArgs.erl").
-module(cmdargs).
ok.
```

The `lineByLine/1` function reads a file line by line and prints its contents with the help of the `read_line_by_line(FD)` function.

As you can see, opening a file for reading can fail for various reasons, including file not found and not having the right file permissions to open a file. So, if there is such an error somewhere, you will get the following kind of error message:

```
4> workText:lineByLine("cmdargs").
** exception error: no match of right hand side
value {error,enent}
5> in function workText:lineByLine/1 (workText.erl, line 5)
```

Learning to interpret and work with error messages is critical and handy because it allows you to decide what to do depending on the kind of error you get. Please note that you are going to get the same error message when you are dealing with a binary file.

*Figure 1* (overleaf) shows the implementation of both `lineByLine/1` and `read_line_by_line/1` functions as found in `workText.erl`. The `file:read_line()` function reads a single line from a file.

# Opening text files for writing

In order to open a file for writing, you will need to change the value of the second argument of the `file:open()` function, which is the *Mode*. If the file you are opening for writing already exists, it will be truncated, so be extra careful with it. If you do not want this behaviour, use the append mode.

*Figure 2* shows the implementation of `writeToFile/1` that illustrates the use of the `file:write()` function. Executing `writeToFile/1` generates the following results:

```
1> c(workText).
{ok, workText}
2> workText:writeToFile("./testing").
ok
3> q().
ok
4> $ cat testing
A Message.
```

# Error handling

Error handling is a crucial task when you have to deal with file read and write operations because many things can go wrong during file I/O. Once again, error handling in