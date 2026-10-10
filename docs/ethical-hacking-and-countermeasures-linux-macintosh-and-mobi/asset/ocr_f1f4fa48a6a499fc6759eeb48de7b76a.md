response will be RES1. The laptop sends RAND3 to the attacker, which is then forwarded to the mobile device. The mobile device then sends the response as REC3 to the attacker, which is forwarded to the laptop. The attacker begins the Bluetooth encryption by using the same challenge EN RAND recorded in the first phase. The attacker replays the EAP authentication sequence, which the laptop forwards to the WLAN access point controlled by the attacker. In the final stage, the attacker sends a message consisting of the compromised MSK recorded during the initial phase. The victim, believing it to be a legitimate network, sends encrypted data to the attacker's WLAN.

# Online PIN Cracking Attack

An online PIN cracking attack takes place when a target device has a fixed PIN. The attacker attempts to gain access to the target device by trying all possible PIN combinations until the correct number is discovered. Attackers use the following security analysis tools to crack the device's PIN:

+   - A PIN cracking script
+   - Brute-force BD_ADDR scanning script

# BTKeylogging Attack

An attacker can perform a BTKeylogging attack if the target device has a fixed PIN and the attacker knows its BD_ADDR. The attacker first uses the PIN cracking attack to discover the fixed PIN of the target device. The attacker needs to know the initial pairing sequence within the target keyboard and the target computer. The attacker then uses a protocol analyzer to intercept the information required to use the keyboard as a keylogger. The keylogger intercepts all information entered into the device and then decrypts it.

# BTVoiceBugBing Attack

Similar to a BTKeylogging attack, a BTVoiceBugBing attack records data entered into the targeted device. In this instance, the device is a headset, which can be used to record sound; the sound recording can then be exported and stored in WAV format for later use.

# Blueprinting

Blueprinting is when an attacker remotely accesses details about a target device. All Bluetooth-enabled devices have characteristics that are either unique or model specific. Blueprinting is the use of this information to discover the manufacturer and the device model. Based on these different characteristics, it is possible to determine the software that runs on the device and discover weaknesses in the device's security.

# Bluesmacking

A Bluesmacking attack is when an attacker sends an oversized ping packet to a victim's device. This causes a buffer overflow in the victim's device. This type of attack is similar to an ICMP ping of death.

# Denial-Of-Service Attack

Denial-of-service attacks curtail the ability of a device to access other Bluetooth resources or devices. This type of attack consumes all of a particular device's bandwidth so it is unable to communicate with other devices. The attacker pairs up with the victim's device and requests data. However, the attacker does not acknowledge when the data has been received; this causes the victim's device to retransmit the information. If the attacker has enough devices or requests enough data, he or she will tie up the victim's bandwidth. The victim will then be unable to communicate with other devices.

Another form of the denial-of-service attack is exhausting the battery of the target device by overwhelming it with data transfers. The attack can also be used to drain power from a device with a low battery level. The attacker has to be in radio proximity to achieve the attack, and he or she must work around any security roadblocks on the target device while requesting data.

# Bluedumping Attack

Bluedumping is an attack method used to cause a Bluetooth-enabled device to dump the stored link key, which gives the attacker a chance to sniff the key-exchange process. Sniffing the key-exchange process allows the attacker to obtain the encryption keys. The attacker must know the BD_ADDR of a set of paired devices to carry out a Bluedumping attack. The attacker spoofs one of the device's addresses and connects to the other