
Patching Layer 8

Therefore, you should always push to avoid giving admin right to all users; however, if your company decides to grant admin rights to all employees, then you need to take the following countermeasures:

- 1. Define a clear policy about software installation.
- 2. Create a whitelist and blacklist of applications that can be installed.
- 3. If possible, create a repository to host the whitelisted software (this reduces the risk of a user installing hacked versions of the software).
- 4. Set alerts if a blacklisted software is installed on a corporate workstation.

## Implementing a strong BYOD policy

If you allow employees to use their personal devices for work, make sure that you have a strong BYOD policy in place.

## Performing random social engineering campaigns

The best way to evaluate the level of preparedness or exposure that users have against a social engineering attack is by testing them with real-life controlled attacks.

Here is how you can do:

- **Set up your environment:** Purchase a domain from where you will launch the attacks. Look for similar names as the ones that a real attacker will use, for example, `support-companyname.com`.
- **Test one attack per cycle:** First, need to define the cycles, as every 3 months, 6 months, or 1 year. For example, phishing in early 2020, baiting in late 2020, pro quo in early 2021, and extortion in late 2021.
- **Analyze the results:** The goal of this is not to chase your employees and put them on a “wall of shame”. Instead, this is gathering intelligence to determine areas of improvement for upcoming training and education.
- **Set up rewards:** You can set up a rewarding system for those employees that found the attack and used the proper channels to report it to the cybersecurity team.

> Rewards are not always about money
> You can also leverage free perks as digital badges, a wall of fame, a secure employee of the month (which you might want to use a catchier name as “Cybersecurity Rockstar”), a preferential parking spot for a month, or more.

- Announcements and communications: You might not want to spoil your assessments by communicating the start of it. However, it is a good idea to send a communication after the assessments are finished so that people are aware of these types of initiatives, but also to share relevant numbers with them (for instance, how many people fell victim to the attack, potential losses, and more).

To avoid disruption of services, we recommend that you roll out campaigns to a randomly selected group of individuals (depending on the size of the company, this could be between 10 to 60 percent of employees). Additionally, you need to ensure that this random selection includes participants from all the organizations across the company (for instance, HR, sales, and IT).

## Summary

In this chapter, you learned about all users, including how they can impact your defensive security strategy, their vulnerabilities, and the plurality of attacks aimed at them, but also the tactics that you can apply to mitigate those risks.

This chapter is extremely important because by securing this attack vector, you will exponentially reduce the scope of the attacks against your infrastructure, systems, and data.

Now, get ready for the next exciting chapter in which we will take a deep dive into more technical stuff. In the following chapter, you will learn about the best penetration testing tools, forensics, networking, and many other technologies that you need to master in order to create the best defensive security strategy.

## Further reading

Here is the complete report of *The Cost of Insider Threats*: 2020:

https://www.ibm.com/security/digital-assets/services/cost-of-insider-threats/#.

# 5
Cybersecurity Technologies and Tools

> "Digital transformation offers an enormous opportunity to reduce costs and increase productivity, but if done without stepping up on defensive security, it could end up being a disaster."

– Roberto Sasso – Founder and President, Club de Investigación Tecnológica

There are thousands of tools available for cybersecurity and it will take you hundreds of years just to understand the basics of each of them; to save your precious time, we will provide you with some insight into the best cybersecurity systems, methods, technologies, and tools for you to take advantage of.

Also, we are going to review a must-have hardware device that will help you bring your awareness campaigns to the next level.

Additionally, you will get a better understanding of what an Advanced Persistent Threat (APT) is and how to prevent them.

To get the most of this and understand the tools, in this chapter, we are going to cover the following topics:

- Networking tools and technologies
- Pentesting tools and methods
- Dealing with APT
- Leveraging security intelligence
- Technical requirements

To get the most of this and understand the tools, in this chapter, you may need to install Kali Linux. Another option is to use a virtual machine. All the images, including pre-built, can be found here: https://www.kali.org/downloads/

We will also be reviewing the outstanding WiFi Pineapple. For more information about this must-have pentesting tool, go to https://shop.hak5.org/products/wifi-pineapple.

# Advanced wireless tools for cybersecurity

As masters in defensive security, we need to know about and understand how the latest tools work. Let's start by taking a look at some of the latest and coolest wireless tools.

## Defending from wireless attacks

Wireless networks are far varied by connection types, making them a big target. Therefore, you need to be ahead of them and make sure that wireless security is a fundamental part of your strategy.

There is an entire section in Chapter 8, Enhancing Your Defensive Skills, dedicated to network tools. However, here, we will take a look at the most important tools that are used in wireless attacks so that you can be ahead of them and plan your defensive strategy accordingly.

## The almighty WiFi Pineapple

This is a must-have for auditing Wi-Fi networks. Created by Hak5 back in 2008, this is probably the most recognized pentesting tool in the world – maybe because of the power of this small box, its ease of use, and the huge variety of tools that it contains on a single device.

> Tip The geniuses at Hak5 put tremendous effort into keeping this tool up to date with the latest Wi-Fi auditing tools (for example, the MarkV received 22 firmware updates). However, there is a point where the hardware needs to be upgraded to include new tools (and improve the existing ones in terms of speed, range, and so on). Therefore, and considering the wide range of WiFi Pineapple versions, we decided to make this section as generic as possible to try to generally cover the tools available in most of the WiFi Pineapple versions.

Now, let's explore some of the features of this fantastic tool.

# Rogue access point

Have you ever noticed that your smartphone automatically connects to the wireless of your preferred café you connect to for the first time?

Well, that feature was created to improve the user experience, but it also represents a serious security vulnerability.

To exploit this vulnerability, the attacker needs to mimic one of those trusted Wi-Fi access points (AP) so that the victim device will automatically connect to it. But the question is, how does the attacker know the name of the trusted networks on the victim’s device? Well, here is where the clever attack starts.

First, let’s take a look at the theory and concepts behind this attack.
