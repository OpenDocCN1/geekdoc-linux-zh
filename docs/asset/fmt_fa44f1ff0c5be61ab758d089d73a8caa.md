
此示例选择接收第一条可用消息，而不考虑类型（参数 `msgtyp` 等于 0）。`msz` 的值计算结果包含了接收结构体的最大大小，但不包含 `msg.type` 的大小。

## 应用消息队列

这里介绍使用消息队列的客户端和服务器程序。客户端发布请求，服务器接收消息并响应。客户端仅执行 `stat(2)` 或 `lstat(2)` 调用，并通过消息将结果返回给客户端。

客户端和服务器程序使用已创建的 C++ 对象，使得消息队列的使用更加方便。首先将介绍该 C++ 对象及其实现。

列表 23.1 显示了文件 `msg.h`，它定义了 C++ 类 `Msq`。

### 列表 23.1. `msq-Msq` 类定义文件

```cpp
// msg.h :

//

// 消息队列:

#include <sys/types.h>
#include <sys/ipc.h>
#include <sys/msg.h>

struct msq {
    long mtype;
};

class Msq {
    enum state { ready, notready };
    key_t key;
    int msqid;
    int error;

protected:
    void _verify(state s);

public:
    Msq();
    int create(key_t key, int flags);
    int access(key_t key);
    int destroy();
    int stat(struct msq *buf);
    int change(int flags);
    int send(const void *msgsp, size_t msgs, long msgtype, int flags);
    int recv(void *msgsp, size_t mgsz, long msgtyp, int flags);

    inline int getError() { return error; }
    inline key_t getKey() { return key; }
};
// End Msq
```

行 9-36 定义了 C++ 类 `Msq`。

`Msq` 类维护 `key`、`msqid` 和最后的 `error`。`getError()` 和 `getKey()` 方法访问这些值。`_verify()` 方法检查状态。如果状态不正确，将抛出错误 `EINVAL`。

默认构造函数创建未就绪的 `Msq` 对象。除了 `Msq::send()` 和 `Msq::recv()` 方法外，它们期望对象处于就绪状态。`Msq::create()` 创建一个新的消息队列。而 `Msq::access()` 则尝试访问已有的消息队列。

`Msq::dispose()` 将对象初始化为未就绪状态。`Msq::destroy()` 方法销毁消息队列，然后调用 `Msq::dispose()` 初始化对象为未就绪状态。

`Msq::stat()` 允许调用者获取有关消息队列的信息。`Msq::change()` 方法允许修改队列参数。

`Msq::send()` 和 `Msq::recv()` 是 `msnd(3)` 和 `msgrcv(3)` 的封装函数。它们提供了在接收到信号时处理 `EINTR` 错误的额外功能。

现在查看列表 23.2。

### 列表 23.2. `msqveri.cc` - `Msq::_verify()`, `Msq::dispose()` 和构造函数 `Msq::Msq()` 的实现

```cpp
// msqveri.cc :
#include <stdlib.h>
#include <errno.h>
#include "msq.h"

// (private) Msq::_verify :
// 检查对象是否处于就绪或未就绪状态。
// 如果状态不正确，则抛出错误 EINVAL。

void
Msq::_verify(state s) {
    if (s == ready && msqid < 0 )
        throw error = EINVAL; // 对象未打开
    if (s != ready && msqid >= 0 )
        throw error = EINVAL; // 对象已打开
}

// Msq::dispose :
// 释放当前消息队列（如果有）。
// 对象重新初始化为未就绪状态。

Msq & 
Msq::dispose() {
    key = IPC_PRIVATE;
    msqid = -1;
    return *this;
}

// Msq::Msq :
// 构造函数。该构造函数调用方法 Msq::dispose()
// 来初始化对象。

Msq::Msq() {
    dispose();
}
```

```cpp
Msq::Msq() {
    Msq::dispose();      // 初始化此对象
}

// End msqveri.cc
```

`Msq::verify()` 方法使用枚举数据类型状态作为其参数 `s`。当 `s` 不等于 `ready` 时，私有成员 `msqid` 必须小于零，以表示对象处于就绪状态。如果此测试失败，将在第 18 行抛出错误 `EINVAL`。所有错误都保存在私有成员中供检索。

当 `s` 不等于 `ready` 时，如果测试显示对象当前在私有成员 `msqid` 中持有一个有效的 IPC ID（第 19 和 20 行），则抛出 `EINVAL`。

`Msq::dispose()` 函数将对象初始化为未就绪状态（第 34 和 35 行）。默认构造函数 `Msq::Msq()` 简单地调用 `Msq::dispose()` 来初始化对象。

列表 23.3 显示了 `Msq::create()` 方法的实现。

### 列表 23.3 `msqcr.cc` `Msq::create()` 方法的实现

```cpp
// msqcr.cc

#include <stdlib.h>
#include <errno.h>
#include "msq.h"

///////////////////////////////////////////////////////////////////
// Msq::create : 
// 参数:
//     IPC_PRIVATE
//     // key         消息队列或 IPC 队列的 IPC Key
//     // flags      权限位，可能包含 IPC_EXCL
//
// 此方法创建一个消息队列。对象必须处于
// 未就绪状态。
/////////////////////////////////////////////////////////////////

Msq &
Msq::create(key_t key, int flags) {

    _verify(notReady); // 对象必须未打开状态

    flags = IPC_CREATE; // 强制执行格式语义

    /*
         * 尝试创建消息队列：
     */
    msqid = msq_get(this)->key = key, flags);
    if (msqid == -1)
        throw error = errno;

    return *this;
}
// End msqcr.cc
```

