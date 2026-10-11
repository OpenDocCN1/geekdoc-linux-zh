# COMPRESSION

compression and results in a lower compression ratio. Alternatively, the `-9` option is known as best compression and results in the highest compression ratio at the expense of time. If no level of compression is specified, the `gzip` command assumes the number 6.

The following command compresses the samplefile file shown earlier using fast compression and displays the compression ratio:

```
```
[root@server1 root]# gzip -v -1 samplefile
samplefile:  51.3% -- replaced with samplefile.gz
[root@server1 root]# 
```
```

Notice from the preceding output that samplefile was compressed with a compression ratio of 51.3%, which is much lower than the compression ratio of 36.8% obtained earlier when samplefile was compressed with the default level of 6.

> > **NOTE**
> > You need not specify the level of compression when decompressing files, as it is built in to the compressed file itself.

Many more options are available to the `gzip` utility than to the `compress` utility, and many of these options have a POSIX option equivalent. Table 12-2 shows a list of these options.

| Table 12-2 Common options used with the **gzip** utility |
|---|---|
|**Option**|**Description**| 
| `-#` | Specifies how thorough the compression will be, where `#` can be the number 1–9. The option `-1` represents fast compression, which takes less time to compress but results in a lower compression ratio. The option `-9` represents thorough compression, which takes more time but results in a higher compression ratio. |
| `--best` | Results in a higher compression ratio; same as the `-9` option. |
| `-c`<br/>`--stdout`<br/>`--to-stdout` | Displays the contents of the compress file to Standard Output (same function as the `zcat` command) when used with the `gunzip` command. |
| `-d`<br/>`--decompress`<br/>`--uncompress` | Decompresses the files specified (same as the `gunzip` command) when used with the `gzip` command. |
| `-f`<br/>`--force` | Compresses symbolic links when used with the `gzip` command. When used with the `gunzip` command, it overwrites any existing files without prompting the user. |
| | |