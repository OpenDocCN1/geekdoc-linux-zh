
使用等号会生成所谓的“绝对”权限赋值。

再次列出您的主目录，以确保 **newdir** 的权限与图 8-1 中显示的一致。

图 8-2 展示了一个与我们在 *Linux Made Easy CBT* 中展示图表类似的图表。**chmod** 命令的结构非常简单：(1) ***谁*** 会被该更改影响：**ugoa**（用户、组、其他人、所有人）；(2) 你采取的 ***什么*** *操作*：**+** **-** =（添加、移除、绝对） **rwx**（权限）；(3) 受影响的 ***哪个*** *文件* 或 *目录*：**filename**。

我们可以用三个词来总结 **chmod**：***谁***、***什么***、***哪个***。

![](img/cc8b9fd5970716027fba0d0a45c13900_156_0.png)

# 图 8-2 chmod 命令的语法

在接下来的系列练习中，您将多次更改 **newdir** 的权限。（注意，其中一些生成的权限在 Linux 逻辑上并不合理。这些练习的目的是让您练习使用 **chmod**。）

- 5. 为组添加对 **newdir** 的写权限。
  - a. 输入 **chmod g+w newdir**
  - 谁、什么、哪个。
  - b. 按 <Enter>
  - c. 列出您的主目录，并检查您的工作。您应该看到 **newdir** 的权限如图 8-3 所示。

![](img/cc8b9fd5970716027fba0d0a45c13900_156_1.png)

# 图 8-3 为组添加对 newdir 的写权限的结果

- 6. 移除其他人对 *newdir* 的读权限。
  - a. 输入 **chmod o-r newdir**。
  - 谁、什么、哪个。
  - b. 按 <Enter>
  - c. 列出您的主目录，并检查您的工作。您应该看到 *newdir* 的权限如图 8-4 所示。

```
drwxrwx--x  1  ronsm  1024  Nov 8  16:00  newdir
drwxrwxr-x  1  ronsm  1024  Mar  1  12:23  practice
```

图 8-4 移除其他人对 *newdir* 读权限的结果

- 7. 移除组和他人对 **newdir** 的执行权限。
  - a. 输入 **chmod go-x newdir**
  - 谁、什么、哪个。
  - b. 按 <Enter>
  - c. 列出您的主目录，并检查您的工作。您应该看到 **newdir** 的权限如图 8-5 所示。

```
drwxrw----  1  ronsm  1024  Nov 8  16:00  newdir
drwxrwxr-x  1  ronsm  1024  Mar  1  12:23  practice
```

图 8-5 移除组和他人对 *newdir* 执行权限的结果

- 8. 将 *newdir* 的组权限更改为读和执行；为 **newdir** 的其他人添加读权限。
  - a. 输入 **chmod g=rx,o+r newdir**
  - 谁、什么、哪个。
  - b. 按 <Enter>
  - c. 列出您的主目录，并检查您的工作。您应该看到 **newdir** 的权限如图 8-6 所示。

```
drwxr-xr-x 1 ronsm 1024 Nov 8 16:00 newdir
drwxrwxr-x 1 ronsm 1024 Mar 1 12:23 practice
```

图 8-6 将组权限更改为读和执行并为 others 添加读权限对 newdir 的结果

- 9. 将所有人对 newdir 的权限更改为读和执行。
  - a. 输入 `chmod a=rx newdir`
  - 谁、什么、哪个。
  - b. 按 <Enter>。
  - c. 列出您的主目录，并检查您的工作。您应该看到 newdir 的权限如图 8-7 所示。

```
dr-xr-xr-x 1 ronsm 1024 Nov 8 16:00 newdir
drwxrwxr-x 1 ronsm 1024 Mar 1 12:23 practice
```

图 8-7 将所有人对 newdir 的权限更改为读和执行的結果

- 10. 为用户添加对 newdir 的写权限。
- 11. 列出您的主目录，并检查练习 10 中的工作。您应该看到 newdir 的权限如图 8-8 所示。

```
drwxr-xr-x 1 ronsm 1024 Nov 8 16:00 newdir
drwxrwxr-x 1 ronsm 1024 Mar 1 12:23 practice
```

图 8-8 为用户添加对 newdir 写权限的结果

- 12. 移除其他人对 newdir 的执行权限。

- 13. 列出您的主目录，并检查练习 12 中的工作。您应该看到 **newdir** 的权限如图 8-9 所示。

```
drwxr-xr-- 1 ronsm 1024 Nov 8 16:00 newdir
drwxrwxr-x 1 ronsm 1024 Mar 1 12:23 practice
```

# 图 8-9 移除其他人对 newdir 执行权限的结果

- 14. 为其他人添加写权限；为 **newdir** 的组移除读权限。

