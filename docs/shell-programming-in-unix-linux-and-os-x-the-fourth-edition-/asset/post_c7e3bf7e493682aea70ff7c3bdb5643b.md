
To sort the file instead by the third colon-delimited field (which contains what is known as your *user ID*), you would want an arithmetic sort, starting with the third field (`-k3`), and specifying the colon character as the field delimiter (`-t:`):

```text
$ sort -k3n -t: /etc/passwd                 Sort by userid
root:*:0:0:The super User:/usr/bin/ksh
cron:*:1:1:Cron Daemon for periodic tasks:/
bin:*:3:3:The owner of system files:/
uucp:*:5:5:/usr/spool/uucppublic:/usr/lib/uucp/uucico
asg:*:6:6:The Owner of Assigned Devices:/
sys:*:7:7:I/O Access to System Information:/usr/bin/sh
george:*:75:75:/users/george:/usr/lib/rsh
steve:*:203:100:/users/steve:/bin/ksh
pat:*:300:300:/users/pat:/usr/bin/ksh
mail:*:301:31:/usr/mail:
$
```

Here we’ve bolded the third field of each line so that you can easily verify that the file was sorted correctly by user *ID*.

### Other Options

Other options to sort enable you to skip characters within a field, specify the field to end the sort on, merge sorted input files, and sort in “dictionary order” (only letters, numbers, and spaces are used for the comparison). For more details on these options, look under sort in your *Unix User’s Manual*.

### uniq

The uniq command is useful when you need to find or remove duplicate lines in a file. The basic format of the command is

```text
uniq in_file out_file
```

In this format, uniq copies *in_file* to *out_file*, removing any duplicate lines in the process. uniq’s definition of duplicated lines is *consecutive lines that match exactly*.

If *out_file* is not specified, the results will be written to standard output. If *in_file* is also not specified, uniq acts as a filter and reads its input from standard input.

Here are some examples to see how uniq works. Suppose that you have a file called names with contents as shown:

```text
$ cat names
Charlie
Tony
Emanuel
Lucy
Ralph
Fred
Tony
$
```

You can see that the name Tony appears twice in the file. You can use `uniq` to remove such duplicate entries:

```text
$ uniq names                 Print unique lines
Charlie
Tony
Emanuel
Lucy
Ralph
Fred
Tony
$
```

Oops! Tony still appears twice in the preceding output because the multiple occurrences are not *consecutive* in the file, and thus `uniq`’s definition of duplicate is not satisfied. To remedy this situation, sort is often used to get the duplicate lines adjacent to each other, as mentioned earlier in the chapter. The result of the sort is then run through `uniq`:

```text
$ sort names | uniq
Charlie
Emanuel
Fred
Lucy
Ralph
Tony
$
```

The sort moves the two Tony lines together, and then `uniq` filters out the duplicate line (but recall that sort with the `-u` option performs precisely this function).

### The -d Option

Frequently, you’ll be interested in finding just the duplicate entries in a file. The `-d` option to `uniq` can be used for such purposes: It tells `uniq` to write *only* the duplicated lines to *out_file* (or standard output). Such lines are written just once, no matter how many consecutive occurrences there are.

```text
$ sort names | uniq -d       List duplicate lines
Tony
$
```

As a more practical example, let’s return to our `/etc/passwd` file. This file contains information about each user on the system. It’s conceivable that over the course of adding and removing users from this file that perhaps the same username has been inadvertently entered more than once. You can easily find such duplicate entries by first sorting `/etc/passwd` and piping the results into `uniq -d` as done previously:

```text
$ sort /etc/passwd | uniq -d
$
```

There are no duplicate full line `/etc/passwd` entries. But you really want to find duplicate entries for the username field, so you only want to look at the first field from each line (recall that the leading characters of each line of `/etc/passwd` up to the colon are the username). This can’t be done directly through an option to `uniq`, but can be accomplished by using `cut` to extract the username from each line of the password file before sending it to `uniq`.

```text
$ sort /etc/passwd | cut -f1 -d: | uniq -d
cem
harry
$
```

It turns out that there are multiple entries in `/etc/passwd` for cem and harry. If you wanted more information on the particular entries, you could now grep them from `/etc/passwd`:

