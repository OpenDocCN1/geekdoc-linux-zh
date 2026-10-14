
## 7.5.1 Reliable transmission protocol

The reliable message transmission protocol is very simple. Messages are sent with a “cookie” (changed on every transmission) and are repeatedly sent (after a timeout) until an acknowledgement with the same cookie is received. Transmissions are not overlapped: transmission of message2 does not start until message1 has been acknowledged.

On the reception side, duplicates (detected by the presence of an identical cookie) are suppressed before passing the message on to the upper layer. However, even duplicate messages are acknowledged, as it is possible that the earlier acknowledgements were lost.

In concrete terms, two kinds of packets are used by this protocol: a message transmission packet (reliable_msg_t) and an acknowledgement packet (ack_msg_t). These packets are shown in Figure 7.3, along with the TestSerial messages that are transmitted by the ReliableTestSerial application.

![](img/53ede4f4266a5731b93bff15d85fa06a_144_0.png)

Figure 7.3 Reliable transmission packet layouts.

## 7.5.2 Reliable transmission in Java

The ReliableMoteIF class contains the Java implementation of the simple reliable message transmission protocol. It uses mig to generate AckMsg and ReliableMsg so that it can build and decode ack_msg_t and reliable_msg_t packets respectively. ReliableMoteIF uses nec to access the retransmission timeout (ACK_MSG_TIMEOUT) specified in the nesC implementation (the ReliableSerialC component).

This class is implementing a generic reusable layer, so should be capable of transmitting and receiving an arbitrary message whose layout is specified by a mig-generated class. As a result, the interface is so similar to that of MoteIF that we simply make it a subclass of MoteIF. We first show the transmission side:

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

### Listing 7.10 Reliable transmission protocol in Java - transmission

The send method is synchronized to enforce the rule that a message must be acknowledged before the next message is sent.

This code relies on the fact that the ackMsgReceived handler executes in a different thread than send. After sending a message, the send thread goes to sleep for ACK_MSG_TIMEOUT ms. When an acknowledgement is received, ackMsgReceived checks the cookie against that of the message being transmitted. If it is equal, acked is set to true and the send thread is woken up. If no acknowledgement is received within ACK_MSG_TIMEOUT ms, send will resend the message and wait again. Note that acknowledgements received when send is not waiting are effectively ignored, as they should be.

After transmission is successful, send picks a new cookie – we multiply the old value by three just to make it clear that these cookies are not sequence numbers.

The embedding of the user’s message in a reliable_msg_t packet is simply done by using System.arraycopy to copy data between the backing arrays of the user’s and reliable_msg_t’s mig-generated classes. Note also how the mig-generated offset_data method is used to find the payload offset in reliable_msg_t (see the offsetUserData constant). This code is very similar to MoteIF’s embedding of user messages in serial packets.

Reliable reception is implemented by overriding MoteIF.registerListener. Note, however, that our reliable transmission protocol only knows about one message type (it has no equivalent to AM’s type field), so you can only actually register a listener for one message type:

```
class ReliableMoteIF extends MoteIF {
    ...
    /* Receive side */
    /* ---------- */
    private Message template;
    private MessageListener listener;
```
