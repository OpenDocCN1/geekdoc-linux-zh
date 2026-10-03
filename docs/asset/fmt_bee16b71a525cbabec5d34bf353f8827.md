
# The Project Trailblazer uses the MySQL database engine. See Documentation at http://www.mysql.com/

## 创建并测试 Project Trailblazer 数据库

可以使用以下步骤在 `tbdev1` 上创建并测试 Project Trailblazer 数据库：

1. 以 root 身份登录并从网站 www.embeddedlinuxinterfacing.com 下载 `trailblazerdbbuild.sql` 脚本：

```bash
root@tbdev1[503]: cd /root
root@tbdev1[504]: wget http://www.embeddedlinuxinterfacing.com/chapters/12/trailblazerdbbuild.sql
```

2. 使用 `trailblazerdbbuild.sql` 脚本创建 Project Trailblazer 数据库：

```bash
root@tbdev1[505]: mysql < trailblazerdbbuild.sql
```

3. 现在通过此命令执行简单的数据库查询，确定测试条目是否存在：

```bash
root@tbdev1[506]: echo "select * from temperatures;" | mysql trailblazer
timestamp location temperature
2001122900000 30 32
2001122940000 30 10
2001122980000 30 15
2001129120000 30 20
2001122916000 30 25
2001122920000 30 27
2001123000000 30 30
```

这显示数据库中包含了七个正确的测试温度。

4. 现在通过此命令执行多表内连接（inner joins）数据库查询：

```bash
root@tbdev1[508]: echo "select \
guests.first, guests.last, locations.description, accesses.timestamp \
from guests, guests.last, locations.description \
where guests.passID = accesses.passID and \
locations.location = accesses.location \
order by accesses.timestamp:" | mysql trailblazer
```

| first | last | description | timestamp |
| :--- | :--- | :--- | :--- |
| Melanie | Kline | Lift 1 Base | 200112271330031 |
| Robert | Cort | Lift 1 Base | 200112271330036 |
| John | Stephen | Lift 1 Base | 200112271330038 |
| Scott | Kidner | Lift 1 Base | 200112271330010 |
| Melanie | Kline | Lift 9 Base | 20011227134311 |
| Scott | Kidner | Lift 9 Base | 20011227134327 |
| John | Stephen | Lift 4 Base | 20011227135323 |
| Robert | Cort | Lift 4 Base | 20011227135354 |

该查询显示了四位客人访问了三部电梯，这也是正确的。

> **提示**
>
> 你可以使用 `mysqldump` 命令获取一个包含数据库定义和数据的文本文件。你可以使用此文件备份或重新创建数据库。`trailblazerdbbuild` 脚本是 `mysqldump` 输出文件的编辑版本。

## 开发目标和 CGI 集成脚本

创建 Project Trailblazer 数据库、填充测试数据并进行查询后，你就可以开始开发 Project Trailblazer 目标和 CGI 集成脚本了。

## 收集和发布温度数据

温度数据的收集和存储需要两个 bash 脚本：

- `temperatureReport`——列表 12.2 显示的收集脚本 `temperatureReport` 在目标板上持续执行，定期与外部温度传感器通信，然后通过 HTTP 连接报告温度值。目标板的 init 程序或启动脚本会启动 `temperatureReport` 脚本。
- `temperatureRecord`——列表 12.3 显示的数据库脚本 `temperatureRecord` 作为按需 CGI 脚本执行，接收温度值，然后向 Project Trailblazer 数据库发送格式化的数据库查询。

## 列表 12.2 temperatureReport 温度收集的 bash 脚本

```bash
#!/bin/bash
# temperatureReport v1.0 12/31/01
# www.embeddedlinuxinterfacing.com
#
# 此代码的原始位置位于
# http://www.embeddedlinuxinterfacing.com/chapters/12/
#
# 版权所有 (C) 2001 Craig Hollabaugh
#
# 此程序是免费软件；你可以随意重新分发和/或修改它。
#
# temperatureReport
# temperatureReport 是一个在目标板上执行的 bash 脚本，
# 该板加载了外部温度传感器及其模块。加载
# 模块（如第 10 章中的 LW70_x86.0）会创建
# /proc/trailblazer/temperature 文件。此脚本从 /proc/trailblazer/temperature
# 获取当前温度，使用 temperatureRecord 以温度作为参数
# 构建一个 HTTP GET 查询。此查询被传递到 nc 中，nc 与 tbdev1
# 上 80 端口的 apache HTTP 服务器有 TCP 连接。nc 配置了
# -w 标志，用于设置连接超时。如果 tbdev1 的 apache
# 服务器没有响应，此脚本将继续运行。
#
# 从 init 调用此脚本：
```

