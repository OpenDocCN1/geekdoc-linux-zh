# Table A-2 Hardware Parameters Configuration Examples

| Configuration | Example |
| :--- | :--- |
| ATAPI CD-ROM, jumpered as master on 2nd IDE channel | hdc=cdrom |
| non-IDE Mitsumi CD-ROM on port 340, IRQ 11 | mcd=0x340,11 |
| Three non-IDE Mitsumi CD-ROM drives using the experimental driver, io ports 300, 304, and 320 with IRQs 5, 10 and 11 | mcdx=0x300,5,0x304,10,0x320,11 |
| Sony CDU 31 or 33 at port 340, no IRQ | cdu31=0x340,0 cdu31_port=0x340 cdu31a_irq=0 |
| Aztech CD-ROM at port 220 | aztcd=0x220 |
| Panasonic-type CD-ROM on a SoundBlaster interface at port 230 | sbpcd=0x230,1 |
| Philips/LMS cm206 and cm260 at IO 340 and IRQ 11 | cm206=0x340,11 |
| Goldstar R420 at IO 300 | gscd=0x300 |
| Mitsumi drive on a MAD16 soundcard at IO Addr 330 and IRQ 1, probing DMA | ispl6=0x330,11,0,Mitsumi |
| Sony CDU 531 at IO address 320 | sonycd535=0x320 |

**Please Note**

Most newer Sound Blaster cards come with IDE interfaces. For these cards, you do not need to use sbpcd parameters, only use hdcx parameters.