You can verify at the terminal that the working directory has been changed by using the pwd command:

```
```text
$ pwd
/users/steve/documents
$
```
```

The easiest way to move up one level in a directory is to reference the .. shortcut with the command

```
```shell
cd ..
```
```

because by convention .. always refers to the directory one level up (see Figure 1.6).

```
```text
$ cd ..
$ pwd
/users/steve
$
```
```

![](bbox=[0.133, 0.4, 0.67, 0.632])

Figure 1.6  `cd ..`

If you wanted to change to the letters directory, you could get there with a single cd command by specifying the relative path documents/letters (see Figure 1.7):

```
```text
$ cd documents/letters
$ pwd
/users/steve/documents/letters
$
```
```