## 第 12 章 系统集成

创建 Project Trailblazer 数据库、填充测试数据并进行查询后，你就可以开发 Project Trailblazer 目标和 CGI 集成脚本。

## 收集和发布温度数据

温度数据的收集和存储需要两个 bash 脚本：

- `temperatureReport`——列表 12.2 显示的收集脚本 `temperatureReport` 在目标板上持续执行，定期与外部温度传感器通信，然后通过 HTTP 连接报告温度值。目标板的 init 程序或启动脚本会启动 `temperatureReport` 脚本。
- `temperatureRecord`——列表 12.3 显示的数据库脚本 `temperatureRecord` 作为按需 CGI 脚本执行，接收温度值，然后向 Project Trailblazer 数据库发送格式化的数据库查询。

## 列表 12.2 temperatureReport 温度收集的 bash 脚本

```bash
#!/bin/bash
# temperatureReport v1.0 12/31/01
# www.embeddedlinuxinterfacing.com
#
# 此代码的原始位置位于
# http://www.embeddedlinuxinterfacing.com/chapters/12/
#
# 版权所有 (C) 2001 Craig Hollabaugh
#
# 此程序是免费软件；你可以随意重新分发和/或修改它。
#
# temperatureReport
# temperatureReport 是一个在目标板上执行的 bash 脚本，
# 该板加载了外部温度传感器及其模块。加载
# 模块（如第 10 章中的 LW70_x86.0）会创建
# /proc/trailblazer/temperature 文件。此脚本从 /proc/trailblazer/temperature
# 获取当前温度，使用 temperatureRecord 以温度作为参数
# 构建一个 HTTP GET 查询。此查询被传递到 nc 中，nc 与 tbdev1
# 上 80 端口的 apache HTTP 服务器有 TCP 连接。nc 配置了
# -w 标志，用于设置连接超时。如果 tbdev1 的 apache
# 服务器没有响应，此脚本将继续运行。
```

## 开发目标和 CGI 集成脚本

### 列表 12.5 继续

```bash
# temperatureGetTable 是一个 CGI 脚本。Web 服务发送一个 HTTP
# 请求，并以 Trailblazer 位置号作为参数。
# Apache 调用此脚本并将 $QUERY_STRING 变量
# 设置为位置号。此脚本形成一个 SELECT 语句，
# 返回该位置的温度表。
# 此处是 Apache 要求的头部/内容之间的空分隔行
echo

# 设置位置
location=$QUERY_STRING

# 形成 SELECT 语句并传递给 mysql。
# 你必须以 trailblazer 用户和密码 tb 登录 mysql，
# 因为 apache 将以这种方式执行此脚本
echo "SELECT timestamp, temperature from temperatures where \location = $location order by timestamp asc;" | \
mysql trailblazer --user=trailblazer --pass=tb --silent
```

### 列表 12.6 temperatureGetPlot 温度分布的 bash 脚本

```bash
#!/bin/bash
# temperatureGetPlot v1.0 12/31/01
# www.embeddedlinuxinterfacing.com
# 此代码原始地址为
# http://www.embeddedlinuxinterfacing.com/chapters/12/
# 版权所有 (C) 2001 Craig Hollabaugh
# 本程序是免费软件；你可以随意重新分发和/或修改
# 它。
# temperatureGetPlot
# temperatureGetPlot 是一个 CGI 脚本。Web 服务发送一个 HTTP
# 请求，并以 Trailblazer 位置号作为参数。
# Apache 调用此脚本并将 $QUERY_STRING 变量
# 设置为位置号。此脚本形成一个 SELECT 语句，
# 返回该位置的记录温度表。
# 然后脚本调用 gnuplot 绘制这些温度，
# 创建并输出一个 png 图片。
#
# 此处是 Content-type 行，告诉浏览器该
# 回复是一个 png 图片。
echo Content-type: image/png

# 此处是 Apache 要求的头部/内容之间的空分隔行
echo

# 设置位置
location=$QUERY_STRING

# 形成 SELECT 语句并将其传递给 mysql。
# 你必须以 trailblazer 用户和密码 tb 登录 mysql，
# 因为 apache 将输出重定向到临时文件。
echo "SELECT timestamp, temperature from temperatures where \
location = $location order by timestamp asc;" | \
mysql trailblazer --user=trailblazer --pass=tb --silent > /tmp/tempdata
```

