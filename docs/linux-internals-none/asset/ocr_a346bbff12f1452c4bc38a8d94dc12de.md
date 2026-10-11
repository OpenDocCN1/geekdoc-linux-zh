SERIAL Serial support is enabled.
SMP The kernel is an SMP kernel.
SOUND Appropriate sound system support is enabled.
VGA The VGA console has been enabled.
VT Virtual terminal support is enabled.
XT IBM PC/XT MFM hard disk support is enabled.

In addition, the following text indicates that the option:
BUGS= Relates to possible processor bugs on the said processor.
KNL Is a kernel start-up parameter.

Note that *all* kernel parameters listed below are *case sensitive*, and that a trailing = on the name of any parameter states that that parameter will be entered as an environment variable, whereas its absence indicates that it will appear as a kernel argument readable via /proc/cmdline by programs running once the system is up.

53c7xx= [HW,SCSI] Amiga SCSI controllers.
advb\_buttons= [HW,MOUSE]
advsys= [HW,SCSI]
aha152x= [HW,SCSI]
aha1542= [HW,SCSI]
aic7xxx= [HW,SCSI]
AM53C974= [HW,SCSI]
apm= [APM] Advanced Power Management.
arc\_rmi= [HW,NET]
atalflop= [HW, M68k]
atamouse= [HW,MOUSE] Atari Mouse.
atascsi= [HW,SCSI] Atari SCSI.
aztc= [HW,CD] Aztec CD driver.
baycom\_par= [HW,AX25] BayCom Parallel Port AX.25 Modem.
baycom\_ser\_fdx= [HW,AX25] BayCom Serial Port AX.25 Modem in Full Duplex Mode.
baycom\_ser\_hd= [HW,AX25] BayCom Serial Port AX.25 Modem in Half Duplex Mode.
bmouse= [HW,MOUSE,PS2] Bus mouse.
BusLogic= [HW,SCSI]
cd\_\_31a= [HW,CD]
cm206= [HW,CD]
com2020= [HW,NET]
com9010= [HW,NET]
com90xx= [HW,NET]
console= [KNL] output console + comm spec (speed, control, parity).