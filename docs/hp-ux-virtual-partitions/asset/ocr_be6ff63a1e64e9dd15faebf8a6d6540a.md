There are a number of commands you can use as you go about creating device files. The ioscan command is the first of these. Some of the examples in this section were used in Chapter 3, when building a kernel was covered. The following is an ioscan output of the same Series 700 for which sysdef was run when describing how a kernel is created in Chapter 4. (Using -f with ioscan would have created a full listing; you should try it with and without -f.) I included four ioscan outputs so that you could see examples from a variety of different systems. The last listing is from a large V-Class system used in some of the examples in Chapter 9, where disks and filesystems are covered.

```
($ \$ \text{user/sbin/ioscan})

(on Series 700)

```
H/W Path		Class		Description
==============================

		bc		'
1		graphics		Graphics
2		ba
2/0		unknown
2/0/1			target		Built-in SCSI
2/0/1.1.0		disk		HP C2247
2/0/1.2		target
2/0/1.2.0		disk		TOSHIBA CD-ROM XM-3301TA
2/0/1.6		target
2/0/1.6.0		disk		HP C2247
2/0/2		lan		Built-in LAN
2/0/4		tty		Built-in RS-232C
2/0/6		ext_bus		Built-in Parallel Interface
2/0/8	audio		Built-in Audio
2/0/10	pc		Built-in Floppy Drive
2/0/10.1	\zfloppy		HP PC FDC FLOPPY
2/0/11	ps2		Built-in Keyboard
8		processor		Processor
9		memory		Memory
```
```

The following is an ioscan output from a Series 800 system. Note the four processors shown in this output.