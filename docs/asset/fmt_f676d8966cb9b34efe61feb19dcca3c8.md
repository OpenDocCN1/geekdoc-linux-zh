
假设你想覆盖一个磁带文件，以便使用高级语言 (`HLL`) 程序将物理文件中的记录写入磁带。你可以在调用 `HLL` 程序之前，在 `CL` 程序中指定此覆盖。覆盖和调用显示如下：

```
OvrTapF FILE(QSap) DEV(01) RCDLEN(256) BLKLEN(512)

CALL HLLPROG
```

## 你认为你理解了文件覆盖 339

因为覆盖覆盖，`HLL` 程序打开的是 `QPrint` 而不是 `Report`。

另一个覆盖示例是选择多成员文件的成员。例如，为了处理 `Orders` 中的成员 `Ord2011`（2000 年 11 月的订单），你会指定

```
OvrDbF FILE(Orders) MBR(Ord2011)

CALL HLLProg
```
