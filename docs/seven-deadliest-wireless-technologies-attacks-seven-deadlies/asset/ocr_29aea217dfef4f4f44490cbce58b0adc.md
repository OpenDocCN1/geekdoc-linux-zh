# Radio Frequency Identification Attacks

# INFORMATION IN THIS CHAPTER

+   - RFID Basics
+   - RFID Risks
+   - Physical Access Control
+   - RFID Meets Crypto

Radio Frequency Identification (RFID) is a technology that everyone hears about but most people do not fully understand. Its name is thrown about in terms of efficiency and modernization of commerce, and at the same time, it is associated with Big Brother and privacy invasion. In terms of security, it is a technology that is only starting to come into maturity for security, but it is so often misunderstood and the risks so underestimated that security is often completely forgotten.

Most modern office buildings have done away with physical keys in favor of proximity card systems. We've all seen them, the cards on lanyards being waved in front of the readers at doors like some magical "open sesame" command for the modern age.

At the DEFCON 17 hacker conference, it is widely known that a fair number of attendees are federal agents, some under their own names and some undercover, but all there to learn. There was quite a stir among many of them this year: those who thought they may have had their proximity cards cloned. A project, undertaken by Adam Laurie (major malfunction) and Zac Franke to raise awareness about RFID vulnerabilities, gathered more data than expected.

Their project consisted of a 125-kHz RFID reader and a large antenna hooked to a laptop. The laptop also had a webcam attached to it. All of this was in plain sight on a table in the conference area. Anyone walking up to the table with a compatible RFID card on their person would have it scanned and their picture taken with the webcam. The idea was to then scrub the data and put it on the "wall of sheep," joining other attendees who used insecure protocols to login on the conference network.