
## Operation, Devices, Data-Link Connection Identifiers, and Virtual Circuits

Devices that participate in a Frame Relay WAN include data terminal equipment (DTE) and data circuit-terminating equipment (DCE). Customer-owned equipment such as routers and network stations are examples of DTE devices. Provider-owned equipment provides switching and clocking services, and is contained in the DCE device category. Figure 3.16 illustrates an example of a Frame Relay WAN.

Data-link communication between devices is connected with an identifier and implemented as a Frame Relay *virtual circuit*. A virtual circuit is defined as the logical connection between two DTE devices through a Frame Relay WAN. These circuits support bidirectional communication; the identifiers from one end to another are termed *data-link connection identifiers* (DLCIs). Each frame that passes through a Frame Relay WAN contains the unique numbers that identify the owners of the virtual circuit to be routed to the proper destinations. Virtual circuits can pass through any number of DCE devices. As a result, there are many paths between a sending and receiving device over Frame Relay. For the purposes of this overview, Figure 3.16 illustrates only three packet switches within the Frame Relay WAN. In practice, there may be 10 or 20 routers assimilating a multitude of potential courses from one end to another.

There are two types of virtual circuits in Frame Relay, *switched virtual circuits* (SVCs) and *permanent virtual circuits* (PVCs), defined as follows:

![](img/ba85bb40c695c02adae8cbd6666f2e0c_75_0.png)

Figure 3.16 Frame Relay WAN.

- **Switched Virtual Circuits (SVCs).** Periodic, temporary communication sessions for infrequent data transfers. A SVC connection requires four steps:
    - Call setup between DTE devices.
    - Data transfer over temporary virtual circuit.
    - Defined idle period before termination.
    - Switched virtual circuit termination.

SVCs can be compared to ISDN communication sessions, and as such, use the same signaling protocols.

- **Permanent Virtual Circuits (PVCs)**. Permanent communication sessions for frequent data transfers between DTE devices over Frame Relay. A PVC connection requires only two steps:
    1. Data transfer over permanent virtual circuit.
    2. Idle period between data transfer sessions.

PVCs are currently the more popular communication connections in Frame Relay WANs.

### Congestion Notification and Error Checking

Frame Relay employs two mechanisms for congestion notification: *forward-explicit congestion notification* (FECN) and *backward-explicit congestion notification* (BECN). From a single bit in a Frame Relay header, FECN and BECN help control bandwidth degradation by reporting congestion areas. As data transfers from one DTE device to another, and congestion is experienced, a DCE device such as a switch, will set the FECN bit to 1. Upon arrival, the destination DTE device will be notified of congestion, and process this information to higher-level protocols to initiate flow control. If the data sent back to the originating sending device contains a BECN bit, notification is sent that a particular path through the network is congested.

During the data transfer process from source to destination, Frame Relay utilizes the common cyclic redundancy check (CRC) mechanism to verify data integrity, as explained in the Ethernet section earlier in this chapter.

### Local Management Interface

The main function of Frame Relay’s local management interface (LMI) is to manage DLCIs. As DTE devices poll the network, LMI reports when a PVC is active or inactive. When a DTE device becomes active in a Frame Relay WAN, LMI determines which DLCIs available to the DTE device are active. LMI status messages, between DTE and DCE devices, provide the necessary synchronization for communication.

The LMI frame format consists of nine fields as illustrated in Figure 3.17, and defined in the following list:

- **Flag.** Specifies the beginning of the frame.
- **LMI DLCI.** Specifies that the frame is a LMI frame, rather than a standard Frame Relay frame.
- **Unnumbered Information Indicator (UII).** Sets the poll bit to 0.

| Flag | LMI DLCI | UII | PD | Call Reference | Message Type | VIE | FCS | Flag |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| | | | | | | | | |

**Figure 3.17** Local Management Interface frame format.

