# uncompress:

Click here to view code image

```
$ uncompress backup.tar.Z
$ ls -l backup.tar
-rw-r--r-- 1 taylor wheel 15800320 Feb  8 02:58 backup.tar
```

3. It turns out that there’s a useful flag to compress that lets you see how much it’s compressed things:

```
$ compress -v backup.tar
backup.tar: 49.4% OK
```

A quick turn with a calculator will confirm that it’s just about 50% smaller in size. Before finishing up, I want to uncompress it again:

Click here to view code image

```
$ uncompress -v backup.tar.Z
backup.tar.Z: 202.3% OK
```

4. For comparison, let’s have a quick look at the zip command, which offers very similar capabilities:

Click here to view code image

```
$ ls -l backup.tar
-rw-r--r-- 1 taylor wheel 15800320 Feb  8 02:58 backup.tar
$ zip backup.tar.zip backup.tar
  adding: backup.tar (deflated 67%)
$ ls -l backup.tar.Z
ls: backup.tar.Z: No such file or directory
```

Whoops! I’m running on autopilot. In fact, when zip is invoked, it has two required parameters: the archive name and the name of the file or folder to place in the archive. So not .Z but .zip:

Click here to view code image

```
$ ls -l backup.tar.zip
-rw-r--r-- 1 taylor wheel 5214105 Feb  8 02:58 backup.tar.zip
$
```

You can see that it did a better job of compressing this particular file than compress did: It’s only 5.5MB, instead of 7.8MB. Different files will have different compress/zip results, and some rare files won’t be any smaller when compressed, for reasons known only to the folk who invented the compression algorithms.

5. To uncompress (expand) the file, use unzip, as shown earlier:

Click here to view code image

```
$ unzip backup.tar.zip
Archive: backup.tar.zip
replace backup.tar? [y]es, [n]o, [A]ll, [N]one, [r]ename: y
  inflating: backup.tar
$
```

All back to normal!