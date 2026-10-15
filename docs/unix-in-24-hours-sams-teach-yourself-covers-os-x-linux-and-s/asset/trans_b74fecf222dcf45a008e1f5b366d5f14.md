

```
% echo bu* d* sa*
buckaroo buckaroo.confused dickens.note sample sample2
```

```
% echo bu* d* sa*2
buckaroo buckaroo.confused dickens.note sample2
```

```
% ls
Archives      awkscript      dickens.note   src
InfoWorld     bin            keylime.pie    temp
Mail          buckaroo       owl.c
News          buckaroo.confused sample
OWL           cshrc          sample2
```

```
% alias ls='ls -CP'
% ls
Archives/      awkscript      dickens.note   src/
InfoWorld/     bin/           keylime.pie    temp/
Mail/          buckaroo       owl.c
News/          buckaroo.confused sample
OWL/           cshrc          sample2
```

```
% alias DIR 'ls -lF'
% alias REN 'mv'
% alias COPY 'cp -I'
% alias DEL 'rm -I'
% DIR
total 33
drwx------  2 taylor        512 Nov 21 10:39 Archives/
drwx------  3 taylor        512 Dec  3 02:03 InfoWorld/
drwx------  2 taylor       1024 Dec  3 01:43 Mail/
drwx------  2 taylor        512 Oct  6 09:36 News/
drwx------  4 taylor        532 Dec  6 18:31 OWL/
-rw-rw----  1 taylor        126 Dec  3 16:34 awkscript
drwx------  2 taylor        512 Oct 13 10:45 bin/
-rw-rw----  1 taylor       1393 Dec  5 18:48 buckaroo
-rw-rw----  1 taylor        458 Dec  4 23:22 buckaroo.confused
-rw-------  1 taylor       1339 Dec  2 10:30 cshrc
-rw-rw----  1 taylor       1123 Dec  5 18:16 dickens.note
-rw-rw----  1 taylor      12556 Nov 16 09:49 keylime.pie
-rw-rw----  1 taylor       8729 Dec  2 21:19 owl.c
-rw-rw----  1 taylor        199 Dec  3 16:11 sample
-rw-rw----  1 taylor        207 Dec  3 16:11 sample2
drwx------  2 taylor        512 Oct 13 10:45 src/
drwxrwx---  2 taylor        512 Nov  8 22:20 temp/
% COPY sample newsample
%
```

```
% alias DIR= 'ls -LF | less'
```

```sh
% alias
alias diff='/usr/bin/diff -c -w'
alias from='frm -n'
alias ls='/bin/ls -F'
alias mail='Mail'
alias mailq='/usr/lib/sendmail -bp'
alias newaliases='echo you mean newalias...'
alias rm='/usr/local/bin/rm -d$HOME -L -M -m -- -e -S -/'
alias intuitive='echo Intuitive.com;echo '\''MyPassword'\''|pbcopy;ssh dtaylor@intuitive.com'
```

```
% grep alias .bashrc
alias diff='/usr/bin/diff -c -w'
alias from='frm -n'
alias ll='ls -l'
alias ls='/bin/ls -F'
alias mail=Mail
alias mailq='/usr/lib/sendmail -bp'
alias newaliases='echo you mean newalias...'
alias rn='/usr/local/bin/rn -d$HOME -L -M -m -e -S -/'
alias intuitive='echo Intuitive.com; \
echo '\''MyPassWord.'\'' | pbcopy;ssh dtaylor@intuitive.com'
```

```
$ alias intuitive
alias intuitive='echo Intuitive.com;echo '\''MyPassWord.'\'' '| pbcopy;ssh ► dtaylor@intuitive.com'
```

是的，主人？ PS1="In \w, oh master: "
In /users/taylor, oh master:

```
In /users/taylor, oh master: cd /
In /, oh master:
```

In /, oh master: PS1="(The current command is #\!) $ "
(The current command is #132) $

```
(132) $ echo hi
hi

(133) $ ls News
mailing.lists.usenet usenet.1 usenet.alt

(134) $ !132
echo hi
hi

(135) $
```

limbo (136) $ PS1="\h (\W) \! : "
limbo (taylor) 137 :

#33 - 我对 Unix 很了解。例如：

```
$ man sort
```

# 名称

sort - 排序或合并文件

# 用法

sort [ -mubdfinrtx ] [ +pos1 [ -pos2 ] ] ... [ -o name ] [ -T directory ] [ name ] ...

# 描述

Sort 会将所有命名文件中的行一起排序并写入标准输出。名称 '-' 表示标准输入。如果没有命名输入文件，则对标准输入进行排序。

默认排序键为整行。默认排序方式为按机器排序序列中的字节进行字典排序。排序方式受以下选项的全局影响，可以出现一个或多个。

+   b    忽略字段开头的空白字符（空格和制表符）

