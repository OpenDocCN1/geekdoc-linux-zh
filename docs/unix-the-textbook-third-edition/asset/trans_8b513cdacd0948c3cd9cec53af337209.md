

## 表 3.18 Emacs 概要

### Emacs 命令

| 命令 | 操作 |
| --- | --- |
| <Ctrl+X><Ctrl+F> | 访问一个文件 (find-file) |
| <Ctrl+X><Ctrl+R> | 以只读方式访问文件，不允许对其进行更改 (find-file-read-only) |
| <Ctrl+X><Ctrl+V> | 改为访问另一个文件，而不是上次访问的文件 (find-alternate-file) |
| <Ctrl+X><Ctrl+S> | 将当前缓冲区保存到其文件中 (save-buffer) |
| <Ctrl+X> s | 将一个或所有缓冲区保存到其文件中 (save-some-buffers) |
| <Alt+~> | 忘记当前缓冲区已被更改 (not-modified) |
| <Ctrl+X><Ctrl+W> | 使用指定的文件名保存当前缓冲区 (write-file) |
| <Ctrl+H> | 显示有关这些选项的帮助信息 |
| <Ctrl+X><Ctrl+C> | 退出 emacs |
| <Ctrl+X><Ctrl+Z> | 挂起 emacs 并退出到 shell |
| **Emacs 帮助命令** |  |
| <Ctrl+H> a topics <Enter> | 显示名称与 topics 匹配的命令列表 (apropos-command)。 |
| <Ctrl+H> b | 显示所有活动键绑定——先是次要模式绑定，然后是主要模式绑定，最后是全局绑定 (describe-bindings)。 |
| <Ctrl+H> c key | 显示键序列 key 所绑定的命令名称 (describe-key-briefly)。 这里 c 代表 "character"。 要获取有关 key 的更详细信息，请使用 <Ctrl+H> k。 |
| <Ctrl+H> d topics <Enter> | 显示文档与 topics 匹配的命令和变量 (apropos-documentation)。 |
| <Ctrl+H> e | 显示 *Messages* 缓冲区 (view-echo-area-messages)。 |
| <Ctrl+H> f function <Enter> | 显示名为 function 的 Lisp 函数的文档 (describe-function)。 由于命令是 Lisp 函数，因此这也适用于命令。 |
| <Ctrl+H> r | 在 Info 中显示 emacs 手册 (info-emacs-manual)。 |
| <Ctrl+H> s | 显示当前语法表的內容 (describe-syntax)。 语法表说明哪些字符是打开的分隔符，哪些是单词的一部分，等等。 |
| <Ctrl+H> t | 进入 emacs 交互式教程 (help-with-tutorial)。 |
| <Ctrl+H> K key | 进入 Info 并转到记录键序列 key 的节点 (Info-goto-emacs-key-command-node)。 |
| <Ctrl+H> | 显示特殊文本区域的帮助信息，如果光标位于其中 (display-local-help)。 （例如，“帮助”缓冲区中的链接。） |

### Emacs 光标移动

| **要移动的实体** | **向后** | **向前** |
| --- | --- | --- |
| 字符 | <Ctrl+B> | <Ctrl+F> |
| 单词 | <Alt+B> | <Alt+F> |
| 行 | <Ctrl+P> | <Ctrl+N> |
| 移至行开头（或结尾） | <Ctrl+A> | <Ctrl+E> |
| 句子 | <Alt+A> | <Alt+E> |
| 段落 | <Alt+{> | <Alt+}> |
| 页面 | <Ctrl+X> [ | <Ctrl+X> ] |
| **要删除的实体** | **向后** | **向前** |
| 字符（删除，而非杀死） | <Del> | <Ctrl+D> |
| 单词 | <Alt+Del> | <Alt+D> |
| 行（至行尾） | <Alt+O> | <Ctrl+K> |
|  | <Ctrl+K> |  |
| 句子 | <Ctrl+X> DEL | <Alt+K> |
| 杀死区域 | <Ctrl+W> |  |
| 将区域复制到杀死环 | <Alt+W> |  |
| 粘贴上次杀死的内容 | <Ctrl+Y> |  |

### Emacs 交互式搜索和替换

| **搜索和替换操作** | **按键** |
| --- | --- |
| 向前搜索 | <Ctrl+S> |
| 向后搜索 | <Ctrl+R> |
| 正则表达式搜索 | <Ctrl+Alt+S> |
| 反向正则表达式搜索 | <Ctrl+Alt+R> |
| 选择上一个搜索字符串 | <Alt+P> |
| 选择下一个搜索字符串 | <Alt+N> |
| 退出增量搜索 | <Enter> |
| 撤销上一个字符的效果 | <Del> |
| 中止当前搜索 | <Ctrl+G> |
| 交互式替换文本字符串 | <Alt+%> |
| 使用正则表达式 | <Alt+X> query-replace-regexp |
| 替换此项，继续下一个 | <Space> 或 y |
| 替换此项，不移动 | , |
| 跳过下一个不替换 | <Del> 或 n |
| 替换所有剩余匹配项 | ! |
| 返回到上一个匹配项 | ^ |
| 退出 query-replace | <Enter> |
| 进入递归编辑（<Ctrl+Alt+C> 退出） | <Ctrl+R> |

### 更改 Emacs 行为

| 自定义操作 | 按键 |
| **缩写** |  |
| 添加全局缩写 | <Ctrl+X> a g |
| 添加模式本地缩写 | <Ctrl+X> a l |
| 为此缩写添加全局展开 | <Ctrl+X> a i g |
| 为此缩写添加模式本地展开 | <Ctrl+X> a i l |
| 显式展开缩写 | <Ctrl+X> a e |
| 动态展开前一个词 | <Alt+/> |
| **宏** |  |
| 开始定义键盘宏 | <Ctrl+X> ( 或 <F3> |
| 结束键盘宏定义 | <Ctrl+X> ) 或 <F4> |
| 执行上次定义的键盘宏 | <Ctrl+X> e 或 <F4> |
| 向上次键盘宏追加 | <Ctrl+U> <Ctrl+X> ( |
| 为上次键盘宏命名 | <Alt+X> name-last-kbd-macro |
| 在缓冲区中插入 Lisp 定义 | <Alt+X> insert-kbd-macro |
| 自定义变量和外观 | <Alt+X> customize |

## 问题与练习

### Vi, Vim, Gvim

1. 尽管有功能强大且花哨的字处理器，为什么文本编辑仍然很重要？
2. 列出 10 个常用的文本编辑操作。
3. UNIX 中最流行的四个文本编辑器是什么？你最喜欢哪一个？为什么？
4. 什么是编辑器缓冲区？
5. 本题假设你在使用 PC-BSD 上的 C shell，并且将从你的主目录在系统上执行你将创建的文件。 如果你运行的是 Solaris，请对以下 shell 脚本文件做出适当更改以使其在 Bash 中工作。 请注意 Solaris 中没有 /etc/shells 文件，因此可以从你的 shell 脚本文件中省略该行。
   a. 如何确保你的搜索路径包含你保存以下脚本文件的目录，并且该文件具有执行权限？
   使用你系统上的 vi 并创建一个 C shell 脚本文件，其中包含以下行：

   ```
   #!/bin/csh
   ```
