# CHAPTER 3 | Basic Security: Facilities Through the Boot Process

Port knocking is private only if the connections are made through a secure tunnel, such as IP packets that are encapsulated. Another example of privacy is the use of one-time passwords. The password on the client and server should match. The passwords change in the same way on both client and server every time both are configured with the same algorithm.

# Integrity

The integrity of information is important. If information has integrity, you know it hasn't changed. A black-hacker can intercept a secret message such as the balance of a bank account and change it, only the black-hacker is served.
Integrity as a process requires options such as digital signatures. As a process control, integrity depends on using a TPM chip or a GPU Privacy Guard (GPG) key. That tool verifies the digital signature, ensuring the integrity of the data between the source and the destination.
IBM is taking this concept one step further with the Integrity Measurement Architecture (IMA). The IMA is a Linux module that uses the TPM to check the executable files associated with Linux before it is loaded during the boot process. IBM has explicitly stated that IMA is not related to DRM.

# Alarm

An alarm, such as one of those from log files, is an important tool to the security professional. A good alarm is based on sufficient cause, such as suspicious activity from what should be an inactive account.
A black-hacker has a couple of options with respect to alarms. He could try to replace alarm-related commands with Trojans. In such case, Trojans could use multifunctional commands or scripts with appropriate file names. He could also try to delete the associated log files. The resulting lack of an alarm is one possible cause of false negatives. He could to set off additional alarms, so administrators start to ignore them. There are so many logs that an administrator has to deal with, such false positives could cause a security professional to stop trusting the alarm.

# Best Practices: Basic Security

The "best practices" section in this and upcoming chapters is designed as a "lessons learned" review of the chapter. If you already know the basics of a particular topic, the notes from this section may be all that you need.

First, some security is required wherever the server is stored. It mere seconds for someone to remove an unsecured server. It takes just a few seconds to remove a hard drive from an unsecured server. Anyone with access to a bootable device such as a CD/DVD drive or USB port can have his own system on his servers. Anyone with access to an open network port can watch your traffic with a protocol analyzer. Anything you can do to secure these systems will help.

![](bbox=[0.915, 0.315, 0.998, 0.665])