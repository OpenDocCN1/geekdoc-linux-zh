hdisk2  0000406c0c388efc4  vg00
hdisk3  000015082c65e92df  vg00
hdisk4  0000150837cc1a85  vg01
hdisk5  000015082c28f5c7  vg01
hdisk6  000015082c2931f5  vg01
hdisk7  000015082c296d8f  vg01

To add the new disk to a new or existing volume group, use **SMIT** or the `mkvg` and `extendvg` commands (see Figure 11-4):

```
```bash
#  mkvg -f -y vg10 hdisk10 hdisk11  ←– Create a volume group vg10 using hdisk10 and hdisk11
#  extendvg -f rootvg hdisk8  ←– Add hdisk8 to the rootvg volume group

#  smit mkvg
```
```

A volume group identifier (VGID) is assigned to each volume group. The VGID is a sixteen-digit hexadecimal number in older AIX versions and is a 32-digit hexadecimal number in AIX 5L. Each VGID in the system is represented by an entry in the `/etc/vg` directory.

```
```bash
# ls /etc/vg
vg00012560841690B0   vg0001256084A8C772
vg00012560841690B00000000000000000
```
```

![](bbox=[0.14, 0.58, 0.85, 0.93])