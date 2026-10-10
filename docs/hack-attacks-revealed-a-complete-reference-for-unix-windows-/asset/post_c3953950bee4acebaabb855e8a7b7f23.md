
Type 1 and 2 cabling is used for 16 Mbps data transfer rates. To avoid jitter, a maximum of 180 devices per ring is recommended. The maximum distance between stations and MAU on a single MAU LAN is 300 meters. The maximum advisable distance between stations and MAUs on a multiple MAU LAN is 100 meters. The maximum recommended distance between MAUs on a multiple MAU LAN is 200 meters.

Type 3 cabling is primarily used for 4 Mbps data transfer rates. To avoid jitter, a maximum of 90 devices per ring is recommended. The maximum distance between stations and MAU on a single MAU LAN is 100 meters. The maximum advisable distance between stations and MAUs on a multiple MAU LAN is 45 meters. The maximum recommended distance between MAUs on a multiple MAU LAN is 120 meters.

## Prioritization

In Token Ring, there are two prioritization fields to permit station priority over token utilization: the *priority* and *reservation* fields. Stations with priority equal to or greater than that set in a token can take that token by prioritization. After transmission completion, the priority station must reinstate the previous priority value so normal token passing operation may resume.

> **Hackers that set stations with priority equal to or greater than that in a token can control that token by prioritization.**

## Fault Management

Token Ring employs various methods for detecting and managing faults in a ring. One method includes *active monitor* technology, whereby one station acts as a timing node for transmissions on a ring. Among the active monitor station's responsibilities is the removal of continuously circulating frames from the ring. This is important, as a receiving station may lock up or be rendered temporarily out of service while a passing frame seeks it for processing. As such, the active monitor will remove the frame and generate a new token.

Another fault management mechanism includes station *beaconing*. When a station detects a problem with the network, such as a cable fault, it sends a beacon frame, which generates a failure domain. The domain is defined as the station reporting the error, its nearest neighbor, and everything in between. Stations that fall within the failure domain attempt to electronically reconfigure around the failed area.

> **Beacon generation may render a ring defenseless and can essentially lock up the ring.**

## Addresses, Frame Format

Similar to the three address mechanisms in Ethernet (described earlier in this chapter), Token Ring address types include the following:

- **Individual Address.** Specifies a unique ring station.
- **Group Address.** Specifies a group of destination stations on a ring.
- **All Stations Address.** Specifies all stations as destinations on a ring.

Basically, Token Ring supports two frame types: token frame and data/command frame, as illustrated in Figures 3.8 and 3.9, respectively.

A token frame's fields are defined as follows:

- **Start Delimiter.** Announces the arrival of a token to each station.
- **Access Control.** The prioritization value field.
- **End Delimiter.** Indicates the end of the token or data/command frame.

| Start Delimiter | Access Control | End Delimiter |
|---|---|---|

Figure 3.8 A token frame consists of a Start Delimiter, an Access Control Byte, and an End Delimiter field.

| Start Delimiter | Access Control | Frame Control | Destination Address | Source Address | Data | Frame Check Sequence | End Delimiter | Frame Status |
|---|---|---|---|---|---|---|---|---|

Figure 3.9 A data/command frame consists of the standard fields, including error checking.

A data/command frame's fields are defined as follows:

- **Start Delimiter.** Announces the arrival of a token to each station.
- **Access Control.** The prioritization value field.
- **Frame Control.** Indicates whether data or control information is carried in the frame.
- **Destination Address.** A 6-byte field of the destination node address.
- **Source Address.** A 6-byte field of the source node address.
- **Data.** Contains transmission data to be processed by receiving station.
- **Frame Check Sequence (FCS).** Similar to a CRC (described earlier in this chapter): the source station calculates a value based on the frame contents. The destination station must recalculate the value based on a successful frame transmission. The frame is discarded when the FCS of the source and destination do not match.
- **End Delimiter.** Indicates the end of the token or data/command frame.
- **Frame Status.** A 1-byte field specifying a data frame termination and address-recognized and frame-copied indicators.

## Fiber Distributed Data Interface Technology

The American National Standards Institute (ANSI) developed the Fiber Distributed Data Interface (FDDI) around 1985. FDDI is like a high-speed Token Ring network with redundancy failover using fiber optic cable. FDDI operates at 100 Mbps and is primarily used as a backbone network, connecting several networks together. FDDI utilizes Token Ring *token passing* technology, which, when fully implemented, contains two counter-rotating fiber rings. The primary ring data travels clockwise, and is used for transmission; the secondary ring (traveling counterclockwise) is used for backup failover in case the primary goes down. During a failure, auto-sense technology causes a ring wrap for the transmission to divert to the secondary ring.

