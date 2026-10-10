
| 0 | 0x0 | Zip archive data, at least v2.0 to extract, compressed size: 3576647, uncompressed size: 5439486, name: DAP1320_fw_1.11b10.zip |

| 3576803 | 0x369323 | End of Zip archive, footer length: 22 |

```text
Scan Time: 2021-09-06 12:05:16
Target File: /home/grayhat/DAP-1320_FIRMWARE_1.11b10.zip
MD5 Checksum: 3d1355842d5d1476544e8801a99605c6e
Signatures: 411
```

| DECIMAL | HEXADECIMAL | DESCRIPTION |
| --- | --- | --- |
| 0 | 0x0 | Image header, header size: 64 bytes, CRC: 0x71C7BA94, created: 2013-09-16 08:50:53, size: 799894 bytes, Data Address: 0x80002000, Entry Point: 0x81A8BF0, data CRC: 0xA62B902, OS: Linux, CPU: MIPS, image type: OS Kernel image, compression type: lz, image name: "Linux Kernel Image" |
| 64 | 0x40 | LZMA compressed data, properties: 0x5D, dictionary size: 8388608 bytes, uncompressed size: 2303956 bytes |
| 851968 | 0xD0000 | Squashfs filesystem, little endian, version 4.0, compression:lzma, size: 2774325 bytes, 589 nodes, blocksize: 65536 bytes, created: 2013-09-16 08:51:15 |

```text
Scan Time: 2021-09-06 12:05:18
Target File: /home/grayhat/_DAP-1320_FIRMWARE_1.11B10.zip.extracted/_DAP1320_fw_11b10.bin.extracted/
MD5 Checksum: a741e817c6a2f1609573823968244e2620
Signatures: 411
```

| DECIMAL | HEXADECIMAL | DESCRIPTION |
| --- | --- | --- |
| 78808 | 0x133D8 | Certificate in DER format (x509 v3), header length: |
| 4, sequence length: 30 | 0x13538 | Certificate in DER format (x509 v3), header length: |
| 79604 | 0x136F4 | Certificate in DER format (x509 v3), header length: |
| 4, sequence length: 30 | 0x1B0020 | Linux kernel version 2.6.31 |
| 1790640 | 0x1B5B20 | CRC32 polynomial table, little endian |
| 2090280 | 0xEA8C0 | Neighbor text, "Neighbor init():can't add protocol" |
| 2090300 | 0xEA8D4 | Neighbor text, "Neighbor add" |
| 2101043 | 0xEAFA3 | Neighbor text, "neighbor |
