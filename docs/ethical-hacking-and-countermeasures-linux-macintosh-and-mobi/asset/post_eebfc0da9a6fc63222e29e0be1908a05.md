
response will be RES1. The laptop sends RAND3 to the attacker, which is then forwarded to the mobile device. The mobile device then sends the response as REC3 to the attacker, which is forwarded to the laptop. The attacker begins the Bluetooth encryption by using the same challenge EN RAND recorded in the first phase. The attacker replays the EAP authentication sequence, which the laptop forwards to the WLAN access point controlled by the attacker. In the final stage, the attacker sends a message consisting of the compromised MSK recorded during the initial phase. The victim, believing it to be a legitimate network, sends encrypted data to the attacker's WLAN.

## Online PIN Cracking Attack

An online PIN cracking attack takes place when a target device has a fixed PIN. The attacker attempts to gain access to the target device by trying all possible PIN combinations until the correct number is discovered. Attackers use the following security analysis tools to crack the device's PIN:

- A PIN cracking script
- Brute-force BD_ADDR scanning script

## BTKeylogging Attack

An attacker can perform a BTKeylogging attack if the target device has a fixed PIN and the attacker knows its BD_ADDR. The attacker first uses the PIN cracking attack to discover the fixed PIN of the target device. The attacker needs to know the initial pairing sequence within the target keyboard and the target computer. The attacker then uses a protocol analyzer to intercept the information required to use the keyboard as a keylogger. The keylogger intercepts all information entered into the device and then decrypts it.

## BTVoiceBugBing Attack

Similar to a BTKeylogging attack, a BTVoiceBugBing attack records data entered into the targeted device. In this instance, the device is a headset, which can be used to record sound; the sound recording can then be exported and stored in WAV format for later use.

## Blueprinting

Blueprinting is when an attacker remotely accesses details about a target device. All Bluetooth-enabled devices have characteristics that are either unique or model specific. Blueprinting is the use of this information to discover the manufacturer and the device model. Based on these different characteristics, it is possible to determine the software that runs on the device and discover weaknesses in the device's security.

## Bluesmacking

A Bluesmacking attack is when an attacker sends an oversized ping packet to a victim's device. This causes a buffer overflow in the victim's device. This type of attack is similar to an ICMP ping of death.

## Denial-Of-Service Attack

Denial-of-service attacks curtail the ability of a device to access other Bluetooth resources or devices. This type of attack consumes all of a particular device's bandwidth so it is unable to communicate with other devices. The attacker pairs up with the victim's device and requests data. However, the attacker does not acknowledge when the data has been received; this causes the victim's device to retransmit the information. If the attacker has enough devices or requests enough data, he or she will tie up the victim's bandwidth. The victim will then be unable to communicate with other devices.

Another form of the denial-of-service attack is exhausting the battery of the target device by overwhelming it with data transfers. The attack can also be used to drain power from a device with a low battery level. The attacker has to be in radio proximity to achieve the attack, and he or she must work around any security roadblocks on the target device while requesting data.

## Bluedumping Attack

Bluedumping is an attack method used to cause a Bluetooth-enabled device to dump the stored link key, which gives the attacker a chance to sniff the key-exchange process. Sniffing the key-exchange process allows the attacker to obtain the encryption keys. The attacker must know the BD_ADDR of a set of paired devices to carry out a Bluedumping attack. The attacker spoofs one of the device's addresses and connects to the other device. When the victim's device requests authentication, the attacker's device responds with an HCL_Link_Key_Request_Negative_Reply instead of the link key. This causes the target device to delete its own link key and to go into pairing mode.

## Bluetooth Hacking Tools

### BTScanner

BTScanner is designed to extract as much information as possible from a Bluetooth-enabled device without pairing. Using the gathered information, it is possible to make educated guesses regarding the host’s device type. Figure 5-1 shows a screenshot from BTScanner.

### Bluesnarfer

Bluesnarfer anonymously connects to any mobile device vulnerable to Bluesnarfing and downloads confidential information, including the device’s phonebook, without the owner’s knowledge or consent.

### Bluediving

Bluediving is a Bluetooth penetration-testing suite. It implements attacks such as Bluebugging, Bluesnarfing, and Bluesmacking.
It also executes the following actions:

- Bluetooth address spoofing
- Implements tools like carwhisperer, bss, L2CAP packetgenerator, L2CAP connection resetter, and RFCOMM scanner
- Greeplaque scanning mode (using more than one human-computer interface device)

Figure 5-2 shows a screenshot from Bluediving.

## T-BEAR (Transient Bluetooth Environment AuditoR)

T-BEAR is a suite of applications designed to improve and manage the security of Bluetooth environments. The suite consists of the following utilities:

