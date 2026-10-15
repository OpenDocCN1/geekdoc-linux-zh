

打印机接口程序可以通过三种方式指定：

- **-e printer** – 在这种情况下，*printer* 是现有打印机的名称。这种指定接口程序的方法在添加一台与现有打印机完全相同的打印机时很有用。**lpadmin** 会在新目标名称下复制接口程序。

- **-m model** – 使用此选项时，*model* 是系统具有标准接口程序的设备类型。要确定系统支持哪些型号，请查看 **/var/spool/lp/model**。使用此形式时，**lpadmin** 会复制文件 **/var/spool/lp/model/model**，供新目标专用。

- **-i interface** – 使用 **-i** 选项时，*interface* 是用作接口脚本的程序的完整路径名。大多数版本的 **lpadmin** 会复制接口程序，因此如果您在运行 **lpadmin** 后想更改程序，必须更改目标特定的副本，而不是原始文件。

HP-UX 允许您指定返回状态信息并取消打印机作业的程序。这些程序的指定方式与接口脚本类似，但使用不同的选项前缀（分别用于取消和状态脚本的 **-ocm** 和 **-osm**）。

**lpadmin** 还接受以下附加选项：

- **-p printer** 告诉 **lpadmin** 您指的是哪台打印机或打印机。结合其他选项使用此标志可修改打印机。

- **-c class** 指定打印机应包含的 *class* 名称。可以为给定打印机指定任意数量的类。如果指定不存在的类，则会创建该类。类名限制为 14 个字符。

- **-x printer** 从打印系统中移除打印机。如果 *printer* 是类的唯一成员，则该类也会被移除。如果打印机或类有排队输出的作业，则不能移除。如果排队的作业阻止您移除打印机，请使用 **reject** 命令停止新作业进入 spool，并使用 **lpremove** 或 **cancel** 命令清除现有作业。如果 **lpadmin -x** 仍无法移除打印机，请遵循第 1053 页的建议。

- **-r class** 将打印机从 *class* 中移除。**-r** 标志不会移除打印机；它只是将其从类中移除。如果指定的打印机是类的唯一成员，则类本身将被移除。

**lp** 在被 **accept** 告知之前不会接受新打印机的请求。

System V 打印命令通常接受用引号括起来的、以逗号分隔的目标列表来代替单个目标。例如，命令

```
$ sudo /usr/sbin/lpadmin -p"howler-lw,ralphie-lw" -ceng-printers
```

将打印机 howler-lw 和 ralphie-lw 添加到 eng-printers 类。表 26.3 总结了 lpadmin 理解的标志。

## 表 26.3 lpadmin 标志

| Flag | Function |
|---|---|
| -p printer | Specifies the printer to which other options apply |
| -d dest | Makes dest the system's default printing destination |
| -x dest | Removes dest from the printing system |
| -c class | Adds the printer to class |
| -r class | Removes the printer from class |
| -e dest | Copies another printer's interface program |
| -i interface | Makes interface the interface program for the printer |
| -m model | Makes the printer use the interface program for model |
| -h | Signifies that the printer is hardwired |
| -v file | Specifies the full path of the printer device file |
| -D"desc" | Sets the printer description string to desc |
| -L"location" | Sets a textual description of where a printer lives |

## lpadmin 示例

以下示例展示了 lpadmin 的各种用法。

```
$ sudo lpadmin -phowler-lw -v/dev/tty06 -mPostScript -cpr
```

此命令告诉打印系统，一台名为 howler-lw 的打印机连接到 /dev/tty06，打印机应属于类 pr，并且应使用 PostScript 打印机的接口程序。lpadmin 会为您创建 spool 目录。

命令

```
$ sudo lpadmin -dpr
```

将系统的默认目标设置为类（或打印机）pr，而命令

```
$ sudo lpadmin -phowler-lw -L"Conference room"
```

设置 howler-lw 的描述字符串。

```
$ sudo lpadmin -phowler-lw -rpr -cfast
```

将 howler-lw 从类 pr 中移除并将其添加到类 fast；

```
$ sudo lpadmin -xhowler-lw
```

完全移除 howler-lw。

