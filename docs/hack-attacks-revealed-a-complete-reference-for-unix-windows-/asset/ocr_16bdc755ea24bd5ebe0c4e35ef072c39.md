| Message Type | Description |
| :---: | :---: |
| 0 | Echo Reply |
| 3 | Destination Unreachable |
| 4 | Source Quench |
| 5 | Route Redirect |
| 8 | Echo Request |
| 11 | Datagram Time Exceeded |
| 12 | Datagram Parameter Problem |
| 13 | Timestamp Request |
| 14 | Timestamp Reply |
| 15 | Information Request |
| 16 | Information Reply |
| 17 | Address Mask Request |
| 18 | Address Mask Reply |

**Figure 1.21**  ICMP message chart.

# **ICMP Messages, Subnet Mask Retrieval**

There are many types of useful ICMP messages; Figure 1.21 contains a list of several, which are described in the following list.

+   * **Echo Reply (Type 0)/Echo Request (Type 8). The basic mechanism for testing possible communication between two nodes. The receiving station, if available, is asked to reply to the ping. An example of a ping is as follows:**

STEP 1: BEGIN ECHO REQUEST

```
Ping 206.0.125.81 (at the command prompt)
```

STEP 2: BEGIN ECHO REPLY

```
Reply from 206.0.125.81: bytes=32 time<10ms TTL=128 (from receiving station 206.0.125.81)
```

```
Reply from 206.0.125.81: bytes=32 time<10ms TTL=128
```

```
Reply from 206.0.125.81: bytes=32 time<10ms TTL=128
```

```
Reply from 206.0.125.81: bytes=32 time<10ms TTL=128
```

+   **Destination Unreachable (Type 3). There are several issuances for this message type, including when a router or gateway does not know how to reach the destination, when a protocol or application is not active, when a datagram specifies an unstable route, or when a router must fragment the size of a datagram and cannot because the Don't Fragment Flag is set. An example of a Type 3 message is as follows:**

STEP 1: BEGIN ECHO REQUEST

```
Ping 206.0.125.81 (at the command prompt)
```

STEP 2: BEGIN ECHO REPLY

```
Pinging 206.0.125.81 with 32 bytes of data:
```

```
Destination host unreachable.
```