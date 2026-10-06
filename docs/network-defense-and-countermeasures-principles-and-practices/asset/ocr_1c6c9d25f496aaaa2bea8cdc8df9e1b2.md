# Chapter 5

# Intrusion-Detection Systems

# Chapter Objectives

After reading this chapter and completing the exercises, you will be able to do the following:

+   - Explain how intrusion-detection systems work.
* Implement strategies for preventing intrusion.
* Identify and describe several popular intrusion-detection systems.
* Define the term honeypot.
* Identify and describe at least one honeypot implementation.

# Introduction

Chapter 4, “Firewall Practical Applications,” discussed several firewall solutions that have built-in intrusion-detection systems (IDS). An IDS is designed to detect signs that someone is attempting to breach a system and to alert the system administrator that suspicious activity is taking place. This chapter analyzes how an IDS works and how to implement some specific IDS solutions.

IDSs have become much more widely used in the last few years. An IDS inspects all inbound and outbound port activity on a machine/firewall/system and looks for patterns that might indicate an attempted breach. For example, if the IDS finds that a series of packets were sent to each port in sequence from the same source IP address, this probably indicates that a system is being scanned by network-scanning software such as Cerberus (scanners are described at length in Chapter 12, “Assessing System Security”). Since this is often a prelude to an attempt to breach a system, it can be very important to know that someone is performing preparatory steps to infiltrate a system. The IDS may also detect an abnormally large flow of packets from the same IP address, all in a brief period of time. This may indicate a DoS attack. In either case, these are situations the network administrator should be aware of and should take steps to prevent.