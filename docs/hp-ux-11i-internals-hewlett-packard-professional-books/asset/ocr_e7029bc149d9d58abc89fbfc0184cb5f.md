you want to examine, how many of them to load, and how to find them. The simplest form of the `load` command is `load <type> from <address>`. The type can be any publicly visible kernel structure or typedef. If you're using a structure, you must include the `struct` keyword. The address can either be a numeric value or a symbol. For example, to load the first `mpinfo` struct from the `mproc_info` array, we would type

```
q4> load struct mpinfo from mproc_info
```

Because `struct mpinfo` is also typedefed to `mpinfo_t`, we could also say

```
q4> load mpinfo_t from mproc_info
```

# Displaying the Contents of a Pile

Once you've got a pile with a structure in it, you need to be able to look at the data. To print that pile, we use the `print` command. The `print` command with no arguments prints out the entire structure. If you're going to print a lot of elements, you probably want to add the `-t` flag to the `print` command. This option tells the command to print one element per line with the names on the left rather than print the data in columns with the names across the top. The `mpinfo` structure is very large—it has over 2,000 elements in it—so even with the `-t` option, you'll get over 2,000 lines of output. Fortunately, you don't have to see it all.

You can pipe `q4` commands through shell commands. So, after you've got your `mpinfo` pile loaded, you might want to do `print -tx | more` to see it a page at a time. You could find out how many items there are in an `mpinfo` structure by doing `print -tx | wc -l`. You can also tell `q4` exactly which items to print. If you type `print -tx procindex prochnpa`, you'll get something like the following:

```
procnindex      0
prochnpa      0xfffffffffed21000
```

# Using Skip to Load Structures

So far, we've loaded up the first `mpinfo` structure into a pile. But `mpinfo` is an array—what if you want to look at the `mpinfo` structures for other processors? The `skip` keyword tells `q4` how many array elements to skip over. If you want to look at the second entry (the entry for processor 1), for example, type

```
q4> load struct mpinfo from mproc_info skip 1
```

Now, if we look at `procnindex` and `prochnpa`, we get

```
procnindex      0x1
prochnpa      0xfffffffffed61000
```