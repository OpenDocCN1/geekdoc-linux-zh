# 2.6 Forgiveness Is Better than Permission

The command then pipes both standard output and standard error to the Mail command to mail the results to the system administrator's account. Becue find take many minutes to run on the entire file system, it is often preferable to mail the results to yourself and do something else while find runs.

When I go through such purification ritual, I will usually redirect the output into a file as foo or pipe the output to tee and specify the output file to tee. Everyone who knows this find is shocked at the results. Even though I run a tight ship, I was surprised by how many problems this found on my laptop. This was particularly surprising because it does not have many packages installed on it because it originally had a 300 MB disk.

After the find puts the suspicious file names in a file, I edit the file down to those files that actually have a problem, prepend

```
chmod o-w
```

to each line (with a space after the w) and then I do

```
sh foo
rm foo
```

or

```
csh foo
rm foo
```

This removes write permission for others from the files.

As an alternative, either of the two following commands will find all world-writable files (except directories with the sticky bit on and character devices) and for each one, will ask you if you want the world-writable bit (002) turned off.

Note that you do not check the /proc file system

Note that the -ok action is like -exec it first prompts you with the name of the command (the first argument to -ok) and the name of the file being processed and waits for you to type a line. If the line begins with y or r, the command is executed; otherwise it is not. Rereading the find(1) manual page might prove value. The first assumes that /home is a separate file system and will not check file systems other than /home. The second form is preferable for general use.

```
find / -home -mount -perm -002 \( -type f \
-o -type d -o -type p -o -type b \ \
\ ! -type d -o ! -perm -1000 \ \ \
-ls -ok chmod o-w '{}' \;
```

```
find / -fstype -perm -002 \( -type f \
-o -type d -o -type p -o -type b \ \
\ ! -type d -o ! -perm -1000 \ \
-ls -ok chmod o-w '{}' \;
```