![](img/ba85bb40c695c02adae8cbd6666f2e0c_67_0.png)

**Figure 3.10** An FDDI dual ring backbone connecting two local LANs via MAUs and one WAN via a router.

### Operation

FDDI frame sizes may not exceed 4,500 bytes. This makes FDDI a feasible medium for large graphic and data transfers. The maximum length for FDDI is 200 kilometers with 2,000 stations for a single ring, and one-half that for a dual ring implementation. FDDI was designed to function as a high-speed transport backbone; therefore, FDDI assumes workstations will not attach directly to its rings, but to a MAU or router, as they cannot keep up with the data transfer rates (see Figure 3.10). Consequently, frequent station power cycles will cause ring reconfigurations; therefore, it is recommended that directly connected MAUs be powered on at all times.

FDDI rings operate in synchronous and asynchronous modes, which are defined as follows:

- **Synchronous.** Stations are guaranteed a percentage of the total available bandwidth.
- **Asynchronous.** Stations transmit in restricted or nonrestricted conditions. A restricted station can transmit with up to full ring bandwidth for a period of time allocated by station management; as nonrestricted stations, all available bandwidth, minus restrictions, will be distributed among the remaining stations.

Stations can attach to FDDI as single-attached-stations (SAS) or dual-attached-stations (DAS). SAS connect only to the primary ring through a FDDI MAU. The advantage of this method is that a station will not affect the ring if it is powered down. DASs are directly connected to both rings, primary and secondary. If a DAS is disconnected or powered off, it will cause a ring reconfiguration, interrupting transmission performance and data flow.

### FDDI Design, Cabling

FDDI can operate with optical fiber or copper cabling, referred to as Copper Distributed Data Interface (CDDI). FDDI was designed for optical fiber, which has many advantages over copper, including performance, cable distance, reliability, and security.

Two types of FDDI optical fiber are designed to function in modes (defined as rays of light that enter fiber at specific angles): *single-mode* and *multi-mode*. These modes are defined as follows:

- **Single-mode**. One mode of laser light enters the fiber and is capable of giving high performance over long distances. This mode is recommended for connectivity between buildings or widely dispersed networks.
- **Multi-mode**. Multiple modes of LED lights enter the fiber at different angles and arrive at the end of the fiber at different times. Multi-mode reduces bandwidth and potential cable distance and is therefore recommended for connectivity within buildings or between closely dispersed networks.

Fiber does not emit electrical signals and therefore cannot be tapped nor permit unauthorized access.

## Frame Format

Remember that FDDI frames can be up to 4,500 bytes. As stated, this size makes FDDI a feasible medium for large graphic and data transfers. Not surprisingly, Token Ring and FDDI formats are very similar; they both function as token-passing network rings, and therefore contain similar frames, as shown in Figure 3.11, whose fields are defined in the following list:

| Preamble | Start Delimiter | Frame Control | Destination Address | Source Address | Data | Frame Check Sequence | End Delimiter | Frame Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

Figure 3.11 FDDI data frame.

- **Preamble**. A sequence that prepares a station for upcoming frames.
- **Start Delimiter**. Announces the arrival of a token to each station.
- **Frame Control**. Indicates whether data or control information is carried in the frame.
- **Destination Address**. A 6-byte field of the destination node address.
- **Source Address**. A 6-byte field of the source node address.
- **Data**. Contains transmission data to be processed by the receiving station.
- **Frame Check Sequence (FCS)**. Similar to a CRC (described earlier in this chapter): the source station calculates a value based on the frame contents. The destination station must recalculate the value based on a successful frame transmission. The frame is discarded if the FCS of the source and destination do not match.
- **End Delimiter**. Indicates the end of the frame.
- **Frame Status**. Specifies whether an error occurred and whether the receiving station copied the frame.

## Analog Technology

Analog communication has been around for many years, spanning the globe with longer, older cabling and switching equipment. However, the problems inherent to analog communication now seem to be surpassing its effective usefulness. Fortunately, other means of communication now exist to address the complications of analog transmission. Some of the newer engineering is digital and ISDN/xDSL technologies (covered in the next section).

Dial-up analog transmission transpires through a single channel, where the analog signal is created and handled in the electrical circuits. A modem provides communication emulation, in the form of an analog stream on both the dialing and answering networks. Telephone system functionality derives from analog transmissions through equipment switching, to locate the destination and open an active circuit of communication. The cabling, microwaves, switching equipment, and hardware involved in
