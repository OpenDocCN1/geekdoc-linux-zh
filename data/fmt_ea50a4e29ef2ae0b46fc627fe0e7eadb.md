
| `bundle-group-members` (`bgl`) | `zlman bundle-group-members <options> <group>` | 列出包组的成员。 |

### ZLMAN 命令摘要（续）

| 命令 | 用法/选项 | 说明 |
|---|---|---|

| `bundle-group-` (`bga`) | `zlman bundle-group-add <options> <group> <bundle>` | 将包添加到组中。 |

| `bundle-group-remove` (`bgr`) | `zlman bundle-group-remove <options> <bundle>` | 从组中移除一个包。 |

| `bundle-dep-list` (`bdl`) | `zlman bundle-dep-list <options> <name>` | 列出包的依赖项。 |

| `bundle-dep-add` (`bda`) | `zlman bundle-dep-add <options> <dependency name>` | 为包添加依赖项。 |

| `bundle-dep-remove` (`bdr`) | `zlman bundle-dep-remove <options> <dependency name>` | 从包中移除依赖项。 |

| `patch-bundle-create` (`pbc`) | `zlman patch-bundle-create <options> <Product Name> <Product Version> <Product Arch> <Patch File> <folder>` | 创建一个新的补丁包。 |

| `catalog-list` (`cl`) | `zlman catalog-list <options> <folder> <filter>` | 列出文件夹中的目录。 |

| | `-r, --recursive` `-f, --filter=<filter>` | 包含子文件夹中的对象。仅显示匹配特定过滤器的选项。如果过滤器使用了引号，可以使用 `*`。 |

| `catalog-create` (`cc`) | `zlman catalog-create <options> <name>` | 创建一个新的目录。 |

| `catalog-folder-create` (`cfc`) | `zlman catalog-folder-create <options> <name>` | 创建一个用于包含目录的新文件夹。 |

| `catalog-delete` (`cd`) | `zlman catalog-delete <options><catalog>` | 删除目录。 |

| `catalog-rename` (`cr`) | `zlman catalog-rename <options> <new name>` | 重命名目录。 |

## 附录 A：命令

### ZLMAN 命令摘要（续）

| 命令 | 用法/选项 | 说明 |
| --- | --- | --- |

| `catalog-move` (`cmv`) | `zlman catalog-move <catalog> <folder>` | 移动目录。 |

| `catalog-list-bundles` (`clb`) | `zlman catalog-list-bundles <options> <catalog>` | 显示与目录关联的所有包的列表。 |

| `catalog-add-bundle` (`cab`) | `zlman catalog-add-bundle <options> <bundle>` | 将包与目录关联。 |

| | `--dry-run` `-a, --allow-removal` `--prepare-time=<HH:MM>` | 指定执行操作的时间。时间格式应为 "HH:MM"，小时采用 24 小时制。 |

| `--prepare-date=<YYYY-MM-DD>` | | 指定执行操作的特定日期。日期格式应为 "YYYY-MM-DD"。 |

| `--time=<HH:MM>` | | 指定执行操作的时间。时间格式应为 "HH:MM"，小时采用 24 小时制。 |

| `--date=<YYYY-MM-DD>` | | 指定执行操作的特定日期。日期格式应为 "YYYY-MM-DD"。 |

| `--now` | | 指定尽可能尽快执行该操作。可以指定重复频率。如果没有指定其他计划，则默认为现在。 |

### ZLMAN 命令摘要（续）

| 命令 | 用法/选项 | 说明 |
|---|---|---|

| | `--relative=<DD:HH:MM>` | 指定相对于当前时间执行操作的时刻。时间格式应为 "DD:HH:MM"。可以指定重复频率。 |

| | `--weekly=<MWF>` | 指定执行操作的星期几。如果指定，则操作每七天重复一次。例如："MWF" 表示每周一、周三、周五执行操作。周一 = M，周二 = TU，周三 = W，周四 = TH，周五 = F，周六 = SA，周日 = SU。 |

| | `--monthly=<DD>` | 指定每月执行操作的日期。如果指定，则操作每月重复一次。不能指定多个日期。 |

| | `--yearly=<MM-DD, MM-DD,...>` | 指定每年执行操作的日期。如果指定，则操作每年重复一次。日期格式应为 "MM-DD"。多个日期之间用逗号分隔。 |

| | `--repeat=<DD:HH:MM>` | 指定操作的重复频率，格式为 "DD:HH:MM"。天数可选可选。 |

| | `--gmt` | 所有时间均被视为 GMT。如果未给出，所有时间均被视为 `catalog-remove-bundle` (`crb`)。移除包与目录之间的关联。 |

## 附录 A：命令

ZLMAN 命令摘要（续）

| 命令 | 用法/选项 | 明明 |
| --- | --- | --- |

| `Catalog-remove-bundle` (`crb`) | `zlman catalog-remove-bundle <options> <bundle>` | 移除包与目录之间的关联。 |

| `workstation-info` (`wi`) | `zlman workstation-info <options> <Workstation>` | 显示工作站的信息。 |

| `workstation-list` (`wl`) | `zlman workstation-list <options> <folder> -r, --filter=<filter>` | 列出文件夹中的目录。包含子文件夹中的对象。仅显示匹配特定过滤器的选项。如果过滤器使用了引号，可以使用 `*`。 |

| `workstation-messages` (`wm`) | `zlman workstation-messages <options> <Workstation>` | 确认消息。 |

| `workstation-delete` (`wd`) | `zlman workstation-delete <options> <Workstation>` | 删除消息。 |

| `workstation-refresh` (`wr`) | `zlman workstation-refresh <options> <Service>` | 刷新服务。 |

| `workstation-rename` (`wrn`) | `zlman workstation-rename <options> <name>` | 重命名设备。 |

| `workstation-move` (`wmv`) | `zlman workstation-move <options> <folder>` | 移动目录。 |

### ZLMAN 命令摘要（续）

| 命令 | 用法/选项 | 说明 |
| --- | --- | --- |

| `workstation-folder-create` (`wfc`) | `zlman workstation-folder-create <options> <name>` | 创建新文件夹。 |

| `workstation-group-create` (`wgc`) | `zlman workstation-group-create <options> <name>` | 创建新组。 |

| `workstation-group-members` (`wgm`) | `zlman workstation-group-members <options> <catalog>` | 列出组的成员。 |

| `workstation-group-add` (`wga`) | `zlman workstation-group-add <options> <bundle>` | 将包添加到组中。 |

| `workstation-group-remove` (`wgr`) | `zlman workstation-group-remove <options> <bundle>` | 从组中移除一个包。 |

| `workstation-list-bundles` (`wlb`) | `zlman workstation-list-bundles <options> <catalog>` | 显示与目录关联的所有包的列表。 |
