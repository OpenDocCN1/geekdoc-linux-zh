# 312 Appendixices

(continued)

| hdx=nowerr | ignore the WRRRR_STAT bit on this drive |
| hdx=cdrom | drive is present, and is a cdrom drive |
| hdx=cyl,head,sect | disk drive is present, with specified geometry |
| hdx=autotune | driver will attempt to tune interface speed to the fastest PIO mode for supported, if possible for this drive only. Not fully supported by all chipset types, and quite likely to cause trouble with older/odd IDE drives |
| idex=noprobe | do not attempt to access/use this interface |
| idex=base | probe for an interface at the address specified, where "base" is usually 0x1F0 or 0x70 and "ctl" is assumed to be "base+0x20" |
| idex=base.ctl | specify both base and ctl |
| idex=base.ctl,irq | specify base, ctl, and irq number |
| idex=autotune | driver will attempt to tune interface speed to the fastest PIO mode supported, for all drives on this interface. Not fully supported by all chipset types, and quite likely to cause trouble/odd IDE drives |
| idex=noautotune | driver will NOT attempt to tune interface speed This is the default for most chipsets, except the cmd640. |
| idex=serialize | do not overlap operations on index and ide(x1) |