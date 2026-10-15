
```bash
#!/bin/bash
# githubuser-- 获取一个 GitHub 用户名，提取关于该用户的信息

if [ $ -ne 1 ]; then
echo "Usage: $0 <username>"
exit 1
fi
```

```bash
# -s 选项静默 curl 通常的详细输出。
curl "https://api.github.com/users/$1" | \
awk -F\""": {
  \"name\":{\n
    print "$4" is the name of the GitHub user.
  }
  \"followers\":{\n
    split($3, a, " ")
    sub(/\",, "", a[2])
    print "They have \a[2] followers."
  }
  \"following\":{\n
    split($3, a, " ")
    sub(/\",, "", a[2])
    print "They are following \a[2] other users."
  }
  \"created_at\":{\n
    print "Their account was created on \$4."
  }
}
exit 0
```

列表 7-6: `githubuser` 脚本

## 工作原理

诚然，这与其说是一个 `bash` 脚本，不如说是 `awk` 脚本，但有时你需要 `awk` 提供的额外火力来解析（GitHub API 返回的是 JSON）。我们使用 `curl` 获取 JSON，然后使用 `awk` 进行进行解析。脚本使用字段分隔符从 JSON 中提取所需信息。

调用脚本的标准方式是在命令行中指定邮政编码。如果该编码有效，将显示城市和州，如列表 7-7 所示。

## 结果

```
$ githubuser username
John Doe is the name of the GitHub user.
They have 123 followers.
They are following 45 other users.
Their account was created on 2021-01-01.
```

## 代码

```bash
#!/bin/bash
```

# `arecode`--给定一个三位美国电话区号，通过 Bennett Yee 网站上的

# 简单表格数据来识别城市和州份。

`source="http://www.bennettee.org/ucsd-pages/area.html"`

```bash
if [ -z "$1" ]; then
echo "usage: arecode <three-digit US telephone area code>"
exit 1
fi
```

```bash
# wc -返回字符数 +换行符，所以 3 位数字 = 4 个字符
if [ "$(echo $1 | wc -c)" -ne 4 ]; then
echo "arecode: wrong length: only works with three-digit US area codes"
exit 1
fi
```

```bash
# 都是数字吗？
if [ -z "$(echo $1 | sed 's/[[:digit:]]//g')" ]; then
echo "arecode: not-digits: area codes can only be made up of digits" (区号只能由数字组成)
exit 1
fi
```

```bash
# 现在，最后，让我们查询该区号。
```

```bash
result="$(curl -s -dump $source | grep name="\$1" | \
sed 's/<[^>]*>//g' | \
cut -f2 -d| | cut -f1 -d())"
```

```bash
echo Area code $1 = $result
```

```bash
exit 0
```

列表 7-10：`arecode` 脚本

## 工作原理

此 `shell` 脚本中的代码主要用于输入验证，确保用户提供的数据是有效的区号。脚本的核心是 `curl`，它的输出通过管道交给 `sed` 进行清理，然后用 `cut` 裁剪成我们要显示给用户的内容。

## 运行脚本

该脚本接受一个参数，即要查询信息的区号。列表 7-11 给出了脚本使用的示例。

## 结果

```bash
$ areacode 817
Area code 817 = N Cent. Texas: Fort Worth area (德克斯州中部：沃特沃斯地区)
$ areacode 512
Area code 512 = S Texas: Austin (德克斯州南部：奥斯汀)
$ areacode 903
Area code 903 = NE Texas: Tyler (德克斯州东北部：泰勒)
```

列表 7-11：测试 `arecode` 脚本

# 破解脚本

简单的破解方法是反转代码，使得你提供一个州和城市，然后脚本打印出该城市所有的区号。

# #58 追踪天气

整天坐在办公室或服务器机室内，鼻子对着终端，会让你渴望去室外，尤其是当天气非常好的时候。Weather Underground (`http://www.wunderground.com/`) 是一个很棒的网站，如果你注册 API 密钥，它实际上为开发者提供免费的 API。有了 API 密钥，我们可以编写一个快速的 `shell` 脚本（见列表 7-12）来告诉我们外面天气有多好（多糟）。然后我们就可以决定出去散步是否真的是个好主意。

## 代码

```bash
#!/bin/bash
# weather--使用 Underground API 获取指定邮政编码的天的天气

if [ $# -ne 1 ]; then
  echo "Usage: $0 <zip>"
  exit 1
fi
apikey="b03fdsaf3b2e7cd23" # 不是免费 API 密钥--你需要自己的。

curl -s \
  "https://api.wunderground.com/api/$apikey/conditions/q/$1.xml" > weather
state=$(xmlint --xpath \
  "//response/current_observation/display_location/text()[1]" \
  < weather)
zip=$(xmlint --xpath \
  "//response/current_observation/display_location/zip()[1]" \
  < weather)
current=$(xmlint --xpath \
  "//response/current_observation/temp_f/text()[1]" \
  < weather)
```

```bash
condition=`xmlint --xpath \
//response/current_observation/text()[1]` \
< weather)

echo "$state" "$zip" : Current temp "$current"F and "$condition" outside.
```

```
exit 0

列表 7-12：天气脚本

## 工作原理

在这个脚本中，我们使用 `curl` 调用 Wunderground API，并将 HTTP 响应数据保存到 `weather` 变量中。我们随后使用 `xmlint`（通过你喜爱的包管理器如 `apt`、`yum` 或 `brew` 安装）对返回的数据执行 XPath 查询。在调用 `xmlint` 时使用 `<echo $weather>` 的时候，我们还使用了一种有趣的语法。这种语法获取内部命令的输出并将其作为文件描述符传递给命令，程序认为它正在读取一个真实的文件。从返回的 XML 中收集所有相关信息后，我们打印一条带有通用天气统计的友好消息。

## 运行脚本

当执行调用脚本时，只需指定所需的邮政编码，如列表 7-13 所示。非常简单！

## 结果

```bash

$ weather 78727

Austin, TX (78727) : Current temp 59.0F and Clear outside.

$ weather 80304

Boulder, CO (80304) : Current temp 59.2F and Clear outside.

$ weather 10010

New York, NY (10010) : Current temp 68.7F and Clear outside.
```
