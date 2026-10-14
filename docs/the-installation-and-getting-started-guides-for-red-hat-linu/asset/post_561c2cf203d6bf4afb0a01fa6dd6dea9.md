
## Appendix D: General Parameters and Modules

Here are some examples of these modules in use:

| Configuration | Example |
|---|---|
| ATAPI CD-ROM, jumpered as master on 2nd IDE channel | hdc=cdrom |
| non-IDE Mitsumi CD-ROM on port 340, IRQ 1 | mcd=0x340,11 |
| Three non-IDE Mitsumi CD-ROM drives using the experimental driver, io ports 300, 304, and 320 with IRQs 5, 10 and 11 | mcdx=0x300,5,0x304,10,0x320,11 |
| Sony CDU 31 or 33 at port 340, no IRQ | cdu31=0x340,0 |
| (module arguments for above) | cdu31_port=0x340 cdu31a_irq=0 |
| Aztech CD-ROM at port 220 | aztcd=0x220 |
| Panasonic-type CD-ROM on a SoundBlaster interface at port 220 | sbpcd=0x230,1 |
| Philips/LMS cm206 and cm260 at IO 340 and IRQ 11 | cm206=0x340,11 |
| Goldstar R420 at IO 300 | gscd=0x300 |
| Mitsumi drive on a MAD16 soundcard at IO Addr 330 and IRQ 1, probing DMA | isp16=0x330,11,0,Mitsumi |
| Sony CDU 531 at IO address 320 | sonycd535=0x320 |

Please Note: Most newer Sound Blaster cards come with IDE interfaces. For these cards, you do not need to use sbpcd parameters, only use hdx parameters

## SCSI parameters

| Hardware | Module | Parameters |
|---|---|---|
| NCR53c810/820/720 | 53c7_8xx.o | |
| NCR53c700/710/700-66 | 53c7_8xx.o | |
| AM53/79C974 PC-SCSI Driver | AM53C974.o | AM53C974=host-scsi-id |
| Qlogic PCI-Basic |  | target-scsi-id,max-rate, max-offset |
| Most Buslogic (now Mylex) cards with "BT" part number | BusLogic.o | BusLogic_Options=option,option,... |
|  |  | (See /usr/src/linux/drivers/scsi/README.BusLogic) |
|  | NCR53c406a.o | ncr53c406a=io,port[,IRQ[,FASTPIO]] |
|  |  | ncr53c406a io=port irq=IRQ fastpio=FASTPIO |
| Advanys SCSI Cards | advansys.o | |
| Adaptec AHA 152x | aha152x.o | aha152x=io_base,IRQ,scsi_id,reconnect,parity |
| Adaptec AHA 1542 | aha1542.o | aha1542=io_base,bus on, busoff,dmaspeed |
| Adaptec AHA 1740 | aha1740.o | |
| Adaptec AHA-274x, AHA-284x, AHA-29xx, AHA-394x, AHA-398x, AHA-274x, AHA-274xT, AHA-2842, AHA-2910B, AHA-2920C, AHA-2930U/U2, AHA-2940W/U/UW/AU/U2W/U2B/U2BOEM, AHA-2944DWD/UD/UWD, AHA-2950U/W/B, AHA-3940/U/W/UW, AUW/U2W/U2B, AHA-3950U2D, AHA-3985/U/W/UW, AIC-777x, AIC-785x, AIC-786x, AIC-787x, AIC-788x, AIC-789x, AIC-3860 | aic7xxx.o | aic7xxx=string |
| Data Technology Corp DTC3180/3280 | dtc.o | |
| DTP SCSI host adapters (EATA/DM A) | eata.o | eata=port0,port1,port2,...options |
| PM2011B/9X ISA, PM2021A/9X ISA, PM2012A |  | |
| PM2012B, PM2022A/9X EISA, PM2122A/9X, PM2322A/9X, |  | eata io_port=port0,port1,port2,...option=value |

## Appendix D: General Parameters and Modules

|  |  |  |
|---|---|---|
| SmartRAID PM3021, PM3222, PM3224 |  |  |
| DTP SCSI Adapters PM2011, PM2021, PM2041, | eata_dma.o |  |
| PM3021, PM2012B, PM2022, PM2122, PM2322, PM2042, PM3122, PM3222, PM3322, PM2024, PM2124, PM2044, PM2144, PM3224, PM3334 |  |  |
| DTP EATA-PIO boards | eata_pio.o |  |
| Future Domain TMC-16x0-based cards | fdomain.o | fdomain=io_base,IRQ,[ADAPTER_ID] |
| TMC-1800, TMC-18C50 |  |  |
| TMC-18C30, TMC-36C70 |  |  |
| Future Domain TMC-1650 |  |  |
| TMC-1660, TMC-1670, TMC-1680, TMC-1610M/MER/MEX, TMC-3260 (PCI) |  |  |
| Quantum ISA-200S, ISA-250MG |  |  |
| Adaptec AHA-2920A (PCI) (NOT AHA-2920C) |  |  |
| NCR5380 and NCR53c400 cards | g_NCR5380.o | ncr5380=io_port,IRQ,dma |
|  |  | ncr53c400=io_port,IRQ |
|  |  | ncr5380 io=io_port irq=IRQ dma=dma |
|  |  | ncr53c400 io=io_port irq=IRQ |
| GDT ISA/EISA/PCI Disk Array Controller | gdth.o | gdth=IRQ0,IRQ1,IRQ2... options.values |
| IOMEGA MatchMaker parallel port |  |  |
| SCSI adapter | imm.o |  |
| Always IN2000 ISA SCSI card | in2000.o | in2000=setup_string:value |
|  |  | in2000 setup_string=value |
| Initio INI-9X00/UW SCSI host adapters | initio.o |  |
| AMI MegaRAID 418, 428, 438, 466, 762 | megaraid.o |  |
| NCR SCSI controllers with 810/810A/815/825/825A/860/875/876/895 chipsets | ncr53c8xx.o | ncr53c8xx="option1:value1,option2:value2,..." |
|  |  | ncr53c8xx="option1:value1 option2:value2..." |
| Pro Audio Spectrum/Studio 16 | pas16.o | pas16=port,irq |
| IOMEGA PPA3 parallel port |  |  |
