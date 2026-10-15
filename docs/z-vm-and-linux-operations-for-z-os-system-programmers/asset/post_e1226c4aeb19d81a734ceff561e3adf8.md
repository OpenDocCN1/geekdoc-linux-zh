
You may now shut down and re-IP L the system. It is the fastest way to put the previous changes into effect because no production systems are running yet. Pass the parameter IPLPARMS CONS=SYSC to the SHUTDOWN REIPL command:

```
==> shutdown re ipl iplparms cons=sysc
```

You will lose your session, but it should come back in a few minutes.

If the network settings are correct, you can now access your z/VM through the network instead of using the HMC. You can use a 3270-like emulator, such as IBM Personal Communications, to access your network-enabled z/VM by its IP address.

## 4.3.3 Relabeling the system volumes

This step is optional, however, it is recommended. Sometimes you will want to change the volume labels of the five z/VM system volumes (or three if you installed onto multiple 3390-9s). In the event that another vanilla z/VM system with the same labels is installed onto volumes accessible by your z/VM system, one of the systems will not IPL correctly.

When installing z/VM, it is possible to modify all but one volume label, that of the 530RES volume. This alleviates the problem that is described next, but it does not alleviate the problem of duplicate volume names. To understand this possibility, refer to Figure 4-16.

![](img/b0a4b9056f819dccd4781a5105c92d45_180_0.png)

Figure 4-16 The problem with two z/VM systems with identical volume labels

The z/VM system with the lower device addresses starting at E340 should IPL fine (though you might see a warning at system startup time about duplicate volume labels). However, if the z/VM system starting at device address F000 is IPLed, the 530RES volume will be used, but the remaining volumes in the system are searched for by volume label, not by device address. Because z/VM system 1's addresses are lower than z/VM system 2's, system 2 will use system 1's volumes. This is not good for either system!

Linux systems that use label conventions to access their root partitions also suffer from a similar problem. If you install two Linux systems onto the same disk, both using labels to identify their partitions, the second system will actually use the first partition labelled as the root filesystem. Using labels in Linux is not recommended by the authors of this book.

If there is a possibility of another z/VM system being installed on DASD that this system will have access to, the recommendation is that you perform the steps in the following sections:

- "Modifying labels in the SYSTEM CONFIG file" on page 166
- "Modifying labels in the USER DIRECT file" on page 168
- "Changing the labels on the five volumes" on page 169
- "Shutting the system down and re-IPLng it" on page 170

You must have access to the HMC to perform the steps.

> Note: This process must be done as documented. Making a mistake in one of the steps can easily result in an unusable system. Check your steps carefully and your system will come back with no problems. Try to do all steps in succession in a short amount of time. Close your door, do not answer your phone or e-mail, turn off instant messaging:))

### Modifying labels in the SYSTEM CONFIG file

This file controls what DASDs are used by the system, what virtual resources are defined and so on. Modify various DASD settings to allow the system to correctly start up with the new labels.

You must have an HMC 3270 session because z/VM will have to be restarted with a FORCE option.

To modify labels in the SYSTEM CONFIG file:

- 1. Start an Integrated 3270 Console session on the HMC from the CPC Recovery (or just Recovery) menu.
- 2. Note the first five CP-owned volumes by using the QUERY CPOWNED command:

```
==> q cpowned
Slot  Vol-ID  Rdev  Type  Status
1     S30RES  A700  Own   Online and attached
2     LX6SPL  A701  Own   Online and attached
3     LX6PAG  A702  Own   Online and attached
4     LX6W01  A703  Own   Online and attached
5     LX6W02  A704  Own   Online and attached
6     MPA705  A705  Own   Online and attached
```
