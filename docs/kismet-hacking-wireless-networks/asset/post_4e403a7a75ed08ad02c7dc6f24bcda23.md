
# 4 FREE BOOKLETS
YOUR SOLUTIONS MEMBERSHIP

![](img/d6ac176c353d2b7687c1186a140180a1_0_0.png)

# Kismet Hacking

The Only Book on the Industry Standard for Examining Wireless Network Traffic!

- Complete Coverage of Kismet’s NewCore
- Special Section on Creating Wireless Intrusion Detection Systems
- Learn All About Drones, IDS Setup, and GPSmap

Brad Haines (Renderrman)
Frank Thornton (Thorn)

# Kismet Hacking

Brad ‘RenderMan’ Haines
Michael J. Scheerer
Frank Thornton

Elsevier, Inc., the author(s), and any person or firm involved in the writing, editing, or production (collectively “Makers”) of this book (“the Work”) do not guarantee or warrant the results to be obtained from the Work. There is no guarantee of any kind, expressed or implied, regarding the Work or its contents. The Work is sold AS IS and WITHOUT WARRANTY. You may have other legal rights, which vary from state to state.

In no event will Makers be liable to you for damages, including any loss of profits, lost savings, or other incidental or consequential damages arising out from the Work or its contents. Because some states do not allow the exclusion or limitation of liability for consequential or incidental damages, the above limitation may not apply to you.

You should always use reasonable care, including backup and other appropriate precautions, when working with computers, networks, data, and files.

Syngress Media®, Syngress®, “Career Advancement Through Skill Enhancement®”, “Ask the Author UPDATE®”, and “Hack Proofing®”, are registered trademarks of Elsevier, Inc. “Syngress: The Definition of a Serious Security Library™”, “Mission Critical™”, and “The Only Way to Stop a Hacker is to Think Like One™” are trademarks of Elsevier, Inc. Brands and product names mentioned in this book are trademarks or service marks of their respective companies.

| KEY | SERIAL NUMBER |
|:----|:--------------|
| 001 | HJR1TCV764 |
| 002 | PO98T3DSFG |
| 003 | 829KMBNJH2 |
| 004 | BAL923457U |
| 005 | CVPLQ6WQ23 |
| 006 | VBPR65ST55 |
| 007 | HJJ863WD3E |
| 008 | 298TGWYMMK |
| 009 | 629MPPSDJT |
| 010 | IWMQ2295T6 |

PUBLISHED BY

Syngress Publishing, Inc.
Elsevier, Inc.

30 Corporate Drive
Burlington, MA 01803

Kismet Hacking

Copyright © 2008 by Elsevier, Inc. All rights reserved. Printed in the United States of America. Except as permitted under the Copyright Act of 1976, no part of this publication may be reproduced or distributed in any form or by any means, or stored in a database or retrieval system, without the prior written permission of the publisher, with the exception that the program listings may be entered, stored, and executed in a computer system, but they may not be reproduced for publication.

Printed in the United States of America

1 2 3 4 5 6 7 8 9 0

ISBN 13: 978-1-59749-117-4

Page Layout and Art: SPi Publishing Services

Copy Editor: Judy Eby

For information on rights, translations, and bulk sales, contact Matt Pedersen, Commercial Sales Director and Rights, at Syngress Publishing; email m.pedersen@elsevier.com.

![](img/d6ac176c353d2b7687c1186a140180a1_3_0.png)

## Contributing Authors

Brad ‘RenderMan’ Haines is one of the more visible and vocal members of the wardriving community, appearing in various media outlets and speaking at conferences several times a year. Render is usually near by on any wardriving and wireless security news, often causing it himself. His skills have been learned in the trenches working for various IT companies as well as his involvement through the years with the hacking community, sometimes to the attention of curious Canadian and American intelligence agencies. A firm believer in the hacker ethos and promoting responsible hacking and sharing of ideas, he wrote the ‘Stumbler ethic’ for beginning wardrivers and greedily enjoys speaking at corporate conferences to dissuade the negative image of hackers and wardrivers.

