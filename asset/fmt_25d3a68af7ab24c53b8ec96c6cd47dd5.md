
- 选择你想使用 ActionScript 的帧、按钮或电影剪辑。
- 此示例将赋值给变量。
- 点击 `Window Actions` 打开 `Actions` 面板。

注意：此示例使用了可以在随书光盘找到的 `fla`。

96

## 变量与字符串操作

### 此脚本演示了 `charCodeAt`。它检索变量 `phrase` 中字符的 ASCII 编码。变量 `sampleText` 是动态文本框。

你使用 `string.fromCharCode` 方法来获取 ASCII 编码。`string.fromCharCode` 方法如下：

示例：

```
(release) {
  phrase = 'JUMP OVER THE MOON';
  sampleText = phrase.charAt(6);
}
```

`string.fromCharCode(code1..., codeN)`; 代表字符编码。在此脚本中，用户输入字符并检索到编码。变量 `userEntry` 是输入框。变量 `character` 是动态文本。
示例：

```
(release) {
  character = string.fromCharCode(userEntry);
}
```

![](img/72fce958343eeb5d6d0322213ea85399_112_0.png)

![](img/72fce958343eeb5d6d0322213ea85399_112_1.png)

从六开始提取索引位置：
跳过月亮。

![](img/72fce958343eeb5d6d0322213ea85399_112_2.png)

![](img/72fce958343eeb5d6d0322213ea85399_112_3.png)

- 提取字符。
- 进入测试环境。
- ActionScript 提取索引位置 6 的字符。
- 此示例提取索引位置 6 的字符。

注意：查看第 38 页关于如何测试你的移动的说明。

- 如果将变量与动态文本框关联，可以将返回的值显示给用户。

## 从字符串中提取子字符串

你可以使用 `string.substring` 方法来提取嵌入另一个字符串中的字符串。这在你只需要字符串的一部分或验证用户输入时非常有用。例如，如果用户输入的第五到第九个字符应该是数字，你可以使用 `string.substring` 方法提取这些字符。假设我们有以下数据：`userEntry = "ABC12345"`；索引位置加上你想要的最后一个字符。如果你不指定值，将提取字符串的末尾。关于索引位置的说明，请参见第 96 页。

```
part = userEntry.substring(4,9);
```

使用 `substring` 方法时，如果起始位置大于结束位置，ActionScript 将返回空字符串。如果起始位置等于结束位置，ActionScript 将交换参数。ActionScript 提供了多种可以使用的方法来获取子字符串。

### 提取子字符串示例脚本

![](img/72fce958343eeb5d6d0322213ea85399_113_0.png)

- 1 选择你想执行 ActionScript 的帧、按钮或电影剪辑。
- 此示例使用了名为 `address` 的变量。
- 2 点击 `Window Actions` 打开 `Actions` 面板。
- 3 将字符串赋值给变量。

注意：此示例使用了可以在随书光盘找到的文件。

## 变量与字符串操作

### 应用

你也可以使用 `slice` 方法来获取子字符串。`slice` 方法使用此语法：
`stringVariable.slice(start, end);`

`start` 参数表示要提取的子字符串第一个字符的索引位置。`start` 为负数时，从字符串末尾计数。`end` 参数表示要提取的最后一个字符的索引位置。如果 `end` 为负数，计数从字符串末开始。

```
输入以下内容：
on (release) {
  nameAddress = "George Allen—153 Kings Way—Brooklyn NY";
  sampleText = nameAddress.slice(-24,11);
}
```

```
结果：
153 Kings Way
```

```
输入以下内容：
on (release) {
  nameAddress = "George Allen—153 Kings Way—Brooklyn NY";
  sampleText = nameAddress.slice(15,28);
}
```

```
结果：
153 Kings Way
```

![](img/72fce958343eeb5d6d0322213ea85399_114_0.png)

- 提取子字符串。
- 如果将变量与动态文本框关联，可以将返回的值显示给用户。
- 进入测试环境。
- ActionScript 提取子字符串并显示在屏幕上。

99

## FLASH SCRIPTING

## 拼接字符串

你可以使用 `string.concat` 方法将多个字符串连接成一个字符串。这在你需要包含用户输入的数据时非常有用。该方法会将它们相。在这里，字符串开头或结尾的空格也被视为字符串的一部分。

![](img/72fce958343eeb5d6d0322213ea85399_115_0.png)

- 1 选择你想执行 ActionScript 的帧、按钮或电影剪辑。
- 此示例使用了 `concat`。
- 2 点击 `Window Actions` 打开 `Actions` 面板。
- 3 将字符串赋值给变量。

## 变量与字符串的操作

### 运用

你可以使用 `+` 运算符来拼接字符串。后面的脚本提供了一个示例。变量 `sampleText` 是一个动态文本框。变量 `userEntry` 是一个输入文本框。当用户在 `userEntry` 字段中输入颜色并在点击按钮后释放鼠标时，输入的颜色将与变量 `phrase1` 和 `phrase2` 拼接。

```
TYPE THIS:
on(release) {
  phrase1 = "JUMP OVER THE ";
  phrase2 = "MOON";
  sampleText = phrase1 + userEntry + phrase2;
}
```

结果：
如果用户输入 PINK，结果如下。
JUMP OVER THE PINK MOON

![](img/72fce958343eeb5d6d0322213ea85399_116_0.png)

![](img/72fce958343eeb5d6d0322213ea85399_116_1.png)

- 拼接字符串。
- 如果你将变量与动态文本框关联，你就可以显示返回给用户的值。
- 如果你将变量与输入文本框关联，你就可以从用户处获取输入。
- 进入测试环境。

注意：查看第 38 页有关如何测试你的电影的说明。

- 输入单词或短语。
- 点击按钮。
- ActionScript 会拼接字符串。

## FLASH ACTIONSCRIPT

## 获取字符串的长度

你可以使用 `length` 属性来计算字符串中的字符数。该属性在验证输入时非常有用。例如，如果用户输入的值恰好是 10 个字符，你可以评估长度；如果输入多于或少于 10 个字符，向用户发送错误消息。

示例：

```
"Hello".length
```

在 4 中，`length` 函数用于获取字符串的长度。`length` 函数的语法为 `length(expression)`；使用表达式参数来指定想要获取长度的表达式或变量。

要使用 `length` 属性，只需在想要获取长度的字符串或变量后面跟上 `length` 单词即可。

示例：在下面的示例中，"S2498" 被赋值给变量 `studentID`。然后，使用 `length` 属性获取变量 `studentID` 的值。变量 `enteredLength` 返回 5。

示例：

```
studentID = S249876
enteredLength = length(studentID)
```
