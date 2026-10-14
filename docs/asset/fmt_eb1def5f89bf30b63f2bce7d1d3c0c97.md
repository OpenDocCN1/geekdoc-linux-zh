
#### Listing 7.10 Java 中的可靠传输协议 - 传输

`send` 方法是同步的，以强制执行在发送下一条消息之前必须先确认一条消息的规则。

此代码依赖于 `ackMsgReceived` 处理程序在与 `send` 不同的线程中执行这一事实。发送消息后，`send` 线程会休眠 `ACK_MSG_TIMEOUT` 毫秒。当收到确认时，`ackMsgReceived` 会将 cookie 与正在传输的消息的 cookie 进行比较。如果相等，则将 `acked` 设置为 `true` 并唤醒 `send` 线程。如果在 `ACK_MSG_TIMEOUT` 毫秒内未收到确认，`send` 将重新发送消息并再次等待。注意，当 `send` 未在等待时收到的确认实际上会被忽略，正如它们应该的那样。

传输成功后，`send` 会选择一个新的 cookie——我们将旧值乘以三，只是为了明确这些 cookie 不是序列号。

将用户消息嵌入到 `reliable_msg_t` 数据包中只是简单地使用 `System.arraycopy` 在用户消息和 `reliable_msg_t` 的 mig 生成类的支持数组之间复制数据。还要注意 mig 生成的 `offset_data` 方法如何用于查找 `reliable_msg_t` 中的有效载荷偏移量（参见 `offsetUserData` 常量）。此代码与 `MoteIF` 将用户消息嵌入到串行数据包中的代码非常相似。

可靠接收是通过重写 `MoteIF.registerListener` 实现的。需要注意的是，我们的可靠传输协议只知道一种消息类型（它没有相当于 AM 的 type 字段的字段），因此你实际上只能为一种消息类型注册一个监听器：

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

```
class ReliableMoteIF extends MoteIF {
    ...
    /* Receive side */
    /* ---------- */
    private Message template;
    private MessageListener listener;
```

/* Build a reliable receive handler for 'template' messages */

public void registerListener(Message m, MessageListener l) {

    template = m;

    listener = l;

    /* Register handler (reliableMsgReceived method below) for receiving

     * reliable_msg_t messages */

    super.registerListener

    (new ReliableMsg(),

     new MessageListener() {

        public void messageReceived(int to, Message m) {

            reliableMsgReceived(to, (ReliableMsg)m);

        }

    });

}

private short recvCookie; /* Cookie of last received message */

void reliableMsgReceived(int to, ReliableMsg rmsg) {

    /* Acknowledge all received messages */

    AckMsg ack = new AckMsg();
