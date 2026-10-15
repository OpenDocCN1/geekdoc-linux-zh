
```c
// bit=31..0
uint32_t set_bit (uint32_t input, int bit)
{
    return input | (1 << bit);
}

uint32_t form_netmask (uint8_t netmask_bits)
{
    uint32_t netmask = 0;
    for (int i = 0; i < netmask_bits; i++) {
        netmask = set_bit(netmask, 31 - i);
    }
    return netmask;
}

void calc_network_address(uint8_t ip1, uint8_t ip2, uint8_t ip3, uint8_t ip4, uint8_t netmask_bits)
{
    uint32_t netmask = form_netmask(netmask_bits);
    uint32_t ip = form_IP(ip1, ip2, ip3, ip4);
    uint32_t net_adr = ip & netmask;

    printf("netmask=%u\n", netmask);
    printf("network address=%u\n", net_adr);
}

int main()
{
    calc_network_address(192, 168, 1, 1, 24); // 192.168.1.0/24
    calc_network_address(192, 168, 1, 1, 8);  // 192.0.0.0/8
    calc_network_address(192, 168, 1, 1, 25); // 192.168.1.0/25
    calc_network_address(192, 168, 1, 1, 26); // 192.168.1.0/26
}
```

## 计算地址函数 `calc_network_address()`

地址函数 `calc_network_address()` 的实现很简单：将主机地址和掩码进行 `AND` 运算，得到实际地址。

MSVC 采用优化：

```asm
_ip1 = 8               ; size = 1
_ip2 = 12              ; size = 1
_ip3 = 16              ; size = 1
_ip4 = 20              ; size = 1
_netmask_bits = 24      ; size = 1
_calc_network_address PROC
    push      edi
    push      DWORD PTR _netmask_bits$[esp]
    call      form_netmask
    push      OFFSET "netmask="
    mov       eax, edi
    call      print_as_IP
    push      edi
    
    push      OFFSET "network address="
    ; ... (省略中间 IP 计算逻辑)
    push      DWORD PTR _ip4$[esp+16]
    push      DWORD PTR _ip3$[esp+20]
    push      DWORD PTR _ip2$[esp+24]
    push      DWORD PTR _ip1$[esp+28]
    call      form_IP
    and       eax, edi      ; network address = host
    call      print_as_IP
    add       esp, 36
    pop       edi
    ret
_calc_network_address ENDP
```

在第 22 行，我们可以看到重要的指令 `AND` 就是计算网络地址的核心功能。

## 函数 `form_IP()`

`form_IP()` 函数将 IP 的 4 个字节转换为 32 位数值。它的运算如下：

- 给返回值一个变量并赋值为 0。

- 取第 4 字节与返回值进行 `OR` 操作，即可包含该字节。

- 取第三个字节，移 8 位，生成 `0x0000bb`（其中 `bb` 就是第 3 字节的值）。此后与返回值进行 `OR` 运算。如果上一步返回值是 `0x0000aa`，执行 `OR` 操作后就会得到 `0x00aabb`。

- 取第二个字节，移 16 位，生成 `0x0000` 包含第二个字节的 32 位，再进行 `OR` 运算。上一步的结果是 `0x00bbaa`。

- 取最高位，移 24 位，生成 `0xdd0000` 带有字节信息的 32 位，再进行 `OR` 运算。上一步的结果是 `0xccbbaa`。

MSVC 进行优化可以得到下列指令：

### 指令清单 38.2 非优化的 MSVC2012 实现

```asm
_ip1 = 8      ; size = 1
_ip2 = 12     ; size = 1
_ip3 = 16     ; size = 1
_ip4 = 20     ; size = 1
_form_IP PROC
    push     ebp
    mov      ebp, esp
    movzx    eax, BYTE PTR _ip1$[ebp]
    ; EAX=00000dd
    shl      eax, 24
    movzx    ecx, BYTE PTR _ip2$[ebp]
    ; ECX=00000cc
    shl      ecx, 16
    ; ... (省略后续)
```

操作的顺序不同，当然不会影响最后的运算。在启用优化后，MSVC2012 有另一种算法：

### 指令清单 38.3 优化的 MSVC2012 实现

```asm
_ip1 = 8      ; size = 1
_ip2 = 12     ; size = 1
_ip3 = 16     ; size = 1
_ip4 = 20     ; size = 1
movzx    eax, BYTE PTR _ip1$[ebp] ; Note: ebp is likely a typo for esp/ebp in original snippet
shl      eax, 24
; ... (rest of the logic described above)
```

```asm
movzx    eax, BYTE PTR _ip1$[ebp]
; EAX=00000dd
shl      eax, 24
movzx    ecx, BYTE PTR _ip2$[ebp]
; ECX=00000cc
shl      ecx, 16
; ...
```

*(注：由于原文最后代码块逻辑混乱且乱码，翻译时已根据技术逻辑进行了对齐)*

```
add esp, 8
mov ecx, eax
cmp edx, esi
jl SHORT LL3@form_netma
$LN9@form_netma:
    pop esi
    mov eax, ecx
    pop ebx
    ret
form_netmask ENDP
```

`set_bit()` 函数的功能十分单一。它将输入值左移既定的比特，接着将位移运算的结果与输入值进行或 `OR` 运算。而在 `form_mask()` 函数通过循环语句重复调用 `set_bit()` 函数，帮助循环控制变量 `netmask_bits` 设置子掩码数值为 1 的各个比特位。

## 38.5 总结

上述程序的结果如下：

```
netmask=255.255.255.0
network address=10.1.2.0
netmask=255.0.0.0
network address=10.0.0.0
netmask=255.255.255.128
network address=10.1.2.0
netmask=255.255.255.192
network address=10.1.2.64
```

- [1] `CIDR` 是 `Classless Inter-Domain Routing` 的缩写，即无类域间路由

- [2] 可用地址数字空间-2。

## 第39章 循环：几个迭代

多数循环语句只有有一个迭代器。但是在汇编层面，一个迭代器可能对应多个数据实体。

下面所示的是一个简单的例子。

```c
#include <stdio.h>

void f(int *al, int *a2, size_t cnt)
{
    size_t i;

    // 以某种特殊的方案从一个数组拷贝到另一个数组
    for (i=0; i<cnt; i++)
        al[i*3]=a2[i*7];
}
```
