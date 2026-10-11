is somewhat awkward (to say the least). If you do not want to acquire RSS pains from the printer installation clicking orgy alone, you need to think about a non-interactive script. If more than one printer is using the same driver, the **rpclient setdriver** command *can* be used to set the driver associated with an installed queue. If the driver is uploaded to `/print/$` once and registered with the printing TDBs, it can be used by multiple print queues. In this case, you just need to repeat the **setprinter** subcommand of **rpclient** for every queue (without the need to conduct the **adddriver** repeatedly). The following is an example of how this can be accomplished:

```
```bash
root# rpclient SAMBA-CUPS -U root%secret -c 'enumdrivers'
cmd = enumdrivers

[Windows NT x86]
Printer Driver Info 1:
  Driver Name: [infotec   IS 2075 PCL 6]

Printer Driver Info 1:
  Driver Name: [DANKA InfoStream]

Printer Driver Info 1:
  Driver Name: [Heidelberg Digimaster 9110 (PS)]

Printer Driver Info 1:
  Driver Name: [dm9110]

Printer Driver Info 1:
  Driver Name: [mydrivername]

[....]
```
```

```
```bash
root# rpclient SAMBA-CUPS -U root%secret -c 'enumprinters'
cmd = enumprinters
  flags: [0x800000]
  name: [\\SAMBA-CUPS\\dm9110]
  description: [\\\\SAMBA-CUPS\\dm9110,,110ppm HiVolume DANKA Stuttgart]
  comment: [110 ppm HiVolume DANKA Stuttgart]
[....]
```
```

```
```bash
root# rpclient SAMBA-CUPS -U root%secret -c \
'setdriver dm9110 "Heidelberg Digimaster 9110 (PS)"'
cmd = setdriver dm9110 Heidelberg Digimaster 9110 (PPD)
Successfully set dm9110 to driver Heidelberg Digimaster 9110 (PS).
```
```