His work frequently borders on the absurd as his approach is usually one of ignoring conventional logic and just doing it. He can be found in Edmonton, Alberta, Canada, probably taking something apart.

Michael J. Scheerer is an active-duty Naval Flight Officer and Electronic Countermeasures Officer with the U.S. Navy. He flew combat missions during Operations Enduring Freedom, Southern Watch, and Iraqi Freedom. He later took his electronic warfare specialty to Iraq, where he embedded on the ground with Army units to lead the counter-IED fight. He currently serves as an instructor of Naval Science at the Pennsylvania State University Naval Reserve Officer Training Corps Unit, University Park, PA.

Michael is an active member of the Church of WiFi and has spoken at Shmoocon, DEFCON, and Penn State’s Security Day, as well as other forums. His work has been cited in Forbes, InfoWorld and Wired.

Michael is an alumnus of Bloomsburg University where he studied Political Science and Georgetown University where he obtained his degree in National Security Studies. While at Penn State, he is actively involved in IT issues. He is a licensed amateur radio operator, moderator of the Church of WiFi and Remote-Exploit Forums, and a regular on the DEFCON and NetStumbler forums.

Frank Thornton runs his own technology consulting firm, Blackthorn Systems, which specializes in wireless networks. His specialties include wireless network architecture, design, and implementation, as well as network troubleshooting and optimization. An interest in amateur radio helped him bridge the gap between computers and wireless networks. Having learned at a young age which end of the soldering iron was hot, he has even been known to repair hardware on occasion. In addition to his computer and wireless interests, Frank was a law enforcement officer for many years. As a detective and forensics expert he has investigated approximately one hundred homicides and thousands of other crime scenes. Combining both professional interests, he was a member of the workgroup that established ANSI Standard “ANSI/NIST-CSL 1-1993 Data Format for the Interchange of Fingerprint Information.” He co-authored *RFID Security* (Syngress Publishing, ISBN: 1597490474), *WarDriving: Drive, Detect, and Defend: A Guide to Wireless Security* (Syngress, ISBN: 193183603), as well as contributed to *IT Ethics Handbook: Right and Wrong for IT Professionals* (Syngress, ISBN: 1931836140) and *Game Console Hacking: Xbox, PlayStation, Nintendo, Atari, & Gamepark 32* (ISBN: 1931836310). He resides in Vermont with his wife.

# Contents

- **Chapter 1 Introduction to Wireless Networking, Wardriving, and Kismet**... 1
    - Exploring Past Discoveries That Led to Wireless... 2
        - Discovering Electromagnetism... 2
        - Exploring Conduction... 3
        - Inventing the Radio... 4
        - Mounting Radio-Telephones in Cars... 5
        - Inventing Computers and Networks... 6
        - Inventing Cell Phones... 7
    - Exploring Present Applications for Wireless... 9
        - Applying Wireless Technology to Vertical Markets... 10
            - Using Wireless in Delivery Services... 10
            - Using Wireless for Public Safety... 10
            - Using Wireless in the Financial World... 11
            - Using Wireless in the Retail World... 11
            - Using Wireless in Monitoring Applications... 12
        - Applying Wireless Technology to Horizontal Applications... 12
            - Using Wireless in Messaging... 12
            - Using Wireless for Mapping... 12
            - Using Wireless for Web Surfing... 13
            - Using Bluetooth Wireless Devices... 13
    - Introduction to Wardriving... 14
        - The Origins of Wardriving... 14
        - Definition... 14
        - The Terminology History of Wardriving... 15
        - Wardriving Misconceptions... 15
        - The Truth about Wardriving... 16
        - The Legality of Wardriving... 17
    - Introduction to Wardriving with Linux... 17
        - Preparing Your System to Wardrive... 17
        - Preparing the Kernel... 17
        - Preparing the Kernel for Monitor Mode... 18
        - Preparing the Kernel for a Global Positioning System... 21
