# cat & friends

cat concatenates files

```
$ cat myfile.txt
prints contents of myfile.txt
```

```
$ cat *.txt
prints all .txt files put together!
```

you can use cat as an EXTREELY BASIC text editor:

+   - Run $ cat > file.txt
- type the contents (don't make mistakes)
- press ctrl+d to finish

```
cat -n
```

prints out the file with line numbers!

+   1. Once upon a midnight...
2. Over many a quaint.
3. While I nodded, nearly

# zcat

cats a gzipped file!
Actually just a 1-line shell script that runs 'zip -cd', but easier to remember.

# tee

'tee file.txt' will write its stdin to both stdout and file.txt

```
stdin -> tee a.txt -> stdout
a.txt
```

how to redirect to a file owned by root

```
$ sudo echo "hi" >> x.txt
```

this will open x.txt as your user, not as root, so it fails!
$ echo "hi" | sudo tee -a x.txt will open x.txt as root :)