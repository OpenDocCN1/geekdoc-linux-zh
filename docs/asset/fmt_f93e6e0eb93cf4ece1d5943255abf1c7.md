
用于记录任何获取 root 权限的用户按键的 shell 脚本。

`banybody`

用于捕获 shell 脚本定义的任何用户按键的 shell 脚本。

`log_keystrokes.ksh`

记录用户在键盘上打字时按键记录的 shell 脚本。

# 函数

## 第 1 章

`rotate_line`

该函数是一个进度指示器，显示为闪烁的线条。

`elapsed_time`

该函数将秒转换为小时、分钟和秒的格式。

`ping_host`

该函数检测 UNIX 变体，然后使用函数的 `$1` 参数指定的宿主机，使用该系统正确的语法进行 ping。

## 第 2 章

`build_random_line`

该函数使用随机数来选择一个数组元素。

`load_default_keyboard`

该函数将默认键盘布局加载到数组中。以下所有 24 个函数都是逐行处理文件的不同方法：

`cat_while_read_LINE`
`while_read_LINE_bottom`
`cat_while_LINE_line`
`while_LINE_line_bottom`
`cat_while_line_cmdsub2`
`while_LINE_line_bottom_cmdsub2`
`for_LINE_CAT_FILE`
`for_LINE_CAT_FILE_cmdsub2`
`while_line_outfile`
`while_read_LINE_FD_IN`
`cat_while_read_LINE_FD_OUT`
`while_read_line_bottom_FD_OUT`
`while_line_bottom_cmdsub2_FD_OUT`
`for_LINE_CAT_FILE_FD_OUT`
`for_LINE_CAT_FILE_cmdsub2_FD_OUT`
`while_line_outfile_FD_IN`
`while_line_outfile_FD_OUT`
`while_line_outfile_FD_IN_AND_OUT`
`while_LINE_LINE_FD_IN`
`while_LINE_LINE_cmdsub2_FD_IN`
`while_read_LINE_FD_IN_AND_OUT`
`while_LINE_LINE_FD_IN_AND_OUT`
`while_LINE_line_cmdsub2_FD_IN_AND_OUT`

## 第 3 章

第 3 章没有需要列出的函数。

## 第 4 章

`dots`

该函数用作进度指示器，每隔约10 秒显示一系列点。

`rotate`

该函数用作进度指示器，显示旋转线条的出现。

`elapsed_time`

该函数将秒转换为小时、分钟和秒的格式。

## 第 5 章

`parse_fixed_length_records`

该函数使用 `cut` 命令解析固定长度的记录文件。

`parse_variable_length_records`

该函数使用 `cut` 命令解析变长长度的记录文件。

`merge_fixed_length_records`

该函数将记录文件的文件名追加到文件中每条记录的末尾。

`merge_variable_length_records`

该函数将记录文件的文件名追加到文件中每条记录的末尾。

## 第 6 章

`pre_event`

允许在处理之前执行预事件的函数。

`post_event`

允许在处理之后执行后事件的函数。

## 第 7 章

`elapsed_time`

该函数将秒转换为小时、分钟和秒的格式。

`verify_copy`

该函数验证本地机器与一个或多个远程机器的文件大小是否匹配。

`ready_to_run`

该函数从 shell 脚本开始，并循环直到在系统中找到 `$READY_TO_RUN` 文件为止。

## 第 8 章

`increment_by_1`

此 Expect 过程（函数）将数字加 1。

## 第 9 章

第 9 章没有需要列出的函数。

## 第 10 章

`mon_proc_end`

该函数循环直到被监控的进程执行结束。

`mon_proc_start`

该函数循环直到被监控的进程开始执行。

`pre_event_script`

该函数在处理开始前作为预事件执行。

`startup_event_script`

该函数作为启动事件执行。

`post_event_script`

该函数在处理完成后执行。

`test_string`

该函数用于测试文本字符串。

`proc_watch`

该函数监控被监控进程的启动和停止。

## 第 11 章

`get_random_number`

该函数产生一个于 1 到 32,767 之间的伪随机数。

`in_range_random_number`

创建一个小于或等于用户定义的 `$UPPER_LIMIT` 值的伪随机数。

`in_range_fixed_length_random_number_typeset`

使用 `typeset` 创建一个范围内的伪随机数。

`get_random`

该函数使用 `typeset` 创建一个伪随机数。

`get_time`

该函数显示日期。

`get_second`

该函数显示时间。

`my_program`

该函数显示程序。

`build_random_line`

该函数使用随机数来选择一个数组元素。

`elapsed_time`

该函数将秒转换为小时、分钟和秒的格式。

`load_default_keyboard`

该函数加载默认键盘布局。

## 第 12 章

`in_range_random_number`

创建一个小于或等于用户定义的 `$UPPER_LIMIT` 值的伪随机数。

`in_range_fixed_length_random_number_typeset`

使用 `typeset` 创建一个范围内的伪随机数。

`get_random`

该函数使用 `typeset` 创建一个伪随机数。

`get_time`

该函数显示日期。

`get_second`

该函数显示时间。

`my_program`

该函数显示程序。

`build_random_line`

该函数使用随机数来选择一个数组元素。

`elapsed_time`

该函数将秒转换为小时、分钟和秒的格式。

`load_default_keyboard`

该函数加载默认键盘布局。

## 第 13 章

`verify_copy`

该函数验证本地机器与一个或多个远程机器的文件大小是否匹配。

`ready_to_run`

该函数从 shell 脚本开始，并循环直到在系统中找到 `$READY_TO_RUN` 文件为止。

## 第 14 章

`increment_by_1`

此 Expect 过程（函数）将数字加 1。

## 第 15 章

`mon_proc_end`

该函数循环直到被监控的进程执行结束。

`mon_proc_start`

该函数循环直到被监控的进程开始执行。

## 附录 A 网站上的内容

此函数启用所有处于禁用状态的打印机和队列的打印功能。

`CUPS_printing`

此函数启用所有处于禁用状态的打印机和队列的 CUPS 打印。

`HP_UX_printing`

此函数启用所有处于禁用状态的打印机和队列的打印功能。

`Linux_printing`

此函数启用所有处于禁用状态的打印机和队列的打印功能。

`OpenBSD_printing`

此函数启用所有处于禁用状态的打印机和队列的打印功能。

`Solaris_printing`

此函数启用所有处于禁用状态的打印机和队列的打印功能。

## 第 26 章

26 章没有没有列出的函数。

## 第 27 章

`display_main_menu`

此函数显示 `dirvish_ctrl` 壳脚本的主菜单。

`read_input`

此函数将持续读取输入直到输入 99 为止。

`parse_conf`

此函数用于解析 Dirvish 的 `master.conf` 文件。
