
# Linux Socket Programming

- Master the concepts
    - Network/distributed programming
    - Networking clients, servers, and peers
    - I/O control and multitasking
    - Unicast, broadcast, and multicast messages
    - Security and Secure Sockets Layer (SSL)
- Build the applications
    - Clients and servers (simple, multitasked, and multithreaded)
    - OpenSSL programs that connect to commercial products
    - Tools that use Remote Procedure Calls (RPCs)
    - Multicast and broadcast messengers

![](img/03334662da8fdfb8d95a02f270c522f6_0_0.png)

Release: TeamOR 2001

![](img/03334662da8fdfb8d95a02f270c522f6_0_1.png)

# Table of Contents

- Acknowledgments 2
- Tell Us What You Think! 3
    - Expanding the Programming Challenge 3
    - Book Organization 3
    - Professional Reader's Styles 4
    - Audience and Expected Interaction 5
    - Disclaimers and Limits 5
    - Conventions Used in This Book 5

- Chapter 1. Introducing the Cookbook Network Client .. 6
    - Connecting the World with Sockets 9
    - Talking the Talk: TCP/IP Addressing Overview 9
    - Hearing the Server: The Client's Basic Algorithm 11
    - Summary: What's Going On Behind the Scenes? 20

- Chapter 2. TCP/IP Network Language Fluency 21
    - An IP Numbering Overview 22
    - IP Host Port Numbers 27
    - Network Byte Ordering 29
    - Different Kinds of 35
        - UNIX Named Pipes 35
    - Summary: Applying IP Numbering and Tools 36

- Chapter 3. Different Types of Internet Packets 36
    - The Fundamental Network Packet 37
    - Dissecting the Various Packets 41
    - How the IP Protocols Fit Together 51
    - Sniping the Network with Tcpdump 52
    - Writing a Custom Network Sniffer 53
    - Summary: Choosing the Best Packets for Sending Messages 54

- Chapter 4. Sending Messages Between Peers 54
    - What Are Connection-Based Sockets? 55
    - Example: Connecting to the HTTP Daemon 58
    - What Are Connectionless Sockets? 60
    - Sending a Direct Message 64
    - Ensuring UDP Message Arrival 68
    - Juggling Tasks: A Multitasking Introduction 71
    - Summary: Connected Versus Connectionless Models 72

- Chapter 5. Understanding the Network Layering 72
    - Model
    - Solving the Network Challenge 73
    - Open Systems Interconnection (OSI) Network Model .... 77
    - Internet Protocol Suite 81
    - Fundamental Differences Between OSI and IP 84
    - What Services What? 85
    - Summary: From Theory to Application 85

- Part II: The Server Perspective and Load Control 86
- Chapter 6. A Server Primer 86
    - Mapping the Socket: The Server's General Program 86
    - Flow 86
    - A Simple Echo Server 88
    - General Rules About Defining Protocols 94
    - An Extended Example: An HTTP Directory Server 96
    - Summary: The Server's Basic Elements 98

- Chapter 7. Dividing the Load: Multitasking 99
    - Defining Multitasking: Processes Versus Threads 100
    - Beating the Clock: Race Conditions and Mutexes 121
    - Controlling Children and Killing Zombies 124
    - Extending Current Clients and Servers 127
    - Calling External Programs with the 127
    - Server 127
    - Summary: Distributing the Process Load 130

- Chapter 8. Choosing when to Wait for I/O 130
    - I/O Blocking: Why? 131
    - When Do I Block? 132
    - Alternatives to I/O Blocking 132
    - Comparing the Different I/O Programming 133
    - Interactions 133
    - Polling I/O 134
    - Asynchronous I/O 138
    - Solving Unwanted I/O Blocking with 143
    - and 143
    - Implementing Timeouts 145
    - Summary: Choosing the I/O Techniques 146

- Chapter 9. Breaking Performance Barriers 147
    - Creating the Servlets Before the Client Arrives 147
    - Extending Control with a Smart Select 153

- Chapter 10. Designing Robust Linux Sockets
    - Delving Deeper into Socket Control
    - Recovering the Socket Descriptor
    - Sending Before Received: Message Interleave
    - Noting File I/O Problems
    - Using Demand-Based I/O to Recover CPU Time
    - Sending High-Priority Messages
    - Summary: Pulling Together Performance Features

- **Chapter 10. Designing Robust Linux Sockets**
    - Using Conversion Tools
    - Eying Return Values
    - Capturing Signals
    - Resource Management
    - Critical Servers
    - Client/Server Concurrency Issues
    - Denial of Service Attacks
    - Summary: Solid-as-a-Rock Servers

- **Part III: Looking at Sockets Objectively**

- **Chapter 11. Saving Time with Objects**
    - The Software Engineering Evolution
    - Reaching Programming Nirvana
    - Object Features
    - Special Forms
    - Language Support
    - Summary: Object-Oriented Thinking

- **Chapter 12. Using Java's Networking API**
    - Exploring Different Java Sockets
    - Connecting Through I/O
    - Configuring the Java Socket
    - Multitasking the Programs
    - Implementation Limitations
    - Summary: Java-Style Network Programming

