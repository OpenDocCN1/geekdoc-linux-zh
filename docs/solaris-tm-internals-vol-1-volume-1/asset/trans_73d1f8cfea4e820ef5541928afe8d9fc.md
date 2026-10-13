

```c
        printf("Total User Time:...............", &user);
        printf("Total System Time:..............", &sys);
        printf("Other System Trap Time:.........", &pup->pt_time);
        printf("Text Page Fault Sleep Time:.....", &pup->pt_ftime);
        printf("Data Page Fault Sleep Time:.....", &pup->pf_dftime);
        printf("Kernel Page Fault Sleep Time:...", &pup->pk_ftime);
        printf("User Lock Wait Sleep Time:......", &pup->pltime);
        printf("All Other Sleep Time:...........", &pup->pslptime);
        printf("Time Waiting for a CPU..........", &pup->wt_time);
        printf("Stopped Time....................", &pup->p_stoptime);
    }

    (void) close(fd);
    return (rval);
}

static void
hr_min_sec(char *buf, long sec)
{
        if (sec >= 3600)
                (void) sprintf(buf, "%ld:%2.2ld:%2.2ld",
                    sec / 3600, (sec % 3600) / 60, sec % 60);

        else if (sec >= 60)
                (void) sprintf(buf, "%ld:%2.2ld",
                    sec / 60, sec % 60);

        else
                (void) sprintf(buf, "%ld", sec);
}

static void
prtime(char *name, timestruct_t *ts)
{
        char buf[32];

        hr_min_sec(buf, ts->tv_sec);
        (void) fprintf(stdout, "%s%s.%3u\n",
            name, buf, (u_int)ts->tv_nsec/1000000);
}

static int
perr(const char *s)
{
        if (s)
                (void) fprintf(stderr, "%s: ", progname);
        else
                s = progname;
        perror(s);
        return (1);
}

static void
tsadd(timestruct_t *result, timestruct_t *a, timestruct_t *b)
{
        result->tv_sec = a->tv_sec + b->tv_sec;
        if ((result->tv_nsec = a->tv_nsec + b->tv_nsec) >= 1000000000) {
                result->tv_nsec -= 1000000000;
                result->tv_sec += 1;
        }
}

static void
tssub(timestruct_t *result, timestruct_t *a, timestruct_t *b)
{
        result->tv_sec = a->tv_sec - b->tv_sec;
        if ((result->tv_nsec = a->tv_nsec - b->tv_nsec) < 0) {
                result->tv_nsec += 1000000000;
                result->tv_sec -= 1;
        }
}
```

## 参考文献

