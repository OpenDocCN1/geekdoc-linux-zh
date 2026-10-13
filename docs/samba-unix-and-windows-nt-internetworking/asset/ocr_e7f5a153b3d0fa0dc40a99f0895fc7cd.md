Chapter 15 culminates the text with on overview of troubleshooting procedures for diagnosing and correcting problems. A synopsis of the tools available in Samba, UNIX, and Windows is provided along with descriptions of how they can be used together to sleuth Samba problems. A listing of additional Samba documents and on-line discussion groups is provided for those "when all else fails—cry for help" situations.

The appendices provide example configurations and additional reference information.

That being said, it's time to Samba!

# Part I: Introduction and Planning

# Part Overview

+   - Chapter 1: Internetworking UNIX and Windows
+   - Chapter 2: UNIX Overview
+   - Chapter 3: Windows Overview
+   - Chapter 4: Samba Overview

# Chapter 1: Internetworking UNIX and Windows

# Overview

When network engineers talk about internetworking, the flow of conversation usually eddies around the various lower-level protocols and circuits involved in the connectivity between some set of networked devices, be it computers, routers, switches, or just about any pair of semi-intelligent appliances. They don't normally use the term when discussing connectivity between services residing higher up in the protocol stack (Table 1.1).

Table 1.1 OSI Protocol Stack

| Layer | Description |
|---|---|
| 7 Application | User interface and services |
| 6 Presentation | Application data transformations |
| 5 Session | Connection authentication |
| 4 Transport | End-to-end data ordering |
| 3 Network | Routing and reporting mechanisms |