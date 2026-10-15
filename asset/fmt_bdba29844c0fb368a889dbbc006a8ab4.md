
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
