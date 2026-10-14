the compressed version of the file has been replaced with the original, again with the permissions and time stamp preserved.

gzip has many options. Here are a few:

Table 19-1: gzip Options

| Option | Description |
| --- | --- |
| -c | Write output to standard output and keep original files. May also be specified with --stdout and --to-stdout. |
| -d | Decompress. This causes gzip to act like gunzip. May also be specified with --decompress or --uncompress. |
| -f | Force compression even if compressed version of the original file already exists. May also be specified with --force. |
| -h | Display usage information. May also be specified with --help. |
| -l | List compression statistics for each file compressed. May also be specified with --list. |
| -r | If one or more arguments on the command line are directories, recursively compress files contained within them. May also be specified with --recursive. |
| -t | Test the integrity of a compressed file. May also be specified with --test. |
| -v | Display verbose messages while compressing. May also be specified with --verbose. |
| -number | Set amount of compression. number is an integer in the range of 1 (fastest, least compression) to 9 (slowest, most compression). The values 1 and 9 may also be expressed as --fast and --best, respectively. The default value is 6. |

Going back to our earlier example:

```
[me@linuxbox ~]$ gzip foo.txt
[me@linuxbox ~]$ gzip -tv foo.txt.gz
foo.txt.gz: OK
[me@linuxbox ~]$ gzip -d foo.txt.gz
```

Here, we replaced the file foo.txt with a compressed version, named foo.txt.gz.