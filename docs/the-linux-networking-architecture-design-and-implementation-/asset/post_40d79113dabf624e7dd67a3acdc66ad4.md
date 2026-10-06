
# Chapter 8 The Point-to-Point Protocol (PPP)

is closed again. all subprotocols are notified accordingly by the function pointer close(). For the authentication protocols PAP and CHAP, the value NULL each is entered for open() and close() as callback function.

## 8.4.2 States

The logical logic of subprotocols can be represented elegantly in the form of a finite state machine (FSM). To save cost and avoid errors, the PPP daemon implements a generic FSM, which handles things like state transitions and timers. It is implemented in ppp/fsm.c and primarily takes care that the correct callback functions are invoked at the right time. Examples for subprotocols with an implementation that accesses this generic finite state machine include LCP and IPCP.

PPP itself, and thus the PPP daemon, also know different states: however, these states have little to do with the states of subprotocols. These so-called phases are listed in Table 8–3. The PPP daemon behaves differently, depending on the state. For example, it would be fatal to admit configuration protocols for the network layer, such as IPCP, before a successful authentication.

A callback function can be invoked upon request in each of these state transitions. To this end, the callback function need only be added to the otherwise unused global variable new_phase_hook.

**TABLE 8–3 States (phases) of the PPP daemon.**

| State | Meaning |
|---|---|
| PHASE_INITIALIZE | Initial state: pppd initialization. |
| PHASE_DORMANT | Waiting for activity (for dial-on-demand). |
| PHASE_SERIALCONN | Establish physical connection. |
| PHASE_ESTABLISH | Physical connection is up and running. |
| PHASE_AUTHENTICATE | Authentication in progress. |
| PHASE_CALLBACK | CBCP (see Section 8.2-4) is running. |
| PHASE_NETWORK | Network protocols are being configured. |
| PHASE_RUNNING | Higher layers can start working. |
| PHASE_TERMINATE | LCP requested connection to be torn down. |
| PHASE_DISCONNECT | Program to tear down connection has started. |
| PHASE_HOLDOFF | Wait a little before the next connection is established. |
| PHASE_DEAD | Connection was interrupted |

# CHAPTER 9
PPP over Ethernet

## 9.1 INTRODUCTION
Chapter 8 introduced the Point-to-Point protocol (PPP). Today, it is most frequently used in access networks that use ADSL as the access technology.

The ADSL (Asymmetric Digital Subscriber Line) access technology offers high-speed Internet access for private or commercial customers. From the technical view-point, this is a dedicated line (i.e., a permanent connection). Dedicated lines are normally billed on basis of transmission volumes. In contrast, private Internet links are billed on a time basis. To enable ADSL to support time-specific billing as well, a new protocol, PPPoE, was developed. PPPoE is based on two accepted standards—PPP and Ethernet.

More specifically, an ADSL modem (NTBBA—Network Termination Point Broad-Band Access), installed behind a so-called splitter, is connected to the computer over Ethernet. This means the computer has to be equipped with an Ethernet network card. This dedicated Ethernet line between the PC of the home user and the dialup computer of the access network operator is used to establish a PPP connection, which allows the access network operator to identify the user and bill for the time between the PPP dialup and the termination of that PPP session. The PPP connection can be used to exchange IP packets.

Figure 9–1 shows the resulting protocol stack. This first chapter introduces the PPPoE (PPP over Ethernet) protocol described in [MLEC+99]. Then, it introduces the implementation in the user space, which is used in kernel Versions 2.2 and 2.3. Finally, this chapter discusses the implementation in the kernel from kernel version 2.4 and up.

## 9.2 PPPoE SPECIFICATION IN RFC 2516

To be able to transport PPP protocol units over Ethernet, they are inserted as payload in Ethernet frames. For this purpose, two newertype values were defined, which show the receiver that the Ethernet frame contains PPP payload.

![](img/5a25b942ec3329b8799f2b5f0de564f6_185_0.png)
FIGURE 9–1 Protocol stack for the use of PPP over Ethernet.

