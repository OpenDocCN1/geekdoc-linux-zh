+   □ MS-KB-Q180094 How to Write an LMHOSTS File for Domain Validation and Other Name Resolution Issues

+   □ MS-KB-Q262655 Primary Domain Controller (PDC) Names Entered in LMHOSTS File Are Case-Sensitive

+   □ MS-KB-Q266729 Netlogon Behavior in Windows NT 4.0

# Discovery and secure channels

You can control which DC a machine establishes its secure channel with by setting your node type to M-node, or using settings in the Lmhosts file, or using the setprfdc, nltest, or netdom tools:

+   □ MS-KB-Q181171 Secure Channel Manipulation with TCP/IP

+   □ MS-KB-Q158148 Domain Secure Channel Utility – Nltest.exe

+   □ MS-KB-Q183859 Integrity Checking on Secure Channels with Domain Controllers

How to solve the "missing computer account" problem:

+   □ MS-KB-Q175024 Resetting Domain Member Secure Channel

# The logon authentication itself

Logon uses RPCs (remote procedure calls) – one machine specifies a subroutine or system call that's to be executed on a remote machine. If the traffic weren't encrypted you'd be able to see RPC calls for NetrServerReqChallenge, NetrServerAuthenticate2, NetrSamLogon, and NetrSamLogoff functions in your Netmon traces, and old documentation – before logon traffic encryption was introduced – still shows some of these.

# Different types of logon

For an explanation of the different types, how they work, and some examples:

+   □ Resource Kit, pages 90–93

+   □ MS-KB-Q122422 Example of Remote Logon with Windows NT Server

# LM, NTLM, and NTLMv2 authentication methods

+   □ MS-KB-Q147706 How to Disable LM Authentication on Windows NT

# Replication between PDC and BDC

+   □ MS-KB-Q173882 Netlogon Synchronization Errors

+   □ MS-KB-Q149664 Verifying Domain Netlogon Synchronization

In spite of the following article's title, it discusses the whole process of promoting and demoting a BDC when your PDC fails:

+   □ MS-KB-Q167248 How to Demote to BDC When Two PDCs are Present