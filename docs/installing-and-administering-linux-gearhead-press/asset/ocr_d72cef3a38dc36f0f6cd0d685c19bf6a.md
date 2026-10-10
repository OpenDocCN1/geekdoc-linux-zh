Create a zero-length file named *letter1* in the *level1* subdirectory:

```
$ touch level1/letter1<Enter>
```

Change to the *level1* subdirectory:

```
$ cd level1<Enter>
```

Make a subdirectory under *level1* called *level2*:

```
$ mkdir level2<Enter>
```

Create a zero-length file named *letter2* in the *level2* subdirectory:

```
$ touch level2/letter2<Enter>
```

Change to your home directory:

```
$ cd<Enter>
```

From your home directory, issue the command to list all files starting with the letter 1. Record the names displayed:

```
$ ls 1*<Enter>
```

From your home directory, issue the command to find only files starting with the letter 1 :

```
$ find . -name '1\*' -type f<Enter>
```

Finally, record the names displayed.