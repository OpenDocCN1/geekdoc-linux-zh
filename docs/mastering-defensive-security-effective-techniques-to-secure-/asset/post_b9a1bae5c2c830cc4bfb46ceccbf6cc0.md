
# Summary

By now, you should have mastered all the aspects of securing your web applications. In this chapter, we have learned about active and passive data gathering of your web application and the best tools used to discover sensitive data about your web application on the internet. We also learned about the risk of not obfuscating public information about your web application.

We also learned how to install, configure, and use the best virtual environment to become familiar with the most common vulnerabilities on web applications (the DVWA platform). Additionally, we explored how to install, configure, and use the best tool to assess the security of a given web application in real time (Burp Suite).

And we also experienced a hands-on example to see how easily an attacker can take advantage of common vulnerabilities to exploit your web application.

But there are many other tools to find vulnerabilities in your web application and even the entire infrastructure, let's move to the next chapter, in which we will review the best tools used to perform vulnerability assessments like a pro!

# Further reading

- Additional information about the DVWA can be found on the official Git page at the following link: https://github.com/digininja/DVWA
- This page highlights some other web application attacks that you may want to review: https://owasp.org/www-project-top-ten/

# Section 3: Deep Dive into Defensive Security

This section will help you to move from pro to master by exposing you to the best systems, tools, and methods in defensive security.

This section contains the following chapters:

- Chapter 13, Vulnerability Assessment Tools
- Chapter 14, Malware Analysis
- Chapter 15, Leveraging Pentesting for Defensive Security
- Chapter 16, Practicing Forensics
- Chapter 17, Achieving Automation of Security Tools
- Chapter 18, The Master's Compilation of Useful Resources

# 13 Vulnerability Assessment Tools

"In the midst of a disruptive and exponential rollout of the IV Industrial Revolution, more and more processes are being digitized and robotized, and there is an explosion of data increasingly managed by artificial intelligence. In tandem with this rollout of new and enhanced IT capabilities, there are increased risks posed by cybercrime. Increased cybersecurity capabilities thus become one of the challenges to allow society to reap the benefits from the IV Industrial Revolution."

– Ennio Rodriguez, Ph.D. in Economics and President of the Association of Economists of Costa Rica

We have talked a lot about vulnerabilities throughout this book; however, this chapter was created as a single-point reference to this topic so that you can reach all the information you need about Managing vulnerabilities in a single place.

While Chapter 2, Managing Threats, Vulnerabilities, and Risks, described what vulnerabilities are and how to classify them, this chapter is more about how to identify those vulnerabilities once they are categorized.

Therefore, we can say that while Chapter 2, Managing Threats, Vulnerabilities, and Risks, was the theoretical part of vulnerability management, this chapter is more about the practical/technical side, including a deep dive into the tools used to find those vulnerabilities in our systems and infrastructure.

To achieve these goals, we will cover the following topics through this chapter:

- How to deal with vulnerabilities like a chief information security officer (CISO)
- Types of vulnerability testing tools
- Installing and configuring the most recognized vulnerability assessment scanner (Open Vulnerability Assessment System, also known as OpenVAS)
- An overview of Nexpose and other vulnerability assessment scanners available

# Technical requirements

To fully leverage the content of this chapter, it is recommended to have installed a virtual machine (VM) with Kali Linux to properly follow the labs.

# Dealing with vulnerabilities

As we saw in Chapter 2, Managing Threats, Vulnerabilities, and Risks, there is a process to manage vulnerabilities at the company level that includes identification, analysis, assessment, and remediation.

Now, that process is what we called the management side of the story. Now, it's time to understand how that is achieved from the operational (day-to-day) point of view.

# Who should be looking for vulnerabilities?

If you have a large enough budget, you must assign this task to either internal or external (third-party) Red Teams (as explained in Chapter 1, A Refresher to Defensive Security Concepts).

On the other hand, if your budget is limited, you can encourage your company to report any vulnerability on your infrastructure. To make this effective, you must establish and communicate a process for that purpose and, when possible, provide incentives to the people that find and report those vulnerabilities.

# Bug bounty programs

**Bug bounty** is a clever idea to encourage others to tell you about your vulnerabilities instead of exploiting them against you.

The goal of this program is to *offer economic incentives* to external people who find unknown vulnerabilities in your web resources (apps, pages, and so on).

> Tip
> Bug bounty programs are more suitable for companies with high security standards and softwares that have already been tested and hardened by internal Red and Blue teams. Therefore, publishing a bug bounty of a recently created site that has not properly hardened is a waste of resources.

As mentioned, bug bounty programs are normally offered by strong companies who invested a lot of resources on their platforms, so if you have very good pentesting skills, I highly encourage you to check these sites and learn more about these programs:

- https://hackerone.com/bug-bounty-programs
- https://hackproof.com/bug-bounty-solutions
- https://bugcrowd.com/programs
- https://www.facebook.com/BugBounty/
- https://www.microsoft.com/en-us/msrc/bounty
- https://github.com/
- https://internet.org/

Payment of bug bounty programs is normally classified based on the impact of the vulnerability, as shown in the following:

| Critical | High | Medium | Low |
| :--- | :--- | :--- | :--- |
| $2,500 | $500 | $300 | $150 |

Figure 13.1 – Bug bounty payment

# However, this may raise the following question:

Should I only check for external (internet-facing) systems?

# Internal vulnerabilities

While external-facing systems are more vulnerable to attacks, you are still in charge of the overall security of your data, which means you also need to take care of the availability and the integrity of that data, and those two factors are especially vulnerable to insider attacks (either malicious or unintentional).

Therefore, Red Teams should also perform testing on internal systems to ensure that the confidentiality, integrity, and availability of the data are preserved.

Have a look at the following screenshot:

img/8c6a223c57e25ea0cc1593903a1b20f_392_0.png

As seen in the preceding screenshot, vulnerability testing programs can be supplemented to enhance the security of your systems by leveraging even external sources.

# Vulnerability testing tools

There are a huge number of tools that can be used to perform vulnerability testing, and we can classify them into two main groups: manual vulnerability assessment and automated vulnerability scanners.

# Manual vulnerability testing

You can leverage many of the tools we have reviewed in the previous chapters to manually look for vulnerabilities—for example, Burp Suite, Nmap, Wordpress, Shodan, and Web Scrapers.

These types of testing require more technical skills and are normally done by cybersecurity experts or Red/Purple Teams.

# Automated vulnerability scanners

These scanners are created with the objective of making our lives easier by allowing us to scan a given web resource or system against one or more vulnerabilities with just a few steps—in fact, for most of them, with a single click.

This allows an organization to scan their systems for complex vulnerabilities without the need of a pentester to perform the vulnerability assessment, making these scanners a more suitable option for companies with little budget to hire pentes.
