

-rw-rw-r--. 1 student 0 Feb 4 18:23 snap6.jpg

# 视频:

```
total 0
rw-rw-r--. 1 student 0 Feb 4 18:23 film1.avi
-rw-rw-r--. 1 student 0 Feb 4 18:23 film2.avi
-rw-rw-r--. 1 student 0 Feb 4 18:23 film3.avi
-rw-rw-r--. 1 student 0 Feb 4 18:23 film4.avi
-rw-rw-r--. 1 student 0 Feb 4 18:23 film5.avi
-rw-rw-r--. 1 student 0 Feb 4 18:23 film6.avi
```

- 5. 继续在用户主目录下操作，创建三个子目录将你的文件组织到不同的项目中。将子目录命名为 **friends**（朋友）、**family**（家庭）和 **work**（工作）。使用单个命令同时创建所有目录。

你将使用目录将你的文件重新组织到项目中。

```
[student@servera ~]$ mkdir friends family work
[student@servera ~]$ ls -l
total 0
-drwxr-xr-x. 2 student 6 Feb 4 18:34 family
-drwxr-xr-x. 2 student 6 Feb 4 18:38 friends
-drwxr-xr-x. 2 student 108 Feb 4 18:36 Music
-drwxr-xr-x. 2 student 108 Feb 4 18:36 Pictures
-drwxr-xr-x. 2 student 108 Feb 4 18:36 Videos
-drwxr-xr-x. 2 student 6 Feb 4 18:38 work
```

- 6. 将一组新文件复制到 **family** 和 **friends** 项目目录。根据需要使用多个命令。你不需要像示例那样只使用一个命令。对于每个项目，先切换到项目目录，然后将源文件复制到目录。请记住，你是在进行复制，在文件复制到项目目录后，原始文件将保留在原始位置。

- * 复制 **friends** 子目录中包含数字 1 和 2 的文件（所有类型）。
- * 将包含数字 3 和 4 的文件复制到 **family** 子目录。

当从多个位置将文件复制到单个位置时，Red Hat 建议在复制文件之前先进入目标目录。使用最简单的语法（绝对路径或相对路径）来访问每个文件任务源。

```
[student@servera]$ cd friends
[student@servera]$ cp ~/Music/song1.mp3 ~/Music/song2.mp3 \
> ~/Pictures/snap1.jpg ~/Pictures/snap2.jpg ~/Videos/film1.avi \
> ~/Videos/film2.avi
[student@servera]$ ls -l
total 0
-rw-rw-r--. 1 student 0 Feb 4 18:42 film1.avi
-rw-rw-r--. 1 student 0 Feb 4 18:42 film2.avi
-rw-rw-r--. 1 student 0 Feb 4 18:42 snap1.jpg
-rw-rw-r--. 1 student 0 Feb 4 18:42 snap2.jpg
-rw-rw-r--. 1 student 0 Feb 4 18:42 song1.mp3
-rw-rw-r--. 1 student 0 Feb 4 18:42 song2.mp3
[student@servera friends]$ cd ~/family
[student@servera family]$ cp ~/Music/song3.mp3 ~/Music/song4.mp3 ~
```

## 第 2 章 | 使用命令行管理文件

```
> ~/Pictures/snap3.jpg ~/Pictures/snap4.jpg \
> ~/Videos/film4.avi \
[student@servera]$ ls -l
total 0
-rw-r--r-- 1 student student 0 Feb 4 18:44 film3.avi
-rw-r--r-- 1 student student 0 Feb 4 18:44 film4.avi
-rw-r--r-- 1 student student 0 Feb 4 18:44 snap3.jpg
-rw-r--r-- 1 student student 0 Feb 4 18:44 snap4.jpg
-rw-r--r-- 1 student student 0 Feb 4 18:44 song3.mp3
-rw-r--r-- 1 student student 0 Feb 4 18:44 song4.mp3
```

对于你的项目工作，请创建额外的副本。

```
[student@servera]$ cd ../work
[student@servera]$ cp ~/Music/song5.mp3 ~/Music/song6.mp3 \
> ~/Pictures/snap5.jpg ~/Pictures/snap6.jpg \
> ~/Videos/film5.avi ~/Videos/film6.avi
[student@servera]$ ls -l
total 0
-rw-r--r-- 1 student student 0 Feb 4 18:44 film5.avi
-rw-r--r-- 1 student student 0 Feb 4 18:44 film6.avi
-rw-r--r-- 1 student student 0 Feb 4 18:44 snap5.jpg
-rw-r--r-- 1 student student 0 Feb 4 18:44 snap6.jpg
-rw-r--r-- 1 student student 0 Feb 4 18:44 song5.mp3
-rw-r--r-- 1 student student 0 Feb 4 18:44 song6.mp3
```

你的项目现在完成了，现在是时候清理项目了。

切换到学生的主目录。尝试使用单个 **rmdir** 命令同时删除 **family** 和 **friends** 项目目录。

```
[student@servera]$ cd ~
[student@servera]$ rmdir family friends
rmdir: failed to remove 'family': Directory not empty
rmdir: failed to remove 'friends': Directory not empty
```

使用 **rm -r** 命令将会失败，因为子目录中包含文件。

- 9. 使用 **rm -r** 命令递归删除 **family** 和 **friends** 子目录及其内容。

```
[student@servera]$ rm -r family friends
[student@servera]$ ls -l
total 0
drwxrxr-x. 2 student student 108 Feb 4 18:36 Music
drwxrxr-x. 2 student student 108 Feb 4 18:36 Pictures
drwxrxr-x. 2 student student 108 Feb 4 18:36 Videos
drwxrxr-x. 2 student student 108 Feb 4 18:44 work
```

- 10. 删除 work 项目中的所有文件，但不要删除 work 目录。

```
[student@servera ~$] cd work
[student@servera ~] rm song5.mp3 song6.mp3 snap5.jpg snap6.jpg \
> film5.avi film6.avi
[student@servera ~]$ ls -l
total 0
```

- 11. 最后，从学生的主目录使用 rmdir 命令删除 work 目录。该命令应该成功。

```
[student@servera]$ cd ~
[student@servera]$ rmdir family friends
[student@servera]$ ls -l
total 0
```

- 12. 退出 servera。

```
[student@servera]$ exit
```

