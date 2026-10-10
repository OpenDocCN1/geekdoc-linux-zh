+   * **Single-mode**. One mode of laser light enters the fiber and is capable of giving high performance over long distances. This mode is recommended for connectivity between buildings or widely dispersed networks.
+   * **Multi-mode**. Multiple modes of LED lights enter the fiber at different angles and arrive at the end of the fiber at different times. Multi-mode reduces bandwidth and potential cable distance and is therefore recommended for connectivity within buildings or between closely dispersed networks.

Fiber does not emit electrical signals and therefore cannot be tapped nor permit unauthorized access.

# Frame Format

Remember that FDDI frames can be up to 4,500 bytes. As stated, this size makes FDDI a feasible medium for large graphic and data transfers. Not surprisingly, Token Ring and FDDI formats are very similar; they both function as token-passing network rings, and therefore contain similar frames, as shown in Figure 3.11, whose fields are defined in the following list:

| Preamble | Start Delimiter | Frame Control | Destination Address | Source Address | Data | Frame Check Sequence | End Delimiter | Frame Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |

Figure 3.11 FDDI data frame.

+   * **Preamble**. A sequence that prepares a station for upcoming frames.
+   * **Start Delimiter**. Announces the arrival of a token to each station.
+   * **Frame Control**. Indicates whether data or control information is carried in the frame.
+   * **Destination Address**. A 6-byte field of the destination node address.
+   * **Source Address**. A 6-byte field of the source node address.
+   * **Data**. Contains transmission data to be processed by the receiving station.
+   * **Frame Check Sequence (FCS)**. Similar to a CRC (described earlier in this chapter): the source station calculates a value based on the frame contents. The destination station must recalculate the value based on a successful frame transmission. The frame is discarded if the FCS of the source and destination do not match.
+   * **End Delimiter**. Indicates the end of the frame.
+   * **Frame Status**. Specifies whether an error occurred and whether the receiving station copied the frame.

# Analog Technology

Analog communication has been around for many years, spanning the globe with longer, older cabling and switching equipment. However, the problems inherent to analog communication now seem to be surpassing its effective usefulness. Fortunately, other means of communication now exist to address the complications of analog transmission. Some of the newer engineering is digital and ISDN/xDSL technologies (covered in the next section).

Dial-up analog transmission transpires through a single channel, where the analog signal is created and handled in the electrical circuits. A modem provides communication emulation, in the form of an analog stream on both the dialing and answering networks. Telephone system functionality derives from analog transmissions through equipment switching, to locate the destination and open an active circuit of communication. The cabling, microwaves, switching equipment, and hardware involved in