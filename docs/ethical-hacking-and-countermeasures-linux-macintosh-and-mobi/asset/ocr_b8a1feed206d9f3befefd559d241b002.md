consumer’s identity, such as an RFID-enabled identification card, someone may be able to surreptitiously read both tags to establish an association between the purchased item and the consumer’s identity that did not exist previously. As people possess more tagged items and readers become more prevalent in everyday life, the potential for complex associations and inferences increases.

Other factors that impact the level of privacy risk include the following:

+   - Whether personal information is stored on tags
+   - Whether the tagged items are considered personal (e.g., pharmaceuticals, devices that would reveal a medical condition, or a book that might reveal a political or religious affiliation)
+   - The likelihood that the tag will be in the proximity of compatible readers
+   - The length of time records are retained in analytic or archival systems
+   - The effectiveness of RFID security controls, in particular:
+       - The efficiency of tag memory access control and authentication mechanisms
+       - The ability of tags to be disabled after their use in a business process has been completed
+   - The ability of users to effectively shield tags to prevent unauthorized read transactions

# Externality Risk

RFID systems typically are not isolated from other systems and assets in the enterprise. Every connection point between the RFID system and something outside the RFID system represents a potential vulnerability for the entity on the other side of the connection, whether that is an application process, a valued asset, or a person. Externality risks are present for both the RF and enterprise sub- elements of an RFID system. The main externality risk for the RF subsystem is the hazards of electromagnetic radiation, which could range from adverse human health effects to the ignition of a combustible material, such as fuel or ordnance. The main externality risk for the enterprise subsystem is successful computer network attacks on networked devices and applications. Computer network attacks can involve malware (e.g., worms and viruses) or attack tools that exploit software vulnerabilities and configuration weaknesses to gain access to systems, perform a denial of service, or cause other damage. The impact of computer network attacks can range from performance degradation to the complete compromise of a mission-critical application.

# Hazards of Electromagnetic Radiation

RFID technology, like any other radio technology, relies on the use of electromagnetic radiation to communicate information. The potential risks of electromagnetic radiation include the following:

+   - Hazards of electromagnetic radiation to people (HERP)
+   - Hazards of electromagnetic radiation to ordnance (HERO)
+   - Hazards of electromagnetic radiation to fuel (HERF)
+   - Hazards of electromagnetic radiation to other materials including medical supplies such as blood products, vaccines, and pharmaceuticals

# Computer Network Attacks

RFID technology represents a new attack vector on an enterprise network. Once RFID systems are implemented, attackers can possibly reach non-RFID and enterprise subsystem computers through a reader. However, no such attack is known to have successfully occurred. If the system involves wireless handheld readers, then the wireless link between the reader and the networked middleware servers is another point of entry that could be used by an attacker. Once RFID servers are compromised, they can be used to launch attacks on other networked systems. Attack possibilities include the introduction of malware (e.g., a worm or virus) or the exploits of a single adversary compromising one computer at a time. Once additional systems are compromised, all types of adverse consequences to the IT infrastructure are possible, including loss of confidentiality, integrity, and availability.

While the risk of network compromise through an RFID interface is considered low, it is possible, especially as the number of RFID reader, middleware, and enterprise applications increases. RFID air-interface protocols do not support the execution of remote commands on the RFID interface. However, if the reader accepts data formats outside those expected by the protocol, then an adversary could conceivably exploit a buffer overflow vulnerability on a reader by sending noncompliant data. If the system is poorly designed, the adversary may be