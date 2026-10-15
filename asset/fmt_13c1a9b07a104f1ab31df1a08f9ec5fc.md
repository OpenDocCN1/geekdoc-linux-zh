
| 25 | Ctrl-Y | 57 | 9 | 89 | Y | 121 | y |
| 26 | Ctrl-Z | 58 | : | 90 | Z | 122 | z |
| 27 | Ctrl-[ | 59 | ; | 91 | [ | 123 | { |
| 28 | Ctrl-\ | 60 | < | 92 | \ | 124 | | |
| 29 | Ctrl-] | 61 | = | 93 | ] | 125 | } |
| 30 | Ctrl-^ | 62 | > | 94 | ^ | 126 | ~ |
| 31 | Ctrl-_ | 63 | ? | 95 | _ | 127 | <DEL> |

```
void (*handler)(int, void *, struct pt_regs *),
unsigned long irqflags,
const char * devname,
void *dev_id);
```

### 11.4.2 Scalex 中断处理程序

中断处理程序（用汇编语言编写）与程序其余部分之间的一个关键链接是 `scalex` 设备内存区域的定义。由于汇编代码无法访问 C 编译器中使用的标签，因此从结构体开头计算偏移字节非常重要。这些偏移用于访问设备内存。因此，使用 `scalex_area + 4` 代替 `scalex_area.readin`。由于该结构体的所有组件均为 4 字节大小，因此计算中没有技巧可言。

程序 11.9

```
struct cq_struct
{
    unsigned long flags; /* 0 */
    unsigned int readin; /* 4 */
    unsigned int readout; /* 8 */
    unsigned int writein; /* 12 */
    unsigned int writeout; /* 16 */
    char *read_buffer; /* 20 */
    char *write_buffer; /* 24 */
    struct wait_queue *rdwait_q; /* 28 */
    struct wait_queue *wrwait_q; /* 32 */
};
```
