
| 7 | home | wm | 2183 - 2732 | 408.20MB (550/0/0) | 836000 |

> 注意

如果不为驱动器标记，分区更改将不会被保留。

6. 分区磁盘后，你必须在分区提示符下输入 `label` 来标记它：

```
partition> label
```

7. 标记磁盘后，输入 `quit` 退出分区菜单：

`partition> quit`

8. 再次输入 `quit` 退出 `format` 工具：

`format> quit`

> 警告

更改分区大小时将丢失所有数据。请确保在继续之前将数据复制到另一块磁盘或磁带上。

重要的是指出，如果使用 `format` 工具定义磁盘分区时不够小心，可能会发生一些不理想的情况。首先，小心不要浪费磁盘空间。当你减小一个切片的大小而不调整下一个相邻磁盘切片的起始柱面号时，可能会浪费磁盘空间。

其次，不要让磁盘切片重叠。重叠发生在同一个或多个柱面被分配给多个磁盘切片时。例如，在不减小相邻切片大小的情况下增加一个切片的大小会创建重叠的分区。`format` 工具不会警告你磁盘空间浪费或分区重叠的情况。

再提一点：在标准 UFS 文件系统上，不要更改当前正在使用的磁盘切片的大小。当带有现有切片的磁盘被重新分区并重新标记时，任何现有数据都将丢失。在重新分区磁盘之前，先将所有数据复制到磁带或另一块磁盘。

## Free Hog 切片

使用 `format` 工具更改磁盘切片大小时，会自动指定一个临时切片，该切片会扩展和收缩以适应切片调整大小操作。这个临时切片被称为“free hog”，它代表磁盘驱动器上的未使用磁盘空间。如果一个切片减小，free hog 就会扩展。然后 free hog 用于为已增加的切片分配空间。但是，它并不能防止上一节所述的磁盘切片重叠。

free hog 切片仅在运行 `format` 工具时存在。它不会被保存为永久切片。

## 使用 Format 工具修改分区

如果你需要更改特定磁盘上切片的大小，可以按照上一节所述重新创建磁盘切片，或使用 `format` 工具的 `modify` 选项。

`modify` 选项允许 `root` 通过指定每个切片的大小来创建切片，而无需跟踪起始柱面边界。它还会跟踪临时 free hog 切片中的任何多余磁盘空间。

> 注意

如果你尝试修改已挂载的分区，会收到错误信息，提示 Cannot modify disk partitions while it has mounted partitions。

## 逐步操作

### 6.3 修改磁盘切片

要修改磁盘切片，请按以下步骤操作：

1. 备份你的数据。此过程将销毁该磁盘上的数据。

2. 以 `root` 身份进入 `format` 工具的分区菜单，如 6.2 逐步操作所述。

3. 打印现有分区方案后，输入 `modify` 并按 Enter。

输入 `modify` 时，在没有挂载分区的磁盘上会看到以下输出：

```
Select partitioning base:
    0. Current partition table (original)
    1. All Free Hog
Choose base (enter number) [0]?
```

4. 按 Enter 选择默认选项。显示如下：

| 分区 | 标签 | 标志 | 柱面 | 大小 | 块数 |

|------|-----|------|-----------|------|--------|

| 0 | usr | wm | 0 - 194 | 100.26MB | (195/0/0) 205335 |

| 1 | unassigned | wu | 195 - 1167 | 500.28MB | (973/0/0) 1024569 |

| 2 | backup | wm | 0 - 3983 | 2.00GB | (3984/0/0) 4195152 |

| 3 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

| 4 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

| 5 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

| 6 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

| 7 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

是否希望基于上表继续创建新的分区表[yes]？

5. 按 Enter 选择默认选项。以下消息将被显示：

```
Free Hog partition[6]?
```

6. 按 Enter 选择默认选项。如果所有磁盘空间都已使用，将显示以下消息：

```
Warning: No space available from Free Hog partition.
Continue[no]?
```

> 注意

切片 6 未显示，因为那是临时的 free hog。

7. 输入 `yes`。你将被提示输入每个分区的新的大小：

```
Enter size of partition '0' [205335b,195c,100.26mb,0.10gb]: 90m
Enter size of partition '1' [1024569b,973c,500.28mb 0.49gb]:450m
Enter size of partition '3' [0b, 0c, 0.00mb, 0.00gb]: <cr>
Enter size of partition '4' [0b, 0c, 0.00mb, 0.00gb]: <cr>
Enter size of partition '5' [0b, 0c, 0.00mb, 0.00gb]: <cr>
Enter size of partition '7' [0b, 0c, 0.00mb, 0.00gb]: <cr>
```

> 注意

切片 6，即 free hog，表示未使用的磁盘空间。你可能希望将此空间分配给另一个分区，以免它未被使用，或者你可以保存它并在另一时间分配给未使用的分区。

当你完成调整最后一个分区的大小后，将显示以下内容，显示修订后的分区映射：

| 分区 | 标签 | 标志 | 柱面 | 大小 | 块数 |

|------|-----|------|-----------|------|--------|

| 0 | usr | wm | 0 - 175 | 90.49MB | (176/0/0) 185328 |

| 1 | unassigned | wu | 176 - 1051 | 450.40MB | (876/0/0) 922428 |

| 2 | backup | wm | 0 - 3983 | 2.00GB | (3984/0/0) 4195152 |

| 3 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

| 4 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

| 5 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

| 6 | unassigned | wm | 1052 - 3983 | 1.47GB | (2932/0/0) 3087396 |

| 7 | unassigned | wm | 0 | 0 | (0/0/0) 0 |

```
Okay to make this the current partition table[yes]?
```

- 8. 按 Enter 确认您修改的分区表。您将看到以下消息显示：

  `Enter table name (remember quotes):`

- 9. 为修改后的分区表命名并按 Enter：

  `Enter table name (remember quotes): c0t3d0.2gb`

- 10. 输入名称后，将显示以下消息：

  `Ready to label disk, continue?`

- 11. 输入 `yes` 并按 Enter 继续。

- 12. 输入 `quit`（或 `q`）并按 Enter 退出分区菜单。主菜单将被显示。

- 13. 输入 `quit` 并按 Enter 退出格式化实用程序。

## 恢复磁盘分区信息

使用前面描述的 `prtvtoc` 命令将磁盘的 VTOC（卷目录表）保存到文件中始终是一个好主意。此信息随后可用于在当前 VTOC 损坏或意外更改或需要更换磁盘驱动器时恢复磁盘标签。

通过将 `prtvtoc` 命令的输出保存到另一磁盘上的文件中，您可以在运行 `fmthard` 命令时引用它。`fmthard` 命令会更新硬盘上的 VTOC。

## 逐步操作

### 6.4 恢复 VTOC（卷目录表）

要恢复 VTOC，请按照以下步骤操作：

- 1. 在磁盘上运行 `format` 实用程序，并使用默认分区表对其进行标记。

- 2. 使用 `fmthard` 命令将备份的 VTOC 信息写回磁盘驱动器。以下示例使用 `fmthard` 命令恢复名为 `/dev/rdsk/c0t3d0s2` 的磁盘上的损坏标签。备份的 VTOC 信息位于 `/vtoc` 目录中名为 `c0t3d0` 的文件中：
