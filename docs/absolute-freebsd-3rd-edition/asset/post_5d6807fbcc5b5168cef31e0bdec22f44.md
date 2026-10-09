
Doofus like me can get over 90 percent of his bugs successfully closed, anyone can. Be warned, however: if you submit enough correct patches, you’ll find that the committers you work with will start to talk about you behind your back. Eventually, they’ll grow tired of acting as the secretary for your high-quality work and offer you commit access. If you refuse, they’ll offer more insistently. Don’t worry; becoming a committer isn’t that painful. The rumors that the FreeBSD Project initiation ritual involves a bunch of Danes with axes behind a bike shed are completely untrue. Mostly.

Keep filing good bug reports anyway; that’s the only way FreeBSD improves!

The worst sort of bug to deal with is a full-on system crash. Let’s talk about how to get information from one.

## System Panics

A *panic* is when the operating system completely stops working. All systems, from the network stack to the disk drive, stop working. A system chooses to panic, or completely stop working, when the kernel faces an unresolvable conflict. If the system achieves a condition that it doesn’t know how to handle, or if it fails its own internal consistency checks, it throws up its hands and says, “I don’t know what to do!” A panic is the kernel’s version of malicious obedience.[^2] Production versions of FreeBSD are increasingly difficult to panic, but it can still happen. The easiest way to panic a system is to do something daft, like yank out a non–hot swappable hard drive while it’s in use. Panics aren’t uncommon when running -current; they’re not frequent, mind you, but they’re not exotic rarities.

FreeBSD is very complex, and neither its royal blood lineage nor the open source development process can protect it from all bugs. Fortunately, that heritage and the development process do give you the tools you need to provide the information for other people to debug your problem. You might begin with a cryptic error code, but you’ll quickly learn that your string of garbage characters means something to someone.

[^2]: Footnote reference retained as per original text structure, likely referring to a specific note about the term "malicious obedience" or similar context in the source book.

A panicking kernel can copy critical information into a crash dump. The crash dump contains enough information about the panic that hopefully a developer can identify and fix the underlying problem. Configure every system to capture crash dumps before you allow them to enter production. FreeBSD can capture crash dumps with an install-time setting, but if you reconfigure your server or have unique disk partitioning, you'll want to confirm that crash dumps still work. This precaution will be wasted on most of your servers but pays off when something explodes.

### Recognizing Panics

When a system panics, it stops running all programs, writing to the disk, and listening to the network. On any version of FreeBSD except -current, a panicking system automatically reboots. Not all unexplained reboots are panics—bad hardware, such as a failing power supply or cruddy memory, can cause a reboot without any sort of log or console message. If you're running -current, though, a panic will cause a console message much like this:

```text
panic: Assertion cp->co_locker == curthread failed at
/usr/src/sys/modules/smbfs/.../
/netsmb/smb_conn.c:363
cpid = 5
KDB: stack backtrace:
db_trace_self_wrapper() at db_trace_self_wrapper+0x2b/frame 0xfffffe085d0db630
vpanic() at vpanic+0x182/frame 0xfffffe085d0db60
kassert_panic() at kassert_panic+0x126/frame 0xfffffe085d0db720
smb_co_unlock() at smb_co_unlock+0x9c/frame 0xfffffe085d0db740
smb_co_put() at smb_co_put+0x68/frame 0xfffffe085d0db770
nsmb_dev_ioctl() at nsmb_dev_ioctl+0x484/frame 0xfffffe085d0db800
devfs_ioctl_f() at devfs_ioctl_f+0x15d/frame 0xfffffe085d0db860
kern_ioctl() at kern_ioctl+0x230/frame 0xfffffe085d0db8c0
sys_ioctl() at sys_ioctl+0x17e/frame 0xfffffe085d0db9a0
amd64_syscall() at amd64_syscall+0x2de/frame 0xfffffe085d0dbab0
Xfast_syscall() at Xfast_syscall+0xfb/frame 0xfffffe085d0dbb0
--- syscall (54, FreeBSD ELF64, sys_ioctl), rip = 0x08008016a, rsp =
0x7fffffffe4f8, rbp = 0x7fffffffe530 ---
KDB: enter: panic
db>
```

The only part of this message that seems even vaguely sensible to me is the first line. I unmounted an SMB filesystem and got this panic message. The first line mentions smbfss, netsmb, and smb_conn, which seem pretty SMB-ish to me.

The db> at the bottom is a debugger command prompt. Hit ENTER a couple of times and you'll see the debugger respond; you can enter commands. Debugger instructions aren't Unix commands, but they help you extract more information out of the system.

### Responding to a Panic

If you get a panic, the first thing to do is get a copy of the panic message. Since FreeBSD is no longer running, the standard methods for copying data from your machine won't work—you can't SSH in, and script(1) is no longer viable. The console might even be completely locked up and unresponsive instead of being in the debugger. In any event, you must have that error message.

Back in the bad old days of the 1990s, FreeBSD didn't automatically reboot after a panic; originally, it just sat there displaying the panic message. The first time I saw a panic, I scrambled for paper and pen. Eventually, I found an old envelope and a broken stub of pencil that made marks if you held it at just the right angle and crawled between the server rack and the rough brick wall. I balanced the six-inch black-and-white monitor in one hand, and with my other hand, I held the envelope against the wall. Apparently, I grow a third hand under duress because I recorded the panic message on the envelope somehow. Finally, scraped and cramped, I slithered back out of the rack and victoriously typed the whole mess into an email. Surely the FreeBSD Project's Panic Emergency Response Team would be able to look at this garbage and tell me exactly what had happened.

I quickly learned that FreeBSD has no elite PERT standing by to take my problem report. Instead, I got a lonesome email: "Can you send a backtrace?" When I asked how, I was directed to a man page. (Drag yourself all the way back to Chapter 1.) Fortunately, the panic was easily reproducible—the only thing that had to happen to recreate the issue was for a customer to log in to the system. I spent the rest of the day struggling to master serial consoles and core dumps.

The problem with the panic message on my envelope was that it gave only a tiny scrap of the story. It was so vague, in fact, that it was like describing a stolen car as “red, with a scratch on the fender.” If you don’t give the car’s make, model, VIN, and license plate number, you can’t expect the police to make much headway. Similarly, without much more information from your crashing kernel, the FreeBSD developers can’t catch the criminal code.

The good news is, panic handling has vastly improved since those days. FreeBSD can automatically record crash dumps and capture everything about a panic. There’s even a toggle in the installer to enable it. I highly recommend testing the panic capture before putting a machine into production, however. This way, if you get a panic, you’re ready and you’ll be able to easily file a complete problem report.

### Preperations

Configuring crash dumps requires telling FreeBSD which swap device to save the dump on, through the `dumpdev` /etc/rc.conf variable. If you set `dumpdev` to `AUTO`, the kernel will automatically save the dump to the first swap device. You can specify a different swap device if needed, but the whole dump must fit in a single swap device. If your regular swap space doesn’t have enough space to hold the dump, add a disk to get sufficient swap space and set `dumpdev` to that partition.

### The Crash Dump in Action

When a system configured to capture panics crashes, it saves a copy of the kernel memory. The copy is called a *dump*. The system can’t save the dump straight to a file. The crashed kernel doesn’t know anything about filesystems, for one thing, and the filesystem might be corrupt or a write could corrupt it. A crashed kernel understands partitions, however, so it can write the dump to a partition. Most FreeBSD hosts have readily
