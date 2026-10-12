Line 187: broadcast a request for the list of **UIT**'s browsers. This is sent to **UIT<1d>**, i.e. to domain **UIT**'s segment master browser

Line 188: AliceNT looks for domain **UIT**'s domain master browser (but no reply was ever received, for reasons unknown)

Line 191: 212.140.133.7 **UIT**'s PDC and therefore domMB replies to line 187's request with a list of browse servers

Lines 192–193: AliceNT chooses one server name (**TECHPC** in this case) from the list of servers she has just received, and resolves its name to an IP number. Then ...

Lines 194–203: she establishes a NetBIOS session (NBSS) connection to the chosen browse server (**TECHPC**, 212.140.133.7)

Lines 204–205: AliceNT finally asks for the browse list (of servers in domain **UIT**) and receives the information in reply.

| No | Source | Destination | Protocol | Info |
| :--- | :--- | :--- | :--- | :--- |
| 184 | 212.140.133.35 | 212.140.133.13 | LANNMAN | NetServerEnum\ Request |
| 185 | 212.140.133.13 | 212.140.133.35 | LANNMAN | NetServerEnum\ Response |
| 187 | 212.140.133.35 | 212.140.133.127 | BROWSER | Get Backup List Request |
| 188 | 212.140.133.35 | 212.140.133.127 | NBNS | Name query NB **UIT** |
| 191 | 212.140.133.7 | 212.140.133.35 | BROWSER | Get Backup List Response |
| 192 | 212.140.133.35 | 212.140.133.127 | NBNS | Name query NB **TECHPC** |
| 193 | 212.140.133.7 | 212.140.133.35 | NBNS | Name response NB 212.140.133.7 |
| 194 | 212.140.133.35 | 212.140.133.7 | TCP | 1035 > 139 [SYN] Seq=64244 Ack=0 |
| 195 | 212.140.133.7 | 212.140.133.35 | TCP | 139 > 1035 [SYN, ACK] Seq=28887888 |
| 196 | 212.140.133.35 | 212.140.133.7 | TCP | 1035 > 139 [ACK] Seq=64245 Ack=2888788 |
| 197 | 212.140.133.35 | 212.140.133.7 | NBSS | Session request |
| 198 | 212.140.133.7 | 212.140.133.35 | NBSS | Positive session response |
| 199 | 212.140.133.35 | 212.140.133.7 | SMB | SMBnegprot Request |
| 200 | 212.140.133.7 | 212.140.133.35 | SMB | SMBnegprot Response |
| 201 | 212.140.133.35 | 212.140.133.7 | SMB | SMBsessionux Request |
| 203 | 212.140.133.35 | 212.140.133.7 | SMB | SMBsessionux Response |
| 204 | 212.140.133.35 | 212.140.133.7 | LANNMAN | NetServerEnum\ Request |
| 205 | 212.140.133.7 | 212.140.133.35 | LANNMAN | NetServerEnum\ Response |

```
⊕ Frame 185 (170 on wire, 170 captured)
⊕ Ethernet II
⊕ Internet Protocol
⊕ Transmission Control Protocol, Src Port: 139 (139), Dst Port: 1034 (1034), Seq: 11957506
⊕ NetBIOS Session Service
⊕ Server Message Block Protocol
⊕ Microsoft Windows LanMan Protocol
Function Code: NetServerEnum
Status: 0
Convert: 0
Entry Count: 3
Available Entries: 3
⊕ Servers
⊕ Server TEST-NTD
⊕ Server **UIT**
```

**Figure 21.7** *ethereal* trace: *net view /domain* and *net view /domain:uit*