```bash
# 查询数据库获取位置描述以用于图表标题
echo "SELECT description from locations where \
location = $location" | \
mysql trailblazer --user=trailblazer --pass=tb --silent

# 执行 gnuplot，发送各种命令进行设置，然后绘制
# 来自临时数据文件中的温度。更多 gnuplot 信息
# 请访问 http://www.gnuplot.vt.edu/
/usr/bin/gnuplot << ENDINPUT
set terminal png color
set xdata time
set timefmt "%Y/%m/%d %H:%M"
set format "%m/%d\n%H:%M"
set nokey
set title "$locationendes (F)"
set ylabel "Temperature"
set xlabel "Date - Time"
set grid
set rmargin 5
plot "/tmp/tempdata" using 1:2 with linespoints
ENDINPUT
```

由于 Project Trailblazer 数据库是用测试数据生成的（参见列表 12.1），你可以测试 `temperatureGetLast`、`temperatureGetTable` 和 `temperatureGetPlot` 脚本。你可以使用以下命令在 `tbdev1` 上下载并测试这些脚本：

```bash
root@tbdev1[514]: cd /usr/lib/cgi-bin
root@tbdev1[515]: wget http://www.embeddedlinuxinterfacing.com/chapters/12/temperatureGetLast
root@tbdev1[516]: wget http://www.embeddedlinuxinterfacing.com/chapters/12/temperatureGetTable
root@tbdev1[517]: wget http://www.embeddedlinuxinterfacing.com/chapters/12/temperatureGetPlot
root@tbdev1[518]: chmod 755 /usr/lib/cgi-bin/temp*
root@tbdev1[519]: echo "GET /cgi-bin/temperatureGetLast?30" | nc 192.168.1.11 80
30
root@tbdev1[520]: echo "GET /cgi-bin/temperatureGetTable?30" | nc 192.168.1.11 80
2001122900000 32
20011229040000 10
20011229080000 15
20011229120000 20
20011229160000 25
20011229200000 27
20011230000000 30
```

你需要使用浏览器来测试 `temperatureGetPlot`，因为它返回的是一个 PNG 图表。在浏览器中输入此 URL：

http://192.168.1.11/cgi-bin/temperatureGetPlot?30

你应该能看到图 12.2 所示的图表。注意在该图中，你查询了位置 30（即 Lift 1 Base），`temperatureGetPlot` 脚本正确地生成了图表标题 Lift 1 Base Temperature。

## 图像数据的采集与分发

Project Trailblazer 的要求是在每个电梯底部和顶部进行图像采集，并在其他 20 个带有摄像头的目标处进行采集。在第 8 章“USB 接口”中解释的图像抓取软件 `vgrab` 会执行文本叠加操作，在图像上标记位置和时间戳。Project Trailblazer 的工程师希望使用这种叠加功能，但这需要对每个配备摄像头的目标板进行单独配置。例如，在 Lift 1 顶部目标板上执行的 bash 脚本将包含 "Lift 1 Top" 作为 `vgrab` 的叠加命令行参数。同样，在 Lift 2 顶部执行的脚本将包含 "Lift 2 Top"。

## 第 12 章 系统集成

### 列表 12.7 续

```bash
# image 命令还将包含一个 sleep 语句以暂停
# 主循环。
#
```

```bash
### 在 inittab 中 respawn 选项调用此程序，如
### T3:23:respawn:/usr/bin/imageReport
### 如果 imageReport 退出，init 将再次启动它
```

```bash
### 无限循环
while [ 1 ]
do
```

```bash
### 获取命令
imageCommand=`echo "GET /cgi-bin/imageGetCommand" | nc -w 10 192.168.1.11 80`
```

```bash
### 执行命令且不产生输出
eval $imageCommand > /dev/null 2>&1
```

```bash
done
```

### 列表 12.8 imageGetCommand bash CGI脚本

```bash
#!/bin/bash
# imageGetCommand v1.0 12/31/01
# www.embeddedlinuxinterfacing.com
#
```
