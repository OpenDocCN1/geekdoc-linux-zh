
```c
int def_prog_mode()
int def_shell_mode()
int reset_prog_mode()
int reset_shell_mode()
int resetty()
int savory()
int ripoffline(int line, int (*init)(WINDOW *, int))
int napms(int ms)
```

## 屏幕转储 (Screen Dump)

```c
int scr_dump(char *filename)
（注意：尚未实现。）
int scr_restore(char *filename)
（注意：尚未实现。）
int scr_init(char *filename)
（注意：尚未实现。）
int scr_set(char *filename)
（注意：尚未实现。）
```

## Termcap 仿真

```c
int tgetent(char *bp, char *name)
int tgetflag(char id[2])
int tgetnum(char id[2])
char *tgetstr(char id[2], char **area)
char *tgoto(char *cap, int col, int row)
int tputs(char *str, int affcnt, int (*putc)()
```

## Terminfo 函数

```c
int setupterm(char *term, int fildes, int *errret)
int setterm(char *term)
int set_curterm(TERMINAL *nterm)
int del_curterm(TERMINAL *oterm)
int restartterm(char *term, int fildes, int *errret)
```

（注意：尚未实现）。

```c
char *tparam(char *str, p1, p2, p3, p4, p5, p6, p7, p8, p9)
p1 - p9 long int.
int tputs(char *str, int attent, int (*putc)(char))
int putchar(char *str)
int vidputs(ctype attr, int (*putc)(char))
int mvcur(int oldrow, int oldcol, int newrow, int newcol)
int tigetflag(char *capname)
int tigetnum(char *capname)
int tigetstr(char *capname)
```

## 调试函数

- `void _init_trace()`

- `void _tracef(char *, ...)`

- `char *_trace_attr(mode)`

- `void traceon()`

- `void traceoff()`

## Terminfo 能力

### 布尔能力

| 变量 | 能力名称 | 整数代码 |  |
| :--- | :--- | :--- | :--- |
| `auto_left_margin` | `bw` | `bw` | 从第0列到最后一列循环 |
| `auto_right_margin` | `am` | `am` | 终端具有自动边距 |
| `back_color` | `bce` | `ut` | 使用背景色 |
| `can_change` | `ccc` | `cc` | 重新定义 |

### 布尔能力（续）

| 变量 | 能力名称 | 整数代码 |  |
| :--- | :--- | :--- | :--- |
| `ceol_standout` | `xhp` | `xs` | 覆盖 (`hp`) |
| `col_addr_glitch` | `xhpa` | `YA` | 仅正向移动 `hpa/mhpa` |
| `lpi_changes` | `ppi` | `YB` | 字符变化 |
| `cr_cancels_micro_mode` | `crym` | 关闭微模式 |
| `eat_newline` | `xenl` | `xn` | 80列后换行 (概念) |
| `erase_overwrite` | `eo` | `eo` | 空白覆盖 |
| `generic_type` | `gn` | `gn` | 通用行（例如，拨号，切换） |
| `hard_copy` | `hc` | | 硬拷贝终端 |
| `hard_cursor` | `chts` | | 光标难以查看 |
| `has_meta_key` | `km` | `km` | 具有 Meta 键（性位） |
| `has_print_wheel` | `daisy` | `YC` | 修改字符集 |
| `has_status_line` | | | | 额外的“状态行” |
| `hue_lightness_saturation` | `hls` | `hl` | 终端仅使用 HLS 符号 (`Tektronix`) |
| `insert_null` | `in` | `in` | 区分空 |
| `lpi_changes_res` | `lix` | `YG` | 行距 |
| `memory_above` | `da` | `da` | 在屏幕上方保留 |
| `memory_below` | `db` | `db` | 在屏幕下方保留 |
| `move_insert_mode` | `mir` | `mi` | 在插入模式下安全移动 |
| `move_standout_mode` | `msgr` | `ms` | 在突出模式下安全移动 |
| `needs_xon_xoff` | `nxon` | `nx` | 需要 `xon/xoff` |
| `no_esc_ctl` | `xsb` | `xb` | 蜂窝 (`F1=退出，F2=控制`) |
| `no_color_video` | `ncv` | `Nc` | 不能与颜色使用的视频属性 |
| `no_pad_char` | `npc` | `npc` | 字符不存在 |
| `non_rev` | `nrmrc` | `NR` | 反转 |
| `non_dest_scroll_region` | `ndscr` | `ND` | 非破坏性滚动区域 |
| `over_strike` | `os` | `os` | 终端覆盖 |
| `prtr_silent` | `mc5i` | `5i` | 打印机不在屏幕显示 |
| `row_addr_glitch` | `xva` | `Y` | 行符 (`Teleray 161`) |
| `tilde_glitch` | `hz` | `hz` | 海浪；无法打印 `-s` |
| `transparent_underline` | `ul` | `ul` | 下划线覆盖 |
| `xon_xoff` | `xo` | `xo` | 终端使用 `xon/xoff` 握手 |

### 数字

| 变量 | 能力名称 | 整数代码 | 描述 |
| :--- | :--- | :--- | :--- |
| `bit_image_entwinning` | `bitwin` | `Yo` | `SYSV` 中未文档 |
| `buffer_capacity` | `bufsz` | `Ya` | 打印前的缓冲字节数 |
| `columns` | `cols` | `co` | 每行的列数 |
| `dot_vert_spacing` | `spinv` | `Yb` | 每英寸水平点点间距 |
| `dot_horiz_spacing` | `spinh` | `Yc` | 每英寸垂直引脚间距 |
| `init_tabs` | | | 每隔空格初始化标签 |
| `label_height` | `lh` | `Ih` | 每个标签的行数 |
| `label_width` | `lw` | `lw` | 每个标签的列数 |
| `lines` | `lines` | `li` | 屏幕或页的行数 |
| `lines_of_memory` | `lm` | `Im` | 内存行数，`>0` 表示多种 |
| `magic_cookie_glitch` | `xmc` | `sg` | `lm` 或 `rm` 留下的空白字符 |
| `max_colors` | `colors` | `Co` | 屏幕上颜色数量 |
| `max_micro_address` | `madr` | `Yd` | 微地址的最大值 |
| `max_micro_jump` | `mympe` | `Ye` | 参数-微的极大值 |
| `max_pairs` | `pairs` | `Pa` | 屏幕上颜色对的最大数量 |
| `micro_col_size` | `mcs` | `Yf` | 模式下的字符大小 |
| `micro_line_size` | `mls` | `Yg` | 模式下的行步长 |
| `no_color_video` | `ncv` | `Nc` | 不能与颜色使用的视频属性 |
| `number_of_pins` | `npins` | `Yh` | 打印头的引脚数 |
| `num_labels` | `nlab` | | 屏幕上标签的数量 |
| `output_res_char` | `orc` | `Yi` | 每行的水平分辨率 |
| `output_res_horiz_inch` | `orl` | `Yj` | 每英寸垂直分辨率 |
| `output_res_vert_inch` | `orvi` | `Yk` | 每英寸水平分辨率 |
