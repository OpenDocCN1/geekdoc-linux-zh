
# DevOps Troubleshooting

## Linux® Server Best Practices

**Kyle Rankin**

![](img/362b627595d4f10aae346cc0cc8e74eb_0_0.png)

# DevOps
Troubleshooting

*This page intentionally left blank*

# DevOps Troubleshooting

**Linux® Server Best Practices**

**Kyle Rankin**

**Addison-Wesley**

Upper Saddle River, NJ • Boston • Indianapolis • San Francisco
New York • Toronto • Montreal • London • Munich • Paris • Madrid
Capetown • Sydney • Tokyo • Singapore • Mexico City

Many of the designations used by manufacturers and sellers to distinguish their products are claimed as trademarks. Where those designations appear in this book, and the publisher was aware of a trademark claim, the designations have been printed with initial capital letters or in all capitals.

The author and publisher have taken care in the preparation of this book, but make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. No liability is assumed for incidental or consequential damages in connection with or arising out of the use of the information or programs contained herein.

The publisher offers excellent discounts on this book when ordered in quantity for bulk purchases or special sales, which may include electronic versions and/or custom covers and content particular to your business, training goals, marketing focus, and branding interests. For more information, please contact:

U.S. Corporate and Government Sales
(800) 382-3419
corpsales@pearsonedtechgroup.com

For sales outside the United States, please contact:

International Sales
international@pearson.com
Visit us on the Web: informit.com/aw
Cataloging-in-Publication Data is on file with the Library of Congress.

| Role | Name |
| :--- | :--- |
| Editor-in-Chief | Mark Taub |
| Executive Editor | Debra Williams Cauley |
| Development Editor | Michael Thurston |
| Managing Editor | John Fuller |
| Project Editor | Elizabeth Ryan |
| Copy Editor | Rebecca Rider |
| Indexer | Richard Evans |
| Proofreader | Diane Freed |
| Technical Reviewer | Bill Childers |
| Publishing Coordinator | Kim Boedighheimer |
| Compositor | Kim Arney |

Copyright © 2013 Pearson Education, Inc.

All rights reserved. Printed in the United States of America. This publication is protected by copyright, and permission must be obtained from the publisher prior to any prohibited reproduction, storage in a retrieval system, or transmission in any form or by any means, electronic, mechanical, photocopying, recording, or likewise.

To obtain permission to use material from this work, please submit a written request to Pearson Education, Inc., Permissions Department, One Lake Street, Upper Saddle River, New Jersey 07458, or you may fax your request to (201) 236-3290.

ISBN-13: 978-0-321-83204-7
ISBN-10: 0-321-83204-3

Text printed in the United States on recycled paper at RR Donnelley in Crawfordsville, Indiana.
First printing, November 2012

This book wouldn’t be possible without the support of my wife, Joy, who once again helped me manage my time so I could complete the book, only this time while carrying our first child, Gideon. I’d also like to dedicate this book to my son, Gideon, who so far is easier to troubleshoot than any server.

*This page intentionally left blank*

# Contents

- Preface xii
- Acknowledgments xix
- About the Author xxi

### CHAPTER 1 Troubleshooting Best Practices 1

- Divide the Problem Space 3
- Practice Good Communication When Collaborating 4
- Conference Calls 4
- Direct Conversation 5
- Email 6
- Real-Time Chat Rooms 7
- Have a Backup Communication Method 8
- Favor Quick, Simple Tests over Slow, Complex Tests 8
- Favor Past Solutions 9
- Document Your Problems and Solutions 10
- Know What Changed 12
- Understand How Systems Work 13
- Use the Internet, but Carefully 14
- Resist Rebooting 15

### CHAPTER 2 Why Is the Server So Slow? Running Out of CPU, RAM, and Disk I/O 17

- System Load 18
- What Is a High Load Average? 20
- Diagnose Load Problems with top 20
- Make Sense of top Output 22
- Diagnose High User Time 24
- Diagnose Out-of-Memory Issues 25
- Diagnose High I/O Wait 27
- Troubleshoot High I/O Load after the Fact 29
- Configure systat 30
- View CPU Statistics 30
- View RAM Statistics 31
- View Disk Statistics 32
- View Statistics from Previous Days 33

