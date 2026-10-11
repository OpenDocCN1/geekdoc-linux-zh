
- Windows Server 2022 Eval Download - [https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022)
- Bad Blood Documentation - [https://secframe.com/docs/badblood/whatisbadblood](https://secframe.com/docs/badblood/whatisbadblood)

You can use a lab setup using whatever virtual environment that you wish. Though be sure to properly secure it as you will be using vulnerable virtual machines. If you are totally unfamiliar with setting up a testing lab, check out the Bonus Chapter at the end of this book!

## ETHICAL HACKING ISSUES

In Ethical Hacking & Pentesting, a security tester basically acts like a hacker. They use tools and techniques that a hacker would most likely use to test a target network's security. The difference being they are hired by the company to test security and when done reveal to the leadership team how they got in and what they can do to plug the holes. The biggest issue I see in using these techniques is ethics and law. Some security testing techniques covered in this book are actually illegal to do in some areas. So, it is important that users check their Local, State and Federal laws before using the information in this book.

Also, you may have some users that try to use Kali Linux or other Ethical Hacking tools on a network that they do not have permission to do so. Or they will try to use a technique they learned, but may have not mastered on a production network. All of these are potential legal and ethical issues. Never run security tools against systems that you do not have express written permission to do so. In addition, it is always best to run tests that could modify data or possibly cause system instability on an offline, non-production replica of the network, and analyzing the results, before ever attempting to use them on live systems.

## DISCLAIMER

Never try to gain access to a computer you do not own, or security test a network or computer when you do not have written permission to do so. Doing so could leave you facing legal prosecution and you could end up in jail.

> *The information in this book is for educational purposes only!*

There are many issues and technologies that you would run into in a live environment that are not covered in this material. This book only demonstrates some of the most basic usage of the tools covered and should not be considered as an all-inclusive manual to Ethical hacking or Pentesting.

I did not create any of the tools or software programs covered in this book, nor am I a representative of Kali Linux, Offensive Security or Microsoft. Any errors, mistakes, or tutorial goofs in this book are solely mine and should not reflect on the tool creators. Every exercise in this book worked at the time of this writing. Tool usage, capabilities and links change over time, if the information presented here no longer works, please check the tool creator's website for the latest information. Thank you to the developers of Kali Linux for creating a spectacular product and thanks to the individual tool creators, you are all doing an amazing job and are helping secure systems worldwide!

## WHAT WE WILL COVER IN OUR JOURNEY

![](img/4a03f08556c51a14a3b88fe549a54ca8_15_0.png)

In the first chapter, we will cover a basic introduction to the Windows foundational security authentication protocols Kerberos and NTLM. Both of these protocols create encrypted passkeys - tickets for Kerberos, and hashes for NTLM. For simplicity's sake, I will call both of these "password hashes" throughout the book. We will then cover some of the popular tools and techniques used to obtain these hashes.

We then take an extensive look at wordlists. Wordlists are the foundation to password cracking. Using a good wordlist will greatly increase your chances and speed of password cracking. We will cover how to find, create or generate effectual wordlists for password cracking. This includes using tools to create custom wordlists. Then we will dive into the actual cracking tools. How Wordlists are used by cracking programs to unlock access. In the chapters ahead we will briefly cover John the Ripper and then take a deep dive, multiple chapters look at the pre-eminent password cracking tool, Hashcat.

First up, how do we obtain hashes for cracking? We will take a look at how the Kerberos and NTLM Authentication protocols work in Windows and then how to pull hashes from them. Strap in, buckle up, this is going to be a wild ride!

## CHAPTER 2
### Obtaining Password Hashes for Cracking

Windows Server active Directory has several ways in which it can authenticate users. These authentication protocols include NTLM and Kerberos. Let's begin by talking about both briefly.

![](img/4a03f08556c51a14a3b88fe549a54ca8_17_0.png)

NTLM (NT LAN Manager) protocol plays a pivotal role in authentication processes within Windows environments, acting as a key mechanism to verify the identity of users and systems. As a legacy protocol, NTLM has been a stalwart component since the early versions of Windows, although its prominence has diminished with the advent of more advanced authentication protocols, like Kerberos.

Unlike Kerberos, NTLM primarily functions through a challenge-response mechanism. When a user attempts to access a resource, the server generates a random challenge that is sent to the client. The client then encrypts this challenge using the user's credentials and sends the encrypted response back to the server. If the server can successfully decrypt the response using the stored credentials, access is granted. This process provides a level of security by ensuring that both the client and the server possess the necessary credentials for authentication.

However, despite its historical significance, NTLM is not without its vulnerabilities. Over time, security experts have identified weaknesses in the protocol, leading to its gradual replacement by more robust and secure authentication methods like Kerberos. NTLM is susceptible to certain types of attacks, such as pass-the-hash attacks, where an attacker captures the hashed credentials and attempts to use them for unauthorized access. Though there are many ways of dumping NTLM password Hashes, one of the most popular tools is Mimikatz.

Kerberos is the most secure protocol of the two. But many companies still use the older NTLM authentication protocol, so it is still included by default. With the creation and implementation of more secure authentication protocols, like Kerberos, restricting NTLM usage or removing it completely is a very good idea. That being said, Kerberos and NTLM are both frequently targeted by attackers. Though the authentication protocols are different, the attack process, in a way, is similar – hackers use tools or procedure to obtain the encrypted password information from either, and then try to crack it.

We will start with an in-depth look at one way to attack Kerberos Security – "Kerberoasting". We will then look at a quick way of dumping NTLM credentials with Mimikatz. There are many tools and processes you can use to dump credentials from memory. We will only quickly cover a few. I cover additional password recovery topics in my Basic and Advanced Kali books.

This next section will be more theory, it's good to understand the technology behind the process. But if the theory is too complicated and you feel a little lost, don't worry! It really does seem like confusing techno-babble, lol! For now, just understand that Windows can create several types of encrypted passwords including Kerberos and NTLM. And the process of pulling them from a system and cracking them is slightly different.

## KERBEROASTING

“Kerberoasting” is a security attack that targets the Kerberos authentication protocol used in Active Directory environments. In simple terms, in an Active Directory environment, Kerberos is one of several protocols that helps users and systems authenticate themselves securely. Kerberos is a Ticket Based system. Basically, Kerberoasting is a method where an attacker captures encrypted service tickets, targeting service accounts in an Active Directory environment, and then attempts to crack the encrypted information offline to reveal the service account's password.
