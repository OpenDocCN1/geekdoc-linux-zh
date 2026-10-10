# DIAGNOSTICS

Normally, exit status is 0 if matches were found, and 1 if no matches were found. (The `-v` option inverts the sense of the exit status.) Exit status is 2 if there were syntax errors in the pattern, inaccessible input files, or other system errors.

# BUGS

E-mail bug reports to `bug-gnu-utils@prep.ai.mit.edu`. Be sure to include the word “grep” somewhere in the Subject: field.

Large repetition counts in the $(m, n)$ construct may cause `grep` to use lots of memory. In addition, certain other obscure regular expressions require exponential time and space, and may cause `grep` to run out of memory.

Backreferences are very slow, and may require exponential time.

# GZIP(1)

# NAME

`gzip`, `gunzip`, `zcat`	Compress or expand files.

# SYNOPSIS

```
```
gzip [-acdflhLlnNrtVv19] [-S suffix] [name ...]
gunzip
[-acdflhLlnNrtV] [-S suffix] [name ...] zcat [-fhLV] [name ...]
```
```

# DESCRIPTION

gzip reduces the size of the named files using Lempel-Ziv coding (LZ77). Whenever possible, each file is replaced by one with the extension `.gz`, while keeping the same ownership modes, access and modification times. (The default extension is `.gz` for VMS, `z` for MSDOS, OS/2 FAT, Windows NT FAT and Atari.) If no files are specified, or if a file name is `-`, the standard input is compressed to the standard output. gzip will only attempt to compress regular files. In particular, it will ignore symbolic links.

If the compressed file name is too long for its file system, gzip truncates it. gzip attempts to truncate only the parts of the file name longer than three characters. (A part is delimited by dots.) If the name consists of small parts only, the longest parts are truncated. For example, if file names are limited