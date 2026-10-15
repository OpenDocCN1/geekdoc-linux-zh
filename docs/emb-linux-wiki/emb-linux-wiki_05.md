
# 调试入口

主讲调试相关内容，目前主要关注内核部分的调试，后续会补充用户空间的调试内容。

# 内核调试

## Kernel Debugging

About kernel debugging tools and tips.

### Debugging by printing / Printk

> From: [eLinux.org](http://eLinux.org/Debugging_by_printing "http://eLinux.org/Debugging_by_printing")

#### Debugging by printing

Probably the simplest way to get some debug information from your kernel code is by printing out various information with the kernel's equivalent of `printf` - the `printk` function and its derivatives. The `k` in `printk` is used to specifically remind kernel developers that the environment is different.

##### Contents

- 1 Usage
- 2 Log Levels
- 3 Rate limiting and one time messages
- 4 Printk from userspace
- 5 Internals / Changing the size of the `printk` buffer
- 6 Pros and Cons
- 7 Debugging early boot problems
  - 7.1 Accessing the `printk` buffer after a silent hang on boot
    - 7.1.1 Redboot example on a Freescale ADS board
    - 7.1.2 U-boot example on an OMAP OSK board
    - 7.1.3 Grub
  - 7.2 Using `CONFIG_DEBUG_LL` and `printascii()` (ARM only)
- 8 NetConsole
  - 8.1 Netconsole resources
- 9 Misc
  - 9.1 `Dmesg` / Clearing the buffer
  - 9.2 Printk Timestamps
  - 9.3 Printing buffers as hex
  - 9.4 Dynamic Debugging
- 10 Disabling `printk` messages at compile time
- 11 References and external links

##### Usage

`printk` works more or less the same way as `printf` in userspace, so if you ever debugged your userspace program using `printf`, you are ready to do the same with your kernel code, e.g. by adding:

```
printk("My Debugger is Printk\n");
```

This wasn't that difficult, was it?

Usually you would print out some more interesting information like

```
printk("Var1 %d var2 %d\n", var1, var2);
```

just like in userspace.

In order to see the kernel messages, just use the

```
$ dmesg
```

command in one of your shells - this one will print out the whole kernel log buffer to you.

Most of the conversion specifiers supported by the user-space library routine `printf()` are also available in the kernel; there are some notable additions, including `"%pf"`, which will print the symbol name in place of the numeric pointer value, if available.

The supported format strings are quite extensively documented in [Documentation/printk-formats.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=Documentation/printk-formats.txt;hb=HEAD)

However please **note**: always use `%zu`, `%zd` or `%zx` for printing `size_t` and `ssize_t` values. `ssize_t` and `size_t` are quite common values in the kernel, so please use the `%z` to avoid annoying compile warnings.

---

**Author's practical advice:** If you want to debug an oops (e.g caused by releasing a resource twice) in your driver and you don't have a clue where the oops happens, simply add this line

```
printk(KERN_ALERT "DEBUG: Passed %s %d \n",__FUNCTION__,__LINE__);
```

after each possibly offending statement. Recompile and (re-)load the module and trigger the error condition - your log now shows you the last line that was successfully executed before the oops happened.

Of course you should **remove** these 'rude' statements before shipping your module ;)

---

##### Log Levels

If you look into real kernel code you will always see something like:

```
printk(KERN_ERR "something went wrong, return code: %d\n",ret);
```

