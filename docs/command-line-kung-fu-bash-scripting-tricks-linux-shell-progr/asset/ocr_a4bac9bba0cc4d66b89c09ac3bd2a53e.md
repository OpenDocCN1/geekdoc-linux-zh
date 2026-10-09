```
$ df | head -1
Filesystem 1K-blocks Used Available Use% Mounted on
$ for x in $(df)
> do
> echo $x
> done
Filesystem
1K-blocks
Used
Available
Use%
Mounted
on
...
```

We need to read in entire lines at a time like this.

```
$ df | while read LINE
> do
> echo $LINE
> done
Filesystem 1K-blocks Used Available Use% Mounted on
...
```

Here is one way to find file systems that are over 90% utilized.