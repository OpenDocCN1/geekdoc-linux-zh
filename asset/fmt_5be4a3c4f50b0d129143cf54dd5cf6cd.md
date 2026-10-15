
`-`+0 -4` 指定第 4 字段：城市

## 排序文件与管道 第 10 章

前面的输出是按第 4 字段排序的（因为你跳过了三个字段），但它将 `group` 放在了 `accounting` 之前。考虑到第 4 字段实际上看起来如下所示，这就很合理：

```
<space><space><space><space>group
<space><space>accounting
<space><space>accounting
<space>mgr
```

你可以使用 `sort +3b` 来解决这个问题，这意味着在排序时跳过三个字段，并忽略开头的空格。你实际上是在 `+3` 字段指定符之后使用了 `-b` 选项。只要有前后的字段指定符，`-b` 选项在所有 UNIX 系统上都能工作：

```
$ ls -l | sort +3b
total 3
-rw-r--r-- 1 janepf accounting 1972 Feb 1 11:33 rep04
-rw-r--r-- 1 janepf accounting 25 Feb 1 11:33 rep08
-rw-r--r-- 1 mori group 196484 Feb 1 11:33 rep07
-rw-r--r-- 1 william mgr 17157 Feb 1 11:33 acme
(field 1 f2 f3 f4 f5 f6 f7 f8 f9)
```

上面的示例显示你已经成功地按 `group` 排序：先是 `accounting`，然后是 `group`。如果你想按第 5 字段的文件大小对相同输出进行排序，你将遇到类似的问题，需要不同的解决方案。虽然大小数字似乎是右对齐的（因此可以问题地排序），但前面的第 4 字段并没有在每行的列处结束。每个第 5 字段都以随机数量的开头空格开始，这将阻止按所需的顺序排序。如果你像以前一样简单地忽略开头空格，将得到以下结果：

```
$ ls -l | sort +4b
total 3
-rw-r--r-- 1 william mgr 17157 Feb 1 11:33 acme
-rw-r--r-- 1 mori group 196484 Feb 1 11:33 rep07
-rw-r--r-- 1 janepf accounting 1972 Feb 1 11:33 rep04
-rw-r--r-- 1 janepf accounting 25 Feb 1 11:33 rep08
(field 1 f2 f3 f4 f5 f6 f7 f8 f9)
```

在前面的输出中，注意数字是按正确的 ASCII 顺序排序的：

```
171
196
197
25
```

ASCII 顺序并没有按大小排序数字。你希望文件大小按数值排序，而不是按 ASCII 顺序。当你使用 `sort -n` 按数值排序时，它

## 第二部分 与 UNIX 文件的操作、修改、合并与拆分

## 第10 章 比较、排序与合并

会自动忽略开头空格：

```
$ ls -l | sort +4n
total 3
-rw-r--r-- 1 janepf accounting 25 Feb 1 11:33 rep08
-rw-r--r-- 1 janepf accounting 1972 Feb 1 11:31 rep04
-rw-r--r-- 1 william mgr 17157 Feb 1 11:31 acme
-rw-r--r-- 1 mori group 196484 Feb 1 11:33 rep07
(field 1 f2 f3 f4 f5 f6 f7 f8 f9)
```

### 基于主键和次键的排序

假设你有一个 `friends` 文件，其中列出了几个朋友的名字、中间名、姓氏和城市。注意如果按姓氏排序会发生什么：

```
$ sort +2 friends # 这不是我们想要的
William A. Smith, St. Louis
James B. Nguyen, Los Angeles
Henry H. Nguyen, Yuba City
Mary K. Zornan, Cleveland
Mary A. Zornan, Pittsburgh
```

注意 `Smith` 排在最前面，是因为在那个条目中 `Smith` 之前恰好有两个空格，而空格-空格在字母之前，就像 `aa` 在 `ab` 之前一样。你可以通过添加 `-b` 选项来忽略开头空格，如下所示：

```
$ sort -b +2 friends # 这更接近我们想要的
James B. Nguyen, Los Angeles
Henry H. Nguyen, Smith, St. Louis
William A. Smith, St. Louis
Mary K. Zornan, Cleveland
Mary A. Zornan, Pittsburgh
```

注意两个 `Nguyen` 条目是按城市排序的。这是可以理解的，因为你跳过了前两个字段并对行的其余部分进行排序。如果你想按姓氏排序，如果姓氏相同，再按名字排序？这个过程被称为使用主键和次键排序。这里是排序键的一般格式：

```
+m -n
```

`+m` 指定跳过多少字段以到达键的开始。`-n` 指定键中的最后一个字段。

## 排序文件与管道 第二章

在上一个示例中，这里是你可以使用的一些可能的排序键：

- `+0 -1` 指定第 1 字段：名字
- `+1 -2` 指定第 2 字段：中间字母
- `+0 -2` 指定第 1 和第 2 字段：名字和中间字母

## 第二部分 操作 UNIX 文件

## 第 10 章 文件的比较、排序、修改、合并与拆分

> 警告
你将需要知道此密钥的准确拼写，以便稍后解密并使用你的文件。该密钥没有后门可走，因此如果你忘记了这个密钥，就无法解密你的文件。

- 5. 在你于第 4 步中输入密钥后，`tmpfile$$` 将包含加密信息。
- 6. 输入此命令测试 `tmpfile$$`：

```
crypt < tmpfile$$ > tmp2$$
```

再次，你将看到此提示：
输入密钥：

- 7. 输入与加密此文件时相同的密钥。请注意，同一个密钥用于加密和解密该信息。
- 8. 输入 `cmp EXISTING-FILE tmp2$$`。
将 `EXISTING-FILE` 替换为你想要加密的原始文件名。此 `cmp` 命令应该直接返回到 shell 提示符而没有其他输出，表示两个文件是相同的。如果不是，说明出了问题。
不要继续执行此操作。可能是你输入错误的密钥。尝试重新回到第 6 步。如果第 7 步显示文件不相同，请按如下删除临时文件：

```
rm tmpfile$$ tmp2$$
```

然后回到此操作的第 1 步。

- 9. 输入 `mv tmpfile$$ EXISTING-FILE`。
将 `EXISTING-FILE` 替换为你想要加密的原始文件名。这将用加密版本替换原始文件。
- 10. 输入 `rm tmp2$$`。
这将删除你不再需要的临时文件。

要解密文件，输入以下内容：

```
crypt < ENCRYPTED-FILE > DECRYPTED-FILE
```

将 `ENCRYPTED-FILE` 替换为要解密的文件。将 `DECRYPTED-FILE` 替换为你想要创建的任何新名称。确保该名称已存在，因为名称将被此命令覆盖。`crypt` 将输出此提示消息：

输入密钥：
然后输入与加密该文件时相同的密钥。

### 修改文件或管道 第 10 章

你也可以在命令行中提供密钥，例如：

```
crypt "Mary had a little lamb" < file1 file2
```
