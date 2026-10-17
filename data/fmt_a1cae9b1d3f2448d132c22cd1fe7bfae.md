
| `0x000089F5` | `EQL_SETMASTRCFG` | `struct ifreq` // MORE // I-O |

`<include/linux/ifpip.h>`

| `0x000089F0` | `SIOCDEVPLIP` | `struct ifreq` // I-O |

## 第二部分：系统调用

`<include <linux/ifppp.h>`

| 地址 | 常量 | 类型 |
| :--- | :--- | :--- |
| `0x00005490` | `PPPIOCFLAGS` | `int *` |
| `0x00005491` | `PPPIOCSFLAGS` | `const int *` |
| `0x00005492` | `PPPIOCASYNMAP` | `int *` |
| `0x00005493` | `PPPIOCASYNMAP` | `const int *` |
| `0x00005494` | `PPPIOGUNIT` | `int *` |
| `0x00005495` | `PPPIOCSINSIG` | `const int *` |
| `0x00005497` | `PPPIOCDEBUG` | `const int *` |
| `0x00005498` | `PPPIOCDEBUG` | `int *` |
| `0x00005499` | `PPPIOGSTAT` | `struct ppp_stats *` |
| `0x0000549A` | `PPPIOGTIME` | `struct ppp_ddffno *` |
| `0x0000549B` | `PPPIOCASYNMAP` | `struct int[8] *` |
| `0x0000549C` | `PPPIOCASYNMAP` | `const int[8]; *` |
| `0x0000549D` | `PPPIOGMRU` | `const int *` |
| `0x0000549E` | `PPPIOCRASYNMAP` | `const int *` |
| `0x0000549F` | `PPPIOCXAXCID` | `const int *` |

`<include <linux/itpx.h>`

| 地址 | 常量 | 类型 |
| :--- | :--- | :--- |
| `0x0000B9E0` | `SIOCAPXFTCR` | `const char *` |
| `0x0000B9E1` | `SIOCAPXPRLIST` | `const char *` |
| `0x0000B9E2` | `SIOCIFXGFDATA` | `struct ipx_config_data *` |

`<include <linux/kd.h>`

| 地址 | 常量 | 类型 |
| :--- | :--- | :--- |
| `0x00004B60` | `GIO_FONT` | `struct char[8192] *` |
| `0x00004B61` | `P1_FONT` | `const char[8192] *` |
| `0x00004B6B` | `GIO_FONTX` | `struct console_font_desc *` // I-O |
| `0x00004B6C` | `P1_FONTX` | `struct console_font_desc *` // |
| `0x00004B70` | `GIO_MAP` | `struct char[48] *` |
| `0x00004B71` | `P1_MAP` | `const char[48] *` |
| `0x00004B2F` | `K1OCSOUND` | `int` |
| `0x00004B30` | `KDMTONE` | `int` |
| `0x00004B31` | `KGETLED` | `char *` |
| `0x00004B32` | `KOSETLED` | `int` |
| `0x00004B33` | `KDGKBTYPE` | `char *` |
| `0x00004B34` | `KDADDIO` | `int` // |
| `0x00004B35` | `KDDELIO` | `int` // |
| `0x00004B36` | `KDENABIO` | `void` // |
| `0x00004B37` | `KDDISABIO` | `void` // |
| `0x00004B3A` | `KOSETMODE` | `int` |
| `0x00004B3B` | `KODGETMODE` | `int *` |
| `0x00004B3C` | `KDMAD1ISP` | `void` // |
| `0x00004B30` | `KDUNMAPDIS` | `void` // |
| `0x00004B40` | `GIO_SCRMAP` | `struct char[E_TABSZ] *` |
| `0x00004B41` | `PIO_SCRMAP` | `const struct char[E_TABSZ] *` |
| `0x00004B69` | `GIO_UNISCRMAP` | `struct short[E_TABSZ] *` |
| `0x00004B6A` | `PIO_UNISCRMAP` | `const struct short[E_TABSZ] *` |
| `0x00004B66` | `GIO_UNIMAP` | `struct unimapdesc *` // I-O |
| `0x00004B67` | `PIO_UNIMAP` | `const struct unimapdesc *` // |
| `0x00004B68` | `PIO_UNIMAPLR` | `const struct unimapint *` |
| `0x00004B44` | `KDKGBMODE` | `int *` |
| `0x00004B45` | `KDSBMODE` | `int *` |
| `0x00004B62` | `KDBNETA` | `int *` |
| `0x00004B63` | `KDSBNETA` | `int *` |
| `0x00004B64` | `KDBBLED` | `int *` |
| `0x00004B65` | `KDSBLED` | `int *` |
| `0x00004B46` | `KDBGENT` | `struct kbentry` // I-O |
| `0x00004B47` | `KDSBENT` | `struct kbentry *` |
| `0x00004B48` | `KDBGSENT` | `struct kbentry` |
| `0x00004B49` | `KDSBSENT` | `struct kbentry *` |
| `0x00004B4A` | `KDBDIACRS` | `struct kbdiacrs *` |
| `0x00004B4B` | `KDSDIACRS` | `struct kbdiacrs *` |
| `0x00004B4C` | `KDBKEYCODE` | `struct kbkeycode` // I-O |
| `0x00004B4D` | `KDSKEYCODE` | `struct kbkeycode *` |
| `0x00004B4E` | `KDSIGACCEPT` | `int` |

`<include <linux/ip.h>`

| 地址 | 常量 | 类型 |
| :--- | :--- | :--- |
| `0x000006B1` | `LPCHAR` | `int *` |
| `0x000006B2` | `LPTIME` | `int *` |
| `0x000006B4` | `LPABORT` | `int *` |
| `0x000006B5` | `LPSETIRQ` | `int *` |
| `0x000006B6` | `LPGETIRQ` | `int *` |
| `0x000006B8` | `LPWRIT` | `int *` |
| `0x000006B9` | `LPCAREF` | `int *` |
| `0x0000068A` | `LPABORT` | `int *` |
| `0x000006B8` | `LPGETSTATUS` | `int *` |
| `0x000006C0` | `LPSET` | `void` |
| `0x000006D0` | `LPGETSTATS` | `struct stats *` |

`<include <linux/route.h>`

| 地址 | 常量 | 类型 |
| :--- | :--- | :--- |
| `0x000089E0` | `SIOCGETVIF` | `struct sioc_if_req` // I-O |
| `0x000089E1` | `SIOCGETSG` | `struct sioc_sg_req` // I-O |

## 第二部分：系统调用

`<include <linux/mtio.h>`

| 地址 | 常量 | 类型 |
| :--- | :--- | :--- |
| `0x04806D01` | `MTIOCTOP` | `const mtop *` |
| `0x0081CD02` | `MTIOCGET` | `struct mtget *` |
| `0x00804D03` | `MTIOCOPOS` | `struct mtpos *` |
| `0x80206D04` | `MTIOCGETCONFIG` | `struct mtconfiginfo *` |
| `0x042B0D05` | `MTIOCSETCONFIG` | `const mtconfiginfo *` |

`<include <linux/netrom.h>`

| 地址 | 常量 | 类型 |
