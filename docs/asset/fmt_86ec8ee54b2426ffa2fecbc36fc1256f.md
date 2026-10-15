
## 23.6.3.3 `dump` and `restore` (PC-BSD)

The `dump` and `restore` facilities are a simple set of complementary commands that have a small number of options, and are primarily used to back up the system. What differentiates `dump` and `restore` from facilities like `cpio` and `tar` is that `dump` writes a table of contents at the beginning of each volume so that you can selectively `restore` files from the archive. For the creation of a backup, the `dump` command's basic syntax is as follows:

```
dump options file blocking-factor density size device filesystem
```

where `0`, `1`, `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `a`, `c`, `L`, `n`, `r`, `R`, `S`, and `u` are various options, `file`, `blocking-factor`, `density`, and `size` are option arguments that must be supplied in the same order as their respective options given on the command line, and `device` and `filesystem` are the command arguments.

The `restore` command's basic syntax is as follows.

```
restore options blocking-factor file-number device
```

for restoration of a backup, where `options` are various options, `blocking-factor` and `file-number` are option arguments that must be supplied in the same order as their respective options given on the command line, and `device` is the command argument.

An example of how to use `dump` to create a full backup of `/home` to a tape drive named `/dev/rmt/t0` is

```
dump 1unbdsf 512 100000 10000 /dev/rmt/t0 /home
```

An example of how to use `restore` to `restore` the files in `/home/bob` from a tape mounted in `/dev/rmt/t0`, with a blocking factor of 512, to a subdirectory under the current directory is

```
restore xvfby 512 /dev/rmt/t0 ./home/bob
```

## 23.6.3.4 `dd`

The `dd` facility is used to copy a single file, part of a file, a partition, or part of a partition and can treat the data stream using, for example, compression or format conversion.

The basic syntax of `dd` is

```
dd if=device of=device bs=blocksize
```

where `if` is the input file pathname, `of` is the output file pathname, and `bs` specifies the block size.

An example of using `dd` in conjunction with `ssh` and `tar` is as follows.

```
$ ssh bob@192.168.0.13:/home/bob "dd if=backup.tar ibs=512" | tar -xvBf -
```

This command extracts the remote file `backup.tar` file at `/home/bob` in 512 byte blocks and streams it through `dd` to the system you typed this command on.

## 23.6.3.5 `ufsdump` and `ufsrestore` (Solaris)

`ufsdump` is an incremental file system dump facility for Solaris, similar to the `dump` command in PC-BSD. Its purpose is to back up all files specified (usually either a whole file system or files within a file system changed after a certain date) to magnetic tape or a disk file. The `ufsdump` command can only be used on unmounted file systems, or those mounted as read only. Attempting to `dump` a mounted, read–write file system might result in a system disruption or the inability to `restore` files from the `dump`. It is used in conjunction with `ufsrestore`.

partition of `c0t3d0`, on a 1/2 inch reel tape unit 1:

```
# ufsdump 5fuv /dev/rmt/1 /dev/rdsk/c0t3d0s6
```
