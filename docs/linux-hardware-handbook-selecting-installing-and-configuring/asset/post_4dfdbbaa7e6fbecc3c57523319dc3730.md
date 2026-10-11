
## Power Protection

A computer is an expensive product, and you’re likely to want to protect it from mishaps. Power-related mishaps are particularly relevant to computers, and come in two forms: too little power (brownouts or blackouts) or too much (power surges). In the United States, electricity comes through your wall outlet at 120V, but there’s always some small fluctuation at that value. While electrical appliances, including computers, can cope with some amount of fluctuation, larger fluctuations can prove to be quite damaging. There are several different types of devices you can buy to protect your computer against power problems:

- **Surge suppressors** A surge suppressor (also known as a *surge protector*) is a device that blocks large power surges. These devices typically redirect dangerous voltages into the ground wire of your home or office, keeping your computer out of the loop. In the process, surge suppressors usually trip an internal circuit breaker, thus cutting off power to all devices. Really large surges can damage or destroy a surge protector. The theory is that it’s better that it destroy the $50 surge suppressor than the $5,000 of computer equipment to which it’s attached, so the surge suppressor is designed to sacrifice itself for the computer. UL has developed a standard, known as *UL 1449*, which outlines characteristics of an adequate surge suppressor. You should definitely look for this in any new surge suppressor you buy. Some surge suppressors also include jacks for telephone cords, and this is a valuable addition if you use a modem. A few models include similar jacks for cable TV cables, and if you use a cable modem, you should definitely consider such a model. (You’re more likely to find cable-equipped surge suppressors in the television section of a department store than in the computer section.)

> **NOTE**
> The phone line protection of some surge protectors might or might not work with digital subscriber line (DSL) modems. The surge suppressor might or might not need to have four-line support to work with DSL modems, depending upon your wiring. Even if the appropriate wires are connected, surge protectors designed for telephones and conventional modems sometimes interfere with DSL operation, reducing connect speeds or preventing connections altogether. You can buy specialized DSL surge suppressors, or Ethernet surge suppressors to fit between the DSL modem and the computer, if you use an external DSL modem.

- **Line conditioners** Surge suppressors are great for protecting your equipment from massive fluctuations, but smaller power fluctuations can take their toll as well. Most computers can weather events such as minor brownouts, typical power fluctuations, and even very brief power outages without too much difficulty. Such events can cause a power supply to fail earlier than it might, however, and can even cause your computer to malfunction. A **line conditioner** prevents these problems by forcing the power to more closely meet the desired specifications. This device can compensate for a mild brownout and turn a voltage level that fluctuates over a range of several volts into one that’s much steadier. The end result is less wear and tear on your computer and a reduced chance of errors as a result.

- **Standby power supplies** A *standby power supply* (SPS) takes the line conditioner one step further, by adding a battery backup. If the power delivered to the SPS fails or drops below a certain level, the battery kicks in and continues to deliver power for a certain period of time. With any luck, the battery lasts long enough to let you safely exit from all your programs and shut down the computer. There is, however, a very brief interruption in power as the SPS shifts over to its battery. Most computer power supplies can weather the shift without too much difficulty, but the brief gap in coverage is undesirable and could conceivably cause memory errors or other problems, particularly if your computer’s power supply is low in quality.

- **Uninterruptible power supplies** An *uninterruptible power supply* (UPS) is like an SPS in concept, but the design is different. Rather than detect a failure and switch over in the event of a failure, a UPS always operates from its battery, simultaneously charging and discharging it. In the event of a power failure, therefore, your computer experiences no interruption whatsoever; the UPS’s battery simply begins draining without being charged. Some companies advertise their SPSs as if they were UPSs, so terms such as *true UPS* are often used for UPSs.

At a minimum, you should purchase a surge suppressor for your computer system. In fact, I use surge suppressors on all my expensive electrical appliances, such as my television, stereo, and so on. The drawback to a surge suppressor is that it offers no protection against a power outage. A UPS or SPS is an extremely useful device if you live in an area that experiences frequent power outages; you can weather an outage of a few minutes as if nothing happened, and power down safely in case of a longer problem. As you might expect, the cost of these devices rises as you move up the scale from a surge suppressor to a UPS.

