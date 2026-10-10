
> "Impressively thorough, both in laying out the general issues, and particularly in explaining how these issues are addressed in HP-UX."
> —Ronald McCarty, Chair, Computer Science Program, Penn State University

## hp-ux
### 11i internals

chris cooper • chris moore

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_0_0.png)

Invaluable information for optimizing HP-UX performance, reliability, and efficiency

Find out how to approach system administration, tuning, and troubleshooting from a more informed perspective

For every HP-UX sysadmin, programmer, and performance specialist

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_0_1.png)

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_1_0.png)

Digitized by the Internet Archive
in 2023 with funding from
Kahle/Austin Foundation

https://archive.org/details/hpux11internals0000coop

# **HP-UX 11i Internals**

# Hewlett-Packard® Professional Books

# HP-UX

- Cooper/Moore
- Fernandez
- Madell
- Olker
- Poniatowski
- Rehman
- Sauers/Ruenmeller/Weigand
- Wegant
- Wong

- HP-UX 11i Internals
- Configuring CDE
- Disk and File Management Tasks on HP-UX
- Optimizing NFS Performance
- HP-UX 11i Virtual Partitions
- HP-UX 11i System Administration Handbook and Toolkit, Second Edition
- The HP-UX 11.x System Administration Handbook and Toolkit
- HP-UX 11.x System Administration "How To" Book
- HP-UX 10.x System Administration "How To" Book
- HP-UX System Administration Handbook and Toolkit
- Learning the HP-UX Operating System
- HP-UX CSA: Official Study Guide and Desk Reference
- HP-UX 11i Tuning and Performance
- Clusters for High Availability, Second Edition
- HP-UX 11i Security

# UNIX, LINUX, WINDOWS, AND MPE/IX

- Mosberger/Eranian
- Poniatowski
- Stone/Symons

- IA-64 Linux Kernel
- UNIX User's Handbook, Second Edition
- UNIX Fault Management

# COMPUTER ARCHITECTURE

- Evans/Trimper
- Kane
- Markstein

- Itanium Architecture for Programmers
- PA-RISC 2.0 Architecture
- IA-64 and Elementary Functions

# NETWORKING/COMMUNICATIONS

- Blommers
- Brans
- Cook
- Lucke
- Lund

- Architecting Enterprise Solutions with UNIX Networking
- OpenView Network Node Manager
- Practical Planning for Network Growth
- Mobilize Your Enterprise
- Building Enterprise Information Architecture
- Designing and Implementing Computer Workgroups
- Integrating UNIX and PC Network Operating Systems

# SECURITY

- Bruce
- Mao
- Pearson et al.
- Pipkin

- Security in Distributed Computing
- Modern Cryptography: Theory and Practice
- Trusted Computing Platforms
- Halting the Hacker, Second Edition
- Information Security

# WEB/INTERNET CONCEPTS AND PROGRAMMING

- Amor
- Apte/Mehta
- Chatterjee/Webber
- Kumar
- Mowrey/Werry
- Tapadia

- E-business (Re)volution, Second Edition
- UDDI
- Developing Enterprise Web Services: An Architect's Guide
- J2EE Security for Servlets, EJBs, and Web Services
- Online Communities
- .NET Programming

# OTHER PROGRAMMING

- Blinn    Portable Shell Programming
- Caruso    Power Programming in HP OpenView
- Chaudhri    Object Databases in Practice
- Chew    The Java/C++ Cross Reference Handbook
- Grady    Practical Software Metrics for Project Management and Process Improvement
- Grady    Software Metrics
- Grady    Successful Software Process Improvement
- Lewis    The Art and Science of Smalltalk
- Lichtenbelt    Introduction to Volume Rendering
- Mellquist    SNMP++
- Mikkelsen    Practical Software Configuration Management
- Norton    Thread Time
- Tapadiya    COM+ Programming
- Yuan    Windows 2000 GDI Programming

# STORAGE

- Thornburgh    Fibre Channel for Mass Storage
- Thornburgh/Schoenborn    Storage Area Networks
- Todman    Designing Data Warehouses

# IT/IS

- Missbach/Hoffman    SAP Hardware Solutions

# IMAGE PROCESSING

- Crane    A Simplified Approach to Image Processing
- Gann    Desktop Scanners

# HP-UX 11i Internals

