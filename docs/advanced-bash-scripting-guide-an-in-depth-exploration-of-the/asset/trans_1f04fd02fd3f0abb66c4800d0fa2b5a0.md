
# 附录 T. ASCII 表

通常，这类书籍会有一个 ASCII 表附录。这本书没有。相反，这里有几个短脚本，每个脚本都能生成完整的 ASCII 表。

示例 T-1. 一个生成 ASCII 表的脚本

```bash
#!/bin/bash
# ascii.sh
# ver. 0.2, reldate 26 Aug 2008
# 由 ABS Guide 作者修改。

# 原始脚本来自 Sebastian Arming。
# 经许可使用（感谢！）。

exec >ASCII.txt          # 将标准输出保存到文件，
# 如示例脚本中的 +
# reassignment-stdout.sh 和 upperconv.sh。

MAXNUM=256
COLUMNS=5
OCT=64
OCTSUQ=4
LITTLESPACE=-3
BIGSPACE=-5

i=1 # 十进制计数器
o=1 # 进制计数器

while [ "$i -lt "$MAXNUM" ]; do # 我们不需要数到 400 进制。
  paddi="$i"
  echo -n "$paddi: $BIGSPACE"    # 列间距。
  padddo="000$"
  echo -ne "\$paddo: $LITTLESPACE"    # 原始。
  echo -ne "\$paddo: $LITTLESPACE"    # 修复。

  echo -n ""
  if (( i % $COLUMNS == 0 )); then # 换行。
    echo
  fi
  ((i++,o++))
  # 8 的进制表示为 10，十进制 64 是 100。
  (( i % $OCT == 0 )) && ((o+=2))
  (( i % $OCTSUQ == 0 )) && ((o+=20))
done

exit $
# 将此脚本与 "pr-asc.sh" 示例对比。
# 这个处理“不可打印”字符。

练习：
# 重写此脚本使用十进制而不是八进制。
```

示例 T-2. 另一个 ASCII 表脚本

```bash
#!/bin/bash
```

附录 T. ASCII 表

# 高级 Bash 脚本指南

```bash
# 脚本作者：Joseph Steinhauser
# 由 ABS Guide 作者稍作编辑，但未注释。
# 经许可在 ABS Guide 中使用。
#-
# 文件：ascii.sh      打印 ASCII 表，10/8/16 进制 (JETS-2012)
# 用法：ascii [oct|dec|hex|8|10|16]
#-
# 此脚本打印从 到 127 的 ASCII 码摘要。
# 数值可以以十进制、八进制或十六进制（Base16）打印。
#-
# 格式基于：/usr/share/lib/pub/ascii，以十进制为默认。
# 更多细节，请 man ascii ...#-
[ -n "BASH_VERSION" ] && shopt extglob
case "$1" in
oct|([Oo])([Cc]|[Tt]))  Obase=Octal;      Numy=30;
hex|([Hh])([Ee])|16([Xx])) Obase=Hex;       Numy=2X;
help|([Hh]))                    sed -n '/2,/\*$/p' $0;exit;
code|([Cc])([Dd]|[Ee]))      sed -n '/case,$/' $0;exit;
*) Obase=Decimal
nesac # CODE 实际上比图表短！
printf "%t\t\b $ASCII Chart \%s\n" $1="%%0${Numy:-3d}" LD=1-
AB=nul shh stx etx enq aec bc bs tal nt vp cr so si dle"
Ad=dcl2 dc3 dcl4 n3k syn deb em sub fs gs rs us dpr"

for TOK in $AB $AD; do ASCII[$((TOK+1))]=$TOK; done
ABRI[127]=del

IDX=0
while [ $IDX -le 127 ]; do CHR="${ABRI[$IDX]}"
do (( ${CHR} )) && FM2="%%-3s\|" && FM2=printf "\\%o" "$IDX"
printf "%%$FM1 $FM2" "$IDX" $CHR; ((IDX+1)%8))|echo ''
done
exit $
```

# 示例 T-3. 使用 awk 的第三个 ASCII 脚本

```bash
#!/bin/bash
# ASCII 表，使用 awk。
# 作者：Joseph Steinhauser
# 经许可在 ABS Guide 中使用。
#-
# 文件：ascii.sh               打印 ASCII 表，10/8/16 进制 (JETS-2010)
# 用法：ascii [oct|dec|hex|8|10|16]
#-
# 此脚本打印从 到 127 的 ASCII 码摘要。
# 数值可以以十进制、八进制或十六进制（Base16）打印。
#-
# 格式基于：/usr/share/lib/pub/ascii，以十进制为默认。
# 更多细节，请 man ascii
```bash
[ -n "$BASH_VERSION" ] && shopt extglob

case "$1" in
  octal|([Oo])([Cc]|[Tt])) Obase=Octal    Numy=30;
  hex|([Hh])([Ee])|16([Xx])) Obase=Hex    Numy=2X;
  help|([Hh]))()                     sed -n '/2,/\*$/p' $0;exit;
... (此处省略代码逻辑重复部分，翻译已保持格式一致)
```
