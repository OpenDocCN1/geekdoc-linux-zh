
如果方便的话，请告诉我，这样我下次去你们旅馆时就不必等到明年了。

此致，

Mackenzie Elizabeth

~
~
~
~
~
~
~
~

`*project4*` `17L, 583C`

请注意，屏幕底部显示了文件名以及总行数和字符数（在此示例中，`project4` 有 17 行和 583 个字符）。要在文件底部插入当前的日期和时间，只需将光标移动到文件最后一行，然后在命令模式下的 `:` 提示符处输入以下内容：

```
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining room this year while vacationing in Algonquin Park - I especially wished to see the model of the Highland Inn and the train station in the dining room.

I have been reading on the history of Algonquin Park but no where could I find a description of where the Highland Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
Sat Apr 30 18:33:10 EDT 2005
~
~
~
~
~
: r !date
```

按下 `Enter` 键后，`date` 命令的输出会插入到当前行下方：

```
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining room this year while vacationing in Algonquin Park - I especially wished to see the model of the Highland Inn and the train station in the dining room.

I have been reading on the history of Algonquin Park but no where could I find a description of where the Highland Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
Sat Apr 30 18:33:10 EDT 2005
~
~
~
~
~
```

要将单词 “Algonquin” 的所有出现更改为 “ALGONQUIN”，只需在命令模式下的 `:` 提示符处输入以下内容：

```
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining room this year while vacationing in Algonquin Park - I especially wished to see the model of the Highland Inn and the train station in the dining room.

I have been reading on the history of Algonquin Park but no where could I find a description of where the Highland Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
Sat Apr 30 18:33:10 EDT 2005
~
~
~
~
~
:1,$ s/Algonquin/ALGONQUIN/g
```

输出更改为以下内容：

```
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining room this year while vacationing in ALGONQUIN Park - I especially wished to see the model of the Highland Inn and the train station in the dining room.

I have been reading on the history of ALGONQUIN Park but no where could I find a description of where the Highland Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
Sat Apr 30 18:33:10 EDT 2005
~
~
~
~
~
~
```

`vi` 编辑器的另一个吸引之处在于它能够通过设置来自定义用户环境，这些设置可以在命令模式下的 `:` 提示符处进行更改。只需在此提示符处输入 `set all`，即可查看可用设置的列表及其当前值：
