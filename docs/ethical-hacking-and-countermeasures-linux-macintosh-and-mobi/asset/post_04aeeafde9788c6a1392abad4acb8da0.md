
This worm installs itself as an application hook. If the system runs as a root user, then the apphook subdirectory of /Library/InputManagers/ directory is deleted. If it runs as nonroot user, ~/Library/InputManagers/ directory is deleted. The worm replaces it with the following files:

- apphook/Info
- apphook/apphook.bundle/Contents/Info.plist
- apphook/apphook.bundle/Contents/MacOS/apphook

Infected application files have the following extended attributes:

- name: oompa
- value: loompa

This worm creates the following temporary files:

- /tmp/pic.gz
- /tmp/pic
- /tmp/latestpics
- /tmp/latestpics.tar
- /tmp/latestpics.tar.gz
- /tmp/latestpics.tgz
- Several files under /tmp/apphook

## Inqtana.A: F-Secure Worm

The Java-based Inqtana.A worm spreads through Bluetooth and affects unprotected Mac OS X 10.4 systems. This worm arrives as an OBEX push request, requiring the user to accept transferred data. As soon as the transfer is complete, the worm uses a directory traversal exploit to copy its files. The worm then activates on reboot. The active worm searches for devices that accept OBEX push transfer and sends itself to those devices. The files com.openbundle.plist and com.pwned.plist are dropped into a location where they can be called during system startup. The file openbundle.plist unpacks the worm components, and com.pwned.plist executes the worms.

## Preventive Measures for OS X Inqtana.A

OS X/Inqtana.A affects only Mac OS X 10.4. To protect against this worm in OS X 10.4, follow these steps:

1. Patch the system by installing updates from Apple.
2. Delete the following files, which will have been compromised by the worm:
   - /Users/worm-support.tgz
   - /Users/InqTest.class
   - /Users/com.openbundle.plist
   - /Users/com.pwned.plist
   - /Users/libavetanaBT.jnilib
   - /Users/javax
   - /Users/ld
   - /Users/[username]/Library/LaunchAgents/com.pwned.plist
   - /Users/[username]/Library/LaunchAgents/com.openbundle.plist

## Viruses in Macs: Macro Viruses

Macro viruses cause great danger to Macintosh users. The first real macro virus attacked a Microsoft Word file, and macro viruses quickly rose in popularity. Even with increased user awareness, these viruses continue to cause great damage because of the ubiquity of Microsoft software. Macro viruses have been created to attack other Microsoft applications, such as Excel, Visio, PowerPoint, and Access, but Microsoft Word viruses are the most popular. The macro viruses are a real threat, as they can be effective on different platforms; they can damage both Macintosh and Windows systems.

Macro viruses targeting Microsoft Word files use commands like AutoOpen, AutoClose, AutoExec, and AutoExit. These commands are executed when an event occurs while working on the file. They spread when the file is opened and executed. Macro viruses copy to the active template (usually the "Normal" template) when a file is opened. If the template is not opened, the file copies itself to a template opened in the background. Macro viruses can wreak havoc on a system, corrupting files, changing file types and some menu items, or making it so the template cannot be edited. The virus then copies itself to the new files that are opened or saved from the corrupted template. Macro viruses corrupt or delete files and even hide certain applications. By deleting the active template (or the default "Normal" template, in most cases) and corrupted files, these viruses can be removed.

## Antivirus Applications in Mac OS X

### VirusBarrier

VirusBarrier (Figure 2-2) is a nonintrusive antivirus software program that protects Macs against viruses of all types, including macro viruses and those targeting the OS, by constantly examining all the files that it reads and writes. It also patrols for suspicious activity that could be a sign of viruses acting on applications or other files. It can repair or quarantine the infected files and will display an alert. VirusBarrier can scan on-demand or in the background during normal operations. It has an option that skips checking files that have not been changed since the last scan.

Some of the other features of VirusBarrier include the following:

- Heuristic and behavioral analysis
- A designated "Trusted Zone" where background scanning on selected files or folders is disabled
- Improved logging for better scan analysis
- Scans can be scheduled at multiple times
- Scans can be launched automatically when volumes are mounted or when virus definitions are updated
- Command-line control for remote scans
- Archive scanning can be activated by archive type
- Scans files for Windows viruses (can be deactivated)
- Blocks virus execution
- Scans e-mails on receipt and sending
- File analysis by the Intego Virus Monitoring Center
- Contextual menu for quick scans
- Full logs can be saved and exported
- Intego widgets for program and update status
- Turbo Mode technology for faster scans
- Choice of alerts (voice, dialog, or e-mail)
- File analysis from the Dock

### McAfee VirusScan for Mac

McAfee VirusScan for Mac (Figure 2-3) guards against all types of viruses and malicious code, including new and unknown threats and emerging malware, that can affect OS X. VirusScan for Mac protects against viruses, worms, Trojans, and other malicious code that can infect systems. VirusScan for Mac offers policy enforcement for multiple files, directories, or volumes, including volumes on networked computers. On-demand and background scanning are both options in the McAfee product. VirusScan can scan compressed files, and using advanced heuristics and generic detection, it protects against new viruses and other threats.

### Sophos Endpoint Security and Control

Endpoint Security and Control warns of outbreak risk across a network via automatic e-mail alerts. It is an antivirus, antispyware, and client firewall. Sophos can protect Windows, Macs, and Linux machines, and provides cross-platform security and control for desktops, laptops, file servers, and mobile devices. It protects against viruses, spyware, and adware, and controls VoIP, IM, P2P, and games. As new computers join the network, security policies are automatically enforced. This eliminates the risk of unprotected computers compromising security policy. Endpoint Security and Control includes unique Behavioral Genotype protection, which guards against new, unforeseeable viruses, worms, and other threats.

![](img/0c79e6db97822eb68322dfe40d8564fe_73_0.png)

**Figure 2-2** This screen shows ViruBarrier server administrator options.

![](img/0c79e6db97822eb68322dfe40d8564fe_73_1.png)

**Figure 2-3** This screen shows the Scan & Clean option for DropScan.

### Norton Internet Security

Norton Internet Security (Figure 2-4) provides antivirus protection, Internet worm protection, a personal firewall, privacy protection, and parental control. It automatically detects and removes viruses, Trojan horses, and worms from Internet downloads and e-mail attachments. Some other features of NIS include the following:

- Personal firewall gives users control over all incoming and outgoing Internet traffic.
- Privacy control prevents information being sent without the user's permission.
- Automatically blocks hackers and identity thieves.
- Parental control blocks Web sites the user does not want his or her children to visit.
- Protects privacy and saves disk space by removing unwanted cookies and cache files.

## Mac OS X Security Tools

### MacScan

MacScan uses advanced detection methods to isolate and uninstall programs that could compromise security. Remote administration programs, used by hackers, allow remote access to a computer. These often go undetected, as antivirus software does not commonly protect from spyware. Using remote access, a hacker could monitor a user's activity with a keystroke recorder, manipulate files, or lock out a valid user. MacScan can blacklist tracking cookies to lock out these hackers and notifies users of any spyware applications that may be active. MacScan updates spyware definitions regularly to protect against the most current spyware. It also audits and protects systems from remote administrative programs that may have inadvertently been left on or installed. Figure 2-5 shows a MacScan application screen.

### ClamXav

ClamXav is a virus checker for Mac OS X. ClamXav is built upon the free ClamAV open-source command-line antivirus engine. This software has the ability to move files on a computer; therefore, it is vital that a complete
