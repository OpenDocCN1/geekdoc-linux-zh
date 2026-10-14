
```c
MODULE_AUTHOR("OSR Open Systems Resources, Inc.");
MODULE_DESCRIPTION("The NT Insider");
MODULE_LICENSE("GPL");

static struct file_system_type ntinsiderfs_fs_type = {
    .owner    = OSR,
    .name     = "The NT Insider",
    .fs_flags = FS_SEPTEMBER | FS_OCTOBER | FS_2017,
    .mount    = ntinsiderfs_mount,
};

static int __init init_ntinsiderfs_fs(void)
{
    int err;

    err = init_sept_oct_issue();
    if (err)
        panic("FESF on Linux!", 3);

    err = we_need_a_driver_developer_conference(4);
    if (unlikely(err))
        goto out_uninit_issue;

    err = handling_cleanup_close_cancel(6);
    if (err)
        goto out_destroy_pontification;

    standard and isolation minifilters = 8;

    /*
     * TODO: Read about the Isolation Minifilter Solution Framework (IMSF)
     * for Windows on Page 10
     */

    the_scoop_on_universal_drivers = 12;

    err = register_filesystem(&ntinsiderfs_fs_type);
    if (likely(err))
        goto out_cleanup_cleanup_close_cancel;

    return 0;

out_cleanup_cleanup_close_cancel:
    cleanup_cleanup_close_cancel();
out_destroy_pontification:
    destroy_peter_pontificates();
out_uninit_issue:
    uninit_sept_oct_issue();

    return err;
}

module_init(init_ntinsiderfs_fs);
```

- Inside:
  - Peter Pontificates
  - Windows Internals & SW Drivers—Register Now!
  - Seminar Schedule

## 与 OSR 社交

### 实时更新

万一你还没有关注我们 Twitter、Facebook、LinkedIn，或我们自己的“osrhits”邮件列表，下面是近期在 Windows 驱动开发社区引起关注的一些贡献：

**追踪 NTSTATUS 到其来源**

本周我遇到了一个情况，我真的很想调用 API SeTokenIsAdmin。我隐约记得这个 API 周围有一些问题，快速 Google 后很快出现了 NTDEV 和 NTFSU 的几个帖子，暗示了一个在 2015 年修复的安全问题...

[http://www.osr.com/blog/2017/07/14/tracking-ntstatus-source/](http://www.osr.com/blog/2017/07/14/tracking-ntstatus-source/)

**认证签名 — 它并不是一个谜**

在过去几周里，我们接到了来自多位人士的联系——客户和非客户 alike——他们讲述的故事大同小异，惊慌程度各不相同。他们共同点是，他们都对在某些情况下让驱动程序在较新版本的 Windows 上安装所需的过程感到完全困惑。

[http://www.osr.com/blog/2017/07/06/attestation-signing-mystery/](http://www.osr.com/blog/2017/07/06/attestation-signing-mystery/)

**WinDbg、调试器对象和 JavaScript！哦，天哪！**

如果您错过了，WinDbg 内部正在进行大量更改。WinDbg 在授予访问权限和向用户呈现数据方面的基本范式正在发生转变，这可能会带来一些相当酷的结果。

[http://www.osr.com/blog/2017/05/18/windbg-debugger-objects-javascript-oh/](http://www.osr.com/blog/2017/05/18/windbg-debugger-objects-javascript-oh/)

**1394 启动调试已死**

TL;DR：不要像我们一样浪费时间——1394 启动调试在 Windows 10 的最新构建上不再工作。

[http://www.osr.com/blog/2017/04/07/1394-boot-debugging-dead/](http://www.osr.com/blog/2017/04/07/1394-boot-debugging-dead/)

**运行 HLK 测试 真的是最佳实践吗？**

事实证明，HLK 测试的有用程度几乎完全取决于你正在编写的驱动程序类型。

[http://www.osr.com/blog/2017/03/22/running-hlk-tests-really-best-practice/](http://www.osr.com/blog/2017/03/22/running-hlk-tests-really-best-practice/)

**Visual Studio 2017 已发布 — 驱动开发人员：请原地不动**

[http://www.osr.com/blog/2017/03/07/visual-studio-2017-released-driver-devs-must-stay-vs-2015/](http://www.osr.com/blog/2017/03/07/visual-studio-2017-released-driver-devs-must-stay-vs-2015/)

**关于 Windows、Git、FUSE 和道德等价性的意外案例**

如今众所周知，微软正在感受到 Git 的热爱…

[http://www.osr.com/blog/2017/02/24/windows-git-fuse-moral-equivalence/](http://www.osr.com/blog/2017/02/24/windows-git-fuse-moral-equivalence/)

**Bugcheck IRQL_UNEXPECTED_VALUE (C8) 的意外案例**

又一个有趣的案例通过 NTDEV 送到我们这里...

[http://www.osr.com/blog/2017/02/17/unexpected-case-bugcheck-irql_unexpected_value-c8/](http://www.osr.com/blog/2017/02/17/unexpected-case-bugcheck-irql_unexpected_value-c8/)

![](img/feabf7ef0b3bb3419a0ef4d863642d48_1_0.png)