Chris Cooper
Chris Moore

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_8_0.png)

# Library of Congress Cataloging-in-Publication Data

Cooper, Chris. 
HP-UX 11i internals/Chris Cooper, Chris Moore. 
p. cm. -- (Hewlett-Packard professional books) 
ISBN 0-13-032861-8 
I. Operating systems (Computers) 2. HP-UX. I. Moore, C.G. (Chris G.) II. Title. 
III. Series.

QA76.76.O63C6644 2004 
005.4'3--dc22

2003069034

Editorial/production supervision: *Nicholas Radhuber*
Cover design director: *Jerry Votta*
Cover design: *DesignSource*
Manufacturing manager: *Maura Zaldivar*
Acquisitions editor: *Jill Harry*
Editorial assistant: *Brenda Mulligan*
Marketing manager: *Dan DePusquale*

© 2004 Hewlett-Packard Corp.
Published by Prentice Hall PTR
Pearson Education, Inc.
Upper Saddle River, New Jersey 07458

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_9_0.png)

This material may be distributed only subject to the terms and conditions set forth in the Open Publication License, v1.0 or later (the latest version is presently available at <http://www.opencontent.org/openpub/>).

Prentice Hall offers excellent discounts on this book when ordered in quantity for bulk purchases or special sales. For more information, please contact:
U.S. Corporate and Government Sales
1-800-382-3419
corpsales@pearsonedtechgroup.com

For sales outside of the U.S., please contact:
International Sales
1-317-581-3793
international@pearsonedtechgroup.com

Other product or company names mentioned herein are the trademarks or registered trademarks of their respective owners.

Printed in the United States of America

1st Printing

ISBN 0-13-032861-8

Pearson Education LTD.
Pearson Education Australia PTY. Limited 
Pearson Education Singapore, Pte. Ltd.
Pearson Education North Asia Ltd.
Pearson Education Canada, Ltd.
Pearson Educación de México, S.A. de C.V.
Pearson Education — Japan
Pearson Education Malaysia, Pte. Ltd.

# **CONTENTS**

- **Preface** xvii
- **Acknowledgments** xxi
- **List of Figures** xxiii
- **List of Tables** xxix
- **List of Listings** xxxi
- **Chapter 1 PA-RISC 2.0 Architecture** 1

- RISC Architecture 2
- Hardware Modules 2
- Central Processing Unit 3
- Translation Lookaside Buffer 4
- Cache 4
- Assist Processors 5
- Registers 5
- General Registers 5
- Space Registers 6
- Control Registers 6
- Processor Status Word 7
- Virtual Memory Support 10
- Virtual Memory Layout, Narrow Mode 11
- Virtual Memory Layout, Wide Mode 11
- 32-Bit Address Space Layout 12
- 64-bit Address Space Layout 12
- Explicit and Implicit Pointers, Narrow and Wide Mode 13
- Address Swizzling 14
- Global Virtual Addresses 14
- Address Translation 15
- Address Translation Components 16
- Translation Lookaside Buffer 17
- Access Control 17
- TLB Miss Handlers 18
- Cache Organization 18
- Interruptions 19
- Interruption Vector Table 20
- Interruption Handling 21
- Interruption Save State 21
- Summary 22

## Chapter 2  Procedure Calling Conventions 23

- Register Usage 23
- PA-RISC Instructions 24
- Memory Reference Instructions 25
- Base Register Modification 26
- Branch Instructions 26
- Unconditional Branch 27
- Conditional Branch 27
- Delayed Branching 31
- Immediate Instructions 32
- Procedure Call Model 33
- Procedure Return Model 33
- Stack Usage 34
- Stack Usage in Narrow Mode 34
- Stack Usage in Wide Mode 37
- Summary 39

## Chapter 3  The Kernel: Basic Organization 41

- A Generic Overview 41
- All I/O Is File I/O 43
- Abstraction: A Fundamental of Kernel Design 44
- Is It Real or Is It Virtual? 44
- Abstraction Layers 45
- Some Generic Kernel Techniques 46
- Kernel Data Structures 46
- Static Lists (Static Tables) 47
- Dynamic Linked Lists (Dynamic Tables) 48
- Resource Allocation 50
- Bit Allocation Maps 50
- Resource Maps 51
- Searching Lists and Arrays 53
- Hashtables: An Alternative to Linear Searches 53
