
所有错误条件都应打印友好消息并以状态码 1 退出。例如，如果未传递三个参数，或传递的目录不存在，或者某个 `test` 参数无效。请参阅下文 **Answer 1** 中提供的可能解决方案之一。

作为额外挑战，你可以打印所有文件，但根据它们通过测试的数量进行排序。

# Answer 1

```bash
#!/bin/bash

test $# -eq 3 || { echo "Exactly three arguments are required."; exit 1; }

test -d $1 || { echo "Not a directory."; exit 1; }

files=$(ls $1 2>/dev/null) || { echo "I can't read that directory.";
exit 1; }

for f in $files; do

   test $2 $1/$f 2>/dev/null
   rc1=$?

   test $3 $1/$f 2>/dev/null
   rc2=$?

   test $rc1 -gt 1 && { echo "First test argument is invalid."; exit 1;
   }

   test $rc2 -gt 1 && { echo "Second test argument is invalid."; exit 1;
   }

   test $rc1 -eq 0 && test $rc2 -eq 0 && echo $f

done
```

# Notes

请记住，使用 `/bin/sh` 作为解释器可能会产生与 `/bin/bash` 不同的结果！了解什么是 `Bourne-compatible` shell，以及 Bash 中有哪些非 `Bourne-compatible` 的附加功能，这是很有帮助的。
