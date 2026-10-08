# 8.18.1 Analyzing Suspicious Files

> When suspicious files are found, it would be helpful to do some analysis on them. Accidentally doing a cat command on a binary is unpleasant. The file command is another innovation from the distant UNIX past. For those who are not familiar with it, file does a sophisticated analysis of a file's contents to determine and report what kind of file it is, regardless of its name or extension.

Most binary file formats start with a unique byte sequence that find will recognize. ASCII-table of file formats is called magic and is usually found in /usr/share, but sometimes in /etc. It has hundreds of patterns for recognizing scripts for various shells, perl, awk, and so on and almost every binary in common use, even those that are not supported on Linux.

For each on its command line (or standard input as a filename of " " is given), it will list the file's name and its analysis of file content. It will not reveal the contents of the file tree itself so, generally, it should not be considered an invasion of privacy to run it on user directories tree if there is a security justification for it. Such justification might be a search for files with parameters that are indications of suspicious activity, such as file names beginning with.

The file command may be combined with a find invocation to analyze suspicious files. Examples would be

```
(find / ! -fstype proc -perm +6000 -ls \
; find / ! -fstype proc -perm +6000 \
-print | xargs -n 50 md5sum \
; find / ! -fstype proc -perm +6000 \
-print | xargs -n 50 file) \
sort | diff want_su - \\
Mail -s 'SU changed' admin@yoursite.com
and
```

```
(find / ! -fstype proc '(' -nouser -o -nogroup ') -ls \
; find / ! -fstype proc '(' -nouser -o -nogroup ') \
-print | xargs -n 50 file) \
Mail -s 'Unowned files' admin@yoursite.com
```