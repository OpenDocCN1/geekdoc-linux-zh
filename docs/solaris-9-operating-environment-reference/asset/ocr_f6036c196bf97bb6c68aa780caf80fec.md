# diff 253

Attributes
See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SunWcsr |

See Also
hcpagent(1M), ifconfig(1M), init(1M), dhcp_inittab(4), attributes(5) NewM!
Alexander, S., and R. Droms, DHCP Options and BOTP Vendor Extensions, RFC 2132,
Silicon Graphics, Inc., Bucknell University, March 1997.

# diff — Display Line-by-Line Differences between Pairs of Text
Files

# Synopsis

```
/usr/bin/diff [-bitw] [-c | -e | -f | -h | -n | -u] file1 file2 NewM!
/usr/bin/diff [-bitw] [-C number | -U number] file1 file2 NewM!
/usr/bin/diff [-bitw] [-D string] file1 file2
/usr/bin/diff [-bitw] [-c | -e | -f | -h | -n] [-1] [-r] [-S name]
file1 file2
```

# Description

The diff command compares the contents of file1 and file2 by line and produces
a complete index of all of the lines that differ between the two files, along with their line
numbers. It also reports what must be changed to make the files match. No output is
produced if the files are identical.

The example illustrates the diff output for two simple files.
caste$ diff kookaburra1 kookaburra2
4c4
< Gay your life must be.
----
> Glad your life must be.
caste$

Each section of the diff output begins with a code that indicates what kinds of
dif the following lines refer to. In the previous example, the 4c4. This code tells you that there is a change (c) between line 4
in the first file and line 4 in the second file. Lines containing text only in the first
file begin with < . Lines containing text found only in the second file begin with >. The
dashed line separates parts of the output that refer to different sections of the file.
The normal output contains lines of these forms: