![](images/cover.jpg)

![Cover](images/cover.jpg)

First Edition 2025

Copyright © BPB Publications, India

ISBN: 978-93-65896-800

All Rights Reserved. No part of this publication may be reproduced, distributed or transmitted in any form or by any means or stored in a database or retrieval system, without the prior written permission of the publisher with the exception to the program listings which may be entered, stored and executed in a computer system, but they can not be reproduced by the means of publication, photocopy, recording, or by any electronic and mechanical means.

LIMITS OF LIABILITY AND DISCLAIMER OF WARRANTY

The information contained in this book is true to correct and the best of author’s and publisher’s knowledge. The author has made every effort to ensure the accuracy of these publications, but publisher cannot be held responsible for any loss or damage arising from any information in this book.

All trademarks referred to in the book are acknowledged as properties of their respective owners but BPB Publications cannot guarantee the accuracy of this information.

![](images/BPB_Catalogue_QR.png)

[www.bpbonline.com](https://www.bpbonline.com)

**Dedicated to**

My son Filippo – the joy of my life

# About the Author

Luca Berton is a seasoned IT professional with over 18 years of experience in Linux system administration, cloud engineering, and automation. Renowned as an Ansible Automation expert, Luca has authored several best-selling books, including Ansible for VMware by Examples, Ansible for Kubernetes by Examples, Red Hat Ansible Automation Platform, and Hands-on Ansible Automation.

Luca’s dedication to open-source projects and his commitment to sharing knowledge are reflected in his creation of the Ansible Pilot project, which serves as a resource for automation enthusiasts worldwide. His expertise extends to presenting at international conferences, contributing to the growth of the Ansible community, and mentoring aspiring IT professionals.

As a thought leader and practitioner, Luca combines a deep technical understanding with practical insights, making his work a trusted resource for IT professionals globally. Through this book, he aims to equip readers with the skills and confidence to excel as Red Hat Certified Engineers and beyond.

# About the Reviewers

*   Tracy Reed has over 25 years of experience with Linux and cyber security. He is a Security Architect, vCISO, and cybersecurity expert witness as well as instructor at UC San Diego. Tracy has experience with container security, server hardening, intrusion detection, as well as ISO/NIST/SOC/PCI/HIPAA/CMMC compliance in cloud/virtualized/containerized environments. When not hacking, Tracy enjoys being a charter jet pilot, travel, sailing, and spending time with family.

*   Jerome Gotangco is a technology consultant with extensive experience in the IT industry. Currently an OpenShift Specialist at Red Hat, he champions the Open Hybrid Cloud approach for enterprises using open-source software platforms. Jerome has a strong background in OpenStack and Ubuntu development and previously served as an Azure consultant at Microsoft. He previously held technology consultant roles at Accenture and Hewlett Packard Enterprise. Beyond his technical expertise, Jerome enjoys reading, writing short stories and poems, and maintaining an active lifestyle with fitness and golf.

# Acknowledgement

Creating this book, Mastering the Red Hat Certified Engineer (RHCE) Exam, has been a journey of collaboration, effort, and learning. I am profoundly grateful to all who made this possible.

First, I extend my heartfelt thanks to my family for their unending support and patience during this journey. Their encouragement has been my foundation.

I am deeply appreciative of the guidance provided by my mentors and colleagues in the IT and open-source communities. A special acknowledgment goes to the Ansible community for nurturing the growth of automation enthusiasts like me.

Thank you to my publishers for their trust, vision, and professionalism in transforming this work into reality.

Lastly, to the readers, thank you for choosing this book. I hope it serves as a valuable guide on your path to certification and beyond.

# Preface

In today’s dynamic IT landscape, mastering Linux systems and automation is essential for professionals aiming to thrive in enterprise environments. This book, Mastering the Red Hat Certified Engineer (RHCE) Exam, is designed to guide readers through the complex yet rewarding journey of achieving one of the most prestigious certifications in the IT industry.

Comprising ten meticulously crafted chapters, this book equips readers with the knowledge and practical skills necessary to excel in the RHCE certification and beyond. It begins with an overview of the RHCE certification, its significance in the industry, and its alignment with modern IT practices. Subsequent chapters delve into Red Hat Enterprise Linux fundamentals and system administration, laying a solid foundation for managing and optimizing Linux environments.

Automation is at the heart of RHCE, and this book dedicates comprehensive chapters to mastering Ansible, from foundational scripting techniques to advanced enterprise-level automation strategies. Readers will also explore network services and security, learning to configure robust systems while ensuring data protection. The integration of emerging technologies such as containers, virtualization, and cloud platforms is addressed to prepare professionals for the evolving IT landscape.

Chapters on performance optimization and troubleshooting provide tools and frameworks for ensuring system reliability and diagnosing issues effectively. The book culminates with practice exams and real-world scenarios, simulating the challenges of the RHCE certification exam. A final chapter offers career development strategies, emphasizing how to leverage the RHCE certification for long-term success.

This book is not merely an exam preparation resource; it is a roadmap for building expertise in Linux administration and automation. With a structured approach, real-world examples, and actionable insights, this book aims to empower IT professionals at all levels—whether embarking on the RHCE journey or seeking to advance their careers in system management and automation.

I hope this book serves as a valuable resource in your journey to mastering Linux and achieving the RHCE certification.

[Chapter 1: Introduction to RHCE Certification](#ch01.xhtml) - This initial chapter introduces the significance of the Red Hat Certified Engineer (RHCE) credential in the IT industry. It explores the exam blueprint, highlighting the core skills required, such as system management and automation with Ansible. Readers will gain insights into the certification's relevance, career benefits, and practical applications. It also outlines the journey from RHCSA to RHCE, emphasizing essential tools and resources for success. By the end of this chapter, learners will understand how RHCE validates their expertise and enhances their professional standing.

[Chapter 2: Red Hat Enterprise Linux](#ch02.xhtml) - This chapter covers foundational Linux administration tasks with Red Hat Enterprise Linux (RHEL). Topics include system installation, user and group management, file system configuration, and remote access. Readers will also learn storage management techniques and how to configure network interfaces. The chapter emphasizes the role of RHEL in enterprise environments, providing tools for efficient administration and troubleshooting. Through practical exercises, learners will build a solid base for advanced RHEL operations and RHCE preparation.

[Chapter 3: Red Hat System Administration](#ch03.xhtml) - Focusing on key system administration tasks, this chapter prepares readers to manage RHEL systems effectively. Topics include process monitoring, software updates, and access control using ACLs. It delves into scheduling tasks, managing storage with LVM and RAID, and accessing network storage via SMB/NFS. Advanced skills such as systemd service management and boot process control are also covered. This chapter equips administrators to optimize and secure Linux environments while building critical competencies for the RHCE exam.

[Chapter 4: Automating Linux Tasks](#ch04.xhtml) - This chapter explores the transformative power of Ansible in automating routine Linux tasks. Readers will learn to create playbooks, manage inventories, and implement error handling with Ansible Vault. The chapter highlights the shift from traditional Bash scripting to declarative Ansible-based automation. Through hands-on activities, learners will master Ansible architecture, loops, and conditional tasks, enhancing their ability to streamline system management while meeting RHCE exam objectives.

[Chapter 5: Ansible Enterprise](#ch05.xhtml) - Building on automation basics, this chapter delves into Ansible's advanced features, including roles, collections, and the Ansible Automation Platform. It covers deploying secure environments with Ansible Vault and managing configurations across diverse infrastructures. Readers will explore content reuse strategies, such as leveraging prebuilt roles, to optimize automation workflows. Practical scenarios help learners apply these techniques effectively, ensuring proficiency in deploying scalable and secure solutions.

[Chapter 6: Network Services and Security Introduction](#ch06.xhtml) - This chapter addresses configuring and securing RHEL network services. It explains dual-stack networking for IPv4/IPv6, firewalld configuration, and SELinux policy management. Readers will also explore OpenSSH setups and cryptographic techniques for secure communications. The chapter emphasizes monitoring tools like tcpdump and Wireshark for traffic analysis. By mastering these techniques, learners will enhance their ability to secure and optimize RHEL-based networks.

[Chapter 7: Emerging Technologies Integration](#ch07.xhtml) - This chapter explores integrating advanced technologies such as containers, virtualization, and cloud platforms. Topics include using Universal Base Images for containerized applications and configuring RHEL with cloud providers. Readers will also learn about VDO for storage optimization and IMA for integrity assurance. By understanding these technologies, learners will position themselves to implement modern IT solutions effectively, aligning with RHCE competencies.

[Chapter 8: Performance Optimization and Troubleshooting](#ch08.xhtml) - This chapter focuses on ensuring system efficiency and reliability. It covers boot process management, root password recovery, and troubleshooting service failures. Readers will learn strategies for optimizing system performance using tools like tuned and system monitoring frameworks. Practical troubleshooting scenarios reinforce problem-solving skills, preparing learners for real-world challenges and RHCE exam readiness.

[Chapter 9: Practice Exams and Scenarios](#ch09.xhtml) - This chapter provides practical exercises and mock exams to simulate the RHCE certification experience. Readers will apply Ansible to automate administrative tasks, mastering modules and playbook strategies under exam-like conditions. The chapter includes time management tips and recommended resources, ensuring a structured preparation approach. By practicing real-world scenarios, learners gain confidence and refine their skills to excel in the RHCE exam.

[Chapter 10: Real World Application](#ch10.xhtml) - The final chapter explores leveraging the RHCE certification for career advancement. Topics include mapping skills to roles like DevOps engineer and cloud architect, networking within the Linux community, and staying current with industry trends. Readers will also learn how to showcase their expertise through portfolios and resumes. By following these strategies, learners can maximize their RHCE's value, ensuring continued professional growth.

# Code Bundle and Coloured Images

Please follow the link to download the

***Code Bundle*** and the ***Coloured Images*** of the book:

[https://rebrand.ly/dec413](https://rebrand.ly/dec413)

The code bundle for the book is also hosted on GitHub at [https://github.com/bpbpublications/Mastering-the-Red-Hat-Certified-Engineer-Exam](https://github.com/bpbpublications/Mastering-the-Red-Hat-Certified-Engineer-Exam). In case there’s an update to the code, it will be updated on the existing GitHub repository.

We have code bundles from our rich catalogue of books and videos available at [**https://github.com/bpbpublications**](https://github.com/bpbpublications). Check them out!

Errata

We take immense pride in our work at BPB Publications and follow best practices to ensure the accuracy of our content to provide with an indulging reading experience to our subscribers. Our readers are our mirrors, and we use their inputs to reflect and improve upon human errors, if any, that may have occurred during the publishing processes involved. To let us maintain the quality and help us reach out to any readers who might be having difficulties due to any unforeseen errors, please write to us at :

**[errata@bpbonline.com](mailto:errata@bpbonline.com)**

Your support, suggestions and feedbacks are highly appreciated by the BPB Publications’ Family.

**Join our book’s Discord space**

Join the book’s Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 1Introduction to RHCE Certification](#contents.xhtml_ch01a)

[Introduction](#contents.xhtml_sc2_1a)

Welcome to our journey into the world of Red Hat Certified Engineer (RHCE) certification. This chapter provides an essential foundation for understanding the significance of RHCE in the IT industry. Readers will gain insight into the specific skill set that RHCE validates and why it is highly regarded by employers worldwide. We will set the stage for the reader's personal journey toward becoming a certified engineer, emphasizing the value of this achievement and how it can propel one's career in IT.

[Structure](#contents.xhtml_sc2_2a)

The chapter covers the following topics:

*   IT industry
*   Overview of RHCE certification
*   RHCE and RHCSA
*   Getting certified
*   Already certified
*   RHCA
*   Exam blueprint
*   Essential tools
*   After certification

[Objectives](#contents.xhtml_sc2_3a)

By the end of this chapter, readers will learn the content of the RHCE, the exam blueprint, and why it is important in the IT industry today. Readers will have a clear understanding of what to expect from the RHCE certification and why it is a goal worth pursuing.

[IT industry](#contents.xhtml_sc2_4a)

Since 2006, the RHCE has been considered one of the most requested certifications in the IT industry. The RHCE holds significant importance in serving as a key credential for professionals aiming to excel in system administration, particularly within Red Hat Enterprise Linux. This certification equips individuals with the understanding, knowledge, and operational skills essential for managing and administering complex enterprise Linux systems. Red Hat Enterprise Linux, developed by Red Hat, is widely used in commercial markets, including servers, mainframes, and supercomputers. The RHCE program is one of the most recognized Linux accreditations globally, opening doors to many job opportunities and a highly rewarding career. With a focus on practical skills like setting kernel parameters, configuring network services, and utilizing shell scripting for automation, the RHCE program ensures that certified engineers are well-prepared for the challenges of senior system administration roles. The research from Infosec Institute, Inc. estimates 101,527 USD as the average salary of RHEL-certified engineers. The RHCE comprehensive curriculum distinguishes itself among the other Linux certifications in the market: Oracle Certified Professional Oracle Linux System Administrator, CompTIA Linux+, Linux Professional Institute from LPIC-1 to LPIC-3 Mixed Environments , and Linux Foundation Certified System Administrator and Engineer (LFCS). The RHCE is a valuable asset for IT professionals seeking career advancement in the dynamic field of enterprise Linux servers. The independent organization IT Jobs Watch Ltd.^([1](#ch01.xhtml_footnote-005)) is taking some statistics about the requests for the RHCE certification in the IT job posting advertisement in the United Kingdom that confirms this data, as shown in [Figure 1.1](#ch01.xhtml_fig1-1):

![](images/Figure_1.1.png)

Figure 1.1: Job postings citing RHCE as a proportion of all IT jobs advertised, Source: IT Jobs Watch Ltd

[Overview of RHCE certification](#contents.xhtml_sc2_5a)

Embarking on the path to becoming an RHCE is an exciting journey for IT professionals seeking to validate their skills and elevate their careers. This chapter explores the critical steps in this process, from the foundational Red Hat Certified System Administrator (RHCSA) certification to an in-depth analysis of the RHCE exam blueprint. It delves into the theoretical concepts and practical skills required to navigate these certifications successfully. The RHCE certification is the most recognized Linux accreditation in the world today. This book provides a guide about preparation skills and capabilities for successfully administering a Red Hat Enterprise Linux system. This book explains the process of obtaining the solution because the exam is a practical hands-on session. This way, we are future-proof as the exam content might vary, but the knowledge necessary is more or less the same. This book is a strong foundation, but we encourage you to have as much practical experience as possible as it pays out, especially in the work environment. The process involves general knowledge of the system and practical experience. The questions and answers are strictly reserved by the Red Hat Certification Central, and the candidates are discouraged from sharing them. Always remember that the ultimate goal of the RHCE certification is to demonstrate practical skills in the Linux operating system.

The following co-occurring skills and capabilities usually correlate the UK job postings at the moment of writing this book: Linux (100%), Red Hat (95%), Ansible (64%), Docker (64%), Unix (59%), Puppet (59%), Python (54%), configuration management (55%), Agile (55%), DevOps (55%), Kubernetes (55%), and task automation (55%). These skills are expected as the RHCE is based on the Red Hat Enterprise Linux; it uses Ansible technology for configuration and task automation and comprehends container orchestration. A plus is represented by individuals who use the Python programming language. The RHCE opens endless opportunities in the IT industry for DevOps engineers, data center, cloud, DevOps, application development, and application platforms.

IT Jobs Watch Ltd. also evaluated the salary expectation, as shown in [Figure 1.2](#ch01.xhtml_fig1-2):

![](images/Figure_1.2.png)

Figure 1.2: Source IT Jobs Watch Ltd.: 3-month moving average salary quoted in jobs citing RHCE

According to a study conducted by the Ireland company Research and Markets^([2](#ch01.xhtml_footnote-004)), the projected global server operating system market is anticipated to attain a value of $29.4 billion by 2028, showcasing a robust Compound Annual Growth Rate (CAGR) of 8.8% throughout the forecast period. Refer to the following [Figure 1.3](#ch01.xhtml_fig1-3):

![](images/Figure_1.3.png)

Figure 1.3: Server operating system market size

According to the report of IDC, the international advisor organization, Worldwide Server Operating Environments Market Shares, 2018: Overall Market Growth Accelerates:

Red Hat Enterprise Linux subscriptions grew by more than 14% in 2018, representing more than 33% of the total paid enterprise operating system environments. This ties in with Red Hat sponsored research from IDC that shows how Red Hat Enterprise Linux touches more than $10 trillion of the global business economy.

![](images/Figure_1.4.png)

Figure 1.4: Displays the global server operating system distribution market data

[RHCE and RHCSA](#contents.xhtml_sc2_6a)

As organizations increasingly embrace digital transformation, showcasing Linux automation skills has become paramount in the dynamic landscape of IT. The RHCE credential is a testament to an individual's proficiency in managing systems within a DevOps environment, a critical requirement in today's IT operations. At the core of DevOps lies automation, and the RHCE credential extends one's knowledge to encompass the automation of deployment, management, and support across multisystem environments, elevating the credential's value and relevance. For existing and aspiring RHCEs and RHCSAs, there are distinct paths to completing or renewing the RHCE certification provided by Red Hat Learning or ourselves. If we choose the official Red Hat Learning paths for RHCSA, as shown in [Table 1.1](#ch01.xhtml_tab1-1):

| Certification | Standard study path | Rapid study path |
| RHCSA | Red Hat System Administration I (RH124) | RHCSA Rapid Track Course (RH199) |
| Red Hat System Administration II (RH134) |
| RHCE | Red Hat System Administration III: Linux Automation with Ansible (RH294) | Not available |
| Red Hat Certified Architect (RHCA) | Many options | Not available |

Table 1.1: RHCSA and RHCE study paths

Refer to the following [Figure 1.5](#ch01.xhtml_fig1-5) to look at the RHCSA badge:

![](images/Figure_1.5.png)

Figure 1.5: RHCSA badge

[Table 1.1](#ch01.xhtml_tab1-1) shows two Red Hat study paths via the Red Hat training. The standard skills path includes Red Hat courses Red Hat System Administration I (RH124) and Red Hat System Administration II (RH134), whereas the rapid skills path includes only the RHCSA Rapid Track Course (RH199). Both paths culminate in the RHCSA exam, which is the prerequisite for advancing along the RHCE skills path. If we choose the official Red Hat Learning paths for RHCE, refer to [Table 1.1](#ch01.xhtml_tab1-1).

Refer to the following [Figure 1.6](#ch01.xhtml_fig1-6) to look at the RHCE badge:

![](images/Figure_1.6.png)

Figure 1.6: RHCE badge

Once RHCSA is achieved, Red Hat Learning suggests individuals to proceed to enhance their skills through the Red Hat System Administration III: Linux Automation with Ansible (RH294) course, as shown in Table 1.2, preparing them for the RHCE exam (EX294). When writing this book, the course is based on Red Hat Enterprise Linux and Red Hat Ansible Automation Platform. This training is delivered as remote training or in-person training. The duration is five full days and costs nearly 4,000 USD. Large organizations take advantage of the Red Hat Learning Subscription, which provides cost-effective and flexible options for employees. This book is an alternative to these skill paths, offering the foundation and experiences from the real-world use case. It not only validates Linux automation proficiency but also positions individuals at the forefront of IT capabilities in an ever-evolving technological landscape.

The RHCSA is the starting point for individuals aiming to demonstrate their proficiency in managing Red Hat Enterprise Linux systems. This certification validates fundamental skills such as understanding essential tools, operating running systems, configuring local storage, and managing users and groups. Achieving RHCSA certification is a prerequisite for those aspiring to become RHCEs, setting the stage for a deeper exploration of advanced concepts.

The duration of preparation for RHCSA and RHCE certifications varies from person to person based on individual learning pace, prior experience, and familiarity with Linux systems. Given the challenging nature of these certifications, a diligent study plan coupled with extensive hands-on practice is crucial for success. As a general guideline, many candidates allocate several weeks to months of focused preparation before attempting the RHCSA and RHCE exams. During this period, it is essential to immerse oneself in real-time problem-solving scenarios and develop skills in risk management, as these certifications are designed to assess a candidate's ability to handle complex system administration tasks in a Red Hat Enterprise Linux environment. To prepare for the RHCSA exam, candidates should engage in hands-on practice covering tasks such as file and directory handling, partition management, user and group administration, SELinux configuration, and system deployment. A thorough understanding of these tasks is essential before attempting the RHCSA certification.

Once RHCSA is achieved, candidates can progress to RHCE by further refining their skills in configuring networking services, remote logging, kernel parameter setting, and Ansible automation. This phase requires additional study and practical experience, building upon the foundation established during RHCSA preparation.

Resources for study include various books, online materials such as e-books and videos, and specialized training programs like the Red Hat Learning Subscription. Joining Red Hat training institutes is also recommended, providing candidates with hands-on experience under the guidance of certified engineers and exposure to real-world problem-solving scenarios.

The key to success in RHCSA and RHCE certifications lies in a well-structured study plan, hands-on practice, and a commitment to continuous learning. The certifications not only validate our skills as a system administrator but also open doors to advanced career opportunities in the field.

[Getting certified](#contents.xhtml_sc2_7a)

Aspiring IT professionals to embark on a structured journey towards RHCE certification, typically beginning with foundational courses like Red Hat System Administration I (RH124) and Red Hat System Administration II (RH134), as shown in [Table 1.1](#ch01.xhtml_tab1-1). These courses lay the groundwork for the RHCSA certification, covering essential skills and knowledge required for effective system administration. Following this, the RHCSA Rapid Track Course (RH199), as shown in [Table 1.1](#ch01.xhtml_tab1-1), provides an accelerated path for those with comparable work experience.

To further enhance their capabilities, candidates often pursue Red Hat System Administration III: Linux Automation with Ansible (RH294), as shown in [Table 1.1](#ch01.xhtml_tab1-1), which introduces automation using Ansible, a key component of the RHCE exam. This book equips candidates with the skills needed to automate tasks, laying the groundwork for the more advanced challenges presented in the RHCE exam.

[Already certified](#contents.xhtml_sc2_8a)

For existing RHCE who obtained their certification on Red Hat Enterprise Linux 7 or an earlier version, the opportunity to enhance their skill set lies in recertifying through the RHCE exam (EX294). This recertification allows us to augment our automation skills within a container-based infrastructure, a crucial aspect of modern IT environments. While not mandatory, recertifying allows us to familiarize ourselves with the latest advancements and changes in the RHCE credential, presenting unique opportunities to expand our knowledge. The automation skills gained through RHCE are foundational for implementing automation across an organization, making them essential for scaling various Red Hat technologies. Moreover, holding an RHCE credential contributes towards the pursuit of becoming a RHCA in infrastructure, as shown in [Table 1.1](#ch01.xhtml_tab1-1), providing a clear pathway for career advancement. We can also further specialize by applying additional exams, such as the Red Hat Certified Specialist in Developing Automation with Ansible Automation Platform (EX374) and the Red Hat Certified Specialist in Managing Automation with Ansible Automation Platform (EX467), towards our RHCA credential. For any inquiries related to certification renewal or information on RHCA and other RHCE-related tracks, the frequently asked questions section is a valuable resource.

To verify a RHCE certification, we can use the Red Hat Certification Central verification service. Follow these steps to verify an RHCE certification:

1.  Access Red  Hat Certification  Central: Visit the Red Hat Certification Central website, which is the official platform for managing and verifying Red Hat certifications. The URL is [https://www.redhat.com/rhtapps/certification/verify](https://www.redhat.com/rhtapps/certification/verify).
2.  Locate  certification verification section: Look for a section on the webpage that allows we to verify a Red Hat Certified Professional. This section may be labeled Verify a Red Hat Certified Professional or something similar.
3.  Enter  certification ID: In the provided fields, enter the certification ID for the RHCE candidate we want to verify. The certification ID is usually in the format ###-###-###.
4.  Submit the  form: After entering the certification ID, submit the form or click the verification button to initiate the verification process.
5.  Review the  results: The system will check the entered certification ID against its database of certified professionals. If the certification ID is valid and corresponds to an RHCE certification, we will receive confirmation of the certification status.
6.  Check certification  expiry: Keep in mind that Red Hat certifications have an expiration date. Ensure that the certification is still considered current. If it has expired, it may not appear in the verification results.

Suppose we encounter any issues or have specific questions about the verification process. In that case, we may use the contact form provided on the Red Hat Certification Central website to seek assistance or clarification. Always refer to the official Red Hat Certification Central website for the most current and accurate information.

[RHCA](#contents.xhtml_sc2_9a)

Becoming an RHCE is an impressive accomplishment, but for those seeking to further elevate their expertise in Red Hat technologies, pursuing the RHCA credential might be the next step. The RHCA credential allows RHCEs to showcase a broader skill set and in-depth knowledge spanning Red Hat Enterprise Linux and other key products within the Red Hat ecosystem. Refer to the following [Figure 1.7](#ch01.xhtml_fig1-7) to take a look at the RHCA badge:

![](images/Figure_1.7.png)

Figure 1.7: RHCA badge

RHCEs have the flexibility to curate their certification journey by selecting certifications within the RHCA in infrastructure list. Achieving five or more certifications from the system administrator list in the Skills tab qualifies candidates to attain the coveted title of Red Hat Certified Architect in Infrastructure.

For those craving an even higher level of recognition, pursuing more than five credentials beyond the base certifications propels candidates to RHCA Level II. It is essential to maintain the currency of all six credentials for the RHCA Level II designation. If one credential becomes non-current, the status reverts to Level I. Two non-current credentials nullify the RHCA designation.

[Open hybrid cloud program](#contents.xhtml_sc3_10a)

Embracing the open hybrid cloud is integral to contemporary enterprise computing. The open hybrid cloud program equips professionals to guide organizations seamlessly into the cloud, aligning with business needs. Earning five certifications from the following list prepares individuals for this transformative journey:

*   Red Hat Certified Specialist in Virtualization
*   Red Hat Certified Specialist in OpenShift Administration
*   Red Hat Certified Specialist in Cloud Infrastructure
*   Red Hat Certified Specialist in Deployment and Systems Management
*   Red Hat Certified Specialist in Ansible Network Automation
*   Red Hat Certified Specialist in Ceph Cloud Storage
*   Red Hat Certified Specialist in OpenShift Automation and Integration
*   Red Hat Certified Specialist in OpenShift Virtualization
*   Red Hat Certified Specialist in Containers

[DevOps, containers, and OpenShift program](#contents.xhtml_sc3_11a)

Containers are revolutionizing application development, and Red Hat OpenShift Container Platform is at the forefront of this evolution. DevOps practices, containers, and OpenShift pave the way for faster application development cycles. Acquiring the following credentials, plus one from the system administrators list, empowers professionals to reshape the application delivery landscape:

*   Red Hat Certified Specialist in OpenShift Administration
*   Red Hat Certified Specialist in API Management
*   Red Hat Certified Specialist in Advanced Automation: Ansible Best Practices
*   Red Hat Certified Specialist in OpenShift Automation and Integration
*   Red Hat Certified Specialist in OpenShift Virtualization
*   Red Hat Certified Specialist in Containers
*   Red Hat Certified Specialist in OpenShift Data Foundation
*   Red Hat Certified Specialist in MultiCluster Management

[Telco cloud program](#contents.xhtml_sc3_12a)

The telecommunications industry is transforming towards Software-Defined Networking (SDN) and Network Functions Virtualization (NFV). Red Hat technologies, including the OpenStack platform, are pivotal in this evolution. Telco IT professionals can validate their skills by earning the following certifications:

*   Red Hat Certified Specialist in Cloud Infrastructure
*   Red Hat Certified Specialist in Ansible Network Automation
*   Red Hat Certified Specialist in Ceph Cloud Storage
*   Red Hat Certified Specialist in Containers
*   Red Hat Certified Specialist in OpenShift Virtualization
*   Red Hat Certified Specialist in MultiCluster Management

[Linux mastery program](#contents.xhtml_sc3_13a)

The foundational strength of Red Hat technologies lies in Red Hat Enterprise Linux. For those seeking to delve deep into Linux mastery, choosing five certifications from the following options is the key:

*   Red Hat Certified Specialist in Linux Diagnostics and Troubleshooting
*   Red Hat Certified Specialist in Linux Performance Tuning
*   Red Hat Certified Specialist in Identity Management
*   Red Hat Certified Specialist in High Availability Clustering
*   Red Hat Certified Specialist in Deployment and Systems Management
*   Red Hat Certified Specialist in Advanced Automation: Ansible Best Practices
*   Red Hat Certified Specialist in Security: Linux

The journey from RHCE to RHCA is a testament to an IT professional's commitment to continuous learning and mastery of Red Hat technologies. Whether delving into the intricacies of Linux, embracing the open hybrid cloud, leading in DevOps practices, or navigating telco cloud transformations, the RHCA credential opens doors to new opportunities and challenges. Tailor your path based on your passions and organizational needs, and embrace the evolving landscape of IT expertise. The RHCA awaits those ready to ascend to new heights in their Red Hat journey.

[Exam blueprint](#contents.xhtml_sc2_14a)

The RHCE exam is a performance-based assessment designed to evaluate candidates on their ability to manage multiple systems using Red Hat Ansible. The official exam is provided by the Red Hat Training and Certification department. The RHCE exam strikes a balance between theoretical understanding and hands-on experience. Candidates must not only grasp the theoretical concepts of Ansible but also apply them in real-world scenarios. This dual focus ensures that certified engineers are not only well-versed in the principles of automation but also capable of implementing them effectively in diverse environments. The exam blueprint encompasses both theoretical concepts and practical skills, reflecting the diverse responsibilities of a RHCE, as follows:

*   Theoretical  concepts: Candidates are expected to demonstrate an understanding of the core components of Ansible, including inventories, modules, variables, facts, loops, conditional tasks, plays, handling task failure, playbooks, configuration files, and roles. Theoretical knowledge is essential for effectively using Ansible to automate system administration tasks and integrate emerging Red Hat technologies.
*   Practical  skills: The practical aspect of the exam requires candidates to install and configure Ansible Core on multiple systems. They must then create Ansible Playbooks, which are evaluated by applying them to freshly installed systems. Tasks involve configuring systems for specific roles and behaviors, such as managing software packages, services, firewall rules, file systems, storage devices, and more.

While it is technically possible to take the RHCE exam without having first obtained the RHCSA certification, it is important to note that earning the RHCSA certification is a prerequisite for obtaining the RHCE certification. The RHCE exam is a hands-on, practical test that assesses advanced skills in Linux system administration, building upon the foundational knowledge tested in the RHCSA exam. Therefore, although we may be eligible to attempt the RHCE exam without having the RHCSA certification, we will not be awarded the RHCE certification until both credentials are earned. The RHCSA certification is an essential step that ensures candidates have the fundamental skills and knowledge needed to tackle the more advanced topics covered in the RHCE exam. It is highly recommended to follow the proper sequence and obtain the RHCSA certification before pursuing the RHCE certification to ensure a comprehensive understanding of Red Hat Enterprise Linux system administration.

The RHCE exam costs USD 500 at the moment of writing this book, encompassing the examination fee alone and excluding any associated training expenses. We can buy the exam directly from the Red Hat Learning website ([https://www.redhat.com/en/services/certification/individual-exams](https://www.redhat.com/en/services/certification/individual-exams)), as shown in [Figure 1.8](#ch01.xhtml_fig1-8):

![](images/1.png)

Figure 1.8: Red Hat Learning exam

For candidates opting to undergo the RHCE training course before undertaking the exam, an additional investment is required for the training component. This training prepares candidates thoroughly for the challenges presented in the RHCE exam, ensuring a comprehensive understanding of the required knowledge and skills related to Red Hat Enterprise Linux system administration. While the exam fee is a fixed cost, the training investment provides candidates with valuable insights and hands-on experience, potentially enhancing their chances of success in obtaining the RHCE certification. The combined cost of the exam and training reflects the commitment required to excel in the IT industry and leverage the advantages offered by this esteemed certification. As of the latest information available, Red Hat certifications, including the RHCE, are valid for a period of three years. After this duration, the certifications do not expire or become terminated, but they do become non-current. To maintain the current status of the certification, individuals are encouraged to participate in the Red Hat Certification Program's Continuing Education requirements, which involve earning and submitting certain credentials to extend the validity of the certification. This practice ensures that certified professionals stay up-to-date with the evolving technologies and industry standards in the fast-paced field of information technology.

Following are the key details about the RHCE exam:

*   Exam code: EX294
*   Duration: 4 hours (240 minutes)
*   Type: Performance based (hands-on)
*   Questions: 20 questions with no multiple-choice options
*   Restrictions: No internet access and constant video recording
*   Prerequisite: RHCSA certification
*   Passing score: 210 out of 300 total points exclusively from Red Hat Certification Central, communicated within 3 U.S. business days.
*   Retake policy: Candidates are eligible for one exam retake if they are unsuccessful on their first attempt.

The RHCE exam tests our abilities in the following areas, which are fundamental for system administration across various Red Hat products.

The RHCE exam is entirely hands-on and practical. Candidates are required to use the Red Hat Ansible Engine to perform real-world tasks. Multiple systems are provided, and candidates must install and configure Ansible. The exam includes a list of tasks related to the exam objectives. The exam might be executed in person in a fully qualified Red Hat test center location (Red Hat KIOSK) or remotely using the Red Hat remote exam. Full internet access is not allowed during the exam, and candidates are not allowed to bring any hard copy or electronic documentation. If we were to opt-in for the remote execution of the exam, a valid government identifying document and a full 360° scan of the room using the webcam are required before starting the exam. Please note that the exam registered person must match the government identifying document provided. The system will boot from the only authorized Red Hat USB image. The system is based on Fedora Linux and specifically designed for the exam. Please note that we are not allowed to connect any docking station or additional peripherals to the computer used for the exam. We recommend reading the official information provided in the Setting up for your Red Hat remote exam: Things you need to do the first^([3](#ch01.xhtml_footnote-003)) article before scheduling our exam. The remote exam Live USB system will test our system for the requirements during the startup. Please note that virtual machines and screenshots are not allowed by the remote exam system.

Following are the requirements for the remote exam:

*   Computer: Intel-compatible X86_64-bit architecture with one single active monitor.
*   RAM: A minimum 4GB.
*   Internet connection speed: Download speed requirements are 768kbps, and upload speed requirements are 512kbps, wired preferred.
*   Webcam: One external webcam, even if your laptop has one built-in, with at least a 1m cable.
*   Keyboard: Only one keyboard is allowed for the exam. If an external keyboard is used, the laptop lid must be closed.
*   Sound and microphone: A working microphone is required.
*   Power: An Uninterrupted Power Supply (UPS) is required for our computer or a laptop with a full battery connected to the electricity.
*   USB drive: One USB drive with at least 8 GB storage, USB 2.0 or higher.
*   Adapters: Newer Mac users will need a USB-C adapter converter for plugging in a network cable and a USB-C adapter to connect a conventional wired mouse or keyboard.
*   Food and snacks:  These are  allowed but need to be shown in the beginning with the proctor.

Our exam is listed in the Live USB system one hour before the scheduled time in the booking system.

The exam becomes available almost half an hour before the session starts, and a proctor is available via chat during the duration. He/she is going to assist with all the exam needs.

Following are the best advice for succeeding in the exam:

*   Health and well-being: Ensure you are well-rested before the exam. Maintain a healthy balance between study and personal well-being.

*   Preparation is key: Adequate preparation is essential for success in any endeavor. Plan your approach and study schedule to cover all necessary topics.
*   Documentation is helpful: Familiarize yourself with relevant documentation and help pages available in the operating system. Know where to find information quickly during the exam.
*   Understand exam objectives: Thoroughly review the exam blueprint or objectives. Focus on key areas and ensure comprehensive understanding.
*   Community support: Join forums or communities related to the certification. Discuss topics, ask questions, and learn from others' experiences.
*   Review and revise: Regularly review previously covered material. Reinforce your understanding through revision.
*   Technical troubleshooting: Be prepared to troubleshoot technical issues during the exam. Familiarize yourself with common problems and solutions.
*   Confidence building: Believe in your preparation and abilities. Approach the exam with confidence and a positive mindset.
*   Read instructions carefully: Take the time to carefully read all instructions. Understand the format and requirements of each exam section.
*   Time management: Allocate time wisely during the exam. Practice time management during preparation to improve efficiency.
*   Stay calm under pressure: Maintain composure during the exam. If faced with a challenging question, move on and return to it later.
*   Post-exam review: After the exam, reflect on your performance. Identify areas for improvement in future preparations.
*   Continuous learning: Certification is a stepping stone; embrace continuous learning. Stay curious and explore new technologies and advancements.

These points serve as a general guide, and specifics may vary based on the type of certification or exam you are preparing for.

[Essential tools](#contents.xhtml_sc2_15a)

In the realm of Linux system administration, mastering essential tools is foundational for efficiently managing and maintaining a system. These tools serve as the linchpin for administrators, enabling them to perform a diverse array of tasks seamlessly. The command line interface (CLI) becomes a primary workspace, where utilities such as ls for listing directory contents, cp for copying files, and mv for moving or renaming files lay the groundwork for basic file and directory operations. Networking tools like ping and traceroute facilitate network diagnostics, ensuring connectivity and pinpointing issues. Text editors like vim or nano empower administrators to modify configuration files and scripts. Package management tools, including yum, dnf, or apt, streamline software installation and updates. Furthermore, monitoring and troubleshooting utilities such as top or htop provide real-time insights into system performance. These essential tools form the nucleus of a Linux administrator's skill set, allowing them to navigate and orchestrate diverse tasks within the operating system efficiently. The RHCE exam requires the ability of the candidate to use the following tools:

*   Operating running systems
*   Configuring local storage
*   Creating and configuring file systems
*   Deploying, configuring, and maintaining systems
*   Managing users and groups
*   Managing security
*   Understanding core components of Ansible, such as inventories, modules, variables, facts, loops, conditional tasks, plays, handling task failure, playbooks, configuration files, and roles
*   Using Ansible documentation to look up specific information about Ansible modules and commands
*   Working with roles and Ansible Content Collections
*   Installing and configuring an Ansible control node
*   Configuring Ansible-managed nodes
*   Analyzing and converting simple shell scripts into Ansible playbooks
*   Running playbooks with automation content navigator
*   Creating Ansible plays and playbooks
*   Automating standard RHCSA tasks using Ansible modules for software packages, services, firewall rules, file systems, storage devices, file content, archiving, task scheduling, security, and users/groups
*   Managing content using templates and Ansible vault for sensitive data protection

We are going to learn as many terms and concepts as possible but a basic knowledge of the Linux operating system and terminology is recommended to take full advantage of this book.

[After certification](#contents.xhtml_sc2_16a)

Red Hat's comprehensive certification program spans various technology domains, instilling confidence in individuals and organizations by validating expertise in areas such as enterprise architecture, Linux system administration, developer skills, and cutting-edge technologies like containers and cloud computing. Red Hat offers digital credentials in partnership with Credly, serving as a recognized industry achievement that can be shared with professional networks and displayed on social media or resumes. These digital badges are shareable, verified, and portable and provide a data rich representation of one's learning achievements, community contributions, and ecosystem engagement related to Red Hat technologies. Claiming a Red Hat digital badge is a straightforward process involving email acceptance, Credly account creation, and sharing options for various platforms. For inquiries or support, a contact form is available for Red Hat certification related concerns, while Credly offers support for account related queries and badge claiming issues. The collaboration between Red Hat and Credly ensures a seamless experience for individuals showcasing their Red Hat certifications. Showcase your skills, and effectively managing our licenses and certifications can significantly boost our capability of success on professional platforms like LinkedIn. To showcase your knowledge and accomplishments, follow these steps to add or edit your Licenses and certifications section. Credly by Pearson is a leading platform hosting the most extensive and interconnected digital credential network globally. Its primary mission is to facilitate a universal language for validated knowledge, skills, and abilities, enabling individuals and organizations to articulate and recognize competencies effectively. Refer to the following Figure 1.10:

![](images/Figure_1.9.png)

Figure 1.9: Credly logo

By leveraging Credly, organizations can issue digital badges, glean valuable insights from the talent marketplace, and utilize verified skills data to enhance human capital management decision making. With a commitment to empowering the workforce and unlocking an organization's true potential, Credly serves as a pivotal tool for navigating the evolving landscape of credentialing and skill verification. A digital credential or badge is a visual representation of a learning outcome, experience, or competency based on the Open Badges standard. Those issued by Credly are securely verified, making it easy for you to share your achievements online, including on platforms like LinkedIn. Explore badges associated with related skills from a vast selection of over 3,000 employer trusted organizations. Your journey to success continues with the recognition and celebration of your skills and accomplishments.

[Conclusion](#contents.xhtml_sc2_17a)

In this chapter, we covered the RHCE certification, its importance for the IT industry, and the career opportunities. We  covered various types of reasons and blueprints of the RHCE exam.

In the next chapter, we are going to learn about Linux Enterprise Linux internals and get our hands dirty with some terminal interaction and code examples.

[Points to remember](#contents.xhtml_sc2_18a)

*   Since 2006, the RHCE certification has held significant importance in the IT industry, being recognized and requested as one of the hottest certifications for managing and administering complex Red Hat Enterprise Linux systems.
*   RHCSA is an entry level certification validating essential Linux system administration skills, while RHCE is an advanced certification demonstrating in-depth knowledge and practical expertise in managing Red Hat Enterprise Linux systems.
*   RHCE certified engineers are well-prepared for senior system administration roles, contributing to its popularity and competitive average salary.
*   The certification's comprehensive curriculum and high demand in job postings for IT professionals seeking career advancement in the dynamic field of enterprise Linux servers.

[Multiple choice questions](#contents.xhtml_sc2_19a)

1.  How long is the RHCE exam?
    1.  90 minutes (1h 30m)
    2.  120 minutes (2h)
    3.  300 minutes (5h)
    4.  240 minutes (4h)
2.  What is the highest certification among the following?
    1.  RHCA Level I
    2.  RHCA Level II
    3.  RHCE
    4.  RHCSA
3.  What are the two possible exam options?
    1.  Red Hat KIOSK and Red Hat remote exam
    2.  Red Hat office and Red Hat events
    3.  Red Hat KIOSK and Red Hat Summit
    4.  Red Hat remote exam and Red Hat events
4.  What is the passing score for the RHCE exam?
    1.  100 out of 300 total points
    2.  150 out of 300 total points
    3.  210 out of 300 total points
    4.  200 out of 300 total points

[Answer](#contents.xhtml_sc3_20a)

1\. d

2\. b

3\. a

4\. c

[Questions](#contents.xhtml_sc2_21a)

1.  What is the impact of the RHCE certification in the IT market?
2.  Why the RHCSA and RHCE certifications are important?
3.  What are the career opportunities of the RHCSA certification?
4.  What are the career opportunities of the RHCE certification?
5.  How to verify a RHCE certification?
6.  What is the way forward for professionals who would like to elevate their expertise in Red Hat technologies beyond RHCE?

[Key terms](#contents.xhtml_sc2_22a)

*   RHCSA:  The RHCSA certification validates the essential skills and knowledge required to proficiently perform system administration tasks in a Red Hat Enterprise Linux environment.
*   RHCE: The RHCE certification demonstrates advanced proficiency in managing multiple systems using Red Hat Ansible, executing common system administration tasks across diverse systems, and serves as a foundational step towards becoming a RHCA.
*   RHCA: The RHCA credential signifies the pinnacle of expertise in Red Hat technologies, demonstrating a comprehensive mastery across various domains, from Linux administration and open hybrid cloud solutions to DevOps practices and telco cloud transformations.
*   KIOSK: The Red Hat KIOSK is a fully qualified Red Hat test center location where in-person exams, including the RHCE exam, can be conducted.
*   Remote exam: The Red Hat remote exam allows candidates to take exams, such as the RHCE exam, remotely from their own locations using a secure online platform while adhering to specific requirements and protocols.

* * *

[1](#ch01.xhtml_footnote-005-backlink) [https://www.itjobswatch.co.uk/jobs/uk/rhce.do](https://www.itjobswatch.co.uk/jobs/uk/rhce.do)

[2](#ch01.xhtml_footnote-004-backlink) [https://www.researchandmarkets.com/reports/5709460/global-server-operating-system-market-size](https://www.researchandmarkets.com/reports/5709460/global-server-operating-system-market-size)

[3](#ch01.xhtml_footnote-003-backlink) [https://www.redhat.com/en/blog/setting-your-red-hat-remote-exam-things-you-need-do-first](https://www.redhat.com/en/blog/setting-your-red-hat-remote-exam-things-you-need-do-first)

# [CHAPTER 2Red Hat Enterprise Linux](#contents.xhtml_ch02a)

[Introduction](#contents.xhtml_sc2_23a)

This chapter introduces essential Linux administration skills, covering topics such as getting started with Red Hat Enterprise Linux (RHEL), operating systems, configuring storage, creating file systems, accessing Linux file systems, installing on servers and virtual machines, deploying and maintaining systems, configuring remote access, managing users and groups, configuring network interfaces, and handling files from the command line.

[Structure](#contents.xhtml_sc2_24a)

The chapter covers the following topics:

*   Getting started
*   Installation methods
*   Operate running systems
*   Getting help post-installation
*   Users and groups
*   Storage
*   Configure and maintain systems
*   Remote access
*   Network interfaces and settings
*   Manage files

[Objectives](#contents.xhtml_sc2_25a)

The learning objectives of this chapter are designed to equip learners with a robust foundation in managing and operating RHEL systems. By the end of this chapter, students are expected to gain a comprehensive understanding of essential Linux administration tasks. These include navigating the RHEL environment, configuring storage solutions, managing file systems, and ensuring secure access. Additionally, learners will delve into the processes of installing RHEL on servers and virtual machines, deploying and maintaining systems, and configuring remote access. The chapter also emphasizes the importance of managing users and groups, configuring network interfaces, and mastering file manipulation through the command line. Furthermore, creating, viewing, and editing text files will enhance the student's ability to efficiently handle typical system administration tasks. Through this structured learning path, students are prepared to tackle real-world challenges in system administration, ensuring they have the necessary skills to manage RHEL environments effectively.

[Getting started](#contents.xhtml_sc2_26a)

RHEL is an exciting and essential endeavor for anyone looking to establish a strong foundation in Linux system administration. This chapter lays the groundwork for our journey into RHEL, providing the knowledge and skills necessary to navigate and administer Linux systems confidently. Whether we are a novice or an experienced IT professional, mastering these foundational concepts is essential for building a robust and reliable Linux infrastructure. RHEL stands as a stalwart in enterprise IT, delivering flexibility and reliability to new frontiers, from the public cloud to the edge. This robust operating system is a stable foundation for countless innovations, providing a backbone for businesses worldwide. RHEL is the world's leading enterprise Linux platform certified on hundreds of clouds and collaborates with thousands of hardware and software vendors. Beyond being an operating system, it connects users to Red Hat's extensive ecosystem, offering 24/7 support and a ten year life cycle. With the latest release, users gain access to all supported versions, ensuring seamless upgrades and adoption of new features on their schedule.

Red Hat's commitment to simplicity and clarity is evident in the streamlined life cycle phases introduced in the latest RHEL versions. Previously, RHEL followed a four-phase life cycle: Development, Production 1, Production 2, and Extended Life. However, since version 8, this has been refined into three distinct phases: Full Support, Maintenance Support, and Extended Life. The current life cycle as effective for RHEL is shown in [Figure 2.1](#ch02.xhtml_fig2-1):

![](images/Figure_2.1.png)

Figure 2.1: RHEL life cycle

The three phases in the life cycle of the RHEL platform are as follows:

*   Full Support Phase: In this initial phase, Red Hat provides comprehensive support for the RHEL version. This includes regular updates, patches, and security fixes to ensure a robust and reliable operating environment. The Full Support Phase for RHEL version 8 spans a duration of five years, offering customers a stable foundation for their enterprise systems.
*   Maintenance Support Phase: Following the Full Support Phase, RHEL version 8 seamlessly transitions into the Maintenance Support Phase. During this period, customers continue to receive critical security updates and selected urgent fixes. The Maintenance Support Phase extends for an additional five years, totaling a decade of support for version 8.
*   Extended Life Phase: Recognizing the diverse needs of organizations, Red Hat introduced the Extended Life Phase, allowing customers to opt for Extended Life Cycle Support (ELS) through annual add-on subscriptions. With ELS, users can extend limited subscription services beyond the Maintenance Support Phase, providing tailored support to meet specific business requirements.

The main benefits of RHEL are as follows:

*   RHEL supports several CPU architectures: x86, ARM, IBM Power, IBM Z, and IBM LinuxONE.
*   RHEL includes Ansible automation technology that ensures a stable administrative experience, enabling innovation rather than repetitive tasks.
*   Red Hat Insights is a managed service for analytics and remediation that also enables organizations to receive continuous vulnerability alerts and targeted guidance, maximizing uptime and avoiding emergencies. From initial installation to deploying across multiple clouds, Red Hat provides utilities to simplify the process.
*   Migration tools ease the transition from other distributions, while tools like RHEL image builder create optimized operating system images for efficient cloud deployments. RHEL has built-in security and compliance features, including live kernel patching, security profiles, and a trusted software supply chain, simplify risk mitigation, automate security processes, and ensure compliance with high-security standards.
*   Comprehensive performance monitoring and analysis tools help optimize systems, detect anomalies, and apply best practices through preset tuning profiles, ensuring consistent performance across diverse hardware and workloads.
*   The Convert2RHEL tool streamlines the migration process from Red Hat Package Manager (RPM) compatible Linux distributions such as CentOS, Oracle Linux, Rocky Linux, AlmaLinux OS, etc., minimizing redeployment efforts and maintaining existing customizations, configurations, and preferences.
*   RHEL caters to various use cases, including edge computing, hybrid cloud deployments, SAP workloads, SQL Server hosting, application development, and high-performance computing (HPC). Its adaptability extends to the edge, scaling across numerous nodes globally, providing optimized OS images, and facilitating efficient system updates. As a key player in hybrid cloud environments, RHEL enables the deployment and running of applications seamlessly across physical, virtual, private, and public clouds.
*   Collaborations with major cloud providers like Google Cloud, AWS, Microsoft Azure, and Oracle Cloud Infrastructure ensure robust support for future-focused deployments. Organizations such as Salesforce, UPS, Lufthansa Technik, and Tomago Aluminium have harnessed the power of RHEL to streamline IT operations, enhance customer experiences, and improve development efficiency.

In enterprise IT, RHEL stands not just as an operating system but as a technological cornerstone, connecting diverse elements of modern IT stacks. Its open hybrid cloud strategy, built on Linux, containers, and automation, provides the flexibility needed to run applications wherever required. Whether we are developers, system administrators, or part of a large enterprise, RHEL is a proven, reliable, and flexible solution, laying the groundwork for innovation and success in the ever-evolving IT landscape.

[Installation methods](#contents.xhtml_sc2_27a)

The latest RHEL offers multiple installation methods to cater to diverse user requirements. Refer to the official Red Hat Customer Portal website, specifying the RHEL as a product, as shown in [Figure 2.2](#ch02.xhtml_fig2-2):

![](images/Figure_2.2.png)

Figure 2.2: Download Red Hat Enterprise Linux

The following section provides an overview of the available methods, guiding users to choose the most suitable approach for their needs:

*   ISO installation method: Users can install RHEL by downloading the DVD ISO image from the Red Hat Customer Portal. This method supports GUI and Kickstart, with registration completed post-installation. The boot menu (GRUB) offers the options to install RHEL, test the media, and install or troubleshoot an installed system, as shown in [Figure 2.3](#ch02.xhtml_fig2-3):

![](images/Figure_2.3.png)

Figure 2.3: Boot menu

*   Content delivery network (CDN) method: Register and install RHEL from the CDN method, which involves system registration, subscription attachment, and installation from the CDN. Users can opt for either boot ISO or DVD ISO image files. Boot ISO is recommended, with CDN as the default installation source.
*   Remote RHEL installation using Virtual Network Computing (VNC): The RHEL installation program offers two VNC modes, direct and connect, catering to different environments.
*   Install RHEL from the network using PXE: This network installation method requires access to an installation server running the PXE process, all the installation resources, and a minimum of two systems.
*   System or cloud image based installations: System or cloud image based installations are exclusive to virtual and cloud environments. Red Hat image builder facilitates the creation of customized RHEL system images tailored for cloud deployment, leveraging the Dandified YUM (DNF) package manager and updated RPM Package Manager (RPM) packages. RPM-DNF offers a simple and adaptive method for overseeing and modifying the system throughout its lifecycle.
*   Advanced installations: Perform an automated RHEL installation using Kickstart. Kickstart streamlines the OS installation by automating user-specified configurations, ideal for large-scale deployments. Large enterprises manage their fleet through Red Hat Satellite.

RHEL supports various architectures, including Advanced Micro Devices, Inc. (AMD) and Intel 64-bit, 64-bit ARM, IBM Power Systems (little-endian), and 64-bit IBM Z. The stability and security of RHEL extend across hybrid cloud deployments, supporting guest installations on hypervisors and cloud providers. Detailed information on supported architectures, including installation instructions for IBM Power servers, can be found on the official Red Hat catalog and documentation. RHEL installation requirements cover a wide variety of system, hardware, security, memory, and storage options. Specific hardware requirements for virtualization hosts are also supported.

[Anaconda](#contents.xhtml_sc3_28a)

The RHEL installer is called Anaconda, as well as other Linux distributions like CentOS and Fedora. In operating systems, Anaconda serves as the software responsible for guiding users through the installation process of the Linux distribution on their computers. Anaconda stands out because of its unique, parallel installation approach. Unlike many other operating system installers that follow a strict and linear sequence of steps, Anaconda offers users greater flexibility. Following is the installation process for a single node:

1.  The user selects their language and locale preferences (English language and United States is the default choice) as shown in [Figure 2.4](#ch02.xhtml_fig2-4): Anaconda Hat Enterprise Linux installer graphical user interface (GUI).

    ![](images/Figure_2.4.png)

    Figure 2.4: Installation localization

2.  The installation summary screen enables the user to configure four areas, as shown in [Figure 2.5](#ch02.xhtml_fig2-5):
    *   Localization (keyboard, language, timezone)
    *   System (storage, network, and security profile)
    *   User settings (root and users)
    *   Software (registration, installation source, and software selection)

The installation summary displays the overall options before beginning the installation process. The most common options are already pre-selected. The users must provide the choice for the installation destination, root user password, and user account creation as highlighted by red text.

![](images/Figure_2.5.png)

Figure 2.5: Installation summary

One key area is the software section that enables the user to select the installation style for the base environment and additional software for each:

*   Server with GUI: Server installation with GNOME user interface.
*   Server: Terminal-only server installation with the base services already installed.
*   Minimal Install: Terminal-only server with minimal installation.
*   Custom Operating System: Fully customizable installation with software selection.

Some architectures (64-bit ARM) have the option for the kernel page size to either 4 kilobytes (4k) or 64 kilobytes (64k). These options determine the size of the virtual memory pages used by the operating system's kernel for various operations, impacting memory management and system performance. The choice between 4k and 64k page sizes involves trade-offs in terms of efficiency, memory utilization, and overall system behavior, and the selection is often influenced by the specific requirements and characteristics of the workload or application being run on the system. The kernel-64k option is recommended only for large workloads with contiguous memory working sets [large database, HPC, etc.].

The server software options are displayed in [Figure 2.6](#ch02.xhtml_fig2-6):

![](images/Figure_2.6.png)

Figure 2.6: Installation software selection

However, it is important to note that not all parts of the installation process follow this parallel pattern. For instance, when installing from a network location, users must configure the network before selecting specific packages to install. Additionally, Anaconda automatically configures certain screens based on the hardware and installation media, providing a degree of automation to the process. Anaconda's approach is designed to simplify the installation process and make it more user centric. Despite its parallel nature, there are still specific screens that require sequential attention, marked by an exclamation mark. Users must address these settings before initiating the actual installation process that proceeds with installing the desired software in the system without any user intervention.

Once the installation is successful, we are able to reboot the system using the freshly installed operating system.

[Subscription manager](#contents.xhtml_sc3_29a)

To register a system without utilizing a graphical environment, the subscription-manager command can be employed from the command line. This command facilitates the registration process and automatically attaches the system to the most suitable and compatible subscriptions. Following steps include registering the system to a Red Hat account:

# subscription-manager register --username=RHusername --password=RHpassword

We need to specify the Red Hat Customer Console username and password, viewing available subscriptions using:

# subscription-manager list --available | less

We can auto attach a subscription with:

# subscription-manager attach –auto

Alternatively, users can manually attach a subscription from a specific pool by specifying the pool ID. To check consumed subscriptions, use the command:

# subscription-manager list –consumed

To unregister the system, use the command:

# subscription-manager unregister

These command line actions streamline Red Hat systems' registration and subscription management process.

[IT Operations](#contents.xhtml_sc2_30a)

In computer operations, few actions are as fundamental as turning a system on and off. The significance of these processes extends beyond routine actions; they play a crucial role in troubleshooting and completing installations. This section explores the intricacies of booting, shutting down, and suspending a Linux system from the command line.

[Login](#contents.xhtml_sc3_31a)

After a successful boot, our users can connect to the target system, and if the authentication is successful, they can carry on with the workflow. This process is often called Account, Authentication and Authorization (AAA). It might involve simple local system authentication or multiple system and database connection. RHEL supports CLI, GUI, and web console (Cockpit). We interact with the physical console when we type characters via a hardware keyboard connected to the system and see the output on a connected screen. The physical console supports multiple virtual consoles that can run separate terminals. Each virtual console supports an independent login session. We can switch between them by pressing Ctrl+Alt and the relative function key (from F1 to F6). Since RHEL 8, when the GUI is enabled, it replaces the command line login on the second virtual console (tty2) or the first available one onward.

| Note: Many system administrators disable the GUI to save resources to the server services. |

Headless servers are usually located in a data center in racks that do not have a physical keyboard permanently connected. Operators interact with the systems via serial console, Keyboard, Video, and Mouse (KVM), or network login. In a modern computing environment, many headless servers are virtual machines or containers running on-premise or as public or private cloud instances.

[Command line interface](#contents.xhtml_sc3_32a)

The command line is text-based, like a chatbot-style interface that can be used to input instructions to a computer system. The Linux command line is provided by a program called the shell. There are various shell programs for the shell program, and different users can be configured to use different shells. The default interactive shell for users in RHEL is the Bash (GNU Bourne Again SHell). Bash is an improved version of one of the most successful shells used on UNIX-like systems, the Bourne shell (sh). Also, users connected via a GUI or web console can use the bash via the terminal application or something similar.

When the shell is used interactively, it displays a string with the hostname and a blinking line called prompt that indicates that the system is waiting for the user commands. When a normal user accesses the system, the default prompt ends with a $ symbol (dollar character) like the following two examples:

[devops@demo.example.com ~] $

devops@demo.example.com:~$

Whereas when the superuser, root, is connected, the prompt ends with a # symbol (hash character) like the following:

root@demo.example.com:~#

The prefix string indicates the current user root, the hostname demo.example.com and the current directory in the file system (~ indicates the user's home directory). We can customize the string using the PS1 environmental variable. From now on, we will omit the prefix string.

| Note: Microsoft Windows uses the cmd.exe or PowerShell as command line interpreters. Apple Mac uses bash as a default shell in macOS. |

Users interact with the shell with commands. Each command is composed of three parts, as follows:

*   Command to run (example echo)
*   Options to select the command behavior (for example --help or -h)
*   Arguments that often indicate the command target (hello world)

The following command prints on the screen, also called standard output, the input argument Hello world.

$ echo "Hello world"

Hello world

Any error is printed on the screen as well, but we reference it as a standard error.

When a command is not available, misspelled, or the program is not available in the current system, the following message appears on the screen:

$ ansible

bash: ansible: command not found…

Standard users normally cannot install additional programs in the system as this might be dangerous for the system and other users.

[Logout](#contents.xhtml_sc3_33a)

We can disconnect from the system in the terminal by entering the exit command (without any arguments) to terminate the current shell or finish the session by pressing Ctrl+D.

[Shutting down](#contents.xhtml_sc3_34a)

With the adoption of systemd in RHEL, the traditional shutdown command has evolved. The Linux shutdown command now maps to systemd functions, introducing options like --halt and --poweroff.

| Note: Please note that the --halt option only stops the operating system while the --poweroff option turns off the system, typically using the ACPI hardware command. |

The shutdown command also has the ability to schedule timed shutdowns, allowing users to define a shutdown delay. The shutdown command requires special permissions granted via the sudo command. The given examples illustrate how to utilize this feature effectively.

To shut down the system immediately use the now option, as follows:

$ sudo shutdown -r now

To initiate a system halt at a specific time, use the command, as follows:

$ sudo shutdown --halt 23:00

If we prefer to halt the operating system a few minutes from the current time, specify the delay in two minutes, as follows:

$ sudo shutdown --halt +2

We can include a message for all users before the shutdown with the time mention, as follows:

$ sudo shutdown --halt +2 “URGENT. Shut down in TWO minutes.”

To cancel a scheduled shutdown, use the -c option, as follows:

$ sudo shutdown -c

[Reboot](#contents.xhtml_sc3_35a)

While restarting a system can resolve various issues, please limit any unnecessary reboots, especially on servers, as downtime should be minimized. In many situations, restarting a service is an alternative to rebooting the entire system. The systemctl command requires special permissions granted via the sudo command. The following command restarts single services:

$ sudo systemctl restart {service-name}

In certain situations, a system restart becomes unavoidable. To promptly restart the system using the shutdown command, employ the -r option as follows:

$ sudo shutdown -r now

If a delayed restart is preferred, adhere to the hh:mm format. Alternatively, we can utilize the systemctl command to reboot the device:

$ sudo systemctl reboot

It is important to note that a limitation of systemctl is its inability to facilitate delayed restarts.

[Suspending and hibernating](#contents.xhtml_sc3_36a)

Power management is a crucial aspect of system control. The systemctl commands for these operations offer user flexibility in managing power consumption based on their needs. [Table 2.1](#ch02.xhtml_tab2-1) summarizes the main differences between suspension and hibernation:

| Suspension | Hibernation |
| The system shuts down (no-power mode). | The system remains powered on in a low-power state. |
| Contents of memory are moved to the swap location. Upon power up, the system reloads itself from swap. | Applications are stopped. |
| The boot loader is configured to boot directly to the current kernel. | The system state is moved to RAM. |

Table 2.1: Suspension and hibernation comparison

We can suspend or hibernate our system using the commands:

$ sudo systemctl suspend

$ sudo systemctl hibernate

The hybrid-sleep command combines both suspend and hibernate.

$ sudo systemctl hybrid-sleep

The evolving landscape of system control in Linux, where traditional commands now align with systemd functions. Whether scheduling shutdowns, restarting services, or managing power effectively, users are equipped with a comprehensive set of tools. The most modern approach to system control advocates for scheduled operations to minimize disruptions while acknowledging that, at times, bringing down a system is sometimes unavoidable. As Linux administrators, mastering these commands ensures confident and efficient system management.

[Graphical user interface](#contents.xhtml_sc3_37a)

RHEL is well known for balancing convenience and control alternatives. The GUI in RHEL comes from recognizing the diversity of user preferences. It is possible to initialize reboots or shutdowns through GUI interfaces. There are many GUI interface options, but the RHEL default is the GNOME environment. While command line operations offer unparalleled control, GUI options provide a convenient alternative for those less comfortable with terminal commands.

[Figure 2.7](#ch02.xhtml_fig2-7) shows how to initialize a reboot or shutdown from the GNOME user interface (left top corner). Other GUI offers similar options.

![](images/Figure_2.7.png)

Figure 2.7: Reboot via GUI interface

We can interact with the console commands using the Terminal in the GUI, as shown in [Figure 2.8](#ch02.xhtml_fig2-8):

![](images/Figure_2.8.png)

Figure 2.8: Terminal in GUI

[Bash scripts](#contents.xhtml_sc3_38a)

Bash scripts offer a streamlined method for harnessing the power of the shell by enabling users to execute a sequence of commands in a systematic manner. Instead of manually entering individual commands, users can create scripts to automate tasks, improving efficiency and reducing the risk of errors. This scripting approach is particularly valuable for repetitive or complex tasks, as it allows for the organization and execution of multiple commands in a cohesive sequence. Bash scripts enhance the overall user experience in the command line environment, making it easier to manage and perform various tasks with precision and consistency.

This is a simple but effective Hello World Bash script:

#!/bin/bash

# Usage: Hello World Bash Shell Script

# Author: Luca Berton

# -------------------------------------------------

echo "Hello World"

Let us break down the different components:

*   #!/bin/bash: This line is called a shebang, and it tells the system to use the Bash interpreter to execute the script.
*   #: All these lines are comments that provide a brief description or purpose of the script, the author of the script, and a separator.
*   echo "Hello World": This line is the core of the script. It uses the echo command to print Hello World text to the terminal.

To run this script, we need to make it executable by running the following command:

$ chmod +x hello_world.sh

After making it executable, we can run the script using:

./hello_world.sh

When executed, it will print Hello World to the terminal.

[Getting help post-installation](#contents.xhtml_sc2_39a)

Searching for help through the vast amount of information is an invaluable tool for sysadmins, but knowing how to find answers without internet access, such as in air-gapped environments or during exams, is crucial. The man command for sysadmins provides insights into its importance in problem solving, followed by a mention of man page sections for reference and a promise to discuss the top five options in the upcoming article.

Following are the top five options for the man command:

*   List all available man pages with short descriptions using man -k
*   Obtain a short description for a specific man page with man -f <keyword>
*   Search through all man pages using regular expressions and open matching ones with man --regex <keyword>
*   Narrow down search criteria to specific sections using man -S <section ID> <keyword>
*   Searching through all man pages for a keyword and output their locations using man -wK <keyword>

[Red Hat support tool](#contents.xhtml_sc3_40a)

The redhat-support-tool command, included in RHEL, is the Red Hat Support Tool utility that provides a text based interface for searching inside the knowledge base articles and filing support cases on the Customer Portal via the command line.

$ redhat-support-tool

Welcome to the Red Hat Support Tool.

Command (? for help):

The utility presents an interactive way as follows:

*   search  option: Search between Red Hat articles,
*   opencase  option: Open a support case,
*   addattachment  option: Attach diagnostic system information (sosreport).
*   listcases: List the supported cases of our Red Hat Customer account.

[Red Hat Developer](#contents.xhtml_sc3_41a)

The Red Hat Developer program provides subscription entitlements to Red Hat software for development purposes, documentation about technologies, Linux, and information about upcoming events and training. We need to renew our membership every year, as shown in [Figure 2.9](#ch02.xhtml_fig2-9):

![](images/Figure_2.9.png)

Figure 2.9: Red Hat Developer renew

[Red Hat Insights](#contents.xhtml_sc3_42a)

Red Hat Insights is a software as a service (SaaS) predictive analytics tool to help customers identify and remediate threats to security, performance, and stability on systems or infrastructures running Red Hat products. It is an opt-in choice and requires an agent running to acquire system information and send it to the Red Hat cloud systems. When a security threat is detected and a solution to remediate the problem, it provides step by step instructions or an Ansible Playbook to apply to our infrastructure. The architecture design looks like the following:

![](images/Figure_2.10.png)

Figure 2.10: Red Hat Insight diagram

The Insight agent is already installed in RHEL8+ operating systems. We can activate Insight using the following command as a superuser (root) from a system with a valid software entitlement:

# insights-client --register

Once the data flows from our system to the insight service, we are able to perform analyses. We can audit our systems for compliance using the OpenSCAP policy framework project, for example, by auditing our system for the Payment Card Industry Data Security Standard (PCI DSS) policy. We can also compare our system with a reference configuration and evaluate any drift and corrective actions.

[Users and groups](#contents.xhtml_sc2_43a)

Managing users and groups is a pivotal aspect of Linux systems, crucial for enforcing security and access control.

In a multi-user environment, the su and sudo commands might effectively switch between users in the terminal.

[Switch user](#contents.xhtml_sc3_44a)

Linux is a multi-user system that takes advantage of multiple users with specific permissions. We use the su command to switch between users in our terminal. Specifically, the following su command switches between the student and the admin command:

student@demo.example.com:~$ su - admin

Password: ********

admin@demo.example.com:~$

The command is expected from the user to input the password of the destination user in order to grant access. The su command specifies the optional - (dash symbol) parameter that means to switch to the destination user's home directory and settings. If we do not specify any destination user, the root superuser is used by the su command.

[Sudo](#contents.xhtml_sc3_45a)

Some systems configure the superuser (root) with an invalid password that disables the ability to connect directly with this user for better security. Using the sudo command, the user within a group can perform commands with superuser permission.

In the following example, the user devops is able to access the system log file usually permitted only to the superuser (root) typing their password:

devops@demo.example.com $ sudo tail /var/log/secure

[sudo] password for devops: ********

This process is called privilege escalation and is permitted only if the user is within some special system group. Usually, the wheel system group enables the user to perform any command permitted to the superuser (root).

When the user does not have permission, the following message appears on the screen:

devops is not in the sudoers file. This incident will be reported.

[Storage](#contents.xhtml_sc2_46a)

In Linux, all files are stored on file systems, organized in an inverted tree of directories, forming a file system hierarchy. This inverted tree structure has the root at the top, and the branches of directories and subdirectories extend downward from the root. Refer to [Figure 2.11](#ch02.xhtml_fig2-11) for significant RHEL file system directories:

![](images/Figure_2.11.png)

Figure 2.11: Significant file-system directories in RHEL

The / directory is the root directory of the tree at the top of the file system hierarchy. The / character also functions as a directory separator in file names. For instance, if etc is a subdirectory of the / directory, we would denote it as /etc. Similarly, if the /etc directory contains a file named issue, we would reference it as /etc/issue.

| Note: The /etc/issue text file displays a login message or banner to be printed before the login prompt. In comparison, the /etc/motd text file generally displays an issue, security policy, or message. |

Subdirectories stemming from / have standardized purposes for organizing files based on type and function. This systematic arrangement simplifies file retrieval.

The following are the key locations and purposes of a RHEL system:

*   /boot: Files required for system bootstrap.
*   /etc: Configuration files for the system.
*   /dev: Contains special device files used to access hardware.
*   /home: Home directories for regular users to store personal data and configuration files.
*   /root: Home directory for the administrative superuser, root.
*   /usr: Installed software, shared libraries, include files, and read-only program data. Key subdirectories include:
    *   /usr/bin: User commands.
    *   /usr/sbin: System administration commands.
    *   /usr/local: Locally customized software.
*   /var: Variable data specific to this system that persists between boots. It contains dynamically changing files such as databases, cache directories, log files, printer-spooled documents, and website content.
*   /run: Runtime data for processes started since the last boot. Includes process ID files and lock files. The contents are recreated on reboot. In previous RHEL versions, /var/run and /var/lock were used.
*   /tmp: World writable space for temporary files. Files not accessed, changed, or modified for ten days are automatically deleted. Another temporary directory, /var/tmp, automatically deletes files not accessed, changed, or modified in more than 30 days.

[Configure devices](#contents.xhtml_sc3_47a)

Partitioning a disk is a crucial aspect of system administration, allowing the division of a hard drive into logical storage units known as partitions. This practice enables system administrators to allocate different functions to distinct partitions. It facilitates the limitation of available space for applications or users, separation of operating system and program files from user files, creation of a dedicated area for memory swapping, and improvement of diagnostic tools and backup imaging performance through controlled disk space utilization. The Master Boot Record (MBR) partitioning scheme, used since 1982, governed disk partitioning on Basic Input/Output System (BIOS) firmware systems, supporting up to four primary partitions. However, due to the increasing size of physical disks and SAN-based volumes, the 2 TiB limit of MBR has become a real-world challenge. The GUID Partition Table (GPT) has emerged as the successor to MBR, offering enhanced capabilities, including support for up to 128 partitions, larger disk sizes, redundancy through primary and secondary GPTs, and error detection using checksums for improved data integrity. GPT is the standard for laying out partition tables on physical hard disks, particularly on Unified Extensible Firmware Interface (UEFI) firmware systems. The Parted software, a versatile partition editor, facilitates this process by offering commands for creating, deleting, and modifying partitions. When provided with the device name of the entire disk and appropriate subcommands, the parted command allows administrators to manage partitions interactively. The following command prints the partition table of the disk:

# parted /dev/nvme0n1

(parted) print

Model: VMware Virtual NVMe Disk (nvme)

Disk /dev/nvme0n1: 21.5GB

Sector size (logical/physical): 512B/512B

Partition Table: gpt

Disk Flags:

Number Start End Size File system Name Flags

1 1049kB 630MB 629MB fat32 EFI System Partition boot, esp

2 630MB 1704MB 1074MB xfs

3 1704MB 21.5GB 19.8GB lvm (parted)

For instance, the print subcommand displays the partition table, while the unit subcommand alters the default size units. Additionally, administrators can employ parted to write MBR or GPT labels to a new disk, selecting the appropriate scheme for their needs. The tool provides a flexible and interactive environment for creating partitions, specifying partition types, and indicating file system preferences. Whether through interactive mode or direct commands, Parted simplifies the complex process of disk partitioning, offering system administrators a robust tool for efficient disk management. Following creating a partition on a block device, we need to create a file system with it to use it. RHEL supports various file system types, with XFS and .ext4 being two commonly utilized options. By default, Anaconda employs XFS. To apply an XFS file system to a block device, the mkfs.xfs command is utilized as the root user. The provided example demonstrates this process using the command:

# mkfs.xfs /dev/sdb1

The output displays metadata details, including version, log configuration, and various settings such as block size, sector size, and file system attributes. It is worth noting that the mkfs.ext4 command can be used to create an .ext4 file system on the block device if that is the preferred file system type.

[Manual mount](#contents.xhtml_sc3_48a)

Manually mounting file systems is crucial when dealing with removable storage devices in a Linux system. The mount command, typically executed by the root user, allows manually mounting a file system. The first argument specifies the file system to be mounted, while the second argument designates the directory to serve as the mount point within the file-system hierarchy.

# mount /dev/sda1 /mnt/data

Two common methods are employed to identify the file system on a disk partition for the mount command: using the device file name in /dev that contains the file system or utilizing the Universally Unique Identifier (UUID) written to the file system. To mount a device manually, one must identify the specific device, ensure the existence of the mount point, and execute the mount command:

# lsblk

NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINTS

nvme0n1 259:0 0 20G 0 disk

├─nvme0n1p1 259:1 0 600M 0 part /boot/efi

├─nvme0n1p2 259:2 0 1G 0 part /boot

└─nvme0n1p3 259:3 0 18.4G 0 part

├─rhel-root 253:0 0 16.4G 0 lvm /

└─rhel-swap 253:1 0 2G 0 lvm [SWAP]

The lsblk command proves invaluable in listing details about block devices, aiding in identifying hot-pluggable storage devices, such as hard disk drives or USB storage devices. Storage drives are usually identified by the connection interface: /dev/sda for SCSI, /dev/hda for IDE, and /dev/nvme0 for NVMe are the most common for personal computers. Usually, an additional number specifies the partition in the device. By understanding the block device details, users can accurately mount the desired partition, enhancing the overall efficiency of file system management in Linux.

# mount UUID="994b1923-381f-4d39-88e3-180bda039752" /mnt/data

Unmounting file systems is a critical step usually performed in the shutdown and reboot procedures, as it ensures the safe disconnection of storage devices while preventing data corruption. We can disconnect an unused file system using the umount command. It requires the mount point as an argument:

# umount /mnt/data

However, unmounting becomes impossible if the file system is actively in use, requiring the cessation of all processes accessing data under the specified mount point for the umount command to succeed. The lsof command provides the list of resources active for each file system, aiding in resolving unmounting challenges.

| Note: We need to synchronize the data caching in memory to the file system to ensure data integrity on the disk before unplugging. |

[Persistent mount](#contents.xhtml_sc3_49a)

The /etc/fstab file (see Figure 2.13) is a critical configuration file in RHEL that ensures the automatic mounting of file systems during system boot, preventing users from losing access to their data after a reboot. Comprising six white space delimited fields per line, this file specifies device information, mount points, file system types (e.g.,.xfs or .ext4), mount options, dump backup settings, and the fsck order for file system verification. Using UUIDs for devices is crucial to avoid potential issues related to changing block device identifiers. We need to perform the following command after any modification to the /etc/fstab file to update systemd units:

# systemctl daemon-reload

Administrators must exercise caution, ensuring accurate entries in /etc/fstab to prevent potential non-bootable situations, with verification possible through the unmount and mount commands or using the findmnt --verify command to verify the syntax is correct.

[Configure and maintain systems](#contents.xhtml_sc2_50a)

Deploying, configuring, and maintaining systems form the backbone of a robust and efficient IT infrastructure. From the initial deployment of systems to the meticulous configuration of software and services, this exploration encompasses critical aspects of system management. Package management has a pivotal role, using the DNF tool to facilitate the seamless installation, upgrade, and removal of software packages.

[Additional software](#contents.xhtml_sc3_51a)

Installing additional software enables the users to perform more activities or enable our system to provide services to other hosts. The superuser, root, can install additional software in the system via the RHEL package manager. The RHEL package manager is the DNF program. The previous version of the package manager was called YUM. Software is distributed via packages using the RPM package format. This standard format contains the software binaries (the code executed by our computer) and some metadata describing the content of the package, and eventually, some dependencies from other packages that must or might be installed in our system. A typical example is the Firefox browser software that requires the GUI installed in the system to operate. The repository identifier for each supported architecture of RHEL.

Following are the supported architectures:

*   64-bit Intel and AMD - x86_64
*   64-bit ARM - aarch64
*   IBM Power (little endian) - ppc64le
*   IBM Z - s390x

Unlike the low-level RPM command, which lacks repository support and automated dependency resolution, DNF streamlines RPM based software installation and updates. This command enables users to perform various actions, including installing, updating, removing, and obtaining information about software packages and their dependencies. By working seamlessly with multiple Red Hat and third-party software repositories, DNF enhances the overall package management experience. To find software packages, users can leverage commands such as dnf list to display installed and available packages or dnf search to list packages matching specific keywords. Installing and removing software is simplified using DNF. For example, consider the following command:

# dnf install apache2

It installs the specified package and handles its dependencies. We can also install software groups using DNF, where groups represent collections of related software installed for specific purposes.

[Update](#contents.xhtml_sc3_52a)

DNF ensures a smooth and efficient process for software management and an easy way to maintain our system up-to-date. The dnf update command is a fundamental tool in RHEL for maintaining the currency and security of installed software packages. When updating packages, dnf usually tries to preserve existing configuration files. However, if the update detects potential conflicts, it may rename the old configuration file. For example, the old configuration could be renamed to .rpmsave, and the new configuration file will be installed. We can manually review and merge changes.

[Updating all packages](#contents.xhtml_sc4_53a)

To ensure that our entire system stays up to date, we can use the dnf update command without specifying any package. This will look for updates for all installed packages and apply them accordingly:

# dnf update

This command is essential for maintaining system security by applying all available updates for installed software, including kernel updates. It is also advisable to reboot the system after a kernel update to apply the changes.

[Updating a specific package](#contents.xhtml_sc4_54a)

When we want to update a specific package using dnf, we can specify the package name directly. This will ensure only that package, and its dependencies are updated, leaving the rest of the system untouched.

# dnf update httpd

This command will check if there is an update available for the httpd package and install the latest version.

[Kernel management](#contents.xhtml_sc4_55a)

Notably, the dnf update command is crucial in managing system and kernel updates, allowing administrators to maintain multiple kernel versions concurrently for testing purposes. In RHEL, we can keep multiple kernel versions for testing purposes. After a kernel update, RHEL does not automatically remove the previous kernel version, allowing us to boot into older versions if needed.

To check installed kernels, use:

# rpm -q kernel

This will list all installed kernel versions. To remove an older kernel version:

# dnf remove kernel-<version>

Replace <version> with the specific kernel version we want to remove.

[Removing a package](#contents.xhtml_sc4_56a)

Additionally, we use the dnf remove command for uninstalling software packages. We need to be cautious to prevent unexpected removals. This command uninstalls the httpd package along with its dependencies that are no longer required:

# dnf remove httpd

Always review the list of packages to be removed before confirming.

[Log](#contents.xhtml_sc3_57a)

RHEL saves a DNF package transaction history in the /var/log/dnf.rpm.log file, which records all installed and removed transactions, allowing users to track changes made to the system. Utilize the following command to access the DNF transaction history:

# dnf history

This command provides a concise summary of these transactions, displaying relevant information such as the command line used, the date and time of the action, and the packages or groups affected. For instance, the output may reveal the installation of software packages, kernel updates, or removal of specific components. Furthermore, administrators can undo a particular transaction using dnf history undo, effectively reverting the system to its state before the selected action. This feature ensures flexibility and control in managing system changes, allowing for the correction of unintended modifications.

[Remote access](#contents.xhtml_sc2_58a)

Configuring RHEL can be efficiently accomplished through both the web console (Cockpit) and Secure Shell (SSH), offering users flexibility and convenience. To configure using the web console, open a web browser and navigate to the server's IP address or hostname followed by the default port TCP 9090\. Log in with valid credentials, and gain access to Cockpit's intuitive interface, allowing us to manage system services, monitor performance, and perform various administrative tasks. Additionally, SSH provides a CLI for remote configuration. Open a terminal and connect to the server using the ssh command, specifying the username and server address. Once logged in, we can execute commands, edit configuration files, and manage the system as if physically present. Whether through the user friendly web console or the powerful SSH command line, RHEL provides administrators with versatile options for seamless and efficient configuration.

[Web console](#contents.xhtml_sc3_59a)

RHEL introduced the Web User Interface (WUI) via the Cockpit web service. An administrator can connect and manage a system accessing the web interface at the specified address. The interface makes it easy to perform basic and advanced operations such as rebooting or shutting down the system, configuring local users, and installing or removing software. The cockpit service must be configured to run on the system in order to connect. We can verify the status of the service using the following command:

$ systemctl status cockpit.socket

The output shows the Active: active (listening) when the service is running and accepting connections.

We can execute the cockpit service using the following command:

# systemctl start cockpit

Please note that we might need to enable the external connections using SELinux and firewalld:

$ sudo semanage port -a -t websm_port_t -p tcp 9090

$ sudo firewall-cmd --permanent --service cockpit --add-port=9090/tcp

This command starts the cockpit service on the system, enabling administrators to connect and manage the server through the web interface. Suppose the service is active and accepting connections. In that case, administrators can access the web interface by entering the specified address in a web browser via the TCP port 9090, as shown in [Figure 2.12](#ch02.xhtml_fig2-12):

![](images/Figure_2.12.png)

Figure 2.12: Web console dashboard

[SSH network login](#contents.xhtml_sc3_60a)

Accessing a remote system is possible using the SSH via the ssh command. It replaced the insecure telnet protocol by providing a secure and encrypted alternative for remote access and communication between devices over a network. Many Linux distributions and macOS already include the OpenSSH utility out-of-the-box.

The following command connects to the remotehost.example.com system using the remoteuser username:

$ ssh remoteuser@remotehost.example.com

remoteuser@remotehost.example.com's password: ********

[remoteuser@remotehost.example.com ~]$

As we can see, the remote system requires to enter the password of the remoteuser username in order to grant access to the interactive shell. We can execute commands on the remote system like it is local. It is normal to expect some network delay in command execution. As an alternative to the hostname, we can specify the IP address. The communication in the connection is encrypted by the ssh command to secure against eavesdropping or hijacking of the passwords and content (man-in-the-middle attack). Modern cloud instances prefer to use only the public and matching private key authentication without entering a password. For example, Amazon Web Services (AWS) uses the key authentication for remote connections. This authentication method requires sharing and storing the public key associated with the user in the remote server. During the connection, the ssh command provides the private key, and if matching the public key, the access is granted.

The following command uses the mykey.pem private key to connect to the remotehost.example.com hostname using the remoteuser username:

$ ssh -i mykey.pem remoteuser@remotehost.example.com

[remoteuser@remoteuser@remotehost.example.com ~]$

| Note: The private key must be readable only by the current user (0600 permission). |

Ansible, the Red Hat automation, uses the ssh command to connect and execute commands to remote hosts.

Like in a local system, we can disconnect from the remote system by entering the exit command or finishing the session by entering Ctrl+D. The following output message informs about the termination of the SSH session:

Connection to remotehost.example.com closed.

When we need to execute only one command on the remote command, we can specify the command directly via the ssh command. In the following example, we are going to execute the hostname command:

$ ssh -i mykey.pem remoteuser@remotehost.example.com hostname

remotehost.example.com

[SSH key authentication](#contents.xhtml_sc3_61a)

Key authentication is the preferred way to connect to the remote system and is more secure than password authentications because they use multiple encryption algorithms (RSA, DSA, Blowfish, AES, ECDSA, ed25519, etc.) to store information and have an expiration date. The remote server also has a security fingerprint that is saved and checked every time we log in to verify that nobody pretends to impersonate the other host or hijack the connection. The remote host fingerprint is stored in the ~/.ssh/known_hosts file. If the local machine has a host key saved that does not match the one sent by the remote host, the connection is automatically closed with a warning message. We can generate the SSH key for SSH key based authentication using the ssh-keygen command. By default, it uses the RSA 2048bit encryption, and the public key is saved in ~/.ssh/id_rsa.pub and the private key in ~/.ssh/id_rsa and produces on the screen a fingerprint hash in SHA 256\. We can customize the encryption algorithm by specifying the -t option, the number of bits of the key with the -b option, and the filename with the -f option. We can protect the SSH key by specifying a passphrase that acts like a password to open the private key each time we use it or use the ssh-agent software.

| Note: For FIPS 186-2, DSA keys must be exactly 1024 bits. |

We need to share the public key with the system before being able to connect with the remote host. The ssh-copy-id command copies the public key of the SSH public key to the remote system. The following command copies our public key to the remote system connecting with the user username:

$ ssh-copy-id -i .ssh/id_rsa.pub user@remotehost.example.com

The program ssh-copy-id connects to the remote host and copies our specified public key in the file ~/.ssh/authorized_keys, enabling us to connect to the target system using our SSH key.

We can use the ssh-agent program to cache our SSH private key in memory at the beginning or during our session to achieve password less authentication. The GNOME graphical desktop environment can automatically start the ssh-agent automatically. We can always manually launch the ssh-agent in our terminal with the following command:

$ eval $(ssh-agent)

Agent pid 9949

The agent is showing the process identifier (PID) in our system (in this case, 9949). Once the ssh-agent program is running, it is going to cache in-memory our key authentication the next time we use our key with the ssh command and be able to reuse it for password less authentication.

[Network interfaces and settings](#contents.xhtml_sc2_62a)

Network interfaces and settings are fundamental components of a system's connectivity, enabling communication over a network. This article provides a comprehensive overview of managing network interfaces and settings on RHEL, drawing from various authoritative sources, including RHEL's documentation and learning materials.

A network interface can be any hardware or software setup allowing a computer to connect and communicate. Linux systems, including RHEL, identify each network interface using unique names, for example, eth0 for the first Ethernet interface, wlan0 for the first wireless interface, etc..

RHEL utilizes the ip command for network interface management, offering functionalities to display, enable, disable, and configure network interfaces as follows:

*   Displaying network interfaces: The command ip addr or ip link show displays all network interfaces on the system, including their current status (up/down), IP addresses, and other related information.
*   Enabling and disabling network interfaces: To activate a network interface, use ip link set <interface> up, and to deactivate it, use ip link set <interface> down. These commands enable or disable the specified interface without altering its configuration.
*   Configuring network settings:  Network settings on RHEL can be managed manually by editing configuration files or using command line tools like nmcli (network manager command line interface) or nmtui (network manager text user interface).
*   Manual configuration: Network configurations are stored in /etc/sysconfig/network-scripts/ifcfg-<interface> files. Editing these files allows for manually setting IP addresses, netmasks, gateways, and other network parameters. Changes require the network service or the interface to be restarted for them to take effect.
*   Using nmcli and nmtui:  nmcli is a powerful command line tool for managing network settings, allowing us to configure, manage, and troubleshoot network connections. nmtui, on the other hand, provides a text-based user interface for those who prefer not to use command-line tools directly.
*   Persistent network configuration: For changes to network settings to persist across reboots, they must be correctly saved in the system's configuration files or managed through network manager using nmcli or the graphical interface.
*   Network troubleshooting: Common network troubleshooting commands in RHEL include ping, traceroute, netstat, and ip route. These tools can help diagnose connectivity issues, route problems, and monitor active connections.
*   Advanced networking features: RHEL supports advanced networking features such as bonding, teaming, and bridging, which allow for increased reliability, load balancing, and the creation of virtual network interfaces. Configuring these features requires a deep understanding of both the network's requirements and RHEL's networking capabilities.

Effective management of network interfaces and settings is important for administering RHEL systems. By mastering the use of command-line tools and manual configuration files and understanding the principles behind network connectivity, administrators can ensure that their systems remain connected and operate efficiently within their network environment. For detailed examples and further reading, refer to the official Red Hat documentation, man pages (man ip, man nmcli, man nmtui), and other RHEL specific resources.

[Manage files](#contents.xhtml_sc2_63a)

Mastering file management from the command line is a fundamental skill that empowers users to organize and manipulate their digital environment efficiently. The CLI provides a powerful set of tools for creating, viewing, and editing text files. To create a new text file, the touch command can be employed, while the cat and less commands allow users to view the contents of a file directly within the terminal. For editing purposes, commands such as nano or vim can be utilized, providing users with versatile and efficient text editors. As users navigate through directories and perform various tasks, the command line proves to be an indispensable tool for file management, offering flexibility and control over digital assets. Vim, the default fallback editor in POSIX systems, stands out as a ubiquitous and readily accessible tool, making it indispensable for various scenarios, from fresh OS installations to minimal system repairs based on Bill Joy's vi from the 1970s. Competence in Vim is likened to proficiency in one's native language or basic mathematics in the realm of technology. The command used was:

# vim /etc/fstab

[Figure 2.13](#ch02.xhtml_fig2-13) shows how to edit the configuration file /etc/fstab using the Vim editor:

![](images/Figure_2.13.png)

Figure 2.13: Edit file with Vim

Its widespread presence on systems worldwide sets it apart, and its high level of customization allows users to tailor it to their coding preferences. Vim commands enable lightning speed coding, with examples like cursor movement (hjkl), word navigation (w), and powerful deletion and copying operations. The editor, when mastered, empowers programmers to manipulate text seamlessly, reflecting the idea that Vim is for those who aspire to elevate their coding skills, capable of effortlessly handling text at the speed of thought. To save and quit in Vim, first exit insert mode by pressing Escape. Then, enter : to initiate a command line at the bottom of the screen. To save the edited file, type w (:w) and, if needed, specify a new filename with :w filename. To quit Vim, press :q. Vim prompts a warning if changes are unsaved, suggesting the addition of ! to override. For a prompt free exit, use :q!. Alternatively, ZZ can be used to save and quit. Although these commands may seem intricate initially, they collectively form a potent toolkit.

[Conclusion](#contents.xhtml_sc2_64a)

The journey through the foundational aspects of RHEL administration prepares IT professionals and system administrators to navigate the complex landscape of modern computing environments. Through the comprehensive exploration of system operations, storage configurations, file system management, and advanced system deployment techniques, learners acquire a robust toolkit. This toolkit is essential for building and managing resilient systems that meet and exceed the dynamic demands of contemporary organizational infrastructures. The ability to adapt and respond to new challenges is paramount in the rapidly evolving digital ecosystem. The insights gained from mastering RHEL enable professionals to architect secure, scalable, and highly available systems. As administrators become adept at configuring remote access, managing user and group permissions, and utilizing the command line for efficient system manipulation, they position themselves at the forefront of technological advancement. It invites professionals to delve deeper into Linux, network configuration, and security management, further expanding their capabilities.

The next chapter builds upon the foundational knowledge acquired, introducing more complex scenarios and advanced techniques. In this way, we are able take advantage of the operating system that power our world.

[Points to remember](#contents.xhtml_sc2_65a)

*   Anaconda is the installer for RHEL and stands out with its unique parallel installation approach, providing users flexibility in configuring installation options and allowing for automatic configuration based on hardware and installation media.
*   The Linux command line, facilitated by the shell (commonly Bash in RHEL), offers a text-based interface where users can input instructions. Prompt show a dollar sign $ for normal user and a dash # for super user root.
*   The systemd software control the startup, shutdown, and service management in RHEL. The traditional shutdown and reboot commands have transformed to align with systemd functions.
*   The su command facilitates user switching in the terminal, while the sudo command enables privilege escalation.
*   In RHEL, files are stored in a hierarchical file system structure with the root directory (/) at the top, serving as the root of an inverted tree, and subdirectories like /etc, /usr, and /var organized for specific purposes, such as configuration files, installed software, and variable data, providing a systematic arrangement for efficient file retrieval and management.
*   The DNF package manager facilitates the installation of additional software in RHEL, which supports the RPM package format for the installation, updating, and removal of software packages.
*   Remote access allows administrators versatile options for remote management and configuration through the user-friendly web console (Cockpit) or through the command line interface provided by OpenSSH.

[Multiple choice questions](#contents.xhtml_sc2_66a)

1.  What is called the Red Hat Enterprise Installer?
    1.  Dracut
    2.  Anaconda
    3.  Grub
    4.  Kickstart
2.  What is the name of the service used to reboot in Red Hat Enterprise Linux?
    1.  init
    2.  kernel
    3.  upstart
    4.  systemd
3.  What command is used to create a partition on a disk?
    1.  mound
    2.  parted
    3.  lsof
    4.  lsblk
4.  What command generate an SSH key?
    1.  ssh-copy-id
    2.  ssh-agent
    3.  ssh-keygen
    4.  ssh

[Answers](#contents.xhtml_sc3_67a)

1\. b

2\. d

3\. b

4\. c

[Questions](#contents.xhtml_sc2_68a)

1.  What are the installation methods for RHEL?
2.  What is the difference between CLI, GUI and WUI?
3.  How can we mount additional file system to a RHEL system?

[Key terms](#contents.xhtml_sc2_69a)

*   Content delivery network:  For RHEL, a CDN facilitates the efficient distribution of software updates and packages by using strategically located servers, optimizing download speeds, and enhancing the overall performance of software deployment.
*   Web User Interface: It is a graphical and interactive platform accessed through a web browser, facilitating user friendly configuration, monitoring, and management of software applications or systems.
*   Kickstart: It is a system configuration automation tool used in Red Hat based Linux distributions, allowing administrators to automate the installation process by creating a script (Kickstart file) that specifies configuration settings, software packages, and post-installation tasks, streamlining the deployment of multiple systems with consistent configurations.
*   Virtual Network Computing: It is a graphical desktop-sharing system that allows us to remotely control and interact with a graphical desktop environment on another machine. In the context of installing RHEL, using VNC can be a convenient way to perform the installation process without physically being at the machine.
*   Anaconda: It is the installer used by RHEL, featuring a unique parallel installation approach that allows users to configure most aspects in any order after selecting language and locale, providing flexibility in the installation process.
*   Image builder: It is a powerful tool in RHEL that automates the creation of deployment ready, customized system images, including installation disks, virtual machines, and cloud-specific images, offering efficiency by eliminating manual configuration intricacies, taking advantage of RPM-DNF.
*   Systemd: It is a system and service manager for Linux that initializes and manages system processes, providing advanced features such as parallelized startup, on-demand service activation, and dependency tracking.
*   Headless server: it is a computer system or server that operates without a GUI, accessed and managed remotely through a command line interface or network protocols.
*   Red Hat Insights: It is a proactive IT management service that uses predictive analytics to identify and remediate potential issues in RHEL environments before they impact system performance or security.
*   Software as a service: SaaS is a cloud computing model where software applications are provided as a service over the internet, allowing users to access and use the software without needing installation or maintenance on their local devices.
*   Unified Extensible Firmware Interface: UEFI is a modern firmware standard that replaces the traditional BIOS, providing an advanced boot and system initialization process with support for larger storage capacities, faster boot times, and improved security features.
*   PID: Process identifier is a numerical identifier assigned to a specific process in a computer's operating system, facilitating the management and tracking of active processes.
*   Cockpit: it is a web-based system management tool that provides a user friendly interface for administrators to monitor, manage, and configure Red Hat Enterprise Linux servers.
*   Secure Shell: SSH is a cryptographic network protocol that allows secure and encrypted communication between two devices, typically used for remote command line login, file transfers, and tunneling.
*   ECDSA: Elliptic Curve Digital Signature Algorithm is a cryptographic algorithm that uses the mathematical properties of elliptic curves to provide a secure method for creating and verifying digital signatures.
*   Universally Unique Identifier: UUID is a 128-bit identifier that is globally unique and is commonly used in software development to uniquely identify information without requiring a centralized authority for generation.
*   Master Boot Record: MBR is a legacy partitioning scheme that resides at the beginning of a storage device and contains essential information for the system to locate and boot the operating system.
*   GUID partition table:  GPT is a modern disk partitioning scheme that uses GUIDs to define partitions on a storage device, supporting larger disk sizes and improved data integrity features compared to the MBR scheme.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 3Red Hat System Administration](#contents.xhtml_ch03a)

[Introduction](#contents.xhtml_sc2_70a)

In this chapter, we explore the key tasks and tools essential for Red Hat System Administration. We cover fundamental topics such as improving command line productivity, configuring network interfaces, managing local users and groups, and monitoring Linux processes. The chapter also cover how to control services with systemd, scheduling tasks with crontab and anacron, managing storage through Logical Volume Manager (LVM) and Redundant Array of Independent Disks (RAID), and installing and updating software using DNF. Each section equips administrators with practical knowledge, essential for efficiently maintaining, securing, and optimizing Red Hat Enterprise Linux systems. These concepts are foundation for the daily operations and the RHCE certification preparation.

[Structure](#contents.xhtml_sc2_71a)

The chapter covers the following topics:

*   Network settings
*   Date and time
*   Schedule future tasks
*   Manage local users and groups
*   File access control
*   Linux processes
*   Control services and daemons
*   Boot process
*   Log files
*   Managing software using DNF
*   Storage in Linux
*   SMB storage
*   NFS storage

[Objectives](#contents.xhtml_sc2_72a)

This chapter equips readers with a comprehensive understanding and practical skills in Red Hat System Administration, covering essential Linux concepts, installation methods, command-line productivity, user and group management, process monitoring, systemd utilization, log analysis, software installation, access control, storage management, network attached storage access, and boot process control to prepare them for success in the RHCE certification.

[Network settings](#contents.xhtml_sc2_73a)

Linux stores the network settings in many configuration files. In this section, we will learn the key files and commands to test and alter the network configuration. The network configuration addresses are IPv4, IPv6, or both (dual-stack).

[Hostname](#contents.xhtml_sc3_74a)

A hostname identifies each system. Changing the system hostname in Red Hat Enterprise Linux (RHEL) involves using the hostname command to display or temporarily modify the fully qualified hostname. The static hostname can be specified in the /etc/hostname file, and the hostnamectl command is employed to modify this file and view the system's hostname status. If the /etc/hostname file is absent, the hostname is set through a reverse DNS query once the interface is assigned an IP address. In RHEL 6 and earlier, the file /etc/sysconfig/network was used.

[Name resolution](#contents.xhtml_sc3_75a)

The stub resolver converts the hostname to IP addresses and reverses it in the system. The /etc/nsswitch.conf file determines the order of the lookup. By default, the /etc/hosts file that contains static host resolution is first checked.

We can use the following command to test static host resolution:

getent hosts demo.example.com

If the static resolution is unsuccessful, the system tries to contact the DNS defined in the /etc/resolv.conf file. A typical file generated by NetworkManager is as follows:

domain example.com

search example.com

nameserver 192.168.1.254

The best practice for dual-stack systems is to mix an IPv4 and an IPv6 DNS resolver to guarantee the system's high availability.

[Network interfaces](#contents.xhtml_sc3_76a)

In RHEL, guaranteeing the accuracy and performance of network configurations is essential. We will explore how to alter configuration files and leverage command-line utilities to validate and troubleshoot network setups on RHEL systems. In RHEL, the network settings are managed by the NetworkManager tool. We will use the nmcli command of the NetworkManager to configure our network interfaces.

We can interact via the nmcli interactive command or via the configuration files as follows:

# nmcli con mod ID ipv4.dns 192.168.1.254

# nmcli con down ID

# nmcli con up ID

The network configuration on RHEL is stored in the configuration file for the network interfaces located in the /etc/sysconfig directory. The first wired connection configuration is stored in the /etc/sysconfig/network-scripts/ifcfg-Wired_connection_1 file.

The configuration file is as follows:

ONBOOT=yes

IPADDR=192.168.1.1

PREFIX=24

GATEWAY=192.168.1.254

DNS1=8.8.8.8

We can perform changes to the file and activate the changes using the nmcli command, which is given as follows:

nmcli con reload

nmcli con up "Wired connection 1"

We can gather network interface information using the ip, ping, tracepath, and ss commands. These commands provide detailed insights into network configurations, performance metrics, connectivity status, and routing information.

Let us explore several key commands and their applications as follows:

*   Identifying network interfaces: The ip link command lists all the network interfaces available on our system:

    $ ip link show

    In the given example, the server has two network interfaces: lo (loopback), and ens3. We can use the MAC address listed after link/ether to determine the connected network for each interface. For instance, the network card with the MAC address 94:36:CC:00:00:0a corresponds to the network interface ens3.

*   Displaying IP addresses: Use the ip addr command to view device and address information for a specific interface, such as ens3:

    $ ip addr show ens3

    This command provides details about the interface, including its IPv4 and IPv6 addresses.

*   Displaying performance statistics: The ip -s link command can be used to show statistics about network performance, including received and transmitted packets, errors, and drops:

    $ ip -s link show ens3

    These statistics can help identify potential network issues.

*   Checking connectivity between hosts: The ping command is a fundamental tool for testing connectivity. For example, to ping the IP address 192.168.250.251:

    $ ping -c3 192.168.250.251

    The ping6 command is the IPv6 version and works similarly:

    $ ping6 2001:db8:0:1::1

    Ensure that when pinging link local addresses and multicast groups, we explicitly specify the network interface with a scope zone identifier.

*   Displaying the routing table: Use the ip route command to show the IPv4 routing table. The -6 option can be added to the IPv6 routing table:

    $ ip route

    $ ip -6 route

    This provides insights into how packets are routed based on their destination.

*   Tracing routes taken by traffic: Use traceroute or tracepath commands to trace the path that network traffic takes through routers:

    $ tracepath access.redhat.com

    These commands help identify the routers involved in reaching a remote host.

*   Troubleshooting ports and services: The ss command replaces the older netstat tool and displays socket statistics:

    $ ss -ta

    The ss command shows information about listening and established sockets, including the local and peer addresses and ports.

The commands and techniques discussed above provide a solid foundation for troubleshooting and ensuring optimal network performance. For more detailed information, refer to the official configuring and managing networking guide.

[Date and time](#contents.xhtml_sc2_77a)

Maintaining accurate time synchronization using NTP and configuring the correct time zone is essential for ensuring accurate timestamps for events recorded by the system journal and logs.

Following is a step by step guide on how to achieve this:

1.  Verify current time settings: Use timedatectl to review current time settings, time zone, and NTP synchronization status:

    # timedatectl

2.  List available time zones: To configure the system's time zone appropriately, it is essential to know the available options.

    # timedatectl list-timezones

3.  Set the correct time zone:  Use timedatectl set-timezone followed by the desired time zone. For example:

    # timedatectl set-timezone Europe/Paris

4.  Verify changes:  Verify the changes by running timedatectl again.
5.  Configuring NTP synchronization: To ensure accurate timekeeping, enabling NTP synchronization keeps the system clock synchronized with network time servers.

    # timedatectl set-ntp true

    In RHEL, this command adjusts the chronyd NTP service.

6.  Configure chrony (chronyd): By default, chronyd uses NTP pool project servers. Modify /etc/chrony.conf if you need to change NTP servers, especially for isolated networks.

    Add NTP servers or peers in /etc/chrony.conf. For example:

    server 0.pool.ntp.org iburst

    The iburst option is recommended for quicker initial synchronization.

7.  Restart chronyd service: After modifying the chrony.conf file, restart the chronyd service:

    # systemctl restart chronyd

8.  Verify NTP synchronization:  Use chronyc, a client for chronyd, to verify NTP synchronization:

    # chronyc sources -v

    Look for a * next to the server’s name, indicating it is the current synchronized source.

Some additional notes for your reference are as follows:

*   UTC time zone: If you need UTC, set the time zone to UTC using timedatectl set-timezone UTC.
*   Setting local time: To change the local time, use timedatectl set-time with the format YYYY-MM-DD hh:mm:ss.
*   Persistent configuration: Ensure changes to chrony.conf are consistent and maintained across reboots for persistent time configuration.
*   Chrony vs. NTPd: In RHEL, chronyd is preferred over the older NTPd for time synchronization.

[Schedule future tasks](#contents.xhtml_sc2_78a)

Scheduling future tasks is vital for system administrators to automate maintenance, ensure system reliability, and optimize resource use in RHEL. Using crond, tasks can be scheduled to run at fixed times, such as a daily backup at 2 AM with a rsync command. Anacron is suitable for systems not running continuously, ensuring tasks like a weekly system update are executed even after downtime. Systemd provides flexible scheduling with timers, such as hourly cleanup of temporary files using a service and timer unit. Each utility caters to different scheduling needs, ensuring robust and reliable task automation.

[Cron](#contents.xhtml_sc3_79a)

The best way to schedule tasks from system accounts rather than from user accounts is with the crontab  command. The system wide crontab file is located in /etc/crontab and /etc/cron.d (the preferred way). Users can also schedule tasks in their account with the crontab command. The crontab file has a positional syntax, as follows:

*   Minute of the day (0 - 59)
*   Hour of the day (0 - 23)
*   Day of the month (1 - 31)
*   Month (1 - 12) or jan, feb, mar, apr ...
*   Day of week (0 - 6) (Sunday=0 or 7) or sun, mon, tue ...
*   Username to execute the command
*   Command to be executed

In addition, the special directories /etc/cron.hourly, /etc/cron.daily, /etc/cron.weekly, and /etc/cron.monthly contain executable shell scripts to be executed hourly, daily, weekly, or monthly.

The cron service in Linux allows us to schedule tasks to run automatically at specified intervals. These scheduled tasks are called cron jobs.

The following steps are the most common use cases and the practical commands to schedule, edit, remove and access the log history of the cron jobs:

1.  Understanding cron syntax:  A cron job is specified using the following format:

    * * * * * <command>

    | | | | |

    | | | | +---- Day of the week (0 - 7) (Sunday is both 0 and 7)

    | | | +------ Month (1 - 12)

    | | +-------- Day of the month (1 - 31)

    | +---------- Hour (0 - 23)

    +------------ Minute (0 - 59)

2.  Creating and editing cron jobs:  To create or edit cron jobs, use the crontab command.
    *   Edit the current user's cron jobs:

        crontab -e

    *   View the current user's cron jobs:

        crontab -l

    *   Remove the current user's cron jobs:

        crontab -r

3.  Example cron jobs:
    *   Run a script every day at 2 AM:

        0 2 * * * /path/to/your_script.sh

    *   Run a backup script every Sunday at 3 AM:

        0 3 * * 0 /path/to/backup_script.sh

    *   Clear the temporary files every 6 hours:

        0 */6 * * * /usr/bin/clear_temp_files.sh

    *   Check disk usage every Monday at 5 PM and log the output:

        0 17 * * 1 df -h > /var/log/disk_usage.log

4.  Special strings for common intervals: Cron also support special strings that represent common scheduling intervals:

    *   @reboot: Run once at startup.
    *   @yearly: Run once a year (0 0 1 1 *).
    *   @monthly: Run once a month (0 0 1 * *).
    *   @weekly: Run once a week (0 0 * * 0).
    *   @daily: Run once a day (0 0 * * *).
    *   @hourly: Run once an hour (0 * * * *).

    Example:

    Run a script at every system reboot:

    @reboot /path/to/startup_script.sh

5.  Managing system-wide cron jobs: System-wide cron jobs are stored in /etc/crontab and in the /etc/cron.d/ directory. The /etc/crontab file has an additional field to specify the user who should run the command.

    Example entry in  /etc/crontab:

    * * * * * <user> <command>

6.  Logging cron jobs: By default, cron logs its activity to /var/log/cron. We can view these logs to check if our cron jobs are running as expected.

    Example:

    tail -f /var/log/cron

[Automating backup](#contents.xhtml_sc4_80a)

The following steps is an example of how to schedule a backup in a tarball archive of some important data directory with the appropriate date using cron to run every day at 1:00 AM:

1.  Create the backup script:

    vim /usr/local/bin/backup.sh

    Add the following lines to the script:

    #!/bin/bash

    tar -czf /backup/$(date +\%F).tar.gz /important/data

2.  Make the script executable:

    chmod +x /usr/local/bin/backup.sh

3.  Schedule the script to run daily at 1 AM:

    crontab -e

    Add the following line:

    0 1 * * * /usr/local/bin/backup.sh

4.  Verify the cron job:

    crontab -l

By setting up cron jobs, we can automate routine tasks such as backups, system maintenance, and monitoring, ensuring they run consistently without manual intervention.

[Anacron](#contents.xhtml_sc3_81a)

When we want to ensure that important tasks always run in our systems, we use anacron. This is crucial, especially for a system turned off or hibernating when the job should have been executed. The configuration file is stored in /etc/anacrontab. The regular crond service parses this file nowadays. Since RHEL 7, the anacron service was necessary. The START_HOURS_RANGE environment variable defines the allowed list of hours to execute the scheduled tasks.

The syntax of the anacrontab file is as follows:

*   Period in days. Examples are the macro @daily equivalent to the integer 1 and the @weekly equivalent to 7.
*   Delay in minutes before starting the job.
*   Job identifier in the log messages.
*   The command to be executed.

[Systemd timer](#contents.xhtml_sc3_82a)

The systemd timer unit enables timer-based activation of other systemd units. It activates another unit of a different type, usually a service that matches the timer unit name. The following configuration, located in the /usr/lib/systemd/system/sysstat-collect.timer file, collects system statistics every ten minutes for the sysstat service:

[Timer]

OnCalendar=*:00/10

[Install]

WantedBy=sysstat.service

The OnCalendar parameter sets the timer every 10 minutes. We can specify a more complex timer expression or use the OnUnitActiveSec parameter instead. The OnUnitActiveSec=10min option triggers the unit after the last time the timer unit is activated.

| Note: Customize the systemd timer unit by copying the configuration file from /usr/lib/systemd directory to /etc/systemd/system. This prevents overriding during the update process. |

[Manage local users and groups](#contents.xhtml_sc2_83a)

Managing local users and groups in RHEL is essential for maintaining security, access control, and resource sharing. This involves creating new users with home directories and setting passwords, for example with user johndoe, and adding them to groups like wheel for administrative privileges. It also includes creating new groups such as projectteam and adding users like johndoe and janedoe to facilitate collaboration. Additionally, modifying directory ownership and permissions ensure that only designated users and groups can access and manage resources, exemplified by changing ownership to johndoe:projectteam and setting appropriate permissions on the /project directory.

[User](#contents.xhtml_sc3_84a)

A user account in Linux serves the purpose of establishing security boundaries between individuals and programs that execute commands. Users are identified by their usernames and, internally, by a unique identification number known as the User ID (UID). The system enforces access control based on file ownership, with each process and file associated with a specific user.

There are three main types of user accounts, as follows:

*   Superuser: The root account, with UID 0, is reserved for system administration, providing unrestricted access to the entire system.
*   System users UID 1-999: These accounts are used by background processes or daemons, ensuring services run securely without superuser privileges. The range 1-200 is usually reserved for system processes by Red Hat and 201-999 for other software.
*   Regular users UID 1000+: Most users fall into this category, using their accounts for day-to-day tasks with limited system access.

To view information about the currently logged-in user or other users, the id command is employed. This is shown as follows:

$ id

uid=1000(devops) gid=1000(devops) groups=1000(devops),10(wheel) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

The /etc/passwd file stores user account details, such as username, UID, GID, user's full name, home directory, and the default shell. This example showcases the columns separated value for the devops user in our system in the /etc/passwd:

devops:x:1000:1000:devops:/home/devops:/bin/bash

*   Username: devops
*   Password placeholder: x (encrypted password stored in /etc/shadow)
*   UID: 1000
*   Primary group ID (GID): 1000
*   Real name: DevOps User Account
*   Home directory: /home/devops (initial working directory)
*   Default shell: /bin/bash

Creating, modifying, and deleting user accounts is a routine part of system administration. The /etc/passwd file holds user details, and commands like useradd, usermod, and userdel are used to manage users. Securing user accounts involves implementing password management policies. The /etc/shadow file stores encrypted passwords, and administrators can manually lock or unlock user accounts using the passwd command.

The most commonly used commands are as follows:

*   Create a new user:

    # useradd devops

*   Add a new user and create a home directory:

    # useradd -m devops

*   Creating a user with a specific home directory:

    # useradd -m -d /opt/devops devops

*   Creating a user with a specific user id: We can verify using the id command

    # useradd -u 1500 devops

*   Creating a user with a specific group id:

    # useradd -g users devops

*   Creating a user and assign multiple groups:

    # useradd -g users -G wheel,docker devops

*   Creating a user with a specific login shell:

    # useradd -s /usr/bin/zsh devops

    The special nologin (/sbin/nologin) shell is used for non-interactive logins.

*   Creating a user with a custom comment:

    # useradd -c "DevOps User Account" devops

*   Creating a user with an expiry date using the YYYY-MM-DD format:

    # useradd -e 2028-12-31 devops

*   Creating a system user:

    # useradd -r system_user

*   Changing the default useradd values:

    # useradd -D

    We can also lock and unlock the user using the usermod command with the -L or --lock option or -U or --unlock option. When the user is locked, the Authentication failure message is displayed on the screen.

*   Setting passwords from the command line:

    # passwd devops

*   Delete users keeping home directory:

    # userdel devops

*   Delete users deleting the home directory:

    # userdel -r devops

[Shell startup](#contents.xhtml_sc3_85a)

The special variables $HOME contain the current user home directory, and $PATH is the path used to search for executable commands.

$ echo $HOME

/home/devops

$ echo $PATH

/usr/local/bin:/usr/local/bin:/usr/bin

The system-wide Bash shell user variables are defined in the /etc/profile and / etc/bashrc files. Users can customize overriding via the .bash_profile and .bashrc files in the home directories.

These files are loaded when the user login or using the source command as follows:

$ source ~/.bash_profile

[Password](#contents.xhtml_sc3_86a)

The additional shadow password file, accessible only to the root user located in /etc/shadow, is a system file in Linux that stores encrypted user passwords. The line for the devops user is as follows:

devops:$6$j0BdSRjg7eEj14Z3$6fAkEz6K.1cj/jc78GL4NdqV0VdPVApUAxhtB6q8ZCCDjiywfYyQ5xWZRznHR2HONYdEXSqyci3jXemg9IXbK.::0:99999:7:::

Following is the format of the file, each delimited by the $ sign:

*   Hashing algorithm: The first segment indicates the hashing algorithm used for the password. Example: $6$ signifies using the SHA-512 hash (default in RHEL 8+). Other possibilities include $1$ for MD5 and $5$ for SHA-256.
*   Salt: The second segment represents the randomly chosen salt used in the encryption process.
*   Encrypted hash: The third segment comprises the encrypted hash of the user's password.

We can configure the password aging using the chage command and the options, as shown in [Figure 3.1](#ch03.xhtml_fig3-1):

![](images/Figure_3.1.png)

Figure 3.1: Password aging

Following are the most common use cases:

*   List the current password aging setting for the devops user:

    # chage -l devops

*   Set the password for the devops user:

    # sudo passwd devops

*   Enter new UNIX password:

    Retype new UNIX password:

    passwd: password updated successfully

*   Set the minimum days to 0, max 90 days, warning 7 days, and 14 inactivity days:

    # chage -m 0 -M 90 -W 7 -I 14 user03

*   Force the user to update the password on the next login

    # chage -d 0 devops

[Superuser](#contents.xhtml_sc3_87a)

Superuser access is often required for system administration tasks. It is granted through the use of the su or sudo command. These allow authorized users to execute commands with elevated privileges, enhancing security by reducing the need for continuous superuser sessions.

An end-user system typically enables the shutdown command to the users group:

%users localhost=/sbin/shutdown -h now

Another typical setup is to allow the mount of the CDROM drive to the users group:

%users ALL=/sbin/mount /mnt/cdrom, /sbin/umount /mnt/cdrom

The following line in the /etc/sudoers enables all the users in the wheel group to execute superuser commands specifying the user password:

%wheel ALL=(ALL) ALL

The following line is the same without a password request:

%wheel ALL=(ALL) NOPASSWD: ALL

[Group](#contents.xhtml_sc3_88a)

A group is a logical collection of users sharing access to files and system resources. Like users, groups have names, unique identification numbers, and GIDs. The system group has GID 0-999, whereas the custom groups have GID 1000+. Groups facilitate file access control by allowing permissions to be granted to multiple users simultaneously. The /etc/group file stores information about local groups, including group name, GID, and a list of group members.

users:x:100:

Every user has one primary group, listed in the /etc/passwd file, and may belong to supplementary groups defined in the /etc/group. Local groups, defined in the /etc/group file, can be created, modified, and deleted using commands such as groupadd, groupmod, and groupdel. Groups are pivotal in simplifying access control and resource sharing among users. Following are the most command use cases:

*   Display user groups:

    # groups devops

    devops : devops wheel users

*   Create a group:

    # groupadd group1

*   Delete a group:

    # groupdel group1

*   Add an existing user to a group:

    # usermod -a -G users devops

*   Change a user’s primary group:

    # usermod -g groupname username

*   Add an existing user to multiple groups in one command:

    # usermod -aG group1,group2 username

*   Remove a user from a group:

    # gpasswd -d username group1

Effectively managing local users and groups is fundamental to maintaining the security and functionality of a Linux system. Understanding the concepts of users and groups, gaining superuser access, and employing commands to create, modify, and delete user and group accounts are essential skills for any Linux administrator. Regular password management further enhances system security, ensuring a robust and well-organized user environment.

[Files access control](#contents.xhtml_sc2_89a)

The fundamental command for changing permissions is chmod, short for change mode. The chmod command supports two methods: symbolic and numeric.

[Symbolic method](#contents.xhtml_sc3_90a)

It utilizes letters to represent different groups of permissions: u for user, g for group, o for others, and a for all (user, group, and others). It combines permission actions and permissions. Permission actions are + to add permissions, - to remove permissions, = to set exactly those permissions. Permissions are represented by letters: r for read, w for write, x for execute. To modify file permissions on a RHEL system, we can use the chmod command to set the desired access rights.

Following are two examples of how to adjust permissions for specific files:

*   Remove read and write permission for group and others on file1:

    $ chmod go-rw file1

*   Add execute permission for everyone on file2:

    $ chmod a+x file2

[Numeric method](#contents.xhtml_sc3_91a)

The numeric method involves a 3-digit (or 4-digit for special permissions) octal number. Each digit represents permissions for an access level: user, group, and others. The digit is calculated by adding numbers 4 for read, 2 for write, and 1 for execute. To configure file and directory permissions effectively in RHEL, the chmod command is used to specify access rights. The following examples demonstrate how to set permissions for a file and a directory:

*   Set read and write permissions for the user, read permission for group and others on samplefile:

    $ chmod 644 samplefile

*   Set read, write, and execute permissions for the user, read and execute permissions for the group, and no permission for others on sampledir:

    $ chmod 750 sampledir

Change file and directory user or group ownership. File ownership is managed using the chown command. It can change both user and group ownership.

*   Grant ownership of test_file to the devops user:

    $ chown devops test_file

*   Change the group ownership of test_dir to admins group:

    $ chown :admins test_dir

*   Change ownership of test_dir to the visitor and the group to guests:

    $ chown visitor:guests test_dir

Controlling access to files involves understanding and utilizing the chmod and chown commands. The symbolic and numeric methods offer flexibility in managing permissions, while ownership can be modified for users and groups.

[Special permissions](#contents.xhtml_sc3_92a)

Special permissions, the fourth type alongside user, group, and others, offer extra access features beyond basic permissions.

[Table 3.1](#ch03.xhtml_tab3-1) explains the effects of these special permissions:

| Special | # | Symbolic | Effect on file | Effect on directory |
| suid | 4 | u+s | Execute by the file user owner | No effect |
| setgid | 2 | g+s | Execute by the file group owner | New files match the file group owner |
| sticky | 1 | o+t | No effect | Remove only owns files |

Table 3.1: Special permissions

We can identify the setuid permissions by a lowercase s where we would normally expect the x for owner execute permissions. If the owner does not have execute permissions, this is replaced by an uppercase S.

$ ls -l /usr/bin/passwd

-rwsr-xr-x. 1 root root 69296 Aug 10 2021 /usr/bin/passwd

We can identify the setgid permissions by a lowercase s where we would normally expect the x for group execute permissions to be. If the group does not have execute permissions, this is replaced by an uppercase S.

$ ls -l /usr/bin/locate

-rwx--s--x. 1 root slocate 69472 Aug 10 2021 /usr/bin/locate

We can identify the sticky permissions by a lowercase t where we would normally expect the x for other execute permissions.

$ ls -ld /tmp

drwxrwxrwt. 21 root root 4096 Dec 31 10:46 /tmp

[Default permissions](#contents.xhtml_sc3_93a)

We can use special and default permissions to set the group owner of files created in a particular directory. Two factors influence these initial permissions. First, the type of file created, whether a regular file or a directory, determines the default permissions. For directories, the system sets initial octal permissions as 0777 (drwxrwxrwx), while regular files get 0666 (-rw-rw-rw-) as their starting point. Second, the current umask, a bitmask restricting permissions, further refines the initial settings. The umask, set by the shell session, can clear specific permissions for newly created files and directories. For instance, a umask of 0002 clears the write bit for other users. Users can check and modify the umask using the umask command, adjusting the octal value to reflect the desired permissions. This system feature adds a layer of security, especially when combined with default file permissions. Users can customize their umask settings in personal profile files, and administrators can implement system-wide changes by adjusting the shell startup scripts.

Mastering file system permissions is crucial for Linux administrators to ensure proper access control. Understanding the chmod and chown commands, along with the symbolic and numeric methods, empowers users to efficiently manage file permissions and ownership efficiently, contributing to a secure and organized Linux environment.

[Access control lists](#contents.xhtml_sc3_94a)

In RHEL, access control lists (ACLs) provide a powerful mechanism for fine-grained control over file and directory access beyond traditional Unix permissions. ACLs enable administrators to define access permissions for specific users and groups, allowing for more nuanced security configurations. By using the setfacl and getfacl commands, administrators can grant or revoke permissions, such as read, write, and execute, on individual files and directories. This level of granularity is particularly useful in environments where different users or groups require distinct levels of access to shared resources. ACLs complement the standard file permissions in RHEL, offering an additional layer of control that enhances security and facilitates a more flexible and tailored access management system. Leverage ACLs empowers administrators to implement robust and customized file access policies in RHEL environments.

Linux filesystem permissions traditionally revolve around three categories: user owner, owner group, and others. Access levels, such as read, write, and execute, are granted based on these categories. For instance, a directory in the accounting department might have permissions set as drwxrwxr-x, allowing the user owner to read and write, the owner group to read and write, and others to see and execute.

$ getfacl /accounting

# file: accounting

# owner: accounting

# group: accounting

user::rwx

group::rwx

other::---

default:user::rwx

default:user:accounting:rwx

default:group::rwx

default:mask::rwx

default:other::---

The process of setting ACLs involves using the setfacl command with options like -m (modify) or -x (remove). For instance, to grant Alice access to the accounting directory, the following command is used:

$ setfacl -m alice:rwx /accounting

$ getfacl /accounting/example.txt

# file: example.txt

# owner: accounting

# group: accounting

user::rwx

user:alice:rwx

ACLs can be fine-tuned to enable or restrict specific actions, such as read-only access or preventing file creation within a directory. ACLs offer a flexible way to manage access within a group. ACLs allow administrators to control who can read, write, or execute within a directory without changing fundamental ownership structures. Additionally, ACLs enable the creation of isolated folders within a group, providing users like Alice with their workspace. ACLs can be further customized to control access even among specific users or groups within a shared directory. In this section, we explored scenarios involving restricting access to confidential files, granting exclusive access to specific users, and even providing access to individuals outside the owning group.

[Linux processes](#contents.xhtml_sc2_95a)

In Linux, effective process scheduling is essential for optimizing system performance. The Linux process scheduler is embedded in the kernel and employs time-slicing or multitasking to manage the execution of numerous processes on a single core, with each process assigned a relative priority, known as the nice value. On regular systems, the scheduling policy used for most processes is called SCHED_OTHER or SCHED_NORMAL, but other policies exist for various workload needs. The nice and renice commands are key in influencing the priority of processes. Users can utilize the nice command to start processes with specific nice levels, determining their priority. The renice command allows for the dynamic adjustment of the nice level of existing processes. While unprivileged users can increase the nice level to a maximum of 19, only the root user can decrease it up to -20\. These commands provide a means of fine-tuning process prioritization, contributing to a responsive and efficient Linux system, and tools like top and ps offer insights into the real-time status of process prioritization.

[Load average](#contents.xhtml_sc3_96a)

Load average is a metric the Linux kernel provides that offers a straightforward representation of the system load over time. It indicates the number of pending system resource requests, helping administrators gauge system health and performance trends. The kernel calculates the load number every five seconds based on the number of processes in runnable and uninterruptible states. This calculation results in an exponential moving average reported over the most recent 1, 5, and 15 minutes. Linux calculates the load average by considering both CPU and I/O related processes. It represents the number of processes ready to run or waiting for disk/network I/O to complete. Unlike some UNIX systems that only focus on CPU utilization, Linux's load average incorporates disk and network utilization, acknowledging their impact on overall system performance. The load average reflects the number of processes currently waiting for requests to complete, whether it is CPU time or critical disk I/O operations. When load averages are high with minimal CPU activity, it suggests investigating disk and network activity for potential bottlenecks. The uptime command is a quick way to display the current load average. The values represent the load over the last 1, 5, and 15 minutes.

Following is an example:

$ uptime

05:44:08 up 0 min, 1 user, load average: 0.27, 0.06, 0.02

To evaluate the impact of load averages, consider the number of logical CPUs on the system. Using the lscpu command helps determine the CPU configuration. Following is an example:

$ lscpu

On-line CPU(s) list: 0-3

Thread(s) per core: 2

Core(s) per socket: 4

Socket(s): 1

If load averages are mainly due to processes needing CPU time, divide the load average values by the number of logical CPUs. A value below 1 indicates satisfactory resource utilization, while above 1 suggests resource saturation and potential processing delays.

[Real-time process monitoring](#contents.xhtml_sc3_97a)

Understanding load averages is crucial, but real-time monitoring tools provide deeper insights into individual processes. The top program is one such tool that offers a dynamic view of system processes. It continuously refreshes, allowing administrators to identify resource intensive processes.

The key features and keystrokes in top are as follows:

*   Help for interactive keystrokes: ? or h
*   Toggle load, threads, and memory header lines: l, t, m
*   Toggle showing individual CPUs or a summary: 1
*   Change the refresh rate: s
*   Kill a process: k
*   Renice a process: r
*   Sort process listing by memory or CPU usage: Shift + m, Shift + p
*   Quit: q

These functionalities provide administrators with the flexibility to monitor and manage processes effectively. The following top command output provides a real-time snapshot of system performance, displaying the current time, system uptime, logged-in users, and load averages for the last 1, 5, and 15 minutes. It lists 319 total processes, with 1 running, 318 sleeping, and no stopped or zombie processes. CPU usage is detailed with percentages of time spent on user and system processes, idling, and handling interrupts, indicating 99.2% idle time. Memory usage is shown with a total of 3585.8 MiB, of which 2594.2 MiB is free, 733.5 MiB is used, and 426.4 MiB is for buffers/cache. Additionally, swap space totals 2048.0 MiB, all free, with 2852.3 MiB of available memory for new applications.

top - 05:46:10 up 2 min, 1 user, load average: 0.11, 0.06, 0.02

Tasks: 319 total, 1 running, 318 sleeping, 0 stopped, 0 zombie

%Cpu(s): 0.2 us, 0.5 sy, 0.0 ni, 99.2 id, 0.0 wa, 0.0 hi, 0.1 si, 0.0 st

MiB Mem : 3585.8 total, 2594.2 free, 733.5 used, 426.4 buff/cache

MiB Swap: 2048.0 total, 2048.0 free, 0.0 used.  2852.3 avail Mem

[Process signals](#contents.xhtml_sc3_98a)

Understanding the techniques and commands for process control in Linux is important to use different types of signals for effective system administration appropriately. The most important ones are mentioned as follows:

*   Signal characteristics: Each signal has a default action, like terminating or suspending a program, and programs can be designed to handle signals in specific ways.
*   Understanding signals: Signals are software interrupts sent to processes to communicate various events, such as errors, external events, or explicit commands. Examples include SIGHUP (hangup), SIGINT (keyboard interrupt), SIGQUIT (keyboard quit), SIGKILL (kill, unblockable), and SIGTERM (terminate).
*   Sending signals: Signals can be sent to processes using keyboard sequences (e.g., Ctrl+C for SIGINT) or commands (kill, killall, pkill). The kill command, despite its name, is used for sending any signal, not just for terminating processes. The killall command targets multiple processes by their command name, and pkill allows sending signals based on various criteria like command name or user ID.
*   Selective process termination: Processes can be selectively terminated based on various criteria, such as controlling terminal or parent-child relationships. The pstree command can help visualize process relationships, aiding in targeted process management.
*   Process management commands: Various commands, including kill, killall, pkill, pgrep, and pstree, are used for managing and terminating processes. These commands allow targeting specific processes or groups of processes based on different criteria such as process ID, user ID, or parent-child relationships.
*   Administrative user logout: For administrative purposes, it is possible to log out users by terminating their session using signals. The w command can identify login sessions, and commands like pkill can terminate all processes for a specific user. It is recommended to use SIGTERM first, then SIGINT, and resort to SIGKILL only, if necessary, as SIGKILL does not allow processes to perform cleanup routines.

[Services and daemons](#contents.xhtml_sc2_99a)

In RHEL, efficient management of services, daemons, and the boot process is paramount for system administrators. The cornerstone of service and boot process management in RHEL is systemd. As the first process initiated during system startup, systemd orchestrates the activation of system resources, server daemons, and other processes. Its rich feature set includes parallelization for faster boot times, on-demand starting of daemons, and automatic service dependency management. Systemd utilizes units to manage various objects. Notably, service units (ending with .service) represent system services, socket units (ending with .socket) handle inter-process communication, and path units (ending with .path) delay service activation until specific file system changes occur.

[Service status](#contents.xhtml_sc3_100a)

The systemctl command becomes the swiss army knife for administrators, providing insights into the system's state. Users can effortlessly explore loaded units, check their activation states, and view detailed information about specific services by using options like list units and status. System administrators can use systemctl to verify the specific states of a service. Keywords such as loaded, active (running), and inactive provide a quick overview of a service's status. Additionally, the is-active, is-enabled, and is-failed options allow users to check the runtime, startup enablement, and failure status of services, respectively. We can test when the service is enabled or active using the following commands:

$ systemctl is-enabled sshd

enabled

$ systemctl is-active sshd

active

Users can list installed service units and identify active or enabled services. We can list all the status information using the following command:

$ systemctl status sshd

● sshd.service - OpenSSH server daemon

Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: enabled)

Active: active (running) since Sun 2023-12-31 10:45:27 PST; 2min 17s ago

Docs: man:sshd(8)

man:sshd_config(5)

Main PID: 1076 (sshd)

Tasks: 1 (limit: 22573)

Memory: 5.3M

CPU: 113ms

CGroup: /system.slice/sshd.service

└─1076 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Dec 31 10:45:27 localhost.localdomain systemd[1]: Starting OpenSSH server daemon...

Effectively controlling services and managing the boot process is crucial for maintaining a stable and responsive Linux system. RHEL, with its powerful systemd utility, empowers administrators to achieve this efficiently. The systemd process service control and boot process management in the RHEL environment.

[Start and stop services](#contents.xhtml_sc3_101a)

In the complex ecosystem of RHEL, the effective management of system services is a critical task for system administrators to control system daemons and network services using the powerful systemctl utility.

System services often require manual intervention for various reasons, such as updates, configuration changes, or uninstallation. The systemctl utility is a cornerstone of RHEL administration, which provides the means to start and stop services seamlessly. To initiate a service, administrators can use the systemctl start command, ensuring that the service is not already running. Conversely, the systemctl stop command halts a currently running service. The following command starts the sshd.service:

# systemctl start sshd.service

System administrators frequently encounter scenarios where restarting or reloading a service is necessary. The systemctl restart command accomplishes a full restart of a running service, while the systemctl reload command allows services to reload their configuration files without a restart. The first command performs a full process restart, whereas the second only reloads the configuration. There are pros and cons in each command. The first generates some downtime but fully reloads the process, so it is useful when we need to update the software providing the process. The second is faster; it only reloads the configuration without any downtime.

Ensuring that services start or stop automatically during system boot is a common administrative task. The use of systemctl enable and systemctl disable commands to create or remove symbolic links that control the automatic service startup at boot time. The following command is enabled on the book the sshd.service:

# systemctl enable sshd.service

To enable and start a service at the same time, use the --now option:

$ sudo systemctl enable --now sshd.service

[Dependencies and conflicts](#contents.xhtml_sc3_102a)

Dependencies among services are common in complex systems. systemd, coupled with the systemctl utility, dynamically manages service dependencies. The systemctl list-dependencies command reveals the hierarchy of dependencies for a given service unit. Understanding dependencies is crucial for maintaining a stable and responsive system.

Conflicts between services can arise in a system, leading to the need for masking certain services. The systemctl mask command prevents the accidental start of conflicting services by creating symbolic links to /dev/null. The following command masks and unmasks the httpd.service:

# systemctl mask httpd.service

Created symlink /etc/systemd/system/ httpd.service → /dev/null

Mastering the control of system services is fundamental to maintaining a robust and efficient RHEL system.

[Boot process](#contents.xhtml_sc2_103a)

Controlling the boot process in RHEL is a critical aspect of system administration, allowing for efficient management and customization of the system's startup sequence. The boot process is a series of events initiated when the system is powered on or restarted, encompassing hardware initialization, loading the kernel, and launching essential services. In RHEL, administrators can influence this process by configuring various parameters, setting up service dependencies, and employing tools such as Grand Unified Bootloader (GRUB) to manage the bootloader. Understanding and mastering the intricacies of the boot process empowers administrators to optimize system performance, troubleshoot issues, and tailor the startup sequence to meet specific operational requirements. More details about the boot will be explained extensively in [Chapter 8](#ch08.xhtml), Performance Optimization and Troubleshooting.

[Log files](#contents.xhtml_sc2_104a)

Processes and operating systems record a log of events. These log files are particularly useful for troubleshooting or tracing behavior dynamics. We can inspect the files stored in the /var/log directory using the less and tail text commands. The systemd-journald and rsyslog services handle the syslog messages in modern RHEL. The first collects the event messages, while the second writes the events on the file or sends them via network messages. Following are the key log files:

*   /var/log/messages general purpose events
*   /var/log/secure security and authentication events
*   /var/log/maillog mail server events
*   /var/log/cron scheduled job execution events
*   /var/log/boot.log system startup events
*   /var/log/audit/audit.log SELinux audit event log
*   /var/log/dnf.rpm.log all install and remove DNF transactions log

Additional files can be created by specific processes or services.

[Managing software using DNF](#contents.xhtml_sc2_105a)

DNF is a package management system used in RHEL. It provides a powerful and efficient way to install and update software packages on a system. Installing software using DNF is a straightforward process, typically involving a single command, such as dnf install [package_name]. This command automatically resolves dependencies and fetches the required packages from repositories, streamlining the installation process. Similarly, updating installed software is as simple as running dnf update, ensuring the system stays current with the latest versions and security patches. DNF's user-friendly syntax and robust dependency management make it a reliable tool for system administrators and users alike, contributing to a seamless experience in managing software on Linux based systems.

In a RHEL system, the following components are necessary for our systems:

*   Red Hat subscription management: This is a key tool for managing access to Red Hat products and services. It involves registering a system with a Red Hat account, subscribing to it for updates, enabling specific repositories for software packages, and tracking entitlements. This can be done through a graphical interface or the subscription-manager command line. The process involves logging in with Red Hat Customer Portal credentials and may include auto-attaching a subscription.
*   Entitlement certificates: These digital certificates indicate the subscriptions attached to the system, stored in /etc/pki and its subdirectories. They are crucial for managing system updates and software installation entitlements.
*   DNF command: Finding, installing, and updating software packages using the dnf command. DNF interacts with repositories enabled through the subscription management process to install and update packages.
*   Repositories: Enabling and disabling Red Hat or third-party Yum repositories. This is important for controlling the sources from which packages are installed or updated.

    # subscription-manager repos --enable=rhel-9-for-$(uname -m)-baseos-debug-rpms

*   Module streams management: Red Hat Linux allows for the installation of specific versions of software via modules. Some packages have a shorter lifecycle than the distribution. We can list, enable, switch module streams, and install or update packages from a module using the dnf module command.

[Storage in Linux](#contents.xhtml_sc2_106a)

Storage in Linux is a crucial aspect of system management, encompassing a variety of technologies and tools to handle data effectively. Linux provides a flexible and robust storage infrastructure, allowing administrators to employ diverse file systems, storage devices, and volume management solutions. Whether utilizing traditional hard drives or modern solid-state drives, Linux administrators can harness a plethora of storage options, ensuring efficient data organization and accessibility for optimal system performance. Every time we modify a physical partition, the udevadm settle command waits till the system reloads the newest disk geometry.

[Logical Volume Manager](#contents.xhtml_sc3_107a)

LVM provides a dynamic and flexible approach to managing disk space in RHEL. With LVM, administrators can create logical volumes (LVs) that span multiple physical volumes (PVs), allowing for easy resizing, moving, and concatenating storage space. This dynamic storage allocation facilitates tasks such as resizing filesystems without downtime and simplifies disk space management in complex storage environments. LVM also introduces concepts like volume groups  (VGs) and PVs, offering a layer of abstraction between the physical disks and the logical volumes.

Following steps are the most common LVM operations to create, extend, reduce, and delete logical volumes:

1.  Displaying VG information: View information about existing volume groups:

    # vgdisplay

2.  Creating a LV: Create a logical volume named mylv with a size of 10 GB in the volume group myvg:

    # lvcreate -n mylv -L 10G myvg

3.  Displaying LV information: View information about logical volumes:

    # lvdisplay

4.  Formatting a LV: Format the logical volume with a filesystem, for example, ext4:

    # mkfs.ext4 /dev/myvg/mylv

5.  Mounting a LV: Create a mount point and mount the logical volume:

    # mkdir /mnt/mylv

    # mount /dev/myvg/mylv /mnt/mylv

6.  Extending a LV: Extend the logical volume mylv by 5 GB:

    # lvextend -L +5G /dev/myvg/mylv

7.  Resizing the filesystem: Resize the filesystem to reflect the new size:

    # resize2fs /dev/myvg/mylv

8.  Reducing a LV: Reduce the size of the logical volume mylv by 2 GB:

    # lvreduce -L -2G /dev/myvg/mylv

9.  Unmounting and removing a LV: Unmount the logical volume and remove it:

    # umount /mnt/mylv

    # lvremove /dev/myvg/mylv

10.  Displaying free space: View free space in the volume group:

    # vgs

We should replace myvg, mylv, and sizes with our actual volume group, logical volume, and sizes. Proper caution should be exercised while performing operations like reducing logical volumes, as data loss may occur if not done carefully. Always ensure we have backups before making significant changes to our storage configuration.

[RAID configurations](#contents.xhtml_sc3_108a)

RAID configurations in RHEL involve combining multiple physical disks into a single logical unit to improve data redundancy, performance, or a combination of both. Different RAID levels provide varying degrees of redundancy and performance optimization. For instance, RAID 1 mirrors data across multiple disks for redundancy, while RAID 0 stripes data for improved performance. RHEL supports various RAID levels, and administrators can choose the most suitable configuration based on the desired balance between data protection and performance.

The mdadm utility is commonly used for managing software RAID configurations in RHEL. Following are the steps:

1.  RAID 1 (mirroring): Create a RAID 1 array named md0 with two disks /dev/sdb1 and /dev/sdc1.

    # mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1

2.  RAID 0 (striping): Create a RAID 0 array named md1 with two disks /dev/sdb1 and /dev/sdc1:

    # mdadm --create --verbose /dev/md1 --level=0 --raid-devices=2 /dev/sdb1 /dev/sdc1

3.  RAID 5 (striping with parity): Create a RAID 5 array named md2 with three disks /dev/sdb1, /dev/sdc1, and /dev/sdd1:

    # mdadm --create --verbose /dev/md2 --level=5 --raid-devices=3 /dev/sdb1 /dev/sdc1 /dev/sdd1

4.  RAID 10 (mirrored stripes): Create a RAID 10 array named md3 with four disks /dev/sdb1, /dev/sdc1, /dev/sdd1, and /dev/sde1:

    # mdadm --create --verbose /dev/md3 --level=10 --raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1

5.  Displaying RAID information: Display information about the created RAID arrays:

    # cat /proc/mdstat

6.  Monitoring RAID arrays: Monitor the status of RAID arrays:

    # mdadm --detail /dev/md0

7.  Stopping and removing RAID arrays: Stop and remove a RAID array (replace /dev/md0 with the appropriate RAID device):

    # mdadm --stop /dev/md0

    # mdadm --remove /dev/md0

These examples assume that we have disks available (such as /dev/sdb1, /dev/sdc1, etc.) for creating RAID arrays. Adjust the disk names and RAID device names according to our specific configuration. Always exercise caution when working with RAID configurations, as improper actions can lead to data loss. Additionally, it is advisable to check the status of RAID arrays regularly for any issues or disk failures.

[File system](#contents.xhtml_sc3_109a)

In RHEL, the file system plays a pivotal role in organizing and managing data on storage devices. RHEL supports various file systems, with the .ext4 file system being the default choice for its reliability, performance, and features like journaling. .ext4 efficiently handles tasks such as metadata journaling, ensuring data consistency during system crashes. Additionally, RHEL embraces the XFS file system, known for its scalability, high-performance capabilities, and suitability for handling large files and volumes. The file system choices in RHEL also extend to Btrfs, providing advanced features like snapshots and checksums for enhanced data integrity. With options like LVM and RAID configurations, RHEL administrators have a versatile toolkit for managing storage resources, ensuring data security, and optimizing system performance in diverse enterprise environments. The Filesystem Hierarchy Standard (FHS) is a set of guidelines and conventions for organizing the file systems of Unix-like operating systems, including Linux. FHS defines the directory structure and the purpose of each directory, ensuring consistency and compatibility across different Linux distributions. It establishes a standardized hierarchy, such as separating system files from user files, defining directories like /bin for essential command binaries, /etc for configuration files, /home for user home directories, and /var for variable data files. Adhering to the FHS helps maintain a structured and predictable filesystem layout, facilitating software installation, system administration, and interoperability among different Linux distributions. A quota in a filesystem is a mechanism used to limit and manage disk usage for users and groups, ensuring fair allocation of storage resources and preventing excessive consumption by any single user or group. Quotas can enforce both soft limits (allowing temporary overuse) and hard limits (strict caps) on disk space and inodes. They are typically implemented on filesystems like XFS and ext4 and configured using tools such as xfs_quota or quota. The options usrquota and grpquota are used in mount configurations to enable quotas specifically for individual users and groups, respectively. This ensures precise control over resource usage in multi-user environments, maintaining system performance and stability..

[Swap](#contents.xhtml_sc3_110a)

Managing swap space in Linux is crucial for optimizing system performance and creating and managing swap spaces to supplement physical memory. Swap space is controlled by the Linux kernel memory management subsystem, and is utilized to store inactive pages of memory when system RAM usage exceeds defined limits, forming the virtual memory. The size of the swap space is contingent on the system's memory workload, and recommendations are provided based on total physical memory, as shown in [Table 3.2](#ch03.xhtml_tab3-2):

| RAM size | Swap size | Hibernation enabled |
| less 2 GiB | 2x RAM | 3x RAM |
| 2 GiB and 8 GiB | Same as RAM | 2x RAM |
| 8 GiB and 64 GiB | >4 GiB | 1.5 x RAM |
| 64+ GiB | > 4 GiB | Not recommended |

Table 3.2: Suggested swap space according to RAM

We can create a swap partition using the parted and mkswap tools, setting the file system type to linux-swap for clarity. We can activate and deactivate swap spaces using commands like swapon and swapoff are detailed, and the persistence of swap space activation through the /etc/fstab file is discussed. Additionally, this section covers setting swap space priorities to optimize kernel utilization when multiple swap spaces are defined. Overall, it offers a comprehensive understanding of swap space management in Linux, ensuring efficient memory utilization.

[Hard and soft link](#contents.xhtml_sc3_111a)

Creating multiple names that point to the same file using hard and soft (symbolic) links is possible in a Linux file system. Each has its advantages and limitations. Hard links can be created using the ln command, point to the same data on the storage device, and share characteristics such as link count, permissions, ownership, timestamps, and file content. The following command creates the newfile.txt as a hard link to the original.txt file:

$ ln original.txt hard.txt

-rw-r--r--. 2 devops devops 0 Dec 31 10:53 hard.txt

-rw-r--r--. 2 devops devops 0 Dec 31 10:53 original.txt

However, hard links are restricted to regular files and only the same file system. Soft links, created with the ln -s command, can span different file systems and link to directories or special files.

The following command creates the newfile.txt as a soft link to the original.txt file:

$ ln -s soft.txt original.txt

-rw-r--r--. 2 devops devops 0 Dec 31 10:53 original.txt

lrwxrwxrwx. 1 devops devops 12 Dec 31 10:55 soft.txt -> original.txt

The day-to-day management includes creating and managing links, identifying link relationships, and handling dangling soft links. A dangling soft link produces the following message on the screen when trying to access the linked file:

$ cat: soft.txt: No such file or directory

[SMB storage](#contents.xhtml_sc2_112a)

Accessing Network-Attached Storage (NAS) using protocols like Server Message Block  (SMB) and Network File System (NFS) allows users to share and manage files across a network.

Following are basic steps for accessing NAS using SMB/CIFS protocols common in a Windows environment:

1.  Install required packages: Ensure that the necessary SMB client packages are installed. In an RHEL we can use:

    # sudo dnf install cifs-utils

2.  Create a mount point: Create a directory where we want to mount the SMB share. For example:

    # mkdir /mnt/smbshare

3.  Mount the SMB share: Use the mount.cifs command to mount the SMB share. Replace //server/share with the actual SMB share path, and provide our username and password when prompted:

    # mount.cifs //server/share /mnt/smbshare -o username=nas_username,password=nas_password

    We can also add the credentials to a credentials file and use it during the mount:

    # echo "username=nas_username" > ~/.smbcredentials

    # echo "password=nas_password" >> ~/.smbcredentials

    # chmod 600 ~/.smbcredentials

    # mount.cifs //server/share /mnt/smbshare -o credentials=~/.smbcredentials

4.  Access the SMB share: Navigate to the mount point (/mnt/smbshare in this example) to access the SMB share's contents.

[NFS storage](#contents.xhtml_sc2_113a)

In the world of enterprise computing, accessing and managing NAS is a fundamental skill for system administrators. In this section, we will explore two essential methods for accessing NAS in a Linux environment: NFS and the automounter. NFS is an open-standard protocol used by Linux, UNIX, and similar operating systems for their native network file system. It supports native Linux permissions and file system features and is actively enhanced. In RHEL, NFSv4.2 is the default version, with support for NFSv3 as well. NFSv2 is no longer supported.

NFSv4 uses only the TCP protocol, while earlier versions could use TCP or UDP for communication.

[Mounting](#contents.xhtml_sc3_114a)

To access an NFS share, we need to follow these steps:

1.  Identify: Determine the available NFS shares. We can either obtain this information from the NFS server administrator or explore the server's root directory as the root user. Access to shares with Kerberos security may be denied, but share names will still be visible.
2.  Mount point: Create a directory to serve as the mount point. Use the mkdir command to create it.
3.  Mount: We can mount NFS shares in different ways:
    *   Temporary mount: Use the mount command, e.g.,

        $ sudo mount -t nfs -o rw,sync server:/share /mnt/nfs

        This mounts the share temporarily, useful for one time access or testing.

    *   Persistent mount: Add an entry to the /etc/fstab file to ensure the NFS share is mounted at boot time. Then, use the following command to mount it:

        $ sudo mount /mnt/nfs

        The NFS client service reads server and mount options from /etc/fstab, so we do not need to specify them on the command line.

4.  Unmount: As root or using sudo, unmount an NFS share with the umount command, for example:

    $ sudo umount /mnt/nfs

| Note: Unmounting a share does not remove its /etc/fstab entry. |

[Automounting](#contents.xhtml_sc3_115a)

Automount NFS shares using direct and indirect maps, including wildcards.

The automounter (autofs) is a service that automatically mounts NFS shares on demand and unmounts them when they are no longer in use. It offers several benefits, as follows:

*   Users do not need root privileges to mount or unmount shares.
*   NFS shares are available to all users, subject to access permissions.
*   Shares are not permanently connected, conserving resources.
*   Configuration is client-side; no server-side changes are required.
*   It supports various mount options and network file systems.
*   Maps can be either direct or indirect, offering flexibility in mount points.

Configuring an automount involves several steps, which are as follows:

1.  Install autofs: Install the autofs package on our system using our package manager.

    $ sudo yum install autofs

2.  Create master map: Add a master map file (e.g., /etc/auto.master.d/demo.autofs) to identify the base directory for mount points and specify the mapping file. Use an absolute file name and ensure it has the .autofs extension.

    /- /etc/auto.demo

3.  Create mapping files: Create mapping files (e.g., /etc/auto.demo) to define the mount points, options, and source locations for automounts.

    /share -rw,sync server:/nfs/share

4.  Start autofs: Use systemctl to start and enable the autofs service.

    $ sudo systemctl enable --now autofs

[Direct and indirect maps](#contents.xhtml_sc3_116a)

With the automounter, we can configure two types of maps as follows.

*   Direct maps: These map an NFS share to an existing absolute path mount point. In the master map file, use /- as the base directory. In the mapping file, specify the mount point and options.

    /- /etc/auto.direct

    /mnt/docs -rw,sync server:/nfs/docs

*   Indirect maps: When an NFS server exports multiple subdirectories within a directory, we can configure the automounter to access any of these subdirectories using a single mapping entry. Use * as the key and & in the source location.

    * -rw,sync server:/nfs/&

Accessing NAS in a Linux environment is essential for managing shared resources efficiently. The NFS protocol and the automounter provide powerful tools for achieving this. By understanding these concepts and practicing the guided exercise, we will be well equipped to manage network attached storage in our own Linux systems.

[Conclusion](#contents.xhtml_sc2_117a)

This chapter provided a comprehensive exploration of Red Hat System Administration, focusing on the essential skills and tools needed for effective system management. Starting with network configuration, user and group management, task scheduling, storage solutions, and service control, it is a solid foundation for both practical system administration and RHCE certification preparation. Key highlights included the in-depth discussion of network management, covering hostname settings, DNS resolution, and network interface troubleshooting using commands like nmcli and ip. The practical guidance on user and group management emphasized secure account creation and the management of permissions and access control using tools such as chmod, chown, and ACLs. The chapter also covered task scheduling with tools like cron, anacron, and systemd timers, illustrating the flexibility of Linux in automating routine processes. Insights into file system management, including LVM and RAID configurations, showcased the robustness of Linux storage solutions. Additionally, topics like process management and real-time monitoring through commands like top and uptime demonstrated effective resource optimization techniques. Finally, the introduction of systemd as a cornerstone for service management underscored its critical role in modern RHEL systems. Tools like systemctl provided a practical understanding of controlling, enabling, and troubleshooting services and daemons.

In the next chapter, the focus shifts to automation with Ansible, a powerful tool that simplifies and elevates the efficiency of system management. Readers will explore Ansible’s architecture, ad hoc commands, playbooks, and advanced features, setting the foundation for streamlined IT operations and deeper automation expertise.

[Points to remember](#contents.xhtml_sc2_118a)

*   In RHEL, hostname management, DNS configuration, and network interface troubleshooting are accomplished using commands like hostname and hostnamectl, the stub resolver, and tools such as nmcli, ip, ping, tracepath, and ss, ensuring efficient system administration and network functionality.
*   To schedule future tasks on a system, administrators can use crond for recurring commands with specific timing, anacron for ensuring important tasks run even if the system was turned off, and systemd timers for timer-based activation of other systemd units, each with its own configuration and syntax.
*   Managing local users and groups is a crucial aspect of Linux system administration, involving user and group management, password configuration, superuser access, and the use of commands like useradd, usermod, userdel, groupadd, groupmod, and groupdel to create, modify, and delete user and group accounts.
*   Linux administrators can manage file access control effectively by using commands like chmod and chown, understanding symbolic and numeric methods for setting permissions, handling special permissions like setuid, setgid, and sticky, and utilizing default permissions and umask settings, while also having the option to employ ACLs to provide fine-grained control over file and directory access beyond traditional Unix permissions.
*   Effective process scheduling in Linux involves time-slicing, relative priorities (nice values), and commands like nice and renice to manage process priority; load average provides insight into system health and performance trends based on pending resource requests, with the uptime command displaying current load average values; real-time process monitoring is facilitated by tools like top with interactive features for resource-intensive process identification and management.
*   Efficient management of services and daemons in RHEL relies on the systemd utility, enabling the control of service activation, status checking, and dependency management using commands like systemctl, with options such as start, stop, restart, and reload for seamless service management and enable and disable to control automatic service startup at boot time, while understanding dependencies and conflicts is essential for system stability.
*   Linux storage encompasses various technologies and tools for effective data management, including LVM for dynamic disk space allocation, RAID configurations for data redundancy and performance optimization, multiple file systems like .ext4, XFS, and Btrfs, swap space management, and the use of hard and soft links; accessing NAS can be achieved via SMB or NFS protocols by installing the required packages, creating a mount point, and using the appropriate commands.

[Multiple choice questions](#contents.xhtml_sc2_119a)

1.  How can we modify the network IP address in RHEL?
    1.  The hostnamectl command
    2.  The /etc/hosts file
    3.  The nmcli interactive command
    4.  The ip link command
2.  What the following permission mean -rwsr-xr-x?
    1.  Read and execution for all the users
    2.  Write permission for group
    3.  It is a directory
    4.  The setuid permissions
3.  How to start a service and after the boot?
    1.  systemctl enable sshd.service
    2.  systemctl enable --now sshd.service
    3.  systemctl start sshd.service
    4.  systemctl is-enabled sshd.service
4.  What is the best way to increase the reliability of the storage?
    1.  LVM
    2.  RAID configuration
    3.  File system
    4.  Swap

[Answer](#contents.xhtml_sc3_120a)

1\. c

2\. d

3\. b

4\. b

[Questions](#contents.xhtml_sc2_121a)

1.  What command would you use to view the network configuration on a Red Hat system?
2.  How can you schedule a cron job to run daily at 3 AM? Please provide an example.
3.  How to add a user to multiple groups during the creation of the user account?
4.  What is the command to check if the sshd service is active and enabled on a system?
5.  What are the steps to change the static IP address of a network interface using nmcli?
6.  What does the nice value of a process signify and how can it be modified?
7.  What is the  difference between symbolic and numeric methods of changing permissions?
8.  How to create a new logical volume of 10 GB size using LVM?
9.  What are the advantages of using RAID 1 over RAID 0?
10.  What file system is the default choice in RHEL and why?

[Key terms](#contents.xhtml_sc2_122a)

*   hostname:  It is a unique label assigned to a device connected to a computer network.
*   Stub resolver: A DNS stub resolver is an operating system component that performs DNS name resolution for applications running on a computer, cell phone, or another Internet connected device.
*   crond: It is the background daemon process in Unix like operating systems that manages the scheduling and execution of scheduled tasks or cron jobs at specified intervals.
*   anacron: It is a program that performs periodic command scheduling, which is traditionally done by cron for systems that do not run 24/7.
*   Sysstat: System statistics is a collection of performance monitoring tools for Linux.
*   UID: Is a unique numeric identifier assigned to each user in a Linux system, serving as the primary means of distinguishing and managing user accounts.
*   GID: This is a unique numeric identifier assigned to each group in a Linux system, facilitating the organization and control of user access to shared resources.
*   Daemon: It is a background process or service that runs on a computer system independently of user interaction, often performing tasks like managing system services, handling hardware devices, or executing scheduled jobs.
*   File system: It is a method of organizing and managing files and data on a storage device, providing a structured hierarchy, access controls, and metadata for efficient data storage and retrieval in a computer or operating system.
*   .ext4: It is a widely used and robust file system in Linux, offering features such as journaling, scalability, and support for large file sizes and volumes.
*   XFS: It is a high-performance and scalable file system in Linux, known for its efficient handling of large files, rapid crash recovery, and advanced features like delayed allocation.
*   Btrfs, or B-tree file system: Is a modern copy-on-write file system designed for Linux that offers advanced features such as snapshotting, scalability, and data integrity.
*   RAID: A Redundant Array of Independent Disks is a storage technology that combines multiple physical disk drives into a single logical unit to improve performance, reliability, or a combination of both.
*   Swap: In computer memory management, swap is a dedicated area of a storage device (usually a disk) used as virtual memory to temporarily store data that cannot fit into a computer's physical RAM, allowing the system to handle more applications and data than the available RAM would permit.

# [CHAPTER 4Automating Linux Tasks](#contents.xhtml_ch04a)

[Introduction](#contents.xhtml_sc2_123a)

In this chapter, we will learn about Ansible and why it is an essential tool for efficient system management. We will improve our scripting and automation abilities, elevating to a highly proficient Linux administrator who is well-prepared to conquer the challenges of the RHCE certification. The chapter will cover various topics, such as architecture, ad hoc commands, inventories, modules, playbooks, variables, loops, conditional tasks, error handling, and Ansible vault for safeguarding sensitive data.

[Structure](#contents.xhtml_sc2_124a)

The chapter covers the following topics:

*   Bash scripting versus Ansible
*   Ansible architecture
*   Ansible language
*   Creating Ansible plays and playbooks

[Objectives](#contents.xhtml_sc2_125a)

The primary goal of this chapter is to provide a comprehensive understanding and practical mastery of automating tasks within the Linux environment, leveraging the Ansible tool. This chapter is designed to cater to both Linux enthusiasts and RHCE aspirants. It aims to impart essential skills and knowledge for automating routine tasks, thereby streamlining system management. Through a blend of theoretical insights and hands on exercises, readers will gain proficiency in scripting and automation. The chapter will culminate in equipping readers to be more efficient Linux administrators, fully prepared for the automation challenges presented in the RHCE certification.

[Bash scripting versus Ansible](#contents.xhtml_sc2_126a)

Ansible's emergence in IT automation marked a significant shift from traditional Bash scripting. Originally, Bash scripting is vital in system administration for Unix and Linux systems, offering versatility but with complex scripts that were challenging to maintain and scale. In contrast, Ansible, introduced in 2012, revolutionized automation with its simplicity and agentless approach, eliminating the need for software installation on managed nodes. Its user friendly YAML playbooks democratized infrastructure automation, making it more accessible compared to the complex Bash scripts.

The key advantages of Ansible over Bash scripting include its idempotent nature, ensuring consistent results without unintended side effects, superior scalability, and managing numerous machines from a single point. Ansible’s modular design offers extensive flexibility and reusability, seamlessly integrating with cloud services and platforms and aligning with the shift towards hybrid and cloud-native environments.

Ansible symbolizes a new era of more manageable, scalable automation solutions in the shift from traditional system administration to DevOps and infrastructure as code (IaC). While Bash scripting retains its value, Ansible has become the modern standard for automation, efficiently bridging gaps in complex tasks. It excels in inventory management, error handling, and has a robust community and support network, features not inherent in Bash scripting. Ansible’s integration with advanced IT environments and compatibility with Red Hat products make it a holistic tool for RHEL environments, offering a scalable, efficient automation solution.

In the context of Ansible's rise in IT automation compared to Bash scripting, another key distinction lies in the programming paradigms they represent: Ansible is predominantly declarative, whereas Bash scripting is imperative. In declarative programming, as seen with Ansible's YAML based playbooks, we specify the desired state of our system or end goal, and Ansible figures out how to achieve that state. This contrasts with the imperative nature of Bash scripting, where we provide explicit commands in a specific order to achieve the desired outcome. This shift from the step-by-step approach of imperative scripting to the outcome-focused declarative model in Ansible greatly simplifies the automation of complex systems, making them more accessible and maintainable.

[Ansible architecture](#contents.xhtml_sc2_127a)

Ansible's architecture is designed for ease of use and flexibility. Its agentless nature and the ability to manage a wide range of operating systems make it a versatile tool for IT automation. The controller node acts as the command center, sending out tasks to the target nodes, which can be any mix of Linux, Windows, and macOS systems. The simplicity of its design, coupled with powerful features, makes Ansible a go to choice for many system administrators and DevOps professionals. Ansible's architecture is elegantly simple yet powerful, and it operates consistently across different operating systems like Linux, Windows, and macOS. Its architecture mainly revolves around two types of systems: the controller node and the managed or target node, as shown in [Figure 4.1](#ch04.xhtml_fig4-1):

![](images/Figure_4.1.png)

Figure 4.1: Ansible architecture

*   Controller node: The controller node is where Ansible is installed and run. This node orchestrates the automation tasks on target nodes. It is important to note that Ansible can only be installed on Linux based systems. Therefore, the controller node must be a Linux machine. This machine is where we will create and store our Ansible playbooks, which are files written in YAML that define the tasks to be executed.
*   Managed nodes: The managed or target nodes are the nodes that we manage with Ansible. These can be Linux, Windows, macOS, or any supported system. Ansible does not require any agent software to be installed on the target nodes. Instead, it connects to these nodes using SSH for Linux/macOS systems or Windows Remote Management (WinRM) for Windows systems.

Ansible communicates with the following:

*   Linux: Linux systems are typically straightforward to manage with Ansible, as they natively support SSH or via the Python Paramiko library.
*   Windows: Managing Windows systems requires additional setup, like configuring WinRM for secure communication. Ansible can manage a variety of tasks on Windows, including software installation, updates, and configuration management. It might require some initial configuration on the Windows systems to enable and secure WinRM connections.
*   macOS: Similar to Linux, macOS uses SSH for connections. However, the tasks we might automate on macOS could differ, focusing more on developer environments and applications specific to macOS.

In Ansible, modules, tasks, playbooks, and inventory files form the foundation of automating IT environments as follows:

*   Modules and tasks:
    *   Ansible modules are small programs that Ansible sends over to the target nodes. These can be tailored for specific tasks like installing packages, copying files, or managing services. Usually, they are written in native Python.
    *   Each task in a playbook calls a list of modules. When a playbook is run, Ansible copies these modules to the target nodes, executes them, and then deletes them after completion.
*   Playbooks:
    *   Playbooks are the core component of Ansible's automation. They are written in YAML and define the tasks to be executed in a sequenced order on target nodes.
    *   Playbooks can include variables, conditions, loops, and more, making them very powerful and flexible for complex automation tasks.
*   Inventory:
    *   The inventory file in Ansible lists all the target nodes. It can group nodes, useful for targeting specific machines or groups for particular tasks.
    *   The inventory can be a simple static file or a dynamic source that pulls in node information from cloud providers or other services.

[Quick start](#contents.xhtml_sc3_128a)

Introducing and deploying Ansible in an IT environment involves several key steps, from understanding its fundamentals to actual implementation and usage.

Getting started with Ansible involves straightforward steps, including installation, configuring the inventory file, and creating playbooks to automate tasks across your IT infrastructure as follows:

*   Installation: Ansible can be easily installed on a RHEL control machine (which runs the playbooks). It can be installed via package managers like dnf, yum, apt, or pip.

    dnf install ansible-core

*   Configuring inventory: The inventory file (usually /etc/ansible/hosts) is used to define the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. We can specify group names [group_name] by specifying the name between curly brackets, and under each group, we can list hostnames or IP addresses.
*   Creating a playbook: A playbook is a YAML file where we define what tasks need to be performed. It starts with a list of hosts and then a list of tasks. Playbooks can include variables, tasks, and handlers.

[Ansible ad hoc](#contents.xhtml_sc3_129a)

Ad hoc commands in Ansible are a way to execute simple tasks against a set of hosts in our inventory on an as-needed basis without writing a full playbook. These commands are great for tasks that are too small to warrant writing a complete playbook. They are executed using the ansible command followed by the host group, module name, and any appropriate arguments. Following are some basic examples of ad hoc commands:

*   Checking connectivity with ping module:

    ansible localhost -m ping

    This command checks if all hosts in our inventory are ready to be managed by Ansible by utilizing the ping module.

    localhost | SUCCESS => {

    "changed": false,

    "ping": "pong"

    }

*   Running a command on a group of hosts:

    ansible web -m command -a “uptime”

    This command runs the uptime command on all hosts in the web group.

    web.example.com | CHANGED | rc=0 >>

    17:17:56 up 9:01, 2 users, load average: 0.93, 0.85, 0.78

*   Gathering facts:

    ansible localhost -m setup

    This command collects and displays the discovered facts for the localhost. We can do the same for any host. These ad hoc commands are a powerful feature for performing quick tasks across our managed hosts, and they provide a good way to get familiar with Ansible's capabilities before exploring more complex playbooks.

    localhost | SUCCESS => {

    "ansible_facts": {

    "ansible_all_ipv4_addresses": [

    "192.168.130.1"

    [REDUCTED]

[Inventories](#contents.xhtml_sc3_130a)

In Ansible, an inventory is a collection of hosts against which jobs may be launched, as well as a description of these hosts' characteristics. Inventories are crucial for defining which servers or systems should be managed and how to reach them.

Following is a detailed look at Ansible inventories:

*   Basic concept of inventory:

    *   Hosts: Individual machines or servers that Ansible can manage.
    *   Groups: Collections of hosts that can be targeted together. Groups can include other groups, allowing us to model our infrastructure with ease.

        The default inventory file is /etc/ansible/hosts, but we can use any file as an inventory file, provided we specify it in commands or configurations. It can be in INI or YAML format.

        The INI format example is as follows:

        [web]

        webserver1.example.com

        [db]

        dbserver1.example.com

        Here, “web” and “db” are groups that include one host each.

        YAML Format Example:

        all:

        children:

        web:

        hosts:

        webserver2.example.com:

        db:

        hosts:

        dbserver1.example.com:

    This is a YAML equivalent of the INI inventory format shown above.

*   Dynamic inventory: Instead of static files, Ansible can use dynamic inventories sourced from external systems. This is particularly useful in environments like cloud services, where machines and their IP addresses may frequently change. Ansible invokes a script, typically Python, that interacts with the platform API and returns a JSON.
*   Inventory variables: We can assign variables to hosts or groups within the inventory file for use in playbooks. Variables can be defined directly in the inventory, in separate files, or even dynamically generated. This is an example of two variables ntp_server and proxy for the db group:

    [db:vars]

    ntp_server=pool.ntp.org

    proxy=proxy.example.com

*   Aliases: We can define an alias for a host and use that in playbooks instead of actual hostnames.
*   Inventory parameters: Ansible allows us to specify connection parameters (like ansible_ssh_user, ansible_ssh_pass, etc.) within the inventory file.
*   Best practices:
    *   Keep it organized: Structure our inventory to mirror our environment's logical and network layout.
    *   Use version control: Track changes in our inventories with version control systems.
    *   Integrate with CMDB/Cloud: Use dynamic inventories to integrate with our Configuration Management Database (CMDB) or cloud providers for real-time updates.
*   Utilizing the inventory: When running ad hoc commands or playbooks, we can specify the inventory file using -i /path/to/inventory.

    Grouping hosts and defining common variables in the inventory can significantly reduce the complexity of playbook tasks and make our automation more efficient.

In summary, the inventory is a core component of Ansible, defining where and how our automation jobs run. Understanding and effectively organizing our inventory is key to efficient and scalable Ansible deployments.

[Modules](#contents.xhtml_sc3_131a)

Modules in Ansible are the units of code that Ansible executes. Each module is essentially a tool in our Ansible toolkit, performing a specific task. They are the core components that make Ansible a powerful and flexible automation platform.

The key aspects of the Ansible module are as follows:

*   Functionality: Each module is designed to handle a specific task. For example, the file module can change file attributes, the yum module can manage packages using YUM, and the git module can manage Git repositories.
*   Idempotency: One of the defining features of Ansible modules is their idempotency, meaning they will only make changes if those changes are necessary to achieve a desired state. This ensures that the same playbook run multiple times in sequence will have the same outcome and will not unnecessarily alter the state if it is already as desired.
*   Language: While most modules are written in Python, they can be written in any language that can return JSON, such as Perl, Ruby, or Bash. This flexibility allows for a wide range of modules to be developed and integrated into Ansible.
*   Extensibility: Ansible is designed to be easily extendable with custom modules. This allows users to tailor Ansible to their specific needs, adding modules for tasks or integrations unique to their environment.
*   Integration: Modules can integrate with various services and tools, from cloud providers like AWS and Azure to networking devices, databases, and more.

[Using modules in playbooks](#contents.xhtml_sc4_132a)

Modules are used within Ansible playbooks in tasks. Each task calls a module and passes relevant parameters to it. Following is the code for installing a package via Ansible:

- name: Web server installed

ansible.builtin.dnf:

name: httpd

state: present

In this example, the dnf module ensures the Apache (httpd) package is installed. In the same way, we can use the yum module.

Ansible is an open-source automation tool that provides a plethora of modules that enable users to manage and automate various aspects of their IT environment efficiently. These modules are essentially pre-written scripts that the Ansible playbook can invoke to perform specific tasks on managed nodes.

Here, we will explore some of the most commonly used Ansible modules, highlighting their purposes and providing examples of how they can be utilized to streamline our automation workflows as follows:

*   File modules:
    *   copy: Copies files from the local machine to a remote location. It is useful for deploying configuration files or scripts to managed nodes.

        - name: Copy configuration file

        ansible.builtin.copy:

        src: /local/path/to/file.conf

        dest: /remote/path/to/file.conf

    *   fetch: Retrieves files from remote nodes and stores them locally, allowing for backup or analysis of remote data.

        - name: Fetch a file from remote nodes

        ansible.builtin.fetch:

        src: /remote/path/to/file.conf

        dest: /local/path/to/store/file.conf

    *   file: Manages file properties and permissions. It can also be used to create or remove files and directories.

        - name: Ensure a directory exists

        ansible.builtin.file:

        path: /path/to/directory

        state: directory

        mode: '0755'

    *   lineinfile: Ensures a particular line is present in a file or not, which is useful for updating configuration files.

        - name: Ensure line is present in configuration file

        ansible.builtin.lineinfile:

        path: /path/to/file.conf

        line: 'Configuration line to be added'

        state: present

*   Software package modules:
    *   package: Generic module to manage packages using the system's package manager. It automatically detects the package manager, but it is discouraged as the package name might vary between the Linux distributions and lead to unforeseen results.

        - name: Install a package using the system's package manager

        ansible.builtin.package:

        name: nginx

        state: present

    *   yum/apt/dnf: These modules manage packages with YUM (for Red Hat based systems), APT (for Debian based systems), and DNF (for newer Red Hat based systems) respectively.

        - name: Install a package with YUM

        ansible.builtin.yum:

        name: httpd

        state: present

*   System modules:
    *   user: Manages user accounts.

        - name: Add a new user

        ansible.builtin.user:

        name: username

        state: present

    *   service: Manages services, ensuring they are running or stopped.

        - name: Ensure nginx is running

        ansible.builtin.service:

        name: nginx

        state: started

        enabled: true

*   Networking tools modules:
    *   get_url: Downloads files from HTTP, HTTPS, or FTP to the remote node.

        - name: Download a file

        ansible.builtin.get_url:

        url: http://example.com/path/to/file

        dest: /path/to/destination

    *   uri: Interacts with web services and APIs.

        - name: Make a GET request to an API

        ansible.builtin.uri:

        url: http://api.example.com/get/data

        method: GET

        return_content: true

By understanding and leveraging these commonly used modules, we can automate a wide range of tasks, from simple file copies to complex deployments and configurations, enhancing the efficiency and scalability of our IT operations.

[Documentation](#contents.xhtml_sc3_133a)

Ansible has a wide range of built-in modules, and many more are available through Ansible Galaxy or custom development. Detailed documentation for each module, including parameters and usage examples, is available in the Ansible documentation. Modules are the building blocks of Ansible automation, making them essential for anyone looking to use Ansible for their IT infrastructure management and automation needs. By leveraging modules, users can create powerful, scalable, and efficient automation solutions. We can access this documentation using the ansible-doc command, as shown in [Figure 4.2](#ch04.xhtml_fig4-2) or the [https://docs.ansible.com/](https://docs.ansible.com/) website:

![](images/Figure_4.2.png)

Figure 4.2: Output of the command ansible-doc debug

The provided documentation covers essential aspects of how Ansible works and what makes it a great tool for automation.

The document highlights several advantages of using Ansible, including its easy-to-read syntax, agentless architecture (requiring only SSH and Python on the managed nodes), push-based model (as opposed to pull-based), scalability, built-in modules for various tasks, and idempotence, ensuring that operations are performed once and only once, preventing redundant changes on the managed nodes. More for each module specifies every possible parameter with the data type, if it is required or not, and some code snippets as examples of the most common use cases.

The official Ansible documentation and module index provides comprehensive details on the more than 200 integrated modules available, as well as instructions on how to use Ansible for different automation tasks maintained directly by the Ansible Engineering Team. Every additional Ansible resource is present in the documentation and reassembles the same structure.

[Command line interface](#contents.xhtml_sc3_134a)

Ansible operation are performed using various command line utilities that make Ansible versatile and efficient for automation tasks. Following are the key Ansible command line utilities, exploring their functionalities and how they contribute to the overall automation experience:

*   ansible: The ansible command is the cornerstone of the Ansible automation platform, allowing users to execute ad hoc commands across their inventory. It is perfect for tasks that do not require a full playbook, such as quickly gathering information from a group of hosts or executing a single command across multiple machines. For example, checking uptime or rebooting servers can be easily accomplished with ansible command.
*   ansible-doc: The ansible-doc command is a CLI tool included with Ansible that provides documentation for Ansible modules. We can think of it as the man pages for Ansible modules, which show us how to use them, their parameters, examples, and much more. To view documentation for a specific module, we would use the command in the following format:

    ansible-doc <module_name>

    For example, to view documentation for the service module, we would run:

    ansible-doc service

    This command is incredibly useful for understanding the capabilities of modules and how to properly utilize them in our Ansible playbooks.

*   ansible-playbook: The ansible-playbook command is arguably the most frequently used utility designed to run Ansible playbooks. Playbooks are YAML files containing a series of instructions or plays that the automation engine executes. They can perform a wide range of tasks from software installation and update to complex multi-tier deployment and configuration management. The utility offers numerous options to tailor execution, including limiting the set of hosts, choosing specific tasks, and setting runtime variables.
*   ansible-inventory: The ansible-inventory utility manages inventory, which can be static or dynamic, allowing for introspection and manipulation. It is used to list, create, or modify inventory details, making it easier to manage the groups of hosts our playbooks target. This command is essential for understanding the current state of our inventory and for debugging complex inventory setups.
*   ansible-console: The ansible-console command provides an interactive Read-Eval-Print Loop (REPL) environment for running ad hoc Ansible commands. It is particularly useful for exploration and quick tasks, offering tab-completion and history features. This interactive shell allows users to execute commands on hosts in their inventory with immediate feedback, streamlining the process of ad hoc task execution.
*   ansible-connection: The ansible-connection command is slightly more specialized; it is used internally by Ansible to manage persistent connections to devices. While not commonly used directly by most users, it is crucial to understand how Ansible communicates with remote nodes, especially when troubleshooting connection issues or customizing connection behaviors.
*   ansible-config: Managing Ansible configurations is straightforward with the ansible-config utility. It allows users to view, edit, or create new Ansible configuration files. This is particularly helpful for tailoring Ansible's behavior to specific environments or requirements, such as adjusting timeout settings, specifying inventory paths, or enabling additional debugging output.
*   ansible-test: Ensuring our Ansible code is reliable and performs as expected is where ansible-test comes into play. This utility helps in testing Ansible roles and collections, providing a way to execute sanity, unit, integration, and other tests. It is an essential tool for development and continuous integration workflows, helping maintain high-quality Ansible content.
*   ansible-galaxy: The ansible-galaxy command is the gateway to sharing and reusing Ansible content. It allows users to install roles and collections from Ansible Galaxy, Ansible's official community hub for sharing Ansible roles and collections. This utility fosters collaboration and code reuse, making it easier to find, share, and incorporate community developed solutions into our projects.
*   ansible-vault: Security is a paramount concern in automation, and ansible-vault addresses this by encrypting sensitive data within Ansible projects. It can encrypt entire files, such as inventory files or specific variables, ensuring sensitive data like passwords or keys are securely managed. ansible-vault supports creating, editing, and viewing encrypted content, making it a vital tool for secure automation practices.
*   ansible-sign and ansible-verify: These utilities are part of Ansible's security mechanisms, allowing users to sign roles and verify their authenticity. Signing roles helps ensure the integrity and origin of Ansible content, providing an additional layer of security when distributing and consuming automation resources.

Ansible's suite of command line utilities equip developers and system administrators with a powerful set of tools for automating a wide range of IT tasks. From executing simple ad hoc commands with ansible to managing complex deployments with ansible-playbook, and securing sensitive data with ansible-vault, these utilities make Ansible a flexible and indispensable tool in modern IT environments.

[Ansible language](#contents.xhtml_sc2_135a)

In IT automation, Ansible has emerged as a game changer, offering powerful, simple, and efficient ways to automate a wide range of IT tasks. At the core of Ansible's automation capabilities are its playbooks, which serve as the blueprint for automating environments and processes.

Playbooks are essentially YAML files that define the tasks and processes Ansible will automate on remote hosts. They are the core component of Ansible's configuration management and multi-node deployment system. Each playbook contains one or more plays, which target a set of hosts to execute specific tasks in a clearly defined order.

The key features of Ansible playbooks are as follows:

*   Human-readable format: Playbooks are written in YAML, which is both easy to write and understand, even for those new to programming.
*   Task management: They define the tasks and the order in which they should be executed.
*   Variable integration: Playbooks can include variables to create more dynamic and reusable automation scripts.
*   Idempotency: Tasks in playbooks are idempotent, ensuring that the same outcome is achieved regardless of how many times the playbook runs.
*   Error handling: Playbooks can include error handling to ensure the automation process is not disrupted by unforeseen issues.

Creating an effective playbook involves understanding our automation objectives and translating them into a structured format.

Following is a basic outline:

*   Define hosts and groups: Specify which hosts or groups of hosts the playbook should run against.
*   Set variables: Define any necessary variables that will be used in our tasks.
*   List tasks: Outline each task that needs to be performed using Ansible modules where appropriate.
*   Error handling: Implement error handling strategies to manage any potential failures in tasks.

Consider the following example:

- name: Ensure web server is installed and running

hosts: web

become: true

tasks:

- name: Install web server

ansible.builtin.yum:

name: httpd

state: present

- name: Start Apache

ansible.builtin.service:

name: httpd

state: started

enabled: true

This example playbook is designed to automate the installation and starting of Apache on a group of web servers.

[Advanced playbook techniques](#contents.xhtml_sc3_136a)

As we grow more comfortable with basic playbooks, we might explore advanced techniques as follows:

*   Roles and includes: Break down complex playbooks into reusable roles or include other playbooks or tasks.
*   Templates and files: Use Jinja2 templates for dynamic configuration file generation.
*   Handlers: Manage services and processes in response to task outcomes.
*   Loops and conditional statements: Repeat tasks or execute them conditionally based on certain criteria.
*   Testing and deployment: Testing is a critical step in playbook implementation. Use Ansible's --check mode to run playbooks in a dry run mode, simulating changes without making them. Additionally, ansible-lint can be used to check for best practices and potential errors in playbooks.

Implementing playbooks in Ansible is a skill that can revolutionize how IT professionals manage and automate their infrastructure. With their easy-to-understand syntax and powerful capabilities, playbooks make automation accessible, scalable, and maintainable. Whether we are deploying applications, managing configurations, or automating network setups, mastering playbooks is an essential step towards efficient and error-free IT automation.

[Plays](#contents.xhtml_sc3_137a)

With its simple yet powerful automation engine, Ansible provides this capability through the concept of plays. A play in Ansible is a set of tasks intended to be run on specified hosts defined within a playbook. This approach enhances organization and readability and also amplifies the power of automation by allowing for targeted actions on various hosts.

In this section, let us explore the structured, versatile, and scalable concept of Ansible plays.

[The power of multiple plays](#contents.xhtml_sc4_138a)

Utilizing multiple plays within a single Ansible playbook facilitates a more organized, modular, and versatile automation strategy. This technique allows for the execution of differentiated tasks tailored to specific hosts or groups, all within the same playbook. For instance, consider a scenario where we need to manage web servers and database servers differently.

Following is how a multi-play playbook might look:

---

- name: First play

hosts: web

tasks:

- name: Apache installed

ansible.builtin.yum:

name: httpd

state: present

- name: Apache service enabled

ansible.builtin.service:

name: httpd

enabled: true

- name: Second play

hosts: database

tasks:

- name: MariaDB service enabled

ansible.builtin.service:

name: mariadb

enabled: true

In this multipleplays.yml example, the first play targets web servers to install and enable Apache, while the second play focuses on database servers, ensuring MariaDB service is enabled. This structured organization into distinct plays provides clarity and focus, making the playbook easy to understand and maintain.

[Structured organization and task execution](#contents.xhtml_sc4_139a)

Each play within the playbook is defined with a distinct name, target hosts, and a series of tasks, offering a clear overview of the playbook's purpose and scope as follows:

*   Web server play: Targets web.example.com, with tasks to install and enable the Apache service.
*   Database play: Focuses on database.example.com, with a single task to ensure the MariaDB service is enabled.

This level of organization ensures that tasks are executed precisely where they are needed, enhancing the playbook's efficiency and effectiveness.

The use of multiple plays within a playbook introduces unparalleled versatility and scalability into Ansible's automation capabilities, as follows:

*   Versatility: By defining distinct tasks for different hosts or groups, Ansible accommodates varied automation requirements within a single playbook. This flexibility allows for targeted configurations, installations, and updates across our infrastructure.
*   Scalability: As our automation requirements evolve, additional plays can seamlessly integrate into the playbook. This modular approach supports the growth of our infrastructure without compromising maintainability or readability.

Plays are a fundamental component of Ansible's automation prowess, enabling precise, organized, and efficient task execution across diverse hosts. By leveraging multiple plays within a playbook, we can orchestrate complex automation workflows that are both versatile and scalable, tailored to the unique demands of our infrastructure. Whether managing web servers, database servers, or a mix of different technologies, Ansible plays offer a structured path to achieving automation excellence.

[Variables](#contents.xhtml_sc3_140a)

Ansible variables are entities that store values, which can then be used throughout our Ansible playbooks. They can represent anything from strings, numbers, and lists, to more complex data structures like dictionaries.

In Ansible, variable names must conform to certain rules to be valid. These rules are primarily derived from the underlying Python variable naming conventions, as Ansible variables are directly mapped to Python variables during playbook execution.

Following is a table of examples illustrating invalid Ansible variable names and the reason why they are considered invalid:

| Invalid variable name | Reason for invalidity |
| --- | --- |
| 9variable | Cannot start with a number |
| variable-name | Hyphens are not allowed; use underscores (_) instead |
| variable name | Spaces are not allowed |
| variable.name | Dots are not allowed |
| import | Reserved words in Python cannot be used |
| def | Reserved words in Python cannot be used |
| variable(name) | Special characters like parentheses are not allowed |
| variable&name | Special characters like ampersands are not allowed |
| variable*name | Special characters like asterisks are not allowed |
| True | Boolean values True and False are reserved in Python and should not be used |
| None | None is a reserved word in Python and should not be used as a variable name |
| variable-name- with--doublehyphen | Double hyphens are not allowed; use single underscores (_) instead |

Table 4.1: Invalid variables names

Remember, valid variable names in Ansible and Python must start with a letter (a-z, A-Z) or an underscore (_), followed by letters, underscores, or digits (0-9). Avoid using reserved Python keywords and special characters to ensure our Ansible variables are valid and will not cause syntax or runtime errors.

Variables in Ansible can be defined in various places, including in inventory files, playbooks, included files, and roles. They can be used to parameterize tasks, templates, and roles, making our automation more dynamic and reusable.

Understanding different types of variables, how to declare them, and their priority in conflicts for effective variable management in Ansible, as follows:

*   Types of variables in Ansible
    *   Built-in variables (facts): Automatically discovered information about remote systems upon execution.
    *   User defined variables: Defined by the user in various places like playbooks, inventory, roles, etc.
    *   Special variables: Predefined by Ansible and have special meanings, such as inventory_hostname, which represents the current host Ansible is working on.
*   Declaring variables: Variables can be declared in several places, such as:
    *   Inventory file: Often used for variables specific to a host or group of hosts.
    *   Playbooks: At the play level, variables can be applied to tasks within that play.
    *   Roles: Within roles for encapsulation and reuse across different playbooks.
    *   Variable files: Separated YAML files, which can be loaded into playbooks or roles as needed.

        An example of declaring a variable in a playbook is as follows:

        ---

        - name: Configure web server

        hosts: all

        vars:

        http_port: 80

        max_clients: 200

        tasks:

        - name: Start a web server

        ansible.builtin.yum:

        name: httpd

        state: present

*   Variable precedence: Ansible resolves variables by considering their precedence. Variables with higher precedence override those with lower precedence. The order is roughly as follows, from lowest to highest precedence:
    *   Variables defined in inventory
    *   Variables defined in playbooks
    *   Variables passed on the command line
    *   Variables defined in roles
    *   Variables defined in blocks
*   Best practices
    *   Naming conventions: Use meaningful variable names and stick to a consistent naming convention to make our playbooks more readable.
    *   Scoping variables: Define variables at the appropriate scope (global, play, host, role) to avoid unexpected behaviors.
    *   Avoid hard coding: Use variables instead of hard-coded values, especially for data that might change (e.g., IP addresses, port numbers, file paths).
    *   Use facts sparingly: Gathering facts is powerful but can slow down playbook execution. Disable fact gathering if not needed or use the gather_subset option to limit gathered data.
    *   Variable documentation: Document the variables used in our playbooks and roles, especially if we are creating roles that will be used by others.

Variables are an integral part of Ansible's automation capabilities, providing the flexibility to tailor our automation to the unique characteristics of each system we manage. By understanding and effectively utilizing variables, along with Ansible's precedence rules and best practices, we can create more dynamic, efficient, and maintainable Ansible playbooks and roles. Variables allow users to abstract certain values and use them across playbooks, making scripts reusable and adaptable to different environments. Facts, which are gathered by Ansible from target systems, offer a dynamic inventory of system properties that can be utilized to tailor tasks to the specific characteristics of each host.

The transformational capabilities of Ansible are further enhanced by filters and plugins. Filters are used to manipulate data within templates, allowing complex data transformations and logical operations to be performed seamlessly. Plugins extend Ansible's functionality, covering a wide range of purposes from gathering additional facts to providing new filters, lookup capabilities, and more.

[Facts](#contents.xhtml_sc3_141a)

A pivotal aspect of Ansible's power lies in its handling of facts, a way to retrieve system information from the target hosts. Facts enable the use of the state or behavior of one system to influence configurations on other systems. Following is an example:

- name: Print all facts

hosts: all

gather_facts: true

tasks:

- name: Display all facts from the host

ansible.builtin.debug:

var: ansible_facts

In this example, the ansible.builtin.debug module is used to print all the facts collected about a host, which can then be utilized for various automation tasks across our infrastructure. We can decide to enable or disable facts acquisition setting the Boolean gather_facts, default true. A good practice is to disable fact gathering when is not needed for performance boost.

Ansible has established itself as an indispensable tool in the arsenal of IT professionals seeking to navigate the complexities of modern infrastructure with grace and efficiency. By combining ease of use with powerful capabilities for managing variables, facts, filters, and plugins, Ansible empowers organizations to automate their IT operations effectively, ensuring agility, reliability, and scalability. As we look to the future, the continued evolution and community driven enhancements of Ansible promise to keep it at the forefront of IT automation solutions.

[Filters](#contents.xhtml_sc3_142a)

Ansible filters are powerful tools that allow us to transform data inside our Ansible playbooks. They enable us to manipulate variables and their contents by passing them through filters and modifying them in a variety of ways. This section explores the concept of Ansible filters, common use cases, and how to effectively utilize them to streamline our automation tasks.

Filters in Ansible are Jinja2 expressions that work by taking a variable as input and transforming it into a different format or structure through a filtering process. They are applied using the pipe symbol (|) followed by the filter name. Filters can perform tasks such as formatting data, performing mathematical calculations, working with IP addresses, manipulating text, and more, as follows:

*   Common use cases:
    *   Formatting dates: Convert UNIX timestamps into human-readable date formats.
    *   Data transformation: Change the structure or format of data to match a required output.
    *   Mathematical operations: Perform calculations on variables, such as addition, subtraction, or generating hashes.
    *   Working with strings: Manipulate strings by capitalizing, replacing text, converting to JSON or YAML, etc.
    *   List operations: Filter, map, or reduce lists to get specific outputs.
    *   Network data manipulation: Manipulate IP addresses and subnets for network configuration.
*   Examples of Ansible filters:
    *   Formatting dates:

        - name: Display the current date in a specific format

        ansible.builtin.debug:

        msg: "{{ ansible_date_time.epoch | timestamp_custom('%Y-%m-%d %H:%M:%S') }}"

    *   Converting a list into a comma-separated string:

        vars:

        list_variable: ['item1', 'item2', 'item3']

        tasks:

        - name: Convert list to a comma-separated string

        debug:

        msg: "{{ list_variable | join(',') }}"

    *   Calculating the hash of a string:

        vars:

        password: 'secretPassword'

        tasks:

        - name: Output the SHA256 hash of the password

        debug:

        msg: "{{ password | hash('sha256') }}"

    *   Filtering a list of dictionaries:

        vars:

        users:

        - name: John

        age: 25

        - name: Jane

        age: 22

        - name: Doe

        age: 30

        tasks:

        - name: Get names of users who are 25 or older

        debug:

        msg: "{{ users | selectattr('age', '>=', 25) | map(attribute='name') | list }}"

*   Best practices:
    *   Understand the input and output: Knowing what data type we are working with and what we want to achieve helps select the right filter.
    *   Chain filters sparingly: While it is possible to chain multiple filters, doing so can make our playbook harder to read and debug. Use this feature judiciously.
    *   Custom filters: For complex data transformations not covered by existing filters, consider writing custom filters in Python. This requires a deeper understanding of Ansible and Python but offers unlimited flexibility.
    *   Documentation: Refer to Ansible's and Jinja2's official documentation to explore the full range of available filters and their usage.

Ansible filters are a versatile feature that can significantly enhance the functionality and readability of our playbooks by allowing us to perform complex data manipulations inline. By mastering filters, we can simplify our tasks, avoid unnecessary use of additional tasks or modules for data transformation, and make our playbooks more efficient and easier to maintain.

[Retrieve results](#contents.xhtml_sc3_143a)

Using variables to retrieve the results of running commands in Ansible is a powerful technique for capturing and utilizing the output of tasks within our playbooks. By employing the register keyword, we can store the outcome of a command execution in a variable, which then can be used in subsequent tasks for conditional execution, debugging, or any other purpose that requires access to task output.

[Capturing command output](#contents.xhtml_sc4_144a)

To capture the output of a command, we use the command module along with the register keyword to store the command's output in a variable. This variable holds a dictionary with several keys, including stdout for standard output, stderr for standard error, and rc for the return code of the command.

Example: Capturing whoami command output

- name: Capture output of whoami command

ansible.builtin.command: whoami

register: login

In this example, the output of the whoami command is registered to the variable named login. We can then use this variable in subsequent tasks to access the command's output.

[Using registered variable](#contents.xhtml_sc4_145a)

Once a variable is registered, we can access its contents using the variable's name and the keys within the dictionary. For instance, to display the standard output of the command we captured earlier, we can use the debug module.

Example: Displaying the registered variable

- name: Print the login variable

ansible.builtin.debug:

var: login

This task would display the entire dictionary stored in login, including the command's output, return code, and any errors.

For a more targeted approach, especially if we are only interested in the command's output, we can reference the stdout key directly:

- name: Print the login variable

ansible.builtin.debug:

msg: “Logged in as user {{ login.stdout }}”

This task constructs a message that incorporates the standard output of the whoami command, effectively displaying the logged-in user's name.

[Practical use cases](#contents.xhtml_sc4_146a)

Capturing the output of commands and using it in subsequent tasks enables a wide range of practical applications, as follows:

*   Conditional execution: Execute certain tasks based on the output of a previous command.
*   Debugging: Display the output of commands for troubleshooting purposes.
*   Dynamic configuration: Use the command output to configure other tasks or templates dynamically.

By leveraging Ansible's ability to register variables and utilize command output, we can significantly enhance the flexibility and intelligence of our automation workflows.

[Loops](#contents.xhtml_sc3_147a)

Loops allow us to repeat a task over a list or range of items. This feature is invaluable when applying a consistent set of operations across multiple elements, such as installing packages, creating users, or managing services on several hosts. By incorporating loops into our playbooks, we can significantly reduce code redundancy, enhance playbook readability, and ensure consistent task execution across our infrastructure.

[LAMP example](#contents.xhtml_sc4_148a)

Linux, Apache, MySQL, and PHP/Perl/Python (LAMP) is considered a scenario where we need to ensure that multiple services, such as httpd (Apache) web server and MariaDB or MySQL, are running on our servers. Instead of writing separate tasks for each service, we can use a loop to streamline our playbook. Following is a simplified example demonstrating how to use loops to check and ensure services are running:

---

- name: Ensure critical services are running

hosts: all

tasks:

- name: Ensure services are started

ansible.builtin.service:

name: "{{ item }}"

state: started

loop:

- httpd

- mariadb

In this example, the loop iterates over the list of services defined under the loop directive. For each item in the list (httpd and mariadb), the task uses the ansible.builtin.service module to ensure the service is in the started state. The {{ item }} placeholder represents the current item in the loop, dynamically changing with each iteration to reflect the service being managed.

[Execution and output](#contents.xhtml_sc4_149a)

When executed, this playbook gathers facts and then proceeds to ensure each specified service is running. If a service is not running, Ansible starts it; if it is already running, owing to its idempotent nature, Ansible moves to the next item without making changes. The output will indicate the task's result for each service, providing clear feedback on the actions performed.

Ansible loops offer a robust mechanism to automate repetitive tasks efficiently, reducing the potential for errors and code duplication. By understanding and utilizing loops, we can enhance our playbooks' effectiveness, ensuring consistent and reliable automation across our IT environment. Whether managing services, users, packages, or configurations, Ansible loops are an indispensable tool in the arsenal of any IT professional aiming for streamlined operations and automation excellence.

[Conditional](#contents.xhtml_sc3_150a)

Conditionals, particularly the when statement, are indispensable for creating responsive and intelligent automation with Ansible. By conditionally executing tasks, we can ensure that our playbooks are not only more efficient but also more adaptable to the diverse needs of our infrastructure.

[when statement](#contents.xhtml_sc4_151a)

The primary method for implementing conditionals in Ansible is through the when statement. This powerful feature allows tasks to be conditionally executed, enhancing playbook flexibility and ensuring tasks are only run when necessary. Conditions within the when statement utilize Jinja2 tests and filters to evaluate whether a task should proceed.

Example: Basic conditional execution

Consider a scenario with a variable named configure_nginx that dictates whether NGINX should be reloaded. The execution of the task to reload NGINX can be conditionally controlled based on the truth value of configure_nginx.

- name: Conditional execution example

hosts: all

vars:

configure_nginx: false

tasks:

- name: Reload nginx

ansible.builtin.service:

name: nginx

state: reloaded

when: configure_nginx

In this example, the task to reload NGINX will only execute if configure_nginx is set to true. If configure_nginx is false, as shown above, the task will be skipped.

[Conditional execution based on variable values](#contents.xhtml_sc4_152a)

The power of the when statement is further illustrated when toggling the configure_nginx variable's value:

- name: Basic conditional

hosts: all

vars:

configure_nginx: true

tasks:

- name: Reload nginx

ansible.builtin.service:

name: nginx

state: reloaded

when: configure_nginx

With configure_nginx set to true, the task to reload NGINX will execute, demonstrating how easily playbook behavior can be altered through conditionals based on variable values.

[Handlers](#contents.xhtml_sc3_153a)

Ansible handlers are a powerful feature that allows us to trigger tasks based on the outcome of other tasks. They are particularly useful for managing services and applications that need to be restarted or reloaded when configurations change. In this section, we will explore what Ansible handlers are, how they work, and provide examples to demonstrate their utility in infrastructure automation, as follows:

*   Understanding Ansible handlers: At its core, an Ansible handler is a specific type of task that only runs when it is notified by another task. This notification mechanism is conditional, based on whether the notifying task makes changes to the system. Handlers are defined using the same syntax as tasks but are placed under a separate section called handlers in our Ansible playbook.
*   Using handlers: Handlers are ideal for scenarios where we do not want to restart or reload a service unnecessarily. For example, if we have a task that updates a configuration file, we might only want to restart the associated service if the file actually changes. Handlers ensure that these service management tasks are only executed when necessary, making our automation more efficient and reducing the potential for service disruption.
*   Working of handlers:
    *   Notification: A task triggers (notifies) a handler by including a notify directive with the name of the handler. This directive is only activated if the task results in a change. For instance, modifying a configuration file or installing a new package.
    *   Idempotency: Handlers maintain Ansible's idempotent nature, running only when needed and not affecting the system's state if there are no changes.
    *   Order of execution: Handlers are run after all the tasks in a playbook have been completed, not immediately after the notifying task. If multiple tasks notify the same handler, or if one task notifies multiple handlers, Ansible ensures each handler is run only once at the end of the playbook.

[Defining and using handlers](#contents.xhtml_sc4_154a)

Following is a simple example to illustrate how handlers are defined and used within an Ansible playbook:

---

- name: Example playbook with handlers

hosts: web_servers

tasks:

- name: Update web server configuration

ansible.builin.template:

src: templates/nginx.conf.j2

dest: /etc/nginx/nginx.conf

notify: Restart nginx

handlers:

- name: Restart nginx

service:

name: nginx

state: restarted

In this example, a task uses the template module to update the NGINX configuration file. If the task results in a change to the file (for instance, if the template contents have been updated since the last run), it notifies the Restart nginx handler. The handler is defined under the handlers section, then restarts the NGINX service.

[Multiple handlers](#contents.xhtml_sc4_155a)

Multiple handlers can be triggered by a single task or multiple tasks within a playbook. Handlers are executed at the end of a playbook's execution in the order they were notified, but each handler is run only once, even if notified multiple times.

Following is how you can trigger multiple handlers in an Ansible playbook:

Define the handlers in the handlers section of your playbook. Use the notify directive in your tasks to trigger the handler(s).

The following example playbook shows how to trigger multiple handlers:

---

- name: Example playbook to trigger multiple handlers

hosts: all

become: true

tasks:

- name: Install nginx

ansible.builtin.yum:

name: nginx

state: latest

notify:

- Start nginx

- Enable nginx

- name: Update nginx configuration

ansible.builtin.copy:

src: /path/to/new/nginx.conf

dest: /etc/nginx/nginx.conf

owner: root

group: root

mode: '0644'

notify:

- Reload nginx

handlers:

- name: Start nginx

ansible.builtin.service:

name: nginx

state: started

- name: Enable nginx

ansible.builtin.service:

name: nginx

enabled: yes

- name: Reload nginx

ansible.builtin.service:

name: nginx

state: reloaded

The best practices of handlers are as follows:

*   Descriptive handler names: Use clear and descriptive names for our handlers to make our playbooks easier to understand and maintain.
*   Use handlers sparingly: While handlers are useful, they should be used judiciously. Overusing handlers can make our playbooks harder to debug and understand.
*   Handler granularity: Design our handlers to be as granular as possible. A monolithic handler that restarts multiple services, for example, is less efficient and more disruptive than separate handlers for each service.

Ansible handlers are a sophisticated feature that, when used correctly, can significantly enhance the efficiency and reliability of our automation tasks. They provide a smart way to manage service state changes in response to configuration updates, ensuring that services are only restarted or reloaded when absolutely necessary. By integrating handlers into our Ansible playbooks, we can achieve more refined control over our managed environments, making our infrastructure automation both powerful and precise.

[Conditional tasks](#contents.xhtml_sc3_156a)

Conditional tasks in Ansible are tasks that are executed only when certain conditions are met. These conditions can be based on the values of variables, facts gathered from target systems, or the outcomes of previous tasks. By employing conditional statements, Ansible playbooks can make intelligent decisions, executing tasks only when it is necessary or beneficial to do so. This capability significantly enhances playbook efficiency and flexibility, ensuring that operations are performed in a context sensitive manner.

The primary mechanism for implementing conditionals in Ansible is the when statement. This statement evaluates a condition or a series of conditions and determines whether the subsequent task should be executed. Conditions are expressed using the Jinja2 templating language, which provides a rich set of tests and filters to evaluate variables and facts.

[Practical example of conditional task execution](#contents.xhtml_sc4_157a)

Consider a scenario where we need to deploy a web application on a fleet of servers. The application requires a specific version of a software package to be installed, but we want to minimize disruptions by avoiding unnecessary package updates on servers that already have the correct version. This is where conditional tasks come into play.

Consider the following example:

---

- name: Ensure specific package version is installed

hosts: all

tasks:

- name: Check if the required package version is installed

ansible.builtin.command: rpm -qa bash | grep -e '5.2.26'

register: package_check

ignore_errors: true

- name: Install the required package version

ansible.builtin.dnf:

name: apache=5.2.26

state: present

when: package_check.rc != 0

In this playbook:

The first task uses the ansible.builtin.command module to check if the required version of the package is already installed, registering the result in the package_check variable. The task is configured to ignore errors, which ensures the playbook continues executing even if the package is not found.

The second task is responsible for installing the specified version of the package. However, it is only executed if the when condition is met, i.e., the return code (rc) of the first task indicates that the package version was not found on the system (package_check.rc != 0).

Conditional tasks offer several key benefits, as follows:

*   Efficiency: By executing tasks only when needed, Ansible can reduce runtime and avoid unnecessary changes to the system, preserving its stability.
*   Flexibility: Conditionals allow a single playbook to handle a wide range of scenarios, adapting its behavior based on the state of the target systems or external inputs.
*   Idempotency: Ensuring that playbooks are idempotent, meaning they can be run multiple times without causing unintended effects, is easier with conditional tasks. They help prevent actions that would alter the system state unnecessarily.

Conditional tasks are a powerful feature in Ansible that significantly enhances the intelligence and adaptability of automation workflows. By making decisions based on dynamic conditions, Ansible playbooks can manage complex deployments and configurations with ease, ensuring that operations are performed efficiently and appropriately according to the context. Whether we are a seasoned system administrator or new to DevOps, mastering conditional tasks in Ansible is a valuable skill that will help us leverage the full potential of automation in our IT environment.

[Handling task failure](#contents.xhtml_sc3_158a)

The ignore_errors directive in Ansible is a double-edged sword. While it allows a playbook to continue execution even after a task fails, its overuse or misuse can obscure critical failures, leading to unintended consequences and potentially masking significant issues within our infrastructure. The directive should be employed judiciously, with a clear understanding of its implications.

The practical strategies for error handling is as follows:

*   Selective use of  ignore_errors: Instead of a blanket application, ignore_errors should be used selectively, where the failure of a specific task does not critically impact the overall success of the playbook. This approach maintains the playbook's resilience while ensuring that only non-critical errors are overlooked. Following is an example:

    - name: Run dnf update

    ansible.builtin.command: dnf update

    ignore_errors: true

*   Using  ansible_check_mode  for conditional ignoring: A more nuanced approach involves using ignore_errors in conjunction with ansible_check_mode. This allows errors to be ignored only during playbook checks, enabling a safer evaluation of potential issues without executing changes. Following is an example:

    - name: Run dnf update in check mode

    ansible.builtin.command: dnf update

    ignore_errors: "{{ ansible_check_mode }}"

*   Registering errors for later evaluation: By using the register directive along with ignore_errors, we can capture the output of tasks, including any errors or failures. This information can be analyzed later to understand the nature of the errors and decide on the appropriate corrective actions. Following is an example:

    - name: Run dnf update and register output

    ansible.builtin.command: dnf update

    ignore_errors: true

    register: ignore_errors_register

*   Defining specific conditions with failed_when: For more granular control over what constitutes a failure, failed_when can be used to define specific conditions. This approach allows for the precise handling of errors, ensuring that only certain conditions are treated as failures, thus avoiding unintended playbook execution. Following is an example:

    - name: Disable apport

    become: true

    ansible.builtin.lineinfile:

    line: "enabled=0"

    dest: /etc/default/apport

    mode: 0644

    state: present

    register: default_apport

    failed_when: default_apport.rc != 0 and not default_apport.rc == 257

The best practices for error management are as follows:

*   Selective application: Use ignore_errors selectively, focusing on tasks where failure does not impact overall playbook execution.
*   Error evaluation: Utilize register to capture task outputs for later evaluation, enabling controlled and predictable error handling.
*   Condition definition: Employ failed_when to specify precise error conditions, providing fine-grained control over playbook execution.
*   Check mode consideration: Leverage ansible_check_mode to ignore errors conditionally, enhancing playbook testing without risking actual execution.
*   Continuous review: Regularly review and update our playbooks and error-handling strategies to adapt to changing infrastructure and requirements.

Effective error handling is crucial in Ansible automation, ensuring tasks are executed reliably and infrastructure is managed effectively. By adopting these strategies, we can enhance the robustness of our automation workflows, ensuring they are resilient in the face of errors and maintaining the integrity of our IT environment.

[Creating Ansible plays and playbooks](#contents.xhtml_sc2_159a)

Creating Ansible plays and playbooks is an essential skill for automating various IT infrastructure tasks. Ansible plays are ordered sets of tasks executed against selected hosts in our inventory, designed to configure systems, deploy software, and orchestrate more complex IT processes. A playbook is a file containing one or more plays, offering a blueprint for automation across our network.

An Ansible play is a collection of tasks that are run sequentially on a set of hosts from our inventory. Each play specifies the host or group of hosts to target and a list of tasks to be executed. Plays enable us to group related tasks together, making our automation more organized and manageable.

[Crafting our first playbook](#contents.xhtml_sc3_160a)

A playbook is a YAML file that Ansible interprets to apply configurations, deploy applications, or orchestrate steps in a workflow across different systems.

Following is an example of a playbook containing a single play:

---

- name: Apache Web Server installed and running

hosts: web

tasks:

- name: Apache installed

ansible.builtin.yum:

name: httpd

state: present

- name: Apache running

ansible.builtin.service:

name: httpd

state: started

enabled: true

In this playbook:

*   hosts: Specifies the group of hosts (web) the play targets.
*   tasks: Lists the actions the play performs on the targeted hosts. In this example, it installs Apache using the yum module and ensures the Apache service is started and enabled to start on boot.

The best practices for playbook creation includes the following:

*   Use descriptive names: Naming plays and tasks descriptively makes our playbooks easier to understand and maintain.
*   Modular design: Break down complex procedures into multiple plays within a playbook or separate them into different playbooks to enhance readability and reusability.
*   Version control: Store our playbooks in a version control system to track changes and collaborate with others.
*   Idempotency: Write tasks in a way that they can be safely run multiple times without changing the system's state beyond the desired outcome.
*   Error handling: Implement error handling and use conditions to make our playbooks robust and fault-tolerant.

By following these guidelines and using the example provided as a template, we can start building our own Ansible plays and playbooks to automate tasks across our IT environment, enhancing efficiency and reliability.

[Error handling](#contents.xhtml_sc3_161a)

Configuring error handling in Ansible is crucial for creating resilient and fault-tolerant automation workflows. Ansible offers several mechanisms to manage task failures effectively, ensuring our playbooks can handle errors gracefully and execute recovery or cleanup tasks as needed.

[Blocks, rescue, and always](#contents.xhtml_sc4_162a)

Ansible allows us to group tasks using blocks, and within these blocks, we can specify rescue and always sections to manage errors. This structure is akin to try-catch-finally in many programming languages, as follows:

*   block: Defines the main tasks to be executed.
*   rescue: Specifies tasks that should run if any task within the block fails.
*   always: Contains tasks that will run regardless of the success or failure of tasks in the block.

Consider the following example:

- name: Demonstrating error handling

hosts: all

tasks:

- block:

- name: Attempt to execute a task

ansible.builtin.command: /path/to/successful/command

- name: Another task that depends on the success of the previous task

ansible.builtin.command: /path/to/another/successful/command

rescue:

- name: This task runs if any task in the block fails

ansible.builtin.command: /path/to/rescue/command

always:

- name: This task always runs, regardless of previous successes or failures

ansible.builtin.debug:

msg: "This is the cleanup or logging task."

In this example:

*   The tasks under block are attempted first. If both commands execute successfully, Ansible will move on to the always section.
*   If any task in the block fails, Ansible will not execute the remaining tasks in the block but will move to the rescue section to execute those tasks.
*   After executing the rescue section (if needed) or if there were no failures in the block, Ansible will execute the tasks in the always section.

This structure is particularly useful for complex deployments or updates, where we need to ensure that either all tasks are completed successfully or appropriate remediation is performed in the case of failures, with cleanup actions or logging occurring in every case as follows:

*   Handling unreachable hosts: Ansible 2.7 introduced the ignore_unreachable keyword, which allows us to ignore failures caused by unreachable hosts. This can be useful in scenarios where we want the playbook to continue running tasks on other hosts, even if some are unreachable.
*   Using ignore_errors: The ignore_errors directive can be used to continue execution despite failures. This is particularly useful when a task is expected to fail under certain conditions or when we want to handle failures manually without stopping the playbook execution.

[Advanced error handling strategy](#contents.xhtml_sc4_163a)

For a more complex and real-world example, Red Hat's Enable Sysadmin provides a playbook that illustrates advanced error handling with block, rescue, and always sections. This playbook includes roles and tasks within a main block and uses the rescue section to accumulate failures. The always section collects and classifies the results, allowing for detailed reporting on the task outcomes across all nodes. This approach ensures a comprehensive error-handling strategy, enabling not only error recovery but also detailed status reporting.

By leveraging these error-handling features, we can make our Ansible playbooks more robust and adaptable to various failure scenarios, enhancing the reliability of our automation efforts. For more detailed information and examples, refer to the Ansible documentation on blocks and error handling in playbooks.

[Testing a playbook](#contents.xhtml_sc3_164a)

Testing a playbook often involves verifying that the desired state defined in the playbook is achieved on the target hosts. This can be done through assertions or even by designing a secondary playbook that checks the outcomes of the first. To illustrate, consider having a playbook that installs and starts a web server. To test this playbook, you could write a secondary playbook that makes a request to the web server or checks that the service is running on the target host.

Following is a simple example:

*   Primary playbook (webserver-setup.yml): This playbook installs and starts Apache on a target host.

    ---

    - name: Install and start Apache

    hosts: web_servers

    become: true

    tasks:

    - name: Install Apache

    ansible.builtin.yum:

    name: httpd

    state: present

    - name: Start Apache

    ansible.builtin.service:

    name: httpd

    state: started

    notify: restart apache

    handlers:

    - name: restart apache

    ansible.builtin.service:

    name: httpd

    state: restarted

*   Test playbook (test-webserver.yml): This playbook checks if Apache is installed and running.

    ---

    - name: Test Apache Installation and Running Status

    hosts: web_servers

    become: true

    gather_facts: false

    tasks:

    - name: Check if Apache is installed

    ansible.builtin.command: rpm -q httpd

    register: rpm_query

    failed_when: rpm_query.rc != 0

    - name: Ensure Apache is running

    ansible.builtin.service:

    name: httpd

    state: started

    register: apache_status

    failed_when: apache_status.state != "running"

To run the test playbook after the primary playbook, you would execute:

ansible-playbook webserver-setup.yml -i inventory_file

ansible-playbook test-webserver.yml -i inventory_file

This approach allows you to verify the effects of your primary playbook through a secondary, testing-focused playbook. Adjust the tasks according to what exactly you need to test in your environment.

[Configuration management](#contents.xhtml_sc3_165a)

Creating Ansible playbooks to configure systems to a specified state involves defining desired states for our systems and using Ansible's idempotent modules to achieve those states. This process ensures that no matter the initial state of the system, the playbook can bring it to the desired configuration without unintended side effects.

Following is a complete overview with examples to guide us in crafting such playbooks:

*   Structuring our playbook: An Ansible playbook is a YAML file containing a list of plays, each targeting one or more hosts and defining the tasks to be performed on those hosts.

    Following is a basic structure:

    ---

    - name: Configure Web Servers

    hosts: webservers

    become: true

    tasks:

    - name: Install nginx

    ansible.builtin.yum:

    name: nginx

    state: present

    - name: Start nginx service

    ansible.builtin.service:

    name: nginx

    state: started

    enabled: true

*   Key components

    *   hosts: Specifies the target hosts for the play. Use group names from our inventory, or all for all hosts.
    *   become: Elevates privileges, necessary for tasks requiring admin rights.
    *   tasks: Lists the tasks to be performed, invoking Ansible modules.

    Example: Applying security patches

    Regular application of security patches is vital for system integrity. Consider the following example playbook for Red Hat compatible systems using the yum module with a focus on security updates:

    ---

    - name: Apply security updates

    hosts: all

    become: true

    tasks:

    - name: Ensure all packages are updated with security patches

    ansible.builtin.yum:

    name: "*"

    state: latest

    security: true

    This playbook targets all hosts, escalates privileges, and ensures that all installed packages are updated with available security patches.

    Example: Configuring network interfaces

    For network configuration tasks, such as setting up VLANs on Cisco devices, Ansible modules tailored to network automation can be utilized. Take a look at this simplified example:

    ---

    - name: Configure VLANs on Cisco switches

    hosts: switches

    gather_facts: false

    tasks:

    - name: Ensure VLANs are present

    cisco.nxos.nxos_vlans:

    vlan_id: "{{ vlan_id }}"

    name: "{{ vlan_name }}"

    This playbook would target hosts grouped under switches, skipping the gathering of facts to speed up execution and configure VLANs based on provided variables vlan_id and vlan_name.

*   Best practices
    *   Idempotency: Write tasks so they can safely be run multiple times without changing the system state beyond the desired outcome.
    *   Variable  use: Utilize variables for values that might change between environments or over time, such as package names, versions, or network configurations.
    *   Error handling: Include error handling using block, rescue, and always structures to manage failures gracefully.
    *   Task modularization: Break down complex configurations into smaller tasks and use roles for reusability across different playbooks.

By following these guidelines and utilizing Ansible's extensive module library, we can efficiently develop playbooks that ensure our systems are configured precisely as needed, maintaining consistency and reliability across our infrastructure.

[Conclusion](#contents.xhtml_sc2_166a)

This chapter was designed to be an invaluable resource for those seeking to elevate their Linux system administration skills through automation, specifically using Ansible. It is a vital steppingstone toward RHCE certification.

The next chapter focuses on leveraging Ansible’s modules and code reuse with roles and collections to automate IT operations. Learn about the installation and configuration of Ansible, managing Linux and Windows nodes, and utilizing Ansible vault for secure automation, the Ansible Navigator tool, and the enterprise Ansible Automation Platform to set the foundation for more advanced automation strategies.

[Points to remember](#contents.xhtml_sc2_167a)

*   Idempotency: Ensure that tasks in Ansible are written to be idempotent, meaning they can be run multiple times without causing unintended changes to the system state. This helps maintain consistency across environments.
*   Variable management: Use variables effectively across playbooks and roles. Define variables at the appropriate scope and follow naming conventions to avoid conflicts and improve readability.
*   Error handling: Implement robust error handling using blocks, rescue, and always sections. This approach ensures that errors are managed gracefully, allowing for recovery actions and maintaining playbook execution flow.
*   Modular playbook design: Break down complex configurations into smaller, reusable tasks and roles. This modular approach improves playbook maintainability and allows for better organization.
*   Use of loops and conditionals: Leverage loops to iterate over items, reduce code redundancy and employ conditionals (using the when statement) to execute tasks only when certain conditions are met, enhancing playbook efficiency and flexibility.
*   Handler utilization: Handlers should be used sparingly and designed to be as granular as possible, ensuring services are only restarted or reloaded when necessary, thereby minimizing disruptions.

[Multiple choice questions](#contents.xhtml_sc2_168a)

1.  How can we execute simple tasks against a set of hosts?
    1.  Ansible ad hoc
    2.  Ansible playbook
    3.  Ansible inventory
    4.  Ansible conditional
2.  What is the preferred way to connect to a Windows target?
    1.  OpenSSH
    2.  Python Paramiko
    3.  WinRM
    4.  Remote desktop
3.  What statement save the result of an execution to a variable in Ansible?
    1.  vars
    2.  register
    3.  when
    4.  notify
4.  How can we implement a try-catch-finally block?
    1.  ignore_errors
    2.  ansible_check_mode
    3.  failed_when
    4.  blocks-rescue-always

[Answers](#contents.xhtml_sc3_169a)

1\. a

2\. c

3\. b

4\. d

[Questions](#contents.xhtml_sc2_170a)

1.  How can we increase the debug information printed during Ansible playbook execution?
2.  What variable names are not allowed in Ansible?
3.  What is the easiest way to test a playbook?
4.  How can we implement error handling in Ansible?

[Key terms](#contents.xhtml_sc2_171a)

*   WinRM:  This protocol is used for remote management of Windows servers and desktops, enabling secure communication and command execution.
*   Agentless: In Ansible, agentless refers to its ability to manage remote systems without needing to install any additional software on them.
*   Controller node: It is the central machine where Ansible is installed and from which it orchestrates automation tasks on other systems.
*   Target nodes: Also known as managed nodes, they are the remote systems that Ansible configures and manages from the controller node.
*   Idempotency: This ensures that running the same playbook multiple times on managed nodes results in the same state, avoiding unintended changes.
*   Ansible playbook: YAML files that describe the desired state of our systems using Ansible tasks.
*   Module: A discrete unit of code in Ansible that is invoked by a playbook task.
*   Inventory: A collection of hosts and groups in Ansible, where configuration tasks are performed.
*   Task: A block that defines a single procedure to be executed, e.g., installing a package.
*   Role: A way of bundling automation content and making it reusable.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 5Ansible Enterprise](#contents.xhtml_ch05a)

[Introduction](#contents.xhtml_sc2_172a)

In this chapter, we will learn the most used Ansible modules and techniques to apply Ansible in every organization and how to leverage code reuse of Ansible content such as roles and collections to propel the automation of our business.

[Structure](#contents.xhtml_sc2_173a)

The chapter covers the following topics:

*   Ansible installation
*   Ansible navigator
*   Ansible for Linux
*   Ansible vault
*   Configuration files
*   Roles
*   Collections
*   Tests
*   Ansible Automation Platform

[Objectives](#contents.xhtml_sc2_174a)

This chapter provides a comprehensive guide to effectively utilize Ansible for IT automation in the organization moving forward from foundational concepts to advanced techniques. Readers will gain practical skills in setting up, configuring and managing IT infrastructures with Ansible. This includes understanding how to install and configure the Ansible control node, manage Ansible managed nodes, execute playbooks using automation content navigator, manage automation content and implement security measures with Ansible vault. This chapter equips us with the knowledge required to automate standard RHCSA tasks, coordinate rolling updates and understand the full capabilities of the RHCSA.

[Ansible installation](#contents.xhtml_sc2_175a)

The installation of Ansible is super smooth in the controller node as the ansible-core package is included directly in RHEL. On the target node, it is not necessary to install any agent or software like that as it uses the SSH or WinRM connection.

[Control node](#contents.xhtml_sc3_176a)

The Ansible control node is the machine where Ansible is installed and from which all tasks and playbooks will be run. It is essential that the control node has network access to all managed nodes (hosts) for SSH and WinRM communication.

To set up the control node, follow these steps:

1.  Install required packages:
    1.  On a Linux based system: We can install Ansible using our distribution's package manager. For instance, on RHEL, we can use dnf command as follows:

        dnf install ansible-core

        As the package is part of the RHEL Application Stream (AppStream) repository, it is supported throughout the RHEL lifecycle. Like any other package in the distribution, we can check if an update is available (check-update), inspect for more information (info) or upgrade to the latest version using (upgrade), as follows:

        dnf upgrade ansible-core

    2.  On a macOS based system: The Homebrew^([1](#ch05.xhtml_footnote-002)) package manager is the preferred way to install and maintain up-to-date Ansible. We can install the ansible-core or the full ansible community package using the brew command, as follows:

        brew install ansible

    3.  On a Windows system: While Ansible is not directly supported on Windows, we can use the Windows Subsystem for Linux (WSL) to install a Linux distribution and then follow the Linux installation step.
    4.  Using Python package manager (pip): we can retrieve the latest Ansible version using pip. We can use pip command, as follows:

        pip install ansible-core

    | Please note that some Linux distributions require the additional python-pip or python3-pip package. The pip command might have variants such as pip3 for Python 3 or pip3.12 for a specific version. |

2.  Create a static host inventory file:

    The inventory file contains information about the hosts we want to manage. Create a file named inventory in a simple text INI format, short for initialization, in our project directory. Inside the file we can add our hosts under respective groups, as follows:

    [webservers]

    webserver1.example.com

    webserver2.example.com

    [dbservers]

    dbserver1.example.com

    This structure allows us to organize our hosts into groups for targeted automation tasks. With our inventory file set up, we can start running ad hoc commands or playbooks against group(s) of hosts or individual hosts. For example, to ping the hosts in the webservers group, we would use the following:

    ansible webservers -m ping

    This command checks the connection and responsiveness of our web servers.

3.  Create a configuration file, optional:

    Ansible looks for a configuration file in several locations and the first one is found to be used. The default location is /etc/ansible/ansible.cfg. We can create our custom ansible.cfg in our project directory to override default settings. Essential configurations to include are as follows:

    [defaults]

    inventory = ./inventory

    remote_user = ansibleuser

    host_key_checking = False

    This configuration specifies the inventory file location and the default remote user and disables SSH host key checking for new hosts.

[Best practices and tips](#contents.xhtml_sc4_177a)

Following are some best practices and tips to enhance efficiency and security when working with Ansible:

*   Version control: Keep our inventory files, configuration and playbooks under version control to track changes and collaborate with our team.
*   Custom modules and plugins: Explore Ansible's vast ecosystem of modules and plugins to extend its capabilities that fit our needs.
*   Security: Use Ansible vault to encrypt sensitive data like passwords or secret keys within our playbooks or inventory files.

[Linux managed nodes](#contents.xhtml_sc3_178a)

Configuring Ansible managed nodes is a crucial step in setting up our IT infrastructure for automation. This section of the chapter delves into essential tasks such as establishing secure communication with SSH keys, setting up privilege escalation, deploying files and converting shell scripts into Ansible playbooks. Each of these tasks is aimed at ensuring that our managed nodes are correctly configured to execute automated tasks efficiently and securely.

Configuring Linux managed nodes is a critical step in establishing a secure and efficient environment for automation. Following are the key tasks that should be completed to ensure proper communication and setup between the Ansible control node and the managed nodes:

1.  Generate SSH keys: On the Ansible control node, generate a new SSH key pair with the ssh-keygen command if we have not already done so. Keep the passphrase empty, if the key will be used for automated tasks.

    ssh-keygen -t rsa -b 4096

2.  Copy SSH public key: Use the ssh-copy-id command to copy the public SSH key to each managed node. This step requires the password of the remote user’s account and enables password less SSH access.

    ssh-copy-id user@managed_node_address

[Configuring privilege escalation on managed nodes](#contents.xhtml_sc3_179a)

Configuring privilege escalation on managed nodes is an essential step in enabling Ansible to execute administrative tasks without manual intervention. Follow these steps to ensure the correct privilege settings are in place:

1.  Edit sudoers file: Use the visudo command on managed nodes to edit the sudoers file safely. This step is crucial for specifying which users can escalate privileges and under what conditions, as follows:

    Visudo

2.  Configure sudo without password: Add a line to allow the Ansible user (or whichever user our control node uses) to execute sudo commands without a password prompt.

    ansible ALL=(ALL) NOPASSWD: ALL

[Deploying files to managed nodes](#contents.xhtml_sc3_180a)

Use Ansible’s copy module to deploy files from the control node to managed nodes. The following example playbook copies a configuration file to a specific directory on the managed node:

---

- name: Deploy Configuration File

hosts: all

tasks:

- name: Copy configuration file to managed node

ansible.builtin.copy:

src: /path/to/local/config.file

dest: /path/to/remote/config.file

owner: root

group: root

mode: '0644'

[Analyzing shell scripts and converting them to playbooks](#contents.xhtml_sc3_181a)

Converting shell scripts into Ansible playbooks is a powerful way to leverage Ansible's automation capabilities while ensuring tasks are executed in a repeatable and idempotent manner. Follow these steps to transform your shell scripts into Ansible playbooks:

1.  Identify script actions: Examine the shell script to understand the action it performs, such as installing packages, editing files or starting services.
2.  Convert script to playbook: For each action identified in the script, find the corresponding Ansible module and create a task in the playbook. Following is an example of converting a script that installs nginx into an Ansible task using the yum module:

    ---

    - name: Install nginx

    hosts: web_servers

    become: true

    tasks:

    - name: Ensure nginx is installed

    ansible.builtin.yum:

    name: nginx

    state: present

By following these steps, we can configure our Ansible managed nodes for secure and efficient automation. Creating and distributing SSH keys simplifies secure connections while configuring privilege escalation ensures that Ansible can perform necessary tasks on managed nodes without manual intervention. Deploying files with Ansible allows for consistent configuration across our infrastructure and converting shell scripts into playbooks leverages Ansible's idempotent properties ensuring that our automation is reliable and repeatable.

[Windows managed nodes](#contents.xhtml_sc3_182a)

Understanding the prerequisites and setting up the environment is essential for managing Window’s nodes with Ansible and ensuring smooth automation workflows. As mentioned, the minimum requirements for Window’s managed nodes to work with Ansible include PowerShell 3.0 and at least .NET 4.0.

This section provides a brief overview and some additional points for setting up and managing Windows nodes with Ansible. This typically includes Windows server 2008 R2 and later and Windows 7 and later.

[Setting up Windows managed nodes](#contents.xhtml_sc4_183a)

To prepare our Windows machines for management with Ansible, follow these steps:

1.  PowerShell and .NET Framework: Ensure PowerShell 3.0 (or newer) and .NET Framework 4.0 (or newer) are installed. Newer versions of Windows include these by default.
2.  WinRM: Ansible communicates with Windows machines over WinRM. We need to configure WinRM on the Windows host. Microsoft provides a script to facilitate this configuration which can be downloaded and run on the Windows host, as follows:

    ConfigureRemotingForAnsible.ps1

    This script sets up WinRM to use HTTP (insecure) or HTTPS (secure) depending on our preference. HTTPS is recommended for production environment.

3.  Firewall rules: Ensure the firewall on the Windows machine allows connections over the WinRM port (default 5985 for HTTP, 5986 for HTTPS).
4.  Inventory configuration: Add the Windows hosts to our Ansible inventory, specifying the connection variables, as follows:

    [windows]

    windows1.example.com

    windows2.example.com

    [windows:vars]

    ansible_user=ansible

    ansible_password=YourPassword

    ansible_connection=winrm

    ansible_winrm_transport=basic # Or another supported transport method

    ansible_winrm_server_cert_validation=ignore # For HTTPS, consider configuring proper validation

5.  Executing playbooks: When running playbooks against Windows hosts, ensure our tasks use Windows compatible modules such as win_command, win_copy, win_feature, etc.

    Following is an example of an Ansible playbook that ensures the Windows feature telnet client is installed on a Windows server:

    ---

    - name: Ensure Telnet Client feature is installed on Windows Servers

    hosts: windows

    tasks:

    - name: Install Telnet Client

    win_feature:

    name: "Telnet-Client"

    state: present

[Privilege escalation](#contents.xhtml_sc3_184a)

Privilege escalation is a critical concept in the context of computer security and system administration, particularly within environment managed by automation tools like Ansible. It refers to the practice where a user gains elevated access to resources that are normally protected from an entry level account. This can happen in two main contexts, as follows:

*   Vertical privilege escalation: This involves gaining higher level permissions or access rights than originally assigned, typically those reserved for system administrators or services (e.g., root access). This is often the goal of attackers who gain a foothold in a system as a less privileged user but need more control to achieve their objectives.
*   Horizontal privilege escalation: This occurs when a user acquires the permission of another user who has the same level of privileged access as they do but different permissions or capabilities within that level (e.g., accessing another regular user's confidential documents).

[Importance in security](#contents.xhtml_sc4_185a)

Privilege escalation is often used by malicious actors to exploit vulnerabilities in software or misconfigurations in systems to gain extended permissions. With these permissions, an attacker could install persistent threats, access sensitive data or even control the system entirely. From a defensive perspective, understanding privilege escalation is critical for securing systems against such attacks.

[Privilege escalation in Ansible](#contents.xhtml_sc4_186a)

In the context of Ansible, privilege escalation is used responsibly and by design. Ansible can automate the process of privilege escalation for legitimate purposes such as managing configurations and installing software which often require higher privileges than those granted to ordinary users.

Following are the ways in which Ansible handles privilege escalation:

*   become parameter: The most common way to handle privilege escalation in Ansible is through the  become keyword which allows Ansible tasks to be executed with the privileges of another user, typically the superuser (root). This keyword can be set at a task level, play level or even globally in a playbook.

    Following is an example of using become in a playbook:

    ---

    - name: Install package as root

    hosts: all

    become: true

    tasks:

    - name: Install a package

    Ansible.builtin.dnf:

    name: vim

    state: latest

*   become_method: While the default method for privilege escalation is sudo, Ansible supports other methods such as su, pbrun, pfexec and more. This is specified using the become_method keyword.
*   become_user: Specifies the user to whom you want to escalate privileges. The default user is root but you can specify any user.

    Following is an example specifying the method and user:

    ---

    - name: Run script as some_user

    hosts: all

    become: true

    become_method: su

    become_user: some_user

    tasks:

    - name: Run a script

    ansible.builtin.script: /usr/local/bin/somescript.sh

[Security best practices for privilege escalation](#contents.xhtml_sc4_187a)

When configuring privilege escalation, it is important to follow security best practices to mitigate risks and ensure that elevated access is used responsibly.

Following are key practices to consider:

*   Least privilege: Ensure that users and processes operate using the least amount of privilege necessary to complete the job. This minimizes the impact of a potential compromise.
*   Audit and monitoring: Keep detailed logs of when privilege escalation is used and by whom. Monitoring these logs can help detect unauthorized attempts to gain elevated access.
*   Secure credentials management: Use secret management tools to securely store and manage passwords and keys needed for privilege escalation.
*   Regular updates and patching: Keep systems and applications updated to minimize vulnerabilities that could be exploited for privilege escalation.
*   Use strong authentication mechanisms: Employ strong authentication mechanisms (e.g., two factor authentication) for accounts that have the capability to perform privilege escalation.

Understanding and properly configuring privilege escalation within Ansible and other IT systems is essential for maintaining a secure and efficient automated environment. It ensures that automated tasks are performed with appropriate security checks and balances in place.

[Ansible navigator](#contents.xhtml_sc2_188a)

The Ansible navigator is short name of the automation content navigator to expand the capabilities of the original ansible-playbook command. The tool can run playbooks and manage Ansible content collections applying advanced practices that elevate the efficiency and scalability of IT automation strategies. Automation content navigator is a conceptual tool within the Ansible ecosystem designed to streamline the discovery, management and implementation of automation content. Automation content navigator is a command-line tool with a text-based user interface tailored for content creators. Its key capabilities are as follows:

*   Launching and monitoring jobs and playbook execution.
*   Sharing stored, completed playbook and job run artifacts in JSON format.
*   Browsing and introspecting automation execution environments and file-based inventories.
*   Rendering Ansible module documentation and extracting usable examples for playbooks.
*   Providing detailed command outputs via the user interface.

[Installation](#contents.xhtml_sc3_189a)

Follow these streamlined steps to install automation content navigator on RHEL registered with Red Hat Subscription Manager:

1.  Installation procedure:
    *   Attach stock keeping unit (SKU): First, attach our RHEL machine to the Red Hat Ansible Automation Platform SKU using the command:

        subscription-manager attach --pool=<sku-pool-id>

2.  Enable repository:
    *   Enable Ansible Automation Platform (AAP) 2.5 (adapt to our current version) repository for RHEL 9 as follows:

        subscription-manager repos --enable ansible-automation-platform-2.5-for-rhel-9-x86_64-rpms

3.  Install automation content navigator:
    *   Proceed with the installation by executing:

        dnf install ansible-navigator

4.  Verification:
    *   Confirm the installation of automation content navigator by checking its help section:

        ansible-navigator –help

        This command should display help information, indicating a successful installation.

By following these steps, we installed automation content navigator on our RHEL system, ready to streamline our Ansible playbook creation and management processes.

[Command line interface](#contents.xhtml_sc3_190a)

The Ansible CLI offers a range of commands for managing automation tasks directly from the terminal. With the introduction of the Ansible navigator, many familiar CLI commands have been extended, providing enhanced functionality and flexibility in both local and execution environments.

The Ansible navigator stdout mode supports executing familiar Ansible commands and extensions directly from the command line, facilitating quick tasks as follows:

*   Usage: We can use the -m stdout subcommand to execute standard Ansible commands within automation execution environments or on our local machine.
*   Help options: The --help command or any subcommand, such as ansible-navigator config --help, provides comprehensive details about supported parameters and their configurations.

Following is a comparison between standard Ansible CLI commands and their corresponding Ansible navigator commands:

| Ansible command line interface | Ansible navigator |
| ansible-galaxy collection | ansible-navigator collections |
| ansible-config | ansible-navigator config |
| ansible-doc | ansible-navigator doc |
| ansible-inventory | ansible-navigator inventory |
| ansible-playbook | ansible-navigator run |

Table 5.1: Ansible navigator commands

[Text-based interface](#contents.xhtml_sc3_191a)

Text-based interface to Ansible commands offers an interactive mode ideal for content evaluation, playbook execution and post-run troubleshooting using artifact files.

This mode enhances interaction with automation content offering features as follows:

*   Colon commands: Access all automation content navigator commands with a colon prefix, e.g.,:run or :collections.
*   Navigation: Instructions on paging, scrolling and accessing help are displayed, alongside color-coded outputs for easier interpretation of information like deprecated modules.

By understanding how to navigate and utilize an abstracted automation content navigator concept, users can effectively manage playbooks and inventories and enhance their Ansible environments with content collections and execution environments. These practices not only streamline the process of running playbooks but also encourage the reusability and sharing of automation content within the community or across different projects within an organization.

[Ansible for Linux](#contents.xhtml_sc2_192a)

These are the most used code snippets in our Ansible playbook or roles. File, package and service management are very useful. As we discussed in the previous chapter, for every simple shell script, we are able to convert on a playbook for our system. To effectively utilize Ansible for common automation tasks in IT infrastructure, let us explore how to craft Ansible playbooks for the most used code snippets involving file, package and service management as well as executing rolling updates. These tasks form the backbone of many automation scripts, offering a robust foundation for system management.

[File management](#contents.xhtml_sc3_193a)

Managing files is a critical aspect of system administration. It involves tasks such as creating, copying, moving and deleting files or directories.

[Ensure a directory exists](#contents.xhtml_sc4_194a)

To make sure a directory exists and has the proper permissions, we can use the ansible.builtin.file module, as follows:

- name: Ensure directory /example exists

ansible.builtin.file:

path: /example

state: directory

mode: '0755'

[Copying a file](#contents.xhtml_sc4_195a)

To copy a local file to a remote system, the ansible.builtin.copy module is used, as follows:

- name: Copy file to remote system

ansible.builtin.copy:

src: /local/path/to/file.txt

dest: /remote/path/to/file.txt

[Remove a file](#contents.xhtml_sc4_196a)

The ansible.builtin.file module allows you also to manage files and symbolic links on remote hosts. Following are examples of how to remove a file and create a symbolic link using this module:

- name: Remove a file

ansible.builtin.file:

path: /path/to/file

state: absent

Create a symbolic link:

- name: Create a symbolic link

ansible.builtin.file:

src: /path/to/original

dest: /path/to/link

state: link

[Service management](#contents.xhtml_sc3_197a)

Service management involves starting, stopping and ensuring the enabled or disabled status of system services.

Following is an example:

*   Starting a service:

    - name: Start nginx service

    ansible.builtin.service:

    name: nginx

    state: started

    enabled: true.

*   Restart a service:

    - name: Restart nginx

    ansible.builtin.service:

    name: nginx

    state: restarted

*   Stop a service:

    - name: Stop nginx

    ansible.builtin.service:

    name: nginx

    state: stopped

[Rolling updates](#contents.xhtml_sc3_198a)

Rolling updates are essential for minimizing downtime during application updates or configuration changes. In Ansible, rolling updates can be implemented using dynamic inventories and playbooks targeting specific groups of hosts, as follows:

- name: Rolling update for web servers

hosts: webservers

serial: 1 # Update one server at a time

tasks:

- name: Pull latest code

ansible.builtin.git:

repo: 'https://example.com/repo.git'

dest: /path/to/destination

version: master

- name: Restart web service

ansible.builtin.service:

name: nginx

state: restarted

This example playbook performs a rolling update on a group of web servers defined in our inventory. It updates one server at a time, pulls the latest code from a Git repository and restarts the NGINX service.

[Jinja2 templates](#contents.xhtml_sc3_199a)

Jinja2 is a modern and designer friendly templating language popular in Python. It is fast, widely used, secure and integrated inside Ansible. In the context of Ansible, Jinja2 templates are a powerful feature that allows for dynamic expressions and access to variables. Templates are often used to automate configuration files because they are customizable with variables. Jinja2 templates allow us to use placeholders to represent variables and expressions evaluated at runtime. This enables dynamic content creation from static files which is particularly useful in configurations where certain values might change based on the environment, host or any other context specific data.

[Basic syntax](#contents.xhtml_sc4_200a)

Understanding the basic syntax of Jinja2 is essential for working with templates in Ansible. Following are some of the key elements of Jinja2 syntax that are frequently used when developing playbooks and templates:

*   Variables: We can use {{ variable_name }} to insert the value of a variable.
*   Control structures: Jinja2 supports control structures such as loops and conditionals. Following is an example to iterate over a list:

    {% for item in my_list %}

    - {{ item }}

    {% endfor %}

*   Filters: Filters are used to modify the variables. They are applied to variables using the pipe symbol (|). For instance, to capitalize a string: {{ "hello world" | capitalize }} produce the text Hello World on screen.

[Using Jinja2 templates in Ansible](#contents.xhtml_sc4_201a)

In Ansible, Jinja2 templates are commonly used in two ways, as follows:

*   Directly in playbooks: For an inline dynamic content generation.
*   Template files: For generating files from a template. This is done using the template module.

    Example: Generating a configuration file.

    Let us say we have a Jinja2 template for an application configuration file app.conf.j2:

    [server]

    address = {{ server_address }}

    port = {{ server_port | default('80') }}

    [database]

    name = {{ database_name }}

We can use the Ansible template module to generate a configuration file from this template, as follows:

- name: Generate configuration file from template

ansible.builtin.template:

src: app.conf.j2

dest: /etc/myapp/app.conf

vars:

server_address: '192.168.1.10'

database_name: 'mydatabase'

This playbook snippet uses the template module to take app.conf.j2 as the source and renders it to /etc/myapp/app.conf, substituting the server_address and database_name variables with the given values.

[Advanced Jinja2 features in Ansible](#contents.xhtml_sc4_202a)

*   Accessing Ansible facts: We can use Ansible facts which are variables automatically discovered by Ansible from the host system within our templates. For example, {{ ansible_facts[hostname] }}
*   Conditional expressions: Jinja2 allows for conditional expressions in templates, enabling the creation of highly customizable configurations. For example,

    {% if enable_feature %}

    feature_flag = true

    {% endif %}

[Best practices for Jinja2 templates in Ansible](#contents.xhtml_sc4_203a)

When working with Jinja2 templates in Ansible, following best practices ensures that your templates are maintainable, secure, and error-free. Following are some key recommendations:

*   Keep it readable: While Jinja2 templates can be powerful, avoid overly complex expressions that make our templates hard to read and maintain.
*   Template linting: Use linting tools to check our Jinja2 syntax and adhere to best practices.
*   Secure template processing: Be mindful of the data being processed in templates, especially when dealing with user input, to avoid injection vulnerabilities.

Jinja2 templates in Ansible offer a powerful way to create dynamic, data driven configurations. By leveraging these templates, we can streamline our configuration management process making it more efficient and adaptable to changes in our environment.

[User management](#contents.xhtml_sc3_204a)

In any Unix-like operating system, user and group management is essential for securing access to system resources. Users represent individuals or services that can request resources from the system while groups help define collections of users under a common set of permissions. Managing these entities manually can be error-prone and inefficient especially, at scale. Ansible automates the provisioning, configuration and management of user accounts and groups across a multitude of systems, ensuring consistency and reliability while reducing manual overhead and potential errors. It uses modules like user and group, which are idempotent, meaning repeated execution of the playbook results in the same system state without producing side effects.

[Ansible playbook for managing users](#contents.xhtml_sc4_205a)

Following a simple playbook that demonstrates creating a user and adding the user to a group:

---

- name: Manage Users and Groups

hosts: all

become: true

tasks:

- name: Ensure group "webadmin" exists

ansible.builtin.group:

name: webadmin

state: present

- name: Create user "john"

ansible.builtin.user:

name: john

group: webadmin

createhome: yes

shell: /bin/bash

state: present

- name: Ensure user "john" has sudo privileges

ansible.builtin.copy:

dest: /etc/sudoers.d/john

content: "john ALL=(ALL) NOPASSWD: ALL"

validate: 'visudo -cf %s'

Following is the explanation for the above code:

*   Group module: Ensures that the webadmin group is present.
*   User module: Ensures that the user john is present, adds him to the webadmin group and sets default shell and home directory.
*   Copy module: Adds a sudoers file to allow john password less sudo access with syntax validation.

[Advanced usage: Managing multiple users](#contents.xhtml_sc4_206a)

For managing multiple users, Ansible supports looping through a list of users defined either in the playbook itself or externally in a variable file, as follows:

---

- name: Manage Multiple Users

hosts: all

become: true

vars:

users:

- name: john

shell: /bin/bash

- name: jane

shell: /bin/zsh

tasks:

- name: Ensure user exists

ansible.builtin.user:

name: "{{ item.name }}"

shell: "{{ item.shell }}"

state: present

loop: "{{ users }}"

[Handling user absences](#contents.xhtml_sc4_207a)

To remove a user, simply change the state parameter to absent. This is useful for deprovisioning, as follows:

- name: Remove user "john"

ansible.builtin.user:

name: john

state: absent

Ansible provides a robust framework for managing users and groups across diverse environments, leveraging simple, readable syntax and idempotent operations. Whether we are managing a small set of servers or an entire data center, Ansible's user and group management capabilities help streamline our processes and ensure compliance with our access policies. As we expand use of Ansible, consider integrating other modules and plugins to handle more complex tasks and workflows, enhancing the security and manageability of our infrastructure.

[Ansible vault](#contents.xhtml_sc2_208a)

As our appetite for automation grows, especially in enterprise environments, we need to find the best way to store sensitive information in a secure way. Ansible vault is the tool integrated into the Ansible toolchain.

[Creating encrypted file](#contents.xhtml_sc3_209a)

To create a new encrypted file, we can use the command ansible-vault to create a filename. This command prompts us to enter a new vault password before opening the file in the default text editor for editing as follows:

$ ansible-vault create secret.yml

For automated scripts or when we prefer not to enter a password interactively, we can specify a file containing the vault password using the --vault-password-file option, as follows:

$ ansible-vault create --vault-password-file=vault-password.txt secret1.yml

Alternatively, we can create an inline variable vault using the following command:

ansible-vault encrypt_string 'cleartext'

New Vault password:

Confirm New Vault password:

Encryption successful

!vault |

$ANSIBLE_VAULT;1.1;AES256

35663935616433303865313939626335633632373465613839326562313263623535313464653834

3438656536316238636263666364343561626432346435610a656339316531396664653431663562

37636263393637666636616665393035333334626166373764613436313237653363373233623434

3031366561333536320a666661383365356633663130313566663862316136393066323534353938

3739

We can now copy and paste the output in our Ansible playbook and store the single variable encrypted inline.

*   Using the encrypted variable in your playbook: Copy the entire block starting from variable_name: and paste it into your Ansible playbook. Following is how you can structure your playbook:

    ---

    - name: Use Encrypted Variable

    hosts: all

    vars:

    variable_name: !vault |

    $ANSIBLE_VAULT;1.1;AES256 303835383464386461643864666230653731643362376138663139326666343938

    646639393561633764386530376439303539346566656366633465393566343266

    3535663633643965323638343938656638356433663933313234

    tasks:

    - name: Print the secret data

    debug:

    msg: "{{ variable_name }}"

    In this playbook, the debug module prints out the decrypted value of variable_name, demonstrating how Ansible automatically decrypts the vault encrypted content when run with the correct vault password.

*   Running the playbook: To execute this playbook, you must provide the vault password. This can be done using the --ask-vault-pass flag to manually input it or by referencing a file that contains the vault password using --vault-password-file:

    ansible-playbook playbook.yml --ask-vault-pass

    or

    ansible-playbook playbook.yml --vault-password-file=path/to/vault-password.txt

[Best practices](#contents.xhtml_sc4_210a)

To ensure the security and proper usage of Ansible vault for sensitive data, it is important to follow best practices. Following are the key guidelines to keep in mind:

*   Secure vault password: Store the vault password securely and limit access to it. Avoid hardcoding passwords directly in scripts or shared documents.
*   Minimal usage: Only use encrypted variables for sensitive data that must be secured. Keep the use of vault encrypted items to what is necessary to ease maintenance.
*   Version control: Avoid committing the vault password file to version control. Commit only encrypted files or variables, ensuring that plaintext sensitive information is never exposed.
*   Regular rotation: Regularly rotate secrets and vault passwords to enhance security, especially when team members who had access leave the project.

[Editing an encrypted file](#contents.xhtml_sc3_211a)

When we need to modify an encrypted file, the ansible-vault edit command allows us to do so securely. It will request the vault password to decrypt the file. Let us make changes and then re-encrypt the file upon saving, as follows:

$ ansible-vault edit secret.yml

[Using encrypted files in playbooks](#contents.xhtml_sc4_212a)

To use the encrypted variables within our playbooks, include the encrypted file in the vars_files section of our playbook. Then, run our playbook with the --vault-password-file option to provide the necessary vault password.

Following is an example of playbook:

---

- name: Secure Playbook

hosts: all

vars_files:

- secret.yml

tasks:

- name: Ensure sensitive data is protected

debug:

msg: "{{ sensitive_data }}"

Running the playbook securely, as follows:

$ ansible-playbook --vault-password-file=vault-password.txt secure_playbook.yml

[Configuration files](#contents.xhtml_sc2_213a)

In Ansible, configuration files are crucial for defining the behavior of Ansible itself, the managed nodes and the execution of tasks and playbooks. These configuration files allow us to tailor Ansible's settings to meet our specific requirements and infrastructure environment. Following is an overview of the main configuration files in Ansible and their purposes:

The ansible.cfg is the main configuration file for Ansible. It defines global settings that affect all playbooks and roles. It can be located in several places and Ansible will use the first one it finds in the order:

ANSIBLE_CONFIG (an environment variable pointing to a file), ansible.cfg (in the current directory), .ansible.cfg (in the user's home directory) and /etc/ansible/ansible.cfg.

This file controls many aspects of Ansible's behavior including default module paths, inventory locations, privilege escalation settings and more.

Inventory files are used to list and group our managed nodes. These can be static files in INI, short for initialization, or YAML format or dynamic scripts that pull inventory from external sources. Inventory files specify the hosts and groups of hosts upon which commands, modules and tasks in a playbook operate.

While not configuration files in the traditional sense, playbooks are YAML files that describe the tasks to be executed on managed nodes. They can include variables, tasks, handlers and other elements to automate complex multi-tier IT application environments.

Roles are sets of tasks and additional files for variable definitions, templates and handlers, which are organized in a standard directory structure. Each role is designed to accomplish a distinct task or set of tasks and they can be used to organize tasks in a reusable and modular fashion. Following is an overview of the main configuration files and their purposes:

*   hosts: Though technically part of the inventory, it is worth mentioning separately as it is often referred to as a configuration file. The host file contains the list of managed nodes and can define groups and subgroups of these nodes.
*   Group variables and host variables directories (group_vars and host_vars) contain files that define variables applied to groups of hosts or individual hosts, respectively. These are useful for setting variables that differ between groups or specific hosts in our inventory.

While ansible-vault is not a configuration file itself, it is used to encrypt sensitive data in Ansible such as passwords or keys.  Files encrypted with ansible-vault can be seamlessly decrypted by Ansible at runtime, provided the correct password is supplied. Thus, we can store sensitive information in our Ansible configuration files securely.

Understanding and correctly configuring these files are key to leveraging Ansible's full potential in automating our infrastructure.

[Roles](#contents.xhtml_sc2_214a)

We can simplify playbooks using roles and collections to leverage code reuse. Roles provide a structured way to organize playbooks making them more modular and maintainable. They allow us to create roles for specific tasks (e.g., web server setup and database configuration) and reuse them across different playbooks.

A role's directory structure is as follows:

*   tasks: Main actions to be executed.
*   handlers: Tasks triggered by specific conditions.
*   templates: Jinja2 templates for generating files.
*   files: Static files to be deployed to target hosts.
*   vars: Role specific variables.
*   defaults: Default variables with lower priority.
*   meta: Role dependencies and additional information.
*   tests: Contains test inventory and test playbooks.

Utilizing roles facilitates code reuse and ensures that our automation scripts are organized and easy to maintain.

[Use a role](#contents.xhtml_sc3_215a)

The most common way of interacting with the Ansible role is to download from a registry and using in our playbook. Ansible Galaxy is a public archive of Ansible roles and collections. We can explore the vast library via web browser, search for the resource most relevant to our use case and download it via the ansible-galaxy command line utility.

Create a playbook at the root of your project directory (production.yml), as follows:

---

- name: Use the webserver role

hosts: all

become: true

roles:

- webserver

[Create a role](#contents.xhtml_sc3_216a)

Ansible provides the ability to create roles to streamline automation tasks and promote reusability. Roles are a structured way to organize playbooks, tasks, and related files as follows:

Use ansible-galaxy command to manage Ansible roles. To create a new my_role role structure, use the following:

ansible-galaxy init my_role

This command creates a directory structure for my_role under the current directory.

[Working with roles](#contents.xhtml_sc3_217a)

When working with roles in Ansible, it is important to structure your tasks, templates, variables, and handlers effectively to maintain modularity and reusability. Inside the tasks/main.yml file, define the tasks we want our role to perform. For example, to install and start nginx, use the following:

---

- name: Package nginx installed

ansible.builtin.yum:

name: nginx

state: present

- name: Deploy Nginx configuration

ansible.builtin.template:

src: nginx.conf.j2

dest: /etc/nginx/nginx.conf

- name: Service nginx started and enabled on boot

ansible.builtin.service:

name: nginx

state: started

enabled: true

The following are the next steps:

*   Add templates and files: If our role needs to deploy customized configuration files, use the templates/ directory for Jinja2 templates. For static files, use the files/ directory. The following file nginx.conf.j2 is stored under the templates/ directory of our role, as follows:

    server {

    listen 80;

    server_name {{ ansible_facts['hostname'] }}; # Dynamically sets the server name

    location / {

    root /usr/share/nginx/html;

    index index.html index.htm;

    }

    }

*   Declare variables: Use the vars/main.yml or defaults/main.yml to define variables used in our role. Variables in defaults/ have the lowest precedence, making them easy to override.
*   Use handlers: If we need to restart a service when a file changes, define a handler in handlers/main.yml and notify that handler from our task.
*   Define role dependencies: If our role depends on other roles, specify those dependencies in meta/main.yml.

[Using role in playbook](#contents.xhtml_sc3_218a)

Create a playbook that includes the role. For instance, to apply my_role to our hosts, use the following:

---

- hosts: all

roles:

- my_role

[System roles](#contents.xhtml_sc3_219a)

System roles simplify the automation of routine Linux administration tasks enhancing system consistency and reducing the potential for human error by leveraging Ansible and code reuse. They are based on the open-source Linux system roles^([2](#ch05.xhtml_footnote-001)) distributed as fedora.linux_system_roles collection.

RHEL system roles are a set of Ansible roles and modules that provide a consistent configuration interface to automate the management of RHEL systems. They encapsulate best practices and provide a high level abstraction for RHEL configuration tasks such as network setup, SELinux management, time synchronization, etc. By abstracting the complexity of system configuration, RHEL system roles enable administrators to focus on higher level infrastructure strategies rather than getting bogged down in the minutiae of individual configuration files and commands.

Following are the key benefits of RHEL system roles:

*   Consistency and standardization: RHEL system roles ensure that configuration changes are applied uniformly across the infrastructure, mitigating configuration drift and enhancing system stability.
*   Simplified management: Administrators can manage diverse systems with a single, unified approach, significantly reducing the learning curve and simplifying system management.
*   Best practices: Red Hat develops and maintains RHEL System Roles, incorporating Red Hat's good practices^([3](#ch05.xhtml_footnote-000)) deep insights into RHEL best practices and secure configuration guidelines.
*   Scalability: Automation with RHEL System Roles easily scales from managing a few systems to handling thousands making it suitable for both small enterprises and large data centers.

To use RHEL system roles ensure that Ansible and the rhel-system-roles package are installed on our control node. This package is available in the RHEL repository and can be installed using the package managerdnf, as follows:

dnf install rhel-system-roles

Once installed, the system roles are available to Ansible playbooks, allowing administrators to utilize them to manage RHEL configurations. Following is a simple example playbook that uses the timesync role to configure time synchronization:

- hosts: all

roles:

- rhel-system-roles.timesync

vars:

timesync_ntp_servers:

- hostname: time.example.com

iburst: true

This playbook ensures that all targeted systems synchronize their time with time.example.com, using the Network Time Protocol (NTP) protocol with the iburst option for quicker synchronization on start-up.

RHEL System Roles cover a wide range of Linux administration tasks. Some of the notable roles include the following:

*   network: Configures network interfaces, connections and settings.
*   selinux: Manages SELinux policies and settings.
*   firewall: Configures firewall rules and policies.
*   storage: Manages disk partitions, volume groups and filesystems.
*   timesync: Configures time synchronization using NTP or chrony.

Each role comes with a set of variables that administrators can customize to meet their specific requirements, offering flexibility and control over system configurations.

By leveraging system roles, system administrators can ensure consistent configurations, implement best practices and scale their automation efforts across their infrastructure. As automation continues to play a crucial role in IT operations, RHEL system roles represent a vital tool in the administrator's toolkit enabling more time to be spent on strategic initiatives rather than routine maintenance.

[Collections](#contents.xhtml_sc2_220a)

Collections advance the integration of additional Ansible resources. This package format may contain playbooks, roles, modules and plugins under a shared namespace. They were introduced to organize and distribute Ansible content more efficiently especially, after version 2.9\. Collections can be installed from automation hub, Ansible galaxy or other sources making sharing, updating and managing Ansible content easier across projects. Examples of commonly used collections include ansible.builtin, community.general, amazon.aws, azure.azcollection, and google.cloud, each catering to specific automation needs.

[Simplifying playbooks](#contents.xhtml_sc3_221a)

To make Ansible playbooks more manageable and scalable, it is important to focus on simplifying them through the use of roles and collections. Following are some key strategies for simplifying playbooks:

*   To simplify playbooks using roles and collections, start by identifying repetitive tasks and configurations that can be abstracted into roles.
*   Organize our playbooks by separating tasks into roles based on their functionality. For example, create separate roles for setting up a database, configuring a web server and deploying an application.
*   Utilize collections to leverage pre-built roles and modules. This not only saves time but also ensures that we are using well tested and community supported solutions.
*   Keep our playbooks focused on orchestrating roles and defining the flow of our automation tasks rather than detailing every step within the playbook itself.

By following these guidelines, we can significantly simplify our Ansible playbooks making them easier to read, maintain and extend. This approach not only enhances the reusability of our code but also promotes best practices in Ansible automation.

[Installing content collections](#contents.xhtml_sc3_222a)

Installing Ansible content collections and using them in our playbooks can significantly extend the functionality and efficiency of our automation workflows. Ansible collections is a distribution format for Ansible content that can include playbooks, roles, modules and plugins. Following is how we can install collections and use them in our Ansible playbooks:

Installing ansible collections: We can install collections from Ansible Galaxy, Ansible automation hub or a Git repository. The most common source is Ansible Galaxy which is a community hub for sharing Ansible content.

To install a collection from Ansible Galaxy or automation hub, use the ansible-galaxy command followed by the collection namespace and the collection name. For example, to install the amazon.aws collection, we would run the following:

ansible-galaxy collection install amazon.aws

If we are working in an environment without direct internet access, we can download the collection tarball from a machine with internet access using the following command:

ansible-galaxy collection download amazon.aws

Then, we can transfer the .tar.gz file to our target machine and install it using the following:

ansible-galaxy collection install amazon.aws-*.tar.gz

[Using collection in playbook](#contents.xhtml_sc3_223a)

Ansible collections provide a modular and flexible way to use roles, modules, and plugins across projects. By incorporating collections into your playbooks, you can enhance automation tasks with reusable and well maintained content. Following are various ways to specify and use collections in your playbooks:

*   Specifying collections in a playbook: Once we have installed a collection, we can use its content (such as roles and modules) in our playbooks. To specify that a playbook should use a particular collection, we can use the collections keyword at the play level or within a specific task.
*   Using collections at the play level: Specifying a collection at the play level allows all tasks within that play to access the roles and modules within the collection without requiring fully qualified names. Following is an example:

    ---

    - name: Create EC2 instance

    hosts: all

    collections: amazon.aws

    tasks:

    - name: Start an instance with a public IP address

    amazon.aws.ec2_instance:

    name: "public-compute-instance"

    key_name: "prod-ssh-key"

    vpc_subnet_id: subnet-abcdefghi

    instance_type: t3.micro

    security_group: default

    network:

    assign_public_ip: true

    image_id: ami-123456

*   Using collections in tasks:  We can also specify collections within individual tasks by using fully qualified collection names. This method is useful if we only need to use a few modules from a collection and do not want to apply the collection to the entire play, as follows:

    - name: Start virtual machine

    azure_rm_virtualmachine:

    resource_group: {{ resource_group_name }}

    name: {{ vm_name }}

    started: yes

    Ansible collections offers a scalable and flexible way to manage and use Ansible content, allowing us to easily share and reuse Ansible roles, modules and other components across our projects. By installing collections and referencing them in our playbooks, we can enhance our automation tasks and workflows with a wide range of functionalities provided by the Ansible community and other sources.

*   Using collections in a playbook:  Once installed, we can use the roles and modules contained within the collection by specifying them in our playbook. Following is an example playbook that demonstrates how to use a role from a collection to install and configure NGINX:

    ---

    - name: Configure Web Server with NGINX

    hosts: web_servers

    collections:

    - community.nginx

    tasks:

    - name: Include NGINX role from community collection

    ansible.builtin.include_role:

    name: nginx

    vars:

    nginx_http_params:

    - name: client_max_body_size

    value: '10M'

[The requirements.yml file](#contents.xhtml_sc3_224a)

Using a requirements.yml file is a structured and efficient way to manage and install Ansible collections and roles for our projects. This method not only allows us to replicate environments easily but also helps maintain consistency across different setups. Following are the steps on how we can use a requirements.yml file in our Ansible environment:

1.  Create the requirements.yml file:

    This file will contain all the collections and roles that we need. Following is an example of what the file might look like:

    ---

    collections:

    - name: ansible.builtin

    - name: community.mysql

    version: "1.3.0"

    - name: community.kubernetes

    source: https://galaxy.ansible.com

    roles:

    - name: geerlingguy.nginx

    version: "2.7.0"

    source: https://galaxy.ansible.com

    Following are the details:

    *   Collections: This section lists all the collections we want to install. We can specify versions and sources. Omitting the version will install the latest available.
    *   Roles: Similar to collections, we can list roles with optional versions and source specifications.
2.  Installing collections and roles:

    To install the collections and roles specified in our requirements.yml, use the following command:

    ansible-galaxy install -r requirements.yml

    This command will install both collections and roles listed in the requirements.yml file.

3.  Using collections and roles in our playbook:

    Once the required collections and roles are installed, we can use them in our playbooks. Following is how we can structure our playbook:

    ---

    - name: Deploy Web Application

    hosts: web_servers

    gather_facts: yes

    roles:

    - role: geerlingguy.nginx

    vars:

    nginx_vhosts:

    - server_name: "example.com"

    root: "/var/www/html/example"

    tasks:

    - name: Ensure database is present

    community.mysql.mysql_db:

    name: mydb

    state: present

    collections:

    - community.mysql

[Key tips](#contents.xhtml_sc4_225a)

When working with Ansible collections and dependencies, following key best practices can help ensure smooth management and integration within your playbooks. Following are some key tips to keep in mind:

*   Version control: Include our requirements.yml in version control to keep track of dependencies.
*   Private repositories: Configure appropriate keys or tokens if we use private repositories or need access control.

    [galaxy]

    server_list = automation_hub

    [automation_hub]

    url = https://automation-hub.example.com/api/

    token = YOUR_API_TOKEN_HERE

*   Regular updates: Periodically update the versions in requirements.yml to leverage new features or patches from dependencies.

[Troubleshooting](#contents.xhtml_sc4_226a)

When managing collections and dependencies in Ansible, errors can occur during installation or conflicts may arise between versions. Following are some troubleshooting tips to help resolve common issues:

*   Errors during installation: Check the syntax and validity of the requirements.yml file. Ensure that all specified sources are reachable and that versions exist.
*   Dependency conflicts: Sometimes collections or roles might depend on specific versions of other collections or roles leading to conflicts. Carefully read the error messages and adjust our versions accordingly.

By following these steps, we can streamline our Ansible setup process, ensure consistency across environments, and easily manage updates to our automation scripts.

[Tests](#contents.xhtml_sc2_227a)

Writing tests in Ansible is essential to ensure that our automation is reliable and work as expected. It involves various levels of testing including unit, integration, functional testing and more. Following are the types of testing that we can implement in Ansible:

*   Unit testing:  Unit testing in Ansible typically applies to individual playbooks. Although running individual playbooks in an isolated environment might only sometimes be practical, checking the playbook syntax to ensure no deployment breaks due to minor errors is crucial. This can be done using the ansible-playbook --syntax-check command.
*   Integration testing:  Integration testing is more valuable in Ansible. It involves testing small groupings of individual units of code (like roles and tasks) to ensure they work correctly together. This can be done by structuring our playbooks with limited dependencies and testing each role individually in a fresh virtual machine before deploying it as part of a full infrastructure deployment.
*   Functional testing:  Functional testing involves setting up a complete infrastructure environment and running tests against it to ensure everything was installed, deployed and configured correctly. This can be done using Ansible’s own reporting and external tools to test the infrastructure more deeply.

[Debugging and asserting](#contents.xhtml_sc3_228a)

For most playbooks, testing configuration changes and the result of commands as you go is sufficient. Ansible has built-in modules such as debug, fail and asserts that helps in testing conditions and ensuring the system is in the correct state.

*   The debug module can print values of variables or messages during playbook execution aiding in both development and troubleshooting.
*   The failed and assert modules allow us to test conditions explicitly and, if necessary, abort the playbook run based on the outcomes of these tests.

The failed module can be used to forcibly fail and stop the playbook execution if a certain condition is met. It is particularly useful for scenarios where we want to ensure prerequisites are met before proceeding with further tasks.

---

- name: Example playbook using the fail module

hosts: all

tasks:

- name: Check if custom configuration file exists

ansible.builtin.stat:

path: "/path/to/my/custom.config"

register: custom_config_stat

- name: Fail if the file does not exist

ansible.builtin.fail:

msg: "The custom configuration file is missing. Please ensure /path/to/my/custom.config exists."

when: not custom_config_stat.stat.exists

In this example, the playbook checks if a custom configuration file exists at a specified path. If the file does not exist, the failed module is invoked to stop playbook execution providing a clear message about the missing file.

The assert module is used to assert that certain conditions are true and can perform multiple checks in one task. If any of the assertions fail, the playbook execution is halted, as follows:

---

- name: Example playbook using the assert module

hosts: all

gather_facts: true

tasks:

- name: Collect the system's distribution information

ansible.builtin.setup:

filter: ansible_distribution

- name: Assert multiple conditions

ansible.builtin.assert:

that:

- ansible_distribution == "Ubuntu"

- ansible_distribution_version is version('24.04', '>=')

fail_msg: "This playbook can only be run on Ubuntu 24.04 or newer."

success_msg: "Distribution check passed."

The playbook first gathers the system's distribution information using the setup module in this example. Then, it uses the assert module to check two conditions, as follows:

*   The system must run Ubuntu
*   The version must be 24.04 or newer

If neither condition is met, the playbook execution is stopped and a failure message is displayed. If both conditions are met, a success message is shown. Alternatively, we can test the specific version with ansible_facts['lsb']['release'] == "24.04".

[Linting](#contents.xhtml_sc3_229a)

Linting is a crucial step in ensuring the accuracy and quality of your Ansible content and YAML files. By performing linting, you can catch syntax errors early and ensure adherence to best practices. The following tools can assist in linting:

*   ansible-playbook --syntax-check: This tool can be used to check basic syntax.
*   yamllint: This tool can be used to check for common errors in Ansible playbooks such as indentation and formatting issues.
*   ansible-lint: This tool extends beyond YAML syntax, checking Ansible tasks and playbooks for practices that deviate from Ansible’s best practices.
*   spotter: This is a commercial product created by XLAB Steampunk to extend to ansible-lint with the history of every module change and security implication of change of name or security settings.

[Molecule](#contents.xhtml_sc3_230a)

Molecule is a powerful framework for developing and testing Ansible roles, playbooks and collections. It automates the process of setting up test environments, running our playbooks and tearing down the environments after tests. Molecule supports multiple scenarios and backends, making it highly versatile for testing across different platforms and configurations.

Molecule workflows typically involve the following:

*   Creating a new role or scenario with molecule init.
*   Develop our automation and use molecule convergence to apply it to a testing environment.
*   Debugging as necessary with molecule login to interact with the test environment.
*   Running molecule tests to go through a complete test cycle, ensuring our automation works flawlessly and with idempotence.
*   Testing our Ansible content thoroughly before deployment is crucial for maintaining reliable and efficient automation. By incorporating these testing strategies and tools into our development workflow, we can ensure that our Ansible playbooks, roles and collections are robust, reliable and ready for production.

First, ensure we have Ansible, Docker and Molecule installed. We can install Molecule and Docker as dependencies via Python package installer (PIP), if they are not already installed, as follows:

pip install molecule[docker]

Once these prerequisites are met, follow these steps to create and test a new Ansible role:

1.  Initialize a new role with Molecule: Create a new directory for our role and navigate into it, as follows:

    mkdir nginx_role && cd nginx_role

    Initialize a new role and scenario with Molecule, as follows:

    molecule init role –driver-name docker my_namespace.nginx_role

    Replace my_namespace with our actual namespace or username. This command scaffolds a new role in a directory called nginx_role and sets up Molecule to use Docker.

2.  Define our Molecule scenario: Navigate to our role directory and open the molecule/default/molecule.yml file to configure our testing environment. Make sure the platforms section is set up for an Ubuntu container, as following:

    platforms:

    - name: instance

    image: "ubuntu:22.04"

    pre_build_image: true

    This configuration tells Molecule to use the ubuntu:20.04 Docker image for testing.

3.  Write a task to install NGINX:  Edit the tasks/main.yml file in our role directory nginx_role/tasks/main.yml to add a task that installs NGINX, as follows:

    ---

    - name: Install Nginx

    ansible.builtin.apt:

    name: nginx

    state: present

    become: true

    This task uses Ansible's apt module to ensure NGINX is installed.

4.  Create a test assertion: Edit the molecule/default/verify.yml file to add a test that verifies NGINX is installed and running. We might add something as follows:

    ---

    - name: Verify

    hosts: all

    gather_facts: false

    tasks:

    - name: Check if Nginx is installed

    command: nginx -v

    register: nginx_version

    failed_when: nginx_version.stderr is search("command not found")

    - name: Ensure Nginx is running

    ansible.builtin.service:

    name: nginx

    state: started

    This playbook checks that NGINX is installed and running on the container.

5.  Run molecule to test our role: From our role directory, run the following:

    molecule test

    This command goes through each step defined by Molecule, linting our code, creating a test instance with Docker, applying our role to this instance, running the verification playbook and then cleaning up the instance.

Following these steps, we can create a basic Molecule scenario to test the deployment of NGINX on an Ubuntu container. Adjust our tasks and tests based on the specifics of our role and what we need to verify.

[Ansible Automation Platform](#contents.xhtml_sc2_231a)

Managing large projects, content collections and execution environments within the Ansible Automation Platform (AAP) involves a comprehensive understanding of its architecture and components including the automation controller (formerly Ansible tower), automation hub and execution environments.

[Table 5.2](#ch05.xhtml_tab5-2) compare key components of the Ansible community and the Ansible Automation Platform:

| Ansible community | Ansible Automation Platform |
| Controller | Automation controller |
| Galaxy | Automation hub |
| Receptor | Automation mesh |
| Event driven Ansible | Event driver controller |

Table 5.2: Comparison between Ansible community and Ansible automation platform

The AAP architecture is designed to provide a comprehensive solution for managing and automating IT infrastructure, consisting of several key components as follows:

*   Automation controller: The control plane for Ansible automation is replacing Ansible tower with a new container-oriented design. It executes automation code connecting to target nodes. It integrates Role-Based Access Control (RBAC) and workflow management to create complex workflows that combine multiple playbooks, job templates and inventory sources.
*   Automation hub: A centralized location for managing and sharing Ansible content across an organization. It offers a repository for sharing, discovering and collaborating on Ansible roles, playbooks and collections.
*   Execution environments: Container images that include system level dependencies and collection-based content ensuring consistency across different nodes and simplifying the management of Python environments for automation tasks.
*   Role-based access control: With granular access, we can ensure that our users have appropriate access to automation resources, enhancing security and control.
*   Automation analytics: Cloud components to evaluate the impact of the automation in our organization combining clusters and instances.
*   Integrated with Red Hat products: Deeply integrated with Red Hat Insights and Red Hat Satellite.

For large projects, AAP simplifies the management of inventories and playbook projects. Projects in the automation controller refer to a logical group of Ansible playbooks, roles and other related files used to automate tasks and manage infrastructure. These can be managed within a project by either placing them manually under the project base path or utilizing a source code management (SCM) system such as Git, Subversion or Red Hat Insights.

Content collections in AAP are essential for distributing content across an organization. Collections package and distribute Ansible content including roles, modules, plugins and other automation artifacts. They offer a centralized and standardized approach to managing and sharing Ansible content facilitating collaboration among teams and organizations.

Execution environments are a key feature of AAP, providing isolated environments for running automation tasks. They are built using the ansible-builder command line tool and can include collections, Python requirements, system-level packages and custom dependencies. Execution environments allow for the specification of the environment in job templates ensuring that automation tasks are executed in a consistent and controlled manner.

[Best practices](#contents.xhtml_sc4_232a)

To ensure efficient management of automation processes within the Ansible Automation Platform, it is important to follow best practices that promote modularity, consistency, and organization. These practices help streamline large scale projects and ensure reliable execution across environments as follows:

*   Organize and modularize code: Use roles and collections to organize and package automation content into reusable units promoting modularity and reducing duplication.
*   Customize execution environments: Build custom execution environments to include all necessary dependencies and collections, ensuring that our automation tasks run consistently across different environments.
*   Automation hub: Leverage the Red Hat certified hub for managing and sharing Ansible content ensuring access to certified, validated and supported content.
*   Optimize project and inventory management: Utilize software configuration management (SCM) systems for version control of our projects and playbooks ensuring easy updates and management of our automation content.

By following these guidelines and utilizing the components and features of the Ansible automation platform, organizations can effectively manage large projects, content collection and execution environments streamlining their automation processes and improving efficiency across their IT infrastructure.

[Conclusion](#contents.xhtml_sc2_233a)

This chapter is designed to be an invaluable resource for those seeking to elevate their Linux system administration skills through automation specifically using Ansible and is a vital steppingstone toward RHCE certification.

[Points to remember](#contents.xhtml_sc2_234a)

*   Ansible installation and setup: Install Ansible smoothly using package managers like dnf or brew on control nodes and configure managed nodes for SSH or WinRM without needing any agents.
*   Privilege escalation techniques: Utilize Ansible's become features to safely elevate privileges for tasks requiring root access ensuring scripts run effectively under controlled privileges.
*   Ansible roles and collections: Leverage roles for reusing code and collections from Ansible galaxy to incorporate community-maintained roles and modules enhancing playbook efficiency and maintainability.
*   Secure sensitive data: Use Ansible vault to encrypt sensitive playbook variables like passwords and keys ensuring security and compliance in automation scripts.
*   Testing and linting: Implement tests using Molecule for role verification and use ansible-lint for ensuring playbooks follow best practices crucial for maintaining high quality Ansible code.

[Multiple choice questions](#contents.xhtml_sc2_235a)

1.  How can we print the current Ansible configuration on the screen?
    1.  ansible-navigator config
    2.  ansible.cfg
    3.  ansible config --dump
    4.  ansible-navigator settings
2.  How can we store sensitive information with Ansible?
    1.  ansible-galaxy
    2.  ansible inventory
    3.  ansible-vault
    4.  ansible role
3.  What is the primary method for managing privilege escalation in Ansible?
    1.  Use of the ansible-galaxy command
    2.  Implementation of the become keyword
    3.  Configuration of the ansible.cfg file
    4.  Installation of the ansible-core package
4.  What is the main use of Ansible collections?
    1.  ansible-galaxy create-role
    2.  ansible-galaxy init
    3.  ansible-role new
    4.  ansible-init role

Answers

1\. a

2\. c

3\. b

4\. b

[Questions](#contents.xhtml_sc2_236a)

1.  What are the steps involved in installing Ansible on a control node using a Linux system and how does this setup differ when using a Windows system?
2.  Describe the process of managing inventory files in Ansible. What are the best practices for structuring these files for a scalable automation strategy?
3.  Explain how Ansible uses the ansible.cfg configuration file. What are some of the critical settings you might define in this file and why?
4.  Discuss the role of Ansible vault in managing sensitive data within playbooks. How does encrypting data enhance security in automation processes?
5.  How does Ansible manage privilege escalation on managed nodes? Explain the purpose and functionality of the become keyword in this context.
6.  Illustrate how you would convert a shell script into an Ansible playbook. What are the benefits of using playbooks over scripts in automated environments?
7.  What are Ansible roles and collections and how do they facilitate code reuse and automation scalability?
8.  Describe the purpose and use of the Molecule tool in Ansible role development and testing. What specific advantages does Molecule offer to Ansible developers?
9.  Explain the concept of execution environments within the Ansible automation platform. How do these environments standardize and simplify the management of automation tasks across different nodes?
10.  Detail the process and considerations for setting up Windows managed nodes in Ansible. What are the necessary configurations and components to ensure seamless automation?

[Key terms](#contents.xhtml_sc2_237a)

*   AppStream: The RHEL application stream repository is a software source in RHEL that offers a selection of the latest versions of applications and development tools allowing users to install newer software on a stable RHEL base without waiting for a new major release.
*   Jinja2: It is a Python tool integrated in Ansible that lets us create flexible templates for automatically filling in data in file or code which makes it easy to generate customized content based on specific information.
*   ansible-navigator: it is a command line interface tool designed to help users and developers efficiently run, explore and manage their Ansible automation content including playbooks, inventories and collections.
*   System role: System roles are pre-packaged Ansible roles that automate and standardize the setup and configuration of RHEL software and system settings.
*   Ansible vault: This is a feature in Ansible that allows users to encrypt sensitive data such as passwords and keys, making it secure for the storage and management of confidential information within Ansible playbooks, roles and inventory files.
*   Ansible Galaxy: Ansible Galaxy is a repository for sharing and managing Ansible roles and collections, allowing users to download pre-made configurations and integrate them into their own Ansible playbooks to streamline automation tasks.
*   Ansible role: It is a structured way to group together and encapsulate tasks, variables, files and templates that are designed to configure a specific service or function, making it reusable and easily distributable across different playbooks.
*   Ansible collection: It is a package format for distributing Ansible content including roles, plugins and modules which allows for easy sharing, versioning and use of complex Ansible solutions.
*   Automation hub: It is a centralized platform provided by Red Hat that allows users to access, manage and share certified Ansible content including collections and roles to standardize automation practices across their organization.

* * *

[1](#ch05.xhtml_footnote-002-backlink) [https://brew.sh/](https://brew.sh/)

[2](#ch05.xhtml_footnote-001-backlink) [https://linux-system-roles.github.io](https://linux-system-roles.github.io)

[3](#ch05.xhtml_footnote-000-backlink) [https://github.com/redhat-cop/automation-good-practices](https://github.com/redhat-cop/automation-good-practices)

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 6Network Services and Security Introduction](#contents.xhtml_ch06a)

[Introduction](#contents.xhtml_sc2_238a)

In today's digital age, network services' security and efficiency are paramount to any organization's success. This chapter focuses on the critical components of network services and security within the RHEL operating system that is essential for ensuring that network communications are both robust and secure. As RHEL continues to be a preferred platform for enterprise environments, understanding how to manage and secure network services on RHEL enhances system performance and protects data against evolving threats.

We will explore various network services integral to RHEL and discuss methodologies to secure these services effectively. Topics include configuring and optimizing common network services, implementing firewall and routing strategies and an in-depth look at securing connections using advanced cryptographic techniques. Additionally, this chapter will cover best practices for monitoring network traffic and detecting security breaches which are crucial for maintaining the integrity and confidentiality of organizational data.

By mastering the concepts presented in this chapter, readers will be equipped to configure, manage and secure network services expertly in an RHEL environment therefore, supporting their organization's network infrastructure and safeguarding it against vulnerabilities.

[Structure](#contents.xhtml_sc2_239a)

The chapter covers the following topics:

*   Dual stack
*   Security
*   Services
*   Firewalld
*   OpenSSH
*   SELinux
*   Best practices
*   Podman

[Objectives](#contents.xhtml_sc2_240a)

By the end of this chapter, we will learn how to configure our system with dual stack networking in RHEL so that we can interact with systems using the IPv4 and IPv6 network stacks. Security is more important in today’s world as the need for remote working is crucial, especially after the COVID-19 pandemic. We are going to explore the Security-Enhanced Linux (SELinux) security framework for granting granular permission in RHEL. We will configure the networking efficiently, set up and troubleshoot SELinux and activate secure services in our boxes.

[Dual stack](#contents.xhtml_sc2_241a)

Configuring dual stack networking on RHEL allows for simultaneous support of IPv4 and IPv6 on network interfaces ensuring compatibility and scalability with evolving network infrastructures. A practical example of setting up dual stack on a network interface involves editing the network interface's configuration file. Suppose the interface we want to configure is eth0. We would start by opening the configuration file located at /etc/sysconfig/network-scripts/ifcfg-eth0. In this file, we would specify both IPv4 and IPv6 addresses, gateways and other relevant settings.

Following is an example of what the configuration looks like:

DEVICE=eth0

BOOTPROTO=static

ONBOOT=yes

IPADDR=192.168.1.100

NETMASK=255.255.255.0

GATEWAY=192.168.1.1

IPV6INIT=yes

IPV6_AUTOCONF=no

IPV6ADDR=2001:db8:0:1::100/64

IPV6_DEFAULTGW=2001:db8:0:1::1

In this configuration, IPADDR, NETMASK and GATEWAY provide the settings for IPv4, while IPV6INIT, IPV6_AUTOCONF, IPV6ADDR and IPV6_DEFAULTGW are used to set up IPv6\. The IPV6INIT=yes line enables IPv6 on the interface and IPV6_AUTOCONF=no disables the automatic configuration of IPv6 addresses through router advertisements which is useful if we want static addressing.

After making these changes, restart the network service or the interface to apply the new settings as follows:

sudo systemctl restart network

We can restart the specific interface using the following:

sudo ifdown eth0 && sudo ifup eth0

This setup ensures that eth0 is capable of communicating over both IPv4 and IPv6 providing a robust configuration for supporting a dual-stack IP environment on our RHEL system.

[Routing](#contents.xhtml_sc3_242a)

In dual stack environments, where both IPv4 and IPv6 are supported, routing configurations must ensure that traffic is managed correctly for each protocol. RHEL uses routing tables that can store routes for both IPv4 and IPv6 and the system decides which protocol to use based on the destination address of the packets.

For IPv4, routing configurations typically include defining default gateways and network masks that segment the network into subnets. For IPv6, similar principles apply but with an emphasis on prefix lengths and the use of link local addresses for routing on local subnets. Following is an example of how to add a static route for IPv4 and IPv6 on RHEL:

IPv4 route example is as follows:

# ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0

IPv6 route example is as follows:

# ip -6 route add 2001:db8:0:2::/64 via 2001:db8:0:1::1 dev eth0

These commands add routes that direct traffic destined for the specified networks to go through the indicated gateways via the eth0 interface.

The traceroute tool is used to identify the path data takes to reach its destination which is crucial for troubleshooting network issues and understanding path dynamics in dual stack configurations.

To trace the route for an IPv4 address, we can use the following:

traceroute 192.168.1.100

For IPv6, the command changes slightly to accommodate the protocol, as follows:

traceroute6 2001:db8:0:1::100

These commands will output the series of hops that packets take from the source to the destination. Each line represents a hop, showing the IP address of the intermediary router, the hostname if available and the time packets take to get there. Understanding the output from traceroute can help network administrators diagnose where delays or drops in the network occur. For example, if packets are consistently lost or delayed at a particular hop, this might indicate a problem with that router or the link immediately preceding it.

Implementing effective routing strategies and regularly using tools like traceroute are fundamental practices for network administration in a dual stack RHEL environment. These tools assist in routine maintenance and troubleshooting and provide vital information for planning network expansions or migrations. By combining dual stack configurations with thorough routing and diagnostics, administrators can ensure their networks are resilient, future proof and optimized for current and next generation network traffic.

[Monitor](#contents.xhtml_sc3_243a)

Monitoring network traffic and detecting security breaches are critical components of maintaining the integrity and security of information systems, especially in environments powered by RHEL. Effective network monitoring involves continuously analyzing the traffic to detect unusual patterns that may indicate a security threat or breach. Tools such as tcpdump and wireshark are commonly used on RHEL systems for capturing and analyzing packets. These tools allow administrators to examine data packets in real-time or from saved files, providing insights into the types and volumes of traffic flowing through the network. For more automated monitoring, Nagios, Zabbix or Prometheus offer comprehensive solutions that can monitor network traffic and alert administrators about anomalies such as unexpected spikes in traffic, unauthorized access attempts or the presence of malware communication signatures. Detecting security breaches promptly is essential to minimize potential damage and commence remediation efforts.

The tcpdump command line tool is a powerful utility used on RHEL systems for capturing and analyzing network packets. Administrators can use tcpdump to filter and display the headers of packets on a particular network interface. Following is how you might use tcpdump to monitor traffic on the eth0 network interface for all Internet Control Message Protocol (ICMP) packets which are often used in network diagnostic activities:

# tcpdump -i eth0 icmp

This command captures and displays all ICMP packets that traverse the eth0 interface. To save the packet capture for later analysis, you can direct the output to a file, as follows:

# tcpdump -i eth0 icmp -w /path/to/savefile.pcap

While Wireshark is generally used with a graphical interface, it also offers a command line utility called tshark for capturing and analyzing packets. For instance, to capture HTTP traffic on the  eth0 interface, you can use the following:

# tshark -i eth0 -f "tcp port 80"

[Intrusion detection](#contents.xhtml_sc3_244a)

Intrusion Detection Systems (IDS) like Snort or Suricata can be deployed on RHEL to monitor network traffic for signs of malicious activities. These systems compare network traffic against a database of known attack signatures and anomalous traffic patterns to flag potential threats.

Snort is an open-source Network Intrusion Detection System (NIDS) capable of performing real-time traffic analysis and packet logging on IP networks. The basic set up of Snort for monitoring network traffic and generating alerts for any anomalies detected involves defining the network variables in Snort’s configuration file (/etc/snort/snort.conf), as follows:

ipvar HOME_NET 192.168.1.0/24

ipvar EXTERNAL_NET !$HOME_NET

We can run Snort in network intrusion detection mode with console logging, as follows:

# snort -c /etc/snort/snort.conf -i eth0 -A console

This command configures Snort to monitor the eth0 interface using the specified configuration file and outputs alerts to the console.

[Log management and analysis](#contents.xhtml_sc3_245a)

Security Information and Event Management (SIEM) solutions such as Splunk or Elasticsearch, Logstash, and Kibana (ELK) Stack are instrumental on RHEL servers. They aggregate logs from various system components and network devices providing a centralized view of the security state of the network. This holistic view helps in quickly pinpointing the sources of security breaches, understanding the scope of an attack and implementing effective countermeasures. These tools and practices form the backbone of a proactive security posture in RHEL environments ensuring that threats are identified and addressed before they can cause significant harm.

For a comprehensive solution that involves log collection, visualization and alerting, the ELK Stack is highly effective. Following is how you might start collecting logs with Logstash, visualize them with Kibana and store them in Elasticsearch:

Configure Logstash (/etc/logstash/conf.d/logstash.conf) to collect syslogs:

input {

syslog {

port => 514

}

}

output {

elasticsearch {

hosts => ["localhost:9200"]

}

}

Start the Logstash service, as follows:

# systemctl start logstash

Access Kibana through your web browser to create dashboards and visualize the data collected by Logstash and stored in Elasticsearch.

These command line examples offer practical insights into setting up and using advanced monitoring and intrusion detection tools on RHEL systems. By implementing these strategies, administrators can enhance their capabilities in network traffic analysis and security breach detection, ensuring robust security measures are in place.

[Security](#contents.xhtml_sc2_246a)

Managing security on RHEL involves several key areas including user management, access controls, software management and network security.

[User and group management](#contents.xhtml_sc3_247a)

Managing users and groups effectively is foundational to maintaining a secure and well-functioning RHEL environment. Proper user and group management ensures that only authorized individuals can access specific system resources, reducing the risk of unauthorized access and potential security vulnerabilities. Use the following commands to interact with the system:

*   User management: Use commands like useradd, usermod, and userdel to manage user accounts. Set strong password policies and enforce them using Pluggable Authentication Modules (PAM).
*   Group management: Utilize groupadd, groupmod, and groupdel to manage group memberships and permissions.

    User password expiration is as follows:

    chage -M 90 -m 7 -W 14 username

    This command sets a password to expire after 90 days with a minimum of seven days between changes and a warning issued 14 days before expiration.

[File system security](#contents.xhtml_sc3_248a)

Setting the correct permissions and ownerships on files and directories is crucial. Following are the most common operations and commands:

*   Permissions: Use chmod, chown and chgrp to set appropriate permissions and ownerships.
*   ACLs: Extend traditional permissions with ACLs for finer grained control using setfacl and getfacl, as follows:

    setfacl -m u:username:rw file.txt

    Grants read and write access to file.txt for username.

[SELinux management](#contents.xhtml_sc3_249a)

SELinux adds an additional layer of security mechanisms to restrict processes. Following are the most common use cases:

*   Enforcement modes: Toggle between enforcing, permissive and disabled modes depending on our needs.
*   Manage contexts: Use chcon and restorecon to manage file contexts and ensure proper SELinux settings.
*   Booleans: Tweak SELinux policies using Booleans to enable or disable specific functionalities without modifying policies.

[Network security](#contents.xhtml_sc3_250a)

Securing network services and implementing firewall rules are vital. Use the following tools to configure and interact with the system:

*   Firewall configuration: Use firewall-cmd (or iptables on older systems) to manage firewall settings. Ensure only necessary ports and services are exposed.

    These commands permanently allows HTTPS traffic through the firewall as follows:

    firewall-cmd --permanent --add-service=https

    firewall-cmd –reload

*   Secure Shell (SSH):  Modify /etc/ssh/sshd_config for secure SSH configurations like disabling root login and specifying allowed users.

    Restrict SSH access to the user username, as follows:

    echo 'AllowUsers username' >> /etc/ssh/sshd_config

    systemctl restart sshd

*   Fail2ban: Implement Fail2ban to block suspicious IP addresses after certain thresholds of failed login attempts.

[Software package security](#contents.xhtml_sc3_251a)

Keeping software up to date is one of the most effective security measures. Use the following commands to manage the system:

*   YUM or DNF: Use Yellowdog Updater, Modified (YUM) or DNF tools to install, update and remove packages securely. Regularly apply security patches and updates.
*   Repository management: Configure and secure software repositories to prevent installation of unauthorized packages. Use the yum-config-manager command.

[Monitoring and logs](#contents.xhtml_sc3_252a)

Regular monitoring and auditing can preempt security breaches. Following are the principal commands that interact with the system:

*   auditd: Utilize the Linux Audit daemon (auditd) to monitor and log security-relevant events.
*   syslog and journalctl: Review system logs with syslog or journalctl to spot unusual activities.

[Backup and recovery](#contents.xhtml_sc3_253a)

Implement robust backup procedures to recover from data loss or corruption. Following are the most used techniques:

*   Backup tools: Use tools like rsync, tar, dump, and restore for data backup.
*   Automated backups: Schedule regular backups using cron jobs to ensure data redundancy.

[System updates and patches](#contents.xhtml_sc3_254a)

Regularly update the system to patch known vulnerabilities. We can use the following tools:

*   Automatic updates: Configure automatic security updates with yum-cron or dnf-automatic.
*   Security scanners: Use tools like OpenSCAP for vulnerability assessments based on security guides and standards.

These actions, combined with vigilant monitoring and regular audits, will significantly enhance the security posture of our RHEL systems.

Detecting security breaches promptly is essential to minimize potential damage and commence remediation efforts. IDS like Snort or Suricata can be deployed on RHEL to monitor network traffic for signs of malicious activities. To flag potential threats. These systems compare network traffic against a database of known attack signatures and anomalous traffic patterns. Additionally, SIEM solutions, such as Splunk or ELK  stack, are instrumental in RHEL servers. They aggregate logs from various system components and network devices providing a centralized view of the security state of the network. This holistic view helps quickly pinpoint the sources of security breaches, understand the scope of an attack, and implement effective countermeasures. These tools and practices form the backbone of a proactive security posture in RHEL environments ensuring that threats are identified and addressed before they can cause significant harm.

[Services](#contents.xhtml_sc2_255a)

Network services in RHEL are foundational to its operations allowing for network communication and data exchange between computers and devices. These services are built upon the Transmission Control Protocol/Internet Protocol (TCP /IP) stack which defines how data is formatted, addressed, transmitted, routed and received at the destination. RHEL uses various daemon services like httpd for web servers, sshd for secure shell services and dhcpd for network management through Dynamic Host Configuration Protocol (DHCP). Each of these services is configurable through system scripts and managed by systemd, RHEL's system and service manager, providing robust control and the ability to fine-tune network characteristics according to the needs of the enterprise. Managing network security in RHEL involves configuring firewalls, monitoring network traffic and securing data transmissions. The default firewall management tool on RHEL is firewalld, which provides a dynamically managed firewall with support for network or firewall zones that define the trust level of network connections or interfaces. It uses zones and services to simplify the configuration process where each zone corresponds to a different security level and contains network interfaces and sources along with allowed services and ports. Additionally, RHEL employs SELinux  to enforce security policies, including mandatory access controls, further protecting the network from unauthorized access or breaches.

[Firewalld](#contents.xhtml_sc2_256a)

Firewalld is a dynamic firewall management tool available on various Linux distributions including RHEL and its derivatives. It provides a more flexible and configurable firewall solution than the static interfaces provided by other tools like iptables. Firewalld uses zones and services to manage and control network traffic.

We can control network connections to services via the console or using firewalld with an Ansible playbook, as follows.

The playbook will include ensuring firewalld is installed and running, configuring firewall settings for specific services and managing the default zone settings.

This playbook demonstrates how to manage firewall settings for HTTP, HTTPS and SSH services and disable FTP, as follows:

---

- name: Configure and Manage Firewalld

hosts: all

become: true

tasks:

- name: Ensure firewalld is installed

ansible.builtin.package:

name: firewalld

state: present

- name: Start and enable firewalld

ansible.builtin.service:

name: firewalld

state: started

enabled: yes

- name: Enable HTTP and HTTPS services on the default zone

ansible.builtin.firewalld:

service: "{{ item }}"

state: enabled

permanent: true

immediate: true

loop:

- http

- https

- name: Ensure SSH service is allowed

ansible.builtin.firewalld:

service: ssh

state: enabled

permanent: true

immediate: true

- name: Block a specific IP address

ansible.builtin.firewalld:

source: "192.168.100.100"

state: drop

zone: public

permanent: true

immediate: true

- name: Remove FTP service from the default zone

ansible.builtin.firewalld:

service: ftp

state: disabled

permanent: true

immediate: true

[Key components](#contents.xhtml_sc3_257a)

Following are the key tools to manage the security posture of our systems:

*   Firewalld installation and activation: Ensures that firewalld is installed on the target hosts and starts the service, setting it to enable on boot.
*   Service management: Enables services like HTTP, HTTPS and SSH by modifying the default zone (typically the public zone). This allows incoming traffic for these services.
*   Blocking specific IP: Adds a rule to drop all traffic from a specific IP address. This is useful for security purposes when certain IPs are identified as sources of malicious activity.
*   Immediate changes: The immediate, true parameter applies changes immediately without needing to restart the firewalld service.
*   Removing services: Disables a service like FTP by removing it from the allowed services in the default zone. This is useful when we want to tighten security by limiting the services that can receive incoming connections.

This playbook allows for dynamic management of network policies related to how services are exposed on a server, enhancing the server's security posture by controlling access through firewalld.

[OpenSSH](#contents.xhtml_sc2_258a)

Configuring and securing the OpenSSH service on RHEL involves more than just enabling remote access. It requires setting up key-based authentication to replace less secure password-based methods, defining security policies for SSH and configuring the daemon options in the /etc/ssh/sshd_config file. Common security measures include disabling root login, specifying allowed users and setting idle timeout values. Moreover, using SSH keys enhances security by providing a cryptographic handshake that verifies the identity of the connection parties. RHEL also supports advanced SSH configurations like using two factor authentication and port forwarding which further secures the SSH service against potential intrusions.  Following is a breakdown of some of the most used options:

*   Port:
    *   Description: Specifies the port number that sshd will listen on for incoming connections.
    *   Common usage: Changing the default port (22) to a non-standard port can help obscure our SSH service from automated scans.
*   PermitRootLogin:
    *   Description: Controls whether the root user can log in using SSH.
    *   Common usage: Often set to no to disallow root login for security reasons; sometimes configured as without-password to permit root login only with key-based authentication, enhancing security.
*   PasswordAuthentication:
    *   Description: Specifies whether password authentication is allowed.
    *   Common usage: Set to no to disable password authentication, requiring all users to employ key-based authentication, which is more secure against brute force attacks.
*   PubkeyAuthentication:
    *   Description: Enables or disables public key authentication.
    *   Common usage: Typically set to yes to allow users to authenticate using SSH keys instead of or in addition to passwords.
*   ChallengeResponseAuthentication:
    *   Description: Enables challenge response authentication (e.g., one-time passwords).
    *   Common usage: Generally, set to no unless specific challenge-response systems are employed.
*   X11Forwarding:
    *   Description: Determines whether SSH clients are allowed to forward X11 graphical display from the server.
    *   Common usage: Usually set to yes if users need to run graphical applications over SSH, otherwise, it is safer to set it to no to prevent exposing the X11 system to additional security risks.
*   LogLevel:
    *   Description: Defines the verbosity of the messages logged by sshd.
    *   Common usage: Typically set to INFO or VERBOSE to capture a detailed log without being overly verbose. It is useful for monitoring and troubleshooting.
*   UsePAM:
    *   Description: Enables or disables PAM  integration.
    *   Common usage: Usually enabled (yes) to integrate with the system's PAM configuration for additional authentication flexibility and control.
*   Subsystem SFTP:
    *   Description: Specifies the subsystem and command for Secure File Transfer Protocol (SFTP).
    *   Common usage: Configured to use an internal SFTP server or a specific path to an SFTP server executable providing secure file transfer capabilities over SSH.
*   UseDNS:
    *   Description: Specifies whether SSHD should look up the remote hostname and check that the resolved hostname for the remote IP address maps back to the same IP address.
    *   Common usage: Often set to no to speed up logins and to avoid delays during authentication when Domain Name System (DNS) services are slow or misconfigured.

These options are frequently adjusted to balance security requirements with functionality ensuring that the SSH service operates effectively while maintaining the necessary security posture for the environment.

These are the common settings to enable the key-based authentication and disabling password-based authentication on the OpenSSH server in the /etc/ssh/sshd_config file, as follows:

PasswordAuthentication no

ChallengeResponseAuthentication no

UsePAM no

PermitRootLogin no

After modifying the configuration, restart the SSH service to apply the changes, as follows:

# systemctl restart sshd

To ensure that the setup is correct, try logging into the RHEL server from our client machine using verbosity mode to see the key exchange. Multiple -v options increase the verbosity, as follows:

ssh -vvv username@server_ip_address

Using key-based authentication not only strengthens security but also facilitates easier management and automation for administrators. Remember, always keep our private keys secure and manage permissions appropriately. For increased security, consider implementing additional measures like using a passphrase with our SSH keys and setting up SSH agent forwarding. We can execute the SSH agent forwarding in any terminal, as follows:

eval "$(ssh-agent -s)"

After starting the SSH agent, add our SSH private key to the agent. This allows the agent to manage our key and we do not need to enter our passphrase every time we use the SSH key during the current session.

ssh-add ~/.ssh/id_rsa

Ensure that the user SSH configuration file ~/.ssh/config enables the usage of the SSH agent, as follows:

Host *

ForwardAgent yes

The SSH agent forwarding enables us to connect to another server using the same SSH keys from the server we are currently connected to.

[SELinux](#contents.xhtml_sc2_259a)

An important security feature of RHEL is SELinux. It is an additional layer of system security. It enables permission granting at a very granular level. We can verify the current SELinux mode using the getenforce tool, as follows:

# getenforce

Enforcing

The setenforce command line utility changes the current SELinux mode. The most common are Enforcing for production environment and Permissive used prevalently in development environments, as follows:

# setenforce Enforcing

Alternatively, we can use the Enforcing kernel parameter at boot time with permitted values one and zero. It is not advisable to completely bypass SELinux using the selinux=0 kernel parameter. Obviously, the default value of the SELinux kernel parament is one. Another way to configure SELinux is via the /etc/selinux/config configuration file. Two values are important in this file SELINUX and SELINUXTYPE. The SELINUX=enforcing value for production environments controls the security policies. The possible values are enforcing, permissive and disabled. The default for the SELINUXTYPE=targeted for the production environment is to protect every target process. Alternative values are minimum for only selected processes or mls for multi-level security protection. Every change to this configuration file requires a system restart to become active.

The most common way to interact with SELinux is via policy or Boolean settings. SELinux extends the protection to some cornerstone scenarios not covered by the traditional Linux user and group permission system. For example, restricting the read or write permission to only one program. SELinux is founded on a set of policies for each application. There is a policy that defines exactly what actions and access are expected by every binary executable, configuration file and data to make our application run. AppArmor is another canonical technology used in Ubuntu Linux.

SELinux is object based and controlled by a sophisticated rule known as mandatory access control. Without SELinux, a malicious user can compromise a system by using a vulnerability. The Apache HTTPD web server was in the past very sensitive to this type of attack as the compromised process may grant Linux permission to all the resources accessible to apache user and apache group including but not only to /var/www/html, /tmp and /var/tmp. Incidents like this might escalate to data leaks or privilege escalation. Whereas SELinux labels with a SELinux context every file, process, directory and port of the system. By default, the policy disallows any interaction till a rule allows it.

[Table 6.1](#ch06.xhtml_tab6-1) shows the SELinux context for files and directories interacting with the web server type context httpd_t:

| SELinux user | unconfirmed_u |
| Role | object_r |
| Type | httpd_sys_content_t |
| Sensitivity level | S0 |
| File | /var/www/html/index.html |

Table 6.1: SELinux file context

This is the typical Linux, Apache, MariaDB, PHP (LAMP) with this configuration. The HTTPD Apache web service has a type context of httpd_t. The SELinux context of the directory /var/www/html is httpd_sys_content_t. The SELinux context of the directory /tmp is tmp_t. The web server port is http_port_t. The database MariaDB service has the mysqld_t type context. By default, the data in /data/mysql have the mysqld_db_t type context. This type of context allows MariaDB access to those files but disables access by other services, such as the Apache web service.

We can analyze the SELinux context appending the Z parameter to most command line tools like: ps, ls, cp, and mkdir.

[Change SELinux contexts](#contents.xhtml_sc3_260a)

The chcon command changes the SELinux context of files and directories. It is useful for temporary changes as they do not survive a full relabel or the execution of restorecon. For example, if we want to change the SELinux context type of a file named custom_app_data.txt to httpd_sys_content_t to make it accessible by the Apache HTTP server, we would use the following:

chcon -t httpd_sys_content_t custom_app_data.txt

This command only changes the type part of the context. We can also change the user, role, and type fully using the -u, -r and -t options, respectively as follows:

chcon -u system_u -r object_r -t httpd_sys_content_t custom_app_data.txt

[Restore default SELinux contexts](#contents.xhtml_sc3_261a)

The restorecon command line tool resets the SELinux context of files and directories to their default values based on the SELinux policy and file context configurations stored in /etc/selinux/targeted/contexts/files/file_contexts, as follows:

To restore the default SELinux context of the custom_app_data.txt file, as follows:

restorecon custom_app_data.txt

To recursively restore SELinux contexts for all files and directories within a directory such as /var/www/html, use the following:

restorecon -Rv /var/www/html

The -R option makes the command recursive, and -v makes it verbose providing the detailed output of what restorecon is changing.

[Ansible SELinux](#contents.xhtml_sc3_262a)

Ansible use the pure Python selinux library to execute any action on our system related to SELinux. This library is usually installed in our system via the python-selinux package. The following Ansible playbook is designed to configure security settings on RHEL servers. It requires the ansible.posix Ansible collection installed in the system.

The ansible.posix collection included in RHEL and Fedora as follows:

dnf install ansible-collection-ansible-posix

The full Ansible playbook looks as follows:

---

- name: RHEL Security Management

hosts: all

become: true

vars:

user_name: "secureuser"

user_password: "{{ 'securepassword' | password_hash('sha512') }}"

tasks:

- name: Ensure a secure user is present

ansible.builtin.user:

name: "{{ user_name }}"

password: "{{ user_password }}"

comment: "Secure User"

- name: Ensure SSH root login is disabled

ansible.builtin.lineinfile:

path: /etc/ssh/sshd_config

regexp: '^PermitRootLogin'

line: 'PermitRootLogin no'

notify: restart sshd

- name: Ensure SELinux is set to enforcing

ansible.posix.selinux:

policy: targeted

state: enforcing

- name: Ensure firewalld is installed

ansible.builtin.package:

name: firewalld

state: present

- name: Start and enable firewalld

ansible.builtin.service:

name: firewalld

state: started

enabled: yes

- name: Add ssh service to firewalld

ansible.builtin.firewalld:

service: ssh

permanent: yes

state: enabled

- name: Ensure auditd is installed

ansible.builtin.package:

name: audit

state: present

- name: Ensure auditd service is running and enabled

ansible.builtin.service:

name: auditd

state: started

enabled: yes

handlers:

- name: restart sshd

ansible.builtin.service:

name: sshd

state: restarted

It automates several critical security configurations to ensure that the RHEL servers adhere to certain security standards, as follows:

*   User management: Ensures a user (defined by user_name) is present on the system with a password set to user_password and a description of secure user. This helps in maintaining a specific and secure user account for administrative or specialized tasks.
*   SSH configuration: Modifies the SSH configuration to disable root login (PermitRootLogin no). This is a security best practice that prevents direct root access via SSH. A handler named restart SSHD is notified to restart the SSH service to apply this configuration change.
*   SELinux configuration: Ensures that SELinux is set to enforcing mode with a targeted policy.
*   Firewall configuration, with firewalld: Ensures the firewalld package is installed and the service is started and enabled on boot. This task sets up a basic firewall to manage network access. Adds the SSH service to the firewalld rules ensuring that SSH traffic is allowed through the firewall. This is crucial for remote management while keeping the server secure.
*   Audit system configuration: Install and ensure that the auditd service which is responsible for logging security events such as login attempts and file modifications, is in running and enabled status. This is essential for security auditing and compliance.

[SELinux Booleans](#contents.xhtml_sc3_263a)

We can control network connections using SELinux Boolean settings and create or modify policy modules to define custom access controls. The following playbook demonstrates how we enable the NGINX web service with network access:

---

- name: Configure SELinux for Network Services Control

hosts: all

become: true

tasks:

- name: Ensure SELinux is set to enforcing mode

ansible.posix.selinux:

state: enforcing

- name: Allow NGINX to connect to the network

ansible.posix.seboolean:

name: nginx_can_network_connect

state: yes

persistent: yes

- name: Restrict SNMP network access

ansible.posix.seboolean:

name: snmpd_can_talk_tcp

state: no

persistent: yes

Following are the key components:

*   SELinux is enabled and in enforcing mode.
*   It enables the SELinux Boolean value to permit the connection to the NGINX service. Specifically, the value nginx_can_network_connect allows scripts and modules running within NGINX to make network connections.

This code needs to be adjusted based on the specific permissions and interactions our service requires.

[Custom policies](#contents.xhtml_sc3_264a)

The playbook demonstrates how to compile a type enforcement file myservice.te, package it, and install it for a custom SELinux policy. These policies enable us to control over service interactions with the network beyond what is available through Booleans. The .te files (type enforcement) specify the SELinux rules. The myservice.te file in the context of SELinux refers to a Type Enforcement (TE) file. This file defines the SELinux policy module for a specific service or application, myservice in this case. It specifies the security rules that govern the access permissions for processes associated with that service. Creating a .te file involves specifying types, type transitions and rules that define how subjects (like processes) can access objects (like files, sockets, etc.) under SELinux's mandatory access control policies.

Following is an example of what a basic myservice.te file might look like, demonstrating how to define a simple SELinux policy module for a hypothetical service. This service might require permission to read and write files in a specific directory and connect to the network:

module myservice 1.0;

require {

type myservice_t;

type myservice_var_t;

type http_port_t;

class process { fork transition signal };

class file { getattr read write open };

class tcp_socket { name_connect };

}

allow myservice_t myservice_var_t:file { getattr read write open };

allow myservice_t http_port_t:tcp_socket name_connect;

type_transition myservice_t myservice_var_t:process myservice_t;

[Components in myservice.te](#contents.xhtml_sc3_265a)

Following are the components in myservice.te:

*   module: Defines the module name and version.
*   require: Declares the types and classes of operations that the policy module requires. These types are predefined in the SELinux policy or must be declared in the same or other policy modules.
*   myservice_t: It is the SELinux type associated with the service's processes.
*   myservice_var_t: It is the type of file used by the service.
*   http_port_t: It is a common SELinux type for HTTP network ports.
*   class: Specifies the kinds of operations or actions controlled by SELinux such as reading files or making network connections.
*   allow: Rules that permit specific interactions between types such as allowing the service process type (myservice_t) to connect to HTTP ports or read or write certain files.
*   type_transition: Defines what happens when a process of one type creates a new process or object; in this case, when myservice_t creates a new process, it transitions to myservice_t.

[Steps](#contents.xhtml_sc3_266a)

Following are the steps to use the myservice.te file:

1.  Compile the policy: Use tools like checkmodule to compile the .te file into a .mod (module) file, as follows:

    - name: Compile and install custom SELinux policy

    ansible.builtin.command:

    cmd: checkmodule -M -m -o myservice.mod myservice.te

    register: compile_result

2.  Package the module: Use semodule_package to create a .pp (policy package) file from the .mod file, as follows:

    - name: Create SELinux policy package

    ansible.builtin.command:

    cmd: semodule_package -o myservice.pp -m myservice.mod

    when: compile_result is changed

3.  Load the module: Use semodule -i to install the policy package into the SELinux policy, as follows:

    - name: Install SELinux policy module

    ansible.builtin.command:

    cmd: semodule -i myservice.pp

    when: compile_result is changed

Working with SELinux requires a good understanding of the security needs of our application and the principles of SELinux policy management.

[Best practices](#contents.xhtml_sc2_267a)

The adoption of the following system security best practices maintains our system up-to-date and future proof:

*   Regular updates: Regularly update the operating system and all installed software to ensure that security patches are applied. This reduces the risk of exploitation through known vulnerabilities.
*   Principle of least privilege: Ensure that users and applications operate using the minimal level of access necessary. This limits the potential impact of a security breach.
*   Strong authentication mechanisms: Use multi-factor authentication (MFA) wherever possible to enhance security beyond simple username and password authentication.
*   Secure configuration: Harden systems by disabling unnecessary services, securing network ports and applying secure configuration guidelines.
*   Regular audits and monitoring: Implement logging and monitoring to promptly detect and respond to potential security incidents. Regular security audits are also essential to identify and mitigate risks.
*   Backup and disaster recovery: To ensure business continuity in the event of a security incident, maintain regular backups of important data and test disaster recovery procedures.

[Secure Sockets Layer](#contents.xhtml_sc3_268a)

Secure Sockets Layer (SSL) security is essential for protecting data in transit between clients and servers. While SSL has been largely superseded by Transport Layer Security (TLS), the term SSL is still commonly used to refer to both protocols. These security measures ensure the confidentiality, integrity and authentication of data communications over networks such as the Internet. Following is an overview of key components in SSL or TLS security:

SSL or TLS utilizes encryption algorithms to secure data transmitted between two parties ensuring that unauthorized entities cannot read the data even if it is intercepted. It provides a mechanism for clients and servers to authenticate each other's identities using digital certificates issued by trusted Certificate Authorities (CAs). Additionally, SSL or TLS employs Message Authentication Codes (MACs) to maintain the integrity of the data ensuring that any alterations to the data during transit are detected. Following are the best recommendations for success with SSL or TLS:

*   Use strong protocols: To protect against vulnerabilities, only enable strong protocols such as TLS 1.2 and TLS 1.3 while disabling older protocols like SSL 2.0, SSL 3.0 and TLS 1.0/1.1.
*   Strong cipher suites: Configure servers to use strong cipher suites that do not include known weak algorithms like RC4 or MD5\. Prioritize cipher suites that support forward secrecy.
*   Certificate management: Use certificates from a trusted CA and track certificate expiration dates to avoid service disruptions and potential security risks.
*   Regularly update SSL or TLS libraries: Keep SSL or TLS libraries up-to-date to mitigate vulnerabilities that attackers could exploit.
*   SSL or TLS server configuration: Regularly test SSL or TLS configurations using tools like SSL labs' SSL test to ensure the server is configured securely and identify potential improvements.
*   HTTP Strict Transport Security (HSTS): Implement HSTS to ensure that browsers only connect to the server using HTTPS preventing SSL stripping attacks.
*   OCSP stapling: Enable Online Certificate Status Protocol (OCSP) stapling to improve the efficiency of the OCSP protocol and enhance privacy for the end users.

[MD5 and SHA-1 sunset](#contents.xhtml_sc3_269a)

The sunsetting of Message-Digest Algorithm 5 (MD5) and Secure Hash Algorithm 1 (SHA-1) represents a critical shift in cryptographic practices due to their vulnerabilities to various attacks, compromising digital communications' security and data integrity. These hash functions have been foundational in many security protocols and applications but are now considered unsafe for continued use.

[MD5 vulnerabilities and sunsetting](#contents.xhtml_sc4_270a)

MD5 has been deprecated due to its susceptibility to collision attacks where two different inputs produce the same output hash. This flaw can be exploited in security sensitive contexts such as SSL or TLS certificates and code signing where integrity and authenticity are critical. The speed at which collisions can be generated with modern computing power has rendered MD5 obsolete for security purposes. Despite this, MD5 is still used in less critical applications like checksums for file integrity verification where security is not the primary concern.

[SHA-1 vulnerabilities and sunsetting](#contents.xhtml_sc4_271a)

SHA-1 has been a widely used hash function in cryptographic protocols including TLS, SSL, PGP and SSH. However, it has similar vulnerabilities to MD5\. Theoretical attacks on SHA-1 were identified several years ago and practical attacks have become more feasible over time due to increased computational power and cryptographic research advancements. A significant milestone in the sunsetting of SHA-1 was Google's demonstration of a practical collision attack in 2017, dubbed SHAttered, which forcefully drove the industry towards more secure alternatives.

[Implications of hash function sunsetting](#contents.xhtml_sc3_272a)

The transition away from MD5 and SHA-1 impacts various areas, as follows:

*   Digital certificates: The use of SHA-1 in digital certificates has been phased out with web browsers and certificate authorities switching to SHA-256 which is part of the SHA-2 family and offers significantly better security without known practical vulnerabilities.
*   Code signing: Software development and distribution often rely on code signing to verify the integrity and origin of code. The transition to SHA-256 for code signing eliminates the risks of attackers creating a malicious executable with the same hash as a legitimate application.
*   Data integrity checks: While less critical applications might still use MD5 for simplicity and speed in verifying data integrity, more secure alternatives are recommended even in these contexts to prevent potential vulnerabilities.

Organizations and developers are advised to update cryptographic practices by replacing MD5 and SHA-1 with SHA-256 or SHA-3 in all cryptographic operations to provide stronger security, audit and update systems to ensure cryptographic standards no longer use outdated functions, educate and train all relevant stakeholders on these updated practices, and implement robust security policies that mandate the use of secure, up-to-date cryptographic standards for new software development and system implementations.

[Podman](#contents.xhtml_sc2_273a)

Podman is an open source, Linux native tool for managing containers and container images, and it has become a preferred solution in RHEL due to its security, simplicity, and rootless operation. Unlike Docker, which relies on a background daemon, Podman operates without requiring a running service, offering administrators more granular control over container processes. Containers in Podman are treated as standard Linux processes, which can be managed using familiar Linux utilities like ps, top, or kill. One of Podman’s standout features is its support for rootless containers, allowing non-privileged users to create and manage containers without needing root access. This enhances security by reducing the attack surface, especially in multi-user environments where isolated workloads are necessary. Additionally, Podman adheres to the Open Container Initiative (OCI) standards, ensuring compatibility with other container runtimes and registries. Users can easily pull images from sources like Docker Hub or Red Hat’s container registries and run them with Podman without modification.

*   Pulling an image from Docker Hub:

    podman pull nginx

*   Running a container with the pulled image:

    podman run -d --name mynginx -p 8080:80 nginx

*   Listing running containers:

    podman ps

Another important feature is Podman’s ability to manage pods, a concept that allows users to run and manage groups of containers as a single unit, similar to Kubernetes. This is particularly useful in microservice environments, where multiple containers need to share network namespaces and work together seamlessly.

*   Create a new pod:

    podman pod create --name mypod --publish 8080:80

*   Run two containers inside the pod:

    podman run -dt --pod mypod nginx

    podman run -dt --pod mypod redis

*   List containers in the pod:

    podman ps --pod

In terms of security, Podman integrates closely with SELinux, enforcing security contexts that ensure containers operate within their intended boundaries. SELinux policies in RHEL can be used to apply strict controls over container processes, preventing unauthorized access to system resources.

Podman automatically assigns SELinux labels to containers and their processes. To check the security context of a container, you can run the following:

*   Check the security context of the container

    podman inspect --format '{{.ProcessLabel}}' mynginx

This will output the SELinux security label applied to the container, helping ensure that the container complies with SELinux policies.

Podman’s command syntax mirrors Docker’s, making it easy for users transitioning from Docker to use Podman with little to no learning curve. Commands like podman pull, podman run, and podman ps function similarly to their Docker counterparts, ensuring a smooth transition for administrators. Moreover, Podman maintains high compatibility with the Docker CLI, allowing users to alias the Docker command to Podman without impacting workflows.

Docker CLI alias for Podman:

*   Set Docker alias to use Podman commands:

    alias docker=podman

*   Now you can use Docker commands:

    docker run -d nginx

    docker ps

Another advanced feature of Podman is its integration with systemd, the system and service manager used in RHEL 9\. Podman containers can be managed like systemd services, enabling easy container startup at boot and allowing for seamless management of containers within the systemd framework.

Generating systemd unit file for a container:

*   Generate a systemd unit file for an existing container:

    podman generate systemd --name mynginx --files –new

*   Copy the generated file to the systemd directory and enable it:

    cp container-mynginx.service /etc/systemd/system/

    systemctl enable container-mynginx.service

    systemctl start container-mynginx.service

Podman’s networking capabilities, which include support for custom networks and network namespaces, allow users to create isolated networking environments for their containers. This feature is particularly important in rootless mode, where isolated networking configurations are necessary for secure, multi-tenant environments.

Following are the ways for creating a custom network and attaching containers:

*   Create a custom network:

    podman network create mynetwork

*   Run containers attached to the custom network:

    podman run -dt --network mynetwork --name web nginx

    podman run -dt --network mynetwork --name db redis

*   Inspect the network:

    podman network inspect mynetwork

Podman Compose is another useful tool that allows users to manage multi-container applications using Docker Compose's YAML format. This tool provides continuity for developers and administrators who are familiar with Docker Compose, making it easy to define and run complex applications across multiple containers in Podman.

*   Using Podman Compose:

    - docker-compose.yml (sample file for Podman Compose)

    version: '3'

    services:

    web:

    image: nginx

    ports:

    - "8080:80"

    db:

    image: redis

*   Run the application using Podman Compose:

    podman-compose up

In practice, Podman’s rootless mode makes it an excellent choice for development environments where multiple users need to run containers securely without administrative privileges. Developers can build, test, and run containerized applications in an isolated and secure environment, making Podman ideal for collaborative projects.

For production environments, Podman’s tight integration with SELinux and systemd ensures that containers are isolated and secure, with robust control over resources and permissions. Podman also fits seamlessly into Continuous Integration and Continuous Deployment (CI/CD) pipelines due to its rootless operation and Docker command compatibility. Podman can be used to build, test, and deploy container images securely within these pipelines, reducing the risk of vulnerabilities during the deployment process.

Building a container image with Podman:

*   Build a container image from a Dockerfile

    podman build -t myapp .

*   Run the built image

    podman run -d --name app myapp

Podman in RHEL offers a secure, flexible, and rootless container management solution that aligns with Red Hat’s focus on enterprise-grade security and stability. Its compatibility with Docker commands, adherence to OCI standards, and integration with SELinux and systemd make it an ideal choice for organizations looking to transition away from Docker while maintaining existing workflows. With Podman, RHEL users can benefit from increased security, ease of use, and compatibility with the broader container ecosystem.

[Conclusion](#contents.xhtml_sc2_274a)

In this chapter, we explored essential techniques for managing and securing RHEL systems particularly focusing on Ansible automation to enhance network services and security for remote operations. We addressed dual stack networking to facilitate IPv4 and IPv6 interactions and detailed the strategic use of SELinux for rigorous access control. We discussed the management of network security layers, from user and group management with commands like useradd and chgrp to implementing SELinux and firewalld for robust defense mechanisms. Special emphasis was placed on configuring the OpenSSH service and advocating for key-based authentication to reduce brute force attack risks. The chapter highlighted crucial security practices such as regular updates, applying the principle of least privilege and employing strong authentication mechanisms. These practices are supported by strict system and network access controls to ensure only necessary services are exposed. By applying these strategies, RHEL administrators can enhance their systems' security posture, ensuring they are prepared to face current and future cybersecurity challenges. This chapter equips IT professionals with the knowledge to apply these security best practices effectively ensuring the ongoing integrity and security of their RHEL systems. The journey towards maintaining secure network services in RHEL demands continual adaptation and proactive management.

[Points to remember](#contents.xhtml_sc2_275a)

*   SELinux enforcement: Understanding the modes of SELinux (enforcing, permissive, disabled) and how they affect system security is crucial for maintaining stringent security protocols.
*   Firewalld's role: Recognize the importance of firewalld for dynamic firewall management and the use of zones and services to control network traffic efficiently.
*   Dual-stack networking: Be familiar with configuring and managing both IPv4 and IPv6 on RHEL systems to ensure compatibility and future-proof networking capabilities.
*   OpenSSH configurations: To secure remote sessions and services, implement key-based authentication and understand OpenSSH settings in /etc/ssh/sshd_config.
*   Package management with YUM or DNF: Regular updates and proper package management using YUM or DNF tools are essential for system security and integrity.
*   Audit and monitoring: Utilize tools like auditd and system logs to continuously monitor and audit RHEL systems for any unusual or potentially malicious activity.
*   Backup strategies: Develop robust backup and recovery procedures to ensure data redundancy and continuity in case of data loss or system failures.
*   Security best practices: Adhere to security best practices such as the principle of least privilege, regular patching and using multi-factor authentication to enhance overall system security.

[Multiple choice questions](#contents.xhtml_sc2_276a)

1.  What is the primary function of SELinux in RHEL?
    1.  Managing user passwords
    2.  Automating tasks across the network
    3.  Enforcing security policies at the kernel level
    4.  Installing and updating software packages
2.  Which command allows HTTPS traffic through the firewall in RHEL?
    1.  firewall-cmd --permanent --add-service=https
    2.  firewall-cmd --temporary --add-service=https
    3.  firewall-cmd --add-service=https
    4.  firewall-cmd --reload --add-service=https
3.  Which configuration file is used to set up and secure the OpenSSH service in RHEL?
    1.  /etc/ssh/ssh_config
    2.  /etc/ssh/sshd_config
    3.  /etc/ssh/ssh_host_config
    4.  /etc/ssh/ssh_service_config
4.  What is the best practice for managing network security related to SSH on RHEL systems?
    1.  Enabling rosot login for all users
    2.  Using weak passwords for quicker access
    3.  Setting up key-based authentication and disabling password-based login
    4.  Allowing SSH access without restrictions

[Answers](#contents.xhtml_sc3_277a)

1\. c

2\. a

3\. b

4\. c

[Key terms](#contents.xhtml_sc2_278a)

*   Security-Enhanced Linux (SELinux): A security architecture integrated into RHEL that provides a mechanism for supporting access control security policies including mandatory access controls.
*   Booleans (SELinux Booleans): Toggleable options in SELinux that allow administrators to switch on or off particular features or behaviors in SELinux without altering the policy code.
*   Firewalld: A dynamic firewall manager in RHEL that uses zones and services to manage and control network traffic and improve security.
*   Dual stack networking: A method that allows for the configuration and simultaneous operation of IPv4 and IPv6 stacks on network interfaces within RHEL systems.
*   OpenSSH: An open-source implementation of the SSH protocol used in RHEL for secure network communications and securely managing servers and configurations.
*   Key-based authentication: A method of SSH authentication in RHEL that uses cryptographic keys rather than passwords, enhancing security by mitigating the risks associated with brute force attacks.
*   Firewall-cmd: The command line interface for managing firewalld in RHEL which provides support for firewall zones to define the trust level of network connections and interfaces.
*   IPtables: A legacy tool for setting up, maintaining and inspecting the tables of IP packet filter rules in the Linux kernel often used before the introduction of Firewalld in RHEL.
*   Yellowdog Updater Modified (YUM): A package manager used in RHEL to install, update and remove software packages, manage repositories and resolve dependency conflicts.
*   Auditd: The Linux audit daemon in RHEL is used to monitor, collect and store system activities to enable security auditing and post-mortem analysis.
*   Pluggable Authentication Modules (PAM): A suite of shared libraries that enable the local sysadmin to choose how applications authenticate users in RHEL thus, providing a system of layers to support diverse authentication methods.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 7Emerging Technologies Integration](#contents.xhtml_ch07a)

[Introduction](#contents.xhtml_sc2_279a)

In this chapter, we will delve into the integration of Red Hat's emerging technologies, a crucial area for maintaining and enhancing system performance and security in dynamic computing environments. As organizations increasingly rely on complex systems and data-intensive applications, the need to effectively integrate advanced technologies becomes paramount. This chapter explores several key technologies including CentOS Stream, kernel live patching, Virtual Data Optimizer (VDO) volumes, System Security Services Daemon (SSSD), containers, virtualization, Universal Base Images (UBIs) and cloud integration with major providers. Additionally, we discuss Integrity Measurement Architecture (IMA) for enhanced security through digital hashes and signatures.

[Structure](#contents.xhtml_sc2_280a)

The chapter covers the following topics:

*   Integration of Red Hat's emerging technologies
*   CentOS Stream
*   Kernel live patch
*   Advanced storage features
*   System Security Services Daemon
*   Virtualization and containers
*   Universal Base Images
*   Cloud providers
*   Integrity Measurement Architecture

[Objectives](#contents.xhtml_sc2_281a)

The chapter begins with the strategic relationship between Red Hat Enterprise Linux and the open-source upstream CentOS Stream. Together they enable a platform development for the Red Hat ecosystem. Key features include deploying kernel live patching via the web console to reduce system downtime and optimizing operational efficiency. VDO volumes empower advanced storage, providing cost-effective and scalable storage solutions. Strengthening security and authentication through SSSD is a priority, while understanding containers and virtualization enhances competitive positioning, especially within the RHCE certification framework. We leverage Universal Base Images for portable, secure containerized applications and integrate RHEL with major cloud providers like AWS, Google Cloud, and Microsoft Azure, which supports scalable and flexible cloud deployments. Finally, implementing IMA ensures compliance and system integrity, bolstering enterprise security.

[Integration of Red Hat's emerging technologies](#contents.xhtml_sc2_282a)

Red Hat's emerging technologies encompass a wide range of initiatives and innovations particularly in the realms of cloud services, containerization, automation and edge computing. Following are the key areas where Red Hat is focusing its efforts:

*   Cloud services and hybrid cloud: Red Hat offers extensive cloud solutions primarily through OpenShift which supports cloud native applications and provides a consistent environment across multiple cloud platforms. This facilitates easier deployment and scaling combined with enhanced security features.
*   Containerization and Kubernetes: Red Hat has heavily invested in container technologies with Red Hat OpenShift, a Kubernetes based platform. This platform simplifies the development, deployment and management of containerized applications and microservices architectures.
*   Automation with Ansible: Red Hat Ansible automation platform is a pivotal part of Red Hat’s strategy for enterprise automation. It provides tools to automate complex multi-tier IT application environments aiming to increase efficiency and reduce the potential for human error in configurations and deployments.
*   Edge computing: Red Hat is expanding its capabilities in edge computing, emphasizing the need for robust, open-source solutions that can operate at the edge of the network. This includes optimizing RHEL and OpenShift for edge deployments which can process data closer to its source and support IoT applications.
*   AI and machine learning: Red Hat is also working on integrating AI and machine learning more deeply into its enterprise offerings, providing tools and platforms that help businesses leverage these technologies to gain predictive insights and automate processes.
*   Security and compliance: With the increasing focus on data protection, Red Hat is enhancing its security features across its product suite including better compliance tools and security automation through advanced monitoring and response capabilities.

These efforts reflect Red Hat's commitment to providing comprehensive, open-source solutions that support the evolving IT landscape enabling businesses to transition smoothly to modern infrastructure paradigms while maintaining high levels of security and compliance.

[Tuned](#contents.xhtml_sc3_283a)

The tuned service applies system configuration to RHEL defined in a tuning profile. Each tuning profile includes kernel parameters that set the overall performance expectations. With static tuning. These settings are static and they are not adjusted as the activity level changes whereas, with dynamic tuning, the daemon monitors and adjusts the settings based on behavior changes. Some of the monitored parameters include CPU, memory, storage device, network activity, etc. Overall, it reduces the settings during low activity and maximizes the performance during high activity.

We can easily install the tuned package via the DNF package manager, as follows:

# dnf install tuned

We need to ensure that the daemon is enabled and is successfully started before interacting with it, as follows:

# systemctl enable --now tuned

The following table summarizes the available profiles out of the box:

| Profile | Base | Description |
| --- | --- | --- |
| Balanced |  | Compromise power saving and performance. |
| Desktop | Balanced | Faster response of interactive applications. |
| Latency performance |  | Performance and low latency applications. |
| Network latency | Latency performance | Performance for low latency network. |
| Network throughput | Latency performance | Maximize the network throughput. |
| Oracle | Throughput performance | Optimized for Oracle database workload. |
| Powersave |  | Maximize the power saving. |
| Throughput performance |  | Maximize the throughput. |
| Virtual guest |  | Maximize the performance as a virtual machine guest. |
| Virtual host |  | Maximize the performance as a virtual machine host. |

Table 7.1: Tuned performance profiles

The tuned-adm command line interacts with the tuned service and is included in the tuned package. It enables the list of the available profiles to switch between profiles recommend a tuning profile or turn off tuning.

[Active profile](#contents.xhtml_sc4_284a)

We can inquire the active tuned profile using the following command:

# tuned-adm active

The command output displays the powersave current active profile, as follows:

Current active profile: powersave

[List](#contents.xhtml_sc4_285a)

In the same way, we can list the available tuned profiles using the list parameter of the tuned-adm command:

tuned-adm list

The output is going to show the full list of tuned profiles similar to [Table 7.1](#ch07.xhtml_tab7-1) with a short description of each profile.

[Change](#contents.xhtml_sc4_286a)

We can switch between tuned profiles using the profile parameter of the tuned-adm command, as follows:

# tuned-adm profile network-throughput

Once we successfully change the tuned profile, we can verify the current profile as before using the active parameter of the tuned-adm command.

[Recommended](#contents.xhtml_sc4_287a)

The tuned service can recommend a tuning profile for the system based on the activity. It is also used to set the default profile after the installation as follows:

tuned-adm recommend desktop

[Web console](#contents.xhtml_sc4_288a)

We can manage the system performance profile with the web console. However, we need a privilege account to change the current Performance profile.

The [Figure 7.1](#ch07.xhtml_fig7-1) illustrates the web console interface of a RHEL system, providing an overview of system health, usage metrics, system information, and configuration settings, including the system's performance profile set to virtual-guest.

![](images/Figure_7.1.png)

Figure 7.1: Performance profile

We can verify the currently active tuning profile in the performance profile field associated with our system. If the profile is not the one expected, we can modify it via the Change performance profile panel.

[Figure 7.2](#ch07.xhtml_fig7-2) illustrates the process of changing the performance profile of a RHEL system through the web console. The available profiles include options such as network-throughput, powersave, throughput-performance, and virtual-guest, allowing system administrators to optimize the system for specific workloads and environments. The active profile is currently set to virtual-guest, which is recommended for systems running in a virtualized environment.

![](images/Figure_7.2.png)

Figure 7.2: Change profile

The tuned service optimizes our systems for success, taking care of important system and kernel parameters.

[CentOS Stream](#contents.xhtml_sc2_289a)

CentOS Stream is a Linux distribution developed by the CentOS project as a rolling-release version of RHEL. It sits between Fedora and RHEL in the Red Hat family providing a platform that previews the next minor RHEL release. CentOS Stream continues the CentOS project's goal of developing a free, open-source platform accessible to developers and system administrators.

CentOS Stream serves as a midstream between Fedora which acts as the upstream for RHEL, and RHEL itself. It offers a preview of what the next RHEL minor releases are likely to include. This alignment provides several advantages, as follows:

*   Feedback loop: Developers and users can see and contribute to the future of RHEL influencing development with direct feedback on new features and changes.
*   Continuous delivery: Unlike the traditional CentOS, which mirrored RHEL exactly after RHEL releases, CentOS Stream receives updates ahead of RHEL. This provides users with early access to new features and fixes.
*   Integration testing: Enterprises can test their systems, applications and workflows on CentOS Stream to ensure compatibility with future RHEL updates easing the certification process once those changes are officially released in RHEL.
*   Rolling release model: Unlike its predecessor that had periodic releases, CentOS Stream continuously updates which means that there are no major releases to wait for.
*   Compatibility with RHEL: Since it is positioned just ahead of RHEL, CentOS Stream maintains high compatibility with RHEL ensuring a stable environment for development and testing.
*   Community driven innovation: It allows for community involvement directly in the development of RHEL offering a unique opportunity for the open source community to contribute to the ecosystem.

[Installation and management](#contents.xhtml_sc3_290a)

To successfully install and manage CentOS Stream.

Following steps outline the process, from downloading the necessary installation files to keeping the system up to date:

*   Download International Organization for Standardization (ISO) file: Visit the official CentOS website to download the latest CentOS Stream ISO file.
*   Create installation media: Use tools like dd or rufus to create a bootable USB drive.
*   Install on our system: Boot from the USB drive, follow the installation instructions and configure the system as needed.
*   System updates: Keep the system updated using the dnf command as follows:

    dnf update

Installing CentOS is suitable for the following use cases:

*   Development testing: Ideal for developers who build software intended for RHEL environments as it provides a near-future look into the RHEL ecosystem.
*   Sysadmin training: System administrators can use CentOS Stream to train and familiarize themselves with the tools and features expected in RHEL ensuring they are prepared for new releases.
*   Enterprise environments: Businesses can integrate CentOS Stream into their development environment to prepare their applications and systems well in advance for the next RHEL release.

[Transition from CentOS Linux to CentOS Stream](#contents.xhtml_sc3_291a)

The shift from CentOS Linux to CentOS Stream marked a significant change in approach from being a downstream project to an upstream contributor to RHEL. This transition aims to provide a platform that is continually moving forward, reducing the lag between an RHEL release and its availability to the CentOS community. Users and organizations depending on traditional CentOS are encouraged to evaluate their use cases and consider whether CentOS Stream or alternatives like AlmaLinux and Rocky Linux might better serve their needs.

CentOS Stream represents a strategic shift in the CentOS project's approach to open-source development and distribution. By providing a rolling preview of future RHEL content, it aligns more closely with the development process of Red Hat offering enterprises, developers and sysadmins a valuable tool for integration testing and early adoption of new technologies. As CentOS Stream continues to evolve, it will play a crucial role in shaping the future of enterprise Linux environments.

[Kernel live patch](#contents.xhtml_sc2_292a)

Kernel live patching is a crucial feature that allows administrators to apply patches to the kernel while it is still running without needing to reboot the system. This capability is invaluable for environment where uptime and availability are critical such as in servers and production environments. Here, we will explore how to implement kernel live patching using a web console, focusing on RHEL, which utilizes the Cockpit web console.

The following are the benefits of kernel live patching:

*   Minimized downtime: Apply security patches and bug fixes without rebooting thus, maintaining service availability.
*   Immediate effect: Patches take effect immediately without the delay and risk of rebooting.
*   Enhanced security: Quickly apply security patches to mitigate vulnerabilities.

Before performing kernel live patching on a RHEL system, certain prerequisites must be met to ensure successful implementation, as follows:

*   A RHEL system with a subscription to Red Hat insights and management services.
*   The system must have a cockpit installed. On RHEL, Cockpit is often pre-installed, or it can be installed via dnf.
*   Ensure the system is registered to Red Hat Subscription Management and has a subscription that includes support for live kernel patching.

[Cockpit live patching](#contents.xhtml_sc3_293a)

Following steps outline how to set up and use Cockpit for kernel live patching via its web interface, ensuring a streamlined process for applying live kernel patches without system reboots:

1.  Setting up Cockpit:
    1.  Install Cockpit (if not already installed), as follows:

        # dnf install cockpit

    2.  Enable and start the cockpit service, as follows:

        # systemctl enable --now cockpit.socket

    3.  Access Cockpit by navigating to https://<our-server-IP>:9090 and log in using our system credentials.
2.  Configure kernel live patching:
    1.  Access the Subscriptions page within Cockpit which is under the Tools menu.
    2.  Register our system with Red Hat Subscription Management if not already done.
    3.  Attach a subscription that includes support for live kernel patching (such as Red Hat Enterprise Linux for business).
3.  Enable kernel care:
    1.  Navigate to the Software updates section in Cockpit.
    2.  Look for the kernel care option which might be listed under services or tools depending on our RHEL version.
    3.  Enable kernel care by following the on-screen instructions to allow live patching of the kernel.
4.  Apply and manage patches:
    1.  Check for available patches: Regularly visit the Software updates section to check for new patches.
    2.  Apply patches: When available, select the patches and apply them directly through the web interface.
    3.  Monitor patch status: Post application, monitor the status and effectiveness of the patch using the insights and diagnostics tools available within Cockpit.

[Figure 7.3](#ch07.xhtml_fig7-3) shows the Cockpit web interface's software update section, where users can manage available system updates. The interface highlights the status of pending updates, including security fixes, and offers options to enable automatic updates and configure kernel live patching to minimize system downtime during critical updates.

![](images/Figure_7.3.png)

Figure 7.3: Kernel live update

Observe the following best practices:

*   Regular monitoring: Regularly check for updates and monitor the system's health via Cockpit's diagnostic tools.
*   Testing: Test patches in a non-production environment before applying them to critical systems.
*   Security compliance: Regularly review security compliance status via Red Hat Insights or similar tools integrated within Cockpit.

Kernel live patching is a sophisticated tool that enhances operational efficiency by reducing downtime and ensuring that critical security patches are applied without interrupting services. Using the Cockpit web console, system administrators can manage kernel patches effectively and maintain the high availability of Linux servers. This capability not only supports proactive maintenance strategies but also aligns with best practices for system security and reliability.

[Advanced storage features](#contents.xhtml_sc2_294a)

VDO is a Linux-based technology that provides inline data reduction capabilities including deduplication and compression. VDO can significantly reduce storage costs and enhance the efficiency of data storage management. It is especially useful in environments where data redundancy is high such as virtual machine storage and backup systems.

Following are the key features of VDO:

*   Data deduplication: VDO can identify and eliminate duplicate blocks of data, storing only unique data and references to duplicates which conserves storage space.
*   Data compression: After deduplication, VDO compresses the remaining data to further reduce storage requirements.
*   Thin provisioning: VDO supports thin provisioning allowing administrators to allocate more virtual storage capacity than physically available and optimizing storage utilization.

Before setting up VDO, ensure that our system meets the following requirements:

*   A Linux distribution with VDO support such as RHEL 7.5 and later.
*   Sufficient storage space for the VDO volume.
*   Installation of the vdo and kmod-kvdo packages which provide the necessary VDO tools and kernel modules.

Following steps outline the process of installing, configuring, and managing a VDO volume on a RHEL system, ensuring efficient storage utilization through thin provisioning and deduplication techniques:

1.  Install VDO and KVDO:

    We need to install VDO and the KVDO kernel module. On RHEL and similar distributions, we can use yum or dnf, as follows:

    # yum install vdo kmod-kvdo

2.  Creating a VDO volume:

    To create a VDO volume, we will use the vdo command. The following example creates a VDO volume named vdo1 on an existing device /dev/sdb:

    # vdo create --name=vdo1 --device=/dev/sdb --vdoLogicalSize=100G

    Following are the parameters of the command:

    *   --name=vdo1: Specifies the name of the VDO volume.
    *   --device=/dev/sdb: Specifies the underlying storage device.
    *   --vdoLogicalSize=100G: Sets the logical size of the VDO volume which can be larger than the physical size of /dev/sdb due to thin provisioning.
3.  Formatting and mounting the VDO volume:
    1.  Once the VDO volume is created, format it with our preferred filesystem, for example, ext4:

        # mkfs.ext4 /dev/mapper/vdo1

    2.  Create a mount point and mount the VDO volume:

        # mkdir /mnt/vdo1 sudo mount /dev/mapper/vdo1 /mnt/vdo1

4.  Enabling VDO at boot:

    To ensure the VDO volume is automatically mounted at boot, add it to the /etc/fstab file:

    /dev/mapper/vdo1 /mnt/vdo1 ext4 defaults,x-systemd.requires=vdo.service 0 0

    This entry will mount the VDO volume at /mnt/vdo1 with default mount options and ensure it waits for the vdo.service to start before mounting.

5.  Managing VDO volumes:

    We can manage VDO volumes using various vdo commands:

    *   Start a VDO volume:

        # vdo start --name=vdo1

    *   Stop a VDO volume:

        # vdo stop --name=vdo1

    *   Check VDO status:

        # vdo status --name=vdo1

Following are the best practices for adopting the VDO volumes:

*   Monitoring: Regularly monitor the disk space and VDO volume performance. VDO provides tools to check statistics related to deduplication and compression.
*   Backup: Despite the data reduction features, ensure regular backups are performed to prevent data loss.
*   Updates and maintenance: Keep our system and VDO packages updated for optimal performance and security.

VDO is a powerful solution for optimizing storage in Linux environments. By implementing VDO, organizations can reduce physical disk usage, lower storage costs and improve overall system performance. Whether we are running cloud infrastructure, virtual environments or data centers, VDO provides essential benefits for data management and storage efficiency.

[System Security Services Daemon](#contents.xhtml_sc2_295a)

SSSD is a vital component within Linux systems, particularly for enterprises that utilize centralized identity and authentication services. SSSD interacts with directory services such as Active Directory, Lightweight Directory Access Protocol (LDAP) and FreeIPA. Its primary role is to provide access to remote identity and authentication resources through a common framework enhancing both security and user management in Linux environments.

[Key features](#contents.xhtml_sc3_296a)

Following are the key features of the System Security Services Daemon:

*   Single sign-on capabilities: SSSD supports Kerberos authentication which facilitates Single Sign-On (SSO) to all Kerberos-aware applications and services, reducing the number of times users must authenticate themselves.
*   Offline support: One of SSSD's standout features is its ability to cache credentials and other user data. This allows users to continue working even if the connection to the central identity store is temporarily unavailable.
*   Security enhancements: SSSD provides a layer of security by enforcing access control policies defined in centralized directories. It also supports the use of SELinux, adding an extra layer of security by managing access control based on policies.
*   Integration with various identity providers: SSSD can integrate with multiple identity and authentication providers, including LDAP, Active Directory, Kerberos and FreeIPA. This flexibility makes it a robust solution for diverse IT environments.

[Working of SSSD](#contents.xhtml_sc3_297a)

SSSD operates by interacting with various backend services to authenticate users and fetch identity data. It caches this data locally to ensure that users can log in quickly and continue to access resources even when offline. Following is a brief overview of how SSSD functions:

*   Initialization: SSSD starts and reads its configuration from /etc/sssd/sssd.conf.
*   Service activation: Based on the configuration, SSSD decides which services to start, such as the Name Service Switch (NSS) service for user and group information and the PAM service for authentication.
*   Backend connection: SSSD connects to the specified back end (e.g., LDAP or Kerberos) to retrieve user data and authentication mechanisms.
*   Caching: Retrieved data is cached using a local database allowing the system to serve requests locally without needing to repeatedly query the backend.
*   Authentication and authorization: When a user attempts to log in, SSSD processes the authentication request through the appropriate back end. Once authenticated, it handles subsequent authorization requests using cached data if available.

[Configuration and management](#contents.xhtml_sc3_298a)

Configuring SSSD is done through the sssd.conf file located in /etc/sssd/. Proper configuration requires specifying the domains, services and back-end providers. Following is an example for configuration:

[sssd] services = nss, pam config_file_version = 2 domains = LOCAL,LDAP [domain/LOCAL] id_provider = local [domain/LDAP] id_provider = ldap auth_provider = ldap ldap_uri = ldap://ldap.example.com ldap_search_base = dc=example,dc=com

This configuration initializes SSSD with both local and LDAP domains, utilizing NSS and PAM services.

Following are the best practices for using SSSD:

*   Keep SSSD updated: Regularly update SSSD to benefit from security patches and new features.
*   Secure configuration files: Limit access to the sssd.conf file to root to prevent unauthorized modifications.
*   Monitor SSSD logs: Monitoring logs can help diagnose issues with SSSD or connected services.
*   Test configurations: Always test new configurations in a staging environment before rolling them out in production.

SSSD is a powerful tool for managing authentication and identity services in Linux environments. By leveraging SSSD, organizations can enhance their security posture, streamline user management and ensure consistent access controls across all systems. Whether integrating with Active Directory for a corporate environment or using LDAP for flexible authentication, SSSD stands out as an essential component of modern Linux administration.

[Virtualization and containers](#contents.xhtml_sc2_299a)

Distributing an application to the final user requires other libraries, configuration files or services provided via a runtime environment. The application is installed in the target system running on a physical or virtual server. Traditionally, the packaging system solves this problem by grouping together all the resources for our application. In RHEL, we use the Red Hat Package Manager (RPM) format. The major drawback is that the libraries and other dependencies of the package are entangled with the runtime environment. During the software lifecycle, an application might require different versions of libraries or required software. Similarly, more applications running on the same system might require different versions of the same library. We can resolve this problem by deploying our application to a container. Similar to a physical shipping container, we group the application and all the necessary resources together, so they do not affect each other. Compared to virtual machines, containers benefit from security, storage, and network isolation.

[Podman](#contents.xhtml_sc3_300a)

Pod manager (Podman) is an essential tool in RHEL for managing containers and container images directly, offering a daemonless and rootless mode of operation that enhances security. It forms part of a trio of container tools that also includes Skopeo for inspecting, copying, deleting and signing container images and Buildah for creating container images from scratch. All these tools are OCI compatible, meaning they can manage Linux containers created by any OCI compatible container engine such as Docker.

The container tools include the following utilities:

*   Podman: Manages containers and container images.
*   Skopeo: Inspect, copy, delete and sign images.
*   Buildah: Creates new container images.

The container tools are compatible with OCI. The most famous OCI-compatible container engines are Docker, CRI-O, etc.

Podman is particularly noteworthy for its ability to manage containers without requiring a container daemon, setting it apart from traditional Docker like container management. This approach not only simplifies the system architecture by removing the need for a persistent background service but also reduces the potential attack surface which is crucial for system security. Users can run containers as their user account without elevated privileges known as running rootless containers. This capability significantly increases security as it limits the potential damage if a container is compromised. Although, rootless containers have some restrictions such as the inability to bind to privileged ports (below 1024).

Furthermore, Podman integrates well into system management workflows and scripts due to its simple CLI which mirrors that of Docker, making it easier for users to transition from Docker or learn containerization for the first time. Podman's unique features such as the ability to generate Kubernetes Ain't Markup Language (YAML) from existing containers and the ability to play pods directly offer additional flexibility and ease of use for developers and system administrators looking to manage containers efficiently on a single-node RHEL host or scale up to larger deployments.

Following steps provide a comprehensive guide for installing and using Podman to manage OCI containers on a RHEL system. This process includes pulling a UBI, running a container, installing software inside the container, and creating a custom image, followed by managing and troubleshooting containers:

1.  Install Podman, a tool for managing OCI containers and pods:

    First, ensure that Podman is installed on our RHEL system. We can install Podman with the following command:

    dnf install -y podman

2.  Pull a standard Red Hat UBI:

    We can pull an image from a registry such as Docker hub or Red Hat registry using Podman. For instance, to pull the latest ubi9 image, we would use the following:

    podman pull registry.access.redhat.com/ubi9/ubi

3.  Run a simple container using Podman, as follows:

    podman run -it registry.access.redhat.com/ubi9/ubi /bin/bash

4.  Inside the container, install HTTPD server, as follows:

    dnf install -y httpd

5.  Exit the container and create a custom Containerfile to automate the process, as follows:

    echo -e "FROM registry.access.redhat.com/ubi9/ubi\nRUN dnf -y install httpd\nCMD [\"/usr/sbin/httpd\", \"-D\", \"FOREGROUND\"]" > Containerfile

    | Note: While both Dockerfile and container file are used to define the steps to create a container image, container file is often favored in environments using tools like Podman and Buildah for its neutrality, as opposed to Dockerfile which is specifically associated with Docker. |

6.  Build a custom image from Containerfile, as follows:

    podman build -t my-custom-httpd.

7.  Run the newly built HTTPD server container, as follows:

    podman run -d -p 8080:80 my-custom-httpd

    This command runs a new container named my-custom-httpd from the my-custom-httpd image. We can run the container in detached mode using the -d parameter that executes the sleep infinity command to keep the container running indefinitely.

8.  Viewing logs as follows:

    To check the logs of a container which are helpful for debugging and monitoring, use the following:

    podman logs my-custom-httpd

9.  Stopping and removing the container as follows:
    *   When we are finished with the container, we can stop it using the following:

        podman stop my-custom-httpd

    *   Remove it using the following:

        podman rm my-custom-httpd

10.  Managing container images as follows:
    *   To list all container images on our system, we can use the following:

        podman images

    *   To remove an image, for example, the my-custom-httpd image, use the following:

        podman rmi my-custom-httpd:latest

These steps offer a straightforward approach to managing containers with Podman, showcasing its capabilities for handling container lifecycles without requiring a daemon which aligns with security best practices and system simplicity.

[Rootless containers](#contents.xhtml_sc3_301a)

We can run our container as a root user or normal user in the container host. The execution as a normal user, unprivileged is called rootless containers. The rootless containers cannot publish their network services on the privileged ports below 1024 on the container host. Rootless containers are more secure but have other restrictions such as limitations related to accessing specific system resources or capabilities typically reserved for privileged administrative users. If necessary, we can execute our containers as root for debugging or development. Still, the overall system security might be at risk if a bug allows an attacker to compromise the container.

[Kubernetes and OpenShift](#contents.xhtml_sc3_302a)

As our container fleet grows, we need a system that scales our production requirements. Kubernetes is a container orchestration open-source technology that makes it easier to deploy, manage and scale container-based applications. It also simplifies traffic redirection via the load balancer and manages DNS  records. It is based on the postal model and we can configure the application to be routed to maintain uptime when we need to perform maintenance operations to our system.

Red Hat OpenShift is a commercial distribution of Kubernetes that includes a set of addiction modular components and services to reduce the time to market of our solution. It also includes commercial support from Red Hat.

[Universal Base Images](#contents.xhtml_sc2_303a)

Red Hat has introduced a compelling innovation with the UBI. These images serve as a foundational element for building and distributing container applications across various environments, even beyond Red Hat’s ecosystem.

[UBI images](#contents.xhtml_sc3_304a)

UBI images are a subset of the RHEL image ecosystem that Red Hat offers for creating containerized applications. Unlike traditional RHEL base images, UBIs offer a unique advantage, that is, they can be used and shared freely, even if the end user does not have a Red Hat subscription. This flexibility makes UBI images particularly attractive for developers seeking the reliability and security of RHEL without the subscription constraints.

[Comparison with RHEL base images](#contents.xhtml_sc3_305a)

RHEL base images and UBIs are derived from RHEL ensuring high security and reliability standards. However, the key difference lies in the distribution rights, as follows:

*   RHEL base images: Require a Red Hat subscription to use and redistribute, limiting their use to environments where users already have a Red Hat agreement.
*   UBI images: They can be freely shared and used across various environments, including non-Red Hat platforms. This open nature facilitates broader collaboration and distribution in the development community.

[Key features and benefits](#contents.xhtml_sc3_306a)

Following are the key features and benefits of UBIs:

*   Broad compatibility: UBIs can run on any platform that supports containers including non-Red Hat platforms, making them versatile for various deployment scenarios.
*   No subscription required: Users can deploy UBI based applications without a Red Hat subscription, broadening access to Red Hat’s secure and reliable base image.
*   Standardization: UBIs provide a standardized base that can be extended with additional packages and applications suitable for both development and production environments.

[Types](#contents.xhtml_sc3_307a)

Red Hat offers several flavors of UBI images to cater to different needs, as follows:

*   Standard: Includes the full base package utilities suitable for a wide array of applications.
*   Minimal: Stripped down version for smaller footprint applications which is ideal for microservices.
*   Micro: Even smaller than minimal, these images provide just the bare essentials, suitable for edge computing scenarios.

Each variant is tailored to specific use cases ensuring developers can choose the most appropriate base image for their application’s requirements, as follows:

*   Cloud-native applications: UBIs are ideal for building microservices or other cloud-native applications that require a reliable and secure base image.
*   CI or CD pipelines: Developers can integrate UBI images into their CI or CD pipelines to ensure consistent environments from development through to production.
*   ISV software distribution: Independent Software Vendors (ISVs) can use UBIs to distribute their applications more broadly across different cloud platforms without compatibility concerns.

Red Hat’s UBI revolutionize the way developers can use and distribute RHEL based container images. By offering a secure, reliable and freely distributable container based image, UBIs empower developers to build and share their applications more broadly than ever before, whether for individual use, enterprise development or ISV distribution, UBIs provide a flexible and robust foundation for a variety of application needs.

[Cloud providers](#contents.xhtml_sc2_308a)

RHEL is a popular choice among enterprises for its stability, security and robust support. Running RHEL on cloud platforms can greatly enhance flexibility, scalability and ease of management. This section provides insights on how to run RHEL on four major cloud providers, Amazon Web Services (AWS), Google Cloud Platform (GCP), Microsoft Azure and VMware.

[Amazon Web Services](#contents.xhtml_sc3_309a)

AWS offers a highly flexible and scalable platform for running RHEL instances. Through AWS, enterprises can leverage powerful compute resources, advanced networking, and integrations with various AWS services for seamless infrastructure management.

[Launching RHEL on EC2](#contents.xhtml_sc4_310a)

To launch a RHEL instance on AWS, follow these step-by-step instructions to ensure a smooth deployment process using Elastic Compute Cloud (EC2):

1.  Navigate to the AWS Management Console and select EC2.
2.  Choose Launch Instance and select the RHEL Amazon Machine Image (AMI) from the list of supported AMIs.
3.  Configure our instance type, storage, security groups and key pairs.
4.  Launch the instance and connect to it using SSH with the provided key pair.

To efficiently manage RHEL instances on AWS, several tools and services can be leveraged to streamline operations and enhance system reliability as follows:

*   Utilize AWS Systems Manager for patching and configuration management.
*   Leverage AWS CloudWatch for monitoring and AWS backup for data protection.

[Google Cloud Platform](#contents.xhtml_sc3_311a)

Deploying RHEL on GCP Compute Engine is a straightforward process that allows you to leverage the power of cloud computing for your applications. This guide outlines the essential steps for creating a new RHEL instance, ensuring you configure the machine specifications, networking, and security features effectively. Following are the steps to successfully set up your RHEL environment in the cloud.

Follow these steps to deploy RHEL on the compute engine:

1.  Open the Google Cloud console and go to the compute engine section.
2.  Click on create instance, choose the RHEL image from the cloud marketplace.
3.  Configure the machine specifications, disk, networking and security features.
4.  Deploy the instance and use Google Cloud’s SSH browser tool to connect.

Following are the additional tools for deploying RHEL:

*   Implement Google Cloud’s operations suite for monitoring and logging.
*   Use persistent disks for reliable and high-performance block storage.

[Microsoft Azure](#contents.xhtml_sc3_312a)

Microsoft Azure is a comprehensive cloud computing platform that offers a wide range of services and solutions for businesses and developers. With its flexible and scalable infrastructure, Azure enables organizations to deploy and manage applications and services through a global network of data centers.

In order to run RHEL on Azure virtual machines, following are the steps:

1.  Go to the Azure portal and select virtual machines.
2.  Click on add and select RHEL from the available images.
3.  Configure virtual machine size, storage options and network settings.
4.  After deployment, connect to the VM using Azure’s bastion service for secure SSH access.

To optimize the performance and resilience of your RHEL environment on Microsoft Azure, consider implementing the following enhancements:

*   Utilize Azure monitor for comprehensive monitoring across applications.
*   Employ Azure site recovery for disaster recovery capabilities.

[VMware](#contents.xhtml_sc3_313a)

VMware is a leading provider of virtualization and cloud infrastructure solutions. It enables businesses to create, manage, and run virtual machines on physical hardware, allowing for efficient resource utilization, scalability, and flexibility. VMware's suite of products, including VMware vSphere, VMware Workstation, and VMware Cloud, empowers organizations to modernize their IT environments, streamline operations, and enhance application performance.

Follow are the steps to deploy RHEL on a VMware vSphere virtual machine:

1.  Use VMware vSphere to create a new virtual machine.
2.  Select RHEL as the guest operating system and allocate resources such as CPU, memory and storage.
3.  Install RHEL using the ISO file from Red Hat’s official website.
4.  Configure network settings and connect to the virtual machine using VMware’s console or SSH.

Following is the management and automation for deploying RHEL:

*   Apply VMware vRealize automation to automate the deployment and management of virtual machines.
*   Integrate with VMware vCenter for centralized management and VMware NSX for advanced network virtualization and security.

Deploying RHEL on cloud platforms provides enterprises with scalable solutions that leverage the advanced capabilities of cloud computing. Each cloud provider offers unique tools and services that enhance the operation and management of RHEL environments ensuring businesses can optimize their applications effectively in the cloud.

[Integrity Measurement Architecture](#contents.xhtml_sc2_314a)

The Linux kernel's IMA is a security subsystem designed to detect if files have been altered either accidentally or maliciously.

IMA helps maintain system integrity by appraising file measurements (hash values) against previously stored good values as extended attributes on supported file systems like ext3 and ext4\. It works by introducing hooks within the Linux kernel to collect file hashes when they are opened before their contents are accessed. IMA was introduced in Linux kernel version 2.6.30 and is supported by RHEL 8 onward.

Following are the key components of kernel integrity subsystem:

*   IMA: Responsible for collecting file hashes, storing them in kernel memory (inaccessible to userland applications) and allowing verification of these values by local and remote parties.
*   Extended Verification Module (EVM): This module detects offline tampering with security-extended attributes, helping to mitigate attacks such as the evil maid attack.

IMA maintains a runtime measurement list and, if anchored in a hardware Trusted Platform Module (TPM), an aggregate integrity value over this list. Anchoring in TPM makes the measurement list resistant to software attacks, making IMA measurement useful for attesting to system runtime integrity in trusted boot systems.

[Enabling IMA measurement](#contents.xhtml_sc3_315a)

To enable IMA measurement, add the parameters ima=on ima_policy=<policy> to the kernel command line and reboot the system. The policy parameter can take several values, as follows:

*   tcb: Measures all executables, mmap'd files for execution (like shared libraries), kernel modules, firmware and files read by root.
*   appraise_tcb: Appraises all files owned by root.
*   secure_boot: Appraises all loaded modules, firmware, kexec'd kernel and IMA policies, requiring them to have an IMA signature. This is used with CONFIG_INTEGRITY_TRUSTED_KEYRING in secure boot scenarios, with public keys from OEM firmware or via Machine Owner Key (MOK) in shim.

The runtime measurement list can be reviewed via the following:

/sys/kernel/security/ima/ascii_runtime_measurements file:

# head -5 /sys/kernel/security/ima/ascii_runtime_measurements 10 1d8d532d463c9f8c205d0df7787669a85f93e260 ima-ng sha1:ddee6004dc3bd4ee300406cd93181c5a2187b59b boot_aggregate 10 bfe074db49e639b3d65aff5d29714c0ada7584ae ima-ng sha1:b23cdfea2ad736ea9f2591270fe644d8052cc86f /usr/lib/systemd/systemd 10 63c80ba8646fb4d8a48e0b6baf38650fef1b3ffb ima-ng sha1:8c8d12052c4684e696da0bee28d7a2f3c4f408e4 /usr/lib64/ld-2.28.so 10 2a07e7f032ba91832d267e6c58437cec1dccf35d ima-ng sha1:381429f65d66187f866361e8dc19e96808f9424f /usr/lib/systemd/libsystemd-shared-239.so 10 a4c7964b6581dcf3aa5495dc94a17bb7ee82554c ima-ng sha1:1abcf3c99faad55856d49e3ds210abec56d95e4a51 /etc/ld.so.cache

The following is an explanation of columns:

*   Platform Configuration Register (PCR): Indicates the values registered when TPM is in use.
*   Template hash: Combines the length and values of the file content hash and pathname.
*   Template: The method registering the integrity value (e.g., ima-ng).
*   File content hash: Generated from the file's contents.
*   File name: The monitored file's name.

The default hash algorithm is SHA-1 which can be changed to SHA-256 by booting with ima_hash=sha256.

[IMA remeasurement](#contents.xhtml_sc3_316a)

If monitored files change (e.g., system updates), IMA remeasurement can be done. The file system needs to be mounted with the i_version option. To enable i_version on the root file system, edit the /etc/fstab file as follows:

/dev/vda1 / ext4 noatime,iversion 1 2

Upon system update, changes to monitored files will cause hashes to be recomputed and stored.

[IMA appraisal](#contents.xhtml_sc3_317a)

IMA appraisal adds local integrity validation by comparing file measurements against stored good values. Enabling IMA appraisal involves two steps, as follows:

1.  Reboot with relabeling parameters: Add ima_appraise_tcb and ima_appraise='fix' to the kernel command line to relabel the file system. Open all files for reading to relabel them, which can be done as follows:

    find / \( -fstype rootfs -o ext4 -type f \) -uid 0 -exec head -n 1 '{}' >/dev/null \;

2.  Enable appraisal: Reboot with ima_appraise_tcb and ima_appraise=enforce parameters. This ensures the system validates file hashes against stored values before use. If the hash does not match, access to the file is denied, generating a permission denied error and an audit event if auditing is enabled.

    # getfattr -m - -d /sbin/init getfattr: Removing leading '/' from absolute path names # file: sbin/init security.ima=0sAbI83+oq1zbqnyWRJw/mRNgFLMhv security.selinux="system_u:object_r:init_exec_t:s0"

IMA is a powerful tool for enforcing system integrity and detecting tampering. While this guide covers the basics, additional features such as editing default policy files using digital signatures for immutable files and storing signing keys in the TPM chip are available.

[Conclusion](#contents.xhtml_sc2_318a)

This chapter has provided a comprehensive exploration of how emerging technologies can be integrated within the Red Hat environment to drive efficiency, enhance security and support scalable solutions. From the foundational use of CentOS Stream to the advanced implementation of IMA, each section has aimed to equip IT professionals with the knowledge and skills needed to effectively deploy and manage these technologies. As the landscape of enterprise IT continues to evolve, staying abreast of these advancements will ensure that professionals are well-prepared to meet the challenges of modern IT demands.

By mastering these technologies, individuals and organizations can ensure they remain at the cutting edge of enterprise technology, ready to leverage the full potential of their Red Hat systems in any operational context.

In the next chapter, we learn how to optimize the performance and troubleshooting the most common scenarios in RHEL.

[Points to remember](#contents.xhtml_sc2_319a)

*   CentOS Stream serves as a bridge between Fedora and RHEL, providing a rolling preview platform for the next minor RHEL releases.
*   Kernel live patching allows system administrators to apply updates to the Linux kernel without rebooting, thus minimizing downtime and enhancing security.
*   VDO volumes enable data deduplication and compression at the block level which significantly conserves disk space and improves storage efficiency.
*   SSSD enhances system authentication and integrates various identity providers into Linux systems.
*   Containers and virtualization play a pivotal role in deploying and managing lightweight, isolated packages that contain all the necessary elements to run applications.
*   UBIs provide a foundation for building containerized applications that are portable across any system running Docker and compliant with the OCI.
*   Cloud Integration with platforms such as AWS, Google Cloud Platform, Microsoft Azure and VMware enables scalable and flexible cloud deployments of RHEL.
*   IMA ensures system integrity by validating file authenticity through digital hashes and signatures stored in the system.

[Multiple choice questions](#contents.xhtml_sc2_320a)

1.  What is CentOS Stream primarily used for in the Red Hat ecosystem?
    1.  To provide a stable release for enterprise applications
    2.  To act as a rolling preview platform for the next RHEL minor releases
    3.  To replace Fedora as the upstream for RHEL
    4.  To serve as a backup system for RHEL
2.  What is the purpose of the service used to reboot Red Hat Enterprise Linux?
    1.  It allows the kernel to reboot faster
    2.  It requires less disk space
    3.  It enables updates to be applied without rebooting
    4.  It simplifies the user interface
3.  Which feature does VDO provide?
    1.  Increased CPU performance
    2.  Data deduplication and compression
    3.  Enhanced graphic processing
    4.  Reduced RAM usage
4.  What is the primary function of SSSD?
    1.  To monitor system performance
    2.  To manage user authentication and integration with identity providers
    3.  To update system software
    4.  To backup system data

[Answers](#contents.xhtml_sc3_321a)

1\. b

2\. c

3\. b

4\. b

[Questions](#contents.xhtml_sc2_322a)

1.  Explain the significance of CentOS Stream in the development lifecycle of RHEL. How does it improve the feedback loop between Red Hat and its users?
2.  Discuss the benefits and potential challenges of implementing kernel live patching in a production environment. What considerations should system administrators keep in mind when using this feature?
3.  Describe how VDO volumes can impact an organization's storage strategy. What types of environments would benefit the most from VDO volumes?
4.  Analyze the role of SSSD in enhancing system authentication. How does SSSD improve security and efficiency in managing user credentials across different platforms?
5.  What opportunities does the introduction of UBIs provide to developers outside the traditional Red Hat subscription model?
6.  Evaluate the impact of using cloud integration features with major providers like AWS, Google Cloud Platform, Microsoft Azure and VMware. How does Red Hat's approach to cloud integration benefit organizations looking to scale their operations?
7.  Discuss the role of IMA in maintaining system integrity. How does IMA contribute to a more secure Linux environment?
8.  Explore the potential of containers and virtualization in the RHCE context. How do these technologies transform application deployment and management?

[Key terms](#contents.xhtml_sc2_323a)

*   Basic Input or Output System (BIOS):  BIOS is firmware embedded on a computer's motherboard that initializes hardware components during the boot process and provides a basic interface for configuring system settings.
*   Power-on Self-Test (POST): POST is a diagnostic process performed by a computer's firmware BIOS during startup to verify and initialize essential hardware components, ensuring the system's operational readiness.
*   Tuned: It is a system tuning daemon in RHEL that adapts the system performance to suit its usage.
*   Open Container Initiative (OCI): OCI is a project under the Linux foundation designed to create open industry standards around container formats and runtime.
*   Container file: It is a configuration file similar to a Dockerfile used to define the steps for building a container image, typically in non-Docker environments like Podman and Buildah to emphasize its brand-agnostic nature.
*   Integrity Measurement Architecture (IMA): IMA is a Linux security feature that checks and records if files have been altered to help detect unauthorized changes.

# [CHAPTER 8Performance Optimization and Troubleshooting](#contents.xhtml_ch08a)

[Introduction](#contents.xhtml_sc2_324a)

In [Chapter 7](#ch07.xhtml), Emerging Technologies Integration we explored the integration of emerging technologies such as containers and virtualization, outlining how they are becoming integral to modern IT infrastructures. Building upon this foundation, [Chapter 8](#ch08.xhtml), Performance Optimization and Troubleshooting shifts our focus towards ensuring that these technologies not only integrate smoothly but also perform optimally and remain robust under various operational conditions.

As we navigate through the complexities of performance optimization and systematic troubleshooting, this chapter serves as a crucial guide for engineers aiming to enhance the efficiency and reliability of their systems. We will explore a variety of optimization strategies and delve into practical troubleshooting techniques that are essential for diagnosing and resolving issues effectively. From tuning system performance to mastering the art of systematic troubleshooting, we provide us with the knowledge and tools necessary to tackle common and complex problems alike.

As we enhance our troubleshooting skills, prepare to test these abilities in real-world scenarios in [Chapter 9](#ch09.xhtml), Practice Exams and Scenarios where we will engage with practice exams and simulation scenarios. This upcoming chapter is designed to refine our problem-solving techniques further and ensure our readiness for the RHCE certification exam, mirroring the real challenges we face and providing the strategic insights needed to excel.

By the end of this chapter, we understand the critical technical strategies for optimizing system performance but also be equipped with a robust framework for troubleshooting that can be applied across various systems and situations within the RHEL environment.

[Structure](#contents.xhtml_sc2_325a)

The chapter covers the following topics:

*   Bootstrap
*   Root password reset
*   Troubleshooting
*   Service failure
*   Strategies for optimizing system performance
*   Ansible
*   Best practices for role and collection testing

[Objectives](#contents.xhtml_sc2_326a)

The primary objectives of this chapter focus on enhancing the performance and reliability of RHEL systems. First, we aim to optimize system performance by employing various tools and techniques to assess and improve the efficiency of these systems. Additionally, we will develop a systematic approach to troubleshooting system issues, enabling us to diagnose and resolve problems such as performance bottlenecks and operational failures effectively. Furthermore, we will execute recovery techniques that include managing the boot process and resetting root passwords to ensure system resilience. Finally, we will apply practical skills through engaging exercises that simulate real-world scenarios, preparing participants for the troubleshooting and optimization tasks they will encounter in the RHCE exam.

[Bootstrap](#contents.xhtml_sc2_327a)

Booting a Linux system is a process that involves various stages, from firmware detection to the launch of the default target. Historically, Linux was only the name of the kernel, the essential software that communicates with the hardware, a project started in 1991 by Linus Torvalds. A successful bootstrap process moves from the hardware firmware, bootloader program, kernel and systemd initialization. This foundational knowledge is essential for troubleshooting and optimizing system performance. The full process for a physical machine involves the following steps:

1.  The firmware (BIOS or UEFI) finds the boot media after the hardware POST. We can typically configure the boot media using the key F2 or F12 on our keyboard.
2.  The boot loader starts and the Master Boot Record (MBR) or GUID Partition Table (GPT) that uses Universally Unique Identifiers (UUIDs) also known as Globally Unique Identifiers (GUIDs).
3.  The operating system selection menu appears (typically GRUB, short for Grand Unified Bootloader (GNU))  with the kernel available in the system with a timeout.
4.  The boot loader stage two starts and loads the selected kernel and initramfs containing kernel modules for all the hardware, initialization scripts, and a copy of the systemd.
5.  The kernel loads the necessary hardware drivers from initramfs.
6.  The kernel launches the startup process systemd as PID 1 since RHEL8 systemd is linked as /sbin/init.
7.  The systemd starts the services defined in the default.target profile. The first step executes all units for the initrd.target target. One unit takes care of mounting the root filesystem under the /sysroot directory, and the kernel switches (pivots) the root file system from initramfs to the root file system under /.
8.  The systemd program re-executes itself using the copy installed on the disk and executes the units defined in the default target (via command line or configured on the system in /etc/systemd/system/default.target).

The user is typically prompted to authenticate via a console or graphical user interface. On a virtualized system, the hypervisor software (VMware, XEN, KVM or QEMU, Hyper-V, Proxmox, etc.) handles some of the physical interaction with the hardware.

| Note: For reference, different Linux distributions might use different projects for bootloader or process startup services. |

The systemd program is fully configurable and enables us to create customized boot sequences. The most common systemd targets are shown in [Table 8.1](#ch08.xhtml_tab8-1):

| Target | Description |
| graphical.target | Multi-user system with graphical and text logins. |
| multi-user.target | Multi-user system with text logins oily. |
| rescue.target | Basics system initialization with only sulogin prompt. |
| emergency.target | Pivot is complete, and the system root is mounted on or read-only and sulogin prompt. |

Table 8.1: Most common systemd targets

Our system might not include all the targets listed in [Table 8.1](#ch08.xhtml_tab8-1), particularly if the graphical user interface is not installed. In such cases, the system will primarily default to targets like multi-user.target and rescue.target, which are designed for text-based logins and minimal system initialization. This limitation can restrict user access to graphical features and functionalities, thereby affecting the overall usability of the system. We can list all the available systemd targets in our system using the command, as follows:

$ systemctl list-units --type=target –all

A target can include or depend on another target, for example, the graphical.target that depends on the multi-user.target that depends by basics.target. We can list all the units and target dependencies using the command, as follows:

$ systemctl list-dependencies graphical.target

The superuser (root) can switch at runtime to a different target that supports the isolate mode (the AllowIsolate=yes is present in their unit files) using the following command.

# systemctl isolate multi-user.target

We can read the current default target using the following command:

$ systemctl get-default

The super user (root) can change the default target for the system using the following command:

# systemctl set-default multi-user.target

We can select a different target at boot time, appending the following option to the kernel command line from the boot loader, as follows:

systemd.unit=rescue.target

In order to select a different target, we need to interrupt the boot loader countdown by pressing any characters except Enter. Then, move the cursor to the kernel entry that we want to modify, press the e key to edit, and append the text at the end of the line that begins with Linux.

| Note that when we select the emergency.target, the root filesystem is mounted as read-only. Use the remount, rw option of the mount command to remount in read and write mode. |

[Root password reset](#contents.xhtml_sc2_328a)

Resetting the root password in RHEL when the current password is lost involves steps requiring access to the system's bootloader and the command line.

Following are the steps to accomplish this task:

1.  Reboot the system: Reboot our RHEL system.
2.  Interrupt the boot process: As the system starts booting, interrupt the boot loader countdown by pressing any key (except the Enter key).
3.  Edit kernel entry: Use the arrow keys to navigate to the kernel entry we wish to boot. Press e to edit the selected entry.
4.  Modify the kernel command line:
    1.  Find the line that starts with Linux.
    2.  Move the cursor to the end of this line.
    3.  Append rd.break to the end of the line. This command makes the system stop in the early stage of booting (initramfs phase), allowing access to a root shell.
5.  Boot with the modified configuration:  Press Ctrl + x to boot with the modified kernel command line.
6.  Remount the root file system with read or write access: Once the root shell is accessible, remount the root file system as read or write by executing, as follows:

    # mount -o remount,rw /sysroot

7.  Change the root to the system root (chroot): Change the root to the system root directory to perform tasks as if we were in the actual system root. Run as follows:

    # chroot /sysroot

8.  Reset the root password: Reset the root password by running the following:

    # passwd root

    Enter the new password and confirm it when prompted.

9.  Ensure SELinux file relabeling on reboot: To make sure SELinux contexts are correctly applied on the next boot, create an .autorelabel file by running the following:

    # touch /.autorelabel

10.  Exit and reboot:
    1.  Type exit once to leave the chroot environment.
    2.  Type exit again to exit the initramfs debug shell. This will cause the system to continue booting.
    3.  The system will then automatically perform a full SELinux relabel which may take some time, and then reboot.
11.  Log in with the new root password: After the system reboots, we can log in as the root user with the new password we have just set.

| Notes: Once access to the system has been restored, it is crucial to address the security implications of the actions taken. An open root shell accessible during boot presents a considerable security risk, and it is essential to adhere to organizational security policies and best practices to mitigate this risk. If any debug shells or services were enabled to facilitate the recovery process, they must be disabled promptly to secure the system. Additionally, always consult the official Red Hat documentation for the specific version of the operating system being used, as procedures can vary slightly between versions. |

By following these steps, we can reset the root password on a RHEL system, even if the current root password is unknown.

[Troubleshooting](#contents.xhtml_sc2_329a)

In the realm of Linux system administration, ensuring that your system boots correctly is essential, but occasionally, issues with the file system or misconfigurations can prevent a successful startup. Problems like a corrupt file system or errors in critical files like /etc/fstab can lead to the system dropping into an emergency shell, leaving administrators scrambling for solutions. This section provides a detailed, step-by-step guide on diagnosing and resolving these boot-related file system issues. From accessing the emergency shell to fixing configuration errors and reloading system services, this guide equips system administrators with the knowledge to tackle common boot issues effectively and quickly get systems back online. Whether you are dealing with incorrect mount points or corrupt file systems, the strategies outlined here will guide you through a successful recovery.

[File system](#contents.xhtml_sc3_330a)

Manually repairing file-system configuration or corruption issues that impede the boot process is a crucial skill for system administrators. Common file system problems such as errors in /etc/fstab or a corrupt file system can prevent a system from booting properly. Following are the steps on diagnosing and fixing these issues:

1.  Understanding the most common file system issues:
    *   Corrupt file system: systemd attempts an automatic repair. If the issue is severe, it drops to an emergency shell.
    *   Nonexistent device or UUID in /etc/fstab: systemd waits for the device to become available. If it does not, the system enters an emergency shell after a timeout.
    *   Nonexistent mount point in /etc/fstab: This leads to an emergency shell.
    *   Incorrect mount option in /etc/fstab: The system will boot to an emergency shell.
2.  Access the emergency shell:

    If systemd enters an emergency shell, log in with the root password. Alternatively, we can force the system to boot into an emergency shell by appending systemd.unit=emergency.target to the kernel command line in the boot loader.

3.  Diagnose the file system issue:

    Check the /etc/fstab file for errors such as incorrect UUIDs, non-existent device references, invalid mount points or wrong mount options. For filesystem corruption issues, use filesystem check tools such as fsck. Be cautious with fsck on mounted filesystems.

4.  Editing /etc/fstab:

    If the issue is related to /etc/fstab, open the file for editing, use the following:

    vi /etc/fstab

    Make necessary corrections such as updating UUIDs, fixing mount points or adjusting mount options.

5.  Reloading systemd daemon:

    After editing  /etc/fstab, reload the systemd daemon to apply changes, as follows:

    systemctl daemon-reload

6.  Reboot the system:

    Once corrections are made, exit the emergency shell and reboot the system, as follows:

    # reboot

| Notes: The nofail mount option in /etc/fstab allows the system to continue booting even if a filesystem fails to mount. While useful, it should be used carefully, as it may cause applications to start without the necessary storage, leading to critical issues. For repairing corrupted filesystems, tools like fsck are effective, but it is essential to unmount the filesystem or boot into a state where it is not in use before running the tool. Additionally, it is crucial to maintain backups of essential files, particularly when making changes to system files like /etc/fstab or performing filesystem repairs. For further guidance, consulting the man pages (e.g., man systemd-fsck, man systemd-fstab-generator, man  systemd.mount) is recommended for detailed information on the respective commands and their use. |

By following these steps, administrators can effectively address and resolve file system issues that prevent a Linux system from booting properly.

[Virtual Data Optimizer](#contents.xhtml_sc3_331a)

VDO is a powerful tool in RHEL for optimizing storage efficiency. By leveraging deduplication, compression and thin provisioning, VDO helps enterprises reduce their physical storage footprint and lower costs. Implementing VDO in RHEL is straightforward and can lead to significant improvements in storage management and performance. VDO is a feature in RHEL that optimizes data storage by applying data deduplication, compression and thin provisioning to block storage devices. These techniques help minimize the physical storage footprint while maintaining the logical view of the data. VDO is particularly beneficial in environment with large volumes of redundant data such as virtual machine images, backups and content repositories.

Following are the key features of VDO:

*   Data deduplication: VDO identifies and eliminates duplicate blocks of data at a granular level, storing only unique instances of the data.
*   Data compression: VDO compresses the stored data, further reducing the physical space required.
*   Thin provisioning: VDO allocates storage capacity on-demand, allowing for more efficient use of storage resources.

[Installation](#contents.xhtml_sc3_332a)

To successfully set up VDO on our system, follow the steps to install the necessary packages and load the kernel module:

1.  Install the VDO packages, as follows:

    # dnf install kmod-kvdo vdo

2.  Load the KVDO kernel module:

    # modprobe kvdo

[Configuring and managing VDO](#contents.xhtml_sc3_333a)

1.  Create a VDO volume:

    # vdo create --name=<vdo_name> --device=<block_device> --vdoLogicalSize=<size>

    Replace <vdo_name> with the desired name for our VDO volume, <block_device> with the path to the block device and <size> with the logical size of the VDO volume.

2.  Start the VDO volume:

    # vdostart <vdo_name>

3.  Format the VDO volume with a filesystem:

    # mkfs.xfs /dev/mapper/<vdo_name>

    Replace <vdo_name> with the name of our VDO volume.

4.  Mount the VDO volume:

    # mount /dev/mapper/<vdo_name> /mnt/<mount_point>

    Replace <mount_point> with the desired mount point.

[Monitoring VDO](#contents.xhtml_sc3_334a)

Use the vdostats command to monitor the VDO volume:

# vdostats --human-readable

This command provides detailed statistics about space savings, physical storage usage and performance metrics.

[Log files](#contents.xhtml_sc3_335a)

Troubleshooting problems in a Linux system often involves analyzing log files to understand what went wrong. In RHEL, systemd-journald and rsyslog work together to provide a robust logging infrastructure. systemd-journald focuses on log collection and local storage, while rsyslog provides advanced log processing, filtering and forwarding capabilities. Understanding and configuring these tools effectively is essential for comprehensive log management and troubleshooting in RHEL.

[systemd](#contents.xhtml_sc3_336a)

systemd is the system and service manager for RHEL. It is responsible for initializing the system, managing services and handling the system's lifecycle. Following is an overview of how to work with systemd in RHEL:

[Basic concepts](#contents.xhtml_sc4_337a)

In the context of systemd, understanding the role of unit files and targets is essential for effective system management. Unit files serve as the building blocks of systemd, representing various system resources and services, while targets are used to group these units and facilitate synchronization during the boot process.

Following are the specific details of unit files and targets:

*   Unit files: systemd use unit files to represent system resources and services. These unit files have different types, such as service units (.service), socket units (.socket), and target units (.target).
*   Targets: Targets are used to group units and serve as synchronization points during the boot process. For example, multi-user.target and graphical.target.

[Common commands](#contents.xhtml_sc3_338a)

Following are the ways for managing services:

*   Starting a service:

    sudo systemctl start <service_name>

    Following is an example:

    sudo systemctl start httpd

*   Stopping a service:

    sudo systemctl stop <service_name>

*   Restarting a service:

    sudo systemctl restart <service_name>

*   Reloading a service,  if the service supports it:

    sudo systemctl reload <service_name>

*   Enabling a service, start on boot:

    sudo systemctl enable <service_name>

*   Disabling a service, do not start on boot:

    sudo systemctl disable <service_name>

*   Checking the status of a service:

    sudo systemctl status <service_name>

Following are the ways for managing system state:

*   Rebooting the system:

    sudo systemctl reboot

*   Shutting down the system:

    sudo systemctl poweroff

*   Changing the system target:

    sudo systemctl isolate <target>

    Following is an example:

    To switch to multi-user mode without a graphical interface:

    sudo systemctl isolate multi-user.target

Following are the ways for analyzing system boot and services:

*   View boot logs:

    sudo journalctl -b

*   Follow real-time logs:

    sudo journalctl -f

*   View logs for a specific service:

    sudo journalctl -u <service_name>

    Following is an example:

    sudo journalctl -u httpd

[Configuring unit files](#contents.xhtml_sc3_339a)

Unit files are typically located in /etc/systemd/system/ and /lib/systemd/system/. We can create or edit these files to configure services. To create and manage a custom service using system.

Follow the steps which include creating a service unit file and reloading systemd to ensure the changes take effect:

*   Creating a custom service: Create a file /etc/systemd/system/my_service.service with the following content:

    [Unit]

    Description=My Custom Service

    After=network.target

    [Service]

    ExecStart=/usr/bin/my_custom_service

    Restart=always

    [Install]

    WantedBy=multi-user.target

*   Reloading systemd to apply changes:

    sudo systemctl daemon-reload

By mastering these commands and concepts, we can effectively manage system services and the overall state of systems running RHEL with systemd.

[Search logs for relevant entries](#contents.xhtml_sc3_340a)

Use tools like grep, awk, and sed to search for specific entries in log files, as follows:

*   Search for error messages, as follows:

    grep -i error /var/log/messages

*   Search for a specific timestamp, as follows:

    grep "Jun 5 14:30" /var/log/messages

*   Search within journalctl, as follows:

    journalctl | grep -i error

[syslog](#contents.xhtml_sc3_341a)

Logging in RHEL is performed by syslog files and involves understanding the syslog architecture and using specific tools and commands to interpret log messages. The systemd-journald tool is responsible for collecting and managing log data in RHEL. It captures log data from various sources including the kernel, system services and applications.

Following are the key points and steps for reviewing syslog files:

*   Syslog architecture
    *   Syslog protocol: Many programs use the syslog protocol to log events. Each log message is categorized by a facility (the type of message) and a priority (the severity of the message).
    *   Facilities and priorities: The facilities are predefined categories for log messages (e.g., mail, auth). The priorities range from emerg (the system is unusable) to debug (debugging-level messages).
*   Common syslog files
    *   /var/log/messages: Stores most syslog messages except for authentication, mail, cron jobs and debugging-related messages.
    *   /var/log/secure: Stores messages related to security and authentication.
    *   /var/log/maillog: Stores mail server-related messages.
    *   /var/log/cron: Stores messages related to cron jobs.
*   Reviewing syslog files
    *   Viewing logs: Use text utilities like less, tail and cat to inspect logs.
        *   Example: less /var/log/messages
    *   Filtering Logs: Use grep to filter log messages based on specific criteria.
        *   Example: grep "error" /var/log/messages
*   Analyzing logs: Understand the format of the log messages. A typical log message format might look like:

    Feb 11 20:11:48 localhost 172.25.0.10 port 59344 ssh2

[Configuring and testing syslog](#contents.xhtml_sc4_342a)

Configuring the rsyslog service is essential for effective logging and monitoring of system messages.

Following sections outline how to set up rsyslog configuration rules and test the logging functionality using the logger command:

*   rsyslog configuration: The rsyslog service sorts and writes syslog messages to log files based on configuration rules specified in /etc/rsyslog.conf and files in /etc/rsyslog.d.

    Following is an example for configuration rule to log all debug messages:

    *.debug /var/log/debug.log

*   Testing configuration: Use the logger command to send test messages to the syslog.

    Following is an example for testing configuration:

    logger -p local7.notice "Test log entry"

By following the above, we can effectively review and interpret syslog files to troubleshoot issues and monitor system status in RHEL.

[journalctl](#contents.xhtml_sc3_343a)

Reviewing system journal entries is crucial for troubleshooting problems and reviewing system status in RHEL.

Following is a step-by-step guide on how to effectively use the journalctl command to find and interpret entries in the system journal:

1.  Understanding the system journal:

    The systemd-journald service manages the system journal, storing logs in a structured, indexed binary format.

    The journal includes extensive information about log events such as syslog facilities and priorities.

2.  Accessing the journal:

    Use the journalctl command to access the journal. Running journalctl as root provides full access, while regular users might have restricted access. By default, the system journal is stored in /run/log and is cleared after a reboot.

3.  Viewing journal entries:

    Run journalctl to view all messages in the journal, as follows:

    # journalctl

    Entries at notice or warning priority appear in bold, while entries at error priority or higher are in red.

4.  Filtering journal entries:

    To view only the last n number of entries, use the following:

    # journalctl -n [number]

    For real-time monitoring of the journal, similar to tail -f, use the following:

    # journalctl -f

5.  Filtering by priority:

    To filter journal entries by priority, use the following:

    # journalctl -p [priority-level]

    Priority levels include debug, info, notice, warning, err, crit, alert, and emerg.

6.  Time-based filtering:

    Filter entries within a specific time frame using --since and --until options:

    # journalctl --since "YYYY-MM-DD hh:mm:ss" --until "YYYY-MM-DD hh:mm:ss"

    We can also use relative times, like –‘since 1 hour ago’.

7.  Use verbose mode to see extra fields attached to log entries, which can be used for more granular filtering, as follows:

    # journalctl -o verbose

    Filter based on specific journal fields such as _COMM, _EXE, _PID, _UID, or _SYSTEMD_UNIT.

8.  Granular search queries:

    Combine multiple journal fields to form detailed search queries. For example:

    # journalctl _SYSTEMD_UNIT=sshd.service _PID=1182

    To make journal logs persistent across reboots, configure /etc/systemd/journald.conf and set the storage parameter to persistent.

After making changes to the systemd configuration, remember to reload the systemd daemon. By following the above steps, system administrators can effectively utilize the system journal to troubleshoot issues and monitor the system status in RHEL.

[rsyslog](#contents.xhtml_sc3_344a)

The rsyslog tool is a powerful and flexible logging daemon that supports a wide range of input sources and output destinations. It supports various log input sources including systemd-journald can filter and route log messages based on content, supports remote logging and can store logs in various formats including plain text and database formats.

To effectively manage logging on our system, it is important to understand the configuration of the rsyslog service.

Following is the main configuration files, basic settings, and rules for log file management, along with instructions on restarting the service and forwarding logs to a remote server:

*   Configuration files:
    *   Main configuration file: /etc/rsyslog.conf
    *   Additional configuration files can be placed in /etc/rsyslog.d/.
*   Basic configuration:
    *   Modules:

        module(load="imuxsock") # Listen to the local syslog socket

        module(load="imjournal") # Read from systemd journal

    *   Rules for log files:

        *.info;mail.none;authpriv.none;cron.none /var/log/messages

        authpriv.* /var/log/secure

        mail.* /var/log/maillog

        cron.* /var/log/cron

*   Restarting rsyslog:
    *   After making changes to the configuration, restart rsyslog, as follows:

        sudo systemctl restart rsyslog

    *   Forward logs to a remote server:

        *.* @@remote-server:514

[Interaction between systemd-journald and rsyslog](#contents.xhtml_sc3_345a)

Effective log management is crucial for monitoring system performance and troubleshooting issues.

Following the processes of log collection, forwarding, storage, and analysis, detailing how systemd-journald and rsyslog work together to enhance logging capabilities and facilitate centralized management:

*   Log collection:
    *   systemd-journald collects logs from various sources and stores them in a binary format.
    *   rsyslog can read logs from systemd-journald through the imjournal module.
*   Log forwarding and storage:
    *   rsyslog processes logs and can forward them to remote servers or store them in various formats.
    *   This setup allows for centralized log management and advanced log processing capabilities.
*   Log querying and analysis:
    *   Use journalctl for querying logs collected by systemd-journald.
    *   Use rsyslog configuration to filter, route, and manage logs as required.

[Log rotation](#contents.xhtml_sc3_346a)

Log rotation is the process of automatically managing large log files by renaming the current log file and creating a new one, optionally compressing and deleting older log files. To manage log file size and ensure efficient storage, the logrotate utility is essential for automatic log rotation in Linux systems. This section provides an overview of logrotate configuration, including the main configuration file and an example of how to set up log rotation for specific log files.

Following is the key information to remember:

*   Logrotate configuration: Logrotate is the utility used for log rotation in Linux.
*   Configuration file: /etc/logrotate.conf
*   Example configuration:

    /var/log/messages {

    weekly

    rotate 4

    compress

    delaycompress

    missingok

    notifempty

    create 0640 root utmp

    sharedscripts

    postrotate

    /usr/bin/systemctl reload rsyslog > /dev/null 2>&1 || true

    endscript

    }

Key directives

*   weekly: Rotate logs weekly.
*   rotate 4: Keep 4 rotated logs before deleting old ones.
*   compress: Compress rotated log files.
*   missingok: Do not issue an error if the log file is missing.
*   notifempty: Do not rotate empty log files.
*   create: Create a new log file with specified permissions after rotation.
*   postrotate/endscript: Commands to run after log rotation for example, reload rsyslog.

[Service failure](#contents.xhtml_sc2_347a)

Service failure is the most common error that might come in our way. By understanding syslog priorities, rsyslog rules and log rotation, we can effectively manage and optimize our RHEL systems. Using tools like journalctl, grep and logrotate, we can diagnose issues, maintain log files and ensure the smooth operation of our system.

[Apache](#contents.xhtml_sc3_348a)

We follow the steps outlined below to troubleshoot issues with the Apache HTTP Server that are failing to start.

Following steps will help we verify the service's status, check for recent logs, search for potential errors, and increase logging verbosity if needed:

*   Check the status of the service:

    sudo systemctl status httpd

*   View recent logs for the service:

    journalctl -u httpd

*   Search for errors in the Apache error log:

    less /var/log/httpd/error_log

*   Look for configuration issues:

    grep -i "syntax error" /var/log/httpd/error_log

*   If necessary, increase the verbosity of the logs and restart the service:
    *   Modify the Apache configuration to enable more detailed logging.
    *   Restart the service, as follows:

        sudo systemctl restart httpd

    *   Check the logs again for more detailed output.

[SSH](#contents.xhtml_sc3_349a)

Let us troubleshoot a scenario where a user has trouble connecting to the  ssh  service. The following steps can be performed to help we check the service status, view logs, and search for authentication errors:

*   Check SSH service status:

    systemctl status sshd

*   View recent SSH logs:

    journalctl -u sshd

*   Search for authentication errors:

    grep -i "authentication failure" /var/log/secure

[Network](#contents.xhtml_sc3_350a)

Network troubleshooting in RHEL involves a series of steps and tools to diagnose and fix network-related issues.

Following are steps of common commands and techniques for effective network troubleshooting.

1.  Check network configuration:
    *   IP address:

        ip addr show

    *   Routing table:

        ip route show

    *   DNS configuration:

        cat /etc/resolv.conf

2.  Verify connectivity:
    *   Ping:

        ping <hostname_or_ip>

        Example:

        ping 8.8.8.8

        ping www.example.com

    *   Traceroute:

        traceroute <hostname_or_ip>

        Example:

        traceroute www.example.com

3.  Check active connections and listening ports:
    *   Netstat:

        netstat -tuln

        *   -t: TCP
        *   -u: UDP
        *   -l: Listening
        *   -n: Numeric
    *   SS (more modern alternative to netstat):

        ss -tuln

4.  Inspect firewall settings:
    *   Firewall-cmd (if using firewalld):
        *   Check firewall status:

            sudo firewall-cmd –state

        *   List all rules:

            sudo firewall-cmd --list-all

5.  Test specific ports:
    *   Telnet:

        telnet <hostname_or_ip> <port>

        Example: telnet www.example.com 80

    *   Netcat:

        nc -vz <hostname_or_ip> <port>

        Example: nc -vz www.example.com 80

[Common tools for network troubleshooting](#contents.xhtml_sc4_351a)

To diagnose and troubleshoot network-related issues, we utilize the following command-line tools to check connectivity, trace packet paths, analyze network traffic, query DNS servers, and manage network connections as follows:

*   ping:  Tests connectivity to another host.

    Example: ping google.com

*   traceroute: Traces the path packets take to a network host.

    Example: traceroute google.com

*   netstat or ss:  Displays network connections, routing tables, interface statistics, masquerade connections and multicast memberships.

    Example with ss: ss -tuln

*   tcpdump:  Captures and analyzes network packets.

    Example: sudo tcpdump -i eth0

*   dig and nslookup: Queries DNS servers.
    *   Example with dig: dig example.com
    *   Example with nslookup: nslookup example.com
*   nmcli: Command line tool for managing network manager.
    *   Show device status: nmcli device status
    *   Connect to a network: nmcli  device wifi connect <SSID> password <password>

To manage and monitor network interfaces and traffic, the following commands can be useful for checking ARP tables, bringing network interfaces up or down, and monitoring traffic bandwidth as follows:

*   Checking ARP tables:

    Displays the kernel's IPv4 network neighbor cache:

    ip neigh show

*   Checking network interfaces:

    Bring an interface up or down.

    sudo ip link set <interface> up

    sudo ip link set <interface> down

    Example:

    sudo ip link set eth0 up

*   Monitoring network traffic:
    *   iftop: Displays bandwidth usage on an interface by host.
    *   nload: Monitors incoming and outgoing traffic separately on a network interface.

[Diagnosing a network issue](#contents.xhtml_sc4_352a)

To diagnose network connectivity issues, we use the following commands to test connectivity, check interface status, inspect routing, DNS resolution, and analyze network traffic as follows:

*   Ping a known host:

    ping google.com

*   Check the network interface:

    ip addr show eth0

*   Verify routing:

    ip route show

*   Check DNS resolution:

    dig google.com

*   Inspect active connections:

    ss -tuln

*   Capture and analyze packets:

    sudo tcpdump -i eth0

By following these steps and using the mentioned tools, we can diagnose and resolve most network-related issues in RHEL.

[Strategies for optimizing system performance](#contents.xhtml_sc2_353a)

The following are strategies for optimizing system performance that involve analyzing and optimizing processes, understanding process states and signals, adjusting process priorities, and effectively using commands like ps, kill, nice, renice and ansible for better process management.

[Processes](#contents.xhtml_sc3_354a)

Processes in Linux can be in various states during their lifecycle.

Following are the primary process states:

*   Running (R): The process is either executing on the CPU or is ready to run.
*   Sleeping (S): The process is waiting for an event to complete (e.g., I/O operation).
    *   Interruptible (S): Can be woken up by signals.
    *   Uninterruptible (D): Cannot be woken up by signals (usually waiting on I/O).
*   Stopped (T): The process has been stopped, usually by receiving a signal.
*   Zombie (Z): The process has completed execution, but its parent has not yet read its exit status.

    We can view process states using the ps command:

    ps -aux

[Process signals](#contents.xhtml_sc4_355a)

Signals are a way to communicate with and control processes in Linux. They are used to notify processes of events or to instruct them to perform specific actions as follows:

*   SIGHUP (1): Hang up detected on controlling terminal or death of controlling process.
*   SIGINT (2): Interrupt from the keyboard (Ctrl+C).
*   SIGQUIT (3): Quit from keyboard (Ctrl+\).
*   SIGKILL (9): Kill signal that forces the process to terminate immediately. Cannot be caught or ignored.
*   SIGTERM (15): Termination signal that allows the process to clean up before exiting. Can be caught and ignored.
*   SIGSTOP (19): Stop the process execution. It cannot be caught or ignored.
*   SIGCONT (18): Continue the execution of a stopped process.

    We can send signals to processes using the kill command:

    kill -SIGTERM <pid> # Replace <pid> with the process ID

    Or, with signal numbers:

    kill -15 <pid>

[Common commands](#contents.xhtml_sc4_356a)

To manage processes using signals in Linux, we list all available signals, send specific signals to processes, or terminate processes by their PID.

Following are some useful commands:

*   List all signals:

    kill -l

*   Send a signal:

    kill -<signal_number> <pid>

Following is an example:

*   Kill a process with PID 1234:

    kill -9 1234

Understanding process states and signals is crucial for effective process management and troubleshooting in Linux systems.

[Using ps to view processes](#contents.xhtml_sc4_357a)

The ps command is used to display information about active processes. To manage and view system processes in Linux, we can use the following commands to list, filter, and display processes in various formats:

*   List all processes:

    ps -e

*   Detailed view of all processes:

    ps -ef

*   View processes for a specific user:

    ps -u <username>

*   Full format listing of all processes:

    ps aux

*   Display a tree of processes:

    ps -e –forest

    Following is an example:

    ps aux | grep httpd

    This command lists all processes and filters the results to show only those related to httpd.

[Using kill to terminate processes](#contents.xhtml_sc4_358a)

The kill command sends signals to processes, instructing them to terminate or perform specific actions. To manage and terminate processes using the command line, we can use the following commands to kill processes by their PID, send specific signals, and terminate multiple processes simultaneously:

*   Terminate a process using  process identifier (PID):

    kill <pid>

*   Send a specific signal (e.g., SIGKILL):

    kill -9 <pid>

*   Terminate multiple processes:

    kill -9 <pid1> <pid2> <pid3>

*   Send a signal to processes by name:

    pkill <process_name>

    Following is an example:

    kill -TERM 1234

    This command sends the SIGTERM signal to the process with PID 1234.

[Using nice and renice to adjust process priority](#contents.xhtml_sc4_359a)

The nice command runs a program with a modified scheduling priority. The renice command changes the priority of an already running process. To manage process priorities using the nice and renice commands, we start processes with a specific priority, adjust the priority of running processes, or modify the priority of all processes for a particular user.

Following are some useful commands:

*   Start a process with a specific nice value:

    nice -n <priority> <command>

    Priority ranges from -20 (highest priority) to 19 (lowest priority). Default is 0.

    Following is an example:

    nice -n 10 tar czf archive.tar.gz /path/to/directory

    This command runs tar with a lower priority.

*   Change the priority of an existing process:

    renice <priority> -p <pid>

*   Change the priority of processes by user:

    renice <priority> -u <username>

    Following is an example:

    renice -n -5 -p 1234

    This command increases the priority of the process with PID 1234.

[Practical examples](#contents.xhtml_sc4_360a)

To manage processes, change their priorities, and kill them, when necessary, we can use the following commands for viewing, modifying, and terminating processes:

*   Viewing processes:

    ps aux | less

    This lists all processes in a detailed format and allows scrolling.

*   Killing a process:

    ps aux | grep firefox

    kill -9 <firefox_pid>

    This finds PID of the Firefox process and forcefully terminates it.

*   Running a command with lower priority:

    nice -n 10 long_running_script.sh

    This runs the script with a lower priority, allowing other processes to have more CPU time.

*   Changing priority of a running process:

    ps aux | grep python

    renice -n 5 -p <python_pid>

    This finds the PID of a Python process and lowers its priority.

By mastering these commands, we can effectively manage processes, ensure critical tasks get enough CPU time and gracefully handle resource allocation in a Linux environment.

[Cron](#contents.xhtml_sc3_361a)

The cron service in Linux, discussed in [Chapter 3](#ch03.xhtml), Red Hat System Administration, section Schedule future tasks, allows scheduling tasks to run automatically at specified intervals using cron jobs, which can automate routine tasks such as backups, system maintenance, and monitoring.

[Ansible](#contents.xhtml_sc2_362a)

Troubleshooting Ansible involves identifying and resolving issues that arise during the use of Ansible for automation tasks.

[Playbook](#contents.xhtml_sc3_363a)

Following are some common troubleshooting steps and techniques:

1.  Understanding common issues:
    *   Syntax errors:
        *   Check for syntax errors in our playbooks, roles, and variables.
        *   Use ansible-playbook --syntax-check <playbook.yml> to verify the syntax before running a playbook.
    *   Indentation errors:

        Ensure correct indentation in YAML file format. YAML is indentation sensitive and incorrect indentation can cause errors.

    *   Missing variables:
        *   Make sure all variables used in playbooks or roles are defined.
        *   Use -e to pass extra variables if needed.
    *   Connection issues:
        *   Verify SSH connectivity to the target nodes.
        *   Check SSH keys and permissions.
        *   Ensure the target nodes' IP addresses and hostnames are correctly specified in the inventory file.
    *   Module errors:
        *   Review the output for specific module errors.
        *   Ensure that all required modules are installed on the control node.
2.  Debugging techniques:
    *   Verbose output:

        Use -v, -vv, or -vvv for verbose output to get detailed information about what Ansible is doing.

        ansible-playbook -vvv <playbook.yml>

    *   Check mode:

        Use --check to run a playbook in check mode, which simulates the changes without applying them.

        ansible-playbook  <playbook.yml> --check

    *   Dry run:

        Combine --check with -D for a detailed dry run.

        ansible-playbook <playbook.yml> --check -D

3.  Common commands for troubleshooting:
    *   Syntax check:

        ansible-playbook --syntax-check <playbook.yml>

    *   List hosts:

        ansible all --list-hosts -i <inventory_file>

    *   Ping test:

        ansible all -m ping -i <inventory_file>

    *   Gather facts:

        ansible all -m setup -i <inventory_file>

    *   Test playbook:

        ansible-playbook <playbook.yml> --limit <hostname>

4.  Troubleshooting playbook execution:
    *   Review logs: Examine the detailed logs and output from Ansible to pinpoint where the error occurs.
    *   Task isolation: Comment out parts of the playbook and run it incrementally to isolate the task causing the issue.
    *   Module debugging: Add debug tasks to print variables and outputs at various points in our playbook.

        - name: Display the variable my_var

        ansible.builtin.debug:

        msg: "The value of my_var is {{ my_var }}"

5.  Specific error resolution:
    *   Authentication failures:
        *   Ensure SSH keys are correctly configured.
        *   Check user permissions on the remote nodes.
    *   Module specific errors:
        *   Verify that the modules being used are compatible with the target nodes.
        *   Check module documentation for required parameters and usage examples.
    *   Timeouts:
        *   Increase the timeout values for SSH connections if the nodes are slow to respond.

            ansible_ssh_common_args: '-o ConnectionTimeout=60'

By following these steps and techniques, we should be able to diagnose and resolve most issues encountered while using Ansible. If we need specific help with errors, we can provide the error message or describe the issue in more detail.

[Ansible role](#contents.xhtml_sc3_364a)

Molecule is a powerful tool designed to aid in the development and testing of Ansible roles. It allows us to test our roles in various scenarios and environments to ensure they function correctly as follows:

*   Installing Molecule:

    pip3 install molecule

*   Creating a new role with Molecule:

    molecule init role myrole

*   Basic Molecule commands:

    *   Initialize a scenario:

        molecule init scenario -r myrole -d docker

    *   Run tests:

        molecule test

    *   List available scenarios:

        molecule list

    Following is an example of a Molecule configuration (molecule or default or molecule.yml):

    ---

    dependency:

    name: galaxy

    driver:

    name: docker

    platforms:

    - name: instance

    image: quay.io/centos/centos:stream9

    command: /sbin/init

    privileged: true

    provisioner:

    name: ansible

    lint:

    name: ansible-lint

    scenario:

    name: default

    verifier:

    name: testinfra

*   Running Molecule tests:
    *   To start the testing process, run the following:

        molecule test

[Ansible collection](#contents.xhtml_sc3_365a)

Ansible test is another essential tool for testing collections. It allows us to run various tests including sanity, unit, and integration tests as follows:

*   Sanity testing:

    ansible-test sanity --docker

*   Unit testing:

    ansible-test units --python 3.8

*   Integration testing:

    ansible-test integration --docker --python 3.8

[Best practices for role and collection testing](#contents.xhtml_sc2_366a)

To ensure effective and reliable testing of Ansible roles and playbooks, follow these best practices:

*   Isolate each role: Ensure that each role can be tested independently. This means defining clear and minimal dependencies for each role.
*   Use virtual machines or containers: Use tools like Vagrant or Docker to create isolated environments for testing roles and collections.
*   Mock external dependencies: Where possible, mock external dependencies to avoid flakiness in tests due to network or external service issues.
*   Linting and syntax checking: Always lint our playbooks and roles to catch syntax errors and best practice violations early.

    ansible-lint <playbook.yml>

    ansible-playbook --syntax-check <playbook.yml>

By following these practices and utilizing tools like molecule and ansible-test, we can ensure our Ansible roles and collections are robust, reliable, and ready for production deployment.

[Conclusion](#contents.xhtml_sc2_367a)

Optimizing system performance and troubleshooting issues is a critical skill for Linux system administrators. This chapter covered key concepts and procedures related to the Linux boot process, password management, file system maintenance, log analysis, network troubleshooting and process control.

Mastering these areas allows administrators to ensure systems boot properly, recover from issues like lost root passwords or corrupted file systems, analyze log files to diagnose problems, optimize network performance and manage processes effectively. Having a systematic approach to investigating issues by checking logs, network connectivity, process states and applying solutions methodically is invaluable.

While the specifics may vary across Linux distributions, the core principles of topics like the boot sequence, system logging, and process management remain consistent. Continuous learning and hands-on practice are crucial for developing true expertise in Linux systems administration and troubleshooting. The next chapter, [Chapter 9](#ch09.xhtml),  Practice Exams and Scenarios, will focus on preparing for the RHCE exam using Ansible for system administration. It includes exam preparation strategies, practice exams in the RHCE format, detailed solutions, and automation of tasks like managing software packages, services, file systems, users, and more.

[Points to remember](#contents.xhtml_sc2_368a)

*   The Linux boot process involves the firmware, bootloader, kernel, initramfs and finally the systemd initialization.
*   The rd.break kernel option allows dropping to a root shell during initramfs to reset passwords.
*   Check /etc/fstab and use fsck to address file system mounting failures.
*   Understand and analyze logs from journalctl, rsyslog, and log files.
*   Use standard network tools like ping, traceroute, ss, etc. systematically to pinpoint networking issues.
*   Monitor process states and send appropriate signals for process management.
*   Schedule routine tasks using cron jobs for automation.

[Multiple choice questions](#contents.xhtml_sc2_369a)

1.  What is the first stage of the Linux boot process?
    1.  The kernel loads
    2.  The boot loader startsc
    3.  The firmware finds the boot media
    4.  systemd initializes
2.  What command can we use to reset the root password if we have forgotten it?
    1.  passwd
    2.  passwd root)
    3.  rd.break
    4.  chroot
3.  Which file contains the rules for how rsyslog processes log messages?
    1.  /etc/rsyslog.conf
    2.  /etc/syslog.conf
    3.  /etc/systemd/journald.conf
    4.  /etc/logrotate.conf
4.  What command can we use to view logs being written to the systemd journal in real-time?
    1.  tail -f /var/log/messages
    2.  journalctl -f
    3.  rsyslogd -f
    4.  logrotate -f

[Answers](#contents.xhtml_sc3_370a)

1 c.

2 c.

3 a.

4 b.

[Questions](#contents.xhtml_sc2_371a)

1.  What are the key steps involved in the Linux system bootstrap process as described in the chapter?
2.  Describe the procedure to reset a root password in RHEL when it is forgotten.
3.  Explain how systemd targets are utilized in configuring the system boot process. What is the significance of targets like graphical.target and multi-user.target?
4.  How can the VDO be used to improve storage efficiency in RHEL environments? Include details on configuration and monitoring.
5.  What are common file system issues that can prevent a Linux system from booting, and how can these be diagnosed and resolved?
6.  Discuss the role and configuration of systemd-journald and rsyslog in managing system logs in RHEL.
7.  Outline the steps to troubleshoot an Apache web server failure, using systemctl and journalctl commands.
8.  Detail the network troubleshooting steps using commands such as ip, ping, and traceroute. How do these tools assist in diagnosing network issues?
9.  What are the critical process states in Linux and their implications for system performance and troubleshooting?
10.  How does one manage and troubleshoot cron jobs within a Linux system? Provide examples of common cron job configurations.

[Key terms](#contents.xhtml_sc2_372a)

*   BIOS: Basic input or output system is firmware embedded on a computer's motherboard that initializes hardware components during the boot process and provides a basic interface for configuring system settings.
*   POST: Power-on self-test is a diagnostic process performed by a computer's firmware BIOS during startup to verify and initialize essential hardware components, ensuring the system's operational readiness.
*   Bootstrap: The initial set of operations that a computer system performs when power is turned on, which loads the operating system.
*   Systemd: A system and service manager for Linux operating systems, responsible for initializing the system and managing system processes after booting.
*   Root password reset: A critical recovery operation that allows administrative access to be regained if the password is lost.
*   VDO: Virtual Data Optimizer is a technology in RHEL that reduces data storage costs by deduplicating and compressing data.
*   File system troubleshooting: Techniques used to diagnose and repair issues that prevent the Linux file system from mounting or functioning correctly.
*   Systemd-journald: A service within systemd that collects and manages journal logs from system processes.
*   Rsyslog: An enhanced syslog daemon in Linux that provides advanced log processing features.
*   Network troubleshooting tools: Utilities such as IP, ping, traceroute and ss used to diagnose network connectivity and performance issues.
*   Cron Jobs: Tasks scheduled to run at specific times or intervals on Unix-like systems, crucial for routine system maintenance and task automation.
*   System logs: Files that record operations within an operating system or software application, essential for troubleshooting and security monitoring.

# [CHAPTER 9Practice Exams and Scenarios](#contents.xhtml_ch09a)

[Introduction](#contents.xhtml_sc2_373a)

[Chapter 9](#ch09.xhtml), Practice Exams and Scenarios, is dedicated to guiding aspirants through the complexities of the RHCE  exam with a particular focus on leveraging Ansible for system administration tasks. This chapter is intricately designed to serve as both a theoretical and practical guide enhancing the understanding and application of Ansible in real-world scenarios. The content within offers a deep dive into automating standard RHCSA tasks, thereby equipping readers with the skills necessary to excel in the RHCE exam.

[Structure](#contents.xhtml_sc2_374a)

The chapter covers the following topics:

*   Exam preparation
*   Time management techniques
*   Recommended resources
*   Setup
*   Modules
*   Template

[Objectives](#contents.xhtml_sc2_375a)

By the end of this chapter, candidates will be comprehensively prepared for the RHCE certification by providing detailed insights into using Ansible effectively. It focuses on enhancing practical skills through practice exams and detailed solutions, deepening understanding of essential Ansible modules for automating a variety of tasks, and fostering efficient exam preparation with strategic learning advice and resource recommendations. Additionally, the chapter encourages a structured learning approach, enabling candidates to benefit from both self-paced and instructor-led training to optimize their readiness for the exam.

[Exam preparation](#contents.xhtml_sc2_376a)

Achieving a RHCE certification is a significant milestone for IT professionals aiming to excel in using RHEL systems. This article provides a comprehensive guide on how to prepare for the RHCE exam, ensuring candidates are well-equipped to tackle the challenges presented by this advanced-level certification.

[Overview of RHCE exam](#contents.xhtml_sc2_377a)

The RHCE exam (EX294) is a performance-based evaluation of RHEL system administration skills focusing on automation and scripting using Ansible. As a prerequisite, candidates should have the skills of a RHCSA, which includes managing security and users and understanding essential tools and system operations.

Following are the key areas of focus:

*   Understand and use essential tools: Familiarize with basic shell scripting, command-line tools and text file editing.
*   System management and configuration: Learn how to configure local storage, manage system services and create file systems.
*   Security management: Understand user and group management and security-related configurations like firewall settings and SSH key distribution.
*   Mastering Ansible: Dive deep into Ansible for automation, covering playbooks, roles, inventories and variables. Focus on practical usage and the ability to convert scripts into Ansible playbooks.
*   Automation practices: Utilize Ansible to automate common system administration tasks across multiple systems, enhancing configuration efficiency and consistency.

[Preparation strategies](#contents.xhtml_sc3_378a)

To facilitate a thorough understanding and effective preparation for the RHCE exam, consider the following strategies:

*   Structured learning: Consider enrolling in official Red Hat training courses that provide in-depth knowledge and hands-on practice. If in-person training suits our style, look for local learning facilities offering on-site training. Remote learning options are also widely available for those who prefer to study at their own pace.
*   Practice through labs: Engage in practical exercises and labs to reinforce our learning. Setting up a home lab environment can be an invaluable practice tool to simulate real-world scenarios.
*   Join learning communities: Participate in forums and discussion groups, such as the Red Hat Learning Community. This allows us to connect with peers, share knowledge and find out what others are saying about their exam preparation and experiences.
*   Review documentation and resources: Make use of Red Hat's comprehensive documentation and guides to understand the finer details of the systems and software we will be working with. Keep handy the official documentation to look up specific Ansible modules and commands.
*   Mock exams: Taking practice exams can help gauge our preparation level and identify areas where more focus is needed. It also helps us familiarize ourselves with the format and time constraints of the actual exam.
*   Hands-on practice: The RHCE exam is performance-based, emphasizing practical skills over theoretical knowledge. Set up a home lab environment using virtualization tools like VirtualBox or VMwar e to practice tasks covered in the exam objectives.
*   Real-world scenarios: Create and practice real-world scenarios using Ansible and other relevant tools. This not only reinforces our knowledge but also enhances our problem-solving skills.
*   Official Red Hat courses: Enroll in official Red Hat courses, such as RH294, which are specifically designed to prepare candidates for the RHCE exam. These courses provide structured learning and access to experienced instructors.

[Time management techniques](#contents.xhtml_sc2_379a)

Effective time management is crucial during both the preparation phase and the actual exam. The total time allowed for the RHCE EX294 exam is 240 minutes or four hours. Following are some techniques to manage our time efficiently:

*   Set specific goals: Break down our study plan into specific, achievable goals. This helps maintain focus and track progress.
*   Use timed practice sessions: Time yourself while practicing tasks to improve your speed and efficiency. This is particularly important for the performance based RHCE exam.
*   Prioritize tasks: During the exam, prioritize tasks based on their complexity and your confidence in completing them. Address easier tasks first to secure quick points and build momentum.
*   Take breaks: Avoid burnout by taking regular breaks during your study sessions. Short and frequent breaks help maintain concentration and prevent fatigue.

[Recommended resources](#contents.xhtml_sc2_380a)

Utilizing high quality resources is vital for effective preparation. Alongside this book the following resources might be useful:

*   Books:
    *   RHCSA/RHCE Red Hat Linux Certification Study Guide by Michael Jang and Alessandro Orsaria
    *   Red Hat RHCE (EX294) Cert Guide by Sander van Vugt
*   Online courses:
    *   Red Hat Learning Subscription (RHLS)
    *   O'Reilly learning platform
    *   Linux academy
*   Practice platforms:
    *   GitHub repositories with example playbooks (e.g., tmichett/RH294 and tmichett/AnsiblePlaybooks)
*   Community forums:
    *   Reddit r/redhat
    *   Stack Overflow
    *   Red Hat's official discussion forums

[Setup](#contents.xhtml_sc2_381a)

Follow these steps to set up Ansible on a RHEL system. Please consider that Ansible is included in the RHEL AppStream repository in modern systems.

[Installation](#contents.xhtml_sc3_382a)

We can install Ansible and his dependencies using the DNF package manager in RHEL:

# dnf install -y ansible

Check the installed version of Ansible to confirm the installation was successful.

$ ansible --version

ansible [core 2.17.1]

[Inventory](#contents.xhtml_sc3_383a)

Ansible inventory is a file that lists our managed hosts and their groupings. Groups can contain individual hosts or other groups, allowing for hierarchical organization. Following is a detailed explanation, and an example based on the contents of our provided documents.

[INI format inventory](#contents.xhtml_sc4_384a)

An Ansible inventory file is typically written in INI or YAML file formats. Hosts can be organized in groups and child groups. We can also assign variables to groups or hosts directly in the inventory file. The default inventory is stored in INI format in the path /etc/ansible/hosts. In most Ansible commands. We can specify a custom inventory using the -i parameter. Following is an expanded example that includes variables:

[webservers]

web1.example.com

web2.example.com

[databases]

db1.example.com

db2.example.com

[all_servers:children]

webservers

databases

[all_servers:vars]

ansible_user=admin

ansible_port=22

[databases:vars]

db_port=5432

In this example:

*   webservers and databases are groups containing hosts.
*   all_servers is a parent group containing webservers and databases as children.
*   Variables for all_servers are specified under [all_servers:vars].
*   Variables specific to the databases group are defined under [databases:vars].

[YAML format inventory](#contents.xhtml_sc4_385a)

We can use YAML to create a more structured and readable format. Following is the same inventory in YAML format:

all:

children:

webservers:

hosts:

web1.example.com:

web2.example.com:

databases:

hosts:

db1.example.com:

db2.example.com:

vars:

db_port: 5432

vars:

ansible_user: admin

ansible_port: 22

The ansible-inventory command helps us display and validate the contents of our inventory as follows:

*   Display inventory: This command will list all hosts and groups in our inventory.

    ansible-inventory --list

*   Graph inventory: This command will display our inventory in a tree representation.

    ansible-inventory --graph

| Note: Use the additional parameter -i to specify an inventory path |

[Inventory best practices](#contents.xhtml_sc4_386a)

To effectively manage inventory in Ansible, it is important to use the following strategies to structure and manage groups and variables:

*   Hierarchical grouping: Use child groups to logically structure our inventory.
*   Variable inheritance: Define variables at the appropriate group level to ensure they are inherited by child groups and hosts.
*   Dynamic inventories: For large or dynamic environments, consider using dynamic inventories that can automatically update based on our infrastructure.

[Configuration](#contents.xhtml_sc3_387a)

The ansible.cfg file contains a lot of Ansible configurations. The most common changes involve changing custom roles directory and inventory path. We need to modify the configuration file to include these settings. The default configuration file is located in /etc/ansible/ansible.cfg. In most Ansible commands, we can specify a custom configuration using the -c parameter.

Suppose our inventory file is located at /home/user/ansible/inventory and our roles directory is at /home/user/ansible/roles, our ansible.cfg file would look as follows:

[defaults]

inventory = /home/user/ansible/inventory

roles_path = /home/user/ansible/roles

host_key_checking = False

retry_files_enabled = False

[Breakdown of configuration options](#contents.xhtml_sc4_388a)

Following is the breakdown of configuration options:

*   inventory: Specifies a custom path to our inventory file. This tells Ansible where to find our list of hosts and groups.
*   roles_path: Specifies a custom path to our role’s directory. This is useful if we have custom roles st ored in a specific location.
*   host_key_checking: When set to False, disables SSH key host checking, which can be useful in development environments.
*   retry_files_enabled: When set to False, disables the creation of retry files.

[Additional tips](#contents.xhtml_sc4_389a)

When configuring the ansible.cfg file to manage Ansible behavior, it is essential to follow these guidelines:

*   Ensure the paths specified are absolute paths or paths relative to the location of the ansible.cfg file.
    *   library: Defines the path to custom modules, for example:

        library = /path/to/custom/modules

    *   log_path: Specifies the location to save logs, for example:

        log_path = /path/to/ansible.log

*   We can include other configuration options in the ansible.cfg file as needed to suit our environment and preferences as follows:
    *   timeout: Adjusts the SSH timeout for connecting to hosts, for example:

        timeout = 30

    *   forks: Sets the number of parallel processes Ansible runs, for example:

        forks = 10

    *   remote_user: Defines the default SSH user for remote connections, for example:

        remote_user = ansible_user

[View current configuration](#contents.xhtml_sc4_390a)

The ansible-config command displays the current configuration, including default settings and overrides from configuration files and environment variables as follows:

ansible-config dump

This command checks our configuration file for syntax errors and displays the active configuration settings as follows:

ansible-config list

This command shows where each configuration option is set, which helps identify if settings are being overridden by another configuration file as follows:

ansible-config dump --only-changed

[Ad hoc](#contents.xhtml_sc3_391a)

To use an ad hoc command in Ansible we use the ansible command. For example, we can configure a YUM or DNF repository using the yum_repository module, part of the ansible.builtin collection. This module allows us to manage YUM repository configurations directly from the command line without needing a playbook.

Let us assume we want to configure a YUM repository with the following details:

*   Name: myrepo
*   Description: My Custom Repository
*   Base URL: [http://myrepo.example.com/centos/$releasever/os/x86_64/](http://myrepo.example.com/centos/$releasever/os/x86_64/)
*   GPG key URL: [http://myrepo.example.com/RPM-GPG-KEY-RHEL-9](http://myrepo.example.com/RPM-GPG-KEY-RHEL-9)

Following is how we can do it using an Ansible ad hoc command for all hosts in the inventory:

ansible all -m yum_repository -a "name=myrepo description='My Custom Repository' baseurl=http://myrepo.example.com/centos/\$releasever/os/x86_64/ gpgkey=http://myrepo.example.com/RPM-GPG-KEY-RHEL-9 gpgcheck=yes enabled=yes" -i /home/ansible/inventory

Following is a breakdown of the command:

*   ansible all: Run the command on all hosts in the inventory. We can replace all with a specific host group if needed.
*   -m yum_repository: Use the yum_repository Ansible module.
*   -a: Pass the module arguments.
    *   name=myrepo: The name of the repository.
    *   description=my custom repository: A description for the repository.
    *   baseurl=http://myrepo.example.com/centos/\$releasever/os/x86_64/: The base URL for the repository.

        | Note the escape character \ before $ to prevent shell expansion. |

    *   gpgkey=http://myrepo.example.com/RPM-GPG-KEY-RHEL-9: URL of the GPG key for the repository.
    *   gpgcheck=yes: Enable GPG key verification.
    *   enabled=yes: Enable the repository.
    *   -i /home/ansible/inventory: Specify the path to our inventory file.

[Play](#contents.xhtml_sc3_392a)

We can set up different host group tasks in the same Ansible playbook, defining multiple plays within a single playbook. Each play can target different host groups and perform different tasks.

Following is an example which we will create a playbook that:

*   Installs httpd on a group of web servers.
*   Upgrades all packages on a group of database servers.

Following is how we can create a playbook that accomplishes these tasks:

File:  multi_group_playbook.yml

---

- name: Install httpd on web servers

hosts: webservers

become: true

tasks:

- name: Install httpd

ansible.builtin.yum:

name: httpd

state: present

- name: Upgrade all packages on database servers

hosts: databases

become: true

tasks:

- name: Upgrade all packages

ansible.builtin.yum:

name: '*'

state: latest

Following is the explanation of play:

*   The playbook consists of two plays.
*   Each play has a name for easier identification.
*   The hosts directive specifies the target host group for each play.
*   The  become: true directive ensures that tasks are executed with elevated privileges (sudo).

To ensure that the Ansible playbook is executed successfully and the desired tasks are completed, follow these steps for running the playbook and verifying the outcomes:

1.  Run the playbook: Execute the playbook using the ansible-playbook command as follows:

    ansible-playbook -i /home/ansible/inventory multi_group_playbook.yml

2.  Check HTTPD installation: After running the playbook, verify that httpd is installed and running on the web servers as follows:

    ansible webservers -m shell -a "systemctl status httpd" -i /home/ansible/inventory

3.  Check package upgrade: Verify that all packages are upgraded on the database servers as follows:

    ansible databases -m shell -a "yum check-update" -i /home/ansible/inventory

This playbook allows us to manage multiple tasks across different host groups in a single playbook. We can extend this approach to include more groups and tasks as needed, making it a flexible and powerful way to manage our infrastructure with Ansible.

[Modules](#contents.xhtml_sc2_393a)

The examples provided in this section illustrate how to use the yum, yum_repository, rpm_key, service, firewalld, and file modules in Ansible to automate tasks like installing or removing packages, managing repositories and GPG keys, controlling services, configuring firewall rules, and ensuring the presence of files and directories.

[Software packages and repositories](#contents.xhtml_sc3_394a)

This Ansible playbook ensures that the latest version of the httpd package is installed on all managed hosts by using the yum module with elevated privileges  as follows:

- name: Ensure a package is installed

hosts: all

become: true

tasks:

- name: Install the latest version of a package

ansible.builtin.yum:

name: httpd

state: latest

This Ansible playbook removes the httpd package from all managed hosts using the yum module with elevated privileges as follows:

- name: Ensure a package is removed

hosts: all

become: true

tasks:

- name: Remove a package

ansible.builtin.yum:

name: httpd

state: absent

These examples show how to manage software packages and repositories using Ansible, providing us with the tools to automate the installation, removal and updating of packages as well as the management of software repositories and GPG keys on our RHEL systems.

This Ansible playbook ensures that a YUM repository named example-repo is added to all managed hosts, configuring its URL, description, GPG key and enabling it using the yum_repository module with elevated privileges as follows:

- name: Ensure a repository is added

hosts: all

become: yes

tasks:

- name: Add a YUM repository

ansible.builtin.yum_repository:

name: example-repo

description: "Example Repository"

baseurl: http://repo.example.com/yum/

enabled: yes

gpgcheck: yes

gpgkey: http://repo.example.com/RPM-GPG-KEY-example

This Ansible playbook ensures that a YUM repository named example-repo is removed from all managed hosts using the yum_repository module with elevated privileges as follows:

- name: Ensure a repository is removed

hosts: all

become: true

tasks:

- name: Remove a YUM repository

ansible.builtin.yum_repository:

name: example-repo

state: absent

This Ansible playbook ensures that the YUM repository named example-repo is disabled on all managed hosts using the yum_repository module with elevated privileges as follows:

- name: Ensure a repository is disabled

hosts: all

become: yes

tasks:

- name: Disable a YUM repository

ansible.builtin.yum_repository:

name: example-repo

enabled: no

This Ansible playbook ensures that a GPG key from http://repo.example.com/RPM-GPG-KEY, example is added to all managed hosts for verifying packages from a repository using the rpm_key module with elevated privileges as follows:

- name: Ensure a GPG key is added for repository

hosts: all

become: yes

tasks:

- name: Add a GPG key

ansible.builtin.rpm_key:

state: present

key: http://repo.example.com/RPM-GPG-KEY-example

This Ansible playbook removes a GPG key from http://repo.example.com/RPM-GPG-KEY-examp from all managed hosts using the rpm_key module with elevated privileges as follows:

- name: Ensure a GPG key is removed

hosts: all

become: true

tasks:

- name: Remove a GPG key

ansible.builtin.rpm_key:

state: absent

key: http://repo.example.com/RPM-GPG-KEY-example

[Services](#contents.xhtml_sc3_395a)

This Ansible playbook ensures that the httpd service is running and enabled to start on boot on all managed hosts using the service module with elevated privileges as follows:

- name: Ensure a service is running and enabled

hosts: all

become: true

tasks:

- name: Start and enable the httpd service

ansible.builtin.service:

name: httpd

state: started

enabled: yes

[Firewall rules](#contents.xhtml_sc3_396a)

This Ansible playbook configures firewall rules on all managed hosts to permanently open the HTTP port (port 80) and reloads the firewalld service to apply the changes, using the firewalld and service modules with elevated privileges as follows:

- name: Configure firewall rules

hosts: all

become: yes

tasks:

- name: Open HTTP port in the firewall

ansible.builtin.firewalld:

port: 80/tcp

permanent: yes

state: enabled

- name: Reload firewalld to apply changes

ansible.builtin.service:

name: firewalld

state: reloaded

[File systems](#contents.xhtml_sc3_397a)

This Ansible playbook ensures that a directory named /opt/mydirectory exists on all managed hosts, setting its permissions to 0755, using the file module with elevated privileges as follows:

- name: Ensure a directory exists

hosts: all

become: true

tasks:

- name: Create a directory

ansible.builtin.file:

path: /opt/mydirectory

state: directory

mode: '0755'

This Ansible playbook copies a file from /local/file on the control machine to /remote/file on all managed hosts, setting its permissions to 0644, using the copy module with elevated privileges as follows:

- name: Copy a file to remote machines

hosts: all

become: true

tasks:

- name: Copy the file

ansible.builtin.copy:

src: /local/file

dest: /remote/file

mode: '0644'

This Ansible task ensures that the directory /srv/test exists, sets its group ownership to test, and applies the permissions 2755 to set the GID bit, using the file module as follows:

- name: Ensure the directory exists and set GID

ansible.builtin.file:

path: /srv/test

state: directory

group: test

mode: '2755'

[Storage](#contents.xhtml_sc3_398a)

This Ansible playbook ensures that a filesystem is mounted on all managed hosts by first creating a mount point at /mnt/data and then mounting the file system from the device /dev/sdb1 with the .xfs file system type, using the file and mount modules with elevated privileges as follows:

- name: Ensure a filesystem is mounted

hosts: all

become: true

tasks:

- name: Create mount point

ansible.builtin.file:

path: /mnt/data

state: directory

- name: Mount the filesystem

ansible.builtin.mount:

path: /mnt/data

src: /dev/sdb1

fstype: xfs

opts: defaults

st ate: mounted

[Logical Volume Manager](#contents.xhtml_sc3_399a)

To create a logical volume with the Logical Volume Manager (LVM) with a Fourth Extended Filesystem (ext4), a journaling file system commonly used in Linux file system and include error handling for scenarios such as insufficient space and non-existent volume groups using Ansible, we can use the following playbook:

---

- name: Create logical volume with error handling

hosts: localhost

vars:

required_space_mb: 500

tasks:

- name: Check if volume group exists

ansible.builtin.command: vgdisplay vgname

register: vg_check

ignore_errors: yes

- name: Fail if volume group does not exist

ansible.builtin.fail:

msg: "Volume group vgname does not exist."

when: vg_check.rc != 0

- name: Check available space in the volume group

ansible.builtin.command: vgdisplay -C --units m -o vg_free vgname --noheadings --nosuffix

register: vg_free_space

- name: Parse available space

ansible.builtin.set_fact:

available_space: "{{ vg_free_space.stdout | trim | float }}"

- name: Fail if not enough space is available

ansible.builtin.ail:

msg: "Not enough space in volume group vgname."

when: available_space < required_space_mb

- name: Create a logical volume

community.general.lvol:

vg: vgname

lv: lvname

size: "{{ required_space_mb }}"

when: vg_check.rc == 0 and available_space >= required_space_mb

- name: Create ext4 filesystem on logical volume

community.general.filesystem:

fstype: ext4

dev: "/dev/vgname/lvname"

Following is the explanation of LVM:

*   Check if volume group exists:
    *   Uses the command module to run vgdisplay to check if the volume group exists.
    *   Registers the result to vg_check.
    *   Continues on error using ignore_errors: yes.
*   Fail if volume group does not exist:
    *   Uses the fail module to abort the playbook if the volume group does not exist, based on the result from the previous step.
*   Check available space:
    *   Runs vgdisplay to get the available space in the volume group.
    *   Parses the output to get the available space in megabytes.
*   Fail if not enough space:
    *   Uses the failed module to abort the playbook if there is not enough space in the volume group.
*   Create logical volume:
    *   Uses the lvol module to create the logical volume if the volume group exists and there is enough space.
*   Create filesystem:
    *   Uses the filesystem module to create an ext4 filesystem on the new logical volume.

Ensure to customize the correspondent device for vgname, lvname, and set up the required_space_mb variable according to our environment.

[File content](#contents.xhtml_sc3_400a)

This Ansible playbook ensures that the file /etc/motd is created with specific content, sets the owner and group to root and applies the permissions 0644 using the copy module with elevated privileges as follows:

- name: Ensure file content

hosts: all

become: true

tasks:

- name: Create a file with specific content

ansible.builtin.copy:

dest: /etc/motd

content: |

Welcome to the server!

Unauthorized access is prohibited.

owner: root

group: root

mode: '0644'

This Ansible playbook appends the line net.ipv4.ip_forward = 1 to the file /etc/sysctl.conf, creating the file if it does not exist, using the lineinfile module with elevated privileges as follows:

- name: Append a line to a file

hosts: all

become: true

tasks:

- name: Append text to the file

ansible.builtin.lineinfile:

path: /etc/sysctl.conf

line: "net.ipv4.ip_forward = 1"

create: yes

[Archiving](#contents.xhtml_sc3_401a)

This Ansible playbook creates a gzipped tar archive of the /var/log directory, saving it as /root/log_archive.tar.gz, using the archive module with elevated privileges as follows:

- name: Create a tar archive of a directory

hosts: all

become: yes

tasks:

- name: Archive the /var/log directory

ansible.builtin.archive:

path: /var/log

dest: /root/log_archive.tar.gz

format: gz

This Ansible playbook extracts the tar archive /root/log_archive.tar.gz to the /opt directory on all managed hosts, using the unarchive module with elevated privileges as follows:

- name: Extract a tar archive

hosts: all

become: true

tasks:

- name: Extract archive to /opt

ansible.builtin.unarchive:

src: /root/log_archive.tar.gz

dest: /opt

remote_src: yes

[Task scheduling](#contents.xhtml_sc3_402a)

This Ansible playbook schedules a cron job named Daily backup to run the script /usr/local/bin/backup.sh every day at 2:00 AM on all managed hosts, using the cron module with elevated privileges as follows:

- name: Schedule a cron job

hosts: all

become: true

tasks:

- name: Ensure a cron job runs a script daily

ansible.builtin.cron:

name: "Daily backup"

minute: "0"

hour: "2"

job: "/usr/local/bin/backup.sh"

This Ansible playbook removes a specific cron job named Daily backup from all managed hosts, using the cron module with elevated privileges as follows:

- name: Remove a cron job

hosts: all

become: true

tasks:

- name: Ensure a specific cron job is absent

ansible.builtin.cron:

name: "Daily backup"

state: absent

[Users and groups](#contents.xhtml_sc3_403a)

This Ansible playbook ensures that a user named johndoe with UID 1001, a comment of John Doe, and the default shell set to /bin/bash exists on all managed hosts, using the user module with elevated privileges as follows:

- name: Ensure a user exists

hosts: all

become: yes

tasks:

- name: Create a new user

ansible.builtin.user:

name: johndoe

uid: 1001

comment: "John Doe"

shell: /bin/bash

state: present

This Ansible playbook ensures that a group named admin with GID 1001 exists on all managed hosts, using the group module with elevated privileges as follows:

- name: Ensure a group exists

hosts: all

become: yes

tasks:

- name: Create a new group

ansible.builtin.group:

name: admin

gid: 1001

state: present

[Template](#contents.xhtml_sc2_404a)

Templates are very powerful in file configuration, especially when multiple parameters are specified. The following example combines Ansible’s unique features like magic variables, to simplify some typical system administrator tasks.

[Message of the day](#contents.xhtml_sc3_405a)

Message of the day (MOTD) file welcomes every user when connecting via terminal or via SSH. Let us create a customizer /etc/motd file for each host group in Ansible.

Create a Jinja2 template that will be used to generate the MOTD files as follows:

File: templates/motd.j2

Welcome to {{ inventory_hostname }}

Host Group: {{ group_names[0] }}

IP Address: {{ ansible_default_ipv4.address }}

This is an automatically generated message of the day:

Welcome to webserver1

Host Group: web

IP Address: 192.168.1.10

A Jinja2 template that includes placeholders for the hostname, host group and IP address. This template will be used to generate the /etc/motd file content.

[Playbook](#contents.xhtml_sc3_406a)

Create a playbook that uses the template to generate an MOTD file for each host as follows:

File: create_motd_files.yml

---

- name: Create MOTD files for each host group

hosts: all

become: true

gather_facts: true

tasks:

- name: Create MOTD file for each host

template:

src: templates/motd.j2

dest: /etc/motd

owner: root

group: root

mode: '0644'

The playbook runs on all hosts and gathers facts. It uses the template module to create the /etc/motd file on each host. The file is created from the motd.j2 template and has appropriate ownership and permissions.

Run the playbook using the ansible-playbook command:

ansible-playbook -i /home/ansible/inventory create_motd_files.yml

After running the playbook, we can verify that the MOTD file has been created on each host by checking the contents of /etc/motd or connecting via console or SSH.

[Apache](#contents.xhtml_sc3_407a)

In this example, we would like to create a webserver-customized index file using a Jinja2 template that references Ansible facts to insert the hostname and IP address of all the inventory using the magic variable hostvars as follows:

1.  Create a simple template for a web page showing a report of all the hostnames and IP addresses associated.

    File:  templates/index.html.j2

    <!DOCTYPE html>

    <html>

    <head>

    <title>Host Information</title>

    </head>

    <body>

    <h1>Host Information</h1>

    <table border="1">

    <tr>

    <th>Hostname</th>

    <th>IP Address</th>

    </tr>

    {% for host in groups['all'] %}

    <tr>

    <td>{{ hostvars[host]['ansible_hostname'] }}</td>

    <td>{{ hostvars[host]['ansible_default_ipv4']['address'] }}</td>

    </tr>

    {% endfor %}

    </table>

    </body>

    </html>

    This is the Jinja2 template that generates an HTML file listing the hostname and IP address of each host. It loops over all hosts in the inventory (groups['all']) and uses hostvars to access the hostname and IP address.

2.  Create the playbook:

    Next, create a playbook using this template to generate the index file on our target hosts as follows:

    File: hostinformation.yml

    ---

    - name: Generate index file with host information

    hosts: webservers

    become: yes

    tasks:

    - name: Gather host facts

    ansible.builtin.setup:

    gather_subset: 'min'

    - name: Create index file from template

    ansible.builtin.template:

    src: templates/index.html.j2

    dest: /var/www/html/index.html

    notify:

    - Restart Apache

    handlers:

    - name: Restart Apache

    ansible.builtin.service:

    name: httpd

    state: restarted

The playbook targets the webservers group. The template module generates the /var/www/html/index.html file on each web server using the index.html.j2 template. The handler restarts Apache after the index file is created.

[Role](#contents.xhtml_sc3_408a)

The content you have provided from the image appears to be related to using prebuilt roles in Ansible and managing them through Ansible Galaxy as follows:

*   To download and use a prebuilt role in Ansible, use the following:
    *   Search for a role on Ansible Galaxy: Visit Ansible Galaxy and search for a role that fits our requirements. For example, if we need a role to manage Network Time Protocol (NTP), we can search for apache and find a suitable role.
    *   Install the role using Ansible Galaxy command: Once we have identified the role, we can use the Ansible Galaxy command to install it. For instance, to install the geerlingguy.apache role, we would run the following command

        ansible-galaxy install geerlingguy.apache

        This command installs the role into the system wide roles directory or a specified path if provided with the -p flag.

*   Use the role: After installing the role, we can include it in our playbook. Following is an example of how to use the geerlingguy.apache role in a playbook:

    - name: Use role

    hosts: webservers

    roles:

    - geerlingguy.apache

    This playbook applies the geerlingguy.apache role to webservers hosts in the inventory.

*   Using requirements.yml for multiple roles: If we have multiple roles to install, we can create a requirements.yml file and use it to manage role installations.

    Following is an example requirements.yml file:

    ---

    roles:

    - name: geerlingguy.apache

    - name: geerlingguy.mysql

    - name: geerlingguy.php

    Then, install all roles listed in the requirements.yml file with the following command:

    ansible-galaxy install -r requirements.yml

    This approach is useful for managing dependencies and ensuring consistent environments across different setups.

[Custom role](#contents.xhtml_sc3_409a)

Creating an Ansible role for Apache with a custom directory, set GID, symlink and SELinux configuration to handle a new website as follows:

*   Directory structure: Run the ansible-galaxy init command to create the directory structure for the Apache role.

    ansible-galaxy init apache

    This command will create the following directory structure:

    roles/

    ├── apache/

    │ ├── defaults/

    │ │ └── main.yml

    │ ├── tasks/

    │ │ └── main.yml

    │ ├── handlers/

    │ │ └── main.yml

    │ ├── files/

    │ ├── templates/

    │ └── vars/

    │ └── main.yml

*   Define default variables: Edit the defaults/main.yml file to set default variables as follows:

    ---

    custom_directory: /var/www/custom

    symlink_directory: /var/www/html

*   Define tasks: Edit the tasks/main.yml file to include tasks for installing Apache, creating the custom directory with set GID, creating the symlink and setting the SELinux context as follows:

    ---

    - name: Install Apache

    ansible.builtin.yum:

    name: httpd

    state: present

    notify: Restart Apache

    - name: Create custom directory

    ansible.builtin.file:

    path: "{{ custom_directory }}"

    state: directory

    mode: '2775'

    owner: apache

    group: apache

    setype: " httpd_sys_content_t"

    selevel: s0

    serole: object_r

    seuser: system_u

    - name: Create symlink to custom directory

    ansible.builtin.file:

    src: "{{ custom_directory }}"

    dest: "{{ symlink_directory }}"

    state: link

    - name: Restore SELinux context

    ansible.builtin.command: "restorecon -Rv {{ custom_directory }}"

    become: true

*   Create a custom directory: This task creates the custom directory with the specified permissions and ownership. It also sets the SELinux context for the custom directory to system_u:object_r:httpd_sys_content_t:s0 using the native file parameters as follows:

    seuser: system_u

    serole: object_r

    setype: httpd_sys_content_t

    selevel: s0

*   Create symlink to custom directory: This task creates a symlink from the custom directory to the specified symlink location.
*   Restore SELinux context: This task restores the SELinux context for the custom directory to ensure that the settings take effect.
*   Define handlers: Edit the handlers/main.yml file to define the handler for restarting Apache as follows:

    ---

    - name: Restart Apache

    ansible.builtin.service:

    name: httpd

    state: restarted

*   Create playbook: Create a playbook to use this role. For example, site.yml as follows:

    ---

    - hosts: webservers

    roles:

    - apache

*   Run the playbook: Finally, run the playbook to apply the role as follows:

    ansible-playbook site.yml

    This setup will ensure that Apache is installed, the custom directory is created with the correct permissions, the SELinux context is used, a symlink is created to the custom directory, and Apache is restarted to apply the changes.

*   Playbook for role testing: Following is a playbook used to test a role:

    ---

    - name: Test myrole

    hosts: all

    become: true

    roles:

    - role: myrole

    vars:

    some_variable: some_value

    tasks:

    - name: Verify installation

    command: some_command

    register: result

    - name: Ensure the result is successful

    assert:

    that:

    - result.rc == 0

[Vault](#contents.xhtml_sc3_410a)

Ansible vault is a feature that allows you to keep sensitive data such as passwords or keys secure within Ansible files. It provides encryption and password protection to prevent unauthorized access.

Following are the steps to create a new encrypted file and how to change (rekey) the password for an encrypted file:

*   Creation:  To create a new encrypted file using Ansible vault, use the ansible-vault  create command followed by the filename. This command will prompt us to enter and confirm a password, then open the file in our default editor as follows:

    $ ansible-vault create secret.yml

    New Vault password: ********

    Confirm New Vault password: ********

    If we prefer to use a password file, we can specify it with the --vault-password-file option as follows:

    $ ansible-vault create --vault-password-file=password.txt secret.yml

*   Change password: Rekeying an Ansible vault file changes the password used for encryption. This is useful if we suspect the password has been compromised or we want to rotate the password for compliance.

    To rekey a vault, use the ansible-vault rekey command as follows:

    $ ansible-vault rekey secret.yml

    New Vault password: ********

    Confirm New Vault password: ********

    If we use a password file, we can rekey using the following:

    $ ansible-vault rekey --vault-password-file=old-password.txt secret.yml

[Using vault in a playbook](#contents.xhtml_sc4_411a)

When using a vault encrypted file in an Ansible playbook, we need to specify the vault password so Ansible can decrypt the file at runtime.

Following are the steps to include an encrypted file and run a playbook with a vault password:

1.  Include encrypted variables in playbook:

    In our playbook, refer the encrypted file in the vars_files section:

    ---

    - name: Secure Playbook

    hosts: all

    vars_files:

    - secret.yml

    tasks:

    - name: Ensure sensitive data is protected

    debug:

    msg: "{{ sensitive_data }}"

2.  Run the playbook with vault password:

    To run the playbook, provide the vault password interactively or through a password file.

    *   Interactively as follows:

        $ ansible-playbook --vault-id @prompt playbook.yml

    *   Using a password file as follows:

        $ ansible-playbook --vault-password-file=vault-password.txt playbook.yml

        Always use a strong password for our vault. Store our password files securely and avoid checking them into version control. Consider using environment variables or scripts to manage passwords securely.

[Security](#contents.xhtml_sc3_412a)

This Ansible playbook ensures SELinux is in enforcing mode by setting it with the “setenforce 1” command and updating the SELinux configuration file to set SELINUX=enforcing, using the command and replace modules with elevated privileges as follows:

- name: Ensure SELinux is in enforcing mode

hosts: all

become: yes

tasks:

- name: Set SELinux to enforcing

ansible.builtin.command:

cmd: setenforce 1

when: ansible_selinux.status == 'enabled'

- name: Ensure SELinux is set to enforcing in config file

ansible.builtin.replace:

path: /etc/selinux/config

regexp: '^SELINUX=.*'

replace: 'SELINUX=enforcing'

[Securely transfer files](#contents.xhtml_sc4_413a)

Transferring files securely between systems is a fundamental task for system administrators and developers. Ensuring the integrity and confidentiality of the data during transit is paramount. The most widely used methods for secure file transfers in Linux are Secure Copy Protocol (SCP) and Secure File Transfer Protocol (SFTP).

SCP is a command line tool that uses SSH to securely transfer files between hosts. It provides encryption and authentication to ensure that the data remains protected during transit. SFTP is an extension of the SSH protocol that provides secure file transfer capabilities. Unlike SCP, SFTP offers more robust features, including file access, file management and directory operations. As of April 13, 2022, one of the most important security changes for OpenSSH in RHEL is the deprecation of the SCP protocol.

Following are the key changes implemented:

*   Default to SFTP: The SCP command line tool uses the SFTP protocol for file transfers by default.
*   Restoring SCP protocol: Usage of the SCP protocol can be restored using the newly added -O option.
*   Disabling SCP protocol: The SCP protocol can be completely disabled on the system. If the file /etc/ssh/disable_scp exists, any attempt to use the SCP protocol will fail.

These changes stem from the fact that SCP, a decades-old protocol carries multiple security risks and issues without straightforward solutions. New issues are frequently reported (e.g., CVE-2020-15778), making it difficult to fix them all properly due to the protocol's inherent trust in authenticated sessions. As a result, some RHEL customers prefer to disable the SCP protocol entirely. SFTP, a well-defined protocol, covers most of SCP’s use cases and is a more secure alternative. Despite the deprecation, SCP can still be used with the -O option.

[Using SFTP for file transfer](#contents.xhtml_sc4_414a)

Following are the ways for using SFTP for file transfer:

*   To start an SFTP session, use the following command:

    sftp user@remote_host

*   Once connected, we can use various SFTP commands to manage files as follows:
    *   Upload a file:

        put /path/to/local/file /path/to/remote/destination

    *   Download a file:

        get /path/to/remote/file /path/to/local/destination

    *   List files in a directory:

        ls /path/to/remote/directory

    *   Change remote directory:

        cd /path/to/remote/directory

    *   Create a directory on remote host:

        mkdir /path/to/remote/directory

    *   Remove a file on remote host:

        rm /path/to/remote/file

    *   Rename a file on remote host:

        rename /path/to/remote/oldfile /path/to/remote/newfile

[Best practices for secure file transfers](#contents.xhtml_sc4_415a)

Following are the best practices for secure file transfers:

*   Use strong authentication: Prefer key-based authentication over password-based to enhance security.
*   Enable Two-Factor Authentication (2FA): Add an extra layer of security to our SSH access.
*   Limit SSH access: Restrict SSH access to specific IP addresses and users.
*   Keep OpenSSH updated: Regularly update our OpenSSH package to patch vulnerabilities.
*   Monitor and log transfers: Keep logs of our file transfer activities to monitor for any suspicious actions.
*   Use rsync: Consider using rsync for file transfers as it uses its own protocol for file transfer and SSH for transport protection.

Securely transferring files between Linux systems is crucial for maintaining data integrity and confidentiality. Both SCP and SFTP provide robust, secure methods for file transfers, leveraging SSH for encryption and authentication. However, with the deprecation of SCP in RHEL 9 onward, it is advisable to transition to SFTP or other secure methods. By following the examples and best practices outlined in this article, we can ensure our file transfers are both efficient and secure.

[Failure package installation](#contents.xhtml_sc3_416a)

Suppose we have a playbook that fails to install a package as follows:

---

- name: Install Apache

hosts: webservers

tasks:

- name: Ensure Apache is installed

Ansible.builtin.dnf:

name: httpd

state: present

Following are the steps to troubleshoot:

1.  Check syntax:

    ansible-playbook --syntax-check install_apache.yml

2.  Run in check mode:

    ansible-playbook install_apache.yml –check

3.  Run with verbose output:

    ansible-playbook -vvv install_apache.yml

4.  Ping the hosts:

    ansible all -m ping -i inventory

5.  Gather facts:

    ansible all -m setup -i inventory

6.  Review logs and error messages:

    Analyze the verbose output to identify the exact error message. Check if yum is available and properly configured on the target nodes.

[Conclusion](#contents.xhtml_sc2_417a)

As we conclude [Chapter 9](#ch09.xhtml), Practice Exams and Scenarios, candidates should feel well-prepared and confident in their abilities to tackle the RHCE exam. This chapter has provided a thorough exploration of Ansible's capabilities as they pertain to system administration, ensuring that readers are not only able to perform necessary tasks but are also able to automate them efficiently. Through practice exams, detailed explanations and strategic preparation advice, this chapter serves as an indispensable resource for anyone aiming to achieve the RHCE certification. Remember, mastery of the material through diligent study and practical application is crucial to success on the exam. The next chapter focuses on the real-world application of the RHCE certification. It covers strategies for career growth, networking, staying updated with industry trends, and mapping RHCE competencies to various Linux administration and engineering roles, including system administrators, DevOps engineers, and cloud engineers.

[Points to remember](#contents.xhtml_sc2_418a)

*   Automate RHCSA tasks with Ansible: Manage software packages, services, firewall rules, file systems, storage and user accounts.
*   Prepare for the RHCE exam with practice exams, solutions and structured learning approaches.
*   Develop effective time management techniques for the exam.
*   Use Ansible playbooks, roles, inventories and variables to automate tasks.
*   Focus on shell scripting, command line tools and text file editing.
*   Configure local storage, manage services, and create file systems.
*   Manage security settings, including users, groups, firewalls and SSH keys.
*   Employ Ansible modules like ansible.builtin.yum and ansible.builtin.dnf.
*   Verify playbook syntax with ansible-playbook --syntax-check and use conditionals.
*   Understand key concepts like idempotence, YAML, ad hoc commands, and fact gathering.

[Multiple choice questions](#contents.xhtml_sc2_419a)

1.  What command can we use to check the syntax of an Ansible playbook?
    1.  ansible-playbook --check
    2.  ansible-playbook --syntax-check
    3.  ansible-playbook --validate
    4.  ansible-playbook –verify
2.  Which Ansible module is used to manage software packages using DNF on RHEL systems?
    1.  ansible.builtin.apt
    2.  ansible.builtin.package
    3.  ansible.builtin.yum
    4.  ansible.builtin.dnf
3.  What is the purpose of the ansible.builtin.lineinfile module?
    1.  To copy files from the control node to managed nodes
    2.  To ensure a specific line is present or absent in a file
    3.  To manage SELinux policies
    4.  To install software packages
4.  Which module should we use to create a new user in Ansible?
    1.  ansible.builtin.group
    2.  ansible.builtin.user
    3.  ansible.builtin.acl
    4.  ansible.builtin.sudo

[Answers](#contents.xhtml_sc3_420a)

1 b.

2 d.

3 b.

4 b.

[Questions](#contents.xhtml_sc2_421a)

1.  Explain the purpose and use of the ansible.builtin.lineinfile module in Ansible.
2.  Describe the steps we would take to verify the syntax of an Ansible playbook before execution.
3.  What are the key differences between the ansible.builtin.copy and ansible.builtin.template modules? Provide examples of when we would use each.
4.  How can we manage multiple environments (e.g., development, staging, production) in Ansible? Discuss the strategies and configurations we might use.
5.  Discuss the importance of using the ansible.builtin.yum module for package management on RHEL systems. How does it differ from using the ansible.builtin.dnf module?
6.  What are the advantages of using Ansible's ad-hoc commands for system administration tasks? Provide an example of an ad hoc command we might use.
7.  How can we use Ansible to automate the deployment of an application across multiple servers? Outline the steps and modules involved.
8.  Explain the role of the ansible.builtin.service module. How would we use it to ensure a service is always running?
9.  Describe how we would handle secrets and sensitive data in Ansible playbooks to ensure security and compliance.
10.  What are when statements in Ansible, and how do they help in writing flexible playbooks? Provide an example of a use case for a when statement.

[Key terms](#contents.xhtml_sc2_422a)

*   Ansible module: A discrete unit of code that Ansible executes. Examples include ansible.builtin.yum, ansible.builtin.copy, and ansible.builtin.service.
*   Playbook: A YAML file containing one or more plays, which define the tasks to be executed on managed nodes.
*   Inventory: A list of managed nodes that Ansible will control, typically defined in the /etc/ansible/hosts file.
*   Task: A single action to be performed on the managed nodes, such as installing a package or restarting a service.
*   Handler: A special task that is triggered by a notifier in another task, often used for actions like restarting services.
*   Role: A predefined way to organize playbooks and other files, making reusable code easier to manage and distribute.
*   Variable: A way to pass data into playbooks and templates, allowing for dynamic content and configurations.
*   Ad hoc command: A way to run individual Ansible modules on-the-fly without the need for a playbook.
*   YAML: The human-readable data serialization format used by Ansible for writing playbooks.
*   Idempotence: The property of Ansible tasks to be safely run multiple times without changing the managed system beyond the initial application.
*   Syntax check: The process of verifying the syntax of an Ansible playbook using the ansible-playbook --syntax-check command.
*   Conditionals (when statements): Statements used to execute tasks only when certain conditions are met.
*   Module arguments: Parameters passed to Ansible modules to customize their execution.
*   Debugging: The process of identifying and resolving issues in Ansible playbooks, often using increased verbosity with the -vvv flag.
*   Fact gathering: The process by which Ansible collects system information from managed nodes, often used to make decisions in playbooks.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# [CHAPTER 10Real-world Application](#contents.xhtml_ch10a)

[Introduction](#contents.xhtml_sc2_423a)

Achieving the RHCE certification is a significant milestone in a Linux professional career. The journey does not end with certification, it begins there. This chapter helps you to prepare for a successful career as a certified engineer by exploring essential strategies and insights to leverage the certification effectively and continue professional growth. We will explore skill development, career planning, networking and staying current with industry trends as future proof professionals.

[Structure](#contents.xhtml_sc2_424a)

The chapter covers the following topics:

*   RHCE in real-world
*   Real world customers
*   Server use cases
*   High-performance computing
*   Hybrid cloud
*   RHEL artificial intelligence
*   Ansible AI lightspeed

[Objectives](#contents.xhtml_sc2_425a)

By the end of this chapter, readers will learn the importance of continuous learning beyond achieving the RHCE certification, underscoring the need to stay current with evolving technologies and industry trends. It highlights the necessity of developing a clear career roadmap, setting achievable goals, and building a robust professional network to leverage new opportunities. Additionally, the chapter stresses the importance of showcasing skills through a well-crafted professional portfolio and resume, understanding employer expectations for RHCE-certified professionals and maintaining relevance in the job market through ongoing education and professional development.

[RHCE in real-world](#contents.xhtml_sc2_426a)

While obtaining the RHCE certification is an important achievement in our Linux career, it marks the start of a new phase. This chapter explore strategies to effectively leverage our certification for ongoing professional growth. To help us prepare for a successful career as a certified engineer, we will explore essential strategies and insights to ensure we leverage our certification effectively and continue to grow professionally. This guide will cover skill development, career planning, networking, and staying current with industry trends.

[Master the fundamentals and beyond](#contents.xhtml_sc3_427a)

While the RHCE certification validates our expertise in managing and automating RHEL environments, the IT field constantly evolves. Stay current with the latest technologies and advancements in Linux, automation tools and related areas. Develop proficiency in advanced topics such as cloud computing, containerization (Docker, Kubernetes), DevOps practices and artificial intelligence or machine learning. These areas are highly sought after and can significantly enhance our career prospects. Practical experience is invaluable. Engage in real-world projects, contribute to open-source initiatives, or set up a home lab to experiment with new technologies and tools. This hands-on approach solidifies our knowledge and improves our problem-solving abilities.

[Develop a career roadmap](#contents.xhtml_sc3_428a)

Set clear goals by  defining short term and long-term career goals. Determine the roles we aspire to such as systems administrator, DevOps engineer or cloud architect and identify the skills and experiences needed to achieve these goals. Create a learning plan  based on our career goals and create a structured learning plan. Allocate time for studying new technologies, obtaining additional certifications for example, RHCA, AWS Certified Solutions Architect and attending relevant workshops and conferences. Understand the typical career progression in the IT industry. For example, starting as a junior Linux administrator, moving to a senior administrator or engineer role and eventually transitioning into leadership or specialized technical positions.

[Build a professional network](#contents.xhtml_sc3_429a)

Participate in professional associations and groups related to Linux and open-source technologies. Organizations like the Linux Foundation, local Linux User Groups (LUGs) and Red Hat user groups provide valuable networking opportunities. Be active in online forums, social media groups and platforms like GitHub and Stack Overflow. Sharing our knowledge, asking questions and contributing to discussions can help us build a reputation and connect with other professionals. Attend industry conferences, seminars and meetups. Events like Red Hat Summit, LinuxCon, KubeConf and various DevOps conferences offer opportunities to learn from experts, network with peers, and stay updated on industry trends.

[Showcase our skills](#contents.xhtml_sc3_430a)

Create a professional portfolio highlighting your projects, certifications and achievements to make your resume stand out from the pile of others. Include detailed descriptions of the problems solved, the technologies used and your impact on the workplace and ultimately, the world. Craft a compelling resume and LinkedIn profile communicating our skills, experiences and career objectives. Emphasize our RHCE certification and any relevant projects or contributions. Consider writing technical blogs or giving presentations at conferences and meetups. Sharing our knowledge establishes us as experts in our field and enhances our communication skills.

[Understand employer expectations](#contents.xhtml_sc3_431a)

Employers expect RHCE certified professionals to have deep technical knowledge and the ability to effectively manage and automate RHEL environments. Demonstrating proficiency in scripting, configuration management and troubleshooting is crucial. Develop essential soft skills such as communication, teamwork and problem solving. Articulating technical concepts for non-technical stakeholders and working collaboratively in diverse teams are highly valued. The ability to adapt to new technologies and methodologies is paramount. Employers value professionals who quickly learn and integrate new tools and practices into their workflows.

[Stay updated with industry trends](#contents.xhtml_sc3_432a)

Take advantage of continuous education resources like online courses, webinars and certification programs. Platforms like Red Hat Learning Subscription, Coursera, Pluralsight, and Udemy offer a wealth of knowledge. Regularly read industry publications, blogs and news sites to stay informed about the latest developments in Linux, cloud computing, DevOps and other relevant fields. Seek feedback from peers, mentors and supervisors to identify areas for improvement. Constructive feedback helps us refine our skills and stay aligned with industry standards.

Preparing for a career as a certified engineer goes beyond obtaining the RHCE certification. It involves continuous learning, strategic career planning, active networking, showcasing our skills, understanding employer expectations and staying current with industry trends. By following these strategies, we can maximize the value of our RHCE certification, advance our careers and make a meaningful impact in the IT industry.

The RHCE certification is a prestigious credential that validates our ability to manage and automate RHEL environments. Achieving this certification is a significant milestone but the actual value lies in applying this knowledge effectively in real-world roles.

The following top five Linux administration and engineering career positions showcase how to use the competencies gained through RHCE that employers expect from RHCE certified professionals:

*   System administrator: System administrators are responsible for installing, configuring and maintaining Linux servers. They ensure systems run smoothly, perform regular updates, manage user accounts and monitor system performance. We need skills like knowledge of file systems, process management, user and group management and system monitoring tools.
*   Systems engineer: Systems engineers design, implement and manage complex IT systems. They focus on ensuring all components work together seamlessly, often involving scripting, automation and performance tuning. The most requested skills are an advanced understanding of networking, scripting languages (e.g., Bash, Python) and configuration management tools like Ansible.
*   DevOps engineer: DevOps engineers work at the intersection of development and operations. They automate the deployment process, manage CI or CD pipelines, and ensure the reliability and scalability of applications. Employers usually require proficiency in automation tools, containerization technologies (e.g., Docker, Kubernetes), and CI or CD practices.
*   Cloud engineer: Cloud engineers specialize in designing and managing cloud-based infrastructure. They use platforms like AWS, Azure and OpenStack to deploy scalable and secure cloud environments.

    The following skills are needed:

    *   Understanding of cloud architecture
    *   Orchestration tools
    *   Cloud security best practices
*   Security engineer: Security engineers focus on protecting systems and data from threats. They implement security policies, manage firewalls and conduct regular security audits. The required skills are knowledge of security protocols, vulnerability assessment tools and best practices for system hardening.

Mapping RHCE competencies to the top five job responsibilities as follows:

*   System monitoring and performance tuning:
    *   Competencies: RHCE certification ensures we can use tools like top, htop and vmstat to monitor system performance. We also learn how to tune system parameters for optimal performance.
    *   Application: These skills are critical for system administrators who need to ensure systems are running efficiently and for systems engineers who design performance optimized environments.
*   User and group management:
    *   Competencies: RHCE covers creating, modifying and deleting users and groups, setting permissions and managing user policies.
    *   Application: Essential for system administrators managing multi-user environments and security engineers ensuring proper access controls.
*   Network configuration and troubleshooting:
    *   Competencies: We gain expertise in configuring network interfaces, managing firewall rules and troubleshooting network issues.
    *   Application: Vital for systems engineers designing network architectures and DevOps engineers ensuring seamless network connectivity for applications.
*   Automation and scripting:
    *   Competencies: RHCE training includes writing and debugging scripts in Bash and using Ansible for configuration management.
    *   Application: Crucial for DevOps engineers automating deployment processes and cloud engineers managing infrastructure as code.
*   Security implementation:
    *   Competencies: RHCE covers SELinux, firewalls, and best practices for system security.
    *   Application: Key for security engineers implementing robust security measures and system administrators maintaining compliance.

Employers highly value RHCE certified professionals for their verified expertise and practical skills.

Following are the typical employer’s expectations:

*   Technical proficiency:
    *   Employers expect RHCE certified individuals to understand RHEL and related technologies deeply.
    *   Our ability to efficiently manage, troubleshoot, and optimize Linux systems makes us a critical asset in any IT team.
*   Problem solving skills:
    *   Employers look for professionals who can diagnose and resolve complex technical issues swiftly.
    *   The hands-on nature of RHCE training ensures we are well-equipped to handle real-world challenges.
*   Automation and efficiency:
    *   Automation is a key focus for modern IT environments. Employers expect us to leverage scripting and configuration management tools to streamline operations.
    *   Our skills in automating repetitive tasks and managing infrastructure as code increase operational efficiency and reduce downtime.
*   Security awareness:
    *   With increasing cybersecurity threats, employers expect us to implement and maintain robust security practices.
    *   Our knowledge of SELinux, firewall management and security policies help protect the organization’s data and systems.
*   Continuous learning:
    *   Technology evolves rapidly and employers value professionals committed to continuous improvement and staying updated with industry trends.
    *   Our ongoing learning and adaptation to new tools and methodologies ensure we remain a valuable resource in the IT landscape.

The RHCE certification provides a solid foundation in Linux administration and engineering. By understanding how these competencies translate to real-world roles and aligning with employer expectations, we can effectively leverage our RHCE knowledge to advance our careers and significantly impact the IT industry. Whether we aim to become a system administrator, a DevOps engineer, or a security specialist, the skills and insights gained through the RHCE certification will be a powerful steppingstone to success.

[Red Hat Certified Architect](#contents.xhtml_sc3_433a)

The career path from RHCE to RHCA is a progressive journey that signifies the pinnacle of expertise within the Red Hat certification program. Starting as an RHCE, a professional demonstrates proficient skills in managing and automating RHEL environments. This foundational certification is the gateway to advanced roles and responsibilities. To advance to RHCA, RHCE must complete a series of specialized certifications, each focusing on key areas such as DevOps, cloud computing, performance tuning and security. This progression involves rigorous training and hands-on experience, ensuring the professional can architect complex, scalable and secure IT solutions. Achieving RHCA status validates an individual’s technical prowess across multiple disciplines and positions them as a leader capable of designing and implementing sophisticated enterprise-level systems. This esteemed certification opens doors to senior roles such as IT architect, senior DevOps engineer and enterprise solutions architect marking a significant milestone in a Linux professional’s career.

[Job directories](#contents.xhtml_sc3_434a)

RHCEs are highly sought after for their expertise in managing and automating RHEL environments. To navigate the job market effectively, RHCEs can leverage various job directories. This analysis focuses on three prominent platforms: Glassdoor, Jooble, and Indeed, highlighting how each serve RHCE engineers in their job search.

[Glassdoor](#contents.xhtml_sc4_435a)

Glassdoor is a comprehensive platform that combines job listings with company reviews, salary reports and interview insights. This unique blend of features gives RHCE engineers valuable context about potential employers, helping them make informed decisions.

Following are the strengths of Glassdoor:

*   Company insights: Glassdoor's detailed company reviews give RHCE engineers a glimpse into the workplace culture, management style and employee satisfaction. This is crucial for understanding the environment where they might work.
*   Salary information: Glassdoor offers extensive salary data, allowing RHCE engineers to gauge competitive compensation for their skills and experience level.
*   Interview reviews: Insights into the interview process can help RHCE engineers prepare effectively knowing what to expect and what specific skills or questions might be emphasized.

Following are the weaknesses of Glassdoor:

*   Job listings: While Glassdoor has a robust database, its focus on comprehensive company profiles can sometimes mean fewer job listings than more dedicated job search engines.
*   Navigation: The depth of information can be overwhelming, requiring users to sift through various sections to find pertinent job listings.

Glassdoor is ideal for RHCE engineers who value in-depth company research and want to understand the broader context of their potential employers. It is beneficial when considering long term career moves where company culture and fit are critical.

[Jooble](#contents.xhtml_sc4_436a)

Jooble is a job search aggregator that compiles listings from various job boards and company websites providing a wide-ranging search engine for job seekers. Its primary advantage is the sheer volume of job listings it can access.

Following are the strengths of Jooble:

*   Aggregated listings: Jooble’s strength lies in its ability to pull job listings from multiple sources giving RHCE engineers access to many opportunities from a single platform.
*   Simplicity: The straightforward interface makes it easy to quickly find relevant job postings without the distraction of additional content.

Following are the weaknesses of Jooble:

*   Limited context: Unlike Glassdoor, Jooble does not offer company reviews, salary insights or interview tips which can limit the depth of information available to job seekers.
*   Redundancy: Since Jooble aggregates listings from various sources, users might encounter duplicate postings.

Jooble is best for RHCE engineers looking to cast a wide net in their job search. It is particularly useful for identifying a broad range of opportunities quickly, especially for those open to various locations or types of employers.

[Indeed](#contents.xhtml_sc4_437a)

Indeed is one of the most popular job search engines globally, known for its extensive database of job listings, company reviews and salary information. It offers a balanced approach, combining features of both Glassdoor and Jooble.

Following are the strengths of Indeed:

*   Comprehensive listings: Indeed, boasts a vast array of job postings, making it a go-to resource for RHCE engineers seeking diverse opportunities.
*   User reviews and salaries: Similar to Glassdoor, Indeed provides company reviews and salary insights, though not as detailed, which helps job seekers understand their potential employers better.
*   Job alerts: Indeed’s job alert feature ensures that RHCE engineers can stay updated with the latest opportunities matching their criteria.

Following are the weaknesses of Indeed:

*   Ad overload: The platform can sometimes be cluttered with ads, detracting from the user experience.
*   Quality control: Given its size, some job postings might be outdated or less relevant.

Indeed platform is ideal for RHCE engineers who want a comprehensive job search tool that balances extensive job listings with helpful company information. It is particularly effective for those who appreciate regular updates and alerts about new opportunities.

RHCE engineers can leverage job directories like Glassdoor, Jooble and Indeed to significantly enhance their job search. Glassdoor excels in providing detailed company insights. Jooble offers extensive aggregated listings. Indeed provides a balanced combination of both. By using these platforms strategically, RHCE engineers can navigate the job market more effectively, finding opportunities that align with their skills, preferences and career goals.

[Real world customers](#contents.xhtml_sc3_438a)

Organizations use RHEL to create hybrid cloud environments, combining on-premises infrastructure with public cloud resources. This setup provides flexibility and scalability while maintaining control over critical data and applications.

Following is an example:

A financial services company deploys RHEL across its data centers and integrates it with AWS for additional computational power during peak processing times, ensuring compliance and security.

RHEL is the foundation for modernization and automation projects, enabling businesses to update legacy systems and automate workflows.

Following is an example:

A manufacturing company uses RHEL and Red Hat Ansible Automation Platform to automate its supply chain processes, reducing manual intervention and improving efficiency.

With its integrated container tools, RHEL supports modern application development practices, including using containers for microservices architectures.

Following is an example:

A tech startup leverages RHEL and Kubernetes OpenShift to develop, test and deploy its applications in a containerized environment, speeding up the development cycle and ensuring consistency across different stages.

RHEL partners offer managed services to monitor and maintain customer environments, providing patching, performance optimization, and security management support.

Following is an example:

An IT services company provides managed services for clients running RHEL, ensuring their systems are always up-to-date and secure, allowing clients to focus on their core business operations.

RHEL is often used to migrate existing applications to the cloud, providing a stable and secure platform during and after migration.

Following is an example:

A healthcare provider migrates its patient management system to Azure using RHEL, ensuring minimal downtime and maintaining data integrity throughout the migration.

RHEL's flexibility extends to edge computing, which can be deployed in remote locations to process data closer to the source.

Following is an example:

An energy company deploys RHEL at its remote oil rigs to collect and process real-time sensor data, reducing latency and improving decision making.

[Advisory analysis](#contents.xhtml_sc3_439a)

The complex landscape of hybrid cloud environments demands a stable, secure and flexible foundation to meet business and customer needs consistently. RHEL stands out as a robust solution addressing these requirements, offering partners significant opportunities for growth through reselling, deploying and providing services. Recent studies by Forrester and International Data Corporation (IDC), a global provider of market intelligence, advisory services, and events for the information technology, telecommunications, and consumer technology markets) provide in-depth insights into the value proposition and business potential associated with RHEL.

[Forrester](#contents.xhtml_sc4_440a)

Forrester's Total Economic Impact™ (TEI) study commissioned by Red Hat focuses on the partner opportunities with RHEL. The study highlights how partners can generate multiple revenue streams by reselling RHEL subscriptions, engaging in project work such as deployment and migration and offering managed services. According to the study, RHEL's stability and flexibility enable customers to deploy applications and workloads faster with a consistent experience across data center, cloud and edge environments.

Following are the key findings from Forrester:

*   Revenue opportunities: Partners can expand their revenues through three main streams as follows:
    *   RHEL subscriptions: Partners sell RHEL subscriptions in one-to-three-year contracts, retaining 5% to 12% of the total annual subscription revenue.
    *   Project work: Partners help customers deploy and migrate RHEL, billing these consultative services by the week. This work typically adds 60% to 100% of the subscription revenue.
    *   Managed services: Beyond initial deployment, partners provide ongoing management services which can add significant revenue streams.
*   Enhanced partner profitability: The study normalizes financial results against the anticipated total value of RHEL subscriptions consumed by a partner’s customers. For example, if a customer's annual spend on RHEL is $75,000, the additional project work opportunity is calculated to be $54,750 (73% of the subscription revenue).
*   Comprehensive support and training: Red Hat provides partners with the necessary tools, training and support to deploy and build upon RHEL environments at an enterprise scale. Regular interactions with Red Hat account managers significantly enhance partner practices.

[International Data Corporation](#contents.xhtml_sc4_441a)

IDC is the premier global market intelligence, data, and events provider for information technology. IDC’s study underscores the business value of using paid Red Hat solutions versus non-paid open-source alternatives. The research highlights that RHEL and other Red Hat solutions provide essential features, performance and unavailable support with non-paid alternatives. Organizations that invest in Red Hat solutions achieve better IT staff efficiencies, development enablement and improved business outcomes.

Following are the benefits highlighted by IDC:

*   Empowering development teams: Red Hat solutions enable development teams to meet business demands for new applications and features effectively. This leads to higher productivity and reduced time-to-market.
*   Enhanced security and performance: RHEL helps ensure the security and performance of key applications and workloads, thereby limiting risks and related business costs. The time to detect and respond to security vulnerabilities is significantly reduced compared to non-paid open-source solutions.
*   Cost efficiency: While Red Hat solutions involve subscription costs, the operational efficiencies and IT cost savings achieved outweigh these expenses. Over three years, organizations using Red Hat solutions have experienced lower IT infrastructure costs and staff time than non-paid open-source alternatives.

Forrester and IDC studies affirm that RHEL offers substantial benefits to partners and their customers. Partners can drive significant revenue and profitability through subscription sales, project work and managed services. Additionally, organizations leveraging RHEL enjoy improved development productivity, enhanced security and overall cost efficiencies. These insights underscore the strategic advantage of adopting and partnering with Red Hat for long term business growth and innovation in the hybrid cloud era. For partners and organizations considering the transition to or expansion with RHEL, these studies provide a comprehensive framework to evaluate the potential business impact and strategic benefits. As IT environments become increasingly complex, the stability, flexibility and extensive support offered by Red Hat solutions make them a compelling choice for modern enterprises.

[Server use cases](#contents.xhtml_sc2_442a)

RHEL is an excellent choice for server usage as stability is important.

The following six servers provide insights into how to optimize power management and performance for different types of workloads:

[Webserver](#contents.xhtml_sc3_443a)

Apache HTTP server is one of the most popular web servers.

The following steps configure the system as a web server:

1.  Install Apache:

    dnf install httpd -y

2.  Start and enable Apache to run on boot:

    systemctl start httpd

    systemctl enable httpd

3.  Configure firewall to allow HTTP and HTTPS traffic:

    firewall-cmd --permanent --add-service=http

    firewall-cmd --permanent --add-service=https

    firewall-cmd –reload

4.  Create a simple HTML file:

    echo "<html><body><h1>Welcome to RHEL Web Server!</h1></body></html>" |

5.  Verify the installation:

    Open our browser and navigate to http://<our-server-ip>. We should see the welcome message.

A web server requires an efficient network and disk I/O. We can optimize a web server for power savings as follows:

*   Network configuration: Limit the network card to 100 Mbit/s if the external connection speed is sufficient. This is often the case for servers serving mostly static pages.
*   Disk I/O: Disable disk plugins for tuned if disk I/O is minimal.
*   CPU performance: Enable the on-demand governor to balance performance and power savings.
*   Additional tips: Ensure GPU power savings are turned on as graphics performance is generally not required for a webserver.

[Compute server](#contents.xhtml_sc3_444a)

Open MPI is a popular implementation of the Message Passing Interface (MPI) standard for parallel computing. To set up and run a simple MPI program using Open MPI.

Following are the steps to install the necessary packages, configure environment variables, and compile the program:

1.  Install Open MPI:

    dnf install openmpi openmpi-devel -y

2.  Set environment variables:

    Add the following lines to our .bashrc or .bash_profile:

    export PATH=$PATH:/usr/lib64/openmpi/bin

    export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/lib64/openmpi/lib

3.  Compile and run a simple MPI  program:

    Create a file named hello_mpi.c:

    #include <mpi.h>

    #include <stdio.h>

    int  main(int argc, char** argv) {

    MPI_Init(NULL, NULL);

    int world_size;

    MPI_Comm_size(MPI_COMM_WORLD, &world_size);

    int world_rank;

    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);

    printf("Hello world from rank %d out of %d processors\n", world_rank, world_size);

    MPI_Finalize();

    return  0;

    }

4.  Compile and run the program:

    mpicc hello_mpi.c -o hello_mpi

    mpirun -np 4 ./hello_mpi

A computer server focuses primarily on CPU performance. Optimization strategies include the following:

*   Disk and network I/O: Depending on the nature of the compute tasks, we may need to keep disk or network plugins for tuned active. For batch mode systems, consider a fully active tuned configuration.
*   CPU performance: Use the performance governor if the server handles intensive computational tasks.
*   Power management: Assess the utilization levels to determine the appropriate power management settings.

[Mail server](#contents.xhtml_sc3_445a)

Postfix is a popular Mail Transfer Agent (MTA). To set up and optimize a Postfix mail server.

Following are the steps for installation, configuration, and performance tuning:

dnf install postfix -y

1.  Start and enable Postfix:

    systemctl start postfix

    systemctl enable postfix

2.  Configure Postfix:

    Edit /etc/postfix/main.cf and set the following parameters:

    myhostname = mail.example.com

    mydomain = example.com

    myorigin = $mydomain

    inet_interfaces = all

    mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain

    relayhost =

    mynetworks = 127.0.0.0/8, [::1]/128

    home_mailbox = Maildir/

3.  Restart Postfix:

    systemctl restart postfix

A mail server demands efficient disk I/O and CPU utilization. Following is how to optimize it:

*   CPU performance: Turn on the on-demand governor as the final few percent of CPU performance are typically not critical.
*   Network speed: Do not limit network speed. Internal mail operations can benefit from higher link speeds such as one Gbit/s or ten Gbit/s.
*   Disk I/O: Disable disk plugins for tuned unless specific disk optimizations are necessary.

[File server](#contents.xhtml_sc3_446a)

Samba allows file sharing between Linux, macOS and Windows systems as follows:

1.  Install Samba:

    dnf install samba samba-client -y

2.  Configure Samba:

    Edit /etc/samba/smb.conf to define a shared directory as follows:

    [global]

    workgroup = WORKGROUP

    security = user

    [shared]

    path = /srv/samba/shared

    valid users = @smbgroup

    guest ok = no

    writable = yes

    browsable = yes

3.  Create the shared directory and set permissions:

    mkdir -p /srv/samba/shared

    chown -R root:smbgroup /srv/samba/shared

    chmod 2770 /srv/samba/shared

4.  Create a Samba user:

    groupadd smbgroup

    useradd -M -d /srv/samba/shared -s /sbin/nologin smbuser

    smbpasswd -a smbuser

    usermod -aG smbgroup smbuser

5.  Start and enable Samba:

    systemctl start smb

    systemctl enable smb

Fileservers have similar requirements to mail servers but may need more CPU performance depending on the protocol used as follows:

*   CPU performance: Use the on-demand governor. Samba-based servers generally require more CPU than Network File System (NFS) and NFS typically requires more than iSCSI. (Internet Small Computer Systems Interface).
*   Network configuration: Ensure network speed is sufficient for the file transfer load. Higher speeds like one Gbit/s or ten Gbit/s may be necessary for internal operations.
*   Disk I/O: Optimize disk I/O based on the protocol and usage patterns.

[Directory server](#contents.xhtml_sc3_447a)

OpenLDAP is an open-source LDAP implementation. To set up and configure OpenLDAP.

Following are the steps below to install, start, and configure the service, set a root password, and add base domain information and users:

1.  Install OpenLDAP:

    dnf install openldap openldap-servers openldap-clients -y

2.  Start and enable OpenLDAP:

    systemctl start slapd

    systemctl enable slapd

3.  Set up OpenLDAP root password:

    Generate a password hash as follows:

    Slappasswd

    Output will be something as {SSHA}5c4fa38b3e....

    Edit /etc/openldap/slapd.d/cn=config/olcDatabase={2}hdb.ldif and set the root password as follows:

    olcRootPW: {SSHA}5c4fa38b3e...

4.  Add base domain and users:

    Create a file named base.ldif as follows:

    dn: dc=example,dc=com

    objectClass: top

    objectClass: dcObject

    objectClass: organization

    o: Example Organization

    dc: example

    dn: cn=Manager,dc=example,dc=com

    objectClass: organizationalRole

    cn: Manager

    description: Directory Manager

    Add the entries to the LDAP directory as follows:

    ldapadd -x -D "cn=Manager,dc=example,dc=com" -W -f base.ldif

Directory servers generally have lower disk I/O requirements but emphasize network latency. Optimization considerations include the following:

*   Disk I/O: Ensure the server has enough RAM to minimize disk I/O requirements.
*   Network latency: Fine-tune network latency settings. We may consider reducing link speed for latency improvements, but this should be tested carefully.
*   CPU performance: Utilize the on-demand governor to balance performance with power savings.

Optimizing RHEL for these six servers involves a careful analysis of the specific workload requirements. Administrators can balance performance and energy efficiency by adjusting power management settings and using appropriate tuned profiles. Whether configuring a web server, computer server, mail server, fileserver or directory server, the above strategies provide a solid foundation for enhancing server performance while minimizing power consumption.

[High-performance computing](#contents.xhtml_sc2_448a)

High-performance computing (HPC) is crucial for solving complex, data driven challenges across various industries. The operating system is vital in ensuring that HPC infrastructure operates efficiently, seamlessly integrating hardware, software, networking and interfaces into a unified environment. RHEL is designed to meet these demands, providing a robust foundation for HPC workloads across datacenter, cloud, and hybrid environments. HPC has transitioned from large unified systems to expansive clusters of servers in both enterprise data centers and the cloud.

This evolution brings new challenges as follows:

*   Allocation and management: Managing numerous systems as a single entity to maximize performance and resource utilization.
*   Long life cycles: Integrating complex hardware and software over extended periods.
*   Lack of expertise: Addressing the scarcity of HPC specialists through consistent system management.
*   Security and compliance: Ensuring adherence to stringent security standards.
*   Diverse workloads:  Supporting various software and hardware configurations to meet different workload requirements.

RHEL provides a consistent and flexible platform tailored for running HPC workloads. It is the operating system of choice for many of the world's top supercomputers, offering a unified environment that spans datacenter, cloud and hybrid deployments. To support  HPC  environments and large-scale deployments, RHEL offers a variety of tools and features that enhance container management, security, resource optimization, and ensure long term reliability as follows:

*   Container tools: RHEL offers container tools such as Podman, Buildah and Skopeo, enhancing portability and reproducibility for HPC workloads. These tools support integrated container development and provide secure base images, facilitating container adoption for HPC.
*   Management tools: RHEL includes management tools to optimize resource usage and manage compute-intensive workloads at a scale. These tools ensure a streamlined user experience from development through deployment.
*   Built-in security features: RHEL includes advanced security features like live kernel patching and centralized identity and access control management. These features help defend against threats and ensure compliance with regulatory requirements.
*   Image builder: Image builder allows users to create custom images and deploy them in the cloud, providing a flexible and efficient deployment process.
*   Certified ecosystem: RHEL supports a wide range of vendors, products, clouds and open-source projects, ensuring reliable and efficient operation. This certified ecosystem allows organizations to choose preferred technologies without compromising on performance or reliability.
*   Production grade life cycle: RHEL offers a long, enterprise-grade support life cycle, including security updates, bug fixes and feature enhancements. This ensures uptime and prepares organizations for future HPC advancements, making RHEL a dependable platform for running AI and ML models at scale.

RHEL is optimized for high-performance graphics, animation and scientific activities. For example, on AWS cloud delivered via Amazon Desktop Cloud Visualization (DCV), a high-performance remote display protocol.

Red Hat collaborates with various partners to provide comprehensive solutions for HPC environments as follows:

*   CrowdStrike: Provides proven endpoint security through a cloud delivered platform.
*   NGINX plus: Offers a lightweight architecture with Federal Information Processing Standards (FIPS)  and Payment Card Industry (PCI) compliance, high availability and real-time monitoring. PCI compliance refers to adherence to the Payment Card Industry Data Security Standard (PCI DSS), a set of security standards designed to ensure that all companies that process, store, or transmit credit card information maintain a secure environment.
*   SAP HANA: Delivers advanced analytics and high-speed transactions in a single system.
*   Microsoft Structured Query Language (SQL) server: Available as an official container image on RHEL.

RHEL provides a powerful, flexible and secure foundation for high performance computing, supporting the diverse needs of modern HPC environments. By leveraging RHEL, organizations can maximize the value of their HPC clusters, ensure compliance and prepare for future advancements in HPC technology.

[Hybrid cloud](#contents.xhtml_sc2_449a)

Public cloud infrastructure offers numerous advantages including flexible pricing, access to the latest hardware advancements and the ability to run workloads without the need to build and maintain the infrastructure. RHEL is the most deployed commercial Linux distribution in the public cloud, certified for use with all major cloud providers and cloud marketplaces such as Microsoft Azure, AWS, Google Cloud, IBM Cloud and Alibaba Cloud. This certification ensures optimal user experiences across diverse cloud environments, providing multiple purchasing and management options. Maintaining hybrid environments increases overall IT complexity and introduces unique challenges including the following:

*   Managing subscriptions: Procuring, tracking, and managing subscriptions becomes complex.
*   Inconsistent deployment environments: New environments can create migration obstacles and increase deployment complexity.
*   Friction in the developer experience: Developers require quick access to reliable OS images and familiar toolchains, libraries, container tools and runtimes.

RHEL is engineered to reduce IT complexity and support application migration across different cloud environments. RHEL offers tools with best practices and expert guidance for frictionless management. It supports consistent deployment across hybrid clouds, eliminating the need for additional skills for different environments. The seamless integration into the development lifecycle allows team members to access required resources quickly, facilitating a smooth path to production without innovation lock-in. Cloud development RHEL provides easy access to reliable OS images in the cloud along with necessary toolchains, libraries, container tools and runtimes. This ensures a streamlined path from development to production. Updates via application streams allow developers and IT architects to experiment with the latest tools while maintaining earlier versions of production applications.

RHEL supports container technologies with integrated tools like Podman, Buildah and Skopeo and secure base images. It is a consistent yet flexible host for container adoption across various deployment environments. Certified language runtime containers further support evolving development needs.

Standardizing RHEL across IT infrastructure improves security, reduces operational burdens and cuts costs. RHEL offers streamlined OS management with automated, repeatable workflows, intuitive web-based administration and consistent OS administration across infrastructure types.

RHEL’s image builder is a set of CLI  plugins that assist in configuring and creating custom images for cloud deployment. Push-to-cloud capabilities allow direct push of custom images to cloud provider inventories, addressing provisioning and migration challenges in disconnected environments and enabling operations teams to scale using cloud-native infrastructure.

Red Hat Insights provide a single view of where subscriptions are deployed across hybrid cloud environments. It offers administrators and procurement teams reporting on usage against capacity and visibility into hypervisor topology to identify what guests are running and where.

RHEL delivers reliable OS images, toolchains, libraries, container tools and runtimes in the cloud, streamlining the development-to-production path. Collaboration with major cloud providers ensures support for future focused deployments on a solid foundation. RHEL's integrated container tools and secure base images support cloud migration and application development, offering flexibility for container adoption across various environments. Standardizing RHEL across IT infrastructure enhances security, reduces operational burdens, and lowers costs with streamlined OS management. RHEL's image builder allows custom images to be created and deployed directly to cloud providers, simplifying provisioning and migration in hybrid environments. Red Hat Insights provides comprehensive visibility and reporting on hybrid cloud deployments, helping optimize resource utilization and infrastructure management.

RHEL offers a robust, flexible foundation for hybrid cloud environments, simplifying management, enhancing development and supporting seamless integration across diverse cloud infrastructures. With features designed to reduce complexity and improve efficiency, RHEL is an optimal choice for enterprises looking to leverage the benefits of a hybrid cloud. Explore more about RHEL in the cloud through the AWS Marketplace, Azure Marketplace, and Google Cloud Marketplace and take advantage of the close collaboration between Red Hat and its partners to solve our business challenges.

UBI are a set of container images provided by Red Hat that serve as a reliable foundation for building and deploying containerized applications. UBIs are designed to offer the consistency and security of RHEL while providing the flexibility to run on any container host or platform, regardless of subscription status. UBIs include essential tools and libraries allowing developers to build and distribute applications with confidence. For example, UBI minimal is a lightweight image that contains only the core runtime dependencies, which is ideal for microservices. UBI standard includes additional packages that are suitable for a wider range of applications. UBI multi-language is tailored for environments requiring multiple language runtimes. These images can be freely redistributed and used to create custom container images providing a robust and secure base that adheres to RHEL standards.

[RHEL artificial intelligence](#contents.xhtml_sc2_450a)

In recent times, artificial intelligence, machine learning and generative AI have become common words in our dictionary. The world demands more AI use cases and Red Hat proposes RHEL AI as an open-source platform to develop our models. RHEL AI provides a robust and accessible platform for developing, deploying and managing generative AI models within an enterprise environment. It was presented at the Red Hat Summit 2024. Leveraging open-source tools, RHEL AI integrates the InstructLab project and granite language models with a bootable image of RHEL, creating a versatile foundation for enterprise AI applications.

Following are the components of RHEL AI:

*   Granite language models: Granite models are open source, Apache-2 licensed foundation models supported and indemnified by Red Hat and IBM for enterprise use. These models facilitate the development of generative AI applications ensuring reliability and compliance within enterprise environments.
*   InstructLab: InstructLab provides a CLI and backend for tuning and augmenting large language models (LLMs) with additional skills and data. It offers a scalable, cost-effective solution for enhancing LLM capabilities making it easier for organizations to contribute knowledge and skills.
*   RHEL image mode: RHEL AI uses a bootable container image approach allowing for seamless management and scalability. The RHEL image mode integrates granite models and InstructLab tooling packages including essential libraries and hardware accelerators for NVIDIA, Intel and Advanced Micro Devices (AMD).

[Cloud-native scalability and portability](#contents.xhtml_sc4_451a)

RHEL AI is designed for cloud-native scalability, supporting deployment across hybrid cloud environments. It provides an onramp to AI at scale with Red Hat OpenShift AI based on Kubernetes and additional capabilities with IBM watsonx.ai. This portability ensures that enterprises can efficiently manage and scale their AI workloads.

Following are the deployment methodologies:

*   Bootable container image: RHEL AI is distributed as a bootable container image, enabling easy provisioning on both bare metal and cloud instances. This approach ensures a consistent and reproducible environment for running AI models.
*   Kickstart for automated deployment: Using Kickstart, an automation tool integrated with the RHEL installer (Anaconda), organizations can automate the deployment of RHEL AI. A recent addition, the ostreecontainer command in RHEL simplifies the provision of bootable container images over the network.

    Following is an example of kickstart file:

    # Basic configuration

    network --bootproto=dhcp --device=link --activate

    clearpart --all --initlabel --disklabel=gpt

    reqpart --add-boot

    part / --grow --fstype xfs

    # Provisioning the bootable container

    ostreecontainer --url quay.io/<our-user-name>/nvidia-bootc:latest

    # Additional configurations

    firewall --disabled

    services --enabled=sshd

    user --name=cloud-user --groups=wheel --plaintext --password

    sshkey --username cloud-user "ssh-ed25519 AAAAC3Nza....."

    rootpw --iscrypted locked

    sshkey --username root "ssh-ed25519 AAAAC3Nza..."

    reboot

    This kickstart file automates the installation of RHEL AI including network setup, disk partitioning and provisioning the bootable container image.

[Hardware and performance expectations](#contents.xhtml_sc3_452a)

RHEL AI is validated on various server platforms including Dell, IBM, Lenovo and AWS instances.

The minimum hardware requirements are as follows:

*   Total GPU memory: 320GB (e.g., 4 GPUs with 80GB each)
*   Disk space: 200GB for model storage

Training performance depends on the hardware configuration. For example, a single GPU can train approximately 250 samples per minute. With 8 GPUs, training 10,000 samples over 10 epochs should take around 50 minutes.

Following are the steps for initial setup for RHEL AI and InstructLab:

1.  Create a working directory:

    mkdir my-project

    cd my-project

2.  Initialize the project:

    ilab init

3.  Set up hugging face token:

    export HF_TOKEN=<our-token-value>

4.  Download granite and Mixtral models:

    ilab download --repository ibm/granite-7b-base

    ilab download --repository mistralai/Mixtral-8x7B-Instruct-v0.1

Following steps are necessary for training and serving models:

1.  Generate synthetic data:

    ilab generate

2.  Start training:

    ilab train --num-epochs 9

3.  Serve the new model:

    ilab serve --model tuned-0504-0051/samples_49920

4.  Interact with the model:

    ilab chat --model tuned-0504-0051/samples_49920

RHEL AI provides a comprehensive and scalable platform for developing and deploying AI models in enterprise environments. By leveraging open-source technologies and providing robust deployment methodologies, RHEL AI empowers organizations to harness the power of generative AI. With its cloud-native scalability, validated hardware support and integration with Red Hat OpenShift AI, RHEL AI is well suited to meet the growing demands of AI-driven applications in modern enterprises. For further information, resources and community support, visit the official RHEL AI developer preview repository on GitHub.

[Ansible AI lightspeed](#contents.xhtml_sc2_453a)

Ansible AI lightspeed is revolutionizing IT automation by leveraging AI to enhance the creation, optimization and maintenance of Ansible playbooks. This innovative feature integrates AI-driven insights and suggestions into the Ansible development workflow, enabling faster and more efficient generation of high-quality automation code. Key benefits include AI-powered code generation perfectly integrated in the development software Visual Studio which reduces the time and effort required to write and maintain scripts and intelligent suggestions that provide real-time assistance and performance enhancements.

AI lightspeed acts as a mentor for newcomers, guiding them through the process of writing playbooks and explaining the rationale behind suggestions, while experienced users benefit from continuous learning and best practice insights. It integrates seamlessly with existing Ansible tools and workflows, making it easy to adopt without significant changes to current processes. Practical applications include infrastructure provisioning, configuration management, application deployment and security and compliance, where AI-generated playbooks ensure consistency, reduce downtime and enhance security postures.

Ansible AI lightspeed represents a significant leap forward in IT automation, combining Ansible's robust capabilities with the transformative power of AI to achieve new heights of efficiency and productivity making it an indispensable tool for any organization aiming to stay ahead in the rapidly evolving world of IT infrastructure management. Embrace the future of IT automation with Ansible AI lightspeed and transform how we manage our infrastructure today.

[Conclusion](#contents.xhtml_sc2_454a)

Preparing for a career as a certified engineer goes beyond obtaining the RHCE certification. It involves continuous learning, strategic career planning, active networking, showcasing skills, understanding employer expectations and staying current with industry trends. By following these strategies, one can maximize the value of the RHCE certification, advance their career and make a meaningful impact in the IT industry. Good luck with your RHCE exam and future career endeavors!

[Points to remember](#contents.xhtml_sc2_455a)

*   Continuous learning is crucial in the ever-evolving IT field.
*   Setting clear career goals helps in achieving long term success.
*   Networking can open doors to new opportunities and collaborations.
*   A professional portfolio and resume are essential tools for showcasing skills.
*   Employers value technical skills and soft skills like communication and teamwork.
*   Staying current with industry trends ensures relevance and competitiveness in the job market.

[Multiple choice questions](#contents.xhtml_sc2_456a)

1.  What command can we use to check the syntax of an Ansible playbook?
    1.  ansible-playbook --syntax-check
    2.  ansible-playbook --check
    3.  ansible-playbook --validate
    4.  ansible-playbook –verify
2.  Which Ansible module is used to manage software packages on RHEL systems?
    1.  ansible.builtin.apt
    2.  ansible.builtin.package
    3.  ansible.builtin.dnf
    4.  ansible.builtin.yum
3.  What is the purpose of the ansible.builtin.lineinfile module?
    1.  To copy files from the control node to managed nodes
    2.  To ensure a specific line is present or absent in a file
    3.  To manage SELinux policies
    4.  To install software packages
4.  Which module should we use to create a new user in Ansible?
    1.  ansible.builtin.group
    2.  ansible.builtin.acl
    3.  ansible.builtin.user
    4.  ansible.builtin.sudo

[Answers](#contents.xhtml_sc3_457a)

1 a.

2 d.

3 b.

4 c.

[Questions](#contents.xhtml_sc2_458a)

1.  Explain the importance of continuous learning beyond the RHCE certification.
2.  What are the key components of a professional portfolio for an RHCE certified professional?
3.  How can networking benefit a Linux professional in advancing their career?
4.  Describe the role of automation and scripting in enhancing an RHCE certified professional's job performance.
5.  What are some of the key expectations employers have from RHCE certified professionals?
6.  How can RHCE certified professionals stay updated with the latest industry trends and technologies?

[Key terms](#contents.xhtml_sc2_459a)

*   Continuous learning: The ongoing process of learning new skills and technologies to stay current in the field.
*   Career roadmap: A structured plan outlining short-term and long-term career goals and the steps needed to achieve them.
*   Professional network: A group of professional contacts that can provide support, information, and opportunities.
*   Portfolio: A collection of documents and projects that showcase an individual’s skills, achievements, and experiences.
*   Automation: The use of technology to perform tasks without human intervention.
*   Scripting: Writing scripts to automate repetitive tasks and processes.
*   Configuration management: The process of maintaining system settings and configurations in a consistent and automated manner.
*   SELinux: A security architecture integrated into the Linux kernel that provides mechanisms for supporting access control security policies.
*   Continuous integration or continuous deployment (CI or CD): A method to frequently deliver apps to customers by introducing automation into the stages of app development.
*   Cloud computing: The delivery of computing services over the internet, including storage, processing power and applications.
*   Containerization: The encapsulation of an application and its dependencies into a container that can run on any computing environment.
*   DevOps: A set of practices that combine software development (Dev) and IT operations (Ops) to shorten the development lifecycle and deliver high-quality software continuously.
*   Firewall: A network security device that monitors and controls incoming and outgoing network traffic based on predetermined security rules.
*   Lightweight Directory Access Protocol (LDAP): An open, vendor-neutral, industry-standard application protocol for accessing and maintaining distributed directory information services over an IP network.
*   Open source: Software for which the original source code is made freely available and may be redistributed and modified.
*   Hybrid cloud: A computing environment that uses a mix of on-premises, private cloud, and public cloud services with orchestration between these platforms.
*   Red Hat Insights: A predictive analytics tool that helps identify and remediate security and performance issues in Red Hat Enterprise Linux environments.

Join our book’s Discord space

Join the book's Discord Workspace for Latest updates, Offers, Tech happenings around the world, New Release and Sessions with the Authors:

**[https://discord.bpbonline.com](https://discord.bpbonline.com)**

![](images/fm1.png)

# Index

A

AAP, best practices [171](#ch05.xhtml_page171), [172](#ch05.xhtml_page172)

AAP, key components

automation, analytics [171](#ch05.xhtml_page171)

automation, controlling [171](#ch05.xhtml_page171)

automation hub [171](#ch05.xhtml_page171)

execution, environment [171](#ch05.xhtml_page171)

Red Hat, integrating [171](#ch05.xhtml_page171)

role-based access control [171](#ch05.xhtml_page171)

Access Control Lists (ACLs) [73](#ch03.xhtml_page73), [74](#ch03.xhtml_page74)

Anaconda [27](#ch02.xhtml_page27)

Anaconda, installing [27](#ch02.xhtml_page27), [28](#ch02.xhtml_page28)

Anaconda, key area [28](#ch02.xhtml_page28), [29](#ch02.xhtml_page29)

anacron [57](#ch03.xhtml_page57)

Ansible [94](#ch04.xhtml_page94)

Ansible AI Lightspeed [323](#ch10.xhtml_page323), [324](#ch10.xhtml_page324)

Ansible Automation Platform (AAP) [170](#ch05.xhtml_page170)

Ansible CLI [145](#ch05.xhtml_page145)

Ansible Collections [161](#ch05.xhtml_page161)-[165](#ch05.xhtml_page165)

Ansible, communicates

Linux [95](#ch04.xhtml_page95)

macOS [96](#ch04.xhtml_page96)

Windows [96](#ch04.xhtml_page96)

Ansible, foundation

inventory [96](#ch04.xhtml_page96)

module, tasks [96](#ch04.xhtml_page96)

playbooks [96](#ch04.xhtml_page96)

Ansible Hoc, commands [97](#ch04.xhtml_page97)

Ansible, installing steps

Files Nodes, deploying [139](#ch05.xhtml_page139)

Linux Nodes, managing [138](#ch05.xhtml_page138)

node, controlling [136](#ch05.xhtml_page136), [137](#ch05.xhtml_page137)

Privilege Escalation [141](#ch05.xhtml_page141)

privilege escalation, configuring [138](#ch05.xhtml_page138), [139](#ch05.xhtml_page139)

Shell Scripts, converting [139](#ch05.xhtml_page139)

Windows Nodes, managing [140](#ch05.xhtml_page140)

Ansible, inventories

aliases [99](#ch04.xhtml_page99)

collections [98](#ch04.xhtml_page98)

dynamic [98](#ch04.xhtml_page98)

parameters [99](#ch04.xhtml_page99)

variables [99](#ch04.xhtml_page99)

Ansible, modules

file [100](#ch04.xhtml_page100)

network [102](#ch04.xhtml_page102)

software package [101](#ch04.xhtml_page101)

system [102](#ch04.xhtml_page102)

Ansible Modules, key aspects

extensibility [100](#ch04.xhtml_page100)

functionality [99](#ch04.xhtml_page99)

idempotency [100](#ch04.xhtml_page100)

integration [100](#ch04.xhtml_page100)

language [100](#ch04.xhtml_page100)

Ansible Navigator [144](#ch05.xhtml_page144)

Ansible Navigator, capabilities [144](#ch05.xhtml_page144)

Ansible Navigator, installation steps [144](#ch05.xhtml_page144)

Ansible, nodes

controller [95](#ch04.xhtml_page95)

managed [95](#ch04.xhtml_page95)

Ansible Playbooks [105](#ch04.xhtml_page105)

Ansible Playbooks, architecture

Ansible Handlers [118](#ch04.xhtml_page118)

conditional, statements [117](#ch04.xhtml_page117)

Facts [112](#ch04.xhtml_page112)

Filters [112](#ch04.xhtml_page112)

loops [116](#ch04.xhtml_page116)

plays [107](#ch04.xhtml_page107)

results, retrieving [114](#ch04.xhtml_page114), [115](#ch04.xhtml_page115)

task failure, handling [123](#ch04.xhtml_page123)

techniques, configuring [107](#ch04.xhtml_page107)

variables [109](#ch04.xhtml_page109), [110](#ch04.xhtml_page110)

Ansible Playbooks, benefits

efficiency [122](#ch04.xhtml_page122)

flexibility [122](#ch04.xhtml_page122)

idempotency [122](#ch04.xhtml_page122)

Ansible Playbooks, features

error, handling [106](#ch04.xhtml_page106)

human-readable format [106](#ch04.xhtml_page106)

idempotency [106](#ch04.xhtml_page106)

task, managing [106](#ch04.xhtml_page106)

variable, integrating [106](#ch04.xhtml_page106)

Ansible Playbooks, key points

configuration, managing [129](#ch04.xhtml_page129)-[131](#ch04.xhtml_page131)

error, handling [126](#ch04.xhtml_page126)

playbook, testing [127](#ch04.xhtml_page127), [128](#ch04.xhtml_page128)

YAML, configuring [125](#ch04.xhtml_page125)

Ansible Playbooks, outline

error, handling [106](#ch04.xhtml_page106)

hosts/group, defining [106](#ch04.xhtml_page106)

tasks [106](#ch04.xhtml_page106)

variable, setup [106](#ch04.xhtml_page106)

Ansible Playbooks, practices

descriptive name [125](#ch04.xhtml_page125)

error, handling [126](#ch04.xhtml_page126)

idempotency [125](#ch04.xhtml_page125)

modular, designing [125](#ch04.xhtml_page125)

version, controlling [125](#ch04.xhtml_page125)

Ansible Playbooks, use cases

data, transformation [113](#ch04.xhtml_page113)

dates, formatting [113](#ch04.xhtml_page113)

list, operations [113](#ch04.xhtml_page113)

mathematical, operation [113](#ch04.xhtml_page113)

network data, manipulation [113](#ch04.xhtml_page113)

strings, working [113](#ch04.xhtml_page113)

Ansible, tasks

installation [96](#ch04.xhtml_page96)

inventory, configuring [97](#ch04.xhtml_page97)

playbook, optimizing [97](#ch04.xhtml_page97)

Ansible Test [260](#ch08.xhtml_page260)

Ansible Tests [166](#ch05.xhtml_page166)

Ansible Tests, types

functional testing [166](#ch05.xhtml_page166)

integration testing [166](#ch05.xhtml_page166)

unit testing [166](#ch05.xhtml_page166)

Ansible Variables, types

Built-in [110](#ch04.xhtml_page110)

Declaring [110](#ch04.xhtml_page110)

precedence [111](#ch04.xhtml_page111)

Ansible Vault [153](#ch05.xhtml_page153), [154](#ch05.xhtml_page154)

Ansible Vault, key guidelines [154](#ch05.xhtml_page154)

B

Bash Scripting [94](#ch04.xhtml_page94)

Bash Scripts [35](#ch02.xhtml_page35)

Bash Scripts, breakdown [36](#ch02.xhtml_page36)

Boot Process [80](#ch03.xhtml_page80)

Boot Process, key points

dependencies, conflicts [79](#ch03.xhtml_page79)

service, status [78](#ch03.xhtml_page78)

start/stop, services [79](#ch03.xhtml_page79)

Bootstrap [234](#ch08.xhtml_page234)

Bootstrap, steps [234](#ch08.xhtml_page234), [235](#ch08.xhtml_page235)

C

CentOS Stream [212](#ch07.xhtml_page212)

CentOS Stream, advantages

community driven, innovation [213](#ch07.xhtml_page213)

continuous, delivery [212](#ch07.xhtml_page212)

feedback loop [212](#ch07.xhtml_page212)

intergration, testing [213](#ch07.xhtml_page213)

REHL, compatibility [213](#ch07.xhtml_page213)

release model, rolling [213](#ch07.xhtml_page213)

CentOS Stream, architectures [214](#ch07.xhtml_page214)

CentOS Stream, installation [213](#ch07.xhtml_page213)

CentOS Stream, use cases

development, testing [213](#ch07.xhtml_page213)

enterprise, environments [213](#ch07.xhtml_page213)

sysadmin, training [213](#ch07.xhtml_page213)

chmod [71](#ch03.xhtml_page71)

chmod, effects

default permissions [73](#ch03.xhtml_page73)

special permissions [72](#ch03.xhtml_page72)

chmod, methods

Numeric [71](#ch03.xhtml_page71), [72](#ch03.xhtml_page72)

Symbolic [71](#ch03.xhtml_page71)

CLI, functionalities

ansible [104](#ch04.xhtml_page104)

ansible-config [105](#ch04.xhtml_page105)

ansible-connection [104](#ch04.xhtml_page104)

ansible-console [104](#ch04.xhtml_page104)

ansible-doc [104](#ch04.xhtml_page104)

ansible-galaxy [105](#ch04.xhtml_page105)

ansible-inventory [104](#ch04.xhtml_page104)

ansible-playbook [104](#ch04.xhtml_page104)

ansible-sign [105](#ch04.xhtml_page105)

ansible-test [105](#ch04.xhtml_page105)

ansible-vault [105](#ch04.xhtml_page105)

Cloud Providers, types

Amazon Web Service (AWS) [225](#ch07.xhtml_page225)

Google Cloud Platform (GCP) [226](#ch07.xhtml_page226)

Microsoft Azure [226](#ch07.xhtml_page226)

VMware [227](#ch07.xhtml_page227)

Cockpit Live Patch [215](#ch07.xhtml_page215)

Cockpit Live Patch, practices [216](#ch07.xhtml_page216)

Cockpit Live Patch, steps [215](#ch07.xhtml_page215)

Command Line [31](#ch02.xhtml_page31)

Command Line Interface (CLI) [103](#ch04.xhtml_page103)

Command Line, parts [32](#ch02.xhtml_page32)

crontab [57](#ch03.xhtml_page57)

crontab backup, appropriate [64](#ch03.xhtml_page64), [65](#ch03.xhtml_page65)

crontab, steps [63](#ch03.xhtml_page63), [64](#ch03.xhtml_page64)

crontab, syntax [62](#ch03.xhtml_page62)

D

DNF [81](#ch03.xhtml_page81)

DNF, components [81](#ch03.xhtml_page81)

DNF, review

dependencies, updating [45](#ch02.xhtml_page45)

Kernel, managing [45](#ch02.xhtml_page45)

package, removing [45](#ch02.xhtml_page45)

package, updating [44](#ch02.xhtml_page44)

Documentation [102](#ch04.xhtml_page102), [103](#ch04.xhtml_page103)

Dual Stack [178](#ch06.xhtml_page178), [179](#ch06.xhtml_page179)

Dual Stack, environments

Intrusion Detection Systems (IDS) [181](#ch06.xhtml_page181)

Monitor [180](#ch06.xhtml_page180)

routing [179](#ch06.xhtml_page179), [180](#ch06.xhtml_page180)

Security Information Event Management (SIEM) [181](#ch06.xhtml_page181)

E

encrypted file with playbook, optimizing [155](#ch05.xhtml_page155)

Error Handle, strategies [123](#ch04.xhtml_page123)

Error Management, practices

condition, definition [124](#ch04.xhtml_page124)

continuous, reviewing [124](#ch04.xhtml_page124)

error, evaluating [124](#ch04.xhtml_page124)

mode consideration, checking [124](#ch04.xhtml_page124)

selective, application [124](#ch04.xhtml_page124)

Essential Tools [16](#ch01.xhtml_page16)

Essential Tools, ability [17](#ch01.xhtml_page17)

F

File Management [51](#ch02.xhtml_page51)

Firewalld [185](#ch06.xhtml_page185), [186](#ch06.xhtml_page186)

Firewalld, key tools

Firewalld Installation [187](#ch06.xhtml_page187)

immediate, changing [187](#ch06.xhtml_page187)

IP, blocking [187](#ch06.xhtml_page187)

service, managing [187](#ch06.xhtml_page187)

services, removing [187](#ch06.xhtml_page187)

Forrester [310](#ch10.xhtml_page310)

Forrester, key points [310](#ch10.xhtml_page310)

G

GCP, steps [226](#ch07.xhtml_page226)

Glassdoor [307](#ch10.xhtml_page307)

Glassdoor, strengths [307](#ch10.xhtml_page307)

Glassdoor, weakness [307](#ch10.xhtml_page307)

Google Cloud Platform (GCP) [226](#ch07.xhtml_page226)

Graphical User Interface (GUI) [34](#ch02.xhtml_page34)

Group [70](#ch03.xhtml_page70)

Group, use cases [70](#ch03.xhtml_page70), [71](#ch03.xhtml_page71)

GUID Partition Table (GPT) [41](#ch02.xhtml_page41)

H

High-Performance Computing (HPC) [317](#ch10.xhtml_page317)

HPC, aspects

CrowdStrike [318](#ch10.xhtml_page318)

Microsoft SQL [319](#ch10.xhtml_page319)

NGINX Plus [319](#ch10.xhtml_page319)

SAP HANA [319](#ch10.xhtml_page319)

HPC, challenges [317](#ch10.xhtml_page317)

HPC, features [318](#ch10.xhtml_page318)

I

IDC, benefits [311](#ch10.xhtml_page311)

IMA [227](#ch07.xhtml_page227)

IMA, key point

appraisal [229](#ch07.xhtml_page229)

measurement, enabling [228](#ch07.xhtml_page228)

remeasurement [229](#ch07.xhtml_page229)

Indeed [308](#ch10.xhtml_page308)

Indeed, strengths [308](#ch10.xhtml_page308)

Indeed, weakness [308](#ch10.xhtml_page308)

International Data Corporation (IDC) [311](#ch10.xhtml_page311)

Inventories [98](#ch04.xhtml_page98)

J

Jinja2 [148](#ch05.xhtml_page148)

Jinja2, features [150](#ch05.xhtml_page150)

Jinja2, practices [150](#ch05.xhtml_page150)

Jinja2, syntax [149](#ch05.xhtml_page149)

Jinja2, ways [149](#ch05.xhtml_page149)

Jooble [308](#ch10.xhtml_page308)

Jooble, strengths [308](#ch10.xhtml_page308)

Jooble, weaknesses [308](#ch10.xhtml_page308)

journalctl, steps [245](#ch08.xhtml_page245), [246](#ch08.xhtml_page246)

journald/rsyslog, interaction [247](#ch08.xhtml_page247), [248](#ch08.xhtml_page248)

K

Kernel Live Patch [214](#ch07.xhtml_page214)

Kernel Live Patch, benefits

downtime, minimizing [214](#ch07.xhtml_page214)

immediate, effect [214](#ch07.xhtml_page214)

security, enhancing [214](#ch07.xhtml_page214)

Kernel Live Patch, prerequisites [214](#ch07.xhtml_page214)

KIS, key components

EVM [228](#ch07.xhtml_page228)

IMA [227](#ch07.xhtml_page227)

L

Linting [168](#ch05.xhtml_page168)

Linting, tools

ansible-lint [168](#ch05.xhtml_page168)

ansible-playbook--syntax [168](#ch05.xhtml_page168)

spotter [168](#ch05.xhtml_page168)

yamllint [168](#ch05.xhtml_page168)

Linux [75](#ch03.xhtml_page75)

Linux, aspect

Sudo [39](#ch02.xhtml_page39)

Switch User [38](#ch02.xhtml_page38), [39](#ch02.xhtml_page39)

Linux, key points

file, managing [146](#ch05.xhtml_page146)

Jinja2 [148](#ch05.xhtml_page148)

Roll, updating [148](#ch05.xhtml_page148)

service, managing [147](#ch05.xhtml_page147)

user, managing [150](#ch05.xhtml_page150)-[152](#ch05.xhtml_page152)

Linux, process

Load Average [75](#ch03.xhtml_page75)

process, signals [77](#ch03.xhtml_page77)

Real-time, monitoring [76](#ch03.xhtml_page76)

Linux Storage, fundamentals

File System [84](#ch03.xhtml_page84)

Hard/Soft, link [85](#ch03.xhtml_page85)

Logical Volume Manager (LVM) [82](#ch03.xhtml_page82)

RAID Configurations [83](#ch03.xhtml_page83)

Swap [85](#ch03.xhtml_page85)

Linux System, setting up

Hostname [58](#ch03.xhtml_page58)

name, resolution [58](#ch03.xhtml_page58), [59](#ch03.xhtml_page59)

network, interfaces [59](#ch03.xhtml_page59)

Log Files [80](#ch03.xhtml_page80)

Log Files, key events [80](#ch03.xhtml_page80)

Logical Volume Manager (LVM) [82](#ch03.xhtml_page82)

Log Rotation [248](#ch08.xhtml_page248)

Log Rotation, key directives [249](#ch08.xhtml_page249)

LVM, key steps [82](#ch03.xhtml_page82)

M

Manage Local Users [66](#ch03.xhtml_page66)

Manage Local Users, directory

Group [70](#ch03.xhtml_page70)

Password [68](#ch03.xhtml_page68)

Shell Startup [68](#ch03.xhtml_page68)

Superuser [70](#ch03.xhtml_page70)

User Account [66](#ch03.xhtml_page66)

MD5 [199](#ch06.xhtml_page199)

Message-Digest Algorithm 5 (MD5) [199](#ch06.xhtml_page199)

Microsoft Azure [226](#ch07.xhtml_page226)

Microsoft Azure, steps [226](#ch07.xhtml_page226)

Modules [274](#ch09.xhtml_page274)

Modules, key points

archiving [282](#ch09.xhtml_page282)

file content [281](#ch09.xhtml_page281)

file systems [278](#ch09.xhtml_page278)

Firewall, rules [277](#ch09.xhtml_page277)

LVM [279](#ch09.xhtml_page279)

packages, repositories [275](#ch09.xhtml_page275), [276](#ch09.xhtml_page276)

service [277](#ch09.xhtml_page277)

storage [279](#ch09.xhtml_page279)

task, scheduling [283](#ch09.xhtml_page283)

user, group [284](#ch09.xhtml_page284)

Molecule [168](#ch05.xhtml_page168), [259](#ch08.xhtml_page259)

Molecule, steps [169](#ch05.xhtml_page169), [170](#ch05.xhtml_page170)

Molecule, workflow [168](#ch05.xhtml_page168)

myservice.te, best practices

disaster, recovery [198](#ch06.xhtml_page198)

least, privilege [197](#ch06.xhtml_page197)

mechanisms, authentication [197](#ch06.xhtml_page197)

regular audit, monitoring [198](#ch06.xhtml_page198)

regular, updating [197](#ch06.xhtml_page197)

secure, configuration [197](#ch06.xhtml_page197)

myservice.te, components

allow [196](#ch06.xhtml_page196)

class [196](#ch06.xhtml_page196)

http_port_t [196](#ch06.xhtml_page196)

module [196](#ch06.xhtml_page196)

myservice_t [196](#ch06.xhtml_page196)

myservice_var_t [196](#ch06.xhtml_page196)

require [196](#ch06.xhtml_page196)

type_transition [196](#ch06.xhtml_page196)

myservice.te, steps [196](#ch06.xhtml_page196), [197](#ch06.xhtml_page197)

N

Network File System (NFS) [86](#ch03.xhtml_page86)

Network Troubleshoot, tools [251](#ch08.xhtml_page251), [252](#ch08.xhtml_page252)

NFS, version

Automounting [87](#ch03.xhtml_page87), [88](#ch03.xhtml_page88)

Direct Maps [88](#ch03.xhtml_page88)

Indirect Maps [88](#ch03.xhtml_page88)

Mounting [87](#ch03.xhtml_page87)

nmcli [59](#ch03.xhtml_page59)

nmcli, key commands [60](#ch03.xhtml_page60), [61](#ch03.xhtml_page61)

O

OpenSSH [187](#ch06.xhtml_page187)

OpenSSH, breakdown [188](#ch06.xhtml_page188)-[190](#ch06.xhtml_page190)

OSP, process

kill command [255](#ch08.xhtml_page255)

nice command [256](#ch08.xhtml_page256)

ps command [255](#ch08.xhtml_page255)

signals [254](#ch08.xhtml_page254)

signals, managing [254](#ch08.xhtml_page254)

P

Playbooks, roles

defaults [157](#ch05.xhtml_page157)

files [157](#ch05.xhtml_page157)

handlers [157](#ch05.xhtml_page157)

meta [157](#ch05.xhtml_page157)

tasks [157](#ch05.xhtml_page157)

templates [157](#ch05.xhtml_page157)

tests [157](#ch05.xhtml_page157)

vars [157](#ch05.xhtml_page157)

Playbooks Roles, facilitates

ability, optimizing [157](#ch05.xhtml_page157)

hosts, instance [159](#ch05.xhtml_page159)

role, using [157](#ch05.xhtml_page157)

system roles, automation [159](#ch05.xhtml_page159)

tasks, working [158](#ch05.xhtml_page158)

Podman [200](#ch06.xhtml_page200)-[203](#ch06.xhtml_page203)

Power Management [33](#ch02.xhtml_page33)

Privilege Escalation [141](#ch05.xhtml_page141)

Privilege Escalation, importance [142](#ch05.xhtml_page142)

Privilege Escalation, parts

Horizontal [142](#ch05.xhtml_page142)

Vertical [142](#ch05.xhtml_page142)

Privilege Escalation, practices

audit, monitoring [143](#ch05.xhtml_page143)

authentication, mechanisms [143](#ch05.xhtml_page143)

least, privilege [143](#ch05.xhtml_page143)

regular update, patching [143](#ch05.xhtml_page143)

secure credential, managing [143](#ch05.xhtml_page143)

Privilege Escalation, ways [142](#ch05.xhtml_page142)

R

RAID Configurations [83](#ch03.xhtml_page83)

RAID Configurations, steps [83](#ch03.xhtml_page83), [84](#ch03.xhtml_page84)

Red Hat, technologies [17](#ch01.xhtml_page17), [18](#ch01.xhtml_page18)

RHCA [12](#ch01.xhtml_page12), [306](#ch10.xhtml_page306)

RHCA, configuring [309](#ch10.xhtml_page309)

RHCA, directories

Glassdoor [307](#ch10.xhtml_page307)

Indeed [308](#ch10.xhtml_page308)

Jooble [308](#ch10.xhtml_page308)

RHCE [9](#ch01.xhtml_page9), [10](#ch01.xhtml_page10)

RHCE Certification, architectures [3](#ch01.xhtml_page3)-[5](#ch01.xhtml_page5)

RHCE Certification, steps [9](#ch01.xhtml_page9)

RHCE Exam [12](#ch01.xhtml_page12)-[15](#ch01.xhtml_page15)

RHCE Exam, key areas [266](#ch09.xhtml_page266)

RHCE Exam, key details [14](#ch01.xhtml_page14)

RHCE Exam, key points

Practical Skills [12](#ch01.xhtml_page12)

Theoretical Concepts [12](#ch01.xhtml_page12)

RHCE Exam, requirements

Adapters [15](#ch01.xhtml_page15)

Computer [15](#ch01.xhtml_page15)

Food/Snacks [15](#ch01.xhtml_page15)

internet, speed [15](#ch01.xhtml_page15)

Keyboard [15](#ch01.xhtml_page15)

Power [15](#ch01.xhtml_page15)

RAM [15](#ch01.xhtml_page15)

Sound/Microphone [15](#ch01.xhtml_page15)

USB Drive [15](#ch01.xhtml_page15)

Webcam [15](#ch01.xhtml_page15)

RHCE Exam, strategies

documentation, resources [267](#ch09.xhtml_page267)

hands-on [267](#ch09.xhtml_page267)

join learn, communities [267](#ch09.xhtml_page267)

mock, exams [267](#ch09.xhtml_page267)

real-world, scenarios [267](#ch09.xhtml_page267)

reinforce [267](#ch09.xhtml_page267)

structure learning [267](#ch09.xhtml_page267)

RHCE Exam, tips [15](#ch01.xhtml_page15), [16](#ch01.xhtml_page16)

RHCE, history [2](#ch01.xhtml_page2)

RHCE, industry trends

Develop Proficiency [302](#ch10.xhtml_page302)

employer, expectation [303](#ch10.xhtml_page303)

professional network, building [303](#ch10.xhtml_page303)

Roadmap, developing [302](#ch10.xhtml_page302)

showcase, skills [303](#ch10.xhtml_page303)

webinars, resources [303](#ch10.xhtml_page303)

RHCE, program

DevOps/OpenShift [11](#ch01.xhtml_page11)

Linux Mastery [11](#ch01.xhtml_page11)

open hybrid cloud [10](#ch01.xhtml_page10)

Telco Cloud [11](#ch01.xhtml_page11)

RHCSA [6](#ch01.xhtml_page6)-[8](#ch01.xhtml_page8)

RHEL [22](#ch02.xhtml_page22)

RHEL AI [321](#ch10.xhtml_page321)

RHEL AI, components [321](#ch10.xhtml_page321)

RHEL AI, methodologies [322](#ch10.xhtml_page322)

RHEL, approaches

CDN Method [26](#ch02.xhtml_page26)

Cloud Image Installation [26](#ch02.xhtml_page26)

ISO Installation [26](#ch02.xhtml_page26)

Kickstart, streamlines [26](#ch02.xhtml_page26)

PXE [26](#ch02.xhtml_page26)

VNC [26](#ch02.xhtml_page26)

RHEL, benefits [23](#ch02.xhtml_page23), [24](#ch02.xhtml_page24)

RHEL, categories

Anaconda [27](#ch02.xhtml_page27)

Subscription Manager [30](#ch02.xhtml_page30)

RHEL, directories

device, configuring [40](#ch02.xhtml_page40)

manual mount [42](#ch02.xhtml_page42)

persistent mount [43](#ch02.xhtml_page43)

RHEL, fundamentals

Red Hat Developer [37](#ch02.xhtml_page37)

Red Hat Insights [38](#ch02.xhtml_page38)

Red Hat Support Tool [36](#ch02.xhtml_page36)

RHEL, insights

Compute Server [313](#ch10.xhtml_page313)

Directory Server [316](#ch10.xhtml_page316)

File Server [315](#ch10.xhtml_page315)

Mail Server [314](#ch10.xhtml_page314)

Webserver [312](#ch10.xhtml_page312)

RHEL Interfaces, setting up [49](#ch02.xhtml_page49), [50](#ch02.xhtml_page50)

RHEL IT, operations

Bash Scripts [35](#ch02.xhtml_page35), [36](#ch02.xhtml_page36)

Command Line [31](#ch02.xhtml_page31), [32](#ch02.xhtml_page32)

Graphical User Interface (GUI) [34](#ch02.xhtml_page34)

Login [30](#ch02.xhtml_page30), [31](#ch02.xhtml_page31)

Logout [32](#ch02.xhtml_page32)

Reboot [33](#ch02.xhtml_page33)

Shutdown [32](#ch02.xhtml_page32)

Suspension/Hibernation [33](#ch02.xhtml_page33), [34](#ch02.xhtml_page34)

RHEL, navigation

SSH Key, authentication [48](#ch02.xhtml_page48), [49](#ch02.xhtml_page49)

SSH Network, login [47](#ch02.xhtml_page47), [48](#ch02.xhtml_page48)

Web Console [46](#ch02.xhtml_page46)

RHEL, phases life cycle

life plase, extending [23](#ch02.xhtml_page23)

phase, maintenance [23](#ch02.xhtml_page23)

phase, supporting [23](#ch02.xhtml_page23)

RHEL, roles

Log [45](#ch02.xhtml_page45)

software, activities [43](#ch02.xhtml_page43), [44](#ch02.xhtml_page44)

updating [44](#ch02.xhtml_page44)

RHEL Security, key areas

backup, recovery [184](#ch06.xhtml_page184)

File System, security [183](#ch06.xhtml_page183)

logs, monitoring [184](#ch06.xhtml_page184)

Network, security [183](#ch06.xhtml_page183)

SELinux Management [183](#ch06.xhtml_page183)

Software Package, security [184](#ch06.xhtml_page184)

system patches, updating [184](#ch06.xhtml_page184)

User Group, managing [182](#ch06.xhtml_page182)

RHEL System, roles

Red Hat, developing [159](#ch05.xhtml_page159)

scalability [160](#ch05.xhtml_page160)

simplified, managing [159](#ch05.xhtml_page159)

standardization, consistency [159](#ch05.xhtml_page159)

RHEL System, setup

ad hoc [272](#ch09.xhtml_page272)

configuration [271](#ch09.xhtml_page271)

installation [268](#ch09.xhtml_page268)

inventory [269](#ch09.xhtml_page269)

Playbook [273](#ch09.xhtml_page273)

RHET, key areas

AI/ML [209](#ch07.xhtml_page209)

Ansible, automation [208](#ch07.xhtml_page208)

cloud/hybrid [208](#ch07.xhtml_page208)

edge, computing [209](#ch07.xhtml_page209)

Kubernetes, containerization [208](#ch07.xhtml_page208)

security, compliance [209](#ch07.xhtml_page209)

Root Password [236](#ch08.xhtml_page236)

Root Password, steps [236](#ch08.xhtml_page236), [237](#ch08.xhtml_page237)

RPM, drawback

Kubernetes/OpenShift [223](#ch07.xhtml_page223)

Podman [221](#ch07.xhtml_page221)

Rootless Containers [223](#ch07.xhtml_page223)

rsyslog, steps [247](#ch08.xhtml_page247)

S

Schedule Future Tasks [62](#ch03.xhtml_page62)

Schedule Future Tasks, utility

Anacron [65](#ch03.xhtml_page65)

crontab [62](#ch03.xhtml_page62)

Systemd Timer [65](#ch03.xhtml_page65)

Secure Sockets Layer (SSL) [198](#ch06.xhtml_page198)

SELinux [190](#ch06.xhtml_page190), [191](#ch06.xhtml_page191)

SELinux, fundamentals

Ansible [192](#ch06.xhtml_page192)

Boolean [194](#ch06.xhtml_page194), [195](#ch06.xhtml_page195)

context, directories [191](#ch06.xhtml_page191), [192](#ch06.xhtml_page192)

custom, policies [195](#ch06.xhtml_page195)

file context, configuring [192](#ch06.xhtml_page192)

Server Message Block (SMB) [86](#ch03.xhtml_page86)

Service Failure [249](#ch08.xhtml_page249)

Service Failure, strategies

Apache [249](#ch08.xhtml_page249)

Network Troubleshoot [250](#ch08.xhtml_page250), [251](#ch08.xhtml_page251)

SSH [250](#ch08.xhtml_page250)

SHA-1 [199](#ch06.xhtml_page199)

SHA-1, key areas

code, signing [199](#ch06.xhtml_page199)

data, integrity [199](#ch06.xhtml_page199)

digital, certificates [199](#ch06.xhtml_page199)

SHA-1, vulnerabilities [199](#ch06.xhtml_page199)

SMB, steps [86](#ch03.xhtml_page86)

SSSD [218](#ch07.xhtml_page218)

SSSD, best practices [220](#ch07.xhtml_page220)

SSSD, configuring [220](#ch07.xhtml_page220)

SSSD, fundamentals

authentication/authorization [219](#ch07.xhtml_page219)

backend, connection [219](#ch07.xhtml_page219)

caching [219](#ch07.xhtml_page219)

initialization [219](#ch07.xhtml_page219)

service, activation [219](#ch07.xhtml_page219)

SSSD, key features

identity providers [219](#ch07.xhtml_page219)

offline, supporting [219](#ch07.xhtml_page219)

security, enhancing [219](#ch07.xhtml_page219)

single sign-on capabilities [219](#ch07.xhtml_page219)

syslog [244](#ch08.xhtml_page244)

syslog, configuring [244](#ch08.xhtml_page244), [245](#ch08.xhtml_page245)

syslog, key points [244](#ch08.xhtml_page244)

systemd [241](#ch08.xhtml_page241)

systemd, concepts [241](#ch08.xhtml_page241)

T

tcpdump [180](#ch06.xhtml_page180)

Template [284](#ch09.xhtml_page284)

Template, aspects

Apache [286](#ch09.xhtml_page286)

fail package [295](#ch09.xhtml_page295)

MOTD [285](#ch09.xhtml_page285)

Playbook [285](#ch09.xhtml_page285)

Role [287](#ch09.xhtml_page287)

security [293](#ch09.xhtml_page293)

SELinux [288](#ch09.xhtml_page288)

Vault [291](#ch09.xhtml_page291)

Text-based Interface [145](#ch05.xhtml_page145)

Text-based Interface, features

color, command [145](#ch05.xhtml_page145)

navigation [146](#ch05.xhtml_page146)

Time Management [267](#ch09.xhtml_page267)

Time Management, techniques [267](#ch09.xhtml_page267)

Timestamps [61](#ch03.xhtml_page61)

Timestamps, guide [61](#ch03.xhtml_page61), [62](#ch03.xhtml_page62)

Timestamps, notes

Chrony/NTPD [62](#ch03.xhtml_page62)

Local Time, setting up [62](#ch03.xhtml_page62)

Persistent Configuration [62](#ch03.xhtml_page62)

UTC Time Zone [62](#ch03.xhtml_page62)

Troubleshooting [238](#ch08.xhtml_page238)

Troubleshooting, commands [242](#ch08.xhtml_page242)

Troubleshooting, strategies

File System [238](#ch08.xhtml_page238), [239](#ch08.xhtml_page239)

journalctl [245](#ch08.xhtml_page245)

Log Files [241](#ch08.xhtml_page241)

Log Rotation [248](#ch08.xhtml_page248)

relevant, entries [243](#ch08.xhtml_page243)

rsyslog [246](#ch08.xhtml_page246)

syslog [244](#ch08.xhtml_page244)

systemd [241](#ch08.xhtml_page241)

unit files, configuring [243](#ch08.xhtml_page243)

Virtual Data Optimizer (VDO) [240](#ch08.xhtml_page240)

tuned service [209](#ch07.xhtml_page209)

tuned service, aspects

active profile [210](#ch07.xhtml_page210)

list [210](#ch07.xhtml_page210)

parameter, using [210](#ch07.xhtml_page210)

recommend, system [211](#ch07.xhtml_page211)

web console [211](#ch07.xhtml_page211)

U

UBI Image [223](#ch07.xhtml_page223)

UBI Image, key features

broad compatibility [224](#ch07.xhtml_page224)

no subscription [224](#ch07.xhtml_page224)

standardization [224](#ch07.xhtml_page224)

UBI Image/RHEL, comparing [224](#ch07.xhtml_page224)

UBI Image, types

micro [224](#ch07.xhtml_page224)

minimal [224](#ch07.xhtml_page224)

standard [224](#ch07.xhtml_page224)

UBI Image, use cases

CI/CD, pipelines [225](#ch07.xhtml_page225)

cloud-native, applications [225](#ch07.xhtml_page225)

ISV Software [225](#ch07.xhtml_page225)

User Account [66](#ch03.xhtml_page66)

User Account, commands [67](#ch03.xhtml_page67), [68](#ch03.xhtml_page68)

User Account, types

Regular Users UID [66](#ch03.xhtml_page66)

Superuser [66](#ch03.xhtml_page66)

System Users UID [66](#ch03.xhtml_page66)

V

VDO, best practices [218](#ch07.xhtml_page218)

VDO, configuring [240](#ch08.xhtml_page240)

VDO, installation [240](#ch08.xhtml_page240)

VDO, key features

data, compression [217](#ch07.xhtml_page217)

data, deduplication [217](#ch07.xhtml_page217)

thin, provisioning [217](#ch07.xhtml_page217)

VDO, monitoring [241](#ch08.xhtml_page241)

VDO, setting up [217](#ch07.xhtml_page217)

VDO, steps [217](#ch07.xhtml_page217), [218](#ch07.xhtml_page218)

Virtual Data Optimizer (VDO) [216](#ch07.xhtml_page216)

VMware [227](#ch07.xhtml_page227)

VMware, steps [227](#ch07.xhtml_page227)