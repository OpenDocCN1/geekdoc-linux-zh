```
p00>>> show dev

dga1.1001.0.7.1          $1$DGA1          HSG80  V6F

dkc0.0.0.0.7.0          DKC0            R22DD-LS 0306
dqa0.0.0.0.105.0        DQA0            CD-224E 9.5B
dva0.0.0.0.0            DVA0
eia0.0.0.0.0            EIA0            00-50-8B-AE-F3-23
eia0.0.0.0.7.1          PGA0            WWN 2000-0000-c934-7c58
pka0.7.0.6.0            PKA0            SCSI Bus ID 7
pkb0.7.0.106.0          PKB0            SCSI Bus ID 7
pkc0.7.0.7.0            PKC0            SCSI Bus ID 7
...
```

A new device also shows up when we enter the "show dev" command. This will be the device that we use to boot the cluster node after the TruCluster Server software is properly installed and configured.

This process of identifying the cluster member's boot device should be performed on each cluster member's system console before the installation and configuration of the TruCluster Server software.

# 4.3 Firmware for a Cluster

Firmware on the AlphaServer and the StorageWorks storage subsystem components is the first software that is executed when the hardware powers up and usually the last software to execute as the hardware is powered down. It is also the software that directly controls the hardware and as such is platform dependent.

Although firmware is platform dependent, it is operating system independent. There have been many modifications to the operating system that are designed to interoperate with newer firmware features. For this reason, you should always install the latest firmware available from HP for the AlphaServers and for the StorageWorks storage subsystem of your cluster. All too frequently, operating system problems encountered by users can be traced to not having the appropriate firmware and operating system combination. As one colleague once said, "the PAL code makes the difference."10

# 4.3.1 Alpha Firmware

Alpha Firmware updates usually come on new Alpha Firmware Release CDs that accompany the release of a new version of Tru64 UNIX. Alpha Firmware updates can also be found on the Web at:

```
ftp://ftp.digital.com/pub/Digital/Alpha/firmware/
```

> 10 PAL code or Privileged Architecture Library (PAL-code) is made up of non-interruptible functions required to support the lowest level of activities on an AlphaServer system such as context switching, system call initiation, and interrupt/exception dispatching.