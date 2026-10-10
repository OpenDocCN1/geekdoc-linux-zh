
```c
/* protocol.h */	yped enum {OOBPrint = UINT32_C(0), OOBAssert} OOBType;

#define LIST(...) List, ... __VA_ARGS__, N1

#define PUT LIST(is_oob, ...) (put_va(is_oob, LIST( __VA_ARGS__)))

#define OOB_PRINT(fmt, ...) ({	PUT_LIST(true, UInt32, OOBPrint, CString, fmt, __VA_ARGS__); \
})\tsend_msg(MTOOB));
```

```c
/* main.c */

void kmain() {

  setup_serial();

  OOB_PRINT("kmain at 0x%016x", Uint64, &kmain);

  asm __volatile__("hlt");

}
```

```bash
(root@ghg6:~ /labs/lab2)
# gnu-system-x86_64 -display name -boot -cdrom kernel_bios.iso -m 300M
-serial stdio -enable-kv | stdbuf -o hexdump -C | cut -d' ' -f3-
03 03 00 00 32 00 00 00 2f c9 e6 6a 3a 37 16 e8 | ....2../.j7.
00 06 00 00 04 04 00 00 00 00 00 00 00 05 00 00 |
6b 6d 61 69 6e 26 61 74 20 30 78 25 30 31 36 66 | kmain at 0x%016x
78 08 00 00 20 00 00 00 35 14 40 00 00 00 00 07 | x....5.@..|
```

# 启动消息实现

- 物理地址空间（从在 VM 中运行的内核的角度来看）。这起有两个作用：
- 内核地址（符号）。第一个作用是让客户端知道内核加载的位置，这样它在注入代码时就不会意外地覆盖内核。第二个作用是提供已知内核函数的地址，以供外部代码调用。

启动消息的信息将编码在一个关联列表（associative list）中，其中每对的第一个元素是第二个元素内容的标识字符串。第二个元素的布局取决于所提供信息的类型（通常被编码为子列表）。在这种情况下，我们将使用字符串“symbols”和“mmap”来标记信息。

构建“symbols”非常简单；我们只需要将符号名称及其地址构造为一个关联列表：

```c
#define NAMED(n, t, v) LIST(CString, n, t, v)

#define SYMBOL(n) NAMED (#n, UInt64, &n)

extern char __ehdr_start, _end;

static void put_symbols() {
  PUT_LIST(false, CString, "symbols",
    LIST(SYMBOL(_ehdr_start), SYMBOL(_end),
    SYMBOL(put_va), SYMBOL(send_msg)));
}
```

在这种情况下，我们提供了内核的 ELF 头、BSS 段的末尾以及 `put_va` 和 `send_msg` 函数的地址。

为了构建“mmap”，我们将修改引导代码，以利用 GRUB 提供的多重引导信息（MBI）区域：

```asm
[bits64]
code64:
... 为了简洁起见已省略
mov rdi, rbx ; MULTIBOOT_MBI_REGISTER
call kmain
```

`kmain` 的定义必须经过调整，以接受 MBI 作为参数。我们还将添加构建并发送启动消息的代码：

```c
void kmain(const void *mbi) {
  setup_serial();
  OOB_PRINT("kmain at 0x%0161x", Uint64, &kmain);
  put_tp(false, List);
  put_symbols();
  put_mbi(mbi);
  put_tp(false, Nil);
  send_msg(MTBoot);
}
```

最后一部分是 `put_mbi` 函数，用于解析 MBI 并构造“mmap”：

```c
#include "multiboot.h"

#define PTR_ADD(a, s) ((type)(a))((unsigned long)a + s))
#define ALIGN_UP(a, s) ((a + (type)(a))s - 1) & ((type)(a)s - 1))

static void put_mmap(const struct multiboot_tag_mmap *mmap) {
  const struct multiboot_mmap_entry *entry, *end;
  end = PTR_ADD(&mmap->entry, mmap->size - sizeof(*mmap));
  put_tp(false, List);
  for (entry = &mmap->entries[0]; entry != end; entry = ) {
    entry = PTR_ADD(entry, mmap->entry->size);
    PUT_LIST(LIST,
      NAMED("address", Uint64, entry->addr),
      NAMED("length", Uint64, entry->len),
      NAMED("type", Uint32, entry->type));
    put_tp(false, Nil);
  }
}

static void put_mbi(const void *mbi) {
  const struct multiboot_tag *tag;
  for (tag = PTR_ADD(mbi, ALIGN_UP(sizeof(uint64_t)), MULTIBOOT_TAG_ALIGN));
  tag->type != MULTIBOOT_TAG_TYPE_END;
  tag = PTR_ADD(tag, ALIGN_UP(sizeof(uint64_t)), MULTIBOOT_TAG_ALIGN));
  tag->type != MULTIBOOT_TAG_TYPE_END;
  switch (tag->type) {
    case MULTIBOOT_TAG_TYPE_MMAP:
      put_mmap((const struct multiboot_tag_mmap *)tag);
      break;
    default:
      break;
  }
}
```
*(注：由于原文提供的代码片段 `put_mbi` 存在逻辑重复和截断，翻译时已保持其逻辑结构并对明显的语法断裂进行了对齐处理以确保可读性)*

与 C 的实现相同的顺序，我们将定义 TP 值和原语（整数）：

```
TP = c.Enum(cInt32, Uint8=0x001, Uint16=0x002, Uint32=0x004, Uint64=0x008, Int8=0x010, Int16=0x012, Int32=0x104, Int64=0x108, Arrays=0x400, CString=0x500, List=0x600, Nil=0x700)
IntPrefixes = (TP.Uint8, TP.Uint16, TP.Uint32, TP.Uint64, TP.Int8, TP.Int16, TP.Int32, TP.Int64)
IntConstructs = (c.Int8ul, c.Int16ul, c.Int32ul, c.Int64ul, c.Int8sl, c.Int16sl, c.Int32sl, c.Int64sl)
Fixed = (f.Uint8, f.Uint16, f.Uint32, f.Uint64, f.Int8, f.Int16, f.Int32, f.Int64)
def make_adapter(cInt, fInt):
    return c.ExprSymmetricAdapter(cInt, lambda obj, _: fInt(obj))
```

```
IntAdapters = (make_adapter(cInt, fInt) for cInt, fInt in zip(IntConstructs, IntAdapters))
IntList = list(zip(IntPrefixes, IntAdapters))
```
