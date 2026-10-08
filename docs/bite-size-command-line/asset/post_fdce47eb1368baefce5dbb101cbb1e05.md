
# # Bite Size Command Line

By Julia Evans

This zine explains some of the most useful Unix command line tools in 1 page each.

![](img/5f5d02ddabdd2009c88fde2963d57414_1_0.png)

![](img/5f5d02ddabdd2009c88fde2963d57414_1_1.png)

Even if you've used the command before, I might have a new trick or two for you ❤

# Table of contents

BSD≠GNU.........4 bash tricks.....10-11 misc commands...17
grep................5 disk usage......12 head&tail........18
find................6 tar................13 less................19
xargs................7 ps................14 kill................20
awk................8 top................15 cat................21
sed................9 sort&uniq......16 lsof................22

For almost all these tools, there are at least 2 versions:

- 1. The BSD version (on BSDs & Mac OS)
- 2. The GNU version (on Linux)

All of the examples in this zine were tested on Linux. Some things (like sed -i) are different on Mac. Be careful when writing cross-platform scripts!

You can install the GNU versions on Mac with `brew install coreutils`.

# # grep

grep lets you search files for text

use if you want regexps like ".*" work. otherwise you need to use ".\t" recursive! Search all the files in directory.

$ grep bananas foo.txt

Here are some of my favourite grep command line arguments!

- -v invert match: find all lines that don't match
- -o only print the matching part of the line (not the whole line)
- -i case insensitive
- -l only show the filenames of the files that matched
search binaries: treat binary data like it's text instead of ignoring it!
- -A 3 Show context for your search. $ grep -A 3 foo will show 3 lines of context after a match
- -F don't treat the match string as a regex eg $ grep -F ...

grep alternatives: ack, aggrep (better for searching code!)

# # find

find searches a directory for files

- -name [/iname] case insensitive the filename! eg -name '*.txt'
- -type [TYPE]
  f: regular file
  l: symlink
  d: directory
  + more!

find /tmp -type d -print directory which files action to do to search with the files
here are my favourite find arguments!

- -path [/ipath] search the full path ! -path '/home/*.go'
- -maxdepth NUM only descend NUM levels when searching a directory
- -size 0 find empty files! Useful to find files you created by accident
- -print0 print null-separated names Use with xargs -O!

locate:
The locate command searches a database of efile on your system.
good: faster than find
bad: cannot get out of date
$ sudo updatedb updates the database

- -exec COMMAND action: run COMMAND on every file found
- -delete action: delete all files found

# xargs

xargs takes white space separated strings from stdin and converts them into command-line arguments

```
$ echo "/home/tmp" | xargs ls
will run ls /home/tmp
```

this is useful when you want to run the same command on a list of files!

- - delete (xargs rm)
- - combine (xargs cat)
- - search (xargs grep)
- - replace (xargs sed)

how to replace "foo" with "bar" in all .txt files:

```
find . -name '*.txt' | xargs sed -i s/foo/bar/g
```

how to lint every Python file in your Git repo:

```
git ls-files | grep .py | xargs pep8
```

if there are spaces in your filenames "my day.txt" xargs will think it's 2 files "my" and "day.txt", fix it like this:

```
find . -print0 | xargs -O COMMAND
```

more useful xargs options makes xargs run a separate process max-args for each input:

```
- -P max-procs is the max number of parallel processes xargs will start
```

# awk

awk is a tiny programming language for manipulating columns of data

basic awk program structure: extract a column of text with awk

I only know how to do 2 things with awk but it's still useful!

```
BEGIN {...}
CONDITION {action}
CONDITION {action}
END {...}
```

```
awk -F, '{print $5}'
```

column single separator quotes? 5th column

this is 99% of what I do with awk

action on lines matching CONDITION

SO MANY unix commands print columns of text (ps! Is!!)

awk program example: sum the numbers in the 3rd column

awk program example: print every line over 80 characters

so being able to get the column you want with awk is GREAT

```
{ s += $3 }; n
END {print s}
```

```
length($0) > 80
```

action at the end, print the sum!
condition (there's an implicit {print} as the action)

# # sed

sed is most often used for replacing text in a file

$ sed s/cat/dog/g file.txt
be a regular expression

change a file in place with -i

some more sed incantations...

sed -n 12 p
print 12th line

in GNU sed it's -i
in BSD sed, -i SUFFIX
confuses me every time

- -i suppresses output so only what you print with 'p' gets printed

sed 5d
delete 5th line

sed s+/cat+/dog/+
use as a character regex delimiter

sed 6
double space a file (good for long error lines)

sed /cat/d
delete lines matching /cat/

way easier than escaping / is like s/cat//dog//

sed '/cat/a dog'
append 'dog' after lines containing 'cat'

sed -n 5,30 p
print lines 5-30

sed -n s/cat/dog/p
only print changed lines

sed 'i17 panda'
insert 'panda' on line 17

# bash tricks

* ctrl + r *

search your history!

★ magical braces★
$ convert file.{jpg,png}
expands to

!!
ands to the last
command run
$ sudo !!

I use this ♥ constantly ♥
to rerun commands

$ convert file.jpg file.png
{1..5} expands to 1 2 3 4 5
(for i in {1..100}...)

commands that start
with a space don't go
in your history. good if
there's a 🔒 password 🔒

loops
for i in *.png
do
convert $i $i.jpg
done

$() 
gives the output of a
command

$ touch file-$(date -I)
↑
create a file named
file-2018-05-25

more keyboard shortcuts
ctrl a beginning of line
ctrl e end of line
ctrl+l clear the screen

+ lots more emacs
shortcuts too!

![](img/5f5d02ddabdd2009c88fde2963d57414_9.png)

# bash tricks:

cd -
changes to the directory you were in

ctrl+z
suspends (program)

bg
starts background

fg
brings backgrounded program to the foreground

pushd popd you keep a stack

type
tells if something is a alias, function, or builtin

type
tells if something is a alias, function, or builtin (try running :)

# disk usage

du
tells you how much
space directories take up

* df.
tells you how much free
partition has. -h human readable
sizes

summary: total
size of all files

| Filesystem | Size | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- |
| /dev/sda3 | 18G | 2.5G | 86% | / |
| udev | 483M | 4.0K | 483M | 1% | /dev |
| tmpfs | 99M | 1.4M | 97M | 2% | /run |
| /dev/sda4 | 167G | 157G | 9.9G | 95% | /home |

df -i
instead of % disk free,
report how many inodes
are used/ free on
partition

ncdu
see what's using disk space
navigate with arrow keys

iostat
get statistics about
disk reads / writes
interval to report

+   iostat 5
Device: kB_read/s kB_wrt/s
sda 2190.21 652.87
sdb 6.00 0.00

running out of
inodes is VERY
ANNOY - you can't
create new files!

# tar

The .tar file format combines many files into one file.

a.txt dir/c.txt

.tar files aren't compressed by themselves. Usually you gzip them: .tar.gz or .tgz!

Usually when you use the 'tar' command, you'll run some incantation
To unpack a tar.gz, use:

+   - tar -xzf file.gz

[Drawing of characters asking about xzf? saying learn]

-x is for extract into the current directory by default (change with -C)

-c is for create
makes a new tar file!

-t is for list
lists the contents of a archive

tar can compress / decompress
-Z gzip format (.gz)
-j bzip2 format (.bz2)
-J xz format (.xz)
& more! see the man page :)

putting it together
list contents of a .tar.bz2:
$tar -tjvf file.tar.bz2 verbose
create a .tar.gz
$tar -czf file.tar.gz dir/files to go in the archive

-f is for file
Which tar file to create or unpack
