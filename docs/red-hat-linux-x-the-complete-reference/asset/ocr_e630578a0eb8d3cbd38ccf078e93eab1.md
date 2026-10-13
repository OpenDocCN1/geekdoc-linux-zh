```
kernel /boot/vmlinuz-2.4.18-3 ro root=/dev/hda3 hdc=ide-scsi
```

**Tip** If you are not using GRUB, or if for some reason you do not want to modify the `/etc/grub.conf` file, you can configure the `/etc/modules.conf` file ( `/etc/modprob.conf` on 2.5 and 2.6 kernels) to load and implement the SCSI emulation for your IDE CD drives. This involves entering several module configuration commands in the `/etc/modules.conf` file. When your system starts up, it will load the modules as specified in that file.

# scanbus

To check that your IDE drives are being recognized as SCSI drives, run `cdrecord` with the `-scanbus` option (or `dvdrecord` for DVD writers). This example shows two IDE CD drives now emulating SCSI CD drives. One is a Plextor IDE CD-RW drive (`scd0`), and the other is a Toshiba DVD-ROM drive (`scd1`).

```
# cdrecord -scanbus
```

```
Cdrecord 1.9 (i686-pc-linux-gnu) Copyright (C) 1995-2000 Jörg Schilling
Linux sg driver version: 3.1.17
Using libscg version 'schily-0.1'
scsibus0:
    0,0,0 0) 'PLEXTOR ' 'CD-R   PX-W1210A' '1.02' Removable CD-ROM
    0,1,0 1) 'TOSHIBA ' 'DVD-ROM SD-M1402' '1010' Removable CD-ROM
    0,2,0 2) *
    0,3,0 3) *
    0,4,0 4) *
    0,5,0 5) *
    0,6,0 6) *
    0,7,0 7) *
```