# Chapter 15 Topics

This chapter covers the following topics and concepts:
* How to maintain a gold baseline
* How redundancy can help ensure availability
* Which varieties of open source corporate support are available
* Why you should check compliance with security policies
* How to keep Linux up to date
* How to keep distribution-related applications up to date
* How best to manage third-party applications
* Why you should share solutions with the community
* Why you should test new components before using them
* What some future trends in Linux are

# Chapter 15 Goals

When you complete this chapter, you will be able to:
* Understand best practices for keeping Linux software up to date
* Take advantage of corporate and community support
* Plan for changes in Linux security

# Maintain a Gold Baseline

A gold baseline is secure. It's kept secure because only copies of that baseline are used in production. But just like any other system, it has to be kept up to date. By its very nature, the software in a gold baseline is focused on the core commands and libraries associated with a distribution, along with the Linux kernel. It may include critical systems associated with all systems, such as the Secure Shell (SSH) and system log services. A black-hat hacker who breaks into any of these systems could easily gain access to all systems associated with every Linux distribution. While the diversity of available Linux distributions does help promote overall security, that diversity does not extend to the cores associated with the kernel or those basic commands and libraries used on every Linux system. To maintain that gold baseline, you need to monitor security news with selected distributions. When updates are made available, it is up to you to make sure those updates work on local systems, conform to any requirements associated with other software, and process that update on other systems. In addition, you'll need to make sure the database associated with intrusion detection tools such as the Advanced Intr Detection Environment (AIDE) and Tripwire is up to date.