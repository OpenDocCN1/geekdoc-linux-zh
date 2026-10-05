
# TCP/IP and Linux Protocol Implementation

Systems Code for the Linux Internet

Jon Crowcroft
Iain Phillips

# AN LEABHARLANN/LIBRARY
GALWAY-MAYO INSTITUTE OF TECHNOLOGY

This book should be returned not later than the last date shown below. It may be renewed if not requested by another borrower.

The fine for an overdue book is 10p per day.

| DATE DUE | DATE DUE | DATE DUE | DATE DUE |
| --- | --- | --- | --- |
| 06 FEB 2003 | | | |
| 21 OCT 2005 | | | |

059079
004.62
059079
b1073952X

# TCP/IP and Linux Protocol Implementation:
Systems Code for the Linux Internet

Jon Crowcroft
Iain Phillips

Wiley Computer Publishing
John Wiley & Sons, Inc.
NEW YORK • CHICHESTER • WEINHEIM • BRISBANE • SINGAPORE • TORONTO

Publisher: Robert Ipsen
Editor: Carol A. Long
Assistant Editor: Adaobi Obi
Managing Editor: Michele Frederick
Text Design & Composition: Interactive Composition Corporation

Designations used by companies to distinguish their products are often claimed as trademarks. In all instances where John Wiley & Sons, Inc., is aware of a claim appear in initial capital or ALL CAPITAL LETTERS. Readers, however, should contact the appropriate companies for more complete information regarding trademarks and registration.

This book is printed on acid-free paper.

Copyright © 2002 by Jon Crowcroft, Iain Phillips. All rights reserved.

Published by John Wiley & Sons, Inc. New York

No part of this publication may be reproduced, stored in a retrieval system or transmitted in any form or by any electronic, mechanical, photocopying, recording, scanning, or otherwise, as permitted under Sections 107 or 108 of the 1976 United States Copyright Act, without either the prior written permission of the Publisher, or authorization through payment of the per-copy fee to the Copyright Clearance Center, 222 Roosevelt Drive, Denver, MA 01923, (978) 750-8400, fax (978) 750-4744. Requests to the Publisher for permission should be addressed to the Permissions Department, John Wiley & Sons, Inc., 605 Third Avenue, New York, NY 10158-0012, (212) 850-6011, fax (212) 850-6008, E-Mail: PERMQ@WILEY.COM.

This publication is designed to provide accurate and authoritative information in regard to the subject matter covered. It is sold with the understanding that the publisher is not engaged in professional services. If professional advice or other expert assistance is required, the services of a competent professional person should be sought.

Library of Congress Cataloging-in-Publication Data:

+ TCP/IP and Linux protocol implementation: systems code for the Linux Internet/John Crowcroft, Iain Phillips [editors].
p. cm. -(Wiley Networking Council series)
Includes bibliographic references and index.
ISBN 0-741-40882-4 (cloth: soft paper).
1. TCP/IP (Computer network protocol) 2. Linux. 3. Internet. I. Crowcroft, Jon. J.
Phillips, Iain, 1967-III. Series.

TK5105.585-T34 2001
004.6--dc21

| Acc. No: | 059079 | 200104543 |

Printed in the United States of America. Class: 004.62
10 9 8 7 6 5 4 3 2 1
Price: $48.50 usd

# Wiley Networking Council Series

# NETWORKING council

Series Editors:

Scott Bradner
Senior Technical Consultant, Harvard University

Vinton Cerf
Senior Vice President, MCI WorldCom

Lyman Chapin
Chief Scientist, BBN/GTE

# Books in series:

- High Speed Networking: A Systematic Approach to High-Bandwidth Low-Latency Communication
James P. G. Sternbenz, Joseph D. Touch ISBN: 0-471-33036-1

- Planning for PKI: Best Practices Guide for Deploying Public Key Infrastructure
Russ Hough, Tim Polk ISBN: 0-471-39702-4

- Understanding Policy-Based Networking
Dave Kositur ISBN: 0-471-38804-1

- Delivering Internet Connections over Cable: Breaking the Access Barrier
Mark E. Laauch, David J. Farber, Stephen D. Dukes ISBN: 0-471-38950-1

- The NAT Handbook: Implementing and Managing Network Address Translation
Bill Dutcher ISBN: 0-471-39089-5

- WAN Survival Guide: Strategies for VPNs and Multiservices Networks
Howard C. Berkowitz ISBN: 0-471-38428-3

- ISP Survival Guide: Strategies for Running a Competitive ISP
Geoff Houston ISBN: 0-471-31499-4

- Implementing IPsec: Making Security for VPNs, Intranets, and Extranets
Elizabeth Kaufman, Andrew Newman ISBN: 0-471-34467-2

