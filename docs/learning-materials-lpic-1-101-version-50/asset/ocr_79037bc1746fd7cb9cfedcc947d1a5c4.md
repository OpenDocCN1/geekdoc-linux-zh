The following scenario would help you better understand recursion:

You list the contents of a directory *students*, which contains two subdirectories *level 1* and *level 2* and the file named *frank*. By applying recursion, the `ls` command would list the content of *students* i.e. *level 1*, *level 2* and *frank*, but would not end there. It would equally enter subdirectories *level 1* and *level 2* and list their contents and so on down the directory tree.

# ### Recursive Listing with `ls -R`

`ls -R` is used to list the contents of a directory together with its subdirectories and files.

```
```bash
$ ls -R mydirectory
mydirectory/:
file1	newdirectory

mydirectory/newdirectory:
```
```

In the listing above, *mydirectory* including all its content are listed. You can observe *mydirectory* contains the subdirectory *newdirectory* and the file *file1*. *newdirectory* is empty that is why no content is shown.

In general, to list the contents of a directory including its subdirectories, use:

```
```bash
ls -R DIRECTORY_NAME
```
```

Adding a trailing slash to `DIRECTORY_NAME` has no effect:

```
```bash
$ ls -R animal
```
```

is similar to

```
```bash
$ ls -R animal/
```
```

# ### Recursive Copy with `cp -r`

`cp -r` (or -R or --recursive) allows you to copy a directory together with its all subdirectories and files.

```
```bash
$ tree mydir
```
```