### CHAPTER 3 Why Won't the System Boot? Solving Boot Problems 35

- The Linux Boot Process 36
- The BIOS 36
- GRUB and Linux Boot Loaders 37
- The Kernel and init 38
- /sbin/init 39
- BIOS Boot Order 45
- Fix GRUB 47
- No GRUB Prompt 47
- Stage 1.5 GRUB Prompt 48
- Misconfigured GRUB Prompt 49
- Repair GRUB from the Live System 49
- Repair GRUB with a Rescue Disk 50
- Disable Splash Screens 51
- Can't Mount the Root File System 51
- The Root Kernel Argument 52
- The Root Device Changed 52
- The Root Partition Is Corrupt or Failed 55
- Can't Mount Secondary File Systems 55

### CHAPTER 4 Why Can't I Write to the Disk? Solving Full or Corrupt Disk Issues 57

- When the Disk Is Full 58
- Reserved Blocks 59
- Track Down the Largest Directories 59
- Out of Inodes 61
- The File System Is Read-Only 62
- Repair Corrupted File Systems 63
- Repair Software RAID 64

### CHAPTER 5 Is the Server Down? Tracking Down the Source of Network Problems 67

- Server A Can't Talk to Server B 68
- Client or Server Problem 69
- Is It Plugged In? 69
- Is the Interface Up? 70
- Is It on the Local Network? 71
- Is DNS Working? 72
- Can I Route to the Remote Host? 74
- Is the Remote Port Open? 76
- Test the Remote Host Locally 76
- Troubleshoot Slow Networks 78
- DNS Issues 79
- Find the Network Slowdown with traceroute 80
- Find What Is Using Your Bandwidth with iftop 81
- Packet Captures 83
- Use the tcpdump Tool 84
- Use Wireshark 88

### CHAPTER 6 Why Won't the Hostnames Resolve? Solving DNS Server Issues 95

- DNS Client Troubleshooting 95
- No Name Server Configured or Inaccessible Name Server 95
- Missing Search Path or Name Server Problem 97
- DNS Server Troubleshooting 98
- Understanding dig Output 98
- Trace a DNS Query 101
- Recursive Name Server Problems 104
- When Updates Don't Take 107

### CHAPTER 7 Why Didn't My Email Go Through? Tracing Email Problems 120

- Trace an Email Request 120
- Understand Email Headers 123
- Problems Sending Email 125
- Client Can't Communicate with the Outbound Mail Server 126
- Outbound Mail Server Won't Allow Relay 130
- Outbound Mail Server Can't Communicate with the Destination 131
- Problems Receiving Email 135
- Telnet Test Can't Connect 136
- Telnet Can Connect, but the Message Is Rejected 137
- Poke Through the Mail Logs 138

### CHAPTER 8 Is the Website Down? Tracking Down Web Server Problems 141

- Is the Server Running? 143
- Is the Remote Port Open? 143
- Test the Remote Host Locally 144
- Test a Web Server from the Command Line 146
- Test Web Servers with Curl 146
- Test Web Servers with Telnet 148
- HTTP Status Codes 149
- 1xx Informational Codes 150
- 2xx Successful Codes 150
- 3xx Redirection Codes 151
- 4xx Client Error Codes 152
- 5xx Server Error Codes 153
- Parse Web Server Logs 154
- Get Web Server Statistics 158
- Solve Common Web Server Problems 163
- Configuration Problems 163
- Permissions Problems 164
- Sluggish or Unavailable Web Server 166

### CHAPTER 9 Why Is the Database Slow? Tracking Down Database Problems 171

- Search Database Logs 172
- MySQL 173
- PostgreSQL 173
- Is the Database Running? 174
- MySQL 174
- PostgreSQL 175
- Get Database Metrics 177
- MySQL 177
- PostgreSQL 179
- Identify Slow Queries 182
- MySQL 182
- PostgreSQL 183