- 15. 列出您的主目录，并检查练习 14 中的工作。您应该看到 **newdir** 的权限如图 8-10 所示。

```
drwx--xrw 1 ronsm 1024 Nov 8 16:00 newdir
drwxrwxr-x 1 ronsm 1024 Mar 1 12:23 practice
```

# 图 8-10 为其他人添加写权限并为组移除读权限对 newdir 的结果

- 16. 移除用户的读权限；为 **newdir** 的组添加读权限。

- 17. 列出您的主目录，并检查练习 16 中的工作。您应该看到 **newdir** 的权限如图 8-11 所示。

```
d-wxr-xrw 1 ronsm 1024 Nov 8 16:00 newdir
drwxrwxr-x 1 ronsm 1024 Mar 1 12:23 practice
```

# 图 8-11 移除用户读权限并为组添加读权限对 newdir 的结果

- 18. 将 **newdir** 的权限更改为所有人的读和执行。

- 19. 列出您的主目录，并检查练习 18 中的工作。您应该看到 newdir 的权限如图 8-12 所示。

![](img/cc8b9fd5970716027fba0d0a45c13900_160_0.png)

图 8-12 将 newdir 权限更改为所有人读和执行的結果

# 自测

- 1. 谁可以授予您访问 Linux 系统的权限？
  - a. 任何已有访问权限的人
  - b. 超级用户
  - c. 系统的所有者
  - d. 任何既有访问权限又有 Linux 经验的人

- 2. 如果系统不识别您的 userid，您将无法获得访问权限。
  - a. 正确
  - b. 错误

- 3. 文件模式（File mode）指的是
  - a. 普通文件。
  - b. 目录。
  - c. 两者皆是。
  - d. 两者皆非。

- 4. 您使用此命令获取显示文件模式的目录列表：
  - a. ls -l
  - b. ls -a
  - c. ls -l
  - d. ls -m

图 8-13 中的字母 "a"、"b" 和 "c" 标识了文件模式的三个不同部分。问题 5-7 参考此图。

![](img/cc8b9fd5970716027fba0d0a45c13900_161_0.png)

- 5. 哪一部分代表其他人——那些不在用户工作组中的人？
  - a. a
  - b. b
  - c. c

- 6. 哪一部分代表用户——文件的所有者？
  - a. a
  - b. b
  - c. c

- 7. 哪一部分代表组——那些在用户工作组中的人？
  - a. a
  - b. b
  - c. c

- 8. 谁可以更改文件的权限？
  - a. 组的成员
  - b. 用户——文件的所有者
  - c. 仅限超级用户
  - d. 任何人

问题 9–19 参考图 8-14。

```
-rw-r----  1 ronsm sales 7003  Fri Nov 17 jones
        drwxr----- 1 ronsm sales 4365  Wed May 10 letters
        -rw-r----- 1 ronsm sales 3152  Tue Aug 29 misc
        drwxr-xr-- 5 ronsm sales 12343 Tue Jan 18 north
        -rwxr-xr-x 5 roban sales 44689 Tue Aug 29 spell
        drwxr-xr-- 8 sara  admin 23111 Mon Feb 14 staff
```

# 图 8-14 ls -l 的输出

- 9. 哪些文件其他人可以读？
  - a. jones, letters, misc
  - b. jones, misc, staff
  - c. misc, spell, jones, spell

- 10. 哪些文件其他人可以写入？
  - a. jones, north
  - b. misc, spell
  - c. jones, misc
  - d. 无

- 11. 哪些文件组可以读？
  - a. jones, misc, spell
  - b. letters, north, staff
  - c. staff, spell, misc
  - d. jones, letters

- 12. 哪些文件组可以写入？
  - a. letters, misc
  - b. misc, spell
  - c. jones
  - d. misc

- 13. 谁可以执行 spell？
  - a. 用户, 组
  - b. 用户, 组, 其他人
  - c. 仅用户
  - d. 仅组

- 14. 哪些条目是目录？
  - a. jones, letters, north
  - b. letters, north, spell
  - c. letters, north, staff
  - d. north, spell, staff

- 15. 组可以使用 cd 进入哪些目录？
  - a. letters, north, staff
  - b. letters, north
  - c. north, staff
  - d. jones, letters, north

- 16. 组可以使用 cat 查看哪些目录？
  - a. letters, north, staff
  - b. letters, north
  - c. north, staff
  - d. jones, letters, north

- 17. 组可以使用 ls 查看哪些目录？
  - a. letters, north
  - b. letters, north, staff
  - c. north, staff
  - d. jones, letters, north

- 18. 组可以使用 ls -l 查看哪些目录？
  - a. north, staff
  - b. letters, north, staff
  - c. letters, north
  - d. 无

- 19. 组可以使用 rm 操作哪些目录？

