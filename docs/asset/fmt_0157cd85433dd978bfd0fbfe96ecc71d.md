
```nesc
module AntiTheftRootC {
    uses interface RootControl;
    uses interface Receive as RTheft;
    uses interface AMSend as STheft;

    event void CommControl.startDone(error_t error) {
        ...
        // Set ourselves as the root of the collection tree
        call RootControl.setRoot();
    }

    message_t fwdMsg;
    bool fwdBusy;

    /* When we (as root of the collection tree) receive a new theft alert,
       we forward it to the PC via the serial port */
    event message_t * RTheft.receive(message_t * msg, void* payload, uint8_t len)
    {
        if (len == sizeof(theft_t) && !fwdBusy)
        {
            /* Copy payload from collection system to our serial message buffer
               (fwdMsg), then send our serial message */
            theft_t fwdTheft = call STheft.getPayload(&fwdMsg, sizeof(theft_t));
            if (fwdTheft != NULL) {
                *fwdTheft = *(theft_t *)payload;
                if (call STheft.send(TOS_BCAST_ADDR, &fwdMsg, sizeof(fwdTheft)) == SUCCESS)
                    fwdBusy = TRUE;
            }
        }
        return msg;
    }
}
```

```
fwdBusy = FALSE;
}
}
```

#### 清单 6.26 AntiTheft 基站代码：报告盗窃事件

基站应用必须连接串口（已展示），以及上述代码中使用的收集和分发接口。通过使用树收集标识符对参数化接口进行索引来指定从树接收消息；参数化接口将在第 8.3 节中详细说明。最终的收集和分发连接如下：

```nesc
configuration AntiTheftRootAppC { 
implementation {
... boot, serial and radio wiring ...

components DisseminationC, new DisseminatorC(settings_t, DIS_THEFT);
AntiTheftRootC.DisseminationControl -> DisseminationC;
AntiTheftRootC.USettings -> DisseminatorC;

components CollectionC;
AntiTheftRootC.CollectionControl -> CollectionC;
AntiTheftRootC.RootControl -> CollectionC;
AntiTheftRootC.RTheft -> CollectionC.Receive[COL_THEFT];
}
```

#### 清单 6.27 AntiTheft 基站连接

### 6.5 存储

许多节点都包含一定量的基于闪存的非易失性存储，例如 `micaz` 上有 `512 kB`。`TinyOS` 将这种非易失性存储划分为卷。卷是具有一定格式的连续存储区域，可通过关联接口进行访问。`TinyOS` 定义了三种基本的存储抽象：`Log`、`Block` 和 `Config`。`Log` 用于只追加写入和流式读取，`Block` 用于随机读写，`Config` 用于小型配置数据项。`Log` 和 `Config` 的优点在于，它们更有限的接口支持原子操作：当对 `Log` 或 `Config` 卷的写入完成时，即可保证数据已写入。相比之下，`Block` 接口有一个单独的提交操作。

`TinyOS` 使用这种基于卷的抽象方法而非更传统的文件系统，主要有两个原因。首先，它更简单，减少使用永久存储的应用程序的代码和 RAM 需求。其次，传感器网络通常专用于单个应用程序，它应对其存储需求有合理的了解。

#### 6.5.2 配置数据

就目前而言，防盗节点在关机时会丢失其设置。我们可以通过将设置存储在一个小型配置卷（`configuration volume`）中来解决这个问题：

```text
<volume_table>

  <volume name="AT_SETTINGS" size="512"/>

</volume_table>

configuration AntiTheftAppC {

  implementation {

    ...

    components new ConfigStorageC(VOLUME_AT_SETTINGS) as AtSettings;

    MovingC.Mount -> AtSettings;

    MovingC.ConfigStorage -> AtSettings;

  }

}
```

配置卷在使用前必须通过分阶段（`split-phase`）的 `Mount` 接口进行挂载：

```c
interface Mount {

  command error_t mount();

  event void mountDone(error_t error);

}
```

![](img/53ede4f4266a5731b93bff15d85fa06a_126_0.png)

一旦挂载完成，即可通过 `ConfigStorage` 接口访问该卷：

```c
interface ConfigStorage {

  command error_t read(storage_addr_t addr, void* buf, storage_len_t len);

  event void readDone(storage_addr_t addr, void* buf, storage_len_t len,

                      error_t error);

  command error_t write(storage_addr_t addr, void* buf, storage_len_t len);

  event void writeDone(storage_addr_t addr, void* buf, storage_len_t len,

                       error_t error);

  command error_t commit();

  event void commitDone(error_t error);

  command storage_len_t getSize();

  command bool valid();

}
```

![](img/53ede4f4266a5731b93bff15d85fa06a_126_1.png)

`ConfigStorage` 卷有些特殊，因为它实际上保留了两份内容副本：一份是最近一次提交（`commit`）时的内容，另一份是尚未提交的新内容。

![](img/53ede4f4266a5731b93bff15d85fa06a_127_0.png)

#### 图 6.4 ConfigStorage：写入与提交。

这样做的目的是确保配置数据不会丢失：如果在配置更新过程中节点崩溃，最后提交的数据仍然存在且未损坏。读取操作始终读取最后提交的数据，而写入操作则更新新副本——在成功提交之前，你无法看到已写入的数据。

不过，写入操作仍然是更新操作：如果配置卷包含 10 个字节，且第 2 和第 3 字节通过一次写入被更新，然后该卷被提交，那么新内容为写入前的第 0–1 字节和第 4–9 字节，以及写入的第 2–3 字节，如图 6.4 所示。由于配置卷必须存储多份数据副本以提供可靠性，因此实际可用大小小于在卷文件中为其保留的空间。实际可用大小由 `getSize` 命令返回。

虽然配置卷旨在防止数据丢失，但仍有两种情况可能导致其中不包含有效数据：卷首次创建时³，或者闪存内容被某些外部物理过程损坏（但愿不太可能）。可以使用 `valid` 命令来检查配置卷是否包含有效数据。
