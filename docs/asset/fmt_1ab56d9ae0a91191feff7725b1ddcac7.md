
开发者使用以下命令通过 `diff` 的上下文 (`-c`) 选项构建补丁文件（见第 1149 页）。在此示例中，不需要 `--recursive` 选项，因为 `pi` 和 `Old_pi` 中没有子目录，但开发者仍然包含了它：

```
$ diff --recursive -c Old_pi pi >patch.1.1
```

`patch.1.1` 补丁文件包含了将旧版本 pi 应用程序更改为新版本所需信息：

```
$ cat patch.recursive.1
diff --recursive -c Old_pi/Makefile pi/Makefile
*** Old_pi/Makefile Wed Jul 3 14:13:20 2002
--- pi/Makefile Sun Aug 4 08:12:41 2002
**********************************
*** 2,10 ****
# makefile
#
CC = gcc
: CFLAGS = -03 -omit-frame-pointer -fwritable-strings
all: pi
pi: pi.c
$(CC) $(CFLAGS) -o pi $ -lm
--- 2,13 ---
# makefile
#
CC = gcc
! CFLAGS = -03 -omit-frame-pointer -fast-math -fwritable-strings
all: pi
pi: pi.c
$(CC) $(CFLAGS) -o pi $ -lm
clean:
+	rm -f *.o pi patch
+	diff --recursive -c Old_pi/patchlevel.h pi/patchlevel.h
*** Old_pi/patchlevel.h Sun Aug 4 08:16:08 2002
--- pi/patchlevel.h Sun Aug 4 10:24:29 2002
**********************************
*** 0 ****
--- 1,4 ---
+
# +define VERSION1
# +define PATCHLEVEL1
n+	diff --recursive -c Old_pi/pi.c pi/pi.c
*** Old_pi/pi.c Sun Jul 14 09:43:43 2002
--- pi/pi.c Sun Aug 4 08:09:45 2002
**********************************
*** 17,22 ****
--- 17,23 ---
* 486dx2/66 [Linux 1.2.13]: 126 cpu seconds,
* 486dx4/100 [Linux 1.2.13]: 92 cpu seconds)
* Cyrix 586dx4/100 [Linux 1.2.13]: 85 cpu seconds) [no speedups]
* Cyrix 586dx4/120 [Linux 2.0.00]: 77 cpu seconds) [speedups]
*/
**********************************
*** 171,176 ****
--- 172,179 ---
{
  int i;
char *s = "%dd.",NDS";
+ sprintf(s,"%dd",NDS,(int)a[0]);
+ sprintf(s,"%02d.",NDS,NDS);
  for (i = 1; i < nwd; i++) {
    printf(s,(int)a[i]);
