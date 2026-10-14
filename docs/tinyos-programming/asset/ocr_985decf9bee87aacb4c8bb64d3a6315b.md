the radio's configuration memory, which stores things such as cryptographic keys and the local address (which is used for determining whether to send an acknowledgement). These operations may take a while, so are split-phase. For example, before the stack writes to TXONCCA to send a packet, it must first execute a split-phase write of the packet contents with the CC2420Fifo interface (the receive and transmit buffers are FIFO memories).

All of the operations boil down to four interfaces:

+   - **CC2420Strobe**: Access to a command register. Writing a command register tells the radio to take an action, such as transmit a packet, clear its packet buffers, or transition to transmit mode. This interface has a single command, strobe, which writes to the register.
+   - **CC2420Register**: Access to a data register. These registers can be both read and written, and store things such as hardware configuration, addressing mode, and clear channel assessment thresholds. This interface supports reads and writes as single-phase operations.
+   - **CC2420Ram**: Access to configuration memory. This interface supports both reads and writes, as split-phase operations.
+   - **CC2420Fifo**: Access to the receive and transmit FIFO memory buffers. This interface supports both reads and writes, as split-phase operations. While one can write to the receive buffer, the CC2420 supports this only for debugging purposes.

A component that needs to interact with the CC2420 instantiates an instance of CC2420SpiC:

```
generic configuration CC2420SpiC() {

    provides interface Resource;

    provides interface CC2420Strobe as SPLUSHRX;
    provides interface CC2420Strobe as SPLUSHTX;
    provides interface CC2420Strobe as SNOP;
    provides interface CC2420Strobe as SRXON;
    provides interface CC2420Strobe as SRXFOPF;
    provides interface CC2420Strobe as STXON;
    provides interface CC2420Strobe as STXONCCA;
    provides interface CC2420Strobe as SXOSCON;
    provides interface CC2420Strobe as SXOSCOFF;

    provides interface CC2420Register as FSCTRL;
    provides interface CC2420Register as IOCFG0;
    provides interface CC2420Register as IOCFG1;
    provides interface CC2420Register as MDCTRL0;
    provides interface CC2420Register as MDCTRL1;
    provides interface CC2420Register as TXCTRL;

    provides interface CC2420Ram as IBEEREADR;
    provides interface CC2420Ram as PANID;
```