# Attacking and Defending Windows XP Professional • Chapter 4

files. The earlier section of the chapter detailed configuration and implementation aspects of the initial setup of your Software Restriction Policy. After your policy has been configured, there are a couple maintenance initiatives that you should be aware of.

# Figure 4.21 Shaplik's HFNetchkkLT Interface

![](bbox=[0.14, 0.205, 0.857, 0.555])

First, you must learn to update your policies to include the latest threats and published vulnerabilities. For instance, if a new worm were to be exploiting users via a Trojan-introduced game, in most cases you wouldn't want this game to be executed within your network. One way to eliminate the risk would be to disallow it to propagate through the e-mail system by file mailboxes; however, that does not completely address the problem since it doesn't prevent users from downloading it via the network. You could create a hash-based rule that would disallow the computer from executing that particular file, similar to the method previously detailed in the "Software Restriction Policies" section.

The second reactive measure you must take is monitoring new programming languages and executables on the Internet. Common file extensions as .zip, .exe, .dll, and .doc are well known descriptors that quickly flag within the software policies. However, if a new programming language as Visual Z Sharp was released with an extension of .vsz,