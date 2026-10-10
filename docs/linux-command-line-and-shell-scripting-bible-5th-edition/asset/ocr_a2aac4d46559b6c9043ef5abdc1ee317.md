# Chapter 3: Basic Bash Shell Commands



```
```
$ ls -l my*
-rw-rw-r-- .1 christine christine 0 Feb 29 16:12 my_file
-rw-rw-r-- .1 christine christine 0 Feb 29 16:12 my_scrapt
-rwxrw-r-- .1 christine christine 74 Feb 29 16:12 my_script
$ 
```
```

Using the asterisk finds three different files, starting with the name my. As with the question mark, you can place the asterisks anywhere in the filter:

```
```
$ ls -l my*?pt
-rw-rw-r-- .1 christine christine 0 Feb 29 16:12 my_scrapt
-rwxrw-r-- .1 christine christine 74 Feb 29 16:12 my_script
$ 
```
```

Using the asterisk and question mark in the filter is called *file globbing*. File globbing is the processing of pattern matching using wildcards. The wildcards are officially called *metacharacter wildcards*. You can use more metacharacter wildcards for file globbing than just the asterisk and question mark. You can also use brackets:

```
```
$ touch my_scr[y]pt
$ ls -l my_scr[ay]pt
-rw-rw-r-- .1 christine christine 0 Feb 29 16:12 my_scrapt
-rw-rw-r-- .1 christine christine 0 Feb 29 16:18 my_scr[y]pt
$ 
```
```

This example used the brackets along with two potential choices for a single character in that position, a or y. The brackets represent a single character position and give you multiple options for file globbing. You can list choices of characters, as shown in the preceding example, and you can specify a range of characters, such as an alphabetic range [a-i]:

```
```
$ ls f*ill
fall fill filli full
$ ls f[a-i]ill
fall fill filli
$ 
```
```

Also, you can specify what should *not* be included in the pattern match by using the exclamation point (!):

```
```
$ ls -l f[!a]ll
-rw-rw-r-- .1 christine christine 0 Feb 29 16:12 fill
-rw-rw-r-- .1 christine christine 0 Feb 29 16:12 filli
-rw-rw-r-- .1 christine christine 0 Feb 29 16:12 full
$ 
```
```

File globbing is a powerful feature when searching for files. It can also be used with other shell commands besides ls. You'll find out more about this later in the chapter.