Vend or-provided software development kits consist of source code, header files, and information about the design and structure of the USB device. This information is stored on the serial EEPROM of the device that, because of a design flaw, allows access to private information. When initiating a software attack, attackers attempt to obtain this private information by using custom device drivers and commercial USB protocol analyzers to examine the communication channels between the USB device and the host computer. The attackers can use this information to analyze and determine the possibility of a successful attack, and then use one of the following methods:

+   - *Attempt to brute-force a password:* The USB drive is accessed by analyzing and determining the administrator's MKEY value or the genuine user password or PIN.
+   - *Send incorrect and known erroneous USB packets to the USB drive:* Due to a design flaw, the USB drive may allow transmission of the content of protected memory areas.

Once the attack is complete, the results can be replicated to other devices.

# # Windows Buffer Overflow Attack

USB devices plugged into computers with Windows 32-bit operating systems such as Windows Vista, XP, and 2000 are in danger of another type of attack. Buffer overflow vulnerabilities in a USB device driver can allow an attacker to bypass Windows security and gain administrative access on the host machine. An attacker who knows about these vulnerabilities can program a USB drive to pose as the kind of device that uses a vulnerable driver.

Once this is done, the attacker plugs the device into the host system, and when the flawed driver is loaded, the attacker gains the default PIN and the legitimate user's credentials stored on the serial EEPROM of the device. The attacker can use this information to exploit the system and gain access to the locked workstation.

These attacks need physical access to the system and can be prevented through the use of USB security tools, which recognize when a USB device is plugged into the host computer or its network and would prevent the exploitation.

# # Viruses and Worms

The following sections explain some of the viruses and worms that affect USB devices.

# ## Virus: W32/Madang-Fam

W32/Madang-Fam is a family of viruses that infect the Windows platform and can be spread through removable storage devices. These viruses search all drives and connected network shares to locate files with an EXE or SCR extension. The viruses connect to remote Web sites and download other malicious code. Some of these files may place the file Serverx.exe, which is infected with the virus, into the Windows system folder. The viruses modify the system registry by creating the following registry entry in HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run to run the Serverx.exe file on startup:

```
"Serverx" = <System>\Serverx.exe
```

The viruses may also attempt to run the files <System>\setupx.exe and <System>\Update.exe or to inject themselves into the kernel or another currently running process.

# ## Worm and Virus: W32/Hasnot-A

W32/Hasnot-A is a worm and companion virus for the Windows platform that spreads through network shares and removable storage devices, including USB drives. The worm attempts to copy itself to writeable devices accessible to the infected machine. It hides files and folders by appending the original names of files or folders to a copy of itself. It copies itself to the root folder drive as Skynet.exe and adds an Autorun.inf file. Once the drive is mounted, the Autorun.inf file is designed to run Skynet.exe, which spreads the worm. When first run, this worm copies itself to the following files:

+   - <Root>\Dokumente und Einstellungen.exe
+   - <Root>\Documenti e Impostazioni.exe
+   - <Root>\Documents and Settings.000.exe
+   - <Root>\Documents and Settings.exe