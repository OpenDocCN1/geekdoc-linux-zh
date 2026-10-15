
`SADd_type` 值决定了哪些扩展。19.2 消息类型。

| 消息类型 | 到内核？ | 来自内核？ | 描述 |
|---|---|---|---|
| `SADB_ACQUIRE` | | | 请求创建 |
| `SADB_ADD` | | | 添加一个 |
| `SADB_DELETE` | | | 删除一个 |
| `SADB_DUMP` | | | 导出 |
| `SADB_EXPIRE` | | | 通知 |
| `SADB_FLUSH` | | | 刷新整个 |
| `SADB_GET` | | | 获取一个 |
| `SADB_GETSPI` | | | 分配一个 |
| `SADB_REGISTER` | | | 作为回复注册 |
| `SADB_UPDATE` | | | 更新部分 |

19.3 SA 类型。

| 安全关联类型 | 描述 |
|---|---|
| `SAD_STYPE_AH` | IPsec 认证 |
| `SAD_STYPE_ESP` | IPsec 封装安全载荷 |
| `SAD_STYPE_MIP` | 移动 IP |
| `SAD_STYPE_OSPF2` | OSPFv2 认证 |
| `SAD_STYPE_RIPv2` | RIPv2 认证 |
| `SAD_STYPE_RSVP` | RSVP 认证 |
| `SAD_STYPE_UNSPECIFIED` | 未指定；仅有效在 |

19.4 PF_KEY 扩展。

| 扩展头部类型 | 描述 | 结构 |
|---|---|---|
| `SAD_EXT_ADDRESS_DST` | SA 目的地址 | `sad_address` |
| `SAD_EXT_ADDRESS_PROXY` | SA 代理地址 | `sad_address` |
| `SAD_EXT_ADDRESS_SRC` | SA 源地址 | `sad_address` |
| `SAD_EXT_IDENTITY_DST` | 目的身份 | `sad_ident` |
| `SAD_EXT_IDENTITY_SRC` | 源身份 | `sad_ident` |
| `SAD_EXT_KEY_AUTH` | 认证密钥 | `sad_key` |
| `SAD_EXT_KEY_ENCRYPT` | 加密密钥 | `sad_key` |
| `SAD_EXT_LETIME_CURRENT` | SA 的当前寿命 | `sad_lifetime` |
| `SAD_EXT_LETIME_HARD` | SA 的硬寿命限制 | `sad_lifetime` |
| `SAD_EXT_LETIME_SOFT` | SA 的软寿命限制 | `sad_lifetime` |
| `SAD_EXT_PROPOSAL` | 建议方案 | `sad_prop` |
| `SAD_EXT_SA` | SA | `sad_sa` |
| `SAD_EXT_SENSITIVITY` | SA 的敏感性 | `sad_sens` |
| `SAD_EXT_SPIRANGE` | SPI 值的接受范围 | `sad_spirange` |
| `SAD_EXT_SUPPORTED_AUTH` | 支持的认证算法 | `sad_supported` |
| `SAD_EXT_SUPPORTED_ENCRYPT` | 支持的加密算法 | `sad_supported` |

我们现在展示几个示例，以及在密钥管理套接字上几种常见操作中涉及的消息和扩展。

## 19.3 转储安全数据库 (`SADB`)

要转储当前的 `SADB`，进程使用 `SADB_DUMP` 消息。这是最简单的消息，因为该消息不需要任何扩展的16 字节 `sadb_msg` 头部。当进程通过密钥管理套接字向内核发送 `SADB_DUMP` 消息后，内核将向同一套接字返回 `SADB_DUMP` 消息，包含 `SADB` 中的每个条目。列表的末尾由 `sadb_msg_seq` 字段值为 0 的消息来限制。

可以通过将请求中的 `sadb_msg_type` 字段设置为图 19.3 中的任一值来限制 SA 的类型。如果设置为 `SADB_STYPE_UNSPEC`，则会返回数据库中的所有 SA。否则，仅返回指定类型的 SA。并不是所有的实现版本都支持所有类型的安全关联。KAME 实现仅支持 IPSec SA（`SADB_STYPE_AH` 和 `SADB_STYPE_ESP`），因为尝试转储 `SADB_STYPE_RIPV2` 条目将导致错误，错误码为 `EINVAL`。当请求一个空表的特定类型时，将返回错误码 `ENOENT`。

我们使用图 19.5 转储 `SADB` 的程序如下：

### 图 19.5 在密钥管理套接字上包含 `SADB_DUMP` 命令的程序。

```c
key/dump.c

void
sadb_dump(int type)
{
    int s;
    char buf[4096];
    struct sadb_msg msg;
    int gotoef;
    s = socket(PF_KEY, SOCK_RAW, PF_KEY_V2);
    /* Build and write SADB_DUMP request */
    bzero(&msg, sizeof(msg));
    msg.msg_version = PF_KEY_V2;
    msg.msg_type = SADB_DUMP;
    msg.msg_type = sadb_msg_type;
    msg.msg_len = sizeof(msg) / 8;
    msg.msg_pid = getpid();
    printf("Sending dump message:\n");
    print_sadb(&msg, sizeof(msg));
    write(s, &msg, sizeof(msg));
    printf("\nmessages returned:\n");
    /* Read and print SADB_DUMP replies until done */
    gotoef = 0;
    while (gotoef == 0) {
        int msglen;
        struct sadb_msg *msgsp;
        msglen = Read(s, &buf, sizeof(buf));
        msgp = (struct sadb_msg *) &buf;
        print_sadb_msg(msgp, msglen);
        if (msgp->sadb_msg_seq == 0)
        {
            gotoef = 1;
        }
    }
    close(s);
}
main(int argc, char **argv) {
    int    satype = SADB_SATYPE_UNSPEC;
    int c;
    int optterr = 0;   /* don't want getopt () writing to stderr */
    while (c = getopt(argc, argv, "t:")) != -1) {
        switch (c) {
            case 't':
                if (satype = getsypename(optarg)) == -1)
                    err_quit("invalid -t option %s", optarg);
                break;
            default:
                err_quit("unrecognized option: %c", c);
        }
    }
    sadb_dump(satype);
}
```

这是我们第一次遇到 POSIX `getopt` 函数。第三个参数是一个字符串，指定了我们允许作为命令行参数的字符，在本例中为 `t`。后面跟着一个冒号，表示该选项需要参数。在具有多个选项的程序中，它们会被拼接在一起；例如图 29.7 传递 `i:l:v` 表示它接受四个选项：`i` 和 `l` 需要参数，而 `0` 和 `v` 不需要。该函数通过包含 `<unistd.h>` 定义的四个全局变量工作。

```c
extern char *optarg;
extern int optind, optterr, optopt;
```
