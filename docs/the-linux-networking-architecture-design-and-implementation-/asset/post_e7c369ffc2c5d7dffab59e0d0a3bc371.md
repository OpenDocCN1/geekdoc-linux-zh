
# Chapter 10 Asynchronous Transfer Mode—ATM

![](img/5a25b942ec3329b8799f2b5f0de564f6_197_0.png)

FIGURE 10–4
SVC support in Linux.

Requests to establish or tear down connections and other tasks pertaining to connection management are handled by the signaling daemon, atmsigd. More specifically, all corresponding requests, which can originate both from applications and from the network, are forwarded to the signaling daemon. Requests are put asynchronously into a message queue, from which the signaling daemon fetches messages. In most cases, the kernel performs a synchronous (i.e., blocking) wait for the daemon's response.

Many of the functions available in the file net/atm/svc.c correspond to the previously introduced functions in net/atm/pvc.c so we will not describe them here in detail. For example, as with the function pvc_create(), the function svc_create() is initially used to announce operations that belong to the protocol family PF_ATMSVC and should be made available over the socket. Subsequently, atm_create(protocol, PF_ATMSVC) creates a new socket.

### svc_bind() net/atm/svc.c

The function svc_bind(), which is normally invoked at this point of the procedure, serves as an example for the communication between the kernel and the signaling daemon. The following code fragment was taken from the source code:

```
sigd_enq(vcc, as_bind, NULL, NULL, &vcc->sleep);
add_wait_queue(vcc->sleep,wait);
while (vcc->reply == WAITING && sigd) {
  set_current_state(TASK_UNINTERRUPTIBLE);
  schedule();
}
remove_wait_queue(vcc->sleep,wait);

return vcc->reply;
```

## 10.2 Implementing ATM in Linux

First, the function sigd_enq() for the input queue of the signaling daemon, defined in net/atm/signaling.c, is passed the message type as_bind, together with a pointer to the structure as_vcc, which belongs to the connection. Subsequently, the relevant process remains in the TASK_UNINTERRUPTABLE state until the signaling daemon has fetched the message from the input queue and changed the field vcc->reply from WAITING to another value (say, 0) when the action was successful. This value is returned to the function svc_bind().

The full set of messages that can be exchanged between the kernel and the signaling daemon is specified in the atmsvc_msg_type structure, stored in the file include:/linux/atmsvc.h:

```
enum atmsvc_msg_type {
    as_catch_null, as_bind, as_connect, as_accept, as_reject,
    as_listen, as_okay, as_error, as_indicate, as_close, as_itf_notify,
    as_modify, as_identify, as_terminate };
```

The following message types are used for connection control:

- as_okay: The signaling daemon acknowledges a previous message.
- as_error: The signaling daemon reports an error.
- as_close: The kernel informs the daemon that a connection is to be closed.
- as_bind: The kernel sends this message to obtain a local address.
- as_connect: The kernel sends a request to establish a connection to the signaling daemon.
- as_listen: The kernel uses this message to notify that an endpoint was opened, where it will wait for a connection-establishment request.
- as_indicate: The kernel informs the signaling daemon that a connection-establishment request has arrived.
- as_accept: The kernel notifies the signaling daemon that it wants to accept a connection.
- as_reject: The kernel informs the signaling daemon that an incoming connection-establishment request was rejected.

The parameters for these message types are specified in the structure atmsvc_msg in the file include/linux/atmsvc.h. They include addresses and QoS parameters for SVC connections.

### 10.2.3 ATM Device Drivers

In contrast to Ethernet network cards, ATM network cards handle a large part of the protocol-processing work them. Normally, an ATM network card is responsible not only for forming ATM cells, but also for composing these cells into protocol units for the higher ATM adaptation layer (AAL). This means that the system is relieved from these tasks. On the other hand, it means that ATM network cards are more expensive, because the hardware is more costly.

For ATM device drivers, we distinguish between one part that manages the physical layer (PHY driver) and another part that manages resources and coordinates the protocol and handlers.

parameters:

```
struct atm_dev {
    const struct atmdev_ops *ops; /* device operations; NULL if used */
    const struct atmphy_ops *phy; /* PHY operations, may be undefined */
                                /* (NULL) */
    const char *type; /* device type name */
    int number; /* device index */
    struct atm_vcc *vccs; /* VCC table (or NULL) */
    struct atm_vcc *last; /* last VCC (or undefined) */
    void *dev_data; /* per-device data */
    void *phy_data; /* private PHY data */
    struct atm_dev_flags_t flags; /* device flags (ATM_DF*) */
    struct atm_dev_addr *local; /* local ATM addresses */
    unsigned char esi[ESI_LEN]; /* ESI ("MAC") */
    struct ci_range ci_range; /* VPI/VCI */
    struct atm_dev_stats *stats; /* statistics */
    char *signal; /* signal status */
    int link_rate; /* link rate */
#ifdef CONFIG_PROC_FS
    struct proc_dir_entry *proc_entry; /* proc entry */
    char *proc_name; /* proc name */
#endif
    struct atm_dev *prev, *next; /* linkage */
};
```

These structures are linked in a list by the pointers prev and next. The structure serves as an interface between the kernel and the driver; this is where all parameters required by the driver are made available, plus that the driver point to the operations supplied by the driver over the structure atmdev_ops and to the PHY driver operations, which are. (Both structures are also defined in include/atmdev.h.)

The most important operations available from the structure atmdev_ops are:

- open(c): reserves resources on the hardware for a new connection: the VPI and the VCI for the connection are passed to the driver.
- ioctl(): is used to pass it(c) commands to the driver. If the driver does not know these commands, it forwards them to the PHY driver.
- send(c): passes data for transmission.
- phy_put() and phy_get(): are used by the PHY driver to write a byte to or read one from a hardware register of the network card.

### 10.2.4 Further ATM Support

The support of "pure" ATM described above (i.e., the support of applications that ATM sockets directly) was extended by the support of protocols, which convert IP packets to ATM, in a very early stage. This support includes the following protocols:

- Classical IP: Classical IP [Laub94] is the simplest form for transporting IP data over ATM traffic. The functions included in net/atm/clip.c are used to support Classical IP.
- LAN Emulation: LAN Emulation [Foru95] represents a second approach to IP over ATM, which in contrast to Classical IP, uses signaled virtual connections rather than permanent virtual connections. The Linux kernel includes functions for this emulation in the file net/atm/lec.c.
- MPOA: The abbreviation "MPOA" [Hein93] stands for "Multiple Protocols over ATM" and represents a more recent approach for the support of IP over ATM. The Linux kernel includes functions for MPOA in the files net/atm/mpc.c, mpoa_caches.c, and net/atm/mpoa_proc.c for corresponding entries in the proc directory.

The functions used by all of these approaches are grouped in net/atm/ipcommon.c.

## 10 CONFIGURATION

ATM support has been part of the Linux kernel since kernel Version 2.4 and requires no additional patches; however, configuring of the kernel requires the entry "Prompt
