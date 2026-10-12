| Pr Src \ Other Addr Dst \ Other Addr Proto. Description |
| 66 212.140.133.35 212.140.133.7 NBT NS: Query req. for BOBNT |
| 67 212.140.133.7 212.140.133.35 NBT NS: Query (Node Status) resp. for BOBNT |
| 69 \_ARP: Request, Target IP: 212.140.133.31 |
| 69 \_ARP: Reply, Target IP: 212.140.133.35 TAI |
| 70 212.140.133.35 212.140.133.31 TCP ...s.: len: 4, seq: 56794-56795 |
| 71 212.140.133.31 212.140.133.35 TCP ...s.: len: 4, seq: 56931-56934, ack: 56795, win: 7810, src: 1... |
| 72 212.140.133.35 212.140.133.31 TCP 0, seq: 56785-56785 |
| 73 212.140.133.35 212.140.133.31 NBT SS: Session Request, Dest: BOBNT |
| 74 212.140.133.35 212.140.133.35 NBT SS: Positive Session Response, Len: 0 |
| 75 212.140.133.35 212.140.133.31 SMB C negotiate, Dialect = 3 |
| 76 212.140.133.31 212.140.133.35 SMB R negotiate, Dialect # = 7 |
| 77 212.140.133.31 212.140.133.35 SMB C session setup 4 X, Username = adminis... |
| 79 \_ARP: Request, Target IP: 212.140.133.13 |
| 79 \_ARP: Reply, Target IP: 212.140.133.31 Tai |
| 80 212.140.133.31 212.140.133.13 NBT SS: Create 4 X, File = \\BETHOUG |
| 81 212.140.133.13 212.140.133.13 SMB R NT create 4 X, Fid = 0x1009 |
| 82 212.140.133.13 212.140.133.13 MSSRPC c/o RPC Bind: UUID 12345678-1234-...
| 83 212.140.133.13 212.140.133.13 MSSRPC c/o RPC Bind Ack: call Orl assoc gr |
| 84 212.140.133.31 212.140.133.13 MSSRPC c/o RPC Response: call Orl context 0 |
| 85 212.140.133.31 212.140.133.31 MSSRPC c/o RPC Response: call Orl context C |
| 86 212.140.133.31 212.140.133.35 SMB R session setup 4 X, and R tree connect 4 |
| 87 212.140.133.35 212.140.133.31 SMB C NT create 4 X, File = \\usrvss |
| 88 212.140.133.31 212.140.133.13 SMB R NT create 4 X, File = 0x000 |
| 89 212.140.133.35 212.140.133.31 MSSRPC c/o RPC Bind: UUID 48324afc5-1670-... |
| 90 212.140.133.31 212.140.133.13 MSSRPC c/o RPC Bind Ack: call Orl assoc gr |
| 91 212.140.133.31 212.140.133.13 MSSRPC c/o RPC Response: call Orl context 0 |
| 92 212.140.133.31 212.140.133.35 MSSRPC c/o RPC Response: call Orl context 0 |

```
$TCP: AP.... len: 404, seq: 69878-70281, ack: 57735, win: 7810, src: 1
$NBT: SS: Session Message, Len: 400
$SMB: R transact TransactNmPipe (response to frame 91)
$MSSRPC: c/o RPC Response: call Orl context 0x0 hint Oxl40 cancels 0x0

000000120 00 00 49 50 50 00 49 24 00 00 00 FF FF 08 00 . . . . . . . . . . . .
000000130 00 00 00 00 00 00 52 00 55 60 4D 00 . . . . . . . . . . . . . .
000000140 6F 00 74 00 65 00 20 00 45 00 50 00 43 00 00 . o . t . e . . E . P . C . .
000000150 44 00 03 00 00 00 00 00 00 00 00 00 00 00 D . . . . . . . . . . .
000000160 24 00 00 00 00 00 00 08 00 00 00 08 $ . . . . . . . . . . . .
000000170 00 00 44 00 51 66 00 00 01 00 75 00 5C 74 00 . . . Q . f . . . u . \\ . t . .
000000180 20 00 73 00 68 00 61 00 72 00 65 00 00 00 . . s . h . a . r . e . . .
000000190 00 00 00 00 00 00 0A 00 00 00 00 00 75 00 . . . . . . . . . . . u
0000001A0 68 00 00 00 69 00 5C 60 00 65 00 73 00 00 00 k . f . i . l . e . s . . . .
```

Figure 21.13 etherleal trace: retrieving the list of shares

This illustrates clearly that the only involvement of the browse service was to let AliceNT know of the existence of a machine BobNT in the first place, and illustrates a couple of other significant points about browsing:

+   - the browse list contains only names. The client (AliceNT) that receives the browse list still has to resolve the name “BobNT” before she can access resources on the remote machine (BobNT) (cf. Module 21.4).

+   - you can access resources on machines without browsing to them. For example, if AliceNT knew already that the BobNT existed, and had a share called junkdirs, she could just run the command, e.g.

```
type \\\\bobnt\\junkdirs\\bootlog.txt
```

to see the contents of a file. The browser wouldn’t even have to be running. This also illustrates that you can use shares without explicitly mapping a drive. However, often we map the drive first, using Windows Explorer > Tools > Map Network Drive or the command-line equivalent, e.g.

```
net use J:\\\\bobnt\\junkdirs
type J:\\bootlog.txt
```