- *btsniff*: A Bluetooth sniffer to be used with a GNU radio
- *btkbsniff*: Designed to monitor data from a Bluetooth-enabled keyboard

![](img/0c79e6db97822eb68322dfe40d8564fe_132_0.png)

**Figure 5-1** BTScanner extracts information from Bluetooth-enabled devices.

![](img/0c79e6db97822eb68322dfe40d8564fe_133_0.png)

Source: http://www.icewalkers.com/Linux/Software/529650/Bluediving.html. Accessed 4/2/08.

**Figure 5-2** Bluediving implements a number of different Bluetooth attacks.

![](img/0c79e6db97822eb68322dfe40d8564fe_133_1.png)

Source: http://www.mruni.com/~en/security_tools_btc Rack.php. Accessed 4/2/08.

**Figure 5-3** BTCrack is a PIN and link-key cracker.

- *btvsniff*: Designed to monitor voice data from Bluetooth headsets
- *btcrackpin*: A program that attempts to crack a PIN associated with encrypted Bluetooth data
- *thsearch*: A locator for hidden Bluetooth devices

### BTCrack

BTCrack reconstructs a device’s Bluetooth PIN and link key from data sniffed during a pairing session. The reconstructed PIN can authenticate against a device in pairing mode, while the link key is used to get complete access to the master and the slave without any interaction from the user of these devices. An attacker can use the resulting link key to decrypt the data stream between the two devices. Figure 5-3 shows a screenshot from BTCrack.

### Blueover

Blueover is a tool that runs on J2ME-enabled cell phones. It audits whether or not a particular Bluetooth device is vulnerable to a Bluesnarfing attack.

### Hidattack

Hidattack attacks the Bluetooth human interface device (HID) protocol. The *HID protocol* deals with two units: the device, which is the entity that directly interacts with a user, and the host that communicates with the device and receives input data from the device on actions performed by the user. Hidattack enables an attacker who gets a target device's PIN to decrypt its traffic and gain full access to each of the connected Bluetooth devices.

An attacker's Bluetooth device scans for a PC that has an active Bluetooth HID driver running. Once a victim's PC is found, the attacker can use his or her own keyboard to enter information and execute commands on the victim's PC. The attacker then has full control of the device.

In HID, there are two instances: the host (e.g., a PC, laptop, PDA, or cell phone) and the device used to input information into the host (e.g., a keyboard or mouse). The instances are connected through two channels: the control channel and the interrupt channel. The control channel is used for signaling, and the interrupt channel is used for data transfer.

## Viruses and Worms

### Cabir and Mabin

The Cabir worm infects Symbian mobile phones supporting the S60 platform. A file named caribe.sis is sent to the telephone's message inbox. When the user installs caribe.sis, the worm is activated. The application caribe.app is automatically executed after the caribe.sis file is installed. The worm uses the infected telephone to find other devices, which it infects in the same way. The worm will only send a new caribe.sis file to the first device it finds and then will lock the telephone from searching for more victims. Once a device is infected, the worm will continuously try to spread through the system. Disabling Bluetooth does not have any effect.

The Mabin worm is identical to Cabir, infecting Symbian S60 devices and using a file named caribe.sis. However, it can infect the target device using either Bluetooth or MMS messages.

### Worm.SymbOS.Lasco.a

Worm.SymbOS.Lasco.a is a worm that can infect PDAs and mobile phones running the Symbian operating system. As with Cabir, Lasco.a reproduces using Bluetooth connections. When executed, it scans the disk for SIS archives and attempts to infect those files by inserting its code.

## Bluetooth Security Tools

### BlueWatch

BlueWatch is an application that identifies all Bluetooth-enabled devices, their communications and their connectivity within a given area. It provides important information about each device, such as its device class, manufacturer, and signal strength. BlueWatch also identifies services available on each device, including network access, fax, and audio. It can detect devices that are misconfigured, unauthenticated, or unencrypted. It monitors Bluetooth traffic and security threats. This tool can run on any Bluetooth-enabled computer or PDA running Windows 2000, XP, or CE.

### BlueSweep

BlueSweep is a Bluetooth finder and freeware utility that identifies any nearby Bluetooth device, detecting the services it runs and how it connects to other devices. It provides a simple way to enter a Bluetooth device and identify security issues that might otherwise go unnoticed. Figure 5-4 shows a screenshot from BlueSweep.

### Bluekey

Bluekey is a security program that uses Bluetooth to secure a PDA. It uses Bluetooth devices to unlock the PDA. Bluekey automatically tries to authenticate a user when it is turned on; the user doesn't have to remember any passwords or key combinations. Bluekey has multiple profiles and modes for full flexibility.
