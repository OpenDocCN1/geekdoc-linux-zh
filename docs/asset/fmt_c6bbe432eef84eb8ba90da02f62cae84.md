
指定的到 X 服务器的连接。

指定的 GC。

# 图形批处理

如果你扩展 X 以添加更多多形基元（poly primitives），你可能利用库中的功能，允许连续的单次调用转换为多形请求。这可能会显著提高未使用多形请求编写的程序的性能。`display` 结构中名为 `last req` 的 Xreq 指针是正在处理的最后一个请求。通过检查最后一个请求类型、drawable、gc 以及其他选项与新请求相同，并且缓冲区留有足够的空间，你可能可以通过扩展请求长度并将数据附加到缓冲区来扩展之前的请求。这在游戏中可以提高五倍或以上的性能。例如，这里是 `XDrawPoint` 存根的源码（扩展存根将在下一节讨论）。

```c
#include <X11/Xlib.h>

/* 预计算允许的批请求的最大大小 */

static int size = sizeof(XPointReq) * sizeof(XPoint);

XDrawPoint(dpy, d, gc, x, y)

    register Display *dpy;

    Drawable d;

    GC gc;

    int x, y; // INT16 */

{

    XPoint *point;

    LockDisplay(dpy);

    FlushGC(dpy, gc);

    register XPointReq *req = (XPointReq *) dpy->last_req;

    /* 如果与之前的请求具有相同的 drawable，则批处理请求 */

    if (

        (req->reqType == X_PolyPoint)

        && (req->drawable == d)

        && (req->gc == gc->gid)

        && (req->codeMode == CoordOrigin)

        && ((dpy->bufptr + sizeof(XPoint) <= dpy->bufmax) )

        && ((char *)dpy->bufptr - (char *)req < size) )

            point = (XPoint *)dpy->bufptr;

            req->length += sizeof(XPoint) >> 2;

            dpy->bufptr += sizeof(XPoint);

}

else {

    GetReqExtra(PolyPoint, 4, req); /* 1 个点 = 4 字节 */

    req->drawable = d;

    req->gc = gc->gid;

    req->codeMode = CoordOrigin;

```
```
point = (xPoint *) (req + 1);
}
point->x = x;
point->y = y;
}
UnlockDisplay(dpy);
SyncHandle();
```
为了防止客户端生成可能垄断服务器的极长请求，`<X11/Xlibint.h>` 中定义了一个符号 `EPERBATCH`，表示批处理的请求数量。大多数性能收益发生在前几个合并的请求中。请注意，在获取 `last_req` 的值之前调用了 `FlushGC`，因为它可能会修改此字段。

# 扩展 X 存根

所有的 X 请求始终包含请求长度，表示为 32 位宽的 16 位数值。这意味着单个请求的长度不会超过 256K。某些服务器可能不支持这种长度的请求。`dpy->max_req_size` 的值包含最大长度。（此处省略重复内容）

（注：提供的 OCR 文本存在大量重复且损坏，我将根据有意义的部分提供清理后的版本。）

```c
typedef struct _DoSomethingReply {

  BYTE type; /* 总是 X_Reply */

  BYTE someDatum; /* 在不同请求中使用不同 */

  CARD16 sequenceNumber; /* 目前为止发送的请求数 */

  CARD32 length; /* 额外的字节数，除以 4 */

  /* 请求特定数据 */

} xDoSomethingReply;
```

这些回复结构的大部分长度为 32 字节。如果回复值不多，它们将包含足够数量的字段（pad fields）以补齐到 32 字节。`length` 字段是请求总字节数减去 32 后除以 4。只有在以下情况下该值为非零：

- 回复结构后面紧跟变长数据，例如列表或字符串。
- 回复结构长于 32 字节。

在核心协议中，只有 GetWindowAttributes、QueryFont、QueryKeymap 和 GetKeyboardControl 的回复结构不是由 32 字节组成的。

少数协议请求返回的回复不包含数据。`<X11/Xproto.h>` 并没有为这些请求定义回复结构。相反，它们使用 `XGenericReply` 结构，该结构只包含类型、长度和序列号（以及足够的填充以使其达到 32 字节长度）。

# 开始编写存根过程

一个 Xlib 存根过程应该如下所示：

```c
#include "X11/Xlibint.h>

XDoSomething(arguments,  ...)

/* 参数声明 */

register XDoSomethingReq *req;

...
```
如果协议请求有回复，那么变量声明应该包含该请求的回复结构。以下是一个示例：

```c
xDoSomethingReply rep;
```

# 锁定数据结构

对于希望支持对单个显示连接进行多线程访问的系统，每个存根过程都需要锁定其临界区域。

# 扩展

通常，此部分是指从 `GetReq` 调用之前一直直到所有调用参数都存储到缓冲区中的点。实现此锁定所需的精确指令取决于机器架构。提供了两个调用，它们通常以宏的形式实现。

```c
LockDisplay(display);
```

```c
UnlockDisplay(display);
```

`display` 指定到 X 服务器的连接。

# 发送协议请求和参数

在变量声明之后，存根过程应该调用 `<X11/Xlib.h>` 中定义的四个宏之一：`GetReq`、`GetReqExtra`、`GetResReq` 或 `GetEmptyReq`。所有这些宏的第一个参数都是协议请求名称在 `<X11/Xproto.h>` 中声明（除 X 除外）。每个宏都声明了一个名为 `dpy` 的结构指针和一个指向适当类型的请求结构指针 `req`。然后，该宏根据请求结构询问输出缓冲区，填充其类型和长度字段，并将 `req` 指向该位置。

如果协议请求没有参数（例如 XGrabServer），则使用 `GetEmptyReq`。

```c
GetEmptyReq (DoSomething, req);
```

如果协议请求有一个单一 32 位参数（例如 Pixmap、Window、Drawable、Atom 等），则使用 `GetResReq`。宏的第二个参数是该 32 位对象。`XMapWindow` 是一个很好的例子。

```c
GetResReq (DoSomething, rid, req);
```

`rid` 参数是 Pixmap、Window 或其他资源 ID。

如果协议请求接受任何其他参数列表，则调用 `GetReq`。在 `GetReq` 之后，你需要设置请求结构中的所有字段，通常来自存根过程的参数。

```c
GetReq (DoSomething, req);

/*在此处填充参数 */

req->arg1 = arg1;

req->arg2 = arg2;
```

少数存根过程（例如 XCreateGC 和 XPixmap）向调用者返回资源 ID，但作为协议请求的参数。此类过程使用宏 `XAllocID` 从该客户端打开连接时分配给它的 ID 范围中分配一个 ID。

```c
rid = req->rid = XAllocID();
```

# 扩展

```c
return (rid);
```