![](img/5a25b942ec3329b8799f2b5f0de564f6_185_1.png)
FIGURE 9–2 Typical sequence for PPPoE Active Discovery.

The two different types serve to distinguish between two phases within PPPoE: the discovery stage, and the session stage. A typical discovery stage consists of four steps, which appear as follows (Figure 9–2): The host sends a PADI (PPPoE Active Discovery Initiation) packet to the Ethernet broadcast address to find out which access concentrators are available in the Ethernet. One (or several) of these access concentrators replies by sending a PADO (PPPoE Active Discovery Offer) packet, informing the host about the Ethernet address where an access concentrator is available, the host selects one from the available access concentrators and requests that this concentrator establish a connection by sending a PADI*.

(PPPoE Active Discovery Request) packet. The access concentrator replies by sending a PADS (PPPoE Active Discovery Session Confirmation).
Subsequently, the discovery stage is left behind and the session stage begins, where PPP payload is packed transparently in Ethernet frames having ethertype value 0x8864 (in contrast to packets in the discovery stage, which have ethertype value 0x8863). Figure 9–3 shows what a PPPoE packet looks like in the session stage. The underlying Ethernet already forms frames, so PPPoE does not require character stuffing, in contrast to the asynchronous case described in Chapter 8.

The PPP protocol should generally initiate a PPPoE connection to be torn down, but there is also a PADT (PPPoE Active Discovery Terminate) packet, which can be used to terminate a PPPoE connection. When a PADT packet has been sent or received.

## 9.3 Implementation in the User Space

| Client's Ethernet address | Access server's Ethernet address |
|---|---|
| Client's Ethernet address | Access server's Ethernet address |
| Ethertype = 0x8864 | Various flags |
| Session ID | Length |
| PPP protocol data unit | |
| Ethernet frame-check sequence | |

FIGURE 9–3
Protocol data unit of the PPPoE session stage.

![](img/5a25b942ec3329b8799f2b5f0de564f6_186_0.png)
FIGURE 9–4
pppd and ppppoed communicate in the user space.

The kernels of 2.2 and 2.3 do not support PPPoE. Instead, another daemon is started in the user space, in addition to pppd. This daemon is called ppped; it processes packets and forwards them to pppd.

There are various implementations in the user space, including the Roaring implementation [Roar0], which appears to be the most elaborate. The major drawback of this approach and similar approaches is that the pseudo-terminal requires an additional transition between the kernel and the user space, which reduces the performance. For this reason, we will consider only the kernel implementation.

## 9.4 Implementation in the Kernel

Together with kernel Version 2.4, PPPoE support was integrated into the pppd daemon, and the kernel was expanded by a connection between the generic PPP driver and the Ethernet network.

Figure 9–5 shows the interaction between these components. The PPPoE driver assumes various functions within the. To the lower layer (i.e., the Ethernet card and the driver software), the PPPoE driver plays the role of a layer-3 protocol. As we will see later in more detail, Incoming Ethernet packets are allocated to a protocol matching the type identifier in the Ethernet frame (e.g., the IP protocol or the PPPoE protocol for the ethertype value 0x8863 and 0x8864 mentioned earlier). Towards the higher-layer generic PPP driver, which was described in the previous chapter, the PPPoE driver behaves as much as the asynchronous PPP driver. In contrast to that driver, the PPPoE driver does not implement a tty operating mode.

To initiate the PPPoE discovery stage of pppd in the user space, it is additionally necessary to have the PPPoE driver and pppd communicate directly. Section 9.4.2 discusses this communication in detail.

### 9.4.1 Changes to the Kernel

The PPPoE driver, which is included in the kernel Version 2.4 and higher in experimental form, consists of the file drivers/net/pppoe.c. In addition, there is a file called drivers/net/pppox.c, which is intended to harmonize present and future PPP implementations in the kernel. General functions that previously were used only by

![](img/5a25b942ec3329b8799f2b5f0de564f6_187_0.png)
FIGURE 9–5
Communication between pppd and the PPP and PPPoE drivers.
