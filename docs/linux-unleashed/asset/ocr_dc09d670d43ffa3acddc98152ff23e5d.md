```
drwxr-xr-x   6 root      root      1024 Dec 14 01:39 ./
-rw-r--r-   1 fido      users       163 Dec  7 14:31 .kermrc
drwxr-xr-x   2 fido      users      1024 Dec  7 13:36 .term/
-rw-r--r-   1 fido      users       3016 May 13  1994 .emacs
-rwxr-xr-x   1 fido      users       114 Nov 23  1993 .lessrc
-rw-r--r-   1 fido      users         34 Jun  6  1993 .less
```

The **r** option tells **ls** to produce a reverse output. This is often used with the **t** option.

The following is an example of what displays when you enter **ls -altr**:

```
darkstar:~$ **ls -altr**
total 10
-rw-r--r-   1 fido      users         34 Jun  6  1993 .less
-rw-r--r-   1 fido      users        114 Nov 23  1993 .lessrc
-rw-r--r-   1 fido      users        3016 May 13  1994 .emacs
drwxr-xr-x   2 fido      users        1024 Dec  7 13:36 .term/
-rw-r--r-   1 fido      users          163 Dec  7 14:31 .kermrc
drwxr-xr-x   6 root      root         1024 Dec 14 01:39 ./
-rw-r--r-   1 fido      users          333 Dec 21 22:11 .bash_history
drwxr-xr-x   3 fido      users        1024 Jan  2 13:48 /
```

Many other options can be used with **ls**, although you have just worked with the most commonly used ones. The important thing to remember is that you can usually customize a Linux command by using one or more command options.

> **NOTE**
With the basic Linux commands, case is important! For instance, **ls** has an **R** option (recursive: show files in subdirectories, too) which gives much different results from the **r** option.

> **TIP**
You can think of **a** as the “all files” option, **l** as the “long list” option, **t** as the “sort by time” option, **r** as the “reverse sort” option, and so on. In fact, most options in Linux are *mnemonic*—the option letter stands for a word or phrase. Some option letters mean the same thing in many different Linux commands. For instance, **v** often means *verbose*—in other words, “Give me lots of detail.”

However, do not assume that on an unfamiliar command certain options will work in the “usual” way! For instance, **r** is the recursive option for many Linux commands; however, in the case of **ls**, reverse sort is more commonly used, and therefore it gets the easier-to-type lowercase **r**, while recursive is left with the capital **R**. It might seem like not much extra effort to press the Shift key to get the capital letter, but try typing a string of four or five options, one of which is capitalized!