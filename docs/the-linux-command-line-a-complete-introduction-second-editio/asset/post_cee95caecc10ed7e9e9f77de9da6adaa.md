
the same as passing a single filename argument. This is not particularly useful compared to passing a filename argument, but it serves to demonstrate using a file as a source of standard input. Other commands make better use of standard input, as we will soon see.

Before we move on, check out the man page for cat because it has several interesting options.

## Pipelines

The capability of commands to read data from standard input and send to standard output is utilized by a shell feature called pipelines. Using the pipe operator |, the standard output of one command can be piped into the standard input of another.

```
command1 | command2
```

To fully demonstrate this, we are going to need some commands. Remember how we said there was one we already knew that accepts standard input? It's less. We can use less to display, page by page, the output of any command that sends its results to standard output.

```
[me@linuxbox ~]$ ls -l /usr/bin | less
```

This is extremely handy! Using this technique, we can conveniently examine the output of any command that produces standard output.

## Filters

Pipelines are often used to perform complex operations on data. It is possible to put several commands together into a pipeline. Frequently, the commands used this way are referred to as filters. Filters take input, change it somehow, and then output it. The first one we will try is sort. Imagine we wanted to make a combined list of all the executable programs in /bin and /usr/bin, put them in sorted order, and view the resulting list.

```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | less
```

Because we specified two directories (*/bin* and */usr/bin*), the output of `ls` would have consisted of two sorted lists, one for each directory. By including `sort` in our pipeline, we changed the data to produce a single, sorted list.

## THE DIFFERENCE BETWEEN > AND |

At first glance, it may be hard to understand the redirection performed by the pipeline operator `|` versus the redirection operator `>`. Simply put, the redirection operator connects a command with a file, while the pipeline operator connects the output of one command with the input of a second command.

```
command1 > file1
command1 | command2
```

A lot of people will try the following when they are learning about pipelines, “just to see what happens”:

```
command1 > command2
```

Answer: sometimes something really bad.

Here is an actual example submitted by a reader who was administering a Linux-based server appliance. As the superuser, he did this:

```
# cd /usr/bin
# ls > less
```

The first command put him in the directory where most programs are stored, and the second command told the shell to overwrite the file *less* with the output of the `ls` command. Since the */usr/bin* directory already contained a file named *less* (the less program), the second command overwrote the *less* program file with the text from `ls`, thus destroying the less program on his system.

## grep: Print Lines Matching a Pattern

grep is a powerful program used to find text patterns within files. It’s used like this:

```
grep pattern filename
```

When grep encounters a “pattern” in the file, it prints out the lines containing it. The patterns that grep can match can be very complex, but for now we will concentrate on simple text matches. We’ll cover the advanced patterns, called regular expressions, in Chapter 19.

Suppose we wanted to find all the files in our list of programs that had the word zip embedded in the name. Such a search might give us an idea of some of the programs on our system that had something to do with file compression. We would do this:

```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq | grep zip
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
```

There are a couple of handy options for grep.

- -i, which causes grep to ignore case when performing the search (normally searches are case sensitive)
- -v, which tells grep to print only those lines that do not match the pattern

## head/tail: Print First/Last Part of Files
