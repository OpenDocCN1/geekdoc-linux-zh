In the original distributions of UNIX, the tool to compress files was appropriately called **compress**. Unfortunately, the algorithm was patented by someone hoping to make a great deal of money. Instead of paying out, most sites sought and found another compression tool with a patent-free algorithm: **gzip**. Even better, **gzip** consistently achieves better compression ratios than **compress** does. Another bonus: Recent changes have allowed **gzip** to uncompress files that were compressed using the **compress** command.

![](bbox=[0.13, 0.27, 0.3, 0.32])

The filename extension usually identifies a file compressed with **gzip**. These files typically end in .gz (files compressed with **compress** end in .Z).

Optional parameters used most often with **gzip** are as follows; see the man page for a complete list:

| Option for gzip | Description |
| --- | --- |
| -c | Write compressed file to the *stdout* (thereby allowing the output to be piped to another program) |
| -d | Decompress |
| -r | Recursively find all files that should be compressed |
| -9 | Best compression |
| -1 | Fastest compression |

Note that **gzip** compresses the file in place, meaning that after the compression process, the original file is removed, and the only thing left is the compressed file.

![](bbox=[0.13, 0.68, 0.3, 0.73])

While the **bzip2** command produces better compression than **gzip**, it is still used less often, not only because people are more familiar with **gzip**, but also because its compression algorithm is more complex and thus slower for compressing and uncompressed files.

To compress a file and then decompress it, use this command:

```
`[michael@workbox michael]$ gzip myfile` 
`[michael@workbox michael]$ gzip -d myfile.gz`
```