W32/VBaut-B creates registry entries under the following:

+   - HKCU\Software\Yahoo\PagerView\YMSGR_Launchcast
+   - HKCU\Software\Yahoo\PagerView\YMSGR_buzz

# Worm: HTTP W32.Drom

HTTP W32.Drom is a worm for Windows XP that downloads and executes malicious files on the compromised computer and spreads through removable storage devices. The following are actions a user should take to stop further damage:

+   - System restore should be disabled to prevent this worm from infecting the system.
+   - Antivirus software should be updated regularly.
+   - The complete system should be scanned after every infection.
+   - Values added to the registry should be deleted. There are

+   - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\
+   \ShellExecuteHooks\"{09B68AD9-FF66-3E63-636B-B693E2F6236}" = ""
+   - HKEY_CLASSES_ROOT\CLSID\{09B68AD9-FF66-3E63-636B-B693E2F6236}\InProcServer32\
+   \@" = "%ProgramFiles%\Internet Explorer\rdrivers.dll"
+   - HKEY_CLASSES_ROOT\CLSID\{09B68AD9-FF66-3E63-636B-B693E2F6236}\InProcServer32\
+   \ThreadingModel" = "Apartment"

# Hacking Tools

The following section explains the hacking tools that may be used during a USB attack.

# USBDumper

USBDumper is an application that, when installed on a system, runs a background process that silently copies files from any USB flash drive connected to it. The application is very dangerous because it only requires a user to double-click an executable, and once this occurs, the application runs in the background and automatically downloads the content of any USB drive connected to the system. This application can be a security risk when used alone, but the risk is increased when it is integrated with other tools. Hackers are integrating it with other tools (USB HackSaw) and scripts to send the downloaded contents to remote locations through encrypted e-mail or FTP. Figure 7-1 shows the interface for the USBDumper application.

# USB Switchblade

USB Switchblade is the result of a community project that merged various tools and techniques to take advantage of various Microsoft Windows security vulnerabilities, the majority of which were related to USB ports. The tool is used to silently recover information from Windows systems (such as password hashes, LSA secrets, IP information, and browser history), autostill information, and create a backdoor to the target system for later access. The tool exposes some very serious security vulnerabilities in Windows.

The tool takes advantage of a security hole in U3 drives that creates a virtual CD-ROM drive, which allows the Windows AutoRun feature to start (unless disabled on the target system). Even if AutoRun or a U3 drive is not used, the application can be started by executing a single script on the drive.

The most damaging feature of this tool is the ability to extract the password hashes from the target system and load them onto the drive for cracking later through the use of rainbow tables. The weakness of Windows LM hashes is fairly well known. With this application installed on a U3 drive, it only takes a few seconds for someone with malicious intent to plug the drive into an open USB port on a system and walk away with the passwords for that system.

The application also finds the browser history (for both IE and Firefox), including autostill information (exposing Web site passwords and other information), as well as AIM and MSN Messenger passwords. It also reveals product keys for some applications (mostly Microsoft applications). The tool also creates a ghost administrator account, and if the system is not behind a firewall, this account can function as a backdoor to the system.