- 1. Bach, M. J., *UNIX操作系统设计*, Prentice Hall, 1986.
- 2. Bonwick, Jeff, *Slab分配器：一种对象缓存内核内存分配器*. Sun Microsystems, Inc. 白皮书.
- 3. Bourne, S. R., *UNIX系统*, Addison-Wesley, 1983.
- 4. Catanzaro, B., *多处理器系统架构*, Prentice Hall, 1994.
- 5. Cockcroft, A., *Sun性能与调优——Java与Internet*, 第2版, Sun Microsystems Press/Prentice Hall, 1998.
- 6. Cockcroft, A., *CPU时间测量误差*, Computer Measurement Group 论文 2038, 1998.
- 7. Cypress Semiconductor, *CY7C601 SPARC RISC 用户指南*, Ross Technology, 1990.
- 8. Eykholt, J. R., 等, *超越多处理——SunOS内核的多线程化*, 1992年夏季 USENIX 会议论文集.
- 9. Gingell, R. A., Moran, J. P., Shannon, W. A., *SunOS中的虚拟内存架构*, 1987年夏季 USENIX 会议论文集.
- 10. Goodheart, B., Cox, J., *魔幻花园详解——UNIX System V Release 4 内部结构*, Prentice Hall, 1994.
- 11. Hwang, K., Xu, Z., *可扩展并行计算*, McGraw-Hill, 1998.
- 12. Intel Corp., *Intel架构软件程序员手册，第1、2、3卷*, Intel 部件号 243190、243191 和 243192, 1993.
- 13. Kleiman, S. R., *Vnode：Sun UNIX 中多种文件系统类型的架构*, 1986年夏季 USENIX 会议论文集.
- 14. Kleiman, S., Shah, D., Smaalders, B., *线程编程*, Prentice Hall, SunSoft Press, 1996.
- 15. Leffler, S. J., McKusick, M. K., Karels, M. J., Quarterman, J. S., *4.3BSD UNIX 操作系统的设计与实现*, Addison-Wesley, 1989.
- 16. Lewis, B., Berg, D. J., *线程入门：多线程编程指南*, SunSoft Press/Prentice Hall, 1996.
- 17. Lewis, B., Berg, D. J., *使用Pthreads的多线程编程*. Sun Microsystems Press/Prentice Hall, 1998.
- 18. McKusick, M. K., Bostic, K., Karels, M. J., Quarterman, J. S., *4.4 BSD 操作系统的设计与实现*, Addison-Wesley, 1996.
- 19. McKusick, M. K., Joy, W., Leffler, S., Fabry, R., *UNIX快速文件系统*, ACM Transactions on Computer Systems, 2(3):181–197, 1984年8月.
- 20. Moran, J. P., *SUNOS 虚拟内存实现*, 1988年 EUUG 会议论文集.
- 21. Pfister, G., *探索集群*, Prentice Hall, 1998.
- 22. Rosenthal, David S., *演进Vnode接口*, 1990年夏季 USENIX 会议论文集.
- 23. Schimmel, C., *面向现代架构的UNIX系统*, Addison-Wesley, 1994.
- 24. Seltzer, M., Bostic, K., McKusick, M., Staelin, C., *UNIX日志结构文件系统的实现*, USENIX冬季会议论文集, 1993年1月.
- 25. Shah, D. K., Zolnowsky, J., *轻量级线程的UNIX信号模型演进*, Sun 专有/机密，仅供内部使用，白皮书, SunSoft TechConf '96.
- 26. Snyder, P., *tmpfs：虚拟内存文件系统*, Sun Microsystems 白皮书.
- 27. SPARC International, *System V 应用二进制接口——SPARC 版本9处理器补充*, 1997.
- 28. Sun Microsystems, *编写设备驱动程序 - 部件号 805-3024-10*, Sun Microsystems, 1998.
- 29. Sun Microsystems, *STREAMS 编程指南 - 部件号 805-4038-10*, Sun Microsystems, 1998.
- 30. Sun Microsystems, *UltraSPARC 微处理器用户手册 - 部件号 802-7220*, Sun Microsystems, 1995.
- 31. Stevens, W. R., *UNIX环境高级编程*, Addison-Wesley, 1992.
- 32. Stevens, W. R., *UNIX网络编程，第2卷。进程间通信。第2版*. Addison-Wesley, 1998.
- 33. Tanenbaum, A., *操作系统：设计与实现*. Prentice Hall, 1987.
- 34. Tucker, Andy, *调度器激活*, PSARC 1996/021, Sun 内部专有文档. 1996年3月.
- 35. Tucker, Andy, *Solaris中的调度器激活*, SunSoft TechConf '96. Sun 专有/机密——仅供内部使用的文档.
- 36. Talluri, M., 地址转换层次结构中超级页和子块的使用, 计算机科学博士论文, 1995.
- 37. Tucker, Andy, 私人通信.
- 38. UNIX Software Operation, *System V 应用二进制接口 – UNIX System V*, Prentice Hall/UNIX Press, 1990.
- 39. Vahalia, U., *UNIX 内部结构——新前沿*, Prentice Hall, 1996.
- 40. Van der Linden, P., *C语言专家编程——C语言深层秘密*, SunSoft Press/Prentice Hall, 1994.
- 41. Weaver, D., Germond, T., (编辑), *SPARC架构手册，版本9*, Prentice Hall, 1994.
- 42. Wong, B., *Sun Solaris服务器的配置与容量规划*, Sun Microsystems Press/Prentice Hall, 1996.
- 43. Zaks, Rodney, *Z80编程*, Sybex Computer Books, 1982.

## 索引

### 符号

- `%ipf` 600
- `/dev/zero` 153
- `/etc/name_to_sysnum` 44
- `/etc/system` 621
- `/proc` 23, 164
- `_FILE_OFFSET_BITS` 520
- `_LARGEFILE64_SOURCE` 520
- `_t_astflag` 290
- `_t_post_syscall` 290
- `_t_sig_check` 290
- `_t_trapret` 290
- “MemTool — *非捆绑内存工具*” 见第275、163页

### 数字

- 64位应用程序 5
- 64位数据类型 5
- 64位设备支持 518
- 64位文件应用程序编程接口 518
- 64位文件 517
- 64位内核 8
- 64位支持 5

### A

- ABS32 210
- 访问控制列表 531
- 自适应锁 72
- add_invtr() 42
- add_softintr() 42
- 地址空间 137
- 地址空间 (20, 262)
- 地址空间处理器 263
- 地址空间标识符 198
- 地址空间标识符 198
- advise() 146
- AF_UNIX 483
- 代理LWP 318
- aio_read 489
- 对齐 230
- 分配 231
- 分配失败 231
- allocate_vfssw() 554
- 分配与存储 526
- amp 153
- ani_free 156
- anon 头部 155
- anon 槽位 155, 159
- anon_alloc() 155, 159
- anon_copy_ptr() 155
- anon_create() 155

