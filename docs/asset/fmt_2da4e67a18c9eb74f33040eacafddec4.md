
```
UTRG____pfa utopia medium r  0 0 0 0 p iso88859 1
UTI____pfa utopia medium i  0 0 0 0 p iso88859 1
UTB____pfa utopia bold r  0 0 0 0 p iso88859 1
UTBI___pfa utopia bold i  0 0 0 0 p iso88859 1
courp.pfa courier medium r  0 0 0 0 m iso88859 1
couri.pfa courier medium i  0 0 0 0 m iso88859 1
courb.pfa courier bold r  0 0 0 0 m iso88859 1
courbi.pfa courier bold i  0 0 0 0 m iso88859 1
c0648bt-_pfa bitstream charter medium r  0 0 0 0 p iso88859 1
c0649bt-_pfa bitstream charter medium i  0 0 0 0 p iso88859 1
```

# 第 7 章 运行时服务器配置

## 列表 7.2 续

| c0632bt_pfb bitstream charter bold r normal 0 0 0 p o iso8859 1 |

| c0633bt_pfb bitstream charter bold I normal 0 0 0 p o iso8859 1 |

| c0419bt_pfb bitstream courier medium r normal 0 0 0 m o iso8859 1 |

| c0528bt_pfb bitstream courier medium i normal 0 0 0 m o iso8859 1 |

| c0583bt_pfb bitstream courier bold r normal 0 0 0 m o iso8859 1 |

| c0611bt_pfb bitstream courier bold i normal 0 0 0 m o iso8859 1 |

文件的第一行表示找到了多少字体，其余的行是字体名称，随后跟的是 `typeinst` 为字体生成的 X 逻辑字体描述符（X Logical Font Descriptor）。由于 `fonts.scale` 文件已成功生成，请在该目录下运行 `mkfontdir` 来生成你的 `fonts.dir`：

```
mkfontdir
```

此命令也应该无错误地完成。完成后，字体目录即已准备就绪，你的新字体就可以使用了。

## 使用 xset 测试它们

在本章前面的部分，`xset` 命令的几个重要功能当时被刻意忽略了，现在我们来涵盖它们。涉及的功能与运行时字体管理有关。`xset` 命令允许用户动态更改 X 字体路径——这意味着你可以使用 `xset` 让你刚刚安装的字体变得可用。

要做到这一点，你想要使用的命令是：

```
xset fp+ fontpath
```

在这种情况下，路径是指你刚刚安装字体的目录。例如，如果你的 `*.pfa`, `*.pfb`, `fonts.scale` 和 `fonts.dir` 文件安装在 `/usr/X11R6/lib/X11/fonts/` 目录下，你应该执行此命令：

```
xset fp+ /usr/X11R6/lib/X11/fonts/myfonts/
```

执行命令后，你需要等待片刻，让 `xset` 读取该目录下的 `fonts.dir` 文件并收集可用字体的信息。然后，它们会被添加到活动字体列表中，可以通过 `xlsfonts` 命令进行显示：

```
xlsfonts
```

`xset` 支持的与字体相关的操作完整列表请见表 7.7。

## 表 7.7 字体相关操作

| 命令行 | 配置更改 |

|---|---|

| xset fp+ path | 将指定的路径添加到 X 路径的末尾，并将其中找到的字体整合到可用字体列表中。 |

| xset +fp path | 将指定的路径添加到 X 路径的开头，并将其中找到的字体整合到可用字体列表中。 |

| xset fp- path | 分别从 X 路径和可用字体列表中移除指定的路径及所有关联字体。 |

| xset fp rehash | 通过重新扫描 X 路径中包含的目录和服务器，重新构建可用字体列表。 |

| xset fp=list | 将完整的 X 路径设置为列表所包含的由逗号分隔的目录和服务器列表。 |

| xset fp default | 将 X 路径恢复为启动时的原始路径和服务器列表，并使用恢复的路径重新构建可用字体列表 |

注意，字体路径也可以包含指向字体服务器的路径，这些服务器跨网络提供 X 服务。有关更多关于 XFree86 字体服务器的信息，请参阅第 15 章。

