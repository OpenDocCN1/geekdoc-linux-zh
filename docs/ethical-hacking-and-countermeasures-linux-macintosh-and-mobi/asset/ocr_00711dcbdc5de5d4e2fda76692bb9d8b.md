# Vulnerabilities in RFID-Enabled Credit Cards

RFID-enabled credit cards, in particular, are vulnerable to the following types of attacks:

+   • **Tracking attacks:** In a tracking attack, a merchant violates the expected use of the RFID credit card readers. A merchant may use the credit card reader to exploit the credit card and determine when it is used and if it is used with any other credit card.

+   • **Eavesdropping attacks:** In an eavesdropping attack, the attacker uses an antenna to read or record the communication between the tag and the reader; this happens only in live communications (during direct purchase at stores).

+   • **Skimming attacks:** In a skimming attack, the attacker may be a dishonest merchant or employee. The attacker uses a small skimming device, such as a magnetic stripe reader. A skimming device is installed behind the panel of a credit card reader, so when a customer pays with a credit or debit card, the attacker swipes that card on the machine, and the details are obtained from the card.

+   • **Replay-and-relay attacks:** In a replay and relay attack, the attacker sends an exact replay of the radio signals from the transponder's end, which records the past transaction between the RFID reader and the tag. An attacker in the middle of the network uses an authorized reader to get access to the authorized tag.

+   • **Cross-contamination attacks:** A cross-contamination attack occurs when an attacker acquires the cardholder's private information, such as the cardholder's name, number, and expiration date. Then the attacker can use these data to either create a magazine card, reread the stripe of an existing card, or perform a transaction that doesn't require an actual card, such as an online purchase.

# Countermeasures Used to Avoid RFID Attacks

If an organization implements RFID technology, there are a number of countermeasures the organization can take to protect the RFID devices. Individuals can also use certain countermeasures to protect themselves.

# RSA Blocker Tags

RSA blocker tags look like RFID tags and are the same size. When an attacker tries to scan tags without proper authorization, the RSA blocker tags emit radio frequencies that cause the RFID readers to shun data from the source because they believe they are receiving unwanted data or spam. This maintains a consumer's privacy.

# Kill Switches

Kill switches can be incorporated into the chips within RFID tags. If these switches are used, a command can be sent to deactivate the tag, and it can never be reactivated. Consumers are usually given the option of disabling the RFID tag before leaving a store; this helps to avoid profiling and stealth tracking.

# Cryptography

Developers have established lightweight versions of symmetric-key and public-key cryptography to protect RFID tags from attacks.

# Detection and Evasion

Consumers can use devices such as RFID Guardian to detect unauthorized RFID activity and then take their own evasive measures to avoid the attack.

# RFID Guardian

RFID Guardian is a portable, battery-powered device that mediates interactions between RFID readers and RFID tags. Its functions include auditing, key management, access control, and authentication.

RFID Guardian contains an RFID reader and tag emulation capabilities that enable it to audit and control RFID activity. It audits the activity by monitoring RFID scans and tags in its vicinity, which can indicate if there is any unauthorized RFID activity.

The security functionality within modern RFID tags may require the use of associated key values. These present logistical issues because the keys must be acquired, stored, and available for use at appropriate times.