
# Linux Administration: A Beginner's Guide

The advancement and maturity of the Linux operating system and the growth of the open source community have enabled even more applications to be hosted on Linux servers. Voice over Internet Protocol, often referred to as Voice IP or simply VoIP, has matured from being a technology implemented on specialized, high-cost hardware to be an application that can be hosted as a service on a Linux machine built from off-the-shelf components.

VoIP, like Linux, has evolved rapidly since its introduction in 1995 and continues to revolutionize communication, replacing traditional telephone networks all around the world. Every day, international and continental distance calls, local calls, and even calls via smartphone apps (applications on smartphones) utilize VoIP networks in ways most people never think about.

In the following sections, we will review the fundamentals of VoIP technology and Internet telephony, describe the basic elements of VoIP, and show an implementation of VoIP using the open source framework created by the popular Asterisk project (www.asterisk.org). By the end of the chapter, you will have a fully functional VoIP system with which you can make and receive phone calls.

# VoIP Overview

In its simplest form, VoIP is the transmission of digitized speech in “data packets” from one IP address to another one or more IP networks such as the Internet or a LAN. A VoIP system converts un speech as an input, converts it into compressed digital form, packetizes it, puts it on the wire, and sends it to the next station, where the process is reversed, as shown in Figure 21-1. The accuracy and clarity of the reconstructed signal is dependent on various technical factors, such as the compression algorithms

![](img/9f6657924397c33f088db5321b751a83_552_0.png)

Figure 21-1 Basic principles of VoIP

used, the encoding and decoding algorithms used, the sample rate, and so on. This is an obviously seemingly simplified version of how VoIP works, and so we recommend that you consult any of the many other available resources (books and online articles) for the nitty-gritty details.

As with most complex systems, the VoIP system can be broken down into several components. A subset of the components that we will be exploring in the following sections include the following: VoIP servers, analog telephone adapters, IP phones, and VoIP protocols.

# VoIP Server

The VoIP server plays the role of the communications switch. It is central to all VoIP communications for directing, mitigating, controlling the VoIP communications among the various components. The VoIP server provides ways for end users to make and receive VoIP calls and to interact with VoIP systems and other VoIP components.

Besides the seemingly all-important role of the VoIP server, it isn't terribly useful by itself. Its needs and relies on the other components to realize its full potential.

# Analog Telephone Adapter (ATA)

An ATA is a simple device that connects any (analog) telephone to your network so it can use VoIP communication through your Internet connection. The ATA converts the analog signal from your telephone into digital data that can be transmitted over the Internet. VoIP providers, as Vonage, Lingo, and magicjack, typically bundle an ATA with their VoIP telephony service to make it easier for new customers to use their existing analog phones with the VoIP service.

# IP Phones

Depending on the environment, users can interact with VoIP systems/networks using various methods. They can use hardphones or softphones, or simply stick to using analog phones that require ATA devices.

For home use, most people are familiar with going the ATA device route for converting their analog phones into quasi IP phones.

At work, you most likely have an IP phone on your desktop. This device, often termed a "hardphone," simply consolidates the functions of the ATA and the analog phone into one box. The last option, which you are probably more familiar with than you know, is the so-called "softphone." This is a software application that utilizes the hardware of your smartphone, tablet, or PC to do some of the heavy lifting on the VoIP endpoint.

The diagram in Figure 21-2 shows a simplified network layout of a VoIP setup using an ATA and IP phones.

The configuration examples in this chapter are based on softphones. However, you after reading this chapter you will be able to configure any of them as endpoints.

![](img/9f6657924397c33f088db5321b751a83_554_0.png)

**Figure 21-2** VoIP network layout using an ATA and IP phones

# VoIP Protocols

A typical VoIP connection generally involves a series of handshakes, also known as *signaling*, between the VoIP endpoints (and components in between) to exchange information that culminates in two persistent media streams (one for each direction) that carry the actual conversation. There are several protocols created to handle this exchange. In this section, we will discuss some of those that are important to VoIP in general and to Asterisk specifically.

For clarity, we categorize the VoIP protocols into three groups:

- Signaling protocols
- Media protocols
- Codecs

# Signaling Protocols

Generally, VoIP signaling controls the setting up, modifying, and tearing down of a conversation. The signaling protocols are not concerned with the nitty-gritty details of the data streams carrying the actual media content, but instead focus on verifying the identities of the calling and called parties (authentication, authorization), ensuring that the network is not misused, and communicating the capabilities, such as call features and security, supported by the endpoints.

In rough chronological order of introduction, the most widely used signaling protocols for VoIP systems are detailed in Table 21-1.

# CHAPTER 21 Voice over Internet Protocol (VoIP)

| Signaling Protocol | Specification | Description |
| :--- | :--- | :--- |
| H.323 | ITU-Recommendation H.323 (09) | An ITU-T standard that provides multimedia conferencing, voice, and data capability for use over packetsitched networks. It is the most widely deployed in enterprise and carrier markets. |
| Media Gateway Control Protocol (MGCP) | ITU/IETF RFC 3435 | An alternative to H.323 for controlling media gateway Call Agents. |
| Session Initiation Protocol (SIP) | ITU/IETF RFC 3261 | A plaintext signaling protocol that uses HTTP-like messages to initiate, modify, and terminate VoIP connections. SIP provides the necessary protocol mechanisms for caller and called number authentication. |
| Skinny Client Protocol (SCCP), aka Skinny | Cisco proprietary protocol | Defines a simple messaging set that allows skinny clients to communicate with the Cisco Unified Communications Manager (formerly CallManager). |
| Extensible Messaging and Presence Protocol (XMPP) | ITU/IETF RFC 6120 | Based on Extensible Markup Language (XML), XMP is for exchanging near-real-time communications, such as instant messages, presence status, and session control (signaling). |

Table 21-1 Signaling Protocols

| Media Protocol | Specification | Description |
| :--- | :--- | :--- |
| Real-time Transport Protocol (RTP) | ITU/IETF RFC 3550 | Defines how multimedia information is sent and received between VoIP devices. RTP does not guarantee resource reservation and not guarantee Quality of Service (QoS) for audio or video services. |
| Real-time Control Protocol (RTCP) | ITU/IETF RFC 3550 | RTP carries statistical and control data for RTP sessions such as delay, jitter, and packet loss. It augments RTP by monitoring streaming media data across VoIP endpoints to determine whether RTP is providing the necessary QoS for reasonable communication. |

Table 21-2 Media Protocols

**Media Protocols**

Media Protocols are responsible for transporting multimedia data (such as audio and video) over IP networks. RTP and RTCP (RFC 3550) are closely linked media protocols that are often used for this purpose. Both are described in Table 21-2. RTP and RTCP data streams are carried in connectionless UDP packets and are designed to be independent of the underlying Transport and Network layers.

**Codecs**

A codec (coder-decoder) is a set of instructions to convert analog signals to digital form, and back again. The codec used is often referred as the encoding method or the payload type for the RTP packet. Codecs, decribed in Table 21-3, differ in a number of ways, including sound quality, bandwidth, and computational requirements.

| Codec | Bandwidth (kbps) | Comments |
| :--- | :--- | :--- |
| G.711 | 64 | No compression; Delivers precise speech transmission; Very low processor requirements; Needs at least 128 kbps for two-way communication |

Table 21-3 Common Codecs