与 `Msq` 类中的许多方法一样，对象的状态首先会进行测试（第 21 行）。由于此方法意味着创建消息队列，因此在第 23 行将标志 `IPC_CREAT` 与 `flags` 参数进行按位或。第 28 行调用 `msget(3)` 来创建队列。除非 `flags` 参数包含了 `IPC_EXCL`，否则 `Msq::create()` 方法在队列已存在时将返回错误消息。如果遇到错误，将在第 30 行返回。

列表 23.4 显示了 `Msq::access()` 方法的实现。

### 列表 23.4 `msqac.cc` - `Msq::access()` 方法的实现

```cpp
// msgac.cc

#include <stdlib.h>
#include <errno.h>
#include "msgq.h"

///////////////////////////////////////////////////
// Msq::access :

// 参数:
// key 消息队列的 IPC Key 或 IPC_PRIVATE

// 此方法访问消息队列。对象必须处于
// 未就绪状态。

//////////////////////////////////////////////////////
Msq &
Msq::access(key_t key) {

_verify(notReady); // 对象必须未打开状态

/*
* 尝试创建消息队列：
*/
msqid = msgget(this->key = key,0);
if (msqid == -1)
throw error = errno;


return *this;
}
// End msqac.cc
```

`Msq::access()` 与 `Msq::create()` 方法非常相似。注意，`msgget(3)` 函数调用（第 25 行）中的 `flags` 参数值为 0，表示消息队列必须已经存在。

列表 23.5 显示了 `Msq::destroy()` 方法的实现。

### 列表 23.5 `msqdest.cc` - `Msq::destroy()` 方法的实现

```cpp
// msqdest.cc

#include <stdlib.h>
#include <errno.h>
#include "msgq.h"
///////////////////////////////////////////////////////////////////////////////////
// Msq:destroy. 对象必须处于
//
//
// 销毁消息队列。
// 就绪状态。完成后对象被置于未就绪
// 状态。/////////////////////////////////////////////////////////////////////
// Msq &
Msq::destroy() {
_verify(ready); // 对象必须打开

if (msgctl(msqid,IPC_RMID,0) == -1)
throw error = errno;
Msq::dispose(); // 重新初始化对象
return *this; // 以未就绪状态返回
{}
// End msq.cc
```

`Msq::destroy()` 方法在第 20 行使用命令 `IPC_RMID` 调用 `msgctl(3)`。如果成功，则在第 23 行调用 `Msq::dispose()` 将对象初始化回就绪状态。

列表 23.6 说明了 `Msq::stat()` 方法，它从内核获取消息队列状态。

### 列表 23.6 `msqstat.cc` - `Msq::stat()` 方法

```cpp
// msqstat.cc

#include <stdlib.h>
#include <errno.h>
#include "msgq.h"
///////////////////////////////////////////////////////
// Msq::stat :
//
// 参数:
// msqid_ds 结构，用于填充
// buf 消息队列信息。
//
// 此方法填充缓冲区以关于当前
// 队列的状态。对象必须处于
// 就绪状态。/////////////////////////////////////////////////////
//
msqid_ds &
Msq::stat(msqid,msqid_ds &stbuf) {

_verify(ready); // 对象必须打开

if ( msgctl(msqid,IPC_STAT,&stbuf) == -1)
throw error = errno;
return stbuf;
}
// End msqstat.cc
```

在 `Msq::stat()` 方法中，使用命令 `IPC_STAT` 调用 `msgctl(3)`，参数 `stbuf` 以引用传递，因此当没有遇到错误时返回 `stbuf`。

列表 23.7 显示了 `Msq::change()` 方法的实现。使用此方法可以更改所有者、组和权限位。

### 列表 23.7 `msgchg.cc` - `Msq::change()` 方法的实现

```cpp
// msgchg.cc

#include <stdlib.h>
#include <errno.h>
#include "msg.h"
///////////////////////////////////////////////////////

// Msg::change :

// 参数:
// stbuf msqid_ds 结构，包含
//             要做的更改。
// 只有 msg_perm.uid, msg_perm.gid, msg_perm.mode
// 和 msg_qbytes 值可以更改。
// msg_qbytes 值只能由超级用户增加。
// 对象必须处于就绪状态。

/////////////////////////////////////////////////////
// Msq &
// Msg::change(msqid_ds &stbuf) {

    _verify(ready); // 对象必须打开

    if (msgctl(msqid,IPC_SET, &stbuf) == -1 )
        throw error = errno;

        return *this;
    }

// End msgchg.cc
```

函数 `msgctl(3)` 在 `Msg::change()` 中通过引用传递参数 `stbuf` 调用。

`Msg::send()` 的实现见列表 23.8。

### 列表 23.8 `msgsend.cc` - `Msq::send()` 方法的实现

```cpp
// msgsend.cc :
#include <stdlib.h>
#include <errno.h>
#include <msq.h>
/
///////////////////////////////////////////////////////////////////
// Msgsnd::send :
/
/
// 参数:
// msq 要发送的消息
// size 消息的总大小
// flags zero 或 IPC_NOWA (可选)
//
// 返回:
// 0 未发送消息（带有 IPC_NOWA）
// 1 消息已发送
//
// 将字节发送到消息队列。
// size 必须包含消息的总大小，
// 包括消息类型。对象必须处于
// 就绪状态。
/////////////////////////////////////////////////////////////////

int
Msgsnd::send(Msgsq, &msg, size_t size, int flags) {
int z;
size_t msgsz = size - sizeof(msg_type);

// verify(ready);

do
z = msgsnd(msqid, &msgsz, flags);
} while (z == -1 && errno == EINTR);
```