```text
$ grep -n 'cem' /etc/passwd
20:cem:*:91:91::/users/cem:
166:cem:*:91:91::/users/cem:
$ grep -n 'harry' /etc/passwd
29:harry:*:103:103:Harry Johnson:/users/harry:
79:harry:*:90:90:Harry Johnson:/users/harry:
$
```

The `-n` option was used to find out where the duplicate entries occur. In the case of cem, there are two entries on lines 20 and 166; in harry’s case, the two entries are on lines 29 and 79.

### Other Options

The `-c` option to `uniq` adds an occurrence count, which can be tremendously useful in scripts:

```text
$ sort names | uniq -c
    1 Charlie
    1 Emanuel
    1 Fred
    1 Lucy
    1 Ralph
    2 Tony
$
```

One common use of `uniq -c` is to figure out the most common words in a data file, easily done with a command like:

```text
tr '[A-Z]' '[a-z]' datafile | sort | uniq -c | head
```

Two other options that we don’t have space to describe more fully let you tell `uniq` to ignore leading characters/fields on a line. For more information, consult the man page for your particular implementation of `uniq` with the command `man uniq`.

We would be remiss if we neglected to mention the programs `awk` and `perl`, which can be useful when writing shell programs too. They are both big, complicated programming environments unto themselves, however, so we’re going to encourage you to check out *Awk—A Pattern Scanning and Processing Language*, by Aho, et al., in the *Unix Programmer’s Manual, Volume II* for a description of `awk`, and *Learning Perl* and *Programming Perl*, both from O’Reilly and Associates, offering a good tutorial and reference on the language, respectively.

## And Away We Go

Based on our discussions in Chapter 2, “What Is the Shell?”, you should now realize that whenever you type something like

```text
who | wc -l
```

you are actually programming in the shell. That’s because the shell is interpreting the command line, recognizing the pipe symbol, connecting the output of the first command to the input of the second, and initiating execution of both commands.

In this chapter, you’ll learn how to write your own commands and how to use shell variables.

### Command Files

A shell program can be typed directly, as in

```text
$ who | wc -l
```

or it can be typed into a file and then the file can be executed by the shell. For example, suppose that you need to find out the number of logged-in users several times throughout the day. It’s not unreasonable to type in the preceding pipeline each time you want the information, but for the sake of example, let’s type this pipeline into a file.

We’ll call the file nu (for number of users), and its contents will be just the pipeline shown previously:

```text
$ cat nu
who | wc -l
$
```

To execute the commands contained inside the file nu, all you now have to do is type nu as the command name to the shell:

```text
$ nu
sh: nu: cannot execute
$
```

Oops! We forgot to mention one thing. Before you can execute a script from the command line, you must change the file’s permission to make it executable. This is done with the change mode command, chmod. To add execute permission to the file, you simply type

```text
chmod +x *file(s)*
```

The +x indicates that you want to make the *file(s)* that follow executable. The shell requires that a file be *both* readable and executable by you before you can invoke it directly on the command line.

```text
$ ls -l nu
-rw-rw-r--  1 steve  steve  12 Jul 10 11:42 nu
$ chmod +x nu                         *Make it executable*
$ ls -l nu
-rwxrwxr-x  1 steve  steve  12 Jul 10 11:42 nu
$
```

Now that you’ve made it executable, try it again:

```text
$ nu
      8
$
```

This time it worked.

> **Warning**
>
> If you fix the permission issue and still get an error “Command not found,” try adding `./` before the command, like `./nu` to ensure the shell looks in the current directory for commands as well as the usual system locations. To fix it long term, add `.` to the end of your `PATH` (typically within your `.profile` file).

You can put any commands inside a file, make the file executable, and then execute its contents simply by typing its name to the shell. It’s that simple and that powerful, and everything you’ve learned about working on the command line therefore also applies to writing shell scripts too.

The standard shell mechanisms such as I/O redirection and pipes can be used on your own programs as well:

```text
$ nu > tally
$ cat tally
      8
$
```

Suppose that you’re working on a proposal called *sys.caps* and the following command sequence is needed every time you print the proposal:

```text
tbl sys.caps | nroff -mm -Tlp | lp
```
