
S5, ... T `/etc/modules.conf`

S5, ... T `/etc/modules.conf`

M, ... e `/etc/permissions`

M, ... e `/etc/permissions.easy`

M, ... e `/etc/permissions.paranoid`

M, ... e `/etc/permissions.secure`

T5, ... T `/etc/modules.conf`

S,, ... / /etc/mot.

,, ... / ////.

,,, / / ///..

,, e / ///..

5, ... T `/etc/stab.conf`

T,, ... / ///..

,,,, / / /////.,,,,,, / ///.

S5, ... T `/etc/modules.conf`

S5, ... T `/etc/modules.conf`

M, ... e `/etc/permissions`

M, ... e `/etc/permissions.easy`

M, ... e `/etc/permissions.paranoid`

M, ... e `/etc/permissions.secure`

T5, ... T `/etc/modules.conf`

S,, ... / /etc/mot.

,,, ... / /////.

,,,, / ////.

,,,,,/////

,,,,,,,,///,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,/,,,,,,,,,,,,,,,,,//////

,,,,, / /////..

,, ... / / ////.,

,,,,,,,////,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,,

,,,,, / /////.

,,, ... / / / ////.,

,,,, / / ////.

```
（注：此处忽略错误的输出乱码）
```

第三次调用验证已安装的包与包文件。下面的对话框显示了更多详细信息：

```
stimpy $ rpm -vv -vp /root/DOWNLOADS/bind.rpm

D: opening database mode 0 in /var/lib/rpm/

D: Reader signature

D: Signature pad: 72

D: size: 68

D: Header + Archive: 1046019

D: 1046019

D: expected size:

D: dependencies: looking for bndutil

D: dependencies: looking for /bin/sh

D: dependencies: looking for /bin/sh

D: dependencies: looking for ld-linux.so.2

D: dependencies: looking for libc.so.6

D: dependencies: looking for libc.so.6(GLIBC_2.0)

D: dependencies: looking for libc.so.6(GLIBC_2.1)

D: dependencies: looking for bind

stimpy $
```
