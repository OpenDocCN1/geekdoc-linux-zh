With the command lszfcp you can get more information about zfcp adapters, ports, and units that are online. In Figure 6-7 you can see a example of a lszfcp command.

```
# lszfcp -H -D -P
0.0.0 3ec4 host0
0.0.3fc4 host1
0.0.3ec4/0x50050763003008455 rport-0:0-0
0.0.3fc4/0x500507630030c455 rport-1:0-0
0.0.3ec4/0x50050763003008455/0x4050142010000000 0:0:0:0
0.0.3ec4/0x50050763003008455/0x4050402220000000 0:0:0:1
0.0.3fc4/0x500507630030c455/0x4050402220000000 1:0:0:0
0.0.3fc4/0x500507630030c455/0x4051402100000000 1:0:0:1

-H : list information about HBA
-P : list information about ports
-D : list information about units
```

Figure 6-7 lszfcp command

With the SAN discovery tool and using command san_disc, you can display information about SANs such as the world wide port name (wwpn) of ports on storage and the logical unit identifier (lunid).

This is only available on SLES9 SP3 and SLES10. You need to load the zfcp_haapi module. See an example of the san_disc command in Figure 6-8.

```
# san_disc -o HBA_LIST
Number of Adapters: 2
No. Port WWN Node WWN SerialNumber Busid
1 0x50050764012203b3 0x5005076400c4e2d4 IBM5100000004E240 0.0.38c6
2 0x50050764012203b3 0x5005076400c4e2d4 IBM5100000004E240 0.0.39c6
# san_disc -o PORT_LIST -a 1
No. Port WWN Node WWN DID Type
1 0x50050764012203b3 0x5005076300c0d09 0x0300a0 N_Port
2 0x5005076300c1ad9 0x5005076300c0d09 0x0300a0 N_Port
3 0x50050764012203b3 0x5005076400c4e2d4 0x0300a0 N_Port
# san_disc -o REPORT_LUNS -a 1 -p 0x500507630c1ad9
Number of LUNs: 4
No. LUN
1 0x6200000000000000
2 0x6201000000000000
3 0x6202000000000000
4 0x6203000000000000
```

Figure 6-8 san_disc command