| Flag | Address | Data | FCS | Flag |
|---|---|---|---|---|
| | | | | |

Figure 3.18 Frame Relay frame format.

- **Protocol Discriminator (PD).** Always includes a value, marking frame as an LMI frame.
- **Call Reference.** Contains zeros, as field is not used at this time.
- **Message Type.** Specifies the following message types:
    - Status-inquiry message. Allows devices to request a status.
    - Status message. Supplies response to status-inquiry message.
- **Variable Information Elements (VIE).** Specifies two individual information elements:
    - IE identifier. Identifies information element (IE).
    - IE length. Specifies the length of the IE.
- **Frame Check Sequence (FCS).** Verifies data integrity.
- **Flag.** Specifies the end of the frame.

## Frame Relay Frame Format

The following descriptions explain the standard Frame Relay frame format and the fields therein (shown in Figure 3.18):

- Flag. Specifies the beginning of the frame.
- Address. Specifies the 10-bit DLCI value, 3-bit congestion control notification, and FECN and BECN bits.
- Data. Contains encapsulated upper-layer data.
- Frame Check Sequence (FCS). Verifies data integrity.
- Flag. Specifies the end of the frame.

## Looking Ahead

The primers in Parts 1 and 2 were designed to renovate and/or educate you with the technologies required to delve into hacking. First, let us review in some detail, the tools, techniques, and vulnerability exploits ruling hackerdom. The knowledge gained from the next part involves query processes by which to discover and survey a target network, and to prepare for vulnerability scanning and penetration attacking.

## PART Three

Uncovering Vulnerabilities

### A Little Terminology

#### Who Are Hackers, Cracker s, Phreak s, and Cyberpunk s?

Our first “intermission” begins by taking time out to define the terms *hacker*, *cracker*, *phreak*, and *cyberpunk*. This is necessary, because they are often used interchangeably; for example, a hacker could also be a cracker; a phreak may use hacking techniques; and so on. To help pinpoint the specifics of each of these, let’s define how they’re related:

- A *hacker* is typically a person who is totally immersed in computer technology and computer programming, someone who likes to examine the code of operating systems and other programs to see how they work. This individual then uses his or her computer expertise for illicit purposes such as gaining access to computer systems without permission and tampering with programs and data on those systems. At that point, this individual would steal information, carry out corporate espionage, and install backdoors, virii, and Trojans.
- A *cracker* is a person who circumvents or defeats the security measures of a network or particular computer system to gain unauthorized access. The classic goal of a cracker is to obtain information illegally from a computer system to use computer resources illegally. Nevertheless, the main goal of the majority is to merely break into the system.
- A *phreak* is a person who breaks into telephone networks or other secured telecommunication systems. For example, in the 1970s, the telephone system used audible tones at switching signals; phone phreaks used their own custom-built hardware to match the tones to steal long-distance services. Despite the sophisticated security barriers used by most providers today, service itself such as this is quite common globally.
- The *cyberpunk* can be considered a recent mutation that combines the characteristics of the hacker, cracker, and phreak. A very dangerous combination indeed.

It has become an undeniable reality that to successfully prevent being hacked, one must think like a hacker, function like a hacker, and, therefore, become a hacker.

**NOTE** Acknowledging participation from legendary hacker *Shadowlord* and various members of the Underground hacker community, who wish to remain anonymous, the remainder of this intermission will address hacking background, hacker style, and the portrait of a hacker.

### What Is Hacking?

Hacking might be exemplified as inappropriate applications of ingenuity; and whether the result is a practical joke, a quick vulnerability exploit, or a carefully crafted security breach, one has to admire the technological expertise that was applied.

**NOTE** For the purpose of conciseness, this section treats as a single entity the characteristics of hackers, crackers, and phreaks.

Perhaps the best description of hacking, however, is attributed to John Vranesevich, founder of AntiOnline (an online security Web site with a close eye on hacker activity). He called hacking the