在你将新目录添加到字体路径后，你应该能够通过 `xfontsel` 或使用 `xfd` 查看你安装的新字体，只需提供一个类似于 `xfontsel` 生成的 X 逻辑描述符即可。有关 `xfontsel` 和 `xfd` 的更多信息，请参见第 4 章“标准 XFree86 程序与工具”。

## 将新字体添加到 XF86Config

在你对字体满意后，将新字体添加到环境中通常还剩最后一步：必须以永久的方式告诉 X 服务器它们的存在。使用 `xset` 对字体路径进行的编辑只持续到 X 会话结束。之后，除非将其永久，否则所有更改都会消失。这通过将包含字体的目录添加到你的 `XF86Config` 文件来实现。

使用如 `vi` 或 `emacs` 等编辑器编辑 `Files` 部分，在所有现有的 `FontPath` 行之后添加一条 `FontPath` 行以包含你新字体的路径：

```
FontPath "/usr/X11R/lib/X11/fonts/myfonts/"
```

注意，`FontPath` 条目的顺序很重要，除非你希望新字体优先于所有其他字体，否则避免将新的 `FontPath` 条目放在列表顶端。

保存编辑后的文件后，每当 X 服务器启动时，你的新 PostScript 字体都会出现在可用字体列表中。

# 第 7 章 运行时服务器配置

## 向 X 添加 TrueType 字体

尽管互联网和廉价的百货商店批量 CD-ROM 上大量的 PostScript 字体，但今天许多最流行的字体是针对 Windows 平台的，因此它们不是 PostScript 字体，而是 TrueType 字体，以 `.ttf` 结尾。

TrueType 字体不由标准的 X 字体系统处理。相反，我们使用一个名为 `xfst` 的特殊服务器，它可以动态渲染 TrueType 字体。

`xfst` 服务器的工作原理是将 TrueType 字体加载到内存中，然后将其渲染为 X 字体。这允许我们无需将它们转换为 PostScript 格式即可使用 TrueType 字体。

## 安装字体

Linux 用户通常拥有带有 Windows 的多启动系统。在这种情况下，通常希望将 Windows 分区的 `windows/` 和 `system/` 目录下的所有 `.ttf` 文件复制到 `/usr/ttf` 目录，以便在 X 内部也可以使用 Windows 字体。

在将 `.ttf` 文件复制到 `/usr/ttf` 后，有必要使用 `--sync` 选项同步 `xfst` 缓存：

```
xfst --sync
```

工作片刻后，`xfst` 应该无错误地完成，并更新缓存以反映你新安装字体的位置。

## 启动字体服务器并添加路径

在完成所有操作后，从 `xterm` 窗口或其他命令行启动新服务器进行测试：

```
xfst &
```

这将在后台启动 `xfst` 并保持其运行，以响应它管理的 TrueType 字体请求。现在服务器已激活，需要编辑字体路径以反映更改。通过以下命令实现：

```
xset fp+ unix::7100
```

此命令指示 `xset` 查询本地 UNIX 域端口 7100 上的字体服务器以获取字体。运行命令后，运行 `xlsfonts` 时新的 TrueType 字体应该会出现。注意，TrueType 字体的 X 逻辑字体描述符显示字库为 `ttf`，因此可以这样从 `xlsfonts` 列表中提取新字体：

```
xlsfonts | grep 'ttf.*'
```

同样有趣的是，`xfst` 服务器向列表中添加了几个较的字体别名，这些在 `xlsfonts` 列表中看起来像某些垃圾，但可以安全地忽略。

# 第7章 运行时服务器配置

## 表 7.8 xfstt 接受的命令行参数

| 参数 | 说明 |

| --- | --- |

| --sync | 将 xfstt 与 /usr/ttfonts 中安装的字体同步。注意，不应在 xfstt 运行时执行此操作。 |

| --glist | 在 --sync 选项之前提供时，会导致 xfstt 在同步字体时输出适用于 GhostScript 打印的字体列表。 |
