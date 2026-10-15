
### 命令补丁

| PKHL 10453 | B.10.00.00.AA | LVM kernel and semaphores |
| PKHL 10453 | B.10.00.00.AA | system() deadlock & fixes |
| PKHL 10464 | B.10.00.00.AA | HF-PB cumulative patch (fcs) |
| PKHL 10670 | B.10.00.00.AA | disc33/disc3 cumulative patch |
| PKHL 7764 | B.10.00.00.AA | Data loss when truncating VxFS (JFS) |
| PKHL 7600 | B.10.00.00.AA | IMF for kernels larger than 13 Megabytes |
| PKHL 7900 | B.10.00.00.AA | KVM kernel deadlock & fixes |
| PKHL 8188 | B.10.00.00.AA | NDELAY and Zion hang |
| PKHL 8204 | B.10.00.00.AA | Fix for system hang during deployment |
| PKHL 8537 | B.10.00.00.AA | Fix vtrace bug. Release memory. |
| PKHL 8656 | B.10.00.00.AA | connected to FW interface |
| PKHL 8684 | B.10.00.00.AA | Two panics page fault on ICS - unreserve |
| PKHL 8780 | B.10.00.00.AA | patch on GSC/HSC MP machines on kernel |
| PKHL 9076 | B.10.00.00.AA | MMF performance, large SHMEM, buffer cache for RA-8000 |
| PKHL 9152 | B.10.00.00.AA | NFS Kernel Megpatch |
| PKHL 9156 | B.10.00.00.AA | Fix Panic caused by MP race |
| PKHL 9362 | B.10.00.00.AA | Data corruption on RA-BAOD based systems |
| PKHL 9371 | B.10.00.00.AA | Fix for variable VxFS file system |
| PKHL 9570 | B.10.00.00.AA | NFS and VxFS cumulative patch |
| PKHL 9712 | B.10.00.00.AA | select() system call for "ediquota -t" |
| PKHL 9724 | B.10.00.00.AA | fix performance improvement |
| PKHL SP20 | B.10.00.00.AA | Unofficial_test_patch |

huxpl 的命令补丁数量为 11。

| Patch Number | Revision | Description |
| :--- | :--- | :--- |
| PKCO 10016 | A.01.20 | HP Disk Array Utilities w/AutoRAID Manager |
| PKCO 10027 | B.10.00.00.AA | libc cumulative patch |
| PKCO 10048 | B.10.00.00.AA | LVM cumulative patch |
| PKCO 10175 | B.10.00.00.AA | year 2000 white patch |
| PKCO 10295 | B.10.00.00.AA | Fix VxFS snapshot |
| PKCO 10311 | B.10.00.00.AA | HFS maintenance |
| PKCO 8549 | B.10.00.00.AA | fsck error |
| PKCO 9228 | B.10.00.00.AA | large HFS |
| PKCO 9396 | B.10.00.00.AA | Fix for file |
| PKCO 9543 | B.10.00.00.AA | stale file handle |
| PKCO 9895 | B.10.00.00.AA | Cumulative patch |

huxpl 的网络补丁数量为 6。

| Patch Number | Revision | Description |
| :--- | :--- | :--- |
| PHNE 10512 | B.10.00.00.AA | LAN products |
| PHNE 6190 | B.10.00.00.AA | telnetd(1M) |
| PHNE 8328 | B.10.00.00.AA | STREAMS |
| PHNE 9060 | B.10.00.00.AA | ARPA |
| PHNE 9107 | B.10.00.00.AA | ocd |
| PHNE 9438 | B.10.00.00.AA | Mux |

huxpl 的系统补丁数量为 12。

| Patch Number | Revision | Description |
| :--- | :--- | :--- |
| PHSS 7789 | C.10.00 | Predictive Support: SCS-Scan |
| PHSS 8490 | B.10.00.00.AA | pxdb |
| PHSS 8590 | B.10.00.00.AA | diagnostic patch |
| PHSS 8709 | B.10.00.00.AA | Development Nov96 |
| PHSS 8711 | B.10.00.00.AA | X11R/Motif.2 Development Nov96 |
| PHSS 9096 | B.10.00.00.AA | core components (A.10.24) |
| PHSS 9356 | B.10.00.00.AA | X11/Xt/Motif D-Point patch |
| PHSS 9400 | B.10.00.00.AA | cumulative patch |
| PHSS 9778 | B.10.00.00.AA | X11R/Xt/Motif Nov96-D |
| PHSS 9803 | B.10.00.00.AA | CDE Runtime Mar9 |
| PHSS 9855 | B.10.00.00.AA | HP++ (A.10.24) with a correct eh/lib++ |
| PHSS 9977 | B.10.00.00.AA | to fix numerous defects |

以下是运行 `swlist` 命令产生的 `swlist` 输出。你可以看到 `neuropath.sh` 生成的补丁列表比这个 `swlist` 输出易读得多。

```
# Initializing...
# Contacting target "hpux1"...
# Target: hpux1/
# Bundle(s):
User.10 HP-UX 2-User License (For degrading user level)
A3516A_APZA.01.16 HP Disk Array Utilities for Unix (S800)
B2491A_APZB.B.10.20 MirrorDisk/UX
B3191A_APZB.B.10.20 DCE/9000 Core Services Media and Manuals, Intern-version
B3193A_APZB.B.10.20 DCE/9000 Application Development Tools Media and Man-
```

# 示例脚本示例
