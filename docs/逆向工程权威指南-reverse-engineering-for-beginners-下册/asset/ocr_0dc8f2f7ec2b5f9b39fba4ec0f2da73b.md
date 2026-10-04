# 指令清单21.19 WinNT.h

#include "psphack.h"/默认情况下进行4字节边界对齐

PshPack1.h文件有下列内容：

# 指令清单21.20 PshPack1.h

```
#if ! (defined(lint) || !defined(RC_INVOKED))
#if ( _MSC_VER >= 800 && !defined(_M_I86)) ||
defined(__PUSHPOP_SUPPORTED)
#pragma warning (disable:4103)
#if (!defined( MIDL_PASS )) || !defined( __midl )
#pragma pack(push,1)
#else
#pragma pack(1)
#endif
#else
#pragma pack(1)
#endif
#endif /* ! (defined(lint) || defined(RC_INVOKED)) */
```

根据#pragma pack的信息，编译器会在封装结构体时向对应的边界对齐。

现在打开OlyDbg, 加载上述默认封装格式（4字节边界对齐）的程序，如图21.3所示。