where `KERN_ERR` is one of the eight different log levels defined in [include/linux/kern_levels.h](http://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/include/linux/kern_levels.h?id=HEAD) and specifies the severity of the error message.

Note that there is **NO** comma between the `KERN_ERR` and the format string (as the preprocessor concatenates both strings)

The log levels are:

| Name | String | Meaning | alias function |
| --- | --- | --- | --- |
| `KERN_EMERG` | `"0"` | Emergency messages, system is about to crash or is unstable | `pr_emerg` |
| `KERN_ALERT` | `"1"` | Something bad happened and action must be taken immediately | `pr_alert` |
| `KERN_CRIT` | `"2"` | A critical condition occurred like a serious hardware/software failure | `pr_crit` |
| `KERN_ERR` | `"3"` | An error condition, often used by drivers to indicate difficulties with the hardware | `pr_err` |
| `KERN_WARNING` | `"4"` | A warning, meaning nothing serious by itself but might indicate problems | `pr_warning` |
| `KERN_NOTICE` | `"5"` | Nothing serious, but notably nevertheless. Often used to report security events. | `pr_notice` |
| `KERN_INFO` | `"6"` | Informational message e.g. startup information at driver initialization | `pr_info` |
| `KERN_DEBUG` | `"7"` | Debug messages | `pr_debug`, `pr_devel` if `DEBUG` is defined |
| `KERN_DEFAULT` | `"d"` | The default kernel loglevel |  |
| `KERN_CONT` | `""` | "continued" line of log printout (only done after a line that had no enclosing `\n`) [[1]](http://lwn.net/Articles/252651/) | `pr_cont` |

Note that the actual values of the log levels are prepended by the `KERN_SOH` character whose ASCII value is `'\001'`. Read the source for more details.

The `pr_*` macros (with exception of `pr_debug`) are simple shorthand definitions in `include/linux/printk.h` for their respective `printk` call and should probably be used in newer drivers.

`pr_devel` and `pr_debug` are replaced with `printk(KERN_DEBUG ...` if the kernel was compiled with `DEBUG`, otherwise replaced with an empty statement.

For drivers the `pr_debug` should not be used anymore (use `dev_dbg` instead).

If you don't specify a log level in your message it defaults to `DEFAULT_MESSAGE_LOGLEVEL` (usually `"4"`=`KERN_WARNING`) which can be set via the `CONFIG_DEFAULT_MESSAGE_LOGLEVEL` kernel config option (`make menuconfig-> Kernel Hacking -> Default message log level`)

The log level is used by the kernel to determine the importance of a message and to decide whether it should be presented to the user immediately, by printing it to the current console (where console could also be a serial line or even a printer, not an xterm).

For this the kernel compares the log level of the message to the `console_loglevel` (a kernel variable) and if the priority is higher (i.e. a lower value) than the `console_loglevel` the message will be printed to the current console.

To determine your current `console_loglevel` you simply enter:

```
$ cat /proc/sys/kernel/printk
    7       4       1       7
    current default minimum boot-time-default
```

The first integer shows you your current `console_loglevel`; the second the default log level that you have seen above.

To change your current `console_loglevel` simply write to this file, so in order to get all messages printed to the console do a simple

```
# echo 8 > /proc/sys/kernel/printk
```

and every kernel message will appear on your console.

Another way to change the console log level is to use `dmesg` with the `-n` parameter

```
# #set console_loglevel to print KERN_WARNING (4) or more severe messages
# dmesg -n 5
```

Only messages with a value lower (**not** lower equal) than the `console_loglevel` will be printed.

You can also specify the `console_loglevel` at boot time using the `loglevel` boot parameter. (see [Documentation/kernel-parameters.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=Documentation/kernel-parameters.txt;hb=HEAD#l1334) for more details)

---

**Author's practical advice:** Of course you should always specify an appropriate log level for your messages, but for **debugging**, I guess most developers leave the `console_loglevel` unchanged and simply use `KERN_ERR` or `KERN_CRIT` to ensure the message reaches the console.

```
pr_err("REMOVE ME: my debug statement that I swear to remove when I'm done\");
```

Please make sure to remove these 'inappropriately' tagged messages before shipping the module ;)

---

`KERN_CONT` and `pr_cont` are special cases since they do not specify an urgency but rather indicate a 'continued message' e.g.:



```c
printk(KERN_ERR "Doing something was ");
/* <100 lines of whatever>*/
if (success)
   printk(KERN_CONT "successful\n");
else
   printk(KERN_CONT "NOT successful\n");

-> "Doing something was successful"
```

**Important Note:** `KERN_CONT` and `pr_cont` should only be used by core/arch code during early bootup (a continued line is not SMP-safe otherwise). [[2]](http://lwn.net/Articles/252651/)

## Rate Limiting and One-Time Messages

Occasionally you have to insert a message in a section which gets called quite often. This not only might have a severe performance impact, it could also overwrite and spam your kernel buffer, so it should be avoided.

As always, the kernel already provides you with nice functions that solve your problems:

```c
printk_ratelimited(...)
```

and

```c
printk_once(...)
```

`printk_once` is fairly trivial—no matter how often you call it, it prints once and never again.

`printk_ratelimited` is a little bit more complicated—it prints by default not more than 10 times in every 5 seconds (for each function it is called in).

If you need other values for the maximum burst count and the timeout, you can always set up your own ratelimit using the `DEFINE_RATELIMIT_STATE` macro and the `__ratelimit` function—see the implementation of `printk_ratelimited` for an example.

Be sure to `#include *` in order to use `printk_ratelimited()`.

Both functions also have their `pr_*` equivalents, like `pr_info_ratelimited` for `printk_ratelimited(KERN_INFO...` and `pr_crit_once` for `printk_once(KERN_CRIT...`.

**Note:** Both did not work as expected in my tests here; will probably investigate further.

## Printk from Userspace

Sometimes, especially when doing automated testing, it is quite useful to insert some messages in the kernel log buffer in order to annotate what's going on.

It is as simple as:

```bash
# echo "Hello Kernel-World" > /dev/kmsg
```

Of course, this message gets the default log level assigned. If you want, for example, to issue a `KERN_CRIT` message, you have to use the string representation of the log level—in this case, `"2"`:

```bash
# echo "2Writing critical printk messages from userspace" >/dev/kmsg
```

The message will appear like any other **kernel** message—there is **no way** to distinguish them!

**Note:** Don't confuse this with `printf`—we are printing a kernel message from userspace here.

If `/dev/kmsg` does not exist, it can be created with:

```bash
mknod -m 600 /dev/kmsg c 1 11
```

## Internals and Changing the Size of the `printk` Buffer

`printk` is implemented by using a ring buffer in the kernel with a size of `__LOG_BUF_LEN` bytes, where `__LOG_BUF_LEN` equals `(1 << CONFIG_LOG_BUF_SHIFT)` (see [`kernel/printk.c`](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=kernel/printk.c;hb=HEAD) for details).

You can specify the size of the buffer in your kernel config by setting `CONFIG_LOG_BUF_SHIFT` to an appropriate value (for example, 17 for 128 KB):

`make menuconfig -> General Setup -> Kernel log buffer size`

Using a ring buffer implies that older messages get overwritten once the buffer fills up, but this is only a minor drawback compared to the robustness of this solution (that is, minimum memory footprint, callable from every context, not many resources wasted if nobody reads the buffer, no filling up of disk space/RAM when some kernel process goes wild and spams the buffer, and so on). Using a reasonably large buffer size should give you enough time to read your important messages before they are overwritten.

**Note:** `dmesg` reads by default a buffer of a maximum of 16,392 bytes, so if you use a larger log buffer, you have to invoke `dmesg` with the `-s` parameter, for example:

```bash
### CONFIG_LOG_BUF_SHIFT 17 = 128k
$ dmesg -s 128000
```

The kernel log buffer is accessible for reading from userspace through `/proc/kmsg`. `/proc/kmsg` behaves more or less like a FIFO and blocks until new messages appear.

**Please note:** Reading from `/proc/kmsg` consumes the messages in the ring buffer, so they may not be available for other programs. It is usually a good idea to let `klogd` or `syslog` do this job and read the content of the buffer via `dmesg`.

## Pros and Cons

The main advantage of `printk` over other debugging solutions is that it requires no sophisticated setup and can be called anywhere at any time. `printk` can be called while holding a lock, from interrupt and process context, is SMP-safe, and does not need any special preparation. It is just there and just works. The only precondition is that you have some kind of working console to display the messages.

For the early stages in the boot process, where no console is available yet, there is a special function named `early_printk`. This function writes directly to the VGA buffer or a serial line but otherwise works just like `printk`. You have to enable this function by setting `CONFIG_EARLY_PRINTK` in your kernel config:

`make menuconfig -> Kernel Hacking -> Early printk`

The major drawback is that `printk` is quite static, so you have to figure out what you want to trace beforehand. If you want to trace something different, you have to recompile your code, which can become quite cumbersome. (And of course, `printk` is not interactive at all, so you can't modify any variables or the like.)

The other drawback is that printing usually consumes quite some processing power and I/O time, so if you're trying to debug a timing-critical section or a timing bug, you're probably out of luck.

## Debugging Early Boot Problems

### Accessing the `printk` Buffer after a Silent Hang on Boot

Sometimes, if the kernel hangs early in the boot process, you get no messages on the console before the hang. However, there may still be messages in the `printk` buffer, which can give you an idea of where the problem is.

The kernel starts putting messages into the `printk` buffer as soon as it starts. They stay buffered there until the console code has a chance to initialize the console device, often the serial port for embedded devices. Even though these messages are not printed before the hang, it is still possible in some circumstances to dump the `printk` buffer and see the messages.

The tricky parts of doing this are:

1. Using a warm reset, if possible, so the memory contents are not lost when transitioning from the stuck kernel to the bootloader. You can do a cold boot, but if the memory is left unpowered for very long, you will start to see memory corruption.
2. Figuring out the address to use in the bootloader, based on the address of `__log_buf` in `System.map`. You will probably need to subtract the value of `CONFIG_PAGE_OFFSET` from the `__log_buf` address. However, there may be other offsets present as well, such as `TEXT_OFFSET`. Sometimes you can find the buffer by dumping the memory in a suspected area and locating the kernel messages visually in the dump. Note that the mapping offset between the kernel map of memory and the bootloader map of memory should not change. So once you figure it out, you are set.

Quinn Jensen writes:

Something I've found handy when the console is silent is to dump the `printk` buffer from the boot loader. To do it, you have to know how your boot loader maps memory compared to the kernel.

#### Redboot Example on a Freescale ADS Board

Quinn says: Here's what I do with Redboot on i.MX31:

```bash
fgrep printk_buf System.map
```

This shows the linked address of the `printk_buf`, for example:

```text
c02338f0 b printk_buf.16194
```

The address `"c02338f0"` is in kernel virtual memory, which, in the case of i.MX31 ADS, Redboot will have mapped to `0x802338f0`. So, after resetting the target board, but without letting it try to boot again, at the Redboot prompt:

```bash
dump -b 0x802338f0 -l 10000
```

And you see the `printk` buffer that never got flushed to the UART. Knowing what's there can be **very** useful in debugging your console.

#### U-Boot Example on an OMAP OSK Board

Tim Bird tried these steps and they worked:

```bash
grep __log_buf System.map
```

or:

```bash
grep __log_buf /proc/kallsyms
```



These show:

```
c0352d88 B __log_buf
```

In the case of the OSK, this address maps to `0x10352d88`. So I reset the target board and use the following:

```
OMAP5912 OSK # md 10352d88
10352d88: 4c3e353c 78756e69 72657620 6e6f6973    <5>Linux version
10352d98: 362e3220 2e32322e 612d3631 6e5f706c     2.6.22.16-alp_n
10352da8: 7428206c 64726962 6d697440 6b736564    l (tbird@timdesk
10352db8: 2e6d612e 796e6f73 6d6f632e 67282029    .am.sony.com) (g
10352dc8: 76206363 69737265 33206e6f 342e342e    cc version 3.4.4
10352dd8: 34232029 45525020 54504d45 65755420    ) #4 PREEMPT Tue
...
```

#### Grub

Grub also supports a dump command, which you can invoke from the grub prompt.

```
dump  [ -s offset ] [-n length] { FILE | (mem) }
```

### Using `CONFIG_DEBUG_LL` and `printascii()` (ARM only)

If the kernel fails before the serial console is enabled, you can use `CONFIG_DEBUG_LL` to add extra debug output routines to the kernel. These are `printascii`, `printch`, and `printhex`. These routines print directly to the serial port, bypassing the console code, and are available earlier in machine initialization.

To see `printk`s earlier in the boot sequence, before the console is initialized, set `CONFIG_DEBUG_LL=y` and `CONFIG_EARLY_PRINTK=y`.

Alternatively, add your own calls to `printascii`, `printch`, and `printhex` where you believe the problems are located.

Here is an e-mail exchange seen on the linux-embedded mailing list, with answer by George Davis: [[3]](http://www.mail-archive.com/linux-embedded@vger.kernel.org/msg00223.html)

```
> When we try to boot a 2.6.21 kernel after uncompressing the kernel the boot process dies somehow.
> We've figured out so far that the kernel dies somewhere between the gunzip and start_kernel.

Try enabling DEBUG_LL to see if it's an machine ID error.  If you see:

Error: unrecognized/unsupported processor variant.

or:

Error: unrecognized/unsupported machine ID...

Then you either don't have proper processor support enabled for your target or your bootloader is passing in the wrong machine number.

If you still don't see anything, try hacking printk.c to call printascii() (enabled for the DEBUG_LL case) to print directly to the serial port w/o a driver, etc.,.  You can find more details on these low-level debugging hacks via a little googling...
```

## NetConsole

Sometimes you are in the unlucky situation that the machine crashes or hangs and you have no way to access the console afterwards, e.g. the graphic driver hangs and the kernel dies soon after. In this case you could either hook up a serial line to your crashing target machine, if a serial port is available, or use the kernel's netconsole feature to enable `printk` logging via UDP.

In order to use it, you have to enable the `CONFIG_NETCONSOLE` kernel config option (`make menuconfig -> Device Drivers -> Network device support -> Network core driver support -> Network console logging support`) and configure it appropriately by using the `netconsole` configuration parameter:

```
netconsole=[src-port]@[src-ip]/[<dev>],[tgt-port]@<tgt-ip>/[tgt-macaddr]
    where
        src-port      source for UDP packets (defaults to 6665)
        src-ip        source IP to use (interface address)
        dev           network interface (eth0)
        tgt-port      port for logging agent (6666)
        tgt-ip        IP address for logging agent
        tgt-macaddr   ethernet MAC address for logging agent (broadcast)
```

For example, specify the following at the kernel command line in your bootloader:

```
linux netconsole=4444@10.0.0.1/eth1,9353@10.0.0.2/12:34:56:78:9a:bc
```

This sends messages from `10.0.0.1` port `4444` via `eth1` to `10.0.0.2` port `9353` with the MAC `12:34:56:78:9a:bc`.

Alternatively, load the module:

```
# insmod netconsole netconsole=@/,@10.0.0.2/
```

This sends messages via broadcast to `10.0.0.2` port `6666`.

On the other machine, you can now simply fire up:

```
# netcat -u -l -p <port>
```

For example:

```
$ netcat -u -l -p 6666
```

You can then see the `printk` messages from your target dribbling in.

If you don't see any messages, you might have to set the `console_loglevel` to a higher value (see above) or test the connection via telnet. For example, from the target, type:

```
$ telnet 10.0.0.2 6666
```

### Netconsole resources

See [Documentation/networking/netconsole.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/networking/netconsole.txt;hb=HEAD) for more details.

See [Sarah Sharp's blog entry about using netconsole](http://sarah.thesharps.us/2009-02-22-09-00).

## Misc

### Dmesg / Clearing the buffer

```
dmesg -c
```

This clears the `dmesg` buffer. Sometimes it is nice to start with a blank buffer, so you will only see new messages when you invoke `dmesg`.

### Printk Timestamps

```
CONFIG_PRINTK_TIME
```

Setting this kernel config option prepends every `printk` statement with a timestamp representing the time since boot. This is particularly useful to get a general idea about the timings of your code.

You can also specify an argument on the kernel command line to enable this, or you can enable it at any time during runtime by doing the following:

```
$echo 1 >/sys/module/printk/parameters/time
```

There are also tools available to use the information to show relative times between `printk`s (`scripts/show_delta`) and create graphs of durations in the kernel (`scripts/bootgraph.pl`).

See Printk Times for more details.

### Printing buffers as hex

If you want to print a buffer as hex within the kernel, don't reinvent the wheel; use `printk_hex_dump_bytes()` instead.

```
print_hex_dump_bytes(const char *prefix_str, int prefix_type, const void *buf, size_t len)
```

This function prints a buffer as hex values to the kernel log buffer, with level `KERN_DEBUG`.

Example:

```
Kernel Code:
char mybuf[] = "abcdef";
print_hex_dump_bytes("", DUMP_PREFIX_NONE, mybuf, ARRAY_SIZE(mybuf));

dmesg output:
61 62 63 64 65 66 00                             abcdef.
```

If you need something more sophisticated and flexible, have a look at `print_hex_dump()` and `hex_dump_to_buffer()`.

### Dynamic Debugging

It is also possible to enable or disable debug information at runtime using the dynamic debug functionality of the kernel. For this, the `CONFIG_DYNAMIC_DEBUG` kernel config option must be set. See [Documentation/dynamic-debug-howto.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/dynamic-debug-howto.txt;hb=HEAD) for more information.

## Disabling `printk` Messages at Compile Time

There is a configuration option that allows you to turn off all the `printk` messages in the whole kernel (`CONFIG_PRINTK`). This reduces the size of the kernel, usually by at least 100k, since all message strings are not compiled into the kernel binary image.

However, it also means you get absolutely no output from the kernel while it is running. Disabling kernel `printk` messages is usually the last thing you do when you are tuning your kernel for size.

## References and External Links

- [Linux Kernel Development](http://eLinux.org/Linux_Kernel_Development_-_by_Robert_Love "Linux Kernel Development - by Robert Love"), Robert Love, 3rd Edition, Chapter 18 Debugging
- [Linux Device Drivers](http://eLinux.org/Linux_Device_Drivers "Linux Device Drivers"), Corbet, Rubini and Kroah-Hartmann, 3rd Edition, Chapter 4 Section 2
- [Essential Linux Device Drivers](http://eLinux.org/Essential_Linux_Device_Drivers)
- [Documentation/printk-formats.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/printk-formats.txt;hb=HEAD)
- [Documentation/dynamic-debug-howto.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/dynamic-debug-howto.txt;hb=HEAD)
- [Documentation/networking/netconsole.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/networking/netconsole.txt;hb=HEAD)



## 相关资源

- [kernel/printk.c](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=kernel/printk.c;hb=HEAD)：`printk` 及其他函数的实现
- [include/linux/printk.h](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=include/linux/printk.h;hb=HEAD)：`printk` 头文件
- [include/linux/kern_levels.h](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=include/linux/kern_levels.h;hb=HEAD)：日志级别头文件
- [关于不同 `%p` 格式说明符的博客文章](http://www.embedded-bits.co.uk/2010/printk-format-specifiers/)
- [LWN.net: The perils of pr_info()](http://lwn.net/Articles/487437/)
- [内核日志记录：API 与实现，作者 Tim Jones（IBM）](http://www.ibm.com/developerworks/linux/library/l-kernel-logging-apis/index.html)（不错的文章）

与 `printk` 相关的其他页面：

- [Printk Times](http://eLinux.org/Printk_Times "Printk Times") - 包含如何为每条 `printk` 消息启用时间戳的信息
  - `printk` 时间戳示例
- [printk 大小信息](http://eLinux.org/Printk_Size_Info "Printk Size Info")
- [Do Printk](http://eLinux.org/Do_Printk "Do Printk") - 包含如何在模块级别禁用 `printk` 消息的方法

[分类](http://eLinux.org/Special:Categories "Special:Categories")：

- [开发工具](http://eLinux.org/Category:Development_Tools "Category:Development_Tools")
- [技巧与诀窍](http://eLinux.org/Category:Tips_and_Tricks "Category:Tips and Tricks")
- [Printk](http://eLinux.org/Category:Printk "Category:Printk")

# 内核调试技巧

> 来源：[eLinux.org](http://eLinux.org/Kernel_Debugging_Tips "http://eLinux.org/Kernel_Debugging_Tips")

# 内核调试技巧

以下是一些调试内核的杂项技巧：

## 目录

- 1 使用 `printk`
  - 1.1 日志级别
  - 1.2 添加时间信息
  - 1.3 查看日志消息
  - 1.4 控制控制台输出
  - 1.5 更改 `printk` 缓冲区大小
- 2 使用内核符号
- 3 使用内核调试器
- 4 调试早期启动问题
- 5 触发内核事件
  - 5.1 重载 `sync` 系统调用
- 6 解读 Oops 消息
- 7 内核编译技巧
  - 7.1 编译单个文件
  - 7.2 为单个源文件生成预处理文件
  - 7.3 为单个源文件生成汇编文件
  - 7.4 修改编译标志

## 使用 `printk`

要在内核中添加自己的调试消息，可以在内核代码中放置一个 `printk()`。

更多细节请参阅 [通过打印调试 -> 用法](http://eLinux.org/Debugging_by_printing#Usage "Debugging by printing")。

### 日志级别

每条内核消息都可以附加一个标签，用于指示消息的重要性。

更多细节请参阅 [通过打印调试 -> 日志级别](http://eLinux.org/Debugging_by_printing#Log_Levels "Debugging by printing")。

### 添加时间信息

有时，向 `printk` 值添加时间信息会很有用，这样你可以看到特定事件发生的时间。内核包含一个名为 `printk` times 的功能来实现这一点。

有关此功能的更多信息，请参阅文件 `lib/Kconfig.debug` 中 `CONFIG_PRINTK_TIMES` 的帮助。配置内核时，此选项位于“内核黑客”菜单中。

插入到 `printk` 输出中的时间戳由秒和微秒组成，是相对于机器开始运行（或内核开始计时）的绝对值。

内核源码中还有一个工具，可以将时间戳值转换为相对值（这样你可以看到事件之间的间隔）。该工具名为 `show_delta`，位于内核的 `scripts` 目录中。

更多信息请参阅 Printk Times。

### 查看日志消息

`klogd` 程序会从内核日志缓冲区中提取消息，并将其发送到系统日志（在大多数系统上最终位于 `/var/log/messages`）。该命令在大多数桌面或服务器系统上后台运行，并持续将消息从内核日志缓冲区传输到系统日志。

你可以使用 `dmesg` 命令直接查看日志缓冲区的内容。请注意，默认情况下 `dmesg` 会显示缓冲区中的消息，但不会将其移除。因此，可以多次运行此命令来查看内核 `printk` 消息。有关此工具的更多用法，请参阅 `dmesg` 手册页。

### 控制控制台输出

为了减少内核启动时的“噪音”，或为了加快启动速度，有时控制启动期间显示到控制台的消息数量会很有用。你可以通过内核命令行选项在启动时设置内核日志级别。请参阅 [`Documentation/kernel-parameters.txt`](https://www.kernel.org/doc/Documentation/kernel-parameters.txt) 中的 `loglevel=` 参数。

你可以使用内核命令行选项 `quiet` 关闭所有消息。有关这能在启动时节省多少时间的信息，请参阅 Disable Console。

请注意，即使更改了日志级别或使用了 `quiet`，虽然 `printk` 消息不会打印到控制台，但它们仍会进入日志缓冲区，之后仍可使用 `dmesg` 命令提取并显示。

### 更改 `printk` 缓冲区大小

请参阅 [通过打印调试 -> 内部机制 / 更改 `printk` 缓冲区大小](http://eLinux.org/Debugging_by_printing#Internals_.2F_Changing_the_size_of_the_printk_buffer "Debugging by printing")

## 使用内核符号

你可以使用工具链的 `addr2line` 程序查找函数地址对应的源代码。请参阅 [查找内核函数行](http://eLinux.org/Find_a_kernel_function_line "Find a kernel function line") 或 [用于内核调试的 Addr2line](http://eLinux.org/Addr2line_for_kernel_debugging "Addr2line for kernel debugging")。

## 使用内核调试器

你可以使用内核内置调试器：KDB

你可以使用内核远程调试器：Kgdb

此外，你还可以使用 QEMU 和 gdb（以及像 Eclipse 这样的高级 IDE）。

请参阅 [使用 Eclipse/CDT 和 Qemu 调试 Linux 内核](http://issaris.blogspot.com/2007/12/download-linux-kernel-sourcecode-from.html)，这是一篇关于使用 Eclipse（带 CDT 插件）调试 Linux 内核的优秀文章。

## 调试早期启动问题

请参阅 [通过打印调试 -> 调试早期启动问题](http://eLinux.org/Debugging_by_printing#Debugging_early_boot_problems "Debugging by printing")

## 触发内核事件

### 重载 `sync` 系统调用

有时，从用户空间触发内核中的事件会很方便。与其创建处理 `/proc` 事件的基础设施、`ioctl()` 或新的系统调用，不如直接重载一个现有函数来得快速简便。一个不常用的函数是 `sync`。（我发现 `sync` 系统调用通常不会被用户空间程序调用，也不会在标准 Linux 启动过程中被调用。）

在 `sys_sync()` 例程（位于 `fs/sync.c`）中放置一个钩子来调用你自己的内核程序，然后从 shell 命令行执行 `sync` 来触发它，这是非常容易的。这可以作为临时机制来测试你放入内核的内容。

## 解读 Oops 消息

当内核遇到内部错误时，它会打印一条 Oops 消息。以下是一些使用 Oops 消息查找问题来源的技巧。

- 请参阅 [Documentation/oops-tracing.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob_plain;f=Documentation/oops-tracing.txt;hb=HEAD)
- 请参阅 [HOWTO find oops location](http://vmlinux.org/jocke/linux/howto-find-oops-location.shtml)，作者 Denis Vlasenko

## 内核编译技巧

有时，你可能希望修改编译器编译单个内核文件的方式。以下是一些与此相关的技巧。

### 编译单个文件

你可以使用以下命令编译单个输出目标文件：



```bash
make fs/buffer.o
```

This will build JUST `fs/buffer.o` (if it needs rebuilding) and not the entire kernel. To force it to need re-building, use `touch` on the associated source file:

```bash
touch fs/buffer.c
```

### Create the preprocessed file for an individual source file

Using the same technique, you can create the preprocessed file for a C source file. This is useful if you're having trouble tracking down macro expansion or where defines/prototypes are coming from exactly.

```bash
make fs/buffer.i
```

### Create the assembly file for an individual source file

Using the same technique, you can create the assembly file for a C source file. This is useful to get an idea what actual machine instructions are generated from the C source code.

```bash
make fs/buffer.s
```

Another way to get the raw assembly is to dump the object file using `objdump`:

```bash
objdump -d fs/buffer.o > fs/buffer.disassem
```

This will produce a disassembly of the object file, which should show how the assembly was translated into machine instructions.

If the object has been compiled with debug symbols (using `-g`), then you might get more information using the `-S` option with `objdump`:

```bash
objdump -S -d fs/buffer.o >fs/buffer.disassem
```

You can also request that the toolchain show mixed source and assembly by passing extra flags:

```bash
make EXTRA_CFLAGS="-g -Wa,-a,-ad -fverbose-asm" fs/buffer.o >fs/buffer.mixed
```

### Alter the flags for a compilation

Sometimes, you need to alter the compilation flags for an individual file. There are two ways to do this. One is to add the extra flags on the `make` command line:

```bash
make EXTRA_CFLAGS="-g -finstrument-functions" fs/buffer.o
```

This will work if the flags can be appended to the regular set of C flags used for compiling the object.

However, if you need to do something more complicated, like removing or modifying flags, then you can build your own command line by hand. To do this, it is easiest to have `make` produce the default compilation command (which will be several lines long), then copy, paste and edit it, to run on the command line directly. To see the exact compile commands used to compile a particular object, use the `V=1` option with the kernel build system:

```bash
make V=1 fs/buffer.o
```

For me, this produced something like this:

```bash
mipsel-linux-gcc -Wp,-MD,fs/.buffer.o.d -nostdinc -isystem /home/usr/local/mipsel-linux-glibc/bin/../lib/gcc/mipsisa32el-linux/3.4.3/include -D__KERNEL__ -Iinclude -Iinclude2 -I/home/tbird/work/linux/include -I/home/tbird/work/linux/fs -Ifs -Wall -Wstrict-prototypes -Wno-trigraphs -fno-strict-aliasing -fno-common -ffreestanding -O2 -fomit-frame-pointer -g -I/home/tbird/work/linux/ -I /home/tbird/work/linux/include/asm/gcc -G 0 -mno-abicalls -fno-pic -pipe -finline-limit=100000 -mabi=32 -march=mips32r2 -Wa,-32 -Wa,-march=mips32r2 -Wa,-mips32r2 -Wa,--trap -I/home/tbird/work/linux/include/asm-mips/ati -Iinclude/asm-mips/ati -I/home/tbird/work/linux/include/asm-mips/mach-generic -Iinclude/asm-mips/mach-generic -Wdeclaration-after-statement -DKBUILD_BASENAME=buffer -DKBUILD_MODNAME=buffer -c -o fs/buffer.o /home/tbird/work/linux/fs/buffer.c
```

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Development Tools](http://eLinux.org/Category:Development_Tools "Category:Development Tools")

# Kgdb

> From: [eLinux.org](http://eLinux.org/Kgdb "http://eLinux.org/Kgdb")

It is fascinating to think that you have control over running Linux Kernel. You can stop, can single-step, can resume and even can put break-points on running Kernel. In fact, you can debug the kernel as easily as you debug any application.

## Contents

1. How to setup kgdb
2. Hardware Requirements
3. Preparing Kernel to be Debugged
4. There are several possible problems that you may face
5. Using an IDE

## How to setup kgdb

The steps mentioned here are with reference to 2.6.26 Kernel. The main reason is KGDB code is merged into Linux tree from 2.6.26-RC5 kernel. As a side note, for kernel < 2.6.26-RC5, you have to get kgdb patch from [`kgdb.linsyssoft.com/kernel.htm`](http://kgdb.linsyssoft.com/kernel.htm) and apply them to kernel.

## Hardware Requirements

Two x86 machines are required for using KGDB. One of the machines runs a kernel to be debugged called "TEST MACHINE". The other machine runs `gdb`, "DEVELOPMENT MACHINE". A serial line is required between the development and the test machine. And so obviously, machines need one serial port each. Basically, you will be sending "Debugging Commands" from "DEVELOPMENT MACHINE" to "TEST MACHINE".

## Preparing Kernel to be Debugged

1. Download the source of kernel (for e.g., 2.6.26.2) from kernel.org.
2. Recompile the Kernel on "DEVELOPMENT MACHINE". Go to Kernel Hacking and Enable the following options:

   ```text
   -*- Magic SysRq key
   [*] Compile the kernel with debug info
   [*] KGDB: kernel debugging with remote gdb --->
   ```

   And in KGDB:

   ```text
   --- KGDB: kernel debugging with remote gdb
   <*>   KGDB: use kgdb over the serial console
   [ ]   KGDB: internal test suite
   ```

3. Build kernel and modules:

   ```bash
   make -j 12 && make modules && make modules_install
   ```

4. Transfer the `vmlinux`, `system.map` and `initrd.img` files on "TEST MACHINE".
5. Now, edit the GRUB entry for that kernel on "TEST MACHINE". Add kernel options/kernel parameters like `kgdbwait` and `kgdboc=ttyS0,115200`:

   ```text
   For e.g., kernel /vmlinux ro root=LABEL=/ rhgb quiet crashkernel=128M@16M kgdbwait kgdboc=ttyS0,115200
   ```

   `kgdbwait` -- > This will make Kernel to wait on boot time and will expect someone to connect to it and give further commands. `kgdboc` --> This is a KGDB I/O driver and we are supplying two arguments. `ttyS0` will tell that communication will happen on Serial Port 0 and `115200` is the baudrate.

6. Now boot the Kernel with those kernel parameters.
7. On dev machine, start GDB session:

   ```bash
   [dev@einfochips]gdb vmlinux
   ```

   The argument `vmlinux` file is the file that is created with Debug symbols. It will be of much larger size and more than likely to be in the directory where you gave `make` command.

8. Assuming that on "DEVELOPMENT MACHINE" you have set serial interface baudrate as `115200`. Connect to the "TEST MACHINE" with `target` command:

   ```text
   (gdb)target remote /dev/ttyS0
   ```

9. This will stop your Kernel booting on "TEST MACHINE" and will give control to your "DEVELOPMENT MACHINE". Now, you can do Single-stepping or put breakpoints and etc.
10. Once your Kernel is running on "TEST MACHINE" and you want control over your running kernel from "DEVELOPMENT MACHINE", You have to send MANUALLY on TEST machine SysRq command. So, on "TEST MACHINE" press SysRq + `g`.

    (i.e., press "ALT" key then Press "PrintScreen" Key and then Press "g" key)

## There are several possible problems that you may face

1. Your Kernel is booted and SysRq+g is not working.

   ```bash
   [r00t@einfochips] echo 1 > /proc/sys/kernel/sysrq
   ```

   This will enable sending SysRq commands.

2. You may find some time that while stopping execution through SysRq key on "TEST MACHINE", it stops but then it is not able to communicate over serial cable with "DEVELOPMENT MACHINE". The reason can be, your KGDB I/O driver is not passed arguments properly and you may need to reconfigure the driver by following way:

   ```bash
   [root@einfochips]echo "ttyS0,115200" > /sys/modules/<module name>/parameters
   ```

3. The target board has a single serial port that needs to be shared between the console and kgdb.



The kgdb Docbook refers to using a proxy to split the serial port data stream between `gdb` and the console terminal emulator. Proxy programs include:

```text
kgdb demux (kdmx) Media:Kdmx_v140904a.tar.gz
                   (moved to agent-proxy git)

kgdb demux (kdmx)
                   kdmx at elinux.org
                   https://git.kernel.org/cgit/utils/kernel/kgdb/agent-proxy.git/
                   git clone git://git.kernel.org/pub/scm/utils/kernel/kgdb/agent-proxy.git/

agent-proxy
                   https://git.kernel.org/cgit/utils/kernel/kgdb/agent-proxy.git/
                   git clone git://git.kernel.org/pub/scm/utils/kernel/kgdb/agent-proxy.git/
```

(frowand: I have been using `kdmx` successfully. I have not tried using `agent-proxy`.)

## Using an IDE

You can debug the Linux Kernel over KGDB with Visual Studio using the VisualKernel plugin. [This tutorial](http://visualkernel.com/tutorials/kgdb) shows how to use it with KGDB.

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Development Tools](http://eLinux.org/Category:Development_Tools "Category:Development Tools")

# KDB

> From: [eLinux.org](http://eLinux.org/KDB "http://eLinux.org/KDB")

## Contents

1. Introduction and basic resources
   1. Older Information
2. General Information
   1. Kernel Versions supported
3. Kernel configuration
   1. Config variables
   2. Steps
4. Enabling kdb
   1. At runtime
   2. At boot time (via kernel command line)
5. Invoking kdb
   1. Invoking with Magic SysRq `g`
   2. Invocation by panic
   3. Invocation by breakpoint
6. Using `gdb` to see the kernel source listing
7. KDB environment variables
8. Hints and tips
   1. Command line completion
   2. Defining a set of commands
   3. Executing commands on kdb initialization
   4. Piping command results through `grep`
   5. Command history
9. Feature extension notes (by Tim)
   1. internals

## Introduction and basic resources

Here is some information about KDB—the in-kernel debugger for the Linux kernel.

The KDB and KGDB official wiki: [`kgdb.wiki.kernel.org/`](https://kgdb.wiki.kernel.org/) (this only has 2 pages?)

Jason Wessel is the current KDB maintainer. Here is a presentation from him at LinuxCon 2010 (August 2010): [`kernel.org/pub/linux/kernel/people/jwessel/dbg_webinar/State_Of_kernel_debugging_LinuxCon2010.pdf`](http://kernel.org/pub/linux/kernel/people/jwessel/dbg_webinar/State_Of_kernel_debugging_LinuxCon2010.pdf)

Here are some videos showing use of KDB and KGDB:

- Video 1 of 6: [`www.youtube.com/watch?v=V6Qc8ppJ_jc`](http://www.youtube.com/watch?v=V6Qc8ppJ_jc)
  - Example of a call to `panic` from a test module (without a debugger)

- Video 2 of 6: [`www.youtube.com/watch?v=LqAhY8K3XzI`](http://www.youtube.com/watch?v=LqAhY8K3XzI)
  - Example of catching the panic with KDB, and looking up the source line with `gdb`

- Video 3 of 6: [`www.youtube.com/watch?v=bBEh_UduX04`](http://www.youtube.com/watch?v=bBEh_UduX04)
  - Example of a bad access request, and looking up the source line with `gdb`

- Video 4 of 6: [`www.youtube.com/watch?v=MfJU2E0aJwg`](http://www.youtube.com/watch?v=MfJU2E0aJwg)
  - Example of using a hardware breakpoint with `kdb`

- Video 5 of 6: [`www.youtube.com/watch?v=sWiHV5mt8_k`](http://www.youtube.com/watch?v=sWiHV5mt8_k)
  - Use an address watch (hardware watchpoint) using `kgdb` (data access hardware breakpoint on `tp_address_ref`)

- Video 6 of 6: [`www.youtube.com/watch?v=nnopzcwvLTs`](http://www.youtube.com/watch?v=nnopzcwvLTs)
  - Use of `kgdb` over serial—start up the `agent-proxy`, connect, and hit a breakpoint at `sys_sync`

Documentation, up-to-date as of 2010, for KDB and KGDB is at: [`kernel.org/pub/linux/kernel/people/jwessel/kdb/`](http://kernel.org/pub/linux/kernel/people/jwessel/kdb/)

### Older Information

See [`www.ibm.com/developerworks/linux/library/l-kdbug/`](http://www.ibm.com/developerworks/linux/library/l-kdbug/) for a tutorial for the 2.4.20 kernel (from June 2003).

Here's an article from 2002 on KDB vs. KGDB: [`kerneltrap.org/node/112`](http://kerneltrap.org/node/112). It has a good discussion excerpt between Andrew Morton and Keith Owens about the relative merits of KDB versus KGDB.

## General Information

### Kernel Versions supported

`kgdb` was added to the mainline Linux kernel in version 2.6.26.

`kdb` support was added to the mainline Linux kernel in version 2.6.35.

Before those versions, `kgdb` and `kdb` were available as patches which could be applied to the Linux kernel source.

## Kernel configuration

The following descriptions are for a 2.6.35 kernel, using KDB over a serial line between host and target.

All these options are on the "Kernel Hacking" menu.

In order to support KDB, "KGDB" support must be turned on first, even if you aren't using `kgdb`/`gdb`.

### Config variables

- `CONFIG_DEBUG_KERNEL=Y` - includes debug information in the kernel compilation - required for basic kernel debugging support
- `CONFIG_KGDB=Y` - turns on basic kernel debug agent support
- `CONFIG_KGDB_SERIAL_CONSOLE=Y` - shares a serial console with `kgdb`
  - `Sysrq-g` must be used to break in initially.
  - Selecting this will automatically set:
    - `CONFIG_CONSOLE_POLL=Y`
    - `CONFIG_MAGIC_SYSRQ=Y` - turns on MAGIC-SYSRQ key support
- `CONFIG_KGDB_KDB=Y` - actually turns on the KDB debugger feature
- `CONFIG_DEBUG_RODATA=N` - you must disable this on x86 in order to set breakpoints on code or data

Optional other configuration settings:

- `CONFIG_FRAME_POINTER=Y` - this allows for better backtrace support in KDB
- `CONFIG_KALLSYMS=Y` - this adds symbolic information to the kernel, useful for seeing symbols instead of addresses
- `CONFIG_KDB_KEYBOARD` - uses KDB with an attached keyboard (not for use with serial console)
- `CONFIG_KGDB_TESTS` - used to turn on `kgdb` internal self-tests; see the config help for more information

### Steps

To turn on KDB over serial console, do the following:

- `make menuconfig`
  - Go to the "Kernel Hacking" sub-menu.
  - Turn on "KGDB: kernel debugger", and choose "<select>" to go to the sub-menu.
  - Verify that "KGDB: use kgdb over the serial console" is set.
  - Set "KGDB_KDB: include kdb frontend for kgdb".
- Save and exit.

Results:

```text
[]$ diffconfig
KGDB n -> y
+CONSOLE_POLL y
+KDB_KEYBOARD n
+KGDB_KDB y
+KGDB_SERIAL_CONSOLE y
+KGDB_TESTS n
```

## Enabling kdb

### At runtime

Once the kernel is compiled with `kdb` support and is running on your target board, you need to enable it. This can be done on a running system by binding the `kdb`/`kgdb` feature to a serial port and writing a value into the `sys` filesystem.

If your machine starts a serial console on `ttyS0`, you can bind `kdb`/`kgdb` to this serial console by writing the string `"ttyS0"` to `/sys/module/kgdboc/parameters/kgdboc`. The kernel will respond with a message indicating that the driver is registered.

```text
$ echo ttyS0 >/sys/module/kgdboc/parameters/kgdboc
kgdb: Registered I/O driver kgdboc.
```

### At boot time (via kernel command line)

You can enable `kdb` support in your kernel at boot time by using the `kgdboc` option on the kernel command line. Normally, you specify the tty device name, followed by the serial port speed.

```text
kgdboc=ttyS0,115200
```

## Invoking kdb

Once the kernel is running, and the `kgdb`/`kdb` is bound to the serial console, you can invoke the debugger in numerous ways.

First, you can enter the debugger using a [Magic SysRq](http://en.wikipedia.org/wiki/Magic_SysRq_key) command.

`kdb` will also be entered automatically if the kernel panics.



最后，您可以设置一个断点（硬件或软件），以便在满足断点条件时调用调试器。对于代码断点，这意味着在断点位置执行指令时；对于数据断点，则在断点地址发生特定访问时触发。

### 通过魔术 SysRq 'g' 调用

要使用魔术 SysRq 命令调用调试器，可以使用`'g'`命令，该命令可以通过魔术 SysRq 功能支持的任何方式发出。这可以通过以下方式完成：1）在连接的键盘上键入按键序列，2）向`/proc/sysrq-trigger`回显一个值，或3）通过串行控制台发送中断键序列。

示例：

*   从本地 shell 通过 procfs 触发 SysRq：`'echo g >/proc/sysrq-trigger'`
*   通过串行控制台中断序列触发 SysRq：
    *   在 minicom 中，键入`'ctrl-a f g'`（快速）
    *   在 telnet 中，通过支持发送中断的服务器：键入

### 通过 panic 调用

当发生内核 panic 时，说明出现了严重错误，内核会自动进入 kdb。从这里您可以查看内存、进行回溯、检查寄存器以及执行其他操作，以了解更多关于系统状态的信息并调试问题。

### 通过断点调用

要使用断点进入 kdb，首先使用魔术 SysRq 键调用 kdb（见上文），然后设置断点。接着键入`'go'`继续执行。当断点被命中时，调试器 shell 将出现。

在以下示例中，斜体项是用户键入的命令。以`'$'`开头的是在 shell 命令（正常 Linux 用户空间运行时）中键入的命令，以`'kgdb>'`开头的是在 kdb 交互式 shell 中键入的命令。

```
$ echo g >/proc/sysrq-trigger
SysRq : DEBUG

Entering kdb (current=0xdfdff040, pid 71) due to Keyboard Entry
kdb> bp sys_sync+4
Instruction(i) BP #0 at 0xc00c9f00 (sys_sync+0x4)
   is enabled  addr at 00000000c00c9f00, hardtype=0 installed=0

kdb> go
$ sync

Entering kdb (current=0xdfdaa360, pid 72) due to Breakpoint @ 0xc00c9f00
kdb> bt
Stack traceback for pid 72
0xdfdaa360       72       71  1    0   R  0xdfdaa560 *sync
[<c0028cb4>] (unwind_backtrace+0x0/0xe4) from [<c0026d50>] (show_stack+0x10/0x14)
[<c0026d50>] (show_stack+0x10/0x14) from [<c0079e78>] (kdb_show_stack+0x58/0x80)
[<c0079e78>] (kdb_show_stack+0x58/0x80) from [<c0079f1c>] (kdb_bt1.clone.0+0x7c/0xcc)
[<c0079f1c>] (kdb_bt1.clone.0+0x7c/0xcc) from [<c007a240>] (kdb_bt+0x2d4/0x338)
[<c007a240>] (kdb_bt+0x2d4/0x338) from [<c0078328>] (kdb_parse+0x4d4/0x5f8)
[<c0078328>] (kdb_parse+0x4d4/0x5f8) from [<c0078a8c>] (kdb_main_loop+0x448/0x6b0)
[<c0078a8c>] (kdb_main_loop+0x448/0x6b0) from [<c007acb4>] (kdb_stub+0x210/0x398)
[<c007acb4>] (kdb_stub+0x210/0x398) from [<c0073280>] (kgdb_handle_exception+0x384/0x574)
[<c0073280>] (kgdb_handle_exception+0x384/0x574) from [<c0028518>] (kgdb_brk_fn+0x18/0x20)
[<c0028518>] (kgdb_brk_fn+0x18/0x20) from [<c0022198>] (do_undefinstr+0x10c/0x1a8)
[<c0022198>] (do_undefinstr+0x10c/0x1a8) from [<c0022b84>] (__und_svc+0x44/0x60)
Exception stack(0xdfe09f58 to 0xdfe09fa0)
9f40:                                                       00000000 bec93e74
9f60: 000437ac 00034738 00000001 bec93e74 00000049 00000024 c00230e8 dfe08000
9f80: 00000000 bec93e54 00000000 dfe09fa0 c0022f40 c00c9f00 80000013 ffffffff
[<c0022b84>] (__und_svc+0x44/0x60) from [<c00c9f00>] (sys_sync+0x4/0x28)
[<c00c9f00>] (sys_sync+0x4/0x28) from [<c0022f40>] (ret_fast_syscall+0x0/0x30)
kdb> 
```

此示例展示了 kdb 的调用，接着设置断点，然后使用`'go'`恢复执行。然后，在 Linux 用户空间 shell 中运行`'sync'`命令以触发断点。当因断点进入 kdb 时，运行`'bt'`以从当前进程的堆栈获取回溯信息。

## 使用 gdb 查看内核源代码列表

您可以使用 kdb 中打印的地址，配合主机端的 gdb 会话，来查看特定地址周围的源代码或汇编指令。

目标地址可以来自回溯或寄存器转储（例如指令指针）。

要加载内核的源代码，请使用与目标上运行的映像匹配的 vmlinux 启动 gdb（或适当的架构特定的 gdb）。内核应使用调试符号（CONFIG_DEBUG_KERNEL=y）编译。gdb 将启动并加载内核的符号信息。

使用以下命令查看各种信息：

*   指令地址对应的源文件和行号
    *   `info line *0x<目标地址>`
*   指令地址周围的源代码行
    *   `list *0x<目标地址>`
*   地址处的汇编指令
    *   `disas 0x<目标地址>`，或
    *   `x/20i 0x<目标地址>`

## KDB 环境变量

以下是 kdb（在 2.6.35 中）支持的一些环境变量：

*   `LINES` - 设置 KDB 分页输出的行数（默认 24）
*   `BTAPROMPT` - 在 bta 命令中每个进程后提示（默认 0）
*   `LOGGING` - 如果为 1，将所有 KDB 输出回显到内核日志缓冲区（printk 日志）（默认 0）
*   `PROMPT` - 用于 kdb 交互式 shell 提示符的字符串（SMP 上默认`'[%d]kdb>'`，UP 上默认`'kdb>'`）
*   `MOREPROMPT` - 用于 kdb 分页输出提示符的字符串（SMP 上默认`'[%d]more>'`，UP 上默认`'more>'`）
*   `RADIX` - 用于打印输出的基数（默认 16）
*   `MDCOUNT` - md 命令未指定时显示的数据行数（默认 8）
*   `BYTESPERWORD` - md 命令的每字字节数（默认 4）
*   `DTABCOUNT` - 制表符补全时显示的符号数（默认 30）
*   `NOSECT` - 避免在 md 命令中显示章节信息（默认 1）
*   `PS` - 指定用于过滤`'ps'`命令的任务状态列表（每个状态一个字母）（默认`'DRSTCZEU'`）
    *   可以使用列表中的字母：DRSTCZEUIMA，每个字母对应一个任务状态（有关任务状态，请参阅 PS 手册页）
        *   D = 不可中断睡眠
        *   R = 运行中
        *   S = 可中断睡眠
        *   T = 已停止
        *   C = 被跟踪
        *   Z = 已退出并成为僵尸状态
        *   E = 已退出并死亡
        *   U = 不可运行
        *   I = 空闲
        *   M = 守护进程
        *   A = 全部

未使用的参数（在 2.6.35 中）：

*   `BTARGS` - bt 命令中要显示的参数数量（默认 9）
    *   用于内部例程 kdb_bt1 的 argcount，但该例程中从未使用 argcount
*   `BTSYMARG` - ？？？ [在 kdb_cmds 的'dumpall'和'dumpcpu'中设置，但未在代码中使用]
    *   似乎是一个整数

## 提示与技巧

### 命令行补全

kdb 支持使用 tab 键进行命令行补全。在交互式 shell 中键入时，您可以按 tab 键获取可用作命令一部分的符号列表。如果您键入符号名称的前几个字母，然后按 tab 键，shell 将为您补全名称。如果有多个符号匹配您键入的内容，则显示匹配符号的列表。显示的符号数量由 DTABCOUNT 变量控制。

### 定义一组命令

您可以使用`'defcmd'`命令定义一组命令作为一个组（按顺序）运行。该组本质上成为一个新命令，您可以使用指定的名称运行它。

新命令名称后的两个字符串是用法字符串和描述字符串。当运行`'help'`或`'?'`命令时，这些会出现在在线帮助中。

以下是定义新命令的示例：

```
defcmd dumpcommon "" "Common kdb debugging"
  set BTAPROMPT 0
  set LINES 10000
  -summary
  -cpu
  -ps
  -dmesg 600
  -bt
endefcmd 
```

前导破折号表示忽略处理命令时的任何错误。



## Executing commands on kdb initialization

In the kernel source, you can place commands in the file `kdb_cmds`. These commands will be executed by `kdb` on its initialization. By default, a few command sets are declared: `dumpcommon`, `dumpall`, and `dumpcpu`.

## Piping command results through `grep`

`kdb` includes a grep-like capability, which provides the ability to filter command results using a pattern. To use this, type the regular command, and at the end of the line add `| grep <pattern>`, where pattern is the pattern to match.

To see online help for this feature, type `grephelp` at the `kdb` shell prompt.

The pattern may include a very limited set of metacharacters:

```
pattern or ^pattern or pattern$ or ^pattern$
```

And if there are spaces in the pattern, you may quote it:

```
"pat tern" or "^pat tern" or "pat tern$" or "^pat tern$"
```

## Command history

You can access the command history by typing up-arrow and down-arrow, and select a previous command to run.

If you hit `<enter>` without typing a command, sometimes (when it makes sense) the last command run will be run again. For `md` commands, the next command will continue at the address where the last command left off.

## Feature extension notes (by Tim)

This section just has some random notes on Tim Bird's investigation of `KDB` (for kernel version `2.6.35`).

Regular users of `KDB` can ignore this...

- Can break on `__do_user_fault`, to break into `kdb` on user process `SIGSEGV` (on ARM, anyway).
- See `CONFIG_DEBUG_USER` (on ARM) for extra information shown and code paths used, on user-space faults.
- I can't set a breakpoint from `kdb_cmds` (on `kdb` initialization).
  - I get a hang (likely a panic before the console starts) on any breakpoint set on `kdb` initialization.
    - How to debug: 1) `printk` and `logbuf` visibility over reset? 2) Use of `qemu`??

### Internals

Internal functions to retrieve environment variables:

- `kdbgetintenv()`
- `kdbgetenv()`
- `kdbgetulenv()` - get unsigned long env variable

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Development Tools](http://eLinux.org/Category:Development_Tools "Category:Development Tools")

# Kdmx

> From: [eLinux.org](http://eLinux.org/Kdmx "http://eLinux.org/Kdmx")

## Contents

1. Overview
2. Source location
3. Example 1 (simple)
4. Example 2 (automate paths of `gdb` pty and terminal emulator pty)

## Overview

If the target board has a single serial port then a proxy on the host is needed to share the target port between the console and `kgdb`.

`kdmx` (`kgdb` demux) is one of the available proxy programs.

## Source location

The source is located in the `agent-proxy` git repository.

```text
https://git.kernel.org/cgit/utils/kernel/kgdb/agent-proxy.git/
git clone git://git.kernel.org/pub/scm/utils/kernel/kgdb/agent-proxy.git/
```

## Example 1 (simple)

This is a simple example, where I am using a USB serial port to connect between my host and target.

I did all of the commands in "host window 1" before I did the commands in "host window 2".

I did all of the commands in "host window 2" before I did the commands in "host window 3".

```text
+---------------------  HOST  -------------------------------------+                +--  TARGET  --+
|                                                                  |                |              |
|                                                                  |                |              |
v                                                                  v                v              v

terminal  <---->  /dev/pty/29  <---->  +------+
emulator                               |      |
                                       | kdmx |  <---->  serial port  <== cable ==> target console
gdb  <--------->  /dev/pty/53  <---->  |      |          /dev/ttyUSB0
                                       +------+
```

The absolute path of the kernel source directory is in `${LINUX_SOURCE}`.

The path of the kernel build directory, relative to the kernel source directory, is in `${KBUILD_OUTPUT}`.

```shell
$ echo ${LINUX_SOURCE}
/xxx/linux--3.17

$ echo ${KBUILD_OUTPUT}
../build/dragon_linus_3.17

$ echo ${LINUX_SOURCE}/${KBUILD_OUTPUT}
/xxx/linux--3.17/../build/dragon_linus_3.17

-----  host window 1 - kdmx  -----

$ export PS1='[1]: '
[1]: ./kdmx -n -d -p/dev/ttyUSB0 -b115200
serial port: /dev/ttyUSB0
Initalizing the serial port to 115200 8n1
/dev/pts/29 is slave pty for for terminal emulator
/dev/pts/53 is slave pty for gdb

-----  host window 2 - terminal emulator  -----

# In this example, I am using the sysrq debug command instead of the
# kernel command line 'kgdbwait' option to enter kgdb.
#
# The minicom "-o" option tells it not to initialize, so it does not
# send the "Init string" (defaults to "At S7=45 S0=0...") when you run
# minicom.

$ export PS1='[2]: '
[2]: minicom -o -w -p /dev/pts/29
Welcome to minicom 2.5

OPTIONS: I18n
Compiled on May  2 2011, 10:05:24.
Port /dev/tty8

Press CTRL-A Z for help on special keys

# Now in minicom, connected to the target console.
# CONFIG_PRINTK_TIME=y, so timestamps will be added to
# printk() messages to the console.

$ export PS1='% '
% cat /proc/version
Linux version 3.17.0-dirty (frank@ussvlx) (gcc version 4.6.x-google 20120106 (prerelease) (GCC) ) #1 SMP PREEMPT Mon Oct 6 10:19:37 PDT 2014
% echo g >/proc/sysrq-trigger
[   24.246292] SysRq : DEBUG
[   24.247184] Entering KGDB

-----  host window 3 - gdb  -----

$ export PS1='[3]: '
[3]: echo ${CROSS_COMPILE}
arm-eabi-
[3]: cd ${LINUX_SOURCE}
[3]: strings $KBUILD_OUTPUT/vmlinux | grep "^Linux version"
Linux version 3.17.0-dirty (frank@ussvlx) (gcc version 4.6.x-google 20120106 (prerelease) (GCC) ) #1 SMP PREEMPT Mon Oct 6 10:19:37 PDT 2014
Linux version
[3]: ${CROSS_COMPILE}gdb $KBUILD_OUTPUT/vmlinux
GNU gdb (GDB) 7.3.1-gg2
Copyright (C) 2011 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "--host=x86_64-linux-gnu --target=arm-linux-android".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>...
Reading symbols from /xxx/git_linus/build/dragon_linus_3.17/vmlinux...done.
(gdb) target remote  /dev/pts/53
Remote debugging using /dev/pts/53
kgdb_breakpoint ()
    at /xxx/git_linus/linux--3.17/kernel/debug/debug_core.c:1050
1050            arch_kgdb_breakpoint();
(gdb) b sys_sync
Breakpoint 1 at 0xc031d450: file /xxx/git_linus/linux--3.17/fs/sync.c, line 103.
(gdb) c
Continuing.
```

## Example 2 (automate paths of `gdb` pty and terminal emulator pty)

Keeping track of the paths of the pty slaves created by `kdmx` can be annoying, so the status file feature has been added in `kdmx` version `141210a` to automate use of the paths by `gdb` and the terminal emulator.

The status file feature is enabled with the `-s` option, which will create files containing the paths of the `gdb` slave pty and the terminal emulator pty. Each time a slave pty is opened, the contents of the respective status file is updated. The `-s` option provides the path, including a root for the file name, for the location of the status files. The strings `_gdb` and `_trm` will be appended to the path to form the names of the status files.

The absolute path of the kernel source directory is in `${LINUX_SOURCE}`.

The path of the kernel build directory, relative to the kernel source directory, is in `${KBUILD_OUTPUT}`.

```shell
$ echo ${LINUX_SOURCE}
/xxx/linux--3.18

$ echo ${KBUILD_OUTPUT}
../build/dragon_linus_3.18

$ echo ${LINUX_SOURCE}/${KBUILD_OUTPUT}
/xxx/linux--3.18/../build/dragon_linus_3.18
```

In this example, I place the status files in my kernel build directory.



# Debugging The Linux Kernel Using Gdb

> 来源：[eLinux.org](http://eLinux.org/Debugging_The_Linux_Kernel_Using_Gdb "http://eLinux.org/Debugging_The_Linux_Kernel_Using_Gdb")

## 目录

- [1 使用 gdb 调试 Linux 内核](#1-使用-gdb-调试-linux-内核)
  - [1.1 要求](#11-要求)
  - [1.2 基础知识](#12-基础知识)
    - [1.2.1 vmlinuz 与 zImage](#121-vmlinuz-与-zimage)
    - [1.2.2 调试内核](#122-调试内核)
    - [1.2.3 在内存中加载内核](#123-在内存中加载内核)
    - [1.2.4 获取内核日志缓冲区](#124-获取内核日志缓冲区)
    - [1.2.5 调试内核模块（.o 和 .ko）](#125-调试内核模块o-和-ko)
  - [1.3 确定模块加载地址](#13-确定模块加载地址)
  - [1.4 加载已加载模块的符号](#14-加载已加载模块的符号)
  - [1.5 指针](#15-指针)

## 使用 gdb 调试 Linux 内核

日常内核调试的大部分工作是通过在代码中添加打印语句（使用著名的`printk`函数）来完成的。这种技术在[内核调试技巧](http://eLinux.org/Kernel_Debugging_Tips "Kernel Debugging Tips")中有详细描述。使用`printk`是一种相对简单、有效且廉价的问题查找方法。但还有许多其他 Linux 特有的技术可以将调试和分析提升到更高水平。在本页中，我们将讨论使用 GNU 调试器（GDB）进行内核调试。[GDB](http://eLinux.org/GDB "GDB")页面描述了一些基本的 gdb 命令，并提供了良好的文档链接。总的来说，开始使用 gdb 进行内核调试相对容易。

这里的大多数示例适用于两种（开源）场景：使用[JTAG](http://eLinux.org/JTAG "JTAG")和使用[QEMU](http://eLinux.org/Qemu "Qemu")系统仿真。由于第二种选项不需要任何硬件，您可以立即尝试！

开源 JTAG 调试领域并不大。在调试能力方面表现突出的一个项目是 OpenOCD，本文档中使用的工具就是它。[OpenOCD](http://openocd.berlios.de/web/)在我们测试的 ARM11 和 ARM9 目标上非常实用。

## 要求

**GDB：**

您需要获取一个能够理解目标架构的 GDB。通常，这会随交叉编译器一起提供，但如果需要，您也可以自行编译，但您需要理解`--target`和`--host`配置选项之间的区别。GDB 将在主机（例如 x86）上运行，但需要能够理解目标架构（例如 armv6）。您可能还需要`gdbserver`作为用户态调试的存根。

**OpenOCD：**

待补充...

**JTAG 调试器：**

待补充...

## 基础知识

![内核 gdb 调试组件概览图](http://eLinux.org/File:Kernel_gdb_debugging_component_overvierw_small.png)

### 主机窗口 1 - kdmx

```
$ export PS1='[1]: '
[1]: kdmx -n -d -p/dev/ttyUSB0 -b115200 -s${LINUX_SOURCE}/${KBUILD_OUTPUT}/zzz__kdmx_pty
gdb status file: /xxx/linux--3.18/../build/dragon_linus_3.18/zzz__kdmx_pty_gdb
terminal emulator status file: /xxx/linux--3.18/../build/dragon_linus_3.18/zzz__kdmx_pty_trm
serial port: /dev/ttyUSB0
Initalizing the serial port to 115200 8n1
/dev/pts/44 is slave pty for terminal emulator
/dev/pts/45 is slave pty for gdb

Use <ctrl>C to terminate program 
```

以下是状态文件的内容：

```
$ ls -l ${LINUX_SOURCE}/${KBUILD_OUTPUT}/zzz__kdmx_pty*
-rw-r----- 1 frank frank_group 12 Dec 10 22:07 /xxx/linux--3.18/../build/dragon_linus_3.18/zzz__kdmx_pty_gdb
-rw-r----- 1 frank frank_group 12 Dec 10 22:07 /xxx/linux--3.18/../build/dragon_linus_3.18/zzz__kdmx_pty_trm
$ for k in `ls ${LINUX_SOURCE}/${KBUILD_OUTPUT}/zzz__kdmx_pty*`; do echo "$k:" ; cat $k; echo ; done
/xxx/linux--3.18/../build/dragon_linus_3.18/zzz__kdmx_pty_gdb:
/dev/pts/45

/xxx/linux--3.18/../build/dragon_linus_3.18/zzz__kdmx_pty_trm:
/dev/pts/44 
```

终端仿真器的从属 pty 路径从相应的状态文件中获取，并提供给 minicom：

### 主机窗口 2 - 终端仿真器

```
$ export PS1='[2]: '
[2]: minicom -o -w -p `cat ${LINUX_SOURCE}/${KBUILD_OUTPUT}/zzz__kdmx_pty_trm`
Welcome to minicom 2.5

OPTIONS: I18n
Compiled on May  2 2011, 10:05:24.
Port /dev/tty8

Press CTRL-A Z for help on special keys

$ export PS1='% '
% cat /proc/version
Linux version 3.18.0-dirty (frank@ussvlx) (gcc version 4.6.x-google 20120106 (prerelease) (GCC) ) #1 SMP PREEMPT Mon Dec 8 12:27:26 PST 2014
% echo g > /proc/sysrq-trigger
[210227.044514] SysRq : DEBUG 
```

将 gdb 从属 pty 的路径传递给 gdb 的任务稍微复杂一些。（欢迎提供更直接方法的任何建议。）

以下 shell 脚本用于调用适当的 gdb，并创建一个用户定义的 gdb 命令来连接到正确的 pty 路径。`${CROSS_COMPILE}`确保使用为目标架构构建的 gdb。

```
#! /bin/bash

kgdb_set_pty_cmd=`mktemp --tmpdir kgdb_set_pty_cmd.XXXXXXXXXX` || exit 1

# user defined command
#
#   \x5c is '\'
#
echo -e \
   "define tr"                                                                 \
   "\ndont-repeat"                                                             \
   "\necho target remote"                                                      \
   "`cat ${LINUX_SOURCE}/${KBUILD_OUTPUT}/zzz__kdmx_pty_gdb`"                  \
   "\x5cn"                                                                     \
   "\ntarget remote"                                                           \
   `cat ${LINUX_SOURCE}/${KBUILD_OUTPUT}/zzz__kdmx_pty_gdb`                    \
   "\nend"                                                                     \
   "\n"                                                                        \
   "\ndocument tr"                                                             \
   "\ntarget remote to the kdmx gdb pty"                                       \
   "\n"                                                                        \
   "\nThe kdmx gdb pty to be used is: "                                        \
   `cat ${LINUX_SOURCE}/${KBUILD_OUTPUT}/zzz__kdmx_pty_gdb`                    \
   "\nThe kdmx gdb pty was determined at gdb startup.  If the kdmx gdb pty"    \
   "\nhas changed since then, restart gdb"                                     \
   "\n"                                                                        \
   "\nend"                                                                     \
   > ${kgdb_set_pty_cmd}

echo "${CROSS_COMPILE}gdb -x ${kgdb_set_pty_cmd} $KBUILD_OUTPUT/vmlinux"
      ${CROSS_COMPILE}gdb -x ${kgdb_set_pty_cmd} $KBUILD_OUTPUT/vmlinux

rm ${kgdb_set_pty_cmd}
```

### 主机窗口 3 - gdb

```
$ export PS1='[3]: '
[3]: echo ${CROSS_COMPILE}
arm-eabi-
[3]: cd ${LINUX_SOURCE}
[3]: tcgdb
arm-eabi-gdb -x /tmp/kgdb_set_pty_cmd.4xKNf2ah0T ../build/dragon_linus_3.18/vmlinux
GNU gdb (GDB) 7.3.1-gg2
Copyright (C) 2011 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.  Type "show copying"
and "show warranty" for details.
This GDB was configured as "--host=x86_64-linux-gnu --target=arm-linux-android".
For bug reporting instructions, please see:
<http://www.gnu.org/software/gdb/bugs/>...
Reading symbols from /local/nobackup/src/git_linus/build/dragon_linus_3.18/vmlinux...done.
(gdb) help tr
target remote to the kdmx gdb pty

The kdmx gdb pty to be used is:  /dev/pts/45
The kdmx gdb pty was determined at gdb startup.  If the kdmx gdb pty
has changed since then, restart gdb

(gdb) tr
target remote /dev/pts/45
kgdb_breakpoint () at /local/nobackup/src/git_linus/linux--3.18/kernel/debug/debug_core.c:1050
1050        arch_kgdb_breakpoint();
(gdb) b sys_sync
Breakpoint 1 at 0xc031f7b4: file /local/nobackup/src/git_linus/linux--3.18/fs/sync.c, line 103.
(gdb) c
Continuing. 
```

### vmlinuz 与 zImage

（此部分内容在原文中未提供具体内容，仅保留标题结构。）

### 调试内核

（此部分内容在原文中未提供具体内容，仅保留标题结构。）

### 在内存中加载内核

（此部分内容在原文中未提供具体内容，仅保留标题结构。）

### 获取内核日志缓冲区

（此部分内容在原文中未提供具体内容，仅保留标题结构。）

### 调试内核模块（.o 和 .ko）

（此部分内容在原文中未提供具体内容，仅保留标题结构。）

### 确定模块加载地址

（此部分内容在原文中未提供具体内容，仅保留标题结构。）

### 加载已加载模块的符号

（此部分内容在原文中未提供具体内容，仅保留标题结构。）

### 指针

（此部分内容在原文中未提供具体内容，仅保留标题结构。）



要调试内核，你需要将其配置为包含调试符号。完成此操作后，你就可以进行正常的内核开发。当需要时，你可以“挂接”你的调试器，开始调试正在运行的内核。

*   启动`openocd`

### `vmlinuz`与`zImage`

当你想要调试内核时，需要对内核的组成方式有所了解。最重要的是`vmlinux`和`zImage`之间的区别。此时你需要理解的是，`zImage`是一个容器。该容器由引导加载程序加载，并将执行权移交给`zImage`。这个`zImage`将内核解压到相同的内存位置，并开始执行内核。（说明`vmlinux`不一定是真正的内核，因为可以使用未剥离的`vmlinux`来调试“剥离”的内核）。总的来说，如果我们查看编译后的内核，我们会发现`vmlinux`位于内核树的根目录，而`zImage`位于`arch/arm/boot`下。

```
vmlinux
arch/arm/boot
`-- zImage 
```

`vmlinux`将是我们调试Linux内核时使用的文件。

### 调试内核

这里描述的基于JTAG的调试方法是非侵入式的。这意味着除了调试符号之外，你不需要以任何方式修改内核。这是因为我们在硬件、CPU核心级别上操作。总的来说，这意味着你可以遵循正常的开发方法。你可以让你的引导程序和引导加载程序完成它们的工作，例如，开始调试正在运行的内核。如果你的`gdb`调试器正在运行，只需加载`vmlinuz`并连接到远程目标即可：

```
load vmlinuz
target remote :3333 
```

### 在内存中加载内核

一旦你习惯了使用`gdb`调试内核，你就会希望使用`gdb`直接将内核加载到目标板上。最实用的方法是，在内核启动位置设置一个硬件断点，然后使用JTAG复位信号复位你的开发板。你的引导加载程序将初始化开发板，并且执行将在内核启动位置停止。之后，你可以将内核加载到内存中并运行它。

执行以下操作：

```
(gdb) file vmlinux
(gdb) target remote :3333
(gdb) break __init_begin
(gdb) cont
(gdb) mon reset #perhaps this needs to be done from the openocd telnet session..
Breakpoint 1, 0xc0008000 in stext ()
(gdb) load vmlinux
Loading section .text.head, size 0x240 lma 0xc0008000
Loading section .init, size 0xe4dc0 lma 0xc0008240
Loading section .text, size 0x219558 lma 0xc00ed000
Loading section .text.init, size 0x7c lma 0xc0306558
Loading section __ksymtab, size 0x4138 lma 0xc0307000
Loading section __ksymtab_gpl, size 0x1150 lma 0xc030b138
Loading section __kcrctab, size 0x209c lma 0xc030c288
Loading section __kcrctab_gpl, size 0x8a8 lma 0xc030e324
Loading section __ksymtab_strings, size 0xc040 lma 0xc030ebcc
Loading section __param, size 0x2e4 lma 0xc031ac0c
Loading section .data, size 0x1e76c lma 0xc031c000
Start address 0xc0008000, load size 3345456
Transfer rate: 64 KB/sec, 15632 bytes/write.
(gdb) cont 
```

这将启动通过JTAG加载到内存中的内核。

### 获取内核日志缓冲区

有时内核会在串口启动并运行之前发生恐慌。在这种情况下，能够转储内核日志缓冲区是非常有用的。这可以通过查看内核中`__log_buf`的内容来实现。在`gdb`中，可以通过发出以下命令来完成：

```
p (char*) &__log_buf[log_start] 
```

必须有一种简单的方法来打印`log_start`和`log_end`之间的内存区域。

问题是`gdb`在第一行之后停止。目前，我们使用这个从`wchar.gdb`复制的例程，直到有“正常”的东西出现。我们这样定义`dmesg`：

```
define dmesg
        set $__log_buf = $arg0
        set $log_start = $arg1
        set $log_end = $arg2
        set $x = $log_start
        echo "
        while ($x < $log_end)
                set $c = (char)(($__log_buf)[$x++])
                printf "%c" , $c
        end
        echo "\n
end
document dmesg
dmesg __log_buf log_start log_end
Print the content of the kernel message buffer
end 
```

并像这样调用它：

```
dmesg __log_buf log_start log_end 
```

### 调试内核模块（`.o`和`.ko`）

调试内核模块比较困难。

## 确定模块加载地址

`gdb`本身并不了解内核模块，并且在调试内核模块时，我们需要稍微帮助一下`gdb`。模块的一个问题是，在模块实际加载之前，无法确定模块将加载到内存中的哪个位置，因此只有在模块加载后，我们才需要确定它在内存中的地址并告知`gdb`。有很多方法可以确定此信息。这里有3种方法：

```
lsmod

cat /sys/module/mydriver/sections/.text

 #gdb implementation of the linux lsmod
 define lsmod
        set $current = modules.next
        set $offset =  ((int)&((struct module *)0).list)
    printf "Module\tAddress\n"

    while($current.next != modules.next)
                printf "%s\t%p\n",  \
                        ((struct module *) (((void *) ($current)) - $offset ) )->name ,\
                        ((struct module *) (((void *) ($current)) - $offset ) )->module_core
                set $current = $current.next
        end
end 
```

## 加载已加载模块的符号

```
add-symbol-file drivers/mydrivers/mydriver.o 0xbf098000 
```

请注意，我们使用的是`.o`文件而不是`.ko`文件。末尾的地址是内核决定加载模块的地址。

## 指针

在Linux文档目录下的`kdump`中，你会找到一个名为`gdbmacros.txt`的文件，它看起来非常有前途，因为它包含了一个`dmesg`实现。

```
head  linux-2.6.22.1/Documentation/kdump/gdbmacros.txt
#
# This file contains a few gdb macros (user defined commands) to extract
# useful information from kernel crashdump (kdump) like stack traces of
# all the processes or a particular process and trapinfo.
# 
```

在Linux内核目录中执行`find . -name "*gdb*"`也会显示一些有趣的`.gdbinit`文件，这些文件显然可以执行低级初始化。

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Development Tools](http://eLinux.org/Category:Development_Tools "Category:Development_Tools")

# MagicSysRq

> 来自：[eLinux.org](http://eLinux.org/MagicSysRq "http://eLinux.org/MagicSysRq")

# MagicSysRq

* * *

**注意**：本文目前只是一个草稿，并且是我将在未来几个月内发布的一系列文章的一部分——如果你想为此做出贡献，请随意。但是，如果你能与[我](http://eLinux.org/User:Peter_Huewe "User:Peter Huewe")协调你的工作，那就太好了。

本文仍在编写中，仍需要大量工作。

* * *

## 目录

*   1 引言

*   2 示例

*   3 故障排除

*   4 重要文件

*   5 外部链接

## 引言

`MagicSysRq`是一个特殊的组合键，它允许用户执行内核的某些低级任务，并且在系统似乎完全挂起时特别有用。例如，`MagicSysRq`使得能够或多或少地干净地关闭一个甚至对`CTRL+ALT+DEL`都没有响应的系统。

`MagicSysRq`功能通过按下`ALT+SysRq+功能键`来调用，其中功能键描述以下之一。

TODO:在此插入表格

## 示例



The probably most used combination of MagicSysRq functions is the one `RSEIUB`, which can be easyly remebered by the mnemonic trick ``Raising Elephants is so utterly boring*\footnote{``You can still find several references the* mnemonic *Raising Skinny Elephants is utterly boring* on the internet - however it is probably better to do the sync after the tasks exited/were killed} - although we're dealing with penguins here ;)

According to the table above this performs, in order:

- `R`: Put Keyboard in Raw Mode
- `E`: terminate all tasks
- `I`: kill all tasks
- `S`: Sync
- `U`: remount all filesystems read-only
- `B`: Reboot

## Troubleshooting

You can easily and safely check whether MagicSysRq works on your System by pressing `Alt+SysRq+H` - on a console you should now see a short help text of the MagicSysRq Feature or at least print this to `dmesg`.

If you don't see the help text, check whether `CONFIG_MAGIC_SYSRQ=y` is set in your Kernel Config. If it is set, please check the output of `cat /proc/sys/kernel/sysrq`, which should report `1` if MagicSysRq is enabled. To enable it, just do a simple `echo 1 > /proc/sys/kernel/sysrq`.

## Important Files

- `/proc/sys/kernel/sysrq` - enable/disable MagicSysRq at runtime
- `/proc/sysrq-trigger` - trigger MagicSysRq from the console (e.g. useful over ssh)

## TODO Content

- Explanation of remaining keys
- Using it over serial line -> `BREAK+key`, in kermit `ctrl-\ b KEY`
- Interaction with KDB
- Interaction with kexec / crashkernel

## External Links

- [Wikipedia Article about Magic_SysRq_key](http://en.wikipedia.org/wiki/Magic_SysRq_key)
- [Kernel Documentation/sysrq.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob;f=Documentation/sysrq.txt;hb=HEAD)

[Categories](http://eLinux.org/Special:Categories "Special:Categories"):

- [Development Tools](http://eLinux.org/Category:Development_Tools "Category:Development Tools")
- [Tips and Tricks](http://eLinux.org/Category:Tips_and_Tricks "Category:Tips and Tricks")

## External Links

- [Embedded Linux JTAG debugging (CELF presentation)](http://tree.celinuxforum.org/CelfPubWiki/ELC2009Presentations?action=AttachFile&do=get&target=DebuggingWithJtagCelf2009.pdf)
- [Debugging the Linux kernel using Eclipse/CDT and QEMU](http://issaris.blogspot.com/2007/12/download-linux-kernel-sourcecode-from.html)

# 内核跟踪与分析

# Kernel Tracing and Profiling

About kernel tracing and profiling tools and their usage.

## System Tap

> From: [eLinux.org](http://eLinux.org/System_Tap "http://eLinux.org/System_Tap")

This page has information about `System Tap`, which is of interest to embedded developers, because tracers are a useful tool for diagnosing problems during product development.

## Contents

1. Introduction
2. Open Source Projects/Mailing Lists
3. Miscellaneous notes
   1. Probe types
4. See Also
   1. ARM Support
5. Some Performance measurements
6. Links

## Introduction

SystemTap is a flexible and extensible system for adding trace collection and analysis to a running Linux kernel.

SystemTap is designed to be very flexible (allowing for the insertion of arbitrary C code), yet also easy-to-use (most trace statements are written in a simple scripting language, with useful data collection and aggregation routines available in (essentially) library form).

A key aspect of SystemTap is that it is intended to allow you to create a trace set (a "tapset"), and run it on a running Linux system, with no modification or re-compilation of the system required. To do this, it uses the kernel [KProbes](http://www-users.cs.umn.edu/~boutcher/kprobes/) interface and loadable kernel modules to dynamically add probe points and newly generated code to the running kernel.

## Open Source Projects/Mailing Lists

The main SystemTap site is at: [`sourceware.org/systemtap/`](http://sourceware.org/systemtap/)

The SystemTap mail list archives are at: [`sourceware.org/ml/systemtap/`](http://sourceware.org/ml/systemtap/)

The tutorial, which gives a good overview of the system, is at: [`sourceware.org/systemtap/tutorial/`](http://sourceware.org/systemtap/tutorial/)

## Miscellaneous Notes

### Probe Types

There are several types of probes:

- `kprobe` & `kretprobe`, for dynamically insterted probes
- Timers
- Static instrumentation markers
- Performance counter events

In the future, there may be:

- User-space probes
- User-space return probes
- Watchpoint probes (kernel & user)
- And more

## See Also

Note that SystemTap is one of the major tracing systems for the Linux kernel.

There is work afoot (as of spring 2006) to try to collaborate on different parts of the tracing problem, between some of the major tracing projects. See the [Tracing Collaboration Project](http://eLinux.org/Tracing_Collaboration_Project "Tracing Collaboration Project") page for more information.

### ARM Support

System Tap works on ARM & OMAP platforms; instructions are available [here](http://omappedia.org/wiki/Systemtap).

## Some Performance Measurements

Jian Gui writes (in July 2006 on the `System Tap` mailing list):



```
Hi, we've tested the overhead of systemtap/LKET with some benchmarks
on a ppc64 machine.

It shows the overhead of systemtap/LKET is acceptable generally.
But it will also cause significant overhead for some benchmark of
special behavior, e.g. dbench. Dbench calls `kill()` in a very high
frequency to check whether a task is complete, thus leads to a high
overhead.

We categorized the event hooks into five groups in the testing:
grp1 - syscall.entry, process
grp2 - syscall.return, process
grp3 - iosyscall, ioscheduler, scsi, aio, process
grp4 - tskdispatch, pagefault, netdev, process
grp5 - syscall.entry, syscall.return, process

All the results are
   (score1 - score2)/score2 * 100%,  where:
score1: the benchmark score when probed by systemtap
score2: the benchmark score without probing

dbench (<3% is noise)
--------------------
grp1            -14.4%
grp2            -33.1%
grp3            -7.92%
grp4            -13.6%
grp5            -43.3%

specjbb (<3% is noise)
---------------------
grp 1           -0.87%
grp 2           -0.67%
grp 4           +0.47%
grp 5           +0.05%

tiobench (<3% is noise)
----------------------
grp1       sequential reads      +1.45%
           sequential writes     -6.98%
           random reads          +0.57%
           random writes         -2.11%
grp2       sequential reads      +0.11%
           sequential writes     -5.81%
           random reads          +0.03%
           random writes         -2.11%
grp3       sequential reads      +1.42%
           sequential writes     -6.98%
           random reads          +0.51%
           random writes         -2.11%
grp4       sequential reads      +1.38%
           sequential writes     -5.81%
           random reads          +0.60%
           random writes         -2.11%
grp5       sequential reads      +0.22%
           sequential writes     -8.14%
           random reads          -0.10%
           random writes         -1.05%

Rawiobench (<3% is noise)
------------------------
grp1       sequential `aioread()`     0%
           sequential `aiowrite()`    0%
           random `aioread()`         0%
           random `aiowrite()`        0%
grp2       sequential `aioread()`     0%
           sequential `aiowrite()`    0%
           random `aioread()`         0%
           random `aiowrite()`         -0.82%
grp3       sequential `aioread()`     0%
           sequential `aiowrite()`    0%
           random `aioread()`         0%
           random `aiowrite()`        0%
grp4       sequential `aioread()`     0%
           sequential `aiowrite()`    0%
           random `aioread()`         +0.79%
           random `aiowrite()`        -0.82%
grp5       sequential `aioread()`     0%
           sequential `aiowrite()`    -6.41%
           random `aioread()`         +0.79%
           random `aiowrite()`        0%
  
Test environment:
Machine:  Open Power 720/ 8 cpus/ 2 cores/ 6GB RAM (tiobench use 1G)
Software: RHEL4-U3GA/ 2.6.17.2/ systemtap-20060718/ elfutils-0.122-0.4 
```

## Links

- [SystemTap Sans Kernel: A Pure Userspace Backend](https://events.linuxfoundation.org/events/collaboration-summit/stone)
  - [Slides](https://events.linuxfoundation.org/images/stories/pdf/lfcs2012_jstone.pdf)
  - [Video](http://video.linux.com/videos/systemtap-sans-kernel-a-pure-userspace-backend)

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Development Tools](http://eLinux.org/Category:Development_Tools "Category:Development Tools")

# Kernel Trace Systems

> From: [eLinux.org](http://eLinux.org/Kernel_Trace_Systems "http://eLinux.org/Kernel_Trace_Systems")

Here are some links to information about different kernel tracing systems:

## Contents

1. General Purpose tracing systems
2. Special Purpose tracing systems
3. Trace Infrastructure
4. Sampling Systems
5. Related facilities
6. Other Systems
7. Collaboration Efforts

## General Purpose tracing systems

Some major Linux general-purpose tracing systems are:

- `ptrace` - ability to trace syscall entry and exit, and signal delivery, to a process (also used for debugging a process)
  - see "man `ptrace`" and "man `strace`"
- `Ftrace`
  - Ftrace Function Graph ARM - presentations and patches by Tim Bird to add function graph and duration tracing to ARM systems
    - The presentation has good introductory material on ftrace, as well as links to additional resources
  - tracer for kernel functions
  - can also be used for debugging or analyzing latencies and performance issues
  - in mainline since 2.6.27
  - See [Measuring Function Duration with FTrace](http://eLinux.org/Measuring_Function_Duration_with_FTrace "Measuring Function Duration with FTrace")
    - outline of presentation by Tim Bird for Linux Symposium 2009
- `System Tap` - System Tap is a system for building and executing tracing and sampling systems that can be applied to a running Linux system
- `LTTng` - Linux Trace Toolkit, next generation
- `LKST` - Linux Kernel State Tracer

## Special Purpose tracing systems

There are some other notable special-purpose kernel tracing systems:

- `KFT` - Kernel Function Trace - traces functions to show function durations and call graphs
- latency trace - RT-preempt tool for measuring interrupt and mutex latency
  - The latency tracer is embedded in the RT-preempt patch - see Realtime Preemption and [RT-preempt Article](http://lwn.net/Articles/97811/)
- block tracer (`blktrace`) - allows you to see exactly what is going on in the block layer for a given queue
  - Introduction by Jens Axboe: [Introduction](http://lwn.net/Articles/148761/)
  - Execellent presentation: [blktrace.pdf](http://www.gelato.org/pdf/apr2006/gelato_ICE06apr_blktrace_brunelle_hp.pdf)
  - Guide to using is at: [blktrace guide](https://secure.engr.oregonstate.edu/wiki/CS411/index.php/Blktrace_Guide)
  - This appears to have been mainlined as of 2.6.17
  - Timeline utility (blktrace post-processing tool): [blktrace timeline utility](http://www.nabble.com/NEW%3A-btt---blktrace-timeline-utility%3A-analyze-I-Os-collected-with-blktrace.-tf1644874.html)
- delay accounting patches - collect statistics about the delays that are experienced by each task on the system
  - see [delay accounting patches](http://lkml.org/lkml/2006/5/2/30)

## Trace Infrastructure

- `KProbes` - grew out of dprobes, with information at: [dprobes](http://dprobes.sourceforge.net/)
  - see an excellent tutorial at: [kprobes](http://www-users.cs.umn.edu/~boutcher/kprobes/)
  - The mainline version of the KProbes supports x86, Alpha and PPC64 architectures. A MIPS implementation has been completed on the 2.6.16 kernel and tested on the Toshiba TX49 platform. Patch is available in the [Patch Archive](http://eLinux.org/Patch_Archive "Patch Archive").
- [would be nice to have some djprobe stuff here]

## Sampling Systems

Note that profile systems (or "sampling systems") are slightly different, in that they involve sampling instead of event tracing. Some major ones for Linux are:

- `top` - provides a dynamic real-time view of a running system, including processes
  - see "man `top`"
  - see also `ksysguard`, [Gnome system Monitor](http://freshmeat.net/projects/gnome-system-monitor/)
- `OProfile` - system-wide profiler for Linux systems
  - see [oprofile](http://oprofile.sourceforge.net/about/)
  - also: [oprofile at IBM](http://www-128.ibm.com/developerworks/linux/library/l-oprof.html)
- `BootChart` - samples bootup and provides visualization of process startup and system utilization
  - see Bootchart

## Related facilities

- in-kernel statistics infrastructure - proposal for a generic implementation of statistics facilities inside the kernel
  - see [inkernel stats](http://lkml.org/lkml/2006/5/19/106)
- `perfmon2` - interfaces to hardware performance monitoring features of the CPU
  - see [perfmon](http://perfmon2.sourceforge.net/)



- [inotify](http://www-128.ibm.com/developerworks/linux/library/l-inotify.html)

## Other Systems

Here are some systems I haven't classified yet:

- Datastreams - a system for creating and monitoring tracepoints - see [datastreams](http://kusp.ittc.ku.edu/wiki/index.php/Main_Page)

## Collaboration Efforts

Some trace system project leaders are trying to collaborate: see [Tracing Collaboration Project](http://eLinux.org/Tracing_Collaboration_Project "Tracing Collaboration Project")

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Linux tracing](http://eLinux.org/Category:Linux_tracing "Category:Linux tracing")

# Linux Trace Toolkit

> From: [eLinux.org](http://eLinux.org/Linux_Trace_Toolkit "http://eLinux.org/Linux_Trace_Toolkit")

# Linux Trace Toolkit

**Preliminary Draft** — under construction

## Contents

1. Introduction
   1. Rationale
2. Downloads
   1. LTTng
   2. Sample i386 trace for LTTng
   3. 0.9.6 Release (Nov 21, 2004)
   4. Older stuff
   5. Getting attachments from ltt-dev archive
   6. Patch
   7. Utility programs
3. How To Use
   1. Building the software
   2. Using the software
4. References
5. Sample Results
6. Future Work
7. LKML Reaction to tracing

## Introduction

The Linux Trace Toolkit is used to examine the flow of execution (between processes, kernel threads, and interrupts) in a Linux system. This is useful for analyzing where delays occur in the system, and to see how processes interact (especially with regard to scheduling, interrupts, synchronization primitives, etc.)

![Alert.gif](http://eLinux.org/File:Alert.gif)

Note that as of 2.6.14, LTT is being replaced with LTTng. See [LTTng](http://ltt.polymtl.ca/).

See also the announcement here: [Patch: Linux Trace Toolkit Viewer/Next Generation announcement (LTTV/LTTng)](http://lwn.net/Articles/170198/)

### Rationale

Tracing is useful for analyzing stuff.

## Downloads

### LTTng

See the QUICKSTART guide at: [Quickstart](http://ltt.polymtl.ca/svn/ltt/branches/poly/QUICKSTART)

### Sample i386 trace for LTTng

Here is a zip file containing a sample trace on an i386 machine: `i386-ltt-trace.zip`

### 0.9.6 Release (Nov 21, 2004)

I found it a bit difficult to get the appropriate set of patches for LTT. After a bit of frustration, I built my own release for Nov. 23,

1. The release is 0.9.6 (no 'pre') and it works with the Linux kernel 2.6.9. The tar file for the release is in the PatchArchive.

### Older stuff

The latest stable release is 0.9.5a, but this release is over 2 years old.

Here is the patch set I finally used, for kernel 2.6.8.1:

- [message with `ltt-2.6.8.1-relayfs.patch.bz2` by Mathieu Desnoyers](http://www.listserv.shafik.org/pipermail/ltt-dev/2004-August/000638.html)
- [message with `ltt-2.6.8.1-ltt.patch.bz2` by Mathieu Desnoyers](http://www.listserv.shafik.org/pipermail/ltt-dev/2004-August/000637.html)

### Getting attachments from ltt-dev archive

I had to use `munpack` to extract the compressed patches from the mail messages in the archive. `munpack` is part of the package `mpack`, which is available at: `munpack`

### Patch

Here are some patches used by Tim Bird at Sony, targeted at MIPS, but known to also work on other platforms. This tarball contains both an all-in-one patch and a series file with discreet sub-patches.

- [Ltt-2.6.11-from-TimBird.tgz](http://eLinux.org/images/b/b5/Ltt-2.6.11-from-TimBird.tgz "Ltt-2.6.11-from-TimBird.tgz")

- Patches for Linux kernel version 2.6.8.1, and TraceToolkit tarfile are here:
  - `ltt-2.6.8.1.tar.gz`
  - `TraceToolkit-0.9.6pre3-plus.tar.gz`

These are bundles with multiple sub-patches and sub-tars. To install them, do the following:

- Untar kernel patches:

  ```bash
  tar -xzvf ltt-2.6.8.1.tar.gz
  ```

- Apply patches:

  ```bash
  ./tpm -t linux-2.6.8.1.tar.bz2 -f ltt-2.6.8.1.pl -o linux-2.6.8.1-ltt
  ```

- Untar TraceToolkit stuff:

  ```bash
  tar -xzvf TraceToolkit-0.9.6pre3-plus.tar.gz
  ```

- Unpack and apply patch:

  ```bash
  ./tpm -f TraceToolkit-0.9.6pre3-plus.pl -o TraceToolkit
  ```

Now, follow the build and usage instructions for the software in the include docs (`TraceToolkit/Help/index.html`). For cross-compiling, use the instructions on this wiki page.

### Utility programs

## How To Use

### Building the software

Apply the ltt and relayfs patches to your kernel:

- Configure kernel with LTT.
- Turn on RelayFS and LTT.

Run `make menuconfig` and select:

- `File systems ---> Pseudo filesystems ---> Relayfs file system support`
- `General Setup ---> Linux Trace Toolkit support`

You can leave klog debugging support turned off.

Compile the user-space `tracedaemon` program:

I couldn't figure out if the `tracevisualizer` tools handle cross-compilation correctly, by which I mean that you can natively compile the `tracevisualizer` but cross-compile the `tracedaemon`. Instead of blindly trying configure tricks, I instead used the instructions from Karim's book "Building Embedded Linux Systems". In a nutshell, the instructions go something like this:

#### Overview

```text
* install source for user-space stuff
* configure for native build
* hand-build tracedaemon specifying a cross-compiler
* build rest of user-space suite using native compiler
* install programs as appropriate
```

#### Detail

In my case:

```text
* install TraceToolkit-0.9.6pre3, apply "plus" patch
  ** tpm -f user-space.pl -o TraceToolkit-0.9.6pre3
* cd TraceToolkit-0.9.6pre3
* configure --prefix=/home/tbird/work/ltt/tools
* make -C LibUserTrace CC=<cross-compiler-gcc> UserTrace.o
* make -C LibUserTrace CC=<cross-compiler-gcc> LDFLAGS="-static"
* make -C Daemon CC=<cross-compiler-gcc> LDFLAGS="-static"
* cp Daemon/tracedaemon Daemon/Scripts/trace Daemon/Scripts/tracecore
```

`Daemon/Scripts/traceu <target file="" systeu0005c="" class="calibre16">/usr/sbin</target>`

```text
* make
* make install
```

### Using the software

In April, 2004, Karim wrote: [lkml thread](http://lkml.org/lkml/2004/4/3/100)

> The documentation is out of date. Basically, the `createdev.sh` script isn't needed anymore because of relayfs. You need to mount relayfs to use LTT. See the classic dox on filesystem mounting for this kind of thing. It's going to be something like:
>
> `mount -t relayfs nodev /mnt/relay`

There's no `insmod` for LTT. It isn't a device driver module, following LKML recommendations.

## References

- LTT home page is at: [LTT](http://www.opersys.com/LTT/)
- Presentation from OLS 2006:
  - [LTTng Tracer: A low impact performance and behavior monitor for GNU/Linux](http://ltt.polymtl.ca/slides/desnoyers-talk-ols2006.pdf)
- Online documentation is at: [LTT Documentation](http://www.opersys.com/LTT/dox/ltt-online-help/index.html)
  - This documentation is a bit old (2002), and has parts that are out of date.

## Sample Results

## Future Work

Here is a list of things that could be worked on for this feature:

- Online reference needs to be updated.
  - E.g. no mention of relayfs.
- Project seems fairly quiet, and unmaintained.
- See if LTT patch should be refactored to take into account new kprobe support in the kernel.

## LKML Reaction to tracing

In Sep 2002, there was a thread about tracing, where some major kernel developers expressed their concerns about tracing infrastructure in the kernel.

- [Ingo Molnar](http://seclists.org/lists/linux-kernel/2002/Sep/5094.html)

> My problem with this stuff is conceptual: it introduces a constant drag on the kernel sourcecode, while 99% of development will not want to trace, ever. When I do need tracing occasionally, then I take those 30 minutes to write up a tracer from pre-existing tracing patches, tailored to specific problems. ... So use the power of the GPL-ed kernel and keep your patches separate, releasing them for specific stable kernel ranches (or even development kernels).



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`。

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```  
if (condVar > someVal) {console.log("xxx")}  
```

[/content]

[content]
[Linus Torvalds](http://seclists.org/lists/linux-kernel/2002/Sep/5140.html) 提出了以下观点：

> 总结：你认为追踪很有用，但在你所工作的领域，软件追踪仅具有有限的价值。那么其他那些只想开发一个简单驱动程序、而不必理解整个内核的开发者呢？在`printk()`或`kgdb`无法工作的地方，追踪仍然有效。我认为要求用户启用追踪并重现你无法自行重现的问题是合理的。

这就可以成为增加源码冗余的理由吗？我曾用`dprintk()`风格的追踪调试过一些驱动程序，即使最终编译时会被排除，它常常使得代码更难理解。

从我看到的LTT相关情况来看，它过于重量级，不适合许多用途（为追踪事件获取SMP全局锁并不是一个好主意，如果该追踪是为了进行性能追踪，那么一个增加同步的追踪器从根本上会改变正在发生的事情，而这些改变与时序无关）。

我怀疑我们最终会需要某种形式的事件追踪，但我个人非常确信它需要是每CPU（per-CPU）的，并且核心机制必须非常轻量。在轻量级接口之上构建复杂性，要比从重量级接口中提炼出轻量级接口容易得多。

[分类](http://eLinux.org/Special:Categories "Special:Categories")：

*   [启动时间](http://eLinux.org/Category:Boot_Time "Category:Boot_Time")
*   [追踪](http://eLinux.org/index.php?title=Category:Tracing&action=edit&redlink=1 "Category:Tracing (page does not exist)")
*   [内核](http://eLinux.org/Category:Kernel "Category:Kernel")

# LTTng

> 来源：[eLinux.org](http://eLinux.org/LTTng "http://eLinux.org/LTTng")

# LTTng

Linux Trace Toolkit Viewer/Next Generation（Linux追踪工具包查看器/下一代）。

LTTV是一个模块化的查看器/分析工具，专门设计用于处理生产系统生成的海量追踪数据。

它附带了一个Linux内核追踪器，名为Linux Trace Toolkit Next Generation（LTTng），它构建在现有的LTT追踪点和`RelayFS`传递机制之上，但却是对LTT追踪模块和守护进程的完全重写。

其设计旨在促进社区贡献。我们知道，可以对追踪数据执行的海量分析几乎是无限的，因此我们希望尽可能简单有趣地将这些分析添加到项目中。

你可以从[`www.lttng.org`](http://www.lttng.org)获取它。按照快速入门指南了解如何从Debian软件包、RPM或源码中获取它。

LTTV的主要特性：

*   支持大型追踪（已用15GB的追踪文件测试）。它从一开始就被设计用于处理海量追踪数据。
*   可以动态地将来自多个追踪文件的信息合并到一个视图中。
*   处理来自任何架构（大小端）的追踪数据。
*   支持插件的文本命令行接口，用于批量追踪分析。
*   支持可视化插件的图形界面。
*   灵活的事件过滤器。
*   模块化架构：

```
- 动态加载的插件：每个特定的视图/分析成为一个插件。
- 模块依赖架构，用于最大化功能重用和更容易测试。
```

*   通过事件描述解析器和追踪代码生成器（`genevent`），添加新插桩（或任何类型的追踪点）变得更加容易。

你也可以从[`www.lttng.org`](http://www.lttng.org)获取LTTng。提供Debian、RPM和源码包。参见快速入门指南。

LTTng的主要特性：

*   通过支持`genevent`代码生成器，轻松添加新的插桩。
*   通过使用处理器周期计数器作为唯一的单调时间参考，提供非常精确的事件时间戳。
*   对追踪系统影响最小：插桩不会禁用中断或加锁。它改用`RCU`和`cmpxchg`原子操作。
*   非可屏蔽中断（NMI）重入支持。
*   支持多种可嵌套类型：结构体、联合体、数组、序列。
*   支持主机相关类型。
*   以低开销动态对齐追踪数据。
*   与LTTV查看器集成，可以直接从图形界面控制追踪。
*   可以同时记录多个（n个）独立追踪。
*   模块化架构。

[`lwn.net/Articles/166952/`](http://lwn.net/Articles/166952/)

## 外部链接

*   [lwn.net: LTTng 2.0: 面向高级用户和开发者的追踪技术 - 第1部分](http://lwn.net/Articles/491510/)
*   [lwn.net: LTTng 2.0: 面向高级用户和开发者的追踪技术 - 第2部分](http://lwn.net/Articles/492296/)

[分类](http://eLinux.org/Special:Categories "Special:Categories")：

*   [Linux](http://eLinux.org/Category:Linux "Category:Linux")

# Ftrace

> 来源：[eLinux.org](http://eLinux.org/Ftrace "http://eLinux.org/Ftrace")

# Ftrace

Ftrace是Linux内核的内部追踪器，自Linux 2.6.27版本起被包含在内。尽管Ftrace以函数追踪器命名，但它还包含更多功能。不过函数追踪器是Ftrace中使其独一无二的部分，因为你可以追踪内核中几乎任何函数，并且借助动态Ftrace，在未启用时没有任何开销。

Ftrace的接口位于`debugfs`文件系统的`tracing`目录中。相关文档可以在Linux内核源码树中的[Documentation/trace/ftrace.txt](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux-2.6.git;a=blob;f=Documentation/trace/ftrace.txt;)找到。

## 目录

*   1 trace-cmd
*   2 技巧
    *   2.1 使用Ftrace接口追踪特定进程
    *   2.2 使用trace-cmd追踪特定进程
    *   2.3 捕获（启动时的）oops到串行控制台
    *   2.4 查找内核启动时的延迟
    *   2.5 查找最深的内核栈
    *   2.6 附加资源
    *   2.7 pytimechart
    *   2.8 使用ftrace和pytimechart实现类似bootchart的追踪
    *   2.9 输出

## trace-cmd

使用Ftrace的`debugfs`接口可能既笨拙又耗时。创建`trace-cmd`是为了通过一个带有完整man手册文档的二进制工具来与Ftrace交互。

以下是`trace-cmd`的一些示例：

```  
# trace-cmd record -e sched myprogram  
```

上述命令将启用所有在`sched`系统下分组的Ftrace追踪点。你可以通过查看`debugfs`系统找到这些追踪点：

```  
# mount -t debugfs nodev /sys/kernel/debug  
# ls /sys/kernel/debug/tracing/events/sched  
enable                  sched_process_fork  sched_stat_sleep  
filter                  sched_process_free  sched_stat_wait  
sched_kthread_stop      sched_process_wait  sched_switch  
sched_kthread_stop_ret  sched_signal_send   sched_wait_task  
sched_migrate_task      sched_stat_iowait   sched_wakeup  
sched_process_exit      sched_stat_runtime  sched_wakeup_new  
```

`trace-cmd`还允许你无需查看此目录即可看到可能的事件。

```  
# trace-cmd list -e | grep sched:  
sched:sched_kthread_stop  
sched:sched_kthread_stop_ret  
sched:sched_wait_task  
sched:sched_wakeup  
sched:sched_wakeup_new  
sched:sched_switch  
sched:sched_migrate_task  
sched:sched_process_free  
sched:sched_process_exit  
sched:sched_process_wait  
sched:sched_process_fork  
sched:sched_signal_send  
sched:sched_stat_wait  
sched:sched_stat_runtime  
sched:sched_stat_sleep  
sched:sched_stat_iowait  
```

你可以在其[git](http://git.kernel.org/?p=linux/kernel/git/rostedt/trace-cmd.git;a=summary)仓库中找到`trace-cmd`。

同一仓库中还包含`KernelShark`，它是`trace-cmd`的图形用户界面。`trace-cmd`只需使用“make”即可构建，而`KernelShark`则使用“make gui”创建。这使得您可以在嵌入式设备上构建`trace-cmd`，而无需构建`KernelShark`所需的GTK库。

## 技巧

### 使用Ftrace接口追踪特定进程



（改编自 Steven Rostedt 的电子邮件）

要跟踪特定函数上下文中执行的内核函数，只需将伪变量`set-ftrace-pid`设置为该进程的进程 ID（pid）。

如果该进程尚未运行，可以使用包装 shell 脚本和`exec`命令，以已知的 pid 执行命令。

示例如下：

```sh
#!/bin/sh
echo $$ > /debug/tracing/set_ftrace_pid
# can set other filtering here
echo function > /debug/tracing/current_tracer
exec $*
```

在此示例中，`$$`是当前正在执行的进程的 pid（即 shell 脚本的 pid）。该值会被设置到`set_ftrace_pid`变量中，然后启用`function`跟踪器。随后，此脚本会执行命令（由脚本的第一个参数指定）。

示例用法（假设脚本名为`trace_command`）：

```sh
trace_command ls
```

### 使用`trace-cmd`跟踪特定进程

```sh
# trace-cmd record -p function -F ls
```

### 捕获 oops（从启动开始）到串行控制台

可以通过在内核命令行中添加以下内容，捕获导致 panic 的函数调用：

```text
ftrace=function ftrace_dump_on_oops
```

注意：如果更倾向于使用函数图，也可以使用`ftrace=function_graph`。

`Documentation/trace/ftrace.txt`中的 ftrace 文档介绍了如何在运行中的系统中设置`ftrace_dump_on_oops`。但我发现，让系统从内核启动时就配置为转储跟踪信息非常方便，这样在启动期间、用户空间启动之前发生的任何 panic 也都能被捕获。

请注意，输出内容会非常长，请耐心等待。

输出结果大致如下：



```
 ash-56      0d..2\. 159400967us : _raw_spin_lock <-vprintk
     ash-56      0d..2\. 159400972us : __raw_spin_lock <-_raw_spin_lock
     ash-56      0d..2\. 159400974us : add_preempt_count <-__raw_spin_lock
     ash-56      0d..3\. 159400978us : log_prefix <-vprintk
     ash-56      0d..3\. 159400979us : emit_log_char <-vprintk
     ash-56      0d..3\. 159400981us : console_trylock <-vprintk
     ash-56      0d..3\. 159400983us : down_trylock <-console_trylock
     ash-56      0d..3\. 159400985us : _raw_spin_lock_irqsave <-down_trylock
     ash-56      0d..3\. 159400987us : __raw_spin_lock_irqsave <-_raw_spin_lock_irqsave
     ash-56      0d..3\. 159400989us : add_preempt_count <-__raw_spin_lock_irqsave
     ash-56      0d..4\. 159400991us : _raw_spin_unlock_irqrestore <-down_trylock
     ash-56      0d..4\. 159400993us : sub_preempt_count <-_raw_spin_unlock_irqrestore
     ash-56      0d..3\. 159400994us : _raw_spin_unlock <-vprintk
     ash-56      0d..3\. 159400997us : sub_preempt_count <-_raw_spin_unlock
     ash-56      0d..2\. 159400999us : console_unlock <-vprintk
     ash-56      0d..2\. 159401000us : _raw_spin_lock_irqsave <-console_unlock
     ash-56      0d..2\. 159401002us : __raw_spin_lock_irqsave <-_raw_spin_lock_irqsave
     ash-56      0d..2\. 159401004us : add_preempt_count <-__raw_spin_lock_irqsave
     ash-56      0d..3\. 159401006us : _raw_spin_unlock <-console_unlock
     ash-56      0d..3\. 159401008us : sub_preempt_count <-_raw_spin_unlock
     ash-56      0d..2\. 159401010us : _call_console_drivers <-console_unlock
     ash-56      0d..2\. 159401012us : _call_console_drivers <-console_unlock
     ash-56      0d..2\. 159401014us : _raw_spin_lock_irqsave <-console_unlock
     ash-56      0d..2\. 159401015us : __raw_spin_lock_irqsave <-_raw_spin_lock_irqsave
     ash-56      0d..2\. 159401017us : add_preempt_count <-__raw_spin_lock_irqsave
     ash-56      0d..3\. 159401019us : up <-console_unlock
     ash-56      0d..3\. 159401021us : _raw_spin_lock_irqsave <-up
     ash-56      0d..3\. 159401023us : __raw_spin_lock_irqsave <-_raw_spin_lock_irqsave
     ash-56      0d..3\. 159401024us : add_preempt_count <-__raw_spin_lock_irqsave
     ash-56      0d..4\. 159401027us : _raw_spin_unlock_irqrestore <-up
     ash-56      0d..4\. 159401029us : sub_preempt_count <-_raw_spin_unlock_irqrestore
     ash-56      0d..3\. 159401031us : _raw_spin_unlock_irqrestore <-console_unlock
     ash-56      0d..3\. 159401033us : sub_preempt_count <-_raw_spin_unlock_irqrestore
     ash-56      0d..2\. 159401034us : wake_up_klogd <-console_unlock
     ash-56      0d..2\. 159401037us : sub_preempt_count <-vprintk
     ash-56      0d..1\. 159401039us : die <-__do_kernel_fault
     ash-56      0d..1\. 159401041us : oops_enter <-die
---------------------------------
Modules linked in:
CPU: 0    Not tainted  (3.0.27_nl-kzm-a9-rt46-00022-g5e35327 #2)
PC is at sysrq_handle_crash+0x40/0x50
LR is at _raw_spin_unlock_irqrestore+0x34/0x54
pc : [<801b7dd4>]    lr : [<802f5420>]    psr: 60000093
sp : 9f0cdeb0  ip : 802f7ed4  fp : 9f0cdebc
r10: 9f0cdf68  r9 : 9fbaedc8  r8 : 00000000
r7 : 60000013  r6 : 00000063  r5 : 00000001  r4 : 8044b890
r3 : 00000000  r2 : 00000001  r1 : 20000093  r0 : 00000001
Flags: nZCv  IRQs off  FIQs on  Mode SVC_32  ISA ARM  Segment user
Control: 10c5787d  Table: 5f11c04a  DAC: 00000015
Process ash (pid: 56, stack limit = 0x9f0cc2f0)
Stack: (0x9f0cdeb0 to 0x9f0ce000)
dea0:                                     9f0cdee4 9f0cdec0 801b85d0 801b7da0
dec0: 9f0cdf68 00000002 801b867c 9f07a960 00000002 2ad20000 9f0cdefc 9f0cdee8
dee0: 801b86b0 801b852c 9f0cdf68 9fbaed80 9f0cdf2c 9f0cdf00 80108a84 801b8688
df00: 9f0cdf68 00000002 9f07a960 2ad20000 9f0cdf68 2ad20000 00000001 00000000
df20: 9f0cdf5c 9f0cdf30 800c2f14 80108a00 00000002 00000889 800c4978 00000002
df40: 9f07a960 0005a750 00000002 2ad20000 9f0cdfa4 9f0cdf60 800c3250 800c2e5c
df60: 00020001 0004423c 00000000 00000000 9f0cc000 00000000 9f0cdfa4 00000002
df80: 2ad20000 0005a750 00000004 8000db24 9f0cc000 00000000 00000000 9f0cdfa8
dfa0: 8000d8c0 800c3208 00000002 2ad20000 00000001 2ad20000 00000002 00000889
dfc0: 00000002 2ad20000 0005a750 00000004 00000001 00000000 2ad093b8 7e8766d4
dfe0: 00000000 7e8766c0 2ac20f08 2ac023ec 40000010 00000001 00000000 00000000
Backtrace:
[<801b7d94>] (sysrq_handle_crash+0x0/0x50) from [<801b85d0>] (__handle_sysrq+0xb0/0x15c)
[<801b8520>] (__handle_sysrq+0x0/0x15c) from [<801b86b0>] (write_sysrq_trigger+0x34/0x44)
 r8:2ad20000 r7:00000002 r6:9f07a960 r5:801b867c r4:00000002
r3:9f0cdf68
[<801b867c>] (write_sysrq_trigger+0x0/0x44) from [<80108a84>] (proc_reg_write+0x90/0xa4)
 r4:9fbaed80 r3:9f0cdf68
[<801089f4>] (proc_reg_write+0x0/0xa4) from [<800c2f14>] (vfs_write+0xc4/0x150)
[<800c2e50>] (vfs_write+0x0/0x150) from [<800c3250>] (sys_write+0x54/0x110)
 r8:2ad20000 r7:00000002 r6:0005a750 r5:9f07a960 r4:00000002
[<800c31fc>] (sys_write+0x0/0x110) from [<8000d8c0>] (ret_fast_syscall+0x0/0x30)
Code: 0a000000 e12fff33 e3a03000 e3a02001 (e5c32000)
---[ end trace feb441c6e3b9c3f1 ]---
Kernel panic - not syncing: Fatal exception
Backtrace:
[<80011908>] (dump_backtrace+0x0/0x114) from [<802f2304>] (dump_stack+0x20/0x24)
 r6:9f0cdd1c r5:8039bb64 r4:8045dc40 r3:00000002
[<802f22e4>] (dump_stack+0x0/0x24) from [<802f2404>] (panic+0xfc/0x220)
[<802f2308>] (panic+0x0/0x220) from [<80011dd4>] (die+0x18c/0x1d0)
 r3:00000001 r2:9f0cdd28 r1:20000113 r0:8039bb64
 r7:00000001
[<80011c48>] (die+0x0/0x1d0) from [<80014edc>] (__do_kernel_fault+0x74/0x94)
 r8:00000000 r7:9f0cde68 r6:9f0c1d40 r5:00000817 r4:00000000
[<80014e68>] (__do_kernel_fault+0x0/0x94) from [<802f7ca0>] (do_page_fault+0x254/0x274)
 r8:00000817 r7:9f0c1d40 r6:9f06d5e0 r5:00000000 r4:9f0cde68
r3:9f0cde68
[<802f7a4c>] (do_page_fault+0x0/0x274) from [<802f7db0>] (do_DataAbort+0x40/0xa8)
[<802f7d70>] (do_DataAbort+0x0/0xa8) from [<802f5d98>] (__dabt_svc+0x38/0x60)
 r8:00000000 r7:9f0cde9c r6:ffffffff r5:60000093 r4:801b7dd4
[<801b7d94>] (sysrq_handle_crash+0x0/0x50) from [<801b85d0>] (__handle_sysrq+0xb0/0x15c)
[<801b8520>] (__handle_sysrq+0x0/0x15c) from [<801b86b0>] (write_sysrq_trigger+0x34/0x44)
 r8:2ad20000 r7:00000002 r6:9f07a960 r5:801b867c r4:00000002
r3:9f0cdf68
[<801b867c>] (write_sysrq_trigger+0x0/0x44) from [<80108a84>] (proc_reg_write+0x90/0xa4)
 r4:9fbaed80 r3:9f0cdf68
[<801089f4>] (proc_reg_write+0x0/0xa4) from [<800c2f14>] (vfs_write+0xc4/0x150)
[<800c2e50>] (vfs_write+0x0/0x150) from [<800c3250>] (sys_write+0x54/0x110)
 r8:2ad20000 r7:00000002 r6:0005a750 r5:9f07a960 r4:00000002
[<800c31fc>] (sys_write+0x0/0x110) from [<8000d8c0>] (ret_fast_syscall+0x0/0x30)
CPU1: stopping
Backtrace:
[<80011908>] (dump_backtrace+0x0/0x114) from [<802f2304>] (dump_stack+0x20/0x24)
 r6:00000006 r5:00000001 r4:00000000 r3:00000000
[<802f22e4>] (dump_stack+0x0/0x24) from [<80008308>] (do_IPI+0xd8/0x148)
[<80008230>] (do_IPI+0x0/0x148) from [<802f5df4>] (__irq_svc+0x34/0xd0)
Exception stack(0x9fb47f68 to 0x9fb47fb0)
7f60:                   00000000 00000000 f300a000 00000000 9fb46000 80432444
7f80: 8045d464 802fd754 4000406a 411fc092 00000000 9fb47fbc 8000e660 9fb47fb0
7fa0: 8000e67c 8000e680 60000013 ffffffff
 r7:9fb47f9c r6:f0020000 r5:60000013 r4:8000e680
[<8000e64c>] (default_idle+0x0/0x38) from [<8000e920>] (cpu_idle+0x88/0xcc)
[<8000e898>] (cpu_idle+0x0/0xcc) from [<802f0130>] (secondary_start_kernel+0x140/0x164)
 r7:8045d57c r6:10c0387d r5:8043a2f8 r4:00000001
[<802efff0>] (secondary_start_kernel+0x0/0x164) from [<402efab4>] (0x402efab4)
 r5:00000015 r4:5fb4806a 
```

### Find latencies on kernel startup

It is possible to use `ftrace` to record functions that exceed a certain amount of time, using the `tracing_thresh` option. This can be used for finding routines that are taking a long time on kernel startup, to help optimize bootup time:

- Make sure the following kerne configuration options are set:
  - `CONFIG_FTRACE`: "Tracers"
  - `CONFIG_FUNCTION_TRACER`: "Kernel Function Tracer"



# Using Kernel Function Trace

> From: [eLinux.org](http://eLinux.org/Using_Kernel_Function_Trace "http://eLinux.org/Using_Kernel_Function_Trace")

Using Kernel Function Trace Ver. 0.1.1 -- 2007-04-26 Most material provided by Sony

* * *

## Contents

*   1 Introduction
*   2 Quick Overview
*   3 Detailed instructions
    *   3.1 Configuring the kernel for using KFT
    *   3.2 Editing the static trace run configuration (optional)
    *   3.3 Compiling the kernel
    *   3.4 Configuring the trace run
        *   3.4.1 Triggers
        *   3.4.2 Filters
        *   3.4.3 Configuration scenarios
        *   3.4.4 Handling a link error
*   4 Initiating a KFT run
*   5 Reading the trace data
*   6 Processing the data
    *   6.1 Analyzing the data with `kd`
    *   6.2 KFT utilities
*   7 Tips for using KFT
*   8 Online Resources
*   9 Appendices
    *   9.1 Appendix A - KFT configuration language
        *   9.1.1 A note on function names
        *   9.1.2 configuration block
        *   9.1.3 triggers
        *   9.1.4 filters
        *   9.1.5 watches
        *   9.1.6 miscellaneous
        *   9.1.7 Configuration Samples
    *   9.2 Appendix B - Sample results
        *   9.2.1 `kft` log output (excerpt)
        *   9.2.2 `kft` log analysis with `kd`
        *   9.2.3 `kft` nested call trace with `kd -c`
    *   9.3 Appendix C - Using KFT for monitoring stack usage
    *   9.4 Appendix D - Some notes on KFT operation
        *   9.4.1 Trace overhead
            *   9.4.1.1 Overhead measurement
        *   9.4.2 Trace buffer exhaustion
        *   9.4.3 Early clock issues
            *   9.4.3.1 Adding platform support for the KFT clock source
*   10 Modification History

## Introduction

This document describes how to use Kernel Function Trace with the Linux kernel. It assumes you have already applied the KFT patch to your kernel, or that it was otherwise previously integrated with your kernel source code.

Kernel Function Trace (KFT) is a kernel function tracing system, which examines every function entry and exit in the Linux kernel. The KFT system provides for capturing a subset of these events along with timing and other details. KFT is different from other kernel tracing systems in that it is designed to be able to filter the events by the duration of the function calls. Thus, KFT is good for finding out where time is spent in functions and sub-routines in the kernel. When used in unfiltered mode, KFT is very useful to collect information about the flow of control in the kernel, which can help with debugging or optimizing kernel code.

The main mode of operation with KFT is by running a "dynamic" trace. That is, you start the kernel as usual, then, using the `/proc/kft` interface, configure a trace, start it, and retrieve the trace data immediately.

## Quick Overview

*   Kernel configuration options:
    *   `CONFIG_FUNCTION_GRAPH_TRACER`: "Kernel Function Graph Tracer"

*   Use the following on the kernel command line:
    *   `tracing_thresh=200 ftrace=function_graph`
        *   This traces all functions taking longer than 200 microseconds (.2 ms). You can use any duration threshold you want.

*   To get the data:
    *   `$ mount -t debugfs debugfs /debug`
    *   `$ cat /debug/tracing/trace`

These commands should probably be done programmatically (as part of an init script), to avoid data loss.

*   Scope of operation:
    *   The tracer starts sometime during initialization, and you only get timings after it starts.

### Find Deepest Kernel Stack

This is useful to find the routine with the deepest kernel stack. The system continually monitors the stack depth of all processes, and whenever a low-water mark is hit (deepest stack), it records the list of functions.

(The following instructions work for a v3.0 Linux kernel)

*   Kernel configuration: Set the following kernel configuration options:
    *   `CONFIG_FTRACE`: "Tracers"
    *   `CONFIG_FUNCTION_TRACER`: "Kernel Function Tracer"
    *   `CONFIG_STACK_TRACER`: "Trace max stack"

*   Turning it on: You can turn it on at boot time or at runtime.
    *   At boot time, use the following on the kernel command line:
        *   `stacktrace`
    *   Or, at runtime do:
        *   `echo 1 >/proc/sys/kernel/stack_tracer_enabled`

*   To get the data:
    *   `$ mount -t debugfs debugfs /debug`
    *   `$ cat /debug/tracing/stack_trace`

*   Scope of operation:
    *   The stack tracer will continue operating until you turn it off, which can be done with:
        *   `echo 0 >/proc/sys/kernel/stack_tracer_enabled`

### Additional Resources

See [`lwn.net/Articles/295955/`](http://lwn.net/Articles/295955/)

### pytimechart

You can use `pytimechart` to explore ftrace traces visually. See [`packages.python.org/pytimechart/userguide.html`](http://packages.python.org/pytimechart/userguide.html)

### Bootchart Like Traces with ftrace and pytimechart

You can use the following kernel command line parameters to generate a trace at boot, which can then be opened with `pytimechart` to have a browsable bootchart.

```
trace_event=sched:*,timer:*,irq:* trace_buf_size=40M
```

### Output

Here is what the output looks like, on ARM:

```
/debug/tracing # cat stack_trace
        Depth    Size   Location    (42 entries)
        -----    ----   --------
  0)     3328      16   ftrace_test_stop_func+0x28/0x34
  1)     3312      28   __gnu_mcount_nc+0x58/0x60
  2)     3284      52   skb_release_data+0xc0/0xc8
  3)     3232      24   __kfree_skb+0x24/0xc0
  4)     3208      32   consume_skb+0xe4/0xf0
  5)     3176      56   smsc911x_hard_start_xmit+0x188/0x2f4
  6)     3120      72   dev_hard_start_xmit+0x440/0x6a4
  7)     3048      40   sch_direct_xmit+0x8c/0x1f8
  8)     3008      48   dev_queue_xmit+0x2c8/0x570
  9)     2960      56   neigh_resolve_output+0x32c/0x390
 10)     2904      40   ip_finish_output+0x2bc/0x37c
 11)     2864      32   ip_output+0xb0/0xb8
 12)     2832      24   ip_local_out+0x38/0x3c
 13)     2808      32   ip_send_skb+0x18/0xa4
 14)     2776      56   udp_send_skb+0x274/0x394
 15)     2720     240   udp_sendmsg+0x4dc/0x748
 16)     2480      32   inet_sendmsg+0x70/0x7c
 17)     2448     232   sock_sendmsg+0xa8/0x160
 18)     2216      32   kernel_sendmsg+0x40/0x48
 19)     2184      96   xs_send_kvec+0xa8/0xb0
 20)     2088      64   xs_sendpages+0x90/0x1f8
 21)     2024      40   xs_udp_send_request+0x4c/0x13c
 22)     1984      48   xprt_transmit+0x114/0x214
 23)     1936      40   call_transmit+0x208/0x27c
 24)     1896      48   __rpc_execute+0x88/0x334
 25)     1848      24   rpc_execute+0x68/0x70
 26)     1824      24   rpc_run_task+0xa8/0xb4
 27)     1800      64   rpc_call_sync+0x68/0x90
 28)     1736      32   nfs_rpc_wrapper.clone.6+0x3c/0x7c
 29)     1704      48   nfs_proc_getattr+0x70/0xac
 30)     1656      48   __nfs_revalidate_inode+0xe4/0x1f8
 31)     1608      56   nfs_lookup_revalidate+0x1ac/0x40c
 32)     1552      72   do_lookup+0x228/0x2e4
 33)     1480      72   do_last.clone.44+0x10c/0x688
 34)     1408      88   path_openat+0x2fc/0x394
 35)     1320     144   do_filp_open+0x40/0x8c
 36)     1176      40   open_exec+0x2c/0xc0
 37)     1136     136   load_elf_binary+0x1cc/0x12b8
 38)     1000      72   search_binary_handler+0x150/0x3a0
 39)      928      56   do_execve+0x170/0x328
 40)      872      32   sys_execve+0x44/0x64
 41)      840     840   ret_fast_syscall+0x0/0x30
```

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

*   [Linux tracing](http://eLinux.org/Category:Linux_tracing "Category:Linux_tracing")



然而，另一种特殊的操作模式可用于执行启动时追踪。在这种模式下，追踪配置被静态编译进内核，这有时被称为“静态”模式。此模式对于在系统启动期间（用户空间运行之前，且任何可用于配置和启动追踪的服务尚未就绪时）获取内核追踪非常有用。该模式对于发现内核启动时间相关的问题尤其有帮助。

无论哪种情况，您都需要为追踪运行指定一个KFT配置。该配置指定如何自动启动和停止追踪，是否将中断纳入追踪范围，以及是否根据各种标准（如最小函数持续时间、仅限特定函数列表等）过滤事件数据。

当追踪完成时，通过读取`/proc/kft_data`来检索追踪期间收集的事件数据。

最后，KFT提供了处理和解析KFT追踪数据的工具。

## 快速概览

在动态模式下使用KFT的快速概览：

*   配置内核以支持KFT
*   编译内核
*   启动内核
*   将配置写入`/proc/kft`
*   启动追踪
*   从`/proc/kft_data`读取追踪数据
*   处理数据
    *   使用`addr2sym`将地址转换为函数名
    *   使用`kd`解析追踪数据

* * *

在启动时使用KFT的快速概览：

*   配置内核以支持KFT和`KFT_STATIC_RUN`
*   编辑`<linux_src>/kernel/kftstatic.conf`中的配置
*   编译内核
*   启动内核
    *   运行应在启动期间触发
*   从`/proc/kft_data`读取追踪数据
*   处理数据
    *   使用`addr2sym`将地址转换为函数名
    *   使用`kd`解析追踪数据

## 详细说明

### 配置内核以使用KFT

通过编辑内核配置文件（`.config`）来配置内核以支持KFT。

例如，如果您使用`make menuconfig`，请在“内核调试”菜单下设置以下选项。

```
Kernel Hacking --->
[*] Kernel Function Trace 
```

保存此配置。这将在内核`.config`文件中设置`CONFIG_KFT=y`选项。

* * *

如果您希望在启动时执行追踪，还需配置KFT静态模式。

例如，如果您使用`make menuconfig`，请在“内核调试”菜单下设置以下选项。

```
Kernel Hacking --->
[*] Kernel Function Trace
[*] Static function tracing configuration 
```

保存此配置。这将在内核`.config`文件中设置以下选项：

```
CONFIG_KFT=y
CONFIG_KFT_STATIC_RUN=y 
```

### 编辑静态追踪运行配置（可选）

如果您正在执行“静态”追踪，请编辑`kernel/kftstatic.conf`文件，以设置您希望在系统启动时执行的追踪运行配置。（有关追踪配置语法和选项的详细信息，请参见下一节“配置追踪运行”。）请注意，即使您执行启动时间追踪，您仍可在系统运行期间随时执行动态追踪。

### 编译内核

构建内核，并将其安装到目标机器上以便启动。

请务必保存此构建产生的`System.map`文件，因为在处理追踪数据时需要用到它。

如果在编译内核时遇到错误，请参阅下一节关于配置问题故障排除的内容。

### 配置追踪运行

要配置您的追踪，您需要编写一个追踪配置文件。该文件指定何时启动和停止追踪，以及将哪些事件保存为追踪数据的一部分。

以下是一个示例配置文件，常用于启动期间：

```
begin
  trigger start entry start_kernel
  trigger stop entry to_userspace
  filter mintime 500
end 
```

此追踪配置表示：

*   当进入`start_kernel`函数时开始追踪
*   当进入`to_userspace`函数时停止追踪
*   不保存执行时间少于500微秒的任何函数的事件

`start_kernel`函数是内核启动时执行的第一个C函数。`to_userspace`函数是在执行权转移到第一个用户空间程序（通常是`/sbin/init`）之前立即调用的函数。此追踪配置意味着在内核开始执行时立即开始追踪，并在第一个用户空间程序运行前立即停止追踪。它只会在追踪缓冲区中保存执行时间超过500微秒的函数记录。

#### 触发器

配置中的触发器用于启动和停止追踪系统的数据收集。触发器可以基于函数进入或退出事件，也可以基于时间流逝。停止触发器用于控制收集的数据量。如果缓冲区没有足够空间容纳追踪数据，追踪将自动停止。

时间值以十进制微秒表示。开始时间相对于系统启动，或相对于用于追踪的时钟初始化时间（通常是内核内部函数` sched_clock()`使用的时钟）。停止时间相对于开始时间。

以下是一些示例：

*   语句：`trigger start entry start_kernel`
    *   含义：当内核进入`start_kernel`函数时开始追踪
*   语句：`trigger stop exit do_fork`
    *   含义：当内核退出`do_fork`函数时停止追踪
*   语句：`trigger start time 10000000`
    *   含义：启动后10,000,000微秒（10秒）开始追踪
*   语句：`trigger stop time 5000`
    *   含义：追踪开始后5,000微秒（5毫秒）停止追踪

#### 过滤器

过滤器控制追踪期间收集的数据。由于每个内核函数进入和退出都是追踪事件记录的候选对象，KFT可能产生大量数据。为控制记录的数据量，通常设置追踪期间使用的过滤器。

您可以按函数持续时间、中断上下文过滤，或将追踪限制在特定函数。过滤器语句中的时间以微秒表示。静态配置中，过滤器函数列表中的函数可通过名称表示，但动态配置中必须通过地址表示。

以下是一些示例：

*   语句：`filter mintime 100`
    *   含义：仅在追踪中保留持续至少100微秒的函数
*   语句：`filter maxtime 5000000`
    *   含义：剔除追踪中持续超过5,000,000微秒（5秒）的函数
*   语句：`filter noints`
    *   含义：剔除处理器处于中断上下文时执行的函数
*   语句：`filter onlyints`
    *   含义：仅保留处理器处于中断上下文时执行的函数
*   语句：`filter funclist do_fork sys_read fend`
    *   含义：仅保留`do_fork`和`sys_read`函数的事件

#### 配置场景

有关可在追踪配置中包含的其他命令，请参见附录A。

#### 处理链接错误

如果您在`kftstatic.conf`中引用了某些在全局范围内不可见的函数，则在链接内核时可能会出现错误。如果您看到类似“undefined reference to `foo_func`”的链接器错误，则可以通过使`foo_func`可见来解决此问题。通常，这意味着找到`foo_func`的声明，并将其声明中的`static`关键字移除。

## 启动KFT运行

如果您以静态模式运行，在启动内核时，应根据`kernel/kftstatic.conf`中的触发器和过滤器设置自动启动并运行追踪。

如果您以动态模式运行，则通过将KFT配置写入`/proc/kft`，然后进行“预加载”来启动运行。



Traces go through a state machine (a series of event transitions) in order to actually start collecting data. This is to allow trace collection to be separated from trace setup and preparation. The trace configuration specifies a start trigger, which will initiate the collection of data. When the configuration is written to `/proc/kft`, it is not ready to run yet. Making the trace ready to run is called "priming" it.

Therefore, the normal sequence of events for a trace run is:

1. The user writes the configuration file, usually using an editor and creating the file in the local filesystem. Helper scripts can be used to auto-generate simple configurations for common tasks.
   - There is a helper script `scripts/sym2addr`, which converts function names in the configuration file to addresses. This can be copied to the target, along with the current `System.map` file, to make preparing the configuration file easier.

2. The user writes the configuration to KFT (via `/proc/kft`)
   - e.g. `cat /tmp/trace.config >/proc/kft`

3. If needed, the user prepares for trace by setting up programs to run.

4. The user primes the trace
   - e.g. `echo "prime" >/proc/kft`

5. A kernel event occurs which starts the trace (the start trigger fires)

6. Trace data is collected

7. A kernel event or buffer exhaustion stops the trace (that is, the stop trigger fires, or the buffer runs out)

It is possible to force the start or end of a trace using the `/proc/kft` interface. This overrides steps 5 or 7, which are normally performed by triggers in the trace configuration.

- To manually start a trace: `echo "start" >/proc/kft`
- To manually stop a trace: `echo "stop" >/proc/kft`

You can get the status of the current trace by reading `/proc/kft`.

To see the status of the currently configured trace:

- `cat /proc/kft`

## Reading the trace data

When the trace is running, the trace data is accumulated in a buffer inside the kernel. Once the trace data is collected, you can retrieve if from the kernel by copying the data from `/proc/kft_data`. Usually, you will want to save the data to a file for later analysis.

Here is an example:

- `cat /proc/kft_data >/tmp/kft.log`

## Processing the data

Copy the `kft.log` file from the target to your host development system (on which the kernel source resides), for example, into the `/tmp` directory on your host machine.

The raw `kft.log` file will only have numeric function addresses. To translate these addresses to symbols, use the `addr2sym` program, along with the `System.map` file which was produced when you built the kernel.

Change directory to your kernel source top-level directory and run `scripts/addr2sym` to translate addresses to symbols:

Example:

```
$ scripts/addr2sym /tmp/kft.log -m System.map > /tmp/kft.lst 
```

Here is an example fragment of output from `addr2sym` on a TI OMAP Innovator. Entry and Delta value are times in microseconds. The Entry time is the time time since machine boot, and the Delta time is the time between the function entry and exit.

```
 Entry      Delta      PID            Function                    Called At
--------   --------   -----   -------------------------   --------------------------
   23662       1333       0                    con_init   console_init+0x78
   25375     209045       0             calibrate_delay   start_kernel+0xf0
  234425     106067       0                    mem_init   start_kernel+0x130
  234432     105278       0       free_all_bootmem_node   mem_init+0xc8
  234435     105270       0       free_all_bootmem_core   free_all_bootmem_node+0x28
  340498       4005       0       kmem_cache_sizes_init   start_kernel+0x134 
```

In the above, `calibrate_delay` took about 209 milliseconds.

`mem_init` took 106 msecs, the majority of which (105 msecs) was in `free_all_bootmem_core` (which is called by `free_all_bootmem_node`, which is called by `mem_init`).

If you just look at the function duration, it may appear that lots of time is being spent in certain functions, when in reality those functions are "thin", and the real time-consuming function is one of its children. Thus, rather than look just at the function Delta (or duration), you should look at the function entry times. If there is a big leap in the function entry times, that means a lot of time was consumed in the function right before the leap.

In the example above, there is a leap from 234435 to 340498 (about 100 milliseconds) between the Entry times for `free_all_bootmem_core` and `kmem_cache_sizes_init`. No other functions Entries (lasting more than 500 microseconds, based on the KFT configuration used) were recorded during this time, so this means that this time was spent in `free_all_bootmem_core`.

CPU-yielding functions like `schedule_timeout`, `switch_to`, `kernel_thread`, etc. can have large Delta values due intervening scheduling activity, but these can often be quickly filtered out by following the "leaps in the entry times in the Entry column" above.

### Analyzing the data with kd

You can use the program `kd` to further process the data. It is very helpful at this point to have resolved the names of the functions in the log file, but it is not strictly necessary. The `kd` program function reads a KFT log file and determines the time spent locally in a function versus the time spent in sub-routines. It sorts the functions by the total time spent in the function, and can display various extra pieces of information about each function (number of times called, average call time, etc.)

Also `kd` can be used to re-generate a function call trace from the trace log. This can be very helpful to see the sequence of execution (including interrupts, context switches and returns) of the code that was traced.

Use `./kd -h` for more usage help.

As of this writing, KFT and `kd` do not correctly account for scheduling jumps. The time reported by KFT for function duration is just wall time from entry to exit.

For examples of what `kd` can show, try the following commands on the sample kft output file:

[show all functions sorted by time]

```
$ ./kd kftsample.lst | less 
```

[show only 10 top time-consuming functions]

```
$ ./kd -n 10 kftsample.lst 
```

[show only functions lasting longer than 100 milliseconds]

```
$ ./kd -t 100000 kftsample.lst 
```

[show each function's most time-consuming child, and the number of times it was called. (You may want to make your terminal wider for this output.)]

```
$ ./kd -f Fcatlmn kftsample.lst 
```

[show call traces]

```
$ ./kd -c kftsample.lst 
```

[show call traces with timing data, and functions interlaced]

```
$ ./kd -c -l -i kftsample.lst 
```

Note that the call trace mode may not produce accurate results if weird filtering was used in the trace config (routines that are part of the call tree may be missing, which will confuse `kd`).

### KFT utilities

KFT includes the following helper scripts which are located in the kernel `scripts` directory:

- `mkkftrun.pl` - used during building the kernel to convert a configuration file into a C file to be compiled into the kernel. This is run automatically by the kernel make system. Users of KFT should not need to worry about this.
- `sym2addr` - convert function names to addresses in a KFT configuration file (for a dynamic trace). This is only used if a dynamic configuration has function names.
- `addr2sym` - convert function addresses to symbols in the trace data
- `kd` - KFT dump - does filtering, sorting, analysis and trace formatting of KFT trace logs

The use of most these are described elsewhere in this document. But this list is here for the sake of completeness.

## Tips for using KFT

- How to look for long-duration functions?

```
 (searching child functions for local time) 
```

- How to avoid being fooled by bogus local times
- How to see a detailed function trace (don't use a min-filter)



# 如何解析包含上下文切换的跟踪结果

## 在线资源

这里有一个关于 KFT 用法的演示文稿：（实际上，该演示文稿涉及的是 KFT 的前身 KFI，但所有信息基本相同。）

- [Learning the Kernel and Finding Performance Problems with KFI](http://eLinux.org/images/a/a6/KFI-presentation.ppt "KFI-presentation.ppt") —— Tim Bird 于 2005 年在 CELF [国际技术交流会](http://eLinux.org/International_Technical_Jamboree "International Technical Jamboree") 上的演示文稿
  - [Media:omap-serial_init.trace.txt](http://eLinux.org/images/1/1b/Omap-serial_init.trace.txt "Omap-serial init.trace.txt")
    - 演示文稿中使用的示例跟踪记录

## 附录

### 附录 A - KFT 配置语言

本附录描述用于指定 KFT 跟踪运行的语言。它既用于静态模式（`kftstatic.conf`），也用于动态模式（写入 `/proc/kft`）。

#### 关于函数名的说明

请注意，对于引用函数的参数，可以在 `kftstatic.conf` 中使用函数名（即使用静态配置时）。但是，通过 `/proc/kft` 接口设置配置时，必须使用函数地址。原因在于，内核符号在编译时始终可用，但在运行时可能不可用，具体取决于内核配置。

要将函数名转换为地址，可以在当前内核的 `System.map` 文件中查找该符号的地址。提供了一个名为 `sym2addr` 的辅助程序，可用于将配置文件中的函数名转换为地址。手动操作时，请使用：

例如：`grep do_fork System.map`

```
c001d804 T do_fork
```

在这种情况下，您需要在配置文件中将函数名替换为 `0xc001d804`。（注意开头的 `0x`。）

要使用辅助函数 `sym2addr`，请执行以下操作：

```
sym2addr trace_do_fork.conf System.map >trace_do_fork.conf2
cat trace_do_fork.conf2 >/proc/kft
```

#### 配置块

单次运行的配置位于以 `begin` 开头、以 `end` 结尾的块内。块内包含触发器、过滤器和杂项条目。按照惯例，每个配置条目独占一行。当将配置写入 `/proc/kft` 时，关键字 `new` 应出现在块的 `begin` 关键字之前。

#### 触发器

```
trigger:
         either "start" or "stop", and then one of:
        entry <funcname>
        exit <funcname>
        time <time-in-usecs>
syntax:
trigger start|stop entry|exit|time <arg>
```

开始时间相对于系统启动时间。停止时间相对于跟踪开始时间。

#### 过滤器

```
filters
    maxtime <max-time>
    mintime <min-time>
    noints
    onlyints
    funclist <func1> <func2> fend

syntax:
filter noints|onlyints|maxtime|mintime|funclist <args> fend
```

`funclist` 指定将被跟踪的函数列表。当指定了 `funclist` 时，只跟踪这些函数，而忽略所有其他函数。

通过 `/proc/kft` 指定配置时，必须使用关键字 `fend` 来指示函数列表的结束。当通过 `kftstatic.conf` 指定配置时，不应使用 `fend` 关键字。

#### 监视器

```
watches
    stack <low-water-threshold>
    worst-stack <starting-low-water-threshold>

syntax:
watch stack|worst-stack <threshold>
```

监视器用于让 KFT 监控跟踪记录中的特定条件，并针对该条件采取行动（通常保留额外数据以帮助调试该条件）。目前唯一支持的监视器用于监控栈深度。

对于 `stack` 监视器，在跟踪运行期间，会在每次进入函数时检查栈指针的当前位置。如果栈位置低于指定阈值，则当前函数调用栈会被保留在日志中（无论这些函数是否匹配其他 KFT 过滤条件），并且函数持续时间会被标记为 `-2` 值，以在日志中突出显示。此操作（保存调用栈）在每次栈位置低于阈值时执行。在此模式下，可以在日志中记录任意数量的调用栈（最多不超过日志大小的限制）。

对于 `worst-stack` 监视器，其监控方式与 `stack` 监视器相同。但是，每次满足条件时，阈值（最差剩余栈）会被设置为新的低栈值。在此模式下，每次出现新的低水位条件时都会保留一个调用栈。日志中最后一组此类标记函数将记录跟踪期间所见的消耗栈最多的调用栈。另请注意，最低记录栈位置可在 KFT 状态信息中获取（通过 `/proc/kft`）。

#### 杂项

```
logentries <num-entries>
```

指定此运行日志的最大条目数

```
autorepeat
```

无限重复跟踪。即，在跟踪触发器停止时，重新武装跟踪以再次运行，但保留缓冲区中的数据。当开始触发器匹配时，跟踪将再次开始，当停止触发器匹配时，跟踪将再次停止。当缓冲区变满时，跟踪将停止自动重复。

```
# 未来可能支持的其他选项：
# overwrite
# 覆盖跟踪缓冲区中的旧数据。 这会将跟踪缓冲区转换为循环缓冲区，
# 并且不会在缓冲区变满时停止跟踪。
# 在覆盖模式下，如果缓冲区不足以容纳整个跟踪记录，则可用部分为跟踪记录的结尾。
# 在非覆盖模式（常规模式）下，如果缓冲区不足以容纳整个跟踪记录，则可用部分为跟踪记录的开头。

# untimed
# 不对函数持续时间计时。 通常，日志仅包含函数进入事件，带有开始时间和函数持续时间。
# 在 untimed 模式下，日志包含进入和退出事件，带有每个事件的开始时间。
# 函数持续时间的计算必须由日志后处理工具完成。

# prime
# 立即武装跟踪以待执行。 "武装" (Priming) 跟踪意味着使其准备好运行。
# 未使用 "prime" 命令加载的跟踪将不会启用，直到用户通过 /proc 接口发出单独的 "prime" 命令。

# prime entry ??
# primt exit ??
# prime time ??
```

#### 配置示例

以下是一些配置示例：

记录启动期间所有持续时间超过 500 微秒的函数。不包括在中断中执行的函数。

```
new
begin
  trigger start entry start_kernel
  trigger stop exit to_userspace
  filter mintime 500
  filter maxtime 0
  filter noints
end
```

* * *

在下次 `fork` 后 5 秒内，记录所有持续时间超过 500 微秒的函数，忽略中断。

假设 `do_fork` 位于地址 `0xc001d804`

```
new
begin
  trigger start entry 0xc001d804
  trigger stop time 5000000
  filter mintime 500
  filter maxtime 0
  filter noints
end
```

- 记录由 `do_fork` 调用的短时例程
- 使用较小的日志

```
new
begin
  trigger start entry do_fork
  trigger stop exit do_fork
  filter mintime 10
  filter maxtime 400
  filter noints
  logentries 500
end
```

- 在启动后 5 秒开始，记录 5 毫秒内的中断

```
new
begin
  trigger start time 5000000
  trigger stop time 5000
  filter onlyints
end
```

- 在 10 秒后记录对 `schedule` 的所有调用
- 假设 `schedule` 位于地址

`kftstatic.conf` 版本：

```
begin
  trigger start time 10000000
  filter funclist schedule fend
end
```

`/proc/kft` 版本，假设 `schedule` 位于 `c02cb754`

```
new
begin
  trigger start time 10000000
  filter funclist 0xc02cb754 fend
end
```

### 附录 B - 示例结果

以下是从 KFI 日志跟踪中摘录的内容（已用 `addr2sym` 处理）。它显示了从内核进入 `start_kernel()` 到进入 `to_userspace()` 期间，所有持续时间超过 500 微秒的函数。



#### kft log output (excerpt)

```
Kernel Instrumentation Run ID 0

Logging started at 6785045 usec by entry to function start_kernel
Logging stopped at 8423650 usec by entry to function to_userspace

Filters: 
```

500 usecs minimum execution time

```
Filter Counters:

Execution time filter count = 896348
Total entries filtered = 896348
Entries not found = 24

Number of entries after filters = 1757

 Entry      Delta      PID            Function                    Called At
--------   --------   -----   -------------------------   -------------------------
      1          0       0                start_kernel   L6+0x0
     14       8687       0                  setup_arch   start_kernel+0x35
     39        891       0                setup_memory   setup_arch+0x2a8
     53        872       0   register_bootmem_low_pages   setup_memory+0x8f
     54        871       0                free_bootmem   register_bootmem_low_pages+0x95
     54        871       0           free_bootmem_core   free_bootmem+0x34
    930       7432       0                 paging_init   setup_arch+0x2af
    935       7427       0             zone_sizes_init   paging_init+0x4e
    935       7427       0              free_area_init   zone_sizes_init+0x83
    935       7427       0         free_area_init_node   free_area_init+0x4b
    935       3759       0        __alloc_bootmem_node   free_area_init_node+0xc5
    935       3759       0        __alloc_bootmem_core   __alloc_bootmem_node+0x43
   4694       3668       0         free_area_init_core   free_area_init_node+0x75
   4817       3535       0            memmap_init_zone   free_area_init_core+0x2bd
   8807     266911       0                   time_init   start_kernel+0xb6
   8807     261404       0               get_cmos_time   time_init+0x1c
 270211       5507       0                select_timer   time_init+0x41
 270211       5507       0                    init_tsc   select_timer+0x45
 270211       5507       0               calibrate_tsc   init_tsc+0x6c
 275718       1638       0                console_init   start_kernel+0xbb
 275718       1638       0                    con_init   console_init+0x59
 275954        733       0          vgacon_save_screen   con_init+0x288
 277376       6730       0                    mem_init   start_kernel+0xf8
 277376       1691       0            free_all_bootmem   mem_init+0x52
 277376       1691       0       free_all_bootmem_core   free_all_bootmem+0x24
 284118      25027       0             calibrate_delay   start_kernel+0x10f
 293860        770       0                     __delay   calibrate_delay+0x62
 293860        770       0                   delay_tsc   __delay+0x26
 294951       1534       0                     __delay   calibrate_delay+0x62
 294951       1534       0                   delay_tsc   __delay+0x26
 297134       1149       0                     __delay   calibrate_delay+0xbe
 297134       1149       0                   delay_tsc   __delay+0x26
 .
 .
 .
1638605          0     145              filemap_nopage   do_no_page+0xef
1638605          0     145                 __lock_page   filemap_nopage+0x286
1638605          0     145                 io_schedule   __lock_page+0x95
1638605          0     145                    schedule   io_schedule+0x24
1638605          0       5                    schedule   worker_thread+0x217
1638605          0       1                to_userspace   init+0xa6 
```

The log is attached here: [Media:Kfiboot-9.lst](http://eLinux.org/images/6/68/Kfiboot-9.lst "Kfiboot-9.lst") A `Delta` value of 0 usually means the exit from the routine was not seen.

#### kft log analysis with `kd`

Below is a `kd` dump of the data from the above log.

For the purpose of finding areas of big time in the kernel, the functions with high "Local" time are important. For example, `delay_tsc()` is called 156 times, resulting in 619 milliseconds of duration. Other time-consuming routines were: `isapnp_isolate()`, `get_cmos_time()`, `default_idle()`.

The top line showing `schedule()` called 192 times and lasting over 5 seconds, is accounted wrong due to the switch in execution control inside the `schedule` routine. (The count of 192 calls is correct, but the duration is wrong.)

```
$ ~/work/kft/kft/kd -n 30 kftboot-9.lst
Function                  Count Time     Average  Local
------------------------- ----- -------- -------- --------
schedule                    192  5173790    26946  5173790
do_basic_setup                1  1159270  1159270       14
do_initcalls                  1  1159256  1159256      627
__delay                     156   619322     3970        0
delay_tsc                   156   619322     3970   619322
__const_udelay              146   608427     4167        0
probe_hwif                    8   553972    69246      126
do_probe                     31   553025    17839       68
ide_delay_50ms              103   552588     5364        0
isapnp_init                   1   383138   383138       18
isapnp_isolate                1   383120   383120   311629
ide_init                      1   339778   339778       22
probe_for_hwifs               1   339756   339756      103
ide_scan_pcibus               1   339653   339653       13
init_setup_piix               2   339640   169820        0
ide_scan_pcidev               2   339640   169820        0
piix_init_one                 2   339640   169820        0
ide_setup_pci_device          2   339640   169820      242
probe_hwif_init               4   339398    84849       40
time_init                     1   266911   266911        0
get_cmos_time                 1   261404   261404   261404
ide_generic_init              1   214614   214614        0
ideprobe_init                 1   214614   214614        0
wait_for_completion           6   194573    32428        0
default_idle                183   192589     1052   192589
io_schedule                  18   171313     9517        0
__wait_on_buffer             14   150369    10740      141
i8042_init                    1   137210   137210      295
i8042_port_register           2   135318    67659      301
__serio_register_port         2   135017    67508        0 
```

#### kft nested call trace with `kd -c`

Below is a `kd -c` trace of the data from a log taken from a PPC440g platform, from a (dynamic) trace of the function `do_fork()`.

Here is the configuration file that was used:

```
new
begin
  trigger start entry do_fork
  trigger stop exit do_fork
end 
```

Here is the first part of the trace in nested call format: Times (Entry, Duration and Local) are in micro-seconds. Note the timer interrupt during the routine.



### 使用 KFT 监控跟踪数据

以下是一个使用 KFT 捕获的内核函数跟踪示例输出：

```text
 Entry      Duration   Local       Pid    Trace
---------- ---------- ---------- ------- ---------------------------------
        4      20428        209      33 do_fork
        7          6          6      33 |  alloc_pidmap
       18       2643         84      33 |  copy_process
       21        114         19      33 |  |  dup_task_struct
       24          8          6      33 |  |  |  prepare_to_copy
       27          2          2      33 |  |  |  |  sub_preempt_count
       35         22          9      33 |  |  |  kmem_cache_alloc
       38          2          2      33 |  |  |  |  __might_sleep
       43         11          9      33 |  |  |  |  cache_alloc_refill
       49          2          2      33 |  |  |  |  |  sub_preempt_count
       60         65          6      33 |  |  |  __get_free_pages
       63         59         14      33 |  |  |  |  __alloc_pages
       65          3          3      33 |  |  |  |  |  __might_sleep
       71          3          3      33 |  |  |  |  |  zone_watermark_ok
       77         37         17      33 |  |  |  |  |  buffered_rmqueue
       80          4          4      33 |  |  |  |  |  |  __rmqueue
       86          3          3      33 |  |  |  |  |  |  sub_preempt_count
       92          3          3      33 |  |  |  |  |  |  bad_range
       98          2          2      33 |  |  |  |  |  |  __mod_page_state
      103          8          5      33 |  |  |  |  |  |  prep_new_page
      106          3          3      33 |  |  |  |  |  |  |  set_page_refs
      117          2          2      33 |  |  |  |  |  zone_statistics
      141         25          4      33 |  |  do_posix_clock_monotonic_gettime
      143         21          6      33 |  |  |  do_posix_clock_monotonic_get
      146         15          6      33 |  |  |  |  do_posix_clock_monotonic_gettime_parts
      149          9          6      33 |  |  |  |  |  getnstimeofday
      152          3          3      33 |  |  |  |  |  |  do_gettimeofday
      169          3          3      33 |  |  copy_semundo
      174         41         17      33 |  |  copy_files
      177         19          9      33 |  |  |  kmem_cache_alloc
      180          2          2      33 |  |  |  |  __might_sleep
      185          8          5      33 |  |  |  |  cache_alloc_refill
      188          3          3      33 |  |  |  |  |  sub_preempt_count
      200          3          3      33 |  |  |  count_open_files
      209          2          2      33 |  |  |  sub_preempt_count
      218         19          8      33 |  |  kmem_cache_alloc
      220          2          2      33 |  |  |  __might_sleep
      225          9          6      33 |  |  |  cache_alloc_refill
      229          3          3      33 |  |  |  |  sub_preempt_count
      241          2          2      33 |  |  sub_preempt_count
      246        216          9      33 |  |  kmem_cache_alloc
      249        199        199      33 |  |  |  __might_sleep
----------- !!!! start --------------
      253        151         63      33 timer_interrupt
      256          8          6      -1 !  profile_tick
      259          2          2      -1 !  !  profile_hit
      267         61         15      -1 !  update_process_times
      270          8          5      -1 !  !  account_system_time
      273          3          3      -1 !  !  !  update_mem_hiwater
      281          8          5      -1 !  !  run_local_timers
      284          3          3      -1 !  !  !  raise_softirq
      293         27         16      -1 !  !  scheduler_tick
```

### 附录 C - 使用 KFT 监控栈使用情况

```
* 配置 CONFIG_KFI_SAVE_SP（如果希望将栈指针保存为跟踪数据的一部分）
```

### 附录 D - KFT 操作注意事项

#### 跟踪开销

KFT 利用 `gcc` 编译器的 `-finstrument-functions` 功能，在内核函数的入口和出口处添加插桩调用。即使未激活跟踪，这也会在内核执行期间产生大量开销。因此，在目标板的默认配置中，KFT 是关闭的。

这种高开销意味着使用 KFT 可能会干扰设备上的时间敏感操作。当内核配置了 KFT 时，无论是通过 KFT 还是其他性能测量工具获得的结果，在解释设备上的性能数据时都应格外小心。KFT 非常适合提供相对性能比较的数据，但不适合用于绝对性能计时。

* * *

**性能**：KFT 会给内核执行增加相当多的开销。原因是编译器在每个函数的开头和结尾都添加了插桩钩子，这些钩子需要额外的时间来执行。当跟踪激活时，事件会与触发器和过滤器进行比较并记录到跟踪缓冲区，这会消耗更多时间。使用插桩的内核不适合用于生产环境。

**本地时间**：在使用 `kd` 提供的'本地时间'数字时需谨慎。这些数字是通过计算函数的进入和退出时间，然后减去顶层函数生命周期内调用的其他函数的持续时间得出的。然而，由于过滤、中断处理或上下文切换，这些数字可能会严重失准。

##### 开销测量

三菱测量了 KFI（KFT 的前身）的开销，测量周期是从 `start_kernel()` 到 `smp_init()`。

测试平台为：SH7751R 240MHz（内存时钟 80MHz）

```text
启用 KFI    : 922.419 毫秒
未启用 KFI : 666.982 毫秒
开销        : 27.69%
```

#### 跟踪缓冲区耗尽

由于内核中的每个函数都被跟踪，在某些跟踪配置下，跟踪缓冲区可能会非常迅速地填满。即使机器看起来空闲，内核函数每秒也会执行数千次。

跟踪缓冲区不是环形的。一旦缓冲区被数据填满，跟踪捕获将自动停止。因此，在跟踪期间跟踪缓冲区被耗尽是很常见的。

解决方法：

```text
* 增加跟踪缓冲区大小
* 使用过滤器
  * 仅按特定函数过滤
  * 增加要保存到跟踪中的最小函数持续时间
```

* * *

**问：** 是否有办法调整触发器或过滤器以减少内存使用？

**答：** 内存使用量由日志大小决定，日志大小由 KFT 配置中的 `logentries` 指定。如果未指定 `logentries`，它会默认为一个相当大的数字（当前代码中为 20,000）。要使用更小的跟踪日志，请在 KFT 配置中指定更小的 `logentries` 数目。

使用触发器和过滤器可以帮助你将更多（或更相关的）数据放入日志中，从而更容易看到感兴趣的信息。

通过设置更"窄"操作范围的启动和停止触发器，放入日志的数据量将更加有限。例如，静态跟踪的默认配置使用：

```text
trigger start entry start_kernel
trigger stop entry to_userspace
```

这将跟踪内核在这两个例程之间执行的**所有**操作。但是，你可以通过使用更精确的触发器，将跟踪限制在内核初始化的一个小得多的时段内。以下是一个仅监视 `mem_init()` 的触发器示例：

```text
trigger start entry mem_init
trigger stop exit mem_init
```

过滤器对于减少跟踪日志中的条目数也至关重要。如果未设置时间过滤器，KFT 将记录内核执行的每个函数。这会迅速淹没日志（无论你通过 `logentries` 预留了多少空间）。

当使用 KFT 查找内核中的长耗时函数时，我们通常对执行速度快的例程不感兴趣，而是使用类似 `filter mintime 500` 的方式过滤掉耗时少于 500 微秒的例程。

#### 早期时钟问题



On many platforms, the clock used for performing trace timings is not available immediately when the kernel begins execution. Often, the clock is initialized sometime during the `time_init()` function of kernel startup. In this case, the function entry times and durations may be incorrect, for functions which begin before the clock is set up. Also time-related filters will not operate correctly on these functions. Usually, this is not a problem, since the times come back as zero, and any minimum time filters in place will remove the events from the trace buffer.

The result of all this is that, on machines where the clock is not immediately available at kernel start, there will be a "blind spot" during initialization, which is effectively not traceable by `KFT`. You can get event data for this "blind" period, by turning off the time filter for events, but this will result in a very large set of events (all without valid timing information) at the beginning of the event log.

## Adding platform support for the KFT clock source

By default, `KFT` uses `sched_clock()` as the clock source for event timings. This is called from the routine `kft_readclock()`.

`sched_clock()` is new in the 2.6 kernel, and returns a 64-bit value containing nanoseconds (not necessarily relative to any particular time base, but assumed to be monotonically increasing, and relatively frequency-stable.)

If your platform has good support for `sched_clock()`, then `KFT` should work for you unmodified. If not, you may wish to do one of two things:

- improve support for `sched_clock()` in your board port, or
- write a custom `kft_readclock()` routine.

A "good" `sched_clock()` routine will provide at least microsecond resolution on return values. Some architectures have `sched_clock()` returning values based on the `jiffy` variable, which on many embedded platforms only has resolution to 10 milliseconds.

There are some sample custom `kft_readclock()` routines in the current code for different architectures. These alternate routines are not active, via pre-processor conditionals. However, you can use them for samples of how to write your own custom `KFT` clock routine.

## Modification History

| **Date** | **Version** | **Description** |
| --- | --- | --- |
| 2006-10-13 | 0.1.0 | First draft of document |
| 2007-04-26 | 0.1.1 | Fixed "run run" typo, and added some material on filters and triggers |

[Categories](http://eLinux.org/Special:Categories "Special:Categories"):

- [Development Tools](http://eLinux.org/Category:Development_Tools "Category:Development_Tools")
- [Tips and Tricks](http://eLinux.org/Category:Tips_and_Tricks "Category:Tips and Tricks")

# Linux Kernel State Tracer

> From: [eLinux.org](http://eLinux.org/Linux_Kernel_State_Tracer "http://eLinux.org/Linux_Kernel_State_Tracer")

Table Of Contents:

## Contents

- 1 Description
  - 1.1 Rationale
- 2 Resources
  - 2.1 Projects
  - 2.2 Documents and presentations
  - 2.3 Specifications
- 3 Downloads
  - 3.1 Patch
  - 3.2 Utility programs
- 4 How To Use
- 5 How to validate
- 6 Sample Results
  - 6.1 Case Study 1
  - 6.2 Case Study 2
- 7 Status
- 8 Future Work/Action Items

## Description

[This section describes the technology ....]

`LKST` is Kernel State Tracer for Linux in order to keep track of Kernel Event such as:

```
- Process Management
- Interrupt
- Exceptions
- System Calls
- Memory Managements
- Networking: sending packets, receiving packets
- Sys V IPC
- Locks
- Timer
- Oops
```

Originally `LKST` is developed for Linux Enterprise Systems and now we have port it to Reference Boards for Embedded Systems and currently `SH4` port(`RTS7751R2D`), `MIPS/TX49` port (`RBHMA4400CE`) and `ARM/OMAP` port (`TI OMAP INNOVATOR/OSK`) are available.

### Rationale

`LKST` is one of a number of tracing systems available for the Linux kernel. Such event tracing systems are very useful for analyzing kernel behaviour, and learning how interrupts, kernel threads and user-space applications interact on the system.

## Resources

### Projects

Here is some information about `LKST`:

- project home page: [`lkst.sourceforge.net/`](http://lkst.sourceforge.net/)

### Documents and presentations

- [Media:CELF_LKST_SH_Presen-2005-1.pdf](http://eLinux.org/images/a/a4/CELF_LKST_SH_Presen-2005-1.pdf "CELF LKST SH Presen-2005-1.pdf")
  - presentation given by Hitachi at CELF Jan 2005 technical conference.
- [Media:CELF_LKST_SH_Lineo-2005-2.pdf](http://eLinux.org/images/b/b2/CELF_LKST_SH_Lineo-2005-2.pdf "CELF LKST SH Lineo-2005-2.pdf")
  - presentation given by Lineo at CELF Jan 2005 technical conference.
- [Media:HITACHI-LKST-CELF-200601.pdf](http://eLinux.org/images/4/46/HITACHI-LKST-CELF-200601.pdf "HITACHI-LKST-CELF-200601.pdf")
  - presentation given at International Technical Conference, June 2006
- [Media:CELFTokyoJam6_LkstUpdate_Lineo.pdf](http://eLinux.org/images/1/13/CELFTokyoJam6_LkstUpdate_Lineo.pdf "CELFTokyoJam6 LkstUpdate Lineo.pdf")
  - presentation 'Features of lkslogtools' given at CELF Jan 2006 technical jamboree (6)

### Specifications

## Downloads

### Patch

- You can acquire patches at: [`sourceforge.net/projects/lkst/`](http://sourceforge.net/projects/lkst/)
- and click the link of |Patches|: [`sourceforge.net/tracker/?group_id=41854&atid=431465`](http://sourceforge.net/tracker/?group_id=41854&atid=431465)

### Utility programs

[other programs, user-space, test, etc. related to this technology]

## How To Use

## How to validate

[put references to test plans, scripts, methods, etc. here]

## Sample Results

[Examples of use with measurement of the effects.]

### Case Study 1

### Case Study 2

## Status

- Status: [implemented]

```
(one of: not started, researched, implemented, measured, documented, accepted)
```

- Architecture Support:

```
(for each arch, one of: unknown, patches apply, compiles, runs, works, accepted)
```

- i386: works
- x86_64: works
- ia64: works
- ARM: runs
- PPC: unknown
- MIPS: runs
- SH: runs

## Future Work/Action Items

Here is a list of things that could be worked on for this feature:

[Category](http://eLinux.org/Special:Categories "Special:Categories"):

- [Development Tools](http://eLinux.org/Category:Development_Tools "Category:Development_Tools")