- **Chapter 13. Designing and Using a C++ Socket Framework**
    - Why Use C++ for Sockets Programming?
    - Laying Out the Framework
    - Testing the Socket Framework
    - Implementation Limitations
    - Summary: A C++ Socket Framework Simplifies Programming

- Chapter 14. Limits to Objects 222
    - Mind Over Objects 223
    - Objects Don't Solve Everything 227
    - Complexity Give and Take 229
    - Project Management Dilemma 231
    - Summary: Walk Carefully on Shale 234

- Part IV: Advanced Sockets Adding Value 234
- Chapter 15. Network Encapsulation with Remote Procedure Calls (RPCs) 234
    - Revisiting the OSI Model 235
    - Comparing Network and Procedural Programming 235
    - Supplying Middleware Methods 239
    - Creating RPCs with 241
    - Creating Non-Stateless Calls with Open Connections 246
    - Summary: Creating an RPC Toolset 248

- Chapter 16. Adding Security to Network Programs and SSL 248
    - Giving Permission to Work 249
    - The Problem with the Internet 250
    - Securing a Network Node 252
    - Encrypting the Messages 257
    - Secure Sockets Layer (SSL) 258
    - Summary: The Secure Server 263

- Chapter 17. Sharing Messages with Multicast, Broadcast, and Mbone 263
    - Broadcasting Messages to a Domain 264
    - Multicasting Messages to a Group 266
    - Summary: Efficient Message Sharing 271

- Chapter 18. The Power of Raw Sockets 272
    - When Would You Use Raw Sockets? 272
    - What Are the Limitations? 273
    - Putting Raw Sockets to Work 274
    - How Does Ping Work? 276
    - How Does Traceroute Work? 278
    - Summary: Making the Raw Decisions 279

- Chapter 19. IPv6: The Next Generation to IP 279
    - Current Addressing Problems 279
    - Trying Out IPv6 281
    - Summary: Moving Your Code into the Future ........................ 286

# Part V: Appendixes 287

- Appendix A. Data Tables 287
    - Domains: First Parameter to ... 288
    - Types: Second Parameter to ... 291
    - Protocol Definitions ... 292
    - Standard Internet Port Assignments (First 100 Ports) ... 292
    - HTTP 1.1 Status Codes ... 293
    - Socket Options ( ... 294
    - Signal Definitions ... 296
    - ICMP Codes ... 297
    - IPv4 Multicast Allocation ... 298
    - Proposed IPv6 Address Allocation ... 298
    - ICMPv6 Codes ... 299
    - IPv6 Multicast Scope Field ... 300
    - IPv6 Multicast Flags Field ... 300

- Appendix B. Networking API 300
    - Connecting to the Network ... 301
    - Terminating Connections ... 314
    - Network Data Conversions ... 315
    - Network Addressing Tools ... 320
    - Socket Controls ... 324

- Appendix C. Kernel API Subset 325
    - Tasks ... 326
    - Threads ... 331
    - Locking ... 334
    - Signals ... 336
    - Files and So On ... 339

- Appendix D. Object Classes 348
    - C++ Exceptions ... 348
    - C++ Support Classes ... 349
    - C++ Messaging Classes ... 351
    - C++ Socket Classes ... 351
    - Java Exceptions ... 356
    - Java Support Classes ... 357
    - Java I/O Classes ... 358
    - Java Socket Classes ... 364

# Copyright Information

Copyright © 2001 by Sams Publishing

All rights reserved. No part of this book shall be reproduced, stored in a retrieval system, or transmitted by any means, electronic, mechanical, photocopying, recording, or otherwise, without written permission from the publisher. No patent liability is assumed with respect to the use of the information contained herein. Although every precaution has been taken in the preparation of this book, the publisher and author assume no responsibility for errors or omissions. Nor is any liability assumed for damages resulting from the use of the information contained herein.

Library of Congress Catalog Card Number: 99-068862

Printed in the United States of America

First Printing: January 2001

03 02 01 00 4 3 2 1

# Trademarks

All terms mentioned in this book that are known to be trademarks or service marks have been appropriately capitalized. Sams cannot attest to the accuracy of this information. Use of a term in this book should not be regarded as affecting the validity of any trademark or service mark.

# Warning and Disclaimer

Every effort has been made to make this book as complete and as accurate as possible, but no warranty or fitness is implied. The information provided is on an "as is" basis. The author and the publisher shall have neither liability nor responsibility to any person or entity with respect to any loss or damages arising from the information contained in this book or from the use of the CD or programs accompanying it.

# Dedication

> To the Giver of all Good and Prince of perfect Peace.

# Acknowledgments

I know that this book would not have been possible except for several people. First, my beloved wife, Susan, patiently encouraged me and gave me time and coaxing. Second, Wendel, my father, tried to teach me good organization and presentation. Third, the Linux movement selflessly provided me an effective, reliable operating system upon which I could do this work. Fourth, Beverly Scherf opened my eyes and showed me an effective way to communicate. Lastly, I did not realize how important this work was for me professionally until my friends Charles Knutson and Mike Holstein provided input and encouragement.
