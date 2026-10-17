
`注意`：最后一行末尾缺失的分号 `③` 并不是笔误，而是故意为之。在 Rust 中，不以分号结尾的行将从该块返回。在这种情况下，最后一行的值被放在变量 `lisp` 中。

由于 `lisp` 中的值只是指向 `PsInitialSystemProcess` 的指针，我们需要做的下一件事是利用任意读取原语获取其内部的地址：

```rust
let isp = read_ptr(hdev, lisp);
```

这使用任意内核读取来获取 SYSTEM 进程（PID 4）的 `_EPROCESS` 结构的地址。你可能想要验证该值是否正确。要这样做，请添加一个打印语句和暂停（如前所述），然后在调试器中通过命令 `dq nt!PsInitialSystemProcess L1` 转储 `PsInitialSystemProcess` 内部的值。

由于我们正在从 SYSTEM 进程令牌令牌（token），下一步是使用任意读取 `_EPROCESS` 的 `Token` 字段。此时，你应该查找从 `_EPROCESS` 结构基地址到 `UniqueProcessId`、`ActiveProcessLinks` 和 `Token` 字段的偏移。这可以在内核调试器中使用以下命令轻松完成：

```text
2: kd dt _PROCESS UniqueProcessId ActiveProcessLinks Token

nt!_PROCESS

  +0x40 UniqueProcessId : Ptr64 Void

  +0x48 ActiveProcessLinks : Ptr64 Void

  +0x50 Token : Ptr64 Void
```