- Internet Performance Guide: QoS Strategies for Multiservices Networks
Geoff Houston ISBN: 0-471-37808-9

- ISP Liability Survival Guide: Strategies for Managing Copyright, Spam, Cache, and Privacy Regulations
Tim Casey ISBN: 0-471-37748-1

- VPN Applications Guide: Real Solutions for Enterprise Networks
Dave McDys ISBN: 0-471-31775-0

- Converged Networks and Services: Internetworking IP and the PSTN
Igor Faynberg, Hui-Lan Lu, and Lawrence Gabuzda ISBN: 0-471-35644-1

For more information, please visit the Networking Council Web site at: www.wiley.com/networkingcouncil

# Contents

List of Figures: xiii
List of Tables: xvi
Preface: x

1 Overview of the Internet: 1
1.1 Roadmap: 1
1.2 Introduction: 1
1.3 Protocols: 5
1.3 Note on Programming: 5
1.4 Stacks: 9
1.4.1 Basics: 9
1.4.2 IP: 10
1.4.3 Routes: 11
1.4.4 TCP: 12
1.4.5 Patterns: 14
1.5 Security: 16
1.6 Performance: 17
1.6 Note: 17
1.6.1 Differentiated Services: 18
1.6.2 Services: 18
1.7 Summary: 20

2 The Linux Operating System: 21
2.1 Roadmap: 21
2.2 What is an Operating System?: 22
2.2.1 User: 24
2.2.2 Multitasking: 24
2.2.3 Device: 27
2.2.4 Interprocess Communication: 29
2.2.5 Independence: 30
2.2.6 Concurrency: 35
2.7 Memory: 38
2.3 What Could You Ask?: 40
2.3.1 Reliability: 40
2.4 Source Code: 41
2.5 A Day in the Life of a Process: 43
2.6 A Day in the Life of a File: 52
2.7 Start: 53
2.7.1 Kernel: 53
2.7.2 End: 56
2.8 A Day in the Life of a Device: 56
2.9 Module: 63
2.10 SMP: 64
2.10.1 Support: 66
2.11 State: 66
2.12 Summary: 69

3 Three Views of the Path: 71
3.1 Roadmap: 71
3.1 Application, Viewpoints: 72
3.1.2 Source, Memory, Viewpoints: 76
3.2 Example: 76
3.2.1 Socket: 77
3.2.2 TCP Output: 77
3.2.3 IP Output: 78
3.2.4 Link-Level Output: 79
3.2.5 Link-Level Input: 82
3.2.6 IP Input: 82
3.2.7 TCP Input: 82
3.2.8 Socket Input: 82
3.3 DNS/UDP Example: 83
3.3.1 UDP Output: 83
3.3.2 UDP Input: 85
3.4 RTP/UDP (Multicast) Example: 87
3.4.1 On the Wire: 87
3.4.2 But with a Router in the Path...: 88
3.5 Tr of the Path: 88

4 Interprocess Communication: 91
4.1 Roadmap: 91
4.2 Socket API: 93
4.3 Actual Socket API: 93
4.4 Using the Socket API: 98
4.4.1 Polling a Socket: 101
4.4.2 Nonblocking I/O: 102
4.4.3 Asynchronous I/O: 103
4.4.4 System Include: 105
4.5 Summary: 106

5 Protocol Implementation Framework: 107
5.1 Roadmap: 107
5.2 A Day in the Life of a Software Interrupt: 108
5.2.1 Concurrency in the Linux Stack: 108
5.2.2 Producer/Consumer Chain: 108
5.2.3 What About Real Multiprocessor Systems?: 110
5.3 Bottom Up: Interrupts, DMA, and So: 112
5.4 Device Level, Bottom Up, One Level Up: 121
5.4.1 Network Device Driver API: 123
5.4.2 Network Reception: 127
5.4.3 A Specific Device Driver—3c501: 128
5.4.4 Link Driver-Level Configuration: 141
5.5 Top Down: Socket Glue Level: 143
5.5.1 Virtual File System Stack Functions: 149
5.6 Sideways: A Day in the Life of a Socket Buffer: 184
5.6.1 Allocating a Socket Buffer: 187
5.6.2 Allocating and Freeing a Socket Buffer from the: 189
5.6.2 Global Pool: 192
5.6.3 Manipulating Socket Buffers: 196
5.7 A Day in the Life of a Protocol Control Block: 199
5.7.1 Socket and Route-Related Transport State: 205
5.7.2 Future of the Socket Structure: 206
5.7.3 Reference Counting: 208
5.7.4 Sockets and Routes: 212
5.7.5 Socket Credentials Manager Interface: 213
5.7.6 A Brief Comparison with BSD Style Stack Infrastructure: 214
5.8 Summary
