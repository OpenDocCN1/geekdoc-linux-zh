able to insert code or commands in memory buffers which are read by processes that can execute administrative functions such as disabling security controls. In this case, the adversary could gain full control of the device and use that control to attack other systems.

# RFID Security and Privacy Threats

RFID uses the powerful capability of wireless identification to reveal the nature and location of physical objects. For this reason, RFID is a favorite target for attackers, who may use the following methods to carry out an attack:

+   - Sniffing
+   - Tracking
+   - Spoofing
+   - Replay attacks
+   - Denial-of-service attacks

# Sniffing

RFID tags are designed to be readable by any compliant reader; therefore, they are indiscriminate. But this leads to unauthorized readers reading the tags from a distance, which affects privacy. Attackers may collect RFID data by overhearing something on the wireless RFID channel or by eavesdropping on a wireless network. Unauthorized access of tag data leads to serious privacy implications. Medical and personal details can be revealed by the data collected using tags, which can cause denial of insurance coverage or employment of a person. If the collected data reveal information about a product, it can cause a loss of business.

# Tracking

Through the use of tracking, entire groups of people as well as individuals can be monitored by RFID technology. RFID facilitates secret monitoring of an individual's location and actions. RFID readers can be strategically placed to catch the unique responses from the RFID tags of individuals and to help identify the person associated with a tag. However, if there is a recurring group of tags without associated unique identifiers, an individual can still be monitored by LEO (low Earth orbit) constellations. An LEO constellation is a group of LEO satellites that have the ability to monitor and track RFID signals.

# Spoofing

A spoofing attack occurs when attackers mimic genuine RFID tags by writing suitably formatted data on blank RFID tags. Tag cloning is another type of spoofing attack that produces illegal copies of legitimate RFID tags. For example, in a supermarket the item tags can be replaced with similar tags so that thieves can purchase the items at cheaper prices. Similarly, digital signature transponders can be cloned, allowing attackers to unlock a DST-based car immobilization system and purchase gasoline.

# Replay Attacks

Relay devices interrupt and retransmit RFID queries, which the attackers use to attack various RFID applications. RFID-enabled license plates and e-Plates are examples of current RFID systems that are vulnerable to attack by a relay device. The encrypted code of these active e-Plates is stored in the local government's vehicle database. When an attacker scans the license plates of other cars, he or she records the encrypted identifier and replays it later.

# Denial-Of-Service Attacks

To work properly, RFID systems must have properly managed RFID tags and back-end databases; otherwise, attackers can exploit them to carry out a denial-of-service attack. Thieves can steal RFID-tagged items either by removing the tags or by placing them in a foil-lined booster bag that blocks RFID query signals and temporarily deactivates the items. If the tags are removed from RFID tagged items and then wrapped in a foil-lined booster bag, the tags cannot be detected by readers. If attackers remove the RFID tags and place them on other items, the RFID system records useless data. Another denial-of-service attack can occur if the attacker floods the RFID system by providing more data than it can handle normally.