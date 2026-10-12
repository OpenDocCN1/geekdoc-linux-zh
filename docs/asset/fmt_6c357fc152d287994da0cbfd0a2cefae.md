
# 显示器特性说明

一旦你知道如何在此处绘图 `gnuplot` 软件包，你还需要以下显示器特性：

- 带宽 (`VB`)
- 水平同步频率 (`HSF`) 范围
- 垂直同步频率 (`VSF`) 范围

# Shell 脚本示例

```bash
while [ "$1" != "" ]
do
  case $1 in
    -t) TITLE="$2"; shift;
    -b) BANDWIDTH="$2"; shift;
    -h) MINSHF="$2" MAXHF="$3"; shift; shift;
    -v) MINVS="$2" MAXVS="$3"; shift; shift;
    -a) ASPECT="$2"; shift;
    -g) GNUOPTS="$2"; shift;
    -t) cat <<EOF

modeplot 控制开关：
EOF
  esac
done
```

# Gnuplot 配置文件示例

```
# 1542

# 目录

# ($Id: video-modes.sgml,v 1.4 1997/10/31 13:51:07 esr Exp $)

# 显示器描述。带宽单位为 MHz，水平频率单位为 kHz，
# 垂直频率单位为 Hz

TITLE=Viewsonic 21PS

BANDWIDTH=185

MINSHF=31

MAXHF=85

MINVS=50

MAXVS=160

ASPECT=4/3"

# VESA 推荐的最小刷新率

vesa=72.5
```
