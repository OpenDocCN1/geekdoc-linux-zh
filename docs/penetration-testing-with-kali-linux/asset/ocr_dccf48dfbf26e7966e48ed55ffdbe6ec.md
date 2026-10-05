# OffSec

Penetration Testing with Kali Linux

+   * Browser Plugin
* Machine Learning Engine

Each of the above engines work simultaneously with the signature database to rank specific events as either benign, malicious, or unknown. When the engine performs a scheduled scan, it simply parses the entire file system and sends each file's metadata or data to the engine. On the contrary, real-time scans involve detecting and possibly reacting to any new action, such as downloading malware from a website. In order to detect such operations, the real-time scanners might identify events at the kernel level via a specially crafted mini-filter driver.⁵⁵⁰ This is the reason why a modern AV needs to operate in both kernel and user land, in order to validate the entire operating system scope.

The memory engine inspects each process's memory space at runtime for well-known signatures or suspicious API calls that might result in memory injection attacks, as we'll find shortly.

As the name suggests, the network engine inspects the incoming and outgoing network traffic on the local network. Once a signature is marked, a network engine might attempt to block the malware from communicating with its Command and Control (C2)⁵¹ server.

To hinder detection, malware often employs encryption and decryption through custom routines to conceal its true nature. AV counteract this by disassembling the packers or ciphers and loading the malware into a sandbox, or emulator.

The disassembler engine is responsible for translating machine code into assembly language, reconstructing the original code section, and identifying any encoding/decoding routine. A sandbox is special isolated environment in the AV software where malware can be safely loaded and executed without causing potential hazard to the system. Once the malware is unpacked/decoded or decoded in the emulator, it can be thoroughly analyzed by against any known signature.

As browsers are protected by the sandbox, modern AVs often employ browser plugins to get better visibility and detect malicious content that might be executed inside the browser.

Additionally, the machine learning component is a vital part of current AVs as it enables detection of unknown threats by relying on cloud-enhanced computing resources and algorithms.

# 12.1.3 Detection Methods

As mentioned earlier, antivirus signature and scope may differ based on the engine they have been built for, but they will serve the same purpose of uniquely identifying a specific threat or malware.

In this section, we are going to explore the following AV detection methodologies and explain how they work together.

+   * Signature-based Detection

> ⁵⁵⁰ (Microsoft, 2022), https://docs.microsoft.com/en-us/windows-hardware/drivers/ifs/filter-manager-concepts
⁵¹¹ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Botnet#Command_and_control

PWK - Copyright ©2023 OffSec Services Limited. All rights reserved.

352