# gzip, gunzip, gcat

# Advanced Usage

Multiple compressed files can be concatenated. In this case, gunzip extracts all members at once. For example:

```
gzip -c file1 > foo.gz
gzip -c file2 >> foo.gz
```

Then

```
gzip -c foo
```

is equivalent to

```
cat file2
```

When one member of a .gz file is damaged, you can still recover other members if you remove the damaged member. However, you can get better compression by compressing all members at once, as shown in the following example.

```
cat file12 | gzip > foo.gz
```

compresses better than

```
gzip -c file12 > foo.gz
```

To recompress files for better compression, use the following syntax:

```
gzip -cd old.gz | gzip > new.gz
```

When a compressed file consists of several members, the uncompressed size and CRC reported by the --list option applies only to the last member. If you need the uncompressed size for all members, you can use the following command:

```
gzip -cd file.gz | wc -c
```

To create a single archive file with multiple members so that members can later be extracted independently, an archiver such as tar or zip. GNU tar supports the -z option to invoke gzip transparently. gzip is designed to compress a tar, not as a replacement.

# Environment

Environment variable GZIP can hold a set of default options for gzip. These options are interpreted first and can be overwritten by explicit command-line parameters, as shown in the following examples.

+   For sh GZIP=-8 --name; export GZIP
For csh setenv GZIP "-8v --name"
For MS-DOS set GZIP=-8 --name

On VAX/VMS, the name of the environment variable is GZIP_OPT to avoid a conflict with the symbol set for invocation of the program.