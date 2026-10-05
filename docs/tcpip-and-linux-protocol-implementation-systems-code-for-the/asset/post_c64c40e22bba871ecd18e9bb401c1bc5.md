
# Infrastructure Protocols 215

## 6.1 Roadmap 215
## 6.2 IP 215
- 6.2.1 Internet Protocol Output 215
- 6.2.2 Fragmentation 224
- 6.2.3 Internet Protocol Input 235
- 6.2.4 Internet Protocol Forwarding 241
- 6.2.5 Internet Protocol Support Functions 244
- 6.2.6 Internet Protocol Options 256
- 6.2.7 Internet Protocol Socket 270
## 6.3 Addressing 286
## 6.4 Network-Level Debugging—ICMP 309
## 6.5 Group Management—IGMP 332
- 6.5.1 IGMP 332
- 6.5.2 Managing the Group/Interface State 338
- 6.5.3 Multicast Forwarding 347
- 6.5.4 Multicast Transmission 367
- 6.5.5 Multicast Specifics 374
- 6.5.6 Starting Multicast 381
## 6.6 NATs, Tunnels, and Other Hacks 381
## 6.7 Network Address Translation 382
## 6.8 Tunnels 384
- 6.8.1 IP in Tunnels 384
- 6.8.2 GRE Tunnels 402
## 6.9 IP version 6 428
- 6.9.1 IPv6 Header Definitions 428
- 6.9.2 IPv6 API 433
- 6.9.3 IPv6 Auto-Configuration 434
- 6.9.4 IPv6 Neighbor Discovery 444
- 6.9.5 IPv6 Input 450
- 6.9.6 IPv6 Output 451
- 6.9.7 IPv6 Function 459
- 6.9.8 IPv6 Socket 461
- 6.9.9 IPv6 Flow Label 467
- 6.9.10 Extension Headers 469
- 6.9.11 Simple Internet Transition 471
- 6.9.12 Effect on Transport of IPv6 472
## 6.10 Summary 472

## 7 Transport 473
## 7.1 Roadmap 473
## 7.2 Introduction 474
## 7.3 UDP—Datagram Protocol 474
- 7.3.1 Introduction 474
- 7.3.2 Multiplexing 474
- 7.3.3 UDP Packet Anatomy 475
- 7.3.4 Transport Layer Linkage 477
- 7.3.5 The sock Structure 480
- 7.3.6 DNS Lookup 481
## 7.4 TCP—Transmission Control Protocol 486
- 7.4.1 Transport Functionality 486
- 7.4.2 HTTP Request 490
- 7.4.3 TCP Header 493
- 7.4.4 TCP Implementation 493
- 7.4.5 TCP States 494
- 7.4.6 TCP Structures 495
- 7.4.7 TCP Code 501
- 7.4.8 TCP Behavior 538
## 7.5 Management 539
## 7.6 RTP—Real-Time Protocol 539
## 7.7 Writing a New Transport Layer 540
## 7.9 Summary 540

## 8 Routing 541
## 8.1 Roadmap 541
## 8.2 Introduction 542
## 8.3 Forwarding Table Computation 547
- 8.3.1 IP Addressing 547
- 8.3.2 FIB Purpose 551
- 8.3.3 FIB Implementation 552
- 8.3.4 FIB Interface 552
- 8.3.5 FIB Code 555
## 8.4 Multicast 616
- 8.4.1 Dense Mode, Data-Driven Multicast Routing 619
- 8.4.2 Sparse and Single-Source Multicast 620
## 8.5 QoS Routing 620
## 8.6 Routing Table Construction 621
- 8.6.1 GateD 621
- 8.6.2 Route Control and Traffic Control Maintenance 623
## 8.7 Host Routing 629
## 8.8 Managing IP-Level State Information—the IP Command 637
## 8.9 Summary 639

## 9 Forwarding 641
## 9.1 Roadmap 641
## 9.2 Introduction 643
- 9.2.1 Integrated Services 646
- 9.2.2 Admission Test for Integrated Services Guaranteed 647
- 9.2.3 Network Architecture 648
## 9.3 Mixing Traffic onto the Wire 649
- 9.3.1 Performance Parameters 651
- 9.3.2 Probing or Measurement-Based Admission Control? 653
## 9.4 Elastic and Inelastic Applications—Tolerance for Variation? 653
- 9.4.1 Network Source Behavior Characterization: Leaky and Token Buckets 655
## 9.5 Packet-Forward Scheduling and Queue Management 656
## 9.6 Queuing Disciplines 657
- 9.6.1 Common Disciplines 658
- 9.6.2 Class-Based Queuing 660
## 9.7 Queue Management 660
- 9.7.1 Random Early Detection 662
## 9.8 Linux Forwarding Treatment 662
- 9.8.1 Output Interface 662
- 9.8.2 Queue Discipline 663
- 9.8.3 Class/Type 664
- 9.8.4 Filter, or Classifier 665
## 9.9 The Classifier Code 666
- 9.9.1 Classifiers 666
## 9.10 Queuing Discipline 720
## 9.11 Scheduler Framework 721
- 9.11.1 Scheduling API 721
- 9.11.2 Scheduler Framework 744
## 9.12 Class-Based Queuing 758
## 9.13 Queue Management 792
- 9.13.1 Best-Effort (Also Known as FIFO) 792
- 9.13.2 Ingress Queuing 802
- 9.13.3 Differentiated Services 806
- 9.13.4 RED and Friends 815
- 9.13.5 Explicit Congestion Notification 818
- 9.13.6 RED 823
- 9.13.7 Token Bucket 823
- 9.13.8 Ingress Queuing 830
- 9.13.9 Priority Queuing 832
- 9.13.10 Stochastic Fairness Queuing 836
- 9.13.11 Priority Queuing 837
- 9.13.12 Stochastic Fairness Queuing 838
- 9.13.13 Link Equalization 846
- 9.13.14 Profiling 855
## 9.14 Managing Forwarding Treatment—the TC Command 870
- 9.14.1 Traffic Control—Using the Tool 870
- 9.14.2 Traffic Control—How the Tool Implemented 871
- 9.14.3 TC Command Usage 872
## 9.15 BSD 875
## 9.16 Summary 875

## 10 Security 877
## 10.1 Roadmap 877
## 10.2 Security Scenarios 877
- 10.2.1 Firewalls 877
- 10.2.2 NAT—Network Address Translation 878
## 10.3 Netfilter 882
- 10.3.1 Introduction 882
- 10.3.2 IP Tables 883
- 10.3.3 Summary 883
## 10.4 IPSec 883
## 10.5 SSL 883
## 10.6 Summary 884

Afterword 885
Glossary 887
Bibliography 903
Index 911

## List of Figures
- 1.1 Comments, what comments: linux/net/ip/waitheaders.c 1
- 1.2 LAN 5
- 1.3 Layers of abstraction 9
- 1.4 The RFC-style IP header definition 10
- 1.5 C-style IP header definition 10
- 1.6 The RFC-style IP header definition 12
- 1.7 The TCP header definition: linux/include/linux/tcp.h 12
- 1.8 Trends 17
- 1.9 Differentiated services metering and marking 19
- 2.1 POSIX C-type definitions: linux/include/linux/posix.types.h 31
- 2.2 i386 ASM header interface C-type definitions: linux/include/asm-i386/types.h 32
- 2.3 Kernel C-type definitions: linux/include/linux/types.h 33
- 2.4 Kernel C-type definitions: linux/include/linux/types.h 34
- 2.5 Kernel C-type definitions: linux/include/linux/types.h 34
- 2.6 System calls 45
- 2.7 The scheduler i: linux/kernel/sched.c 45
- 2.8 The scheduler ii: linux/kernel/sched.c 45
- 2.9 The scheduler iii: linux/kernel/sched.c 46
- 2.10 The scheduler iv: linux/kernel/sched.c 46
- 2.11 The scheduler iv: linux/kernel/sched.c 47
- 2.12 The scheduler v: linux/kernel/sched.c 48
- 2.13 The scheduler tail: linux/kernel/sched.c 49
- 2.14 The wake-up common code: linux/kernel/sched.c 50
- 2.15 The sleep code: linux/kernel/sched.c 50

## List of Features
- 2.16 The Linux kernel system call entry code—save and restore overhead: linux/arch/i386/kernel/entry.S 50
- 2.17 The Linux kernel system call entry code—example of entry: linux/arch/i386/kernel/entry.S 51
- 2.18 The Linux kernel startup code i: linux/init/main.c 54
- 2.19 The Linux kernel startup code ii: linux/init/main.c 54
