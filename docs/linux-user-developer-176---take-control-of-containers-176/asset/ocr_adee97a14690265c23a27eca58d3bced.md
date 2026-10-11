# # Tutorial

Erlang

**Right.** The code of the `workBin:visit()` function that walks a directory tree in Erlang

![](bbox=[0.19, 0.15, 0.44, 0.45])

![](bbox=[0.53, 0.15, 0.75, 0.39])

**Across.** How you can find information about a module from the Erlang shell. The output also includes the names of the functions that are exported

The `filelib:file_size()` function returns the size of a file or a directory that is given as a parameter to it:

```
5> filelib:file_size(".").
4096
```

The `filelib:is_file()` and `filelib:is_dir()` functions enable you to determine whether the given path is a file or a directory, respectively:

```
6> filelib:is_file(".").
true

7> filelib:is_dir(".").
true

8> filelib:is_file("wc.erl").
false

9> filelib:is_file("wc.erl").
true

10> filelib:is_dir("/dev/random").
false

11> filelib:is_file("/dev/random").
False
```

As you can see, `filelib:is_file()` considers directories as files but can differentiate between regular files and special files such as `/dev/random`.

# ## Visiting all files in a directory tree

There is a very frequent need to visit all files in a directory and its subdirectories. This section will teach you how to perform this task in Erlang. Once again, the developed function requires one argument, which is a directory, and returns the desired information. The `visit()` function is included in the `workBin.erl` file. Executing `visit()`

generates the following kind of output:

```
3> workBin:visit("/var/spool").

/var/spool
/var/spool/cups
/var/spool/mqueue
```

You can see the related Erlang code in **Figure 6**. The most important Erlang function in the implementation of `visit()` is `filelib:wildcard()`, which returns the list of files that match the given criteria.

The `filelib` file holds the definition of the `file_info` record - the information in `file_info` allows you to determine the type of file you are dealing with. On a Debian Linux system, the `file.erl` file can be found at `/usr/lib/erlang/lib/kernel-5.1.1/include`. You can find more information about the data that `file_info` holds at: erlang.org/doc/man/file.html

# ## Finding information about files

The following code illustrates how you can find more information about files using the `file_info` record:

```
file_permissions(Path) ->
    case file:read_file_info(Path) of
        {ok, FR} -> io:lib:format("~.8B", [FR#file_info.mode band 8#777]);
        _ -> error
    end.
```

The previous code prints the file permissions of a file or a directory. Please bear in mind that although `file:read_file_info()` contains information about file size and type, calling `file:file_size()` and `is_dir()` is more practical than using `file:read_file_info()`. However, note that some of the data returned by `file:read_file_info()` cannot be discovered using other Erlang functions. Executing `file_permissions()` generates the next kind of output: