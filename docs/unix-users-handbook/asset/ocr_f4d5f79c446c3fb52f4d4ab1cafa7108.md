![](bbox=[0.86, 0.12, 0.98, 0.21])

# # split

# ## split - Split a file into multiple files.

split(1)
split(1)

# ### NAME

split - split a file into pieces

# ### SYNOPSIS

```
```
split [-l line_count] [-a suffix_length] [file [name]]

split [-b n[k|m]] [-a suffix_length] [file [name]]
```

```

**Obsolescent:**
```
split [-n] [file [name]]
```

# ### DESCRIPTION

split reads file and writes it in pieces (default 1000 lines) onto a set of output files. The name of the first output file is name with aa appended, and so on lexicographically, up to zz (only ASCII letters are used, a maximum of 676 files). If no output name is given, x is the default.

If no input file is given, or if - is given instead, the standard input file is used.

# ### OPTIONS

split recognizes the following command-line options and arguments:

+   - **-l line_count**
The input file is split into pieces line_count lines in size.
- **-a suffix_length**
suffix_length letters are used to form the suffix of the output filenames. This option allows creation of more than 676 output files. The output file names created cannot exceed the maximum file name length allowed in the directory containing the files.
- **-b n**
The input file is split into pieces n bytes in size.
- **-b nk**
The input file is split into pieces n * 1024 bytes in size. No space separates the n from the k.
- **-b nm**
The input file is split into pieces n * 1048576 bytes in size. No space separates the n from the m.
- **-n**
The input file is split into pieces n lines in size. This option is obsolescent and is equivalent to using the -l line_count option.

# ### EXTERNAL INFLUENCES