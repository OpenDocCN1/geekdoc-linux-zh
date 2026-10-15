
## 描述

Motion notify（移动通知）事件表示指针已从屏幕的一个位置移动到另一个位置。`time` 字段表示事件在服务器速率时间中的时间（自上次服务器重置以来的毫秒）。如果窗口与根窗口在同一个屏幕上（通常情况下如此），那么 `x` 和 `y` 是相对于窗口原点的坐标；否则，它们都被设置为 0。`x_root` 和 `y_root` 是相对于根窗口的坐标。`pressure` 始终设置为值 0.5，`xtilt` 和 `ytilt` 始终设置为值 0。`source` 始终设置为 `GDK_SOURCE_MOUSE`，`deviceid` 始终设置为值 `GDK_CORE_POINTER`。如果用于选择事件的掩码 `GDK_POINTER_MOTION_HINT_MASK` 被使用，则 `is_hint` 设置为 1，否则为 0。调用 `pointer()` 时，`state` 指定事件发生前鼠标键和修饰键的状态。`state` 的可能值通过对以下任何项进行按位或构造

### 表 3.5 移动事件状态

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键按下。 |
| `GDK_LOCK_MASK` | lock 键按下。 |
| `GDK_CONTROL_MASK` | control 键按下。 |
| `GDK_MOD1__MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

### 表 3.5 移动事件状态（续）

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

*(注：此处原文表格编号重复，已按逻辑处理)*

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

*(注：由于原文文本中存在大量重复的表格内容和逻辑混乱，此处遵循“不漏掉任何行”原则进行翻译，但实际文档工程中应检查源错误。)*

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_SHIFT_MASK` | shift 键被按下。 |
| `GDK_LOCK_MASK` | lock 键被按下。 |
| `GDK_CONTROL_MASK` | control 键被按下。 |
| `GDK_MOD1_MASK` | mod1 被按下（通常为 Alt_L 或 Alt_R）。 |
| `GDK_MOD2_MASK` | mod2 被按下（通常为 Num_Lock）。 |

*(注：用户提供的原文文本在 Table 3.5 之后出现了严重的逻辑重复和断码，翻译内容已根据原文行进行对应。)*

| 值 | 含义 |
| --- | --- |
| `GDK_BUTTON1_MASK` | 1 键被按下（左键）。 |
| `GDK_BUTTON2_MASK` | 2 键被按下（右键）。 |
| `GDK_BUTTON3_MASK` | 3 键被按下（中键）。 |
| `GDK_BUTTON4_MASK` | 4 键被按下（侧键）。 |
| `GDK_BUTTON5_MASK` | 5 键被按下（侧键）。 |

| 值 | 含义 |
| --- | --- |
| `GDK_BUTTON1_MASK` | 1 键被按下（左键）。 |
| `GDK_BUTTON2_MASK` | 2 键被按下（右键）。 |
| `GDK_BUTTON3_MASK` | 3 键被按下（中键）。 |
| `GDK_BUTTON4_MASK` | 4 键被按下（侧键）。 |
| `GDK_BUTTON5_MASK` | 5 键被按下（侧键）。 |

*(注：由于原文文本在截断处极其混乱且重复，此处为基于对给定“乱码”的忠实翻译。)*

## GdkEventExpose

```
struct _GdkEventExpose {
```
