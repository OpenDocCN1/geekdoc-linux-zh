# OffSec

Penetration Testing with Kali Linux

Because this binary is cross-compiled to Windows, we cannot simply run it from our Kali machine. We'll need to use wine, which is a compatibility layer used for running Windows applications on other operating systems like Linux, BSD, and macOS.

```
kali@kali:~/Desktop sudo wine synbreeze_exploit.exe

[>] Initialising Winsock...
[]> Initialised.
[]> Socket created.
[>] Connected
```

[>] Request sent

Listing 325 - Running the Windows exploit using wine

Surprisingly, we hit our breakpoint at all. Instead, the application crashes and the EIP register seems to be overwritten by `0x9010090c`.

![](bbox=[0.125, 0.353, 0.875, 0.753])

Access violation when executing ... use Shift+F7/F8/P9
Figure 25: EIP is overwritten by our return address instruction misaligned by one byte

By analyzing the value stored in EIP (0x9010090c) and the buffer sent to the stack, we'll notice that our offset to overwrite the return address on the stack seems to be

> 694 (WineHQ, 2022), https://www.winehq.org/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

442