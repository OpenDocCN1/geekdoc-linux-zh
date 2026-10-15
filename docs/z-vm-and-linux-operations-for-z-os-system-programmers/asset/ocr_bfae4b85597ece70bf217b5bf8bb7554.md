220-FTPSERVE IBM VM Level 530 at VMLINUX6.ITSO.IBM.COM, 16:33:09 EDT
THURSDAY 2008-05-15
220 Connection will close if idle for more than 5 minutes.
Name (9.12.4.89:root): lnxmaint 2a
331 Send password please.
Password:lnxmaint 2b
230 LNXMAINT logged in; working directory = LNXMAINT 191
Remote system type is z/VM.
ftp> cd lnxmaint.192 3
250 Working directory is LNXMAINT 192
ftp> put swapgen.exec 4
local: swapgen.exec remote: swapgen.exec
500 Unknown command, 'EPSV'
227 Data transfer will passively listen to 9,12,4,89,4,7
125 Storing file 'swapgen.exec'
100% |******************************************| 16750  14.60 MB/s
--:-- ETA
250 Transfer completed successfully.
16750 bytes sent in 00:00 (1.74 MB/s)
ftp> bin 5
200 Representation type is IMAGE.
ftp> site fix 80 6
200 Site command was accepted.
ftp> put vmrdr.ikr sles10s2.ikr 7
local: vmrdr.ikr remote: sles10s2.ikr
227 Data transfer will passively listen to 9,12,4,89,4,8
125 Storing file 'sles10s2.ikr'
100% |******************************************| 5904 KB  4.48 MB/s
00:00 ETA
250 Transfer completed successfully.
6042680 bytes sent in 00:01 (4.39 MB/s)
ftp> put initrd sles10s2.initrd 8
local: initrd remote: sles10s2.initrd
227 Data transfer will passively listen to 9,12,4,89,4,9
125 Storing file 'sles10s2.initrd'
100% |******************************************| 8067 KB  3.32 MB/s
00:00 ETA
250 Transfer completed successfully.
8261468 bytes sent in 00:02 (3.28 MB/s)
ftp> quit 9
221 Quit command received. Goodbye.