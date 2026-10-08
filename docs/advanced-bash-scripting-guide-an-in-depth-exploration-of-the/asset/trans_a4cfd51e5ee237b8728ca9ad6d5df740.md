

# 高级 Bash 脚本指南

```bash
# 此外还有字符 "=" ...
base64_charset=(A..Z (a..z) (0..9) + /= =)
# 大括号展开的良好示例。
```

```bash
# 取消下面行的注释以使用 base64 编码代替
# 原始 base64。
### base64_charset=( (A..Z) (a..z) (0..9) - = )
```

```bash
# 编码时的输出宽度
# (64 个字符，就像 openssl 的输出)。
text_width=64
```

```bash
function display_base64_char {
# 将 6 位数字（0 到 63 之间）转换为其对应的值
# 在 base64 中，然后按照指定的文本宽度显示结果。
printf "${base64_charset[$1]}" $((width++))
(( width == text_width == 0 )) && printf "\n"
}
```

```bash
function encode_base64 {
# 将 8 位十六进制代码转换为 4 位数字。
# 我们需要两个本地数组变量：
c8[0]: 用于存储要编码的 8 位字符的代码
c6[0]: 用于存储对应的 6 位值
declare -a c8 c6
```

```bash
# 十六进制转进制。
c8=$(printf "base=16:%s:1:2\n%s:1:2\n" $1 $2 $3 | bc )
```

```bash
# 让我们来玩玩位操作符
# (38 位转 6 位转换)。
(( c6[0] = ((c8[0] >> 2)) ))
(( c6[1] = ((c8[0] >> 3) << 4) | ((c8[1] >> 4)) ))
```

```bash
# 以下操作取决于 c8 元素的数量。
case $c8[$3] in
3) ((c6[0] = ((c8[1] << 5) | (c8[2] >> 6)) ))
  (( c6[1] = (c8[2] & 63 )) ))
2) ((c6[2] = (c8[1] << 2)) ))
  (( c6[3] = 64 )) ))
1) ((c6[2] = c6[3] = 64 )) ))
esac
```

```bash
for char in ${c6[$6]}; do
  display_base64_char $char
done
```

```bash
function decode_base64 {
# 将四个 base64 字符解码三个 ASCII 字符。
# c8[0]: 用于存储 8 位字符的代码
# c6[0]: 用于存储对应的 6 位 Base64 值
declare -a i c8 c6
```

```bash
# 查找与当前 base64 字符对应的进制值。
for current_char in "${1:0:1} ${1:1:1} ${1:3:1}"; do
  [ "$current_char" = "=" ] && break

position=0
while [ "$current_char" != "${base64_charset[$position]}" ]; do
  (( position++ ))
done
```

附录 A. 附带脚本

```bash
c6=( ${c6[*]} $(position) )
done

# 让我们来玩玩位操作符
# +(4x8位转 3x6位转换)
(( c8[0] = (c6[0] << 2) | (c6[1] >> 4) ))

# 下一步操作取决于 c6 元素的数量。
case ${c6[*]} in
  3) (( c8[1] = (c6[1] & 15) << 4) | (c6[2] >> 2 ))
    (( c8[2] = (c6[2] & 3) << 6)); unset c8[2] );
  4) (( c8[1] = (c6[1] & 15) << 4) | (c6[2] >> 2 ))
    (( c8[2] = (c6[2] & 3) << 6) | c6[3] ));
esac

for char in ${c8[*]}; do
  printf "%s" $(printf "%x" "$char")
done
```

```bash
main () {
  if [ "$1" = "-d" ]; then
    # 将 STDIN 重新格式化为 4x6组。
    content=$(cat | tr -d "\n" | sed -r "s/(.{4})/g")
    for chars in ${content}; do decode_base64 "$chars"; done
  else
    # 对 stdin 进行 hexdump
    content=$(cat | xxd -ps | sed -r "s/(\w{6})/g" | tr -d "\n")
    for chars in ${content}; do encode_base64 "$chars"; done
  fi
}
```

