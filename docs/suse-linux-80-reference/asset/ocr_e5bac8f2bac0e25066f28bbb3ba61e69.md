The value 0x79 only has to be set when the firmware version is unknown.

*Example:* `aztcd=0x320`

+   - *Goldstar R420 CD-ROM drive*  
+     `gscd={addr}`

+   - *Mitsumi CD-ROM drive*  
+     `mcd={addr},{irq},{wait}`  
+     *Example:* `mcd=0x300,10`

+   - *Mitsumi CD-ROM drive (multisession)*  
+     `mcdx={addr},{irq}`  
+     *Example:* `mcdx=0x300,10`  
+     Up to five drives are supported.

+   - *Mozart interface*  
+     `isp16={addr},{irq},{dma},{type}`

| Variable | Values / Meaning |
|---|---|
| `{type}` | Sanyo, Panasonic, Sony, Mitsumi |

This driver is responsible for CD-ROM drives connected to the types ISP16, MAD16, or Mozart. The value of `{type}` follows the interface plug where the CD-ROM is connected to the sound card.

*Example:* `isp16=0x340,10,3,Sony`

+   - *Optics Storage 8000 AT CD-ROM drive*  
+     `optcd={addr}`  
+     *Example:* `optcd=0x340`

+   - *Philips CM206 CD-ROM drives*  
+     `cm206={addr},{irq}`  
+     *Example:* `cm206=0x340,10`

+   - *Pro Audio Spectrum 16 – SCSI host adapter*  
+     `pas16={addr},{irq}`  
+     On the Pro Audio Spectrum 16 sound card, there is a SCSI host adapter, the settings of which can be passed to the kernel with this parameter.