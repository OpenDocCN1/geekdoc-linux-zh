
### Listing 7-14: The moviedata script

#### How It Works

This script builds a different URL depending on whether the command argument specified is a film title or an IMDb ID number. If the user specifies a title by ID number, the script builds the appropriate URL, downloads it, saves the lynx output to the `$tempout` file ⑧, and finally calls `summarize_film()` ⑩. Not too difficult.

But if the user specifies a title, then the script builds a URL for a search query on IMDb and saves the results page to the temp file. If IMDb can't find a match, then the `<h2>` tag with class="findHeader" value in the returned HTML will say No results. That's what the invocation at ⑨ checks. Then the test is easy: if `$fail` is not zero length, the script can report that no results were found.

如果结果长度为零，则意味着 `$tempfile` 现在包含了用户模式的一个或多个成功搜索结果。可以通过在源中以 `/title/tt` 作为模式进行搜索来提取所有这些结果，但有一个需要注意的地方：IMDb 并没有让解析结果变得容易，因为任何给定的标题链接都有多个匹配项。剩下的那个复杂的 `sed | grep | sed` 序列试图识别并删除重复的匹配项，同时仍保留重要的匹配项。

此外，当 IMDb 有像 "Lawrence of Arabia (1962)" 这样的匹配时，标题和年份在结果中实际上是两个不同的 HTML 元素，位于两行不同。唉。我们需要年份来区分同名但发行年份不同的电影。这就是 ④ 处的 `awk` 语句所做的，以一种棘手的方式。

如果你不熟悉 `awk`，`awk` 脚本的一般格式是 `(condition) { action }`。这一行将奇数行保存到 `$title` 中，然后在偶数行（年份和匹配类型数据）上，它将前一行和当前行的数据作为一行输出。

#### 运行脚本

尽管简短，但该脚本对输入格式非常灵活，如清单 7-15 所示。你可以用引号指定电影标题或作为单独的词，然后可以指定八位 IMDb ID 值来选择特定的匹配项。

#### 结果

```
$ moviedata lawrence of arabia

0056172: Lawrence of Arabia (1962)

0245226: Lawrence of Arabia (1935)

0390742: Mighty Moments from World History (1985) (TV Series)

1471868: Mystery Files (2010) (TV Series)

1471868: Mystery Files (2010) (TV Series)

1478071: Lawrence of Arabia (1985) (TV Episode)

1942509: Lawrence of Arabia (TV Episode)

1952822: Lawrence of Arabia (2011) (TV Episode)

$ moviedata 0056172

Lawrence of Arabia (1962)

  A flamboyant and controversial British military figure and his

  conflicted loyalties during his World War I service in the Middle East.
```

清单 7-15：运行 `moviedata` 脚本

### hack 脚本

对该脚本最明显的 hack 就是去掉输出中的丑陋 IMDb 电影 ID 号码。隐藏电影 ID 是很直接的（因为显示的 ID 既不友好又容易输错），并且让 shell 脚本输出一个带有唯一索引值的简单菜单，然后可以输入该索引值来选择特定电影。

```
#!/bin/sh

# Deal with all non-conversion requests.

if [ $# -ne 4 ] ; then

if [ "$1" = "list" ] ; then

# Produce a listing of all currency symbols known by the converter.

echo "List of supported currencies:"

echo "$currencies"

fi

exit 0

fi

if [ "$1" = "to" ] ; then

echo "Usage: $basename $0 value currency TO currency"

echo "(use \'$basename $0 list\' to get a list of all currency values)"

exit 0

fi

amount=$1

basecurrency="$(echo $2 | tr '[:lower:]' '[:upper:]')"

targetcurrency="$(echo $4 | tr '[:lower:]' '[:upper:]')"

# And let's do it--finally!

$lynx -source "url?amount=$amount&from=$basecurrency&to=$targetcurrency" | \
grep -id currency_converter_result | sed 's/<[^>]*>//g'

exit 0
```

清单 7-16：`convertcurrency` 脚本

Google 货币转换器有三个通过 URL 本身传递的参数：金额、原始货币和要转换成的货币。你可以在以下将 100 美元兑换成墨西哥比索的请求中看到这一点。

`https://www.google.com/finance/converter?a=100&from=USD&to=MXN`

因此，在最基本的使用情况下，脚本期望用户将这三个基本字段作为参数指定，然后全部传递给 Google 的 URL。

脚本还包含一些使用信息，使其使用起来更容易。要查看这些信息，让我们直接跳到演示部分吧？

该脚本设计为易于使用，如清单 7-17 所述，尽管对至少几个国家的货币有基本了解是有益的。

#### 结果

```
$ convertcurrency

Usage: convert amount currency to currency

Most common currencies are CAD, CNY, EUR, USD, INR, JPY, and MXN

Use "convertcurrency list" for a list of supported currencies.

$ convertcurrency list | head -10

List of supported currencies:

AED United Arab Emirates Dirham

AFN Afghan Afghani

ALL Albanian Lek

AMD Armenian Dram

ANG Netherlands Antillean Guilder

AOA Angolan Kwanza

ARS Argentine Peso

AUD Australian Dollar

AWG Aruban Florin

$ convertcurrency 75 eur to usd

75 EUR = 84.5132 USD
```
