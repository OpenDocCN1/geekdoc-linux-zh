https://www.hackers-arise.com/recovery-of-deleted-files), In some cases, even

after being overwritten, they can be recovered by a skilled forensic investigator.

The shred command overwrites the target files with random data multiple times, making it nearly impossible to recover their contents of the command history.

Let’s look at the help screen for shred.

252 | P a g e

```
```bash
root@kali-2019:~# shred --help
Usage: shred [OPTION]... FILE...
Overwrite the specified FILE(s) repeatedly, in order to make it harder
for even very expensive hardware probing to recover the data.

If FILE is -, shred standard output.

Mandatory arguments to long options are mandatory for short options too.
  -f, --force    change permissions to allow writing if necessary
  -n, --iterations=N  overwrite N times instead of the default (3)
  -random-source=FILE  get random bytes from FILE
  -s, --size=N   shred this many bytes (suffixes like K, M, G accepted)
  -u    deallocate and remove file after overwriting
  --remove[=HOW]  like -u but give control on HOW to delete; See below
  -v, --verbose  show progress
  -x, --exact   do not round file sizes up to the next full block;
                this is the default for non-regular files
  -z, --zero    add a final overwrite with zeros to hide shredding
  --help display this help and exit
      --version  output version information and exit
```
```