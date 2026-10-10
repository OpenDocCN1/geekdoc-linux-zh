
C 和 Perl 等效值之间的映射存储在全局变量 `callback` 中。

如果你需要随时注册一个回调，这就足够了。一个示例可以是像概述代码这样的错误处理器。尽管，反复调用 `register_fatal` 将用新函数替换之前注册的函数。

例如，你想连接到一个具有异步文件/O 的库。在这种情况下，你可能希望为每个打开的文件分离不同的 Perl 子程序。目前，处理器示例是不够的，因为它在运行时允许允许一个回调。我们需要一种方法来存储打开的文件与我们想要调用的 Perl 子程序之间的映射。

假设 I/O 库有一个 `async_read`，它将 C 函数 `ProcessRead` 与文件句柄关联——假设它也提供了一些打开文件并获取句柄的例程。

```c
async_expect(fh, ProcessRead)
```

这可能期望如下形式的 C `ProcessRead` 函数：

```c
void ProcessRead(fh, buffer) int fh; char * buffer; { ... }
```

为了给该库提供 Perl 接口，我们需要能够映射 `fh` 和我们想要调用的 Perl 子程序。哈希表是存储这种映射的方便机制。下面的代码显示了可能的实现：

```c
static HV Mapping = (SV)*NULL;
void async_read(fh, int fh SV * callback CODE:
/* 如果哈表不存在，则创建它 */
/* if
(Mapping == (SV)*NULL) Mapping = newSV();
/* 保存 fh -> callback
映射 */
/* hv_store(Mapping, (char*)fh, sizeof(of), newSVcall(callback, 0);
```
/* 与 C 库注册 */
async_read(fh, async_read_if);
而 `async_read_if` 可能如下所示

```c
static void async_read_if(int fh) {
    char * buffer;
    dSP; SV *sv;
    /* Get the callback associated with fh */
    sv = sv_fetch(Mapping, (char*)&fh, sizeof(fh), FALSE);
    if (sv == (**NULL)) croak("Internal error...");
    PUSHMARK(sp); PUSHES(sv_2mortal(newSV(sv)));
    XPUSHES(sv_2mortal(newSVbuffer, 0)));
    PUTBACK;
    /* Call the Perl sub */
    call_sv(*sv, G_DISCARD);
```

为了完整性，这里是 `async_close`。它展示了如何从哈希映射中删除该条目。

```c
void async_close(int fh) {
    /* 从哈表中删除条目 */
    (void) hv_delete(Mapping, (char*)&fh, sizeof(fh), G_DISCARD);
    /* 现在调用
    real async_close */
    async_close(fh);
}
```

Perl 接口看起来如下：

```perl
sub callback { my($handle, $buffer) = @_; }
# 注册 Perl 回调
async_read($fh, &callback);
async_close($fh);
```

C 和 Perl 之间的映射存储在全局哈希 `Mapping` 中。使用此哈希有一个明显的优势，即它允许注册无限数量的回调。

如果 C 回调提供的接口不包含允许将文件句柄映射到 Perl 子程的参数，该怎么办？例如，在异步 I/O 软件包中，回调函数只获取如下所示的参数：

```c
void ProcessBuffer(char * buffer) { ... }
```

如果没有文件句柄，就没有直接的方法从 C 映射回 Perl 子程序。

在这种情况下，绕过此问题的一种可能方法是定义一系列 C 函数作为通往 Perl 的接口，然后：

```c
#define MAX_CB 3
#define NULL_HANDLE -1
typedef void (*FMap)();
struct MapStruct {
    FMap function;
    SV * PerlSub;
    int handle;
};
static void fn1(int);
static void fn2(int);
static void fn3(int);
static struct MapStruct Map[MAX_CB] = {
    {fn1, NULL, NULL_HANDLE},
    {fn2, NULL, NULL_HANDLE},
    {fn3, NULL, NULL_HANDLE}
};
static void Pcb(int index, char * buffer) {
    dSP; PUSHMARK(sp);
    XPUSHES(sv_2mortal(newSVbuffer, 0)));
    PUTBACK;
    /* Call Perl sub */
    call_sv(*Map[index].PerlSub, G_DISCARD);
}
static void fn1(char * buffer) { Pcb(0, buffer); }
static void fn2(char * buffer) { Pcb(2, buffer); }
void array_read(int fh, SV * callback) {
    int index = MAX_CB;
    /* 寻找相同的句柄或空指针 */
    for (index = 0; index < MAX_CB; ++index) {
        if (Map[index].handle == fh) break;
    }
    if (Map[index].handle == NULL_HANDLE) {
        index = index++;
        if (index == MAX_CB) croak("Too many callbacks registered");
    }
    /* 保存文件句柄 */
    Map[index].handle = fh;
    /* 记住 Perl 子程 */
    Map[index].PerlSub = (SV*)newSV(callback);
    async_read(fh, Map[index].function);
}
void array_close(int fh) {
    int index;
    /* 寻找文件句柄 */
    for (index = 0; index < MAX_CB; ++ index) {
        if (Map[index].handle == fh) break;
    }
    if (index == MAX_CB) croak("could not close fh %d", fh);
    Map[index].handle = NULL_HANDLE;
    SVREFCNT_dec(Map[index].PerlSub);
    Map[index].PerlSub = (SV*)NULL;
    async_close(fh);
}
```