All but the lowest-level UPSs contain an interface to the computer. This interface is generally a serial cable, and you can run a Linux program to monitor the UPS’s status. In the event of a power failure, the daemon can order a safe shutdown of your Linux computer, thus saving you the bother, or doing it even if you’re away. UPSs vary in how they communicate with the computer, however, so you should look into available UPS software. Some UPS manufacturers provide Linux software for their UPSs, but for others you might need to rely upon generic Linux software that works with several models, or you might be entirely out of luck. The Linux UPS HOWTO document (included with all major Linux distributions) has pointers to more specifics on UPS models and UPS software.

## Summary

A computer's case is the most externally visible component of a computer, with the possible exception of the monitor, keyboard, and mouse. The case houses all the major computational devices of most computers—the motherboard, CPU, hard disks, expansion cards, and so on. A poor choice in a case can cause you grief for months or years to come, as you struggle against it whenever you upgrade some other component or curse its ungainly size. Checking a case out in person and looking for a few key features can go a long way towards ensuring that you have a computer with which you can live.

One of the most important components of a case is the power supply. The most important issue in picking a power supply is to get one that supplies adequate wattage to the components that reside in the computer's case. The 235W power supplies that are common today are adequate for most modest computers, but if you expect to load your system up with lots of hard disks, internal tape drives, half a dozen expansion cards, and so on, you might want to look into a larger power supply.

# Part II

## Storage

## IN THIS PART

- 5 Hard Disks 135
- 6 Removable Disks 167
- 7 Optical Drives 191
- 8 Tape Backup 227
- 9 SCSI Host Adapters 257

# Hard Disks

## Chapter 5

## IN THIS CHAPTER

- Linux Disk Space Requirements 136
- EIDE Versus SCSI Disks 143
- Evaluating Disk Performance 151
- Hard Disk Form Factors 156
- Tuning Disk Performance in Linux 158

Hard disks use a fairly mature technology and are well standardized in their interfaces. Therefore, you're unlikely to encounter Linux-related difficulties with specific models of hard disks. (SCSI host adapters are another matter, however. Chapter 9, “SCSI Host Adapters,” covers this matter in more detail.) When you purchase a hard disk, therefore, there are few Linux-specific issues you must consider. For the most part, a hard disk that's good for use in any other OS is good for use in Linux.

How you *use* a hard disk is somewhat different in Linux than in other OSs. Linux uses its own filesystem (currently ext2fs, although at least four new filesystems are in the running to become the next standard Linux filesystem). You probably want to partition a hard disk for Linux differently than you would partition it for most other OSs. There are also Linux utilities available that can help you get improved performance out of a hard disk. This chapter covers these issues, as well as the basics of hard disk technology.

## Linux Disk Space Requirements

As with RAM requirements, official Linux disk space requirements vary from one distribution to another, but similar configurations of two distributions will require similar amounts of disk space. As with RAM requirements, most minimum disk space requirements are on the skimpyside. Making adjustments for your particular usage patterns can be tricky in some cases, particularly if you're unfamiliar with Linux.

## Minimum Space Needed

Table 5.1 summarizes official disk space requirements for various popular Linux distributions.

**TABLE 5.1 Official Disk Space Requirements of Linux Distributions**

| Distribution | Minimum Disk Space |
| :--- | :--- |
| Caldera OpenLinux 2.3 | 170MB |
| Corel Linux 1.0 | 500MB |
| Debian GNU/Linux 2.1 | 35MB |
| Linux Mandrake 7.0 | 500MB |
| Red Hat Linux 6.1 | 250MB |
| Slackware Linux 7.0 | 80MB |
| SuSE Linux 6.3 | 300MB |

It's usually not possible to install a distribution on less than the official minimum amount of disk space because the installation routines won't let you remove packages to bring the disk space requirements down. It is often possible, however, to install the official minimum and
