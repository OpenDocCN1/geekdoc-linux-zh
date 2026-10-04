| CIDK规范的掩码 | 数字空间 | 可用地址数（个） | 十进制子网掩码 | 十六进制子网掩码 |
| --- | --- | --- | --- | --- |
| /17 | 32768 | 32766 | 255.255.128.0 | ffff8000 |
| /16 | 65536 | 65534 | 255.255.0.0 | ffff0000 |
| /8 | 16777216 | 16777214 | 255.0.0.0 | ff000000 |

这里举一个简单的例子：将子网掩码应用到主机地址，从而计算的网络地址。

```
#include <stdio.h>
#include <stdint.h>

uint32_t form_IP(uint8_t ip1, uint8_t ip2, uint8_t ip3, uint8_t ip4)
{
    return (ip1<<24) | (ip2<<16) | (ip3<<8) | ip4;
}

void print_as_IP(uint32_t a)
{
    printf("%d.%d.%d.%d\n",
           (a>>24) & 0xFF,
           (a>>16) & 0xFF,
           (a>>8) & 0xFF,
           (a) & 0xFF);
}
```