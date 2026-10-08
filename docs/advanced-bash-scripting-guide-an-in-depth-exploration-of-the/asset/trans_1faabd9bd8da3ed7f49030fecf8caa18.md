

## 高级 Bash 脚本指南

```bash
{
echo "Settings will be saved."
if [ ! -d $savePath ]; then # 检查目录是否存在
  mkdir $savePath # 创建用于保存内容的目录
fi # 如果它还不存在。
}
```

Flag=S
# 告诉最后一段代码执行什么。
# 设置一个标志位，因为工作在主函数中完成。

```bash
return

usage() # 告诉他们它是如何工作的。
echo "欢迎使用 wgetter。这是 wget 的前端界面。"
echo "它将始终使用这些选项运行 wget："
echo "--CommandA"
echo "--以及用于匹配的模式: $pattern \
(你可以在此脚本顶部更改它)。"
echo "--if 还将允许递归深度，\
并且如果你想使用引用页面。"
echo "--wget 接受以下选项:"
echo ""
echo "--help 显示此帮助信息。"
echo "--save 将命令保存到文件 $savePath/wget-$(date)\n 而不是直接运行。"
echo "--run 执行已保存的 wget 命令而不是启动新的 --"
echo "--interactive 以交互方式运行已保存的命令 --"
echo "--脚本将询问你文件名。"
echo "--cook 修改此会话的 cookies 文件。"
echo "--list 告诉我们从列表使用你的 URL 而不是 \
从命令行。"
echo "--swopt 将任何其他选项传递给 wget。"
echo ""
echo "查看 wget man 页面以获取可以 \
传递给 wget 的额外选项。"
echo ""
```

```bash
exit $E_USAGE # 在此结束。停止处理其他任何内容。
```

```
list_func() # 为用户提供在 wget 中使用 -i 选项的选项，
# 以及 URL 列表。

```bash
{
while [ 1 ]; do
echo "输入包含 URL 的文件名（按 q 改变主意）。"
read urlfile
if [ -e "$urlfile" ] && [ "$urlfile" != q ]; then
# 查找文件或退出选项。
echo "该文件不存在!"
elif [ "$urlfile" = q ]; then # 检查退出选项。
echo "不使用 URL 列表。"
return
else
echo "正在使用 $urlfile。"
}
}
```
```

附录 A. 贡献脚本

675

# 高级 Bash 脚本指南

```bash
echo "如果你在命令行上提供了 urls，我将优先使用它们。"
# 向用户报告 wget 的标准行为。
lister -i $urlfile # 这是我们想要传递给 wget 的。
return
fi
done
```

```bash
cookie_func() # 为用户提供使用不同 cookie 文件的选项。
{
while [ 1 ]; do
echo "更改 cookies 文件。如果你不想更改\
它，请按回车。"
read Cookies
# 注意：这与之前的 Cookie 不同。
# 末尾有一个 's'。
# 就像巧克力豆一样。
if [ -z "Cookies" ]; then # 胆小者的逃生语句
return
elif [ -e "Cookies" ]; then
echo "文件不存在。请重试。" # 继续…… . . .
else
CookiesOn=--local-cookies $Cookies # 文件良好，可以使用它！
return
}
done
```

```bash
run_func()
{
if [ -z "OPTARG" ]; then
# 测试我们是使用了内联选项还是查询选项。
if [ -d "$SavePath" ]; then # 如果目录不存在 . . .
echo "$SavePath 似乎不存在。"
echo "请提供保存的 wget 命令的路径和文件名："
read newFile
until [ -f "$newFile" ]; do # 继续直到我们获得某些。
echo "抱歉，文件不存在。请重试。"
# 尽力获取某些东西。
read newFile
done
```

```bash
if [ -z $( grep wget ${newFile} ) ]; then
# 假设他们没有获得正确的文件并退出。
echo "抱歉，该文件不包含 wget 命令。正在中止。"
exit
fi
# 这是一个无效代码。
# 它实际上不起作用。
# 如果有人想修复它，请尽管去尝试！
```

```bash
filePath="${newFile}"
else
echo "保存路径为 $SavePath"
```

附录 A. 贡献脚本

# 高级 Bash 脚本指南

```bash
echo "请输入你想要使用的文件名。"
echo "你有一个选择："
ls $savePath # 给他们一个选择。
read inFile
until [ -f "${savePath}/${inFile}" ]; do # 继续直到
    +# 我们获得某些。
if [ ! -f "${savePath}/${inFile}" ]; then # 如果文件不存在
echo "抱歉，文件不存在。请从以下中选择："
ls $savePath
read inFile
fi # 如果犯了错。
done
filePath="${savePath}/${inFile}" # 创建一个变量 ...
fi
else elsePath="${savePath}/${OPTARG}" # 可能是许多东西

if [ ! -f "${filePath}" ]; then # 无的文件通过了
echo "你没有指定合适的文件。"
echo "先用 -save 选项运行此脚本。"
echo "中止。"
exit $NO_SAVEFILE
fi
echo "使用：${filePath}"
while read; do
    eval REPLY
echo "完成：${REPLY}" # 将我们使用的实际文件馈入循环循环。
done
```

提取提取脚本使用的任何选项。
基于《The Bash Shell》(O'Reilly)。
while getopts ":save:cookie$helplist$run:inpu$wopt" opt
do

```bash
case $opt in
    save) save_func;) # 保存我们的会话以备后用。
    cookie_func;) # 更改 cookie 文件。
    usage) # 获取帮助。
    list_func;) # 允许使用 URL 列表。
    run) run_func;) # 如果我们从 cron 脚本调用 wget 则有用。
    inpu) run_func;) # 当你不知道文件名时。
    wopt) wopts;) # 将选项直接传递给 wget
    \?) echo "不是有效选项。"
    echo "使用 -${wopt} 直接传递选项给 wget"
    echo "或使用 -${help} 获取帮助"; # 捕捉任何其他内容。
esac
```

```bash
done
shift $((OPTIND - 1)) # 对进行神奇魔法操作
```