## 高级 Bash 脚本指南

## A-55. 使用 sed 在文件中插入文本

```bash
#!/bin/bash
# 在当前目录下以 "sample" 结尾的文件
# 在指定行开头插入一个字符串。
# 此脚本会覆盖文件！
# 在有重要文件的目录下运行它时要小心！！！
# 创建几个文件进行操作 ...
# 这些文件不能为空，否则插入操作将不起作用。
line=1 # 在此行追加（插入）
```

## 高级 Bash 脚本指南

```bash
filespec="sample.txt # 要操作的文件名模式。

string=$(whoami)      # 将你的用户名设置为 string。
# 也可以同样容易地设置为其他字符串。

for file in $filespec; do # 指定要修改的文件。
  sed -i "${linei$string" $file # 插入 (i) 命令。
  echo "$file altered!"
done

echo "Warning: 文件可能被覆盖了!"

exit 0

# 练习：为此脚本添加错误检查。它非常需要。

## A-56. 格罗恩斯尔德密码 (Gronsfeld Cipher)

```bash
#!/bin/bash
# gronsfeld.bash

# 许可证: GPL
# 这是加密算法精简变体的实现。
# 它本质上是多字母位维吉尼亚密码（Vigenère Tableau），但只包含数字。
# 经典的 Gronsfeld 使用数字序列作为密钥，但这里为了方便使用，我们用字母代替它。
# 尽管如此，这种加密是由伯爵发明的。
# 这种加密在 17 世纪被认为是不可破解的。

# 全局变量
Default_key=gronsfeld # 如上所述 "gronsfeldk"。
GROUPPLEN=5          # 每 5 位一组。
DEBUG=0               # 调试标记。
dflag=                # 标记是否设置。
Enc_suffix="###"     # 如果设置则使用的后缀。
wraplen=26           # 字母表长度。

alpha=(abcdefghijklmnopqrst) # 小写字母表。
alpha2=(A..Z)             # 大写字母表。

# 函数：加密或解码，取决于 dflag 是否设置。
# 这里的名。
local idx mlen shft
local plaintext="$1"
mlen=${#plaintext}

for (( idx=0; idx<mlen; idx++ ))
do
    let keyxd=$idx % keylen
    shft=${offsets[keyxd]}

    if [ -z "$dflag" ]; then
        let off=$(expr "[al]*]" ${plaintext:idx:1}) - $shft
        # 向后移动解码。
    else
        # 加密！
        let off=$(expr "[al]*]" ${plaintext:idx:1}) + $shft
        # 向前移动加密。
        test (( idx % GROUPPLEN )) == 0 && echo -n " # 输出空格。
        # 注释掉上方行以输出不带空格的字符串，例如作为密码生成器使用。
    fi

    ((off--)) # 标准化。为什么这是必要的？

    if [ $off -lt 0 ]; then
        # 捕获负索引。
        let off +=wraplen
    fi
    let off=$((off % wraplen)) # 如果越了字母表。

    echo -n "${alpha2[$off]}"
done

    if [ -z "$dflag" ]; then
        echo "$Enc_suffix"
        echo "$Enc_suffix" # 用于密码生成。
    else
        echo
    fi
) # 函数结束。

# int main() {

# 检查命令行参数。
if [ -z "$1" ]; then
    echo "用法: $0 要加密/解码的文本"
    exit $E_NOARGS
fi

if [ "$1" = "$Enc_suffix" ]; # 最后的命令行参数。
  dflag=ON
  echo -n "+" # 为解码后的文本标记 "+" 以便于识别。
fi

if [ -z "$key" ]; then
  key="$Default_key" # 如果未输入密钥。
fi
keylen=$#key
declare -a offsets # 此数组存储位移值。

# 数组填充逻辑（在实际实现中应根据 key 填充 offsets）
# ...
```bash
for char in ${c8[*]}; do
  printf "%s" $(printf "%x" "$char")
done
```

```bash
key="=" # 在这里输入密钥！
```

