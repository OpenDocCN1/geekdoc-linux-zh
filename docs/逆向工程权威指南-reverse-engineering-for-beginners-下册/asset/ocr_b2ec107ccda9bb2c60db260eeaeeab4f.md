# ## 第78章 加密狗

# ### 78.1 例:PowerPC平台上的MacOS Classic程序

本例研究的是一款运行在PowerPC平台上的MacOS Classic程序。研发程序的公司早就已经不知向，所以买家十分害怕加密狗出什么意外。

在不插入加密狗的情况下，程序会显示“Invalid Security Device”信息。非常幸运的是，这个字符串在程序的可执行文件里。

那时我不熟悉Mac OS Classic系统，也没有怎么用过PowerPC，但是还是放一搏。

IDA可以毫无难度地打开这个程序。判断该文件的类型为“PEF (Mac OS or Be OS executable)”。标准的Mac OS Classic的程序内核采用了这种文件格式。

接下来，在文件中搜索错误信息的字符串时，我找到了下述指令:

```
seg000:00087FC 38 60 00 01      li      %r3, 1
seg000:0008800 48 03 93 41      check1
seg000:0008804 60 00 00 00      nop
seg000:0008808 54 60 06 3F      clrlwi.%r0, %r3, 24
seg000:000880C 40 82 00 40      bne     OK
seg000:0008810 80 62 9F D8      lzw     %r3,
```