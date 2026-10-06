
- If you reasonably believe that the computer is destroying evidence, immediately shut down the computer by pulling the power cord from the back of the computer.
- If a camera is available and the computer is on, take pictures of the computer screen. If the computer is off, take pictures of the computer, the location of the computer, and any electronic media attached.
- Determine whether special legal considerations apply (doctor, attorney, clergy, psychiatrist, newspapers, publishers, and so on).

These are all important first steps to preserving the chain of custody and ensuring the integrity of the investigation.

## Don’t Touch the Suspect Drive

The first, and perhaps most important guideline, is to touch the system as little as possible. You do not want to make changes to the system in the process of examining it. Let’s look at one possible way to make a forensic copy of a drive. You can make a forensic copy with most major forensic tools such as AccessData’s Forensic Toolkit (FTK), Guidance Software’s EnCase, or PassMark’s Software OSForensics. You, can also do it with free tools using Linux.

You need two bootable copies of Linux: one on the suspect machine and one on the target machine. You may use any Linux distribution you are comfortable with. Whichever version of Linux you use, the steps will be the same:

- 1. Completely wipe the target drive:

```
dd if=/dev/zero of=/dev/hdb1 bs=2048
```

- 2. Set the target forensics drive to receive the copy of the suspect drive you want to examine. The Netcat command helps with that. The specific syntax is as follows:

```
nc -l -p 8888 > evidence.dd
```

This tells the machine to listen on port 8888 and put whatever it receives into evidence.dd.

- 3. On the suspect machine, start the drive’s infection to the forensics server:

```
dd if=/dev/hda | nc 192.168.0.2 8888 -w 3
```

Of course, this assumes that the suspect drive is hda. If it’s not, then replace that part with the partition that you are using. This also assumes the server has an IP address of 192.168.0.2. If it’s not, replace it with whatever forensics server’s IP address is.

- 4. You also want to create a hash of the suspect drive. Later you can make the hash of the drive you have been working with and compare that to the hash of the original drive and confirm that nothing has been altered. You can make a hash using Linux shell commands:

```
md5sum /dev/sda | nc 192.168.0.2 8888 -w 3
```

## CHAPTER 16 Introduction to Forensics

After completing the steps, you have a copy of the drive. Making two copies is often a good idea: one you will work with, and another will simply be stored. Under no circumstances should you do your forensic analysis on the suspect drive.

## Leave a Document Trail

Beyond touching the actual drive, the next concern is documentation. If you have never worked in any investigative capacity, the level of documentation might seem onerous to you. However, the rule is simple: Document everything.

When you first discover a computer crime, you must document exactly what events occurred. Who was present and what were they doing? What devices were attached to the computer, and what connections did it have over the network/Internet? What hardware and operating system were being used?

When you begin your actual forensic investigation, you must document every step. Start documenting the process you use a forensic copy. Every tool you use and every test you perform. You must be able to show in your documentation everything that was done.

## Secure the Evidence

First and foremost, the computer must be offline to prevent further tampering. In some limited circumstances a machine might be online to trace an activity, ongoing attack, but the general rule is to take offline immediately.

The next step is to limit access to the machine. No one who does not absolutely need access to the evidence should have it. Hard drives should be locked in a safe or secure cabinet. Analysis should be done in a room with limited access.

You must also be document every person who had access to the evidence, how they interacted with it, and where the evidence was stored. There must be no period of time that you cannot account for the evidence. This is called chain of custody.

## FBI Forensic Guidelines

Beyond the general guidelines discussed, the FBI gives some specific guidelines. In most cases, they will overlap with the earlier discussion, but covering the FBI recommendations is still useful to do.

If an incident occurs, the FBI recommends that the first responder preserve the state of the computer at the time of the incident by making a backup copy of any logs, damaged or altered files, and of course, any files left by the intruder. This last part is critical. Hackers frequently use tools and might leave traces of their presence. Furthermore, the FBI warns that if the incident is in progress, activate any auditing or recording software you might have available. Collect as much data about the incident as you can. In other words, this might be a case where you do not take the machine offline, but rather analyze the attack in progress.

Another important step is to document the specific losses suffered due to the attack. Losses typically include the following:

- Labor cost spent in response and recovery. (Multiply the number of participating staff by their hourly rates.)
- If equipment was damaged, the cost of that equipment.
- If data was lost or stolen, what was the value of that data?

The FBI also stresses that you should check the following:

- Logs (router, chat)
- Portable storage devices (external drives)
- E-mails
- Devices
- Cell phones

## Finding Evidence on the PC

After you have secured the machine, it is time to start looking for evidence. That evidence can come in many forms. First, remember that the operating system has logs. The following outlines the data that provides insight into the case.

## In the Browser

The browser can be a source of both direct and circumstantial evidence. However, if you suspect someone of creating a virus, you would check the browser.

## In System Logs

Regardless of what operating system you are, the operating system has logs. Those logs can be critical in any forensic investigation and you should retrieve them.

## Windows Logs

Let's start with Windows XP/Vista/7/8/10. With all of versions of Windows, you find the logs by clicking the Start button in the lower-left corner of the desktop and then clicking the Control Panel. You then click on Administrative Tools and double-click the Event Viewer. The following outlines the logs you would check. (Note that not all appear in every version of Windows).

> FYI: Logging
With all the that you have to turn the logging on; otherwise, there will be nothing in these logs.

- Security log: This is probably the most important log from a forensics point of view. It has both successful and unsuccessful login events.
- Application log: This log contains various events logged by applications or programs. Many applications record their errors in the application log.
- System log: This log contains events logged by Windows system components. This includes events such as driver failures. This particular log is not interesting from a forensics perspective as the other logs.
- Forwarded Events log: This log is used to store events collected from remote computers. This will only have data in it if forwarding has been configured.
- Applications and Services Logs: This log is used to store events from a single application or component rather than events that might have systemwide impact.
