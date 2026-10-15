
```
cdemmert ttyS5  Dec  3 23:00   (mentor)
yuenca   ttyS6  Dec  3 23:00   (mentor)
janitor  ttyS7  Dec  3 18:18   (age)
mathisbp ttyS8  Dec  3 23:17   (dov)
```

If your cursor isn’t somewhere in the middle of this line, move it so that you aren’t at an edge.

I had planned to remove this line completely, but perhaps I’d rather just remove the date, time, and name of the system (in parentheses) instead. To accomplish this, I don’t need to type `dw` many times, or even `x` many times but rather `D` to delete through the end of the line:

[Click here to view code image](#)

```
chenlx2  ttyru  Dec  3 21:53   (mentor)
leungtc  ttyS0  Nov 28 15:11   (gold)
chinese  ttyS2  _
cdemmert ttyS5  Dec  3 23:00   (mentor)
yuenca   ttyS6  Dec  3 23:00   (mentor)
```

| 名称 | ttyp | 日期 | 时间 | (角色) |
|------|------|------|------|--------|
| labeck | ttyrt | 12月3日 | 22:02 | (dov) |
| chenlx2 | ttyru | 12月3日 | 21:53 | (mentor) |
| leungtc | ttyrs0 | 11月28日 | 15:11 | (gold) |
| cdemmert | ttyrs5 | 12月3日 | 23:00 | (mentor) |
| yuenca | ttyrs6 | 12月3日 | 23:00 | (mentor) |
| mathisbp | ttyrs8 | 12月3日 | 23:17 | (dov) |
| janitor | ttyrs9 | 12月2日 | 18:18 | (age) |
| gs541 | ttysc | 12月3日 | 15:16 | (solaria) |
| yansong | ttysl | 12月1日 | 14:44 | (math) |
| mdps | ttyso | 11月30日 | 19:39 | (localhost) |
| md | ttysu | 12月2日 | 08:45 | (muller) |
| jac | ttysa | 12月3日 | 18:18 | (localhost) |
| eichsted | ttysb | 12月3日 | 23:21 | (pcl) |
| sweett | ttysc | 12月3日 | 22:40 | (dov) |
| wellman | ttysd | 12月3日 | 23:01 | (dov) |
| tuttleno | ttyse | 12月3日 | 23:03 | (indyvax) |

被删除行下方的每一行都会上移一行来填补空白，新的一行（即 `tuttleno` 的行）则移入视野。

5. 现在我想回到 `buckaroo` 文件，修正一些可怕的排版错误！我并不在意是否保存刚才对这个文件的更改，所以我会使用 `:q!` 退出并放弃对 `big.output` 文件的修改。

输入 `vi buckaroo` 会再次启动 `vi`：

> I found myself stealing a peek at my own watch and overheard
>
> General Catbird's
>
> aide give him the latest.
>
> "He's not even here," went the conservation.
>
> "Who?"
>
> "Banzai."
>
> "Where the hell is he?"
>
> "At the hotspial in El paso."
>
> "What? Why weren’t we informed? What's wrong with him?"

```
"buckaroo" 9 lines, 277 characters
```

你可以很快地做几处修正。第一处是将第三行的 `conservation` 改为 `conversation`。要移到那里，按两次回车键，然后使用 `w` 快速前进，直到光标停在你正在编辑的单词的第一个字母上：

```
I found myself stealing a peek at my own watch and overheard
General Catbird’s
aide give him the latest.
“He’s not even here,” went the conservation.
“Who?”
“Banzai.”
“Where the hell is he?”
```

然后使用 `dw` 命令：

```
I found myself stealing a peek at my own watch and overheard
General Catbird’s
aide give him the latest.
“He’s not even here,” went the _
“Who?”
“Banzai.”
“Where the hell is he?”
```

现在键入 `i` 进入插入模式，输入单词 `conversation` 的正确拼写，然后按 `Escape`：

```
I found myself stealing a peek at my own watch and overheard
General Catbird’s
aide give him the latest.
“He’s not even here,” went the conversation _
“Who?”
“Banzai.”
“Where the hell is he?”
```

6. 这是一处修正。现在向下移动几行，修正 `hospital` 令人发指的拼写错误：

```
“Banzai.”
“Where the hell is he?”
“At the hotsial in El paso.”
“What? Why weren’t we informed? What’s wrong with him?”
~
```

同样，使用 `dw` 删除该单词，键入 `i` 进入插入模式，输入 `hospital`，然后按 `Escape`。现在这一行没问题了：

```
“Banzai.”
“Where the hell is he?”
“At the hospital in El paso.”
“What? Why weren’t we informed? What’s wrong with him?”
~
```

嗯，几乎一切都好了。`Paso` 的首字母需要大写。键入 `w` 向前移动几个单词，移到那里：

```
“Banzai.”
“Where the hell is he?”
“At the hospital in El paso.”
“What? Why weren’t we informed? What’s wrong with him?”
~
```

7. 是时候介绍一个 vi 专家秘密命令了！与其输入 `x` 删除字母、`i` 进入插入模式、`P` 作为正确字母、然后按 `Escape` 返回命令模式，你可以使用一种更快的切换大小写的方法：`~`（波浪号）命令。输入一次 `~`，你会看到：

```
"Banzai."
"Where the hell is he?"
"At the hospital in El Paso."
"What? Why weren’t we informed? What’s wrong with him?"
~
```

很酷吧？再次回到单词开头，输入几次 `~`，看看会发生什么。注意每次输入 `~`，字符的大小写就会切换（转置），并且光标移动到下一个字符。输入 `~` 四次，你应该会得到：

```
"Banzai."
"Where the hell is he?"
"At the hospital in El pASO."
"What? Why weren’t we informed? What’s wrong with him?"
~
```
