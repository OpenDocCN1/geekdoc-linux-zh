
图 30.23 | `replaceFirst`, `replaceAll` 和 `split` 方法。（第1 部分，共 2 部分）。

## 30.7 正则表达式、`Pattern` 类和 `Matcher` 类 1481

原始字符串 1: This sentence ends in 5 stars *****
`^` substituted for: This sentence ends in 5 stars AAAAA
`^` carets substituted for "stars": This sentence ends in 5 carrets AAAAA
Every word replaced by "word": word word word word AAAAA

原始字符串 2: 1, 2, 3, 4, 5, 6, 7
First 3 digits replaced by "digit": digit, digit, digit, 4, 5, 6, 7, 8
String split at: ["digit", "digit", "digit", "4", "6", "7", "8"]

**图 30.23** `replaceFirst`, `replaceAll` 和 `split` 方法。（第2 部分）

那一个正则表达式应该匹配前一个模式的任意次数出现。然而，在第 14 行中，我们找到了字面字符 `*` 的所有出现次数——为了做到这一点，我们必须用 `\*` 转义字符。使用 `\` 转义特殊的正则表达式字符可以使匹配引擎找到实际的字符。由于该表达式存储在 Java 字符串中，而 `\` 是 Java 字符串中的特殊字符，因此我们必须包含一个额外的 `\`。因此，字符串 `"\\*"` 代表正则表达式模式 `\*`，它匹配搜索字符串中的单个字符。在第 19 行中，`first` 中正则表达式 `"stars"` 的每个匹配项都被替换为 `"carets"`，

`replaceFirst` 方法（第 32 行）替换模式匹配的第一次出现。Java 字符串是不可变的，因此 `replaceFirst` 返回一个已替换相应字符的新字符串。这一行获取原始字符串并通过 `replaceFirst` 返回它。通过迭代三次，我们将 `secondString` 中前三个数字（`d`）的实例替换为文本 `"digit"`。

`split` 方法将字符串划分为多个子字符串。原始字符串在任何匹配指定正则表达式的地方被断开。`split` 方法返回一个字符串数组，其中包含正则表达式匹配项的子字符串。在第 38 行中，我们使用 `split` 方法对一个逗号分隔的整数字符串进行分词。参数是正则表达式 `,\s*`，用于在出现逗号的地方分隔子字符串。通过匹配任何空白字符，我们消除了结果子字符串中的额外空格。注意，逗号和空白字符 `\s*` 不会作为子字符串的一部分返回。再次注意，Java 字符串 `,\s*` 代表正则表达式 `,\s*`。

### Pattern 和 Matcher 类

除了 `String` 类的正则表达式功能外，Java 还提供了 `java.util.regex` 包中的其他类来帮助开发和管理正则表达式。`Pattern` 类表示一个正则表达式。`Matcher` 类包含正则表达式模式以及用于搜索该模式的 `CharSequence`。

`CharSequence` 是一个接口，允许对字符序列进行读取访问。该接口要求声明 `charAt`、`length`、`subSequence` 和 `toString` 方法。`String` 和 `StringBuilder` 都实现了 `CharSequence` 接口，因此这些类的任何实例都可以与 `Matcher` 使用。

### 常见编程错误 30.4

正则表达式可以针对实现 `CharSequence` 接口的任意类对象，但正则表达式必须是 `String`。尝试创建一个是一个错误。

![img/1526]

如果正则表达式只使用一次，可以使用静态 `Pattern.matches`。此方法接收一个指定正则表达式的字符串和一个用于执行匹配的 `CharSequence`。该方法返回一个布尔值，表示搜索对象（第二个参数）是否匹配正则表达式。

如果正则表达式使用多次，则使用静态 `Pattern.compile` 方法来为正则表达式创建一个 `Pattern` 对象会更有效。此方法接收一个表示模式的字符串并返回一个新的 `Pattern` 对象，该对象可以用于调用 `matcher` 方法。该方法返回一个用于搜索的 `CharSequence` 并返回一个 `Matcher` 对象。

`Matcher` 提供了 `matches` 方法，它执行与 `Pattern` 方法相同的任务，但不接收参数——模式和搜索对象被封装在 `Matcher` 对象中。`Matcher` 类提供了其他方法：`find`、`lookingAt`、`replaceFirst` 和 `replaceAll`。

图 30.24 展示了一个使用表达式的简单示例。该表达式匹配不在 4 月的生日以及名字以 "J" 开头的人。

第 11-12 行通过调用静态 `Pattern.compile` 方法创建一个 `Pattern`。代码字符 `.` 在正则表达式（第 12 行）中匹配除换行符以外的单个字符。

```java
// RegexMatches.java

// 展示 Pattern 类和 Matcher 类。

import java.util.regex.Matcher;

import java.util.regex.Pattern;

public class RegexMatches {

    // 创建正则表达式

    Pattern expression =

    Pattern.compile("J.*\\d[0-35-9]-\\\d-\\\d-\\\d");

    String string1 = "Jane's Birthday is 05-12-1990" +

        "Dave's Birthday is 04-28-1985" +

        "John's Birthday is 11-15-1978" +

        "Joe's Birthday is 06-20-1993";

    public static void main(String[] args) {

        Matcher matcher = expression.matcher(string1);

        while (matcher.find()) {

            System.out.println(matcher.group());

        }

    } // end main

} // end class
```
