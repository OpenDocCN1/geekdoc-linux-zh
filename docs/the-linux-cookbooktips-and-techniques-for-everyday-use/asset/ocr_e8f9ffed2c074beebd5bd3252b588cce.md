# 6.1.1 Making an Empty File

You may sometimes want to create a new, empty file as a kind of "placeholder." To do so, give the name that you want to use for the file as an argument to touch.

+   - To create the file `a_fresh_start` in the current directory, type:

```
$ touch a_fresh_start RET
```

+   - To create the file `another_empty_file` in the `work/completed` subdirectory of the current directory, type:

```
$ touch work/completed/another_empty_file RET
```

This tool "touches" the files you give as arguments. If a file does not exist, it creates it; if the file already exists, it changes the modification timestamp on the file to the current date and time, just as if you had used the file.

> NOTE: Often, you make a file when you edit it, such as when in a text or image or sound editor; in that case, you don't need to make the file first.

# 6.1.2 Making a Directory

Use mkdir ("make directory") to make a new directory, giving the path name of the new directory as an argument. Directory names follow the same conventions as used with other files—that is, no spaces, slashes, or other unusual characters are recommended.

+   - To make a new directory called `work` in the current working directory, type:

```
$ mkdir work RET
```

+   - To make a new directory called `work` in the `/tmp` directory, type:

```
$ mkdir /tmp/work RET
```