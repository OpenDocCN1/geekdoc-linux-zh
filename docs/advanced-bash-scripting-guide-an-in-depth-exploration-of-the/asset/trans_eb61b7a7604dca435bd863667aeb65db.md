

# 高级 Bash 脚本指南

-f 和 -u 命令的默认路径名为 $CDPath
-f 和 -u 命令的默认文件名为 $CDFile

设置以下环境变量：
CDL_PROMPTLEN - 设置为你所需要的提示符长度。
提示符字符串设置为当前目录的右侧字符。
如果未设置，则提示符保持不变。
CDL_PROMPT_PRE - 设置为提示符的前缀字符串。
默认值为：
非 root 用户："\\[001;34m\]"（设置为蓝色）
root 用户："\\[001;31m\]"（设置为红色）。
CDL_PROMPT_POST - 设置为提示符的后缀字符串。
默认值为：
非 root 用户："\\[00m\]"（重置颜色并显示 $)
root 用户："\\[00m\]"（重置颜色并显示 #）
CDPath - 设置 -f & -u 选项的默认路径。
默认值为家目录。
CDFile - 设置 -f & -u 选项的默认文件名。
默认值为 cdfile

```
cd_version

cd_version () {
    printf "Version: ${VERSION_MAJOR}.${VERSION_MINOR} Date: ${VERSION_DATE}\n"
}

# 右侧截断。
#
# 参数：
# p1 字符串
# p2 截断到的长度
#
# 返回在 tcd 中的字符串
cd_right_trunc () {
    local tlen=$2
    local plen=$1
    local str="${1}"
    local diff
    local filler="<--"
    if [ ${plen} -le ${tlen} ]; then
        tcd="${str}"
    else
        let diff=$(${plen}-${tlen})
        let len=3
        if [ ${diff} -le 2 ]; then
            let len=$(${diff})
        fi
        tlen=$(${tlen})
        let tlen=$(${tlen}+${len})
        tcd="${str:0:len}${filler}${str:tlen}"
    fi}
```

附录 A 贡献脚本

```
fi
}

# 三版本的历史记录命令：
# cd_distory - 将历史记录和特殊项并排显示
# cd_distoryH - 只显示历史记录
# cd_distoryS - 只显示特殊项
```

```
cd_distory ()
{
    cd_getrc
    printf "History:\n"
    local -i count=${cd_histcount}
    while [${TEST} ${count} -ge 0 ];
    do
        cd_right_trunc "${CD[count]}" ${cd_lchar}
        printf "%2d -${cd_lchar}s " ${count} "${tcd}"
        
        cd_right_trunc "${CD[count]}" ${cd_rchar}
        printf "%s%d -${cd_rchar}.${cd_rchar}\n" ${count} "${tcd}"
        count=$((count-1))
    done
}
```

```
cd_distoryH ()
{
    cd_getrc
    printf "History:\n"
    local -i count=${cd_maxhistory}
    while [${TEST} ${count} -ge 0 ];
    do
        printf "%s -${count} -${cd_flchar}.${cd_flchar}\n" ${CD[count]}
        count=$((count-1))
    done
}
```

```
cd_distoryS ()
{
    cd_getrc
    printf "Specials:\n"
    local -i count=${cd_maxspecial}
    while [${TEST} ${count} -ge 0 ];
    do
        printf "%s -${count} -${cd_flchar}.${cd_flchar}\n" ${CDS[count]}
        count=$((count-1))
    done
}
```

```
cd_getrc ()
{
    cd_flchar=$(stty -a | awk -F \ ')
    '/rows/ { print $2 $3 }' | awk '{ print $4 }'
    if [${TEST} ${cd_flchar} -ne 0 ];
    then
        cd_lchar=${{cd_flchar}/2-5}
        cd_rchar=${{cd_flchar}/2-5}
        cd_flchar=${{cd_flchar}-5}
    else
        cd_flchar=${FLCHAR:=75}
        # cd_flchar 用于 @s @ 历史
        cd_lchar=${LCHAR:=35}
        cd_rchar=${RCHAR:=35}
    fi
}
```

cd_doselection {
    local -i nm=0
    cd_dlag="TRUE"
    if [${TEST} "$(CD_MODE)" = "PREV" ];
    then
        if [${TEST} -z "$cd_npwd" ];
        then
            cd_npwd=0
        fi
    fi
    tm=$(echo "${cd_npwd}" | cut -b 1)
    if [${TEST} "$(tm)" = "_" ];
    then
        pm=$(echo "${cd_npwd}" | cut -b 2)
        nm=$(echo "${cd_npwd}" | cut -d -2)
        case "$pm" in
            a) cd_npwd=$(CDS[$nm]);
            s) cd_npwd=$CDS[$nm];
            S) cd_npwd=$CDS[$nm];
        case
    fi
}
```
