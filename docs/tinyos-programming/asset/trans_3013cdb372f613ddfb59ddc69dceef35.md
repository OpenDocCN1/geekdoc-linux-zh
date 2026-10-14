

## 7.5.1 可靠传输协议

可靠的消息传输协议非常简单。消息在发送时带有“cookie”（每次传输都会改变），并在超时后重复发送，直到收到带有相同 cookie 的确认。传输不会重叠：message2 的传输在 message1 得到确认之前不会开始。

在接收端，重复消息（通过相同的 cookie 检测到）在传递给上层之前会被抑制。然而，即使是重复的消息也会被确认，因为之前的确认可能丢失了。

具体来说，该协议使用两种数据包：消息传输数据包（reliable_msg_t）和确认数据包（ack_msg_t）。这些数据包在图 7.3 中显示，同时还显示了 ReliableTestSerial 应用传输的 TestSerial 消息。

![](img/53ede4f4266a5731b93bff15d85fa06a_144_0.png)

图 7.3 可靠传输数据包布局。

## 7.5.2 Java 中的可靠传输

ReliableMoteIF 类包含简单可靠消息传输协议的 Java 实现。它使用 mig 生成 AckMsg 和 ReliableMsg，以便分别构建和解码 ack_msg_t 和 reliable_msg_t 数据包。ReliableMoteIF 使用 nec 访问 nesC 实现中指定的重传超时（ACK_MSG_TIMEOUT）（ReliableSerialC 组件）。

该类实现了一个通用可重用层，因此应该能够传输和接收布局由 mig 生成的类指定的任意消息。因此，其接口与 MoteIF 非常相似，我们只需让它成为 MoteIF 的子类。我们首先展示发送端：

```
import net.tinyos.packet.*;
import net.tinyos.message.*;
import java.io.*;
```

```
class ReliableMoteIF extends MoteIF {
    /* Build an object for performing reliable transmission via `base` */
    public ReliableMoteIF(PhoenixSource base) {
        super(base);
        /* Register handler (`ackMsgReceived` method below) for receiving acks */
        super.registerListener(
            (new AckMsg(), new MessageListener() {
                public void messageReceived(int to, Message m) {
                    ackMsgReceived((AckMsg)m);
                }
            })
        );
    }

    /* Send side */
    /* --------- */
    private Object ackLock = new Object(); /* For synchronization with ack handler */
    private short sendCookie = 1; /* Next cookie to use in transmission */
    private boolean acked; /* Set by ack handler when ack received */
    private final static int offsetUserData = ReliableMsg.offset_data();

    /* Send message `m` reliably with destination `to` */
    public void send(int to, Message m) throws IOException {
        synchronized (ackLock) {
            /* Build a reliable_msg_t packet with the current cookie and the payload in m,
             * total packet size is m.dataLength() + offsetUserData */
            ReliableMsg rmsg = new ReliableMsg(m.dataLength() + offsetUserData);
            rmsg.set_cookie(sendCookie);
            System.arraycopy(m.dataGet(), m.baseOffset(),
                             rmsg.dataGet(), offsetUserData,
                             m.dataLength());

            /* Repeatedly transmit `rmsg` until the ack handler tells us an ack is received. */
            acked = false;
            for (;;) {
                super.send(to, rmsg);
                try {
                    ackLock.wait(RelConstants.ACK_TIMEOUT);
                }
                catch (InterruptedException e) {
                    if (acked)
                        break;
                    System.err.printf("retry\n");
                }
            }

            /* Pick a new cookie for the next transmission */
            sendCookie = (short)((sendCookie + 3) & 0xff);
        }
    }
}
```

```
/* Handler for ack messages. If we see an ack for the current transmission,
 * notify the 'send' method. */
void ackMsgReceived(AckMsg m) {
    synchronized (ackLock) {
        if (m.get_cookie() == sendCookie) {
            acked = true;
            ackLock.notify();
        }
    }
}

... receive side ...
}
```

### Listing 7.10 Java 中的可靠传输协议 - 传输

send 方法是同步的，以强制执行在发送下一条消息之前必须先确认一条消息的规则。

此代码依赖于 ackMsgReceived 处理程序在与 send 不同的线程中执行这一事实。发送消息后，send 线程会休眠 ACK_MSG_TIMEOUT 毫秒。当收到确认时，ackMsgReceived 会将 cookie 与正在传输的消息的 cookie 进行比较。如果相等，则将 acked 设置为 true 并唤醒 send 线程。如果在 ACK_MSG_TIMEOUT 毫秒内未收到确认，send 将重新发送消息并再次等待。注意，当 send 未在等待时收到的确认实际上会被忽略，正如它们应该的那样。

传输成功后，send 会选择一个新的 cookie——我们将旧值乘以三，只是为了明确这些 cookie 不是序列号。

将用户消息嵌入到 reliable_msg_t 数据包中只是简单地使用 System.arraycopy 在用户消息和 reliable_msg_t 的 mig 生成类的支持数组之间复制数据。还要注意 mig 生成的 offset_data 方法如何用于查找 reliable_msg_t 中的有效载荷偏移量（参见 offsetUserData 常量）。此代码与 MoteIF 将用户消息嵌入到串行数据包中的代码非常相似。

可靠接收是通过重写 MoteIF.registerListener 实现的。需要注意的是，我们的可靠传输协议只知道一种消息类型（它没有相当于 AM 的 type 字段的字段），因此你实际上只能为一种消息类型注册一个监听器：

```
class ReliableMoteIF extends MoteIF {
    ...
    /* Receive side */
    /* ---------- */
    private Message template;
    private MessageListener listener;
```

