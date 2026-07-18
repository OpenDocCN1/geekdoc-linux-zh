![](images/cover.jpg)

![image](images/cover.jpg)

# Mastering IBM CMOD
for RedHat Linux and
Windows 11 Servers

![](images/line.jpg)

# Effortlessly Streamline Your Content
Management by Deploying IBM CMOD With
IBM Content Navigator and Filenet Fixed
Content Device for Red Hat Linux and
Windows Platforms

![](images/line.jpg)

# Alan S. Bluck

![](images/logo.jpg)

[www.orangeava.com](http://www.orangeava.com)

Copyright © 2024 Orange Education Pvt Ltd, AVA™

All rights reserved. No part of this book may be reproduced, stored in a retrieval system, or transmitted in any form or by any means, without the prior written permission of the publisher, except in the case of brief quotations embedded in critical articles or reviews.

Every effort has been made in the preparation of this book to ensure the accuracy of the information presented. However, the information contained in this book is sold without warranty, either express or implied. Neither the author nor **Orange Education Pvt Ltd** or its dealers and distributors, will be held liable for any damages caused or alleged to have been caused directly or indirectly by this book.

**Orange Education Pvt Ltd** has endeavored to provide trademark information about all of the companies and products mentioned in this book by the appropriate use of capital. However, **Orange Education Pvt Ltd** cannot guarantee the accuracy of this information. The use of general descriptive names, registered names, trademarks, service marks, etc. in this publication does not imply, even in the absence of a specific statement, that such names are exempt from the relevant protective laws and regulations and therefore free for general use.

**First Published:** October 2024

**Published by:** Orange Education Pvt Ltd, AVA™

**Address:** 9, Daryaganj, Delhi, 110002, India

275 New North Road Islington Suite 1314 London,

N1 7AA, United Kingdom

**ISBN (PBK):** 978-81-97953-44-6

**ISBN (E-BOOK):** 978-81-97953-46-0

**Scan the QR code to explore our entire catalogue**

![](images/cqr.jpg)

[www.orangeava.com](http://www.orangeava.com)

# Dedicated To

*My Beloved Wife, Jenny*

*My Children, Julie and Rosalie*

*and*

*Their Families*

# About the Author

**Alan S. Bluck** is the Director of ASB Software Development Limited and also provides consultancy as a systems architect. He offers a broad range of services, from high-level technical design to mentoring for code development and installation and configuration of IBM FileNet’s core products. He is also a member of the Association of Computing Machinery (ACM), the British Computer Society (MBCS), an IBM Silver Level PartnerWorld Business Partner, and a RedHat Accredited Business Partner.

Nominated as an IBM Champion in 2022 and re-elected in 2023 and 2024, Alan has published six technical books and 40 ResearchGate papers, all available for free download.

He is responsible for high-level analysis and configuration of both existing and new IBM FileNet systems, mentoring and troubleshooting high-level systems and issues, and ensuring that scheduled timelines are maintained and deadlines are met.

With over 45 years of software development experience in both business and scientific systems, Alan has 5 years of experience as a Project Manager/Analyst Developer, 11 years as a Software Development Manager for a team of 12 software engineers, 11 years as a Technical Consultant, and 20 years as a Solutions Architect.

# About the Technical Reviewer

**Gil Metcalf** has had a long and varied career, initially qualifying as an industrial microbiologist, working for an oil company on projects relating to microbial mining of heavy metals as well as enhanced oil recovery from spent wells.

After working as an industrial microbiologist, Gil spent several years at a major pharmaceutical company, where he held roles such as project manager, development team leader, and network administrator. During this time, he developed software for clinical trials management and hospital tools for cancer patient care.

As a solutions architect, Gil has gained extensive experience across financial technologies, manufacturing, logistics, and energy sectors. His expertise covers document management, case management, business process automation, identity management, and online banking technologies.

Renowned in the industry, Gil has collaborated with leading banks and institutions, solving complex challenges with innovative solutions. For the past 10 years, he has focused on fintech, designing and implementing solutions for blue-chip enterprises. He holds multiple qualifications in document management, business automation, and identity management, recently specializing in profile management and passwordless authentication for mobile banking.

Gil believes that successful software architecture requires both technical expertise and strong soft skills, including explaining complex concepts to non-technical audiences, understanding the big picture, and refining vague requirements.

He says that preparing for solution design is often *“an exercise in extrapolation and interpolation at the same time!”.*

He is a member of several professional associations, including the Chartered Institute for IT, the Identity Management Institute, and the International Association for Software Architects.

# Acknowledgements

There are a few people I want to thank for their continued and ongoing support while I wrote this book. First and foremost, I would like to thank my wife, Jenny, for continuously encouraging me to write the book — I could never have completed this book without her support.

I would also like to thank my son-in-law, Dr. Chris Howles, for his advice and encouragement.

I am grateful for the support of the ResearchGate website, which has hosted over 30 of my free publications since 2019, many of which are referenced in this book.

I extend my gratitude to the team at AVA Orange for their support and dedication, allowing me to publish this book in such a short time and update the material during the production process as well as for their invaluable advice.

Lastly, I would like to thank Gil Metcalf, the technical reviewer of this book, for his diligence and helpful suggestions.

# Preface

This book provides ab initio step-by-step instructions for the installation and configuration of IBM Content Manager OnDemand (IBM CMOD) version 10.5.0.7.

The configuration covers the integration of IBM Content Manager OnDemand with IBM Content Navigator and IBM FileNet Content Engine. IBM CMOD is the leading data archiving and retrieval system on the global market.

Additionally, the book includes working examples of the Java API using the ODApi.jar and covers the OnDemand Web Enablement Kit (ODWEK) installation for web development.

The book also describes the Windows Client IBM CMOD installation and details the search and download of Base and Fix Pack from IBM’s Software Catalog and Fix Central websites using IBM Download Director software.

This book is divided into 14 chapters and includes 4 appendices. It is designed for Java programmers, IT consultants, and systems and solution architects, with basic IT knowledge. The book provides step-by-step instructions for downloading, installing, and configuring IBM Content Manager OnDemand (CMOD) version 10.5.0.7 as well as the configuration required for integrating IBM Content Manager OnDemand with IBM Content Navigator and IBM FileNet Content Engine. This is useful for developers and installers involved in document management, as well as for implementation in manufacturing industries, banks, and insurance companies.

**[Chapter 1](#c01.xhtml)** covers the purpose and supported platforms of the IBM Content Manager OnDemand software. It describes the available functions and outlines the prerequisites for its integration with IBM FileNet Content Engine and IBM Content Navigator.

**[Chapter 2](#c02.xhtml)** covers the step-by-step download, installation, and configuration of IBM Content Manager OnDemand version 10.5, including the Base and Fix Pack 10.5.0.7 upgrade on a RedHat Linux version 8.8 server running on a VMware virtual system.

**[Chapter 3](#c03.xhtml)** covers the installation and administration of the supporting optional software components, including the Db2 databases, the PDF Indexing feature, the Distribution Facility feature, and the Full Text Search server feature.

**[Chapter 4](#c04.xhtml)** covers the IBM Fix Pack upgrade RPM files and some additional Linux operating system library packages that are required to be installed to support the GSKit for CMOD version 10.5.0.7\. This chapter describes their installation and the process of debugging the main arssockd program load and run.

**[Chapter 5](#c05.xhtml)** provides step-by-step for downloading, installing, and configuring IBM Content Manager OnDemand version 10.5, including the Base and Fix Pack 10.5.0.7 upgrade on a Windows 11 server, as well as some configuration on the connected Linux server.

**[Chapter 6](#c06.xhtml)** covers the restart of the Linux system server after the upgrade and configuration, including the supporting application systems: the IBM Directory Services (LDAP server), the IBM Db2 (database server), the IBM WebSphere (web application server for IBM FileNet P8 Content Engine), and the IBM Content Navigator (desktop client).

**[Chapter 7](#c07.xhtml)** describes the OnDemand Configurator program V10.5, the OnDemand Client configuration program, the use of the arsxml command on Windows, and the configuration of the system after installing IBM CMOD Fix Pack 10.5.0.7.

**[Chapter 8](#c08.xhtml)** covers the Object Type model and the Object Owner model for decentralizing system administration users, as well as resetting an expired or lost IBM CMOD admin user password on the Linux Db2 server. It also describes the use of the arsstash program for storing encrypted passwords for users.

**[Chapter 9](#c09.xhtml)** lists several example Java programs updated to work with the IBM CMOD OnDemand API and demonstrated running in an Eclipse IDE environment on a Linux server.

**[Chapter 10](#c10.xhtml)** outlines the procedure for creating a repository for the Linux server version of IBM Content Navigator and demonstrates the browse access to the folders on a Windows CMOD server from the Content Navigator desktop created for CMOD.

**[Chapter 11](#c11.xhtml)** describes the network requirements to be checked to successfully run the arssockd program on a Linux server, including the command parameters to use for running and debugging the program. It also covers the use of the IBM OnDemand Full Text Search service, which utilizes the open-source Apache Lucene system, and provides a detailed use of the arsdb database configuration and maintenance program. Additionally, it covers the step-by-step procedure for creating a second Linux IBM CMOD instance, ARCHIVE2.

**[Chapter 12](#c12.xhtml)** covers the purpose and supported platforms of the IBM Content Manager OnDemand arsload software and describes the available functions and prerequisites, including the creation of the System Log and System Load database tables using the arssyscr program. Additionally, it outlines the use of the ARSXML Windows program and the Linux arsxml program to import and export the IBM CMOD Application Groups from XML files and perform XML file validation.

**[Chapter 13](#c13.xhtml)** covers examples of running the ARSLOAD program in both Windows and Linux environments. It describes the Index Fields required for loading documents and explains the use of the ARSSOCKD program to display the list of IBM CMOD program services running on the Windows system. Finally, it covers the use of the arsdoc program to generate the Generic Index Field file used by ARSLOAD.

**[Chapter 14](#c14.xhtml)** demonstrates how to process an AFP input file located in a directory and redirect the line data output to a file using the IBM Content Manager OnDemand ARSXAFP program in both Windows and Linux server environments.

**[Appendix A](#appa.xhtml)** covers the download, extraction, and installation of Windows Fix Pack 7 for IBM Content Manager OnDemand, as well as the running of the Windows IBM Configurator program.

**[Appendix B](#appb.xhtml)** describes the step-by-step procedure required to remove and re-add an IBM CMOD application group.

**[Appendix C](#appc.xhtml)** lists each of the CMOD configuration files and environment settings for the Windows client, Windows server, and Linux server.

**[Appendix D](#appd.xhtml)** lists the supporting documentation provided by ResearchGate and other book publications, along with contact details for supporting IBM CMOD integration, developed by ASB Software Development Limited.

# Downloading the code
bundles and colored images

Please follow the link or scan the QR code to download the
***Code Bundles and Images*** of the book:

# [https://github.com/ava-orange-education/Mastering-IBM-CMOD-for-RedHat-Linux-and-Windows-11-Servers](https://github.com/ava-orange-education/Mastering-IBM-CMOD-for-RedHat-Linux-and-Windows-11-Servers)

![](images/qr.jpg)

The code bundles and images of the book are also hosted on
**[*https://rebrand.ly/f69543*](https://rebrand.ly/f69543)**

![](images/qr1.jpg)

In case there’s an update to the code, it will be updated on the existing GitHub repository.

# Errata

We take immense pride in our work at **Orange Education Pvt Ltd** and follow best practices to ensure the accuracy of our content to provide an indulging reading experience to our subscribers. Our readers are our mirrors, and we use their inputs to reflect and improve upon human errors, if any, that may have occurred during the publishing processes involved. To let us maintain the quality and help us reach out to any readers who might be having difficulties due to any unforeseen errors, please write to us at :

**[errata@orangeava.com](mailto:errata@orangeava.com)**

Your support, suggestions, and feedback are highly appreciated.

# DID YOU KNOW

Did you know that Orange Education Pvt Ltd offers eBook versions of every book published, with PDF and ePub files available? You can upgrade to the eBook version at [**www.orangeava.com**](http://www.orangeava.com) and as a print book customer, you are entitled to a discount on the eBook copy. Get in touch with us at: **[info@orangeava.com](mailto:info@orangeava.com)** for more details.

At **[www.orangeava.com](http://www.orangeava.com)**, you can also read a collection of free technical articles, sign up for a range of free newsletters, and receive exclusive discounts and offers on AVA™ Books and eBooks.

# PIRACY

If you come across any illegal copies of our works in any form on the internet, we would be grateful if you would provide us with the location address or website name. Please contact us at **[info@orangeava.com](mailto:info@orangeava.com)** with a link to the material.

# ARE YOU INTERESTED IN AUTHORING WITH US?

If there is a topic that you have expertise in, and you are interested in either writing or contributing to a book, please write to us at [**business@orangeava.com**](mailto:business@orangeava.com). We are on a journey to help developers and tech professionals to gain insights on the present technological advancements and innovations happening across the globe and build a community that believes Knowledge is best acquired by sharing and learning with others. Please reach out to us to learn what our audience demands and how you can be part of this educational reform. We also welcome ideas from tech experts and help them build learning and development content for their domains.

# REVIEWS

Please leave a review. Once you have read and used this book, why not leave a review on the site that you purchased it from? Potential readers can then see and use your unbiased opinion to make purchase decisions. We at Orange Education would love to know what you think about our products, and our authors can learn from your feedback. Thank you!

For more information about Orange Education, please visit **[www.orangeava.com](http://www.orangeava.com)**.

# [CHAPTER 1](#toc.xhtml_c01)

# [Introduction to IBM Content Manager OnDemand](#toc.xhtml_c01)

# [Introduction](#toc.xhtml_s1a)

This book provides ab initio step-by-step instructions for the installation and configuration of **IBM Content Manager OnDemand** (**CMOD**) version **10.5.0.7**.

The configuration covers the integration of **IBM Content Manager OnDemand** with **IBM Content Navigator** and **IBM FileNet Content Engine**. **CMOD** is the leading data archiving and retrieval system on the world market.

The book also provides working examples of the Java **API** using the **ODApi.jar**, and it covers the **OnDemand Web Enablement Kit** (**ODWEK**) installation for web development.

Additionally, the Windows Client **CMOD** installation is described, along with the process of searching and downloading the Base and Fix Pack from IBM’s Software Catalog and **Fix Central** websites using **IBM Download Director** software.

IBM describes the purpose of **CMOD** in detail, which can be accessed through this link:

[https://www.ibm.com/support/pages/system/files/support/swg/swgdocs.nsf/0/eeee7450f3eb8e6385257b6e0047cef4/$FILE/IBM%20Content%20Manager%20OnDemand%20Best%20Practices_033015v2.pdf](https://www.ibm.com/support/pages/system/files/support/swg/swgdocs.nsf/0/eeee7450f3eb8e6385257b6e0047cef4/$FILE/IBM%20Content%20Manager%20OnDemand%20Best%20Practices_033015v2.pdf)

This introduces the **IBM Content Manager OnDemand** (**CMOD**) system as follows:

“*IBM® Content Manager OnDemand (****CMOD****) is the premier data archiving and retrieval system on the global market.* ***CMOD*** *is installed at thousands of customer locations worldwide serving a user base in the millions of users on a daily basis. The* ***CMOD*** *product is extremely scalable and flexible, allowing customers to create customized solutions that best meet their requirements.* ***CMOD*** *provides extremely high performance for loading, retrieving, and expiring of data*.”

In this chapter, we cover the purpose and supported platforms of the **IBM Content Manager OnDemand** software and describe the available functions supplied. The chapter outlines the prerequisites for **CMOD**s integration with **IBM FileNet Content Engine** and **IBM Content Navigator**.

# [Structure](#toc.xhtml_s2a)

In this chapter, we will discuss the following topics:

*   Links from IBM and the **CMOD** Blog Website
*   Hardware and Software Requirements
*   Operating System Environment Variable Settings
*   Required Extensions for **IBM FileNet** Add-on
    *   Setting Up on the Windows Server for **`CFS-CMOD`**
    *   Creating a Custom Document Class in the **Linux, IBM FileNet P8** Content Engine

# [Links from IBM and the CMOD Blog Website](#toc.xhtml_s3a)

The following ResearchGate free download links can be followed to install the supporting software systems for the base system platform for **IBM Content Manager OnDemand**:

1.  For the user security LDAP server, **IBM Security Directory Services 6.4**: Installation on **RHEL 8.0:**

    [https://doi.org/10.13140/RG.2.2.33527.57761](https://doi.org/10.13140/RG.2.2.33527.57761)

2.  For the installation of the IBM Database**, Db2 10.5** Installation on **RHEL 8.0 V1:**

    [https://doi.org/10.13140/RG.2.2.10491.67369](https://doi.org/10.13140/RG.2.2.10491.67369)

3.  Upgrade of IBM FileNet systems from **DB2 10.5 FP 10** to the latest **DB2 11.5** version on RedHat **RHEL 8.0:**

    [https://doi.org/10.13140/RG.2.2.29470.69441](https://doi.org/10.13140/RG.2.2.29470.69441)

4.  For the Web Application server, **IBM WebSphere 8.5.5.15** Installation on **VMWare Workstation Pro 15.1:**

    [https://doi.org/10.13140/RG.2.2.15007.10408](https://doi.org/10.13140/RG.2.2.15007.10408)

5.  For the **CMOD** Desktop, **IBM Content Navigator 3.0.6** Installation on **RHEL 8.0:**

    [https://doi.org/10.13140/RG.2.2.14590.95049](https://doi.org/10.13140/RG.2.2.14590.95049)

6.  For the **IBM FileNet Fixed Content Device**, **IBM Content Foundation 5.5.3** Installation on **RHEL 8.0:**

    [https://doi.org/10.13140/RG.2.2.21170.76480](https://doi.org/10.13140/RG.2.2.21170.76480)

7.  For initial **CMOD** example configurations, see:

    [https://www.redbooks.ibm.com/redbooks/pdfs/sg246915.pdf](https://www.redbooks.ibm.com/redbooks/pdfs/sg246915.pdf)

For a General Knowledge base, see:

[https://cmod.wiki/](https://cmod.wiki/)

“***CMOD.wiki*** *is a source of information and guidance for users and Administrators of IBM’s Content Manager OnDemand product, also known as IBM* ***CMOD****, or simply OnDemand.*”

“*IBM* ***CMOD*** *10.5 was released in March 2020, and will likely be supported until 2025\. For IBM Content Manager OnDemand Fix Packs, see Security Bulletins & Updates.*”

Additionally, download the PDF from IBM support, as described at:

[https://www.ibm.com/support/pages/content-manager-ondemand-best-practices-guide](https://www.ibm.com/support/pages/content-manager-ondemand-best-practices-guide)

The **CMOD** product line, developed from early releases in the mid-1980s, is installed at thousands of customer locations worldwide, connecting with millions of users every day. The following link provides some idea of the current market interest:

[https://discovery.hgdata.com/product/ibm-content-manager-ondemand](https://discovery.hgdata.com/product/ibm-content-manager-ondemand)

The following links also provide references to the IBM CMOD system:

*   **GitHub Activity:** [https://github.com/francisoud/cmod-migration](https://github.com/francisoud/cmod-migration)
*   **Stack Overflow Activity:** [https://stackoverflow.com/search?q=%5Bondemand%5DCMOD&s=f17a62f1-e2e6-4b56-9fe0-340f4e7f49c3](https://stackoverflow.com/search?q=%5Bondemand%5DCMOD&s=f17a62f1-e2e6-4b56-9fe0-340f4e7f49c3)
*   **YouTube links:** [https://www.youtube.com/watch?v=c9qy-Vw7pFo](https://www.youtube.com/watch?v=c9qy-Vw7pFo)

    [https://youtu.be/vVY2luUSlrg](https://youtu.be/vVY2luUSlrg)

*   **Google Trends:** [https://6sense.com/tech/archiving/ibm-content-manager-ondemand-market-share](https://6sense.com/tech/archiving/ibm-content-manager-ondemand-market-share)

User PDF document downloads are listed in the following *[Table 1.1](#c01.xhtml_tab1_1)*:

| **ISBN/IBM** | **Title** | **Publisher(s)** | **Date** |
| ISBN:9780738440958 | IBM Content Manager OnDemand Guide | **O’Reilly** | **October 2015** |
| **SC19-3358-03** | Content Manager OnDemand Distribution Facility Installation and Reference | IBM and Unicom[https://publibfp.dhe.ibm.com/epubs/pdf/c1933583.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933583.pdf) | 2001, 2020 and2017-2020 |
| SC19-3351-03 | IBM Content Manager OnDemand for Multiplatforms, V10.5 Introduction and Planning | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933513.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933513.pdf) | **2020-03-13** |
| **GC19-3342-03** | Content Manager OnDemand for Multiplatforms Version 10 Release 5 - Installation and Configuration Guide | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933423.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933423.pdf) | **2020-03-20** |
| SC19-3352-03 | Content Manager OnDemand for Multiplatforms Version 10 Release 5 - Administration Guide | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933523.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933523.pdf) | **2020-03-13** |
| SC19-3354-04 | Content Manager OnDemand Version 10 Release 5 - Indexing Reference | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933544.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933544.pdf) | **2020-03-13** |
| SC19-3353-03 | Content Manager OnDemand Version 10 Release 5 - Web Enablement Kit Implementation Guide (ODWEK) | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933533.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933533.pdf) | **2020-03-13** |
| SC19-3362-03 | IBM Content Manager OnDemand, V10.5 Enhanced Retention Management Guide | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933623.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933623.pdf) | **2020-03-13** |
| **ISBN/ IBM** | **Title** | **Publisher(s)** | **Date** |
| SC19-3355-03 | IBM Content Manager OnDemand, V10.5 Windows Client Installation Guide | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933553.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933553.pdf) | **2020-03-13** |
| SC19-3357-03 | IBM Content Manager OnDemand, V10.5 Windows Client Customization Guide | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933573.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933573.pdf) | **2020-03-13** |
| SC19-3356-03 | IBM Content Manager OnDemand, V10.5 Messages and Codes | [https://publibfp.dhe.ibm.com/epubs/pdf/c1933563.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1933563.pdf) | **2020-03-13** |
|  | IBM Content Manager OnDemand Best Practices Guide | [https://www.ibm.com/support/pages/system/ files/support/swg/swgdocs.nsf/0/
eeee7450f3eb8e6385257b6e0047cef4/$FILE/
IBM%20Content%20Manager%20OnDemand%
20Best%20Practices_033015v2.pdf](https://www.ibm.com/support/pages/system/files/support/swg/swgdocs.nsf/0/eeee7450f3eb8e6385257b6e0047cef4/$FILE/IBM%20Content%20Manager%20OnDemand%20Best%20Practices_033015v2.pdf)(Authors: Ben Boltz, Chris Lewis, Darrell Bryant, Hassan (Al) Shazly, Nancy O’Brien, Vanessa Stonesifer) | March 2015 |

**Table 1.1:** The most current IBM Content Manager OnDemand downloadable PDF documentation links

# [Hardware and Software Requirements](#toc.xhtml_s4a)

The complete requirements for the IBM Hardware and Software requirements link can be found at:

https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=B685BAC0A4A411E9AFF08CE80514C01B&osPlatforms=AIX|Linux|Windows&duComponentIds=D005|D001|D003|D002|D012|D004|S007|S006|S010|S011|S009|S008&mandatoryCapIds=9|25|20|16|162|26&optionalCapIds=131|20|162

The supported Operating System versions (8.1 through 8.9 and later) on Linux Red Hat Enterprise Linux are shown in *[Figure 1.1](#c01.xhtml_fig1_1):*

![](images/Figure1.1.jpg)

**Figure 1.1:** The Content Manager OnDemand Version 10.5 Supported RedHat Linux RHEL 8 versions

The Fix Pack version **`10.5.0.7`** requirements can be selected using the dropdown box and the highlighted **`Download PDF`** icon, as shown in *[Figure 1.2](#c01.xhtml_fig1_2):*

![](images/Figure1.2.jpg)

**Figure 1.2:** The Fix Pack version 10.5.0.7 requirements can be selected using the dropdown box

# [Operating System Environment Variable Settings](#toc.xhtml_s5a)

The Linux **root** user bash command window profile file, **`./bash_profile`** *,* should be used to set the required IBM Content Manager OnDemand environment variables, as illustrated in *[Figure 1.3](#c01.xhtml_fig1_3):*

![](images/Figure1.3.jpg)

**Figure 1.3:** The ***root ./bash_profile*** file environment variable settings

**Note:** *The integration with IBM FileNet P8 requires that you purchase and install the Enhanced Retention Management feature of Content Manager OnDemand*

# [Required Extensions for IBM FileNet Add-on](#toc.xhtml_s6a)

The **Add-on** extensions required for the **IBM FileNet Content Engine Fixed Content Device** can be configured by logging into the IBM FileNet **`acce`** web Administration tool, as shown in *[Figure 1.4](#c01.xhtml_fig1_4)*:

![](images/Figure1.4.jpg)

**Figure 1.4:** The Log In into the IBM FileNet ***acce*** web Administration tool

The **IBM FileNet Add-on** extensions, highlighted in *[Figure 1.5](#c01.xhtml_fig1_5)*, are required for the **Content Federated Services**:

![](images/Figure1.5.jpg)

**Figure 1.5:** The ***IBM FileNet Add-on*** extensions highlighted are required for the ***Content Federated Services***

The ***`5.2.1 CFS ICI Lockdown Extensions`*** **Add-on** details are shown in *[Figure 1.6](#c01.xhtml_fig1_6)*:

![](images/Figure1.6.jpg)

**Figure 1.6:** The ***5.2.1 CFS ICI Lockdown Extension Add-on*** details

The ***`5.2.1 CFS-IS Extensions`*** **Add-on** is shown in *[Figure 1.7](#c01.xhtml_fig1_7)*:

![](images/Figure1.7.jpg)

**Figure 1.7:** The ***5.2.1 CFS-IS Extensions Add-on***

The **Db2 11.5** port, **25011**, used by the **ARCHIVE** database for IBM Content Manager OnDemand is enabled using the Linux **`firewall-cmd`** commands, as shown in *[Figure 1.8](#c01.xhtml_fig1_8)***:**

![](images/Figure1.8.jpg)

**Figure 1.8:** The ***DB2 11.5*** port, ***25011,*** used by the ***ARCHIVE*** database for ***IBM Content Manager OnDemand***

**Note**: *IBM recommends that the* ***Content Manager OnDemand Database*** *instance should be named* ***archive*** *to make use of the default configuration settings and to assist with problem determination and support from IBM.*

1.  To create a custom document class in the content engine platform:
    1.  Start the **`Create Class`** wizard in the IBM FileNet Content Engine **`acce`** administration console.
    2.  In the domain navigation pane, select the object store (we use **`DOS1`** as an example).
    3.  In the object store navigation pane, right-click the **`Data Design`** **>** **`Classes`** **>** **`Document`** folder.
    4.  Click **`New Class`**.
    5.  Enter the name **`OD-`*`ClassName`***, where ***`ClassName`*** is the **Application Group** name, and then click **`Next`**.
    6.  Complete the wizard and open the new class.

        See: [https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=cmod-creating-custom-document-class](https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=cmod-creating-custom-document-class)

2.  Adding properties to the new custom document class - IBM Documentation

    See: [https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=cmod-adding-properties-new-custom-document-class](https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=cmod-adding-properties-new-custom-document-class)

3.  Mapping FileNet P8 properties to Content Manager OnDemand application group fields - IBM Documentation

    See: [https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=ccmcc-mapping-filenet-p8-properties-content-manager-ondemand-application-group-fields](https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=ccmcc-mapping-filenet-p8-properties-content-manager-ondemand-application-group-fields)

    **Note:** *The mapping of properties is covered in detail in [Appendix B - Recreating an Application Group](#appb.xhtml), Mapping to a FileNet Fixed Content Device*

4.  **CFS-OD Export** Usage information - IBM Documentation

    See: [https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=federation-usage-information](https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=federation-usage-information)

# [Setting Up CFS-CMOD on Windows Server](#toc.xhtml_s7a)

The Windows Server client administration program, **`OnDemand Administrator V10.5 (64-bit)`**, is clicked, listed in **Windows Explorer**, as highlighted in *[Figure 1.9](#c01.xhtml_fig1_9):*

![](images/Figure1.9.jpg)

**Figure 1.9:** The Windows Server client administration program, ***OnDemand Administrator V10.5 (64-bit)***, is clicked

**Note:** *The installation and configuration for the* ***Windows Server*** *and* ***Client*** *versions of* ***IBM OnDemand*** *should be completed before using the program, as will be described in [Chapter 5, Installing the Windows Version of CMOD](#c05.xhtml), to [Chapter 7, CMOD Administration on Windows](#c07.xhtml), of this book.*

The Windows Server for **IBM OnDemand** (named **`DESKTOP-B3JB93`** on our server) is selected and right-clicked to select the **`Logon`** menu, as highlighted in *[Figure 1.10](#c01.xhtml_fig1_10)*:

![](images/Figure1.10.jpg)

**Figure 1.10:** The ***OnDemand*** server (***DESKTOP-B3JB93R***) is selected and right-clicked for the Logon

The **`ADMIN`** user and password are entered as illustrated in *[Figure 1.11](#c01.xhtml_fig1_11)*, and the **`OK`** command button is selected to Logon to the Windows Server, **`DESKTOP-B3JB93:`**

![](images/Figure1.11.jpg)

**Figure 1.11:** The ***ADMIN*** user and password are entered to Logon to the Windows Server, ***DESKTOP-B3JB93***

The **`Application Groups`** section of the expanded, **`DESKTOP-B3JB93 OnDemand Servers`**, node is selected, as highlighted in *[Figure 1.12](#c01.xhtml_fig1_12)*, and the **`Baxter Bay Credit`** **`Application Group`** is right-clicked to allow the highlighted Properties menu item to be selected, as shown in *[Figure 1.12](#c01.xhtml_fig1_12)*:

![](images/Figure1.12.jpg)

**Figure 1.12:** The ***Baxter Bay Credit*** is right-clicked to allow the Properties menu item to be selected

The **`Advanced…`** command button on the **`General`** tab is selected, as shown in *[Figure 1.13](#c01.xhtml_fig1_13)*:

![](images/Figure1.13.jpg)

**Figure 1.13:** The ***Advanced…*** command button on the ***General*** tab is selected

Under the **`“Interoperate with FileNet P8”`** heading section of the dialog box, check the **`“Yes”`** **radio button in answer** to the question **`“Use Content Federation Services (CFS-OD)?”`**, as highlighted in *[Figure 1.14](#c01.xhtml_fig1_14)*:

![](images/Figure1.14.jpg)

**Figure 1.14:** Select the “***Yes” radio button in response*** to the question “***Use Content Federation Services (CFS-OD)?”***

The **`Federate Documents Automatically`** option, shown in *[Figure 1.14](#c01.xhtml_fig1_14)*, causes the **CMOD** server to generate the information needed to federate documents to **IBM FileNet P8** at the time documents are loaded to the **Application Group**.

**Note:** *This option has no impact on existing* ***CMOD*** *documents for the* ***Application Group****; it only applies to new documents loaded.*

*If this option is not enabled, then the* ***CMOD*** *server does not generate the federation information when documents are loaded to the application group.*

*In this case, documents can be manually selected for federation using one of the* ***CMOD*** *client applications using the **`"Export unscheduled"`** mode.*

After clicking the **`OK`** command button in *[Figure 1.14](#c01.xhtml_fig1_14)*, the **`General`** tab is shown, and the **`Update`** command button can be selected to register the changes to the **`Baxter Bay Credit`** **`Application Group`**, as highlighted in *[Figure 1.15](#c01.xhtml_fig1_15)*:

![](images/Figure1.15.jpg)

**Figure 1.15:** The ***Update*** command button can be selected to register the changes to ***Baxter Bay Credit***

The **`OK`** command button is selected to complete the update, as shown in *[Figure 1.16](#c01.xhtml_fig1_16)*:

![](images/Figure1.16.jpg)

**Figure 1.16:** The ***OK*** command button is selected to complete the update

At this point, if you get the following Error message, as illustrated in *[Figure 1.17](#c01.xhtml_fig1_17)*, then this indicates that the required **`CFS-CMOD`** field is not yet in the list of fields for the **Application Group**. We must add this **`CFS-CMOD`** field using the following steps:

![](images/Figure1.17.jpg)

**Figure 1.17:** The error shown indicates that the required ***CFS-CMOD*** field is missing

Select the **`Field Definition`** tab and add a new name in the “Database Field Name” text box for use as a **`CFS-CMOD`** field (we have used the name **`CMODDescription`**, though this will be an integer field), and click the **`Add`** command button, as highlighted in *[Figure 1.18](#c01.xhtml_fig1_18):*

![](images/Figure1.18.jpg)

**Figure 1.18:** Select the Field Definition tab and add a new field in the “Database Field Name” text box for use as a ***CFS-CMOD*** field

Click on the **`Field Information`** tab, as highlighted in *[Figure 1.19](#c01.xhtml_fig1_19)*:

![](images/Figure1.19.jpg)

**Figure 1.19:** Click on the ***Field Information*** tab to enter the new ***CMODDescription*** field properties

Select the newly created field from the **`Name`** drop-down, as highlighted in *[Figure 1.20](#c01.xhtml_fig1_20):*

![](images/Figure1.20.jpg)

**Figure 1.20:** Select the newly created field, ***CMODDescription***, from the ***Name*** drop-down

Leave the Type drop-down box set as **`Filter`** and select the **`Small Int (2)`** **option from the** Data Type **drop-down box**, as shown in *[Figure 1.21](#c01.xhtml_fig1_21)*:

![](images/Figure1.21.jpg)

**Figure 1.21:** Leave the Type drop-down box set as ***Filter*** and select ***Small Int (2) as*** the Data Type from the drop-down box

Select the **`CFS-CMOD`** box, as illustrated in *[Figure 1.22](#c01.xhtml_fig1_22)*:

![](images/Figure1.22.jpg)

**Figure 1.22:** Select the ***CFS-CMOD*** box and click ***OK*** to save the changes to the Fields

Continue updating or creating the **Application Group** and click **`OK`** to complete the changes and exit.

The IBM **`OnDemand Configurator`** program must now be loaded to reload the **`Running`** status services, as shown in *[Figure 1.23](#c01.xhtml_fig1_23)*:

![](images/Figure1.23.jpg)

**Figure 1.23:** The IBM ***OnDemand Configurator*** program must now be loaded to reload the ***Running*** status services

Each Service is stopped and restarted by right-clicking on the **`Service Name`**, as illustrated in *[Figure 1.24](#c01.xhtml_fig1_24)*:

![](images/Figure1.24.jpg)

**Figure 1.24:** Each Service is stopped and restarted by right-clicking on the ***Service Name***

The Fields created for the **`Baxter Bay Credit Application Group`** are listed as follows:

`name                      String             Index 1`

`account                  String 11          Index 1`

`crd_date                Date`

`balance                   Decimal Float 16`

`CMODDescription         Small Int 2 (for setting the CFS-CMOD flag)`

# [Creating a Custom Document Class in the Linux IBM FileNet P8 Content Engine](#toc.xhtml_s8a)

1.  Start the Create Class wizard in the **`acce`** administration console:

    [http://ecmukdemo22:9080/acce/](http://ecmukdemo22:9080/acce/)

    1.  In the domain navigation pane, select the object store, **`DOS1`**.
    2.  In the **`DOS1`** object store navigation pane, right-click the

        **`Data Design`** > **`Classes`** > **`Document`** folder.

    3.  Click **`New Class`**.
2.  Enter the name **`OD-BaxterBayCredit`** and click **`Next`** and repeat this until the **`OD-BaxterBayCredit`** **`New Document`** class has been created, as shown in *[Figure 1.25](#c01.xhtml_fig1_25)*:

    ![](images/Figure1.25.jpg)

    **Figure 1.25:** The new Document Class, **`OD-BaxterBayCredit`**, is created

3.  Complete the wizard with property fields, as we created in *[Figure 1.19](#c01.xhtml_fig1_19)*, and open the new class.

    Create **account** with a Property Template name of **`od-account`** (symbolic name **`odaccount`**), as shown in *[Figure 1.26](#c01.xhtml_fig1_26):*

    ![](images/Figure1.26.jpg)

    **Figure 1.26:** Create ***account*** with a Property Template name of ***od-account*** (symbolic name ***odaccount***)

    The **`od-account`** property details are displayed and the **`Finish`** command button is selected, as illustrated in *[Figure 1.27](#c01.xhtml_fig1_27)*:

    ![](images/Figure1.27.jpg)

    **Figure 1.27:** The ***od-account*** property details are displayed and the ***Finish*** command button is selected

    The status of the **`od-account`** property template creation is displayed, as shown in *[Figure 1.28](#c01.xhtml_fig1_28)*:

    ![](images/Figure1.28.jpg)

    **Figure 1.28:** The status of the ***od-account*** property template creation is displayed

    Repeat the **Property Template** creation procedure as shown above for the other fields:

    *   For **`crd_date`**, create a Property Template named **`od-crd_date`** (symbolic name **`odcrd_date`**).
    *   For **`balance`**, create a Property Template named **`od-balance`** (symbolic name **`odbalance`**).
    *   For **`CMODDescription`**, create a Property Template named **`od-CMODDescription`**

        (symbolic name **`odCMODDescription)`**.

# [Conclusion](#toc.xhtml_s9a)

In this chapter, we covered the free, downloadable PDF documentation for the supported platforms of the **IBM Content Manager OnDemand** software and the available high-level functions it provides. The chapter outlined the prerequisites for **CMOD**’s integration with **IBM FileNet Content Engine** and **IBM Content Navigator**.

The next chapter, *Installing* ***CMOD*** *on Linux Systems*, covers the step-by-step guide for downloading, installing, and configuring **IBM Content Manager OnDemand** version **10.5, base** and **Fix Pack 10.5.0.7** upgrade, on a **RedHat Linux** **RHEL** version **8.8** server running on a **VMware** virtual system.

# [Multiple Choice Questions](#toc.xhtml_s10a)

1.  Which port does **Db2** 11.5 use for the **CMOD** **ARCHIVE** database in the example for the **`firewall-cmd`** commands?
    1.  50000
    2.  25000
    3.  50011
    4.  25011
2.  The integration with IBM FileNet P8 requires
    1.  The **ARCHIVE** database
    2.  The Enhanced Retention Management feature of **CMOD**
    3.  Red Hat Enterprise Linux
    4.  The **CMOD** Blog website
3.  IBM **CMOD** 10.5 was released in
    1.  April 2021
    2.  March 2020
    3.  The mid-1980s
    4.  October 2015

# [Answers](#toc.xhtml_s11a)

1.  d
2.  b
3.  b

# [Questions](#toc.xhtml_s12a)

1.  Which is the latest Fix Pack version available for IBM Content Manager OnDemand?

    **Note:** *This answer will change over time, but this chapter includes a way to identify the available Fix Packs*.

2.  Which web link provides a good source of information and guidance for users and Administrators of IBM’s Content Manager OnDemand product?
3.  What is IBM’s Content Manager OnDemand product principally used for?

    **Note:** *There is a hint in the name of the Db2 Database for this question.*

# [Key Terms](#toc.xhtml_s13a)

*   **API**: Application Programmer’s Interface is a library of callable software subroutines written to support the intercommunication between two or more separate functional software systems.
*   **CMOD**: IBM Content Manager OnDemand.
*   **ODWEK**: The OnDemand Web Enablement Kit.
*   **PDF:** The Portable Document Format, created by Adobe, provides a standard layout.
*   **RHEL:** The RedHat Enterprise Linux operating system.
*   **acce:** The IBM FileNet P8 Content Engine administration console web application.

# [CHAPTER 2](#toc.xhtml_c02)

# [Installing CMOD on Linux Systems](#toc.xhtml_c02)

# [Introduction](#toc.xhtml_s14a)

This chapter covers the step-by-step download, installation, and configuration of the IBM Content Manager OnDemand version **10.5 base** and **Fix Pack 10.5.0.7** upgrade on a **RedHat Linux** version **8.8** server running on a VMware virtual system.

Refer to the link [https://cmod.wiki/dox/CMOD-v10.5-README.txt](https://cmod.wiki/dox/CMOD-v10.5-README.txt) for the installation notes, which also include the notes for each Fix Pack version.

# [Structure](#toc.xhtml_s15a)

In this chapter, we will discuss the following topics:

*   Downloading the **Base CMOD Version 10.5** System for Linux
*   Linux Prerequisites for **CMOD Release 10.5**
*   Installing **CMOD** on **RedHat RHEL 8.0** Linux
    *   Installing the **Linux GSKit**
    *   Installing **Apache Zookeeper**
*   Configuring **IBM FileNet P8** for a **Fixed Content Device** Using **CMOD**
*   **Fix Pack 10.5.0.7** Installation
*   Older **CMOD** References
*   Creating an Instance of **Content Manager OnDemand**

# [Downloading the Base CMOD Version 10.5 System for Linux](#toc.xhtml_s16a)

The following steps were used to download and install **Content Manager OnDemand** on a **RedHat version 8.8 Linux** server:

1.  Select the link [https://partnerportal.ibm.com/registration/](https://partnerportal.ibm.com/registration/) to log in to the **IBM PartnerWorld** **Software Access Catalog**, as shown in *[Figure 2.1](#c02.xhtml_fig2_1)*. For IBM Customers, use the following link: [https://www.ibm.com/software/passportadvantage/pao_customer.html](https://www.ibm.com/software/passportadvantage/pao_customer.html)

    **Note:** *To access the* ***IBM PartnerWorld Software Access Catalog****, although IBM allows any relevant business to register as an IBM PartnerWorld partner, your company has to have at least* ***IBM Silver Level PartnerWorld*** *accreditation to gain free access to the* ***IBM Software Access Catalog****.*

    ![](images/Figure2.1.jpg)

    **Figure 2.1:** The IBM PartnerWorld Portal is selected

2.  The **`Software Access Catalog`** is then selected, as illustrated in *[Figure 2.2](#c02.xhtml_fig2_2)*:

    ![](images/Figure2.2.jpg)

    **Figure 2.2:** The ***Software Access Catalog*** is selected to show the download search for IBM Software Systems

3.  The **`Software Access Catalog`** **`downloads`** page is loaded, as illustrated in *[Figure 2.3](#c02.xhtml_fig2_3)*:

    ![](images/Figure2.3.jpg)

    **Figure 2.3:** The Software Access Catalog downloads page is loaded

4.  The **`Find by brand`** search option is selected and the dropdown boxes are chosen, as shown in *[Figure 2.4](#c02.xhtml_fig2_4),* to select the **RedHat Linux 8.8** base version of the IBM Content Manager OnDemand (**CMOD**) software installation package for download.

    ![](images/Figure2.4.jpg)

    **Figure 2.4:** The Find by brand search option is selected

    The **`Find by brand`**, **`"Brand"`**, drop-down is set to **`Analytics – Platform`**, the **`Filter options`** are set to the **`Date posted`** drop-down of **`All Post`**, the **`Family name`** drop-down is set to **`Content Manager OnDemand`**, the **`Language`** drop-down is set to **`English`**, and the **`Operating System`** drop-down is set to **`RHEL 8.8`**.

5.  The **`Download Director`** or the **HTTP** download options are available, but the **`Download Director`** has the advantage of restarting a partial download if the download is interrupted. The highlighted **`Search`** command button is then selected, as shown in *[Figure 2.5](#c02.xhtml_fig2_5)*:

    ![](images/Figure2.5.jpg)

    **Figure 2.5:** The Download Director option and the Search command are selected

6.  Since we know that the **eAssembly** part number for the base **IBM Content Manager OnDemand** Version **10.5.0.0** is **`CJ6K6ML`**, we can alternatively use the **`Find by part number`** Search option, as shown in *[Figure 2.6](#c02.xhtml_fig2_6):*

    ![](images/Figure2.6.jpg)

    **Figure 2.6:** The ***Find by part number*** Search option is selected as an alternative

7.  After selecting the **`Search`** command, we can then get the list of the various different platforms supported by **CMOD** version **10.5.0.0**, from which we can select the **Linux** version, as highlighted in *[Figure 2.7](#c02.xhtml_fig2_7)*:

    ![](images/Figure2.7.jpg)

    **Figure 2.7:** The ***CMOD 10.5*** Linux option (Part Number ***CC4JDML***) is selected as highlighted

8.  The tick box for Part Number **`CC4JDML`** is selected and the **`I agree`** radio button option must be selected after reviewing the License agreement (in the link), to allow the **CMOD** 10.5.0.0 Base software to be downloaded, as illustrated in *[Figure 2.8](#c02.xhtml_fig2_8)*:

    ![](images/Figure2.8.jpg)

    **Figure 2.8:** The tick box for Part Number ***CC4JDML*** and the ***I agree*** radio button option must be selected

9.  If the **Download Director** program does not start, then there is a link available, highlighted in *[Figure 2.9](#c02.xhtml_fig2_9)*, which will allow the program to be installed:

    ![](images/Figure2.9.jpg)

    **Figure 2.9:** The ***install / re-install Download Director*** link can be selected if required

10.  The **`install / re-install Download Director`** link is installed following the link instructions, as illustrated in *[Figure 2.10](#c02.xhtml_fig2_10)*:

    ![](images/Figure2.10.jpg)

    **Figure 2.10:** The ***install / re-install Download Director*** link is installed following the link instructions

11.  The highlighted **`Install Download Director`** command button is selected to install the **`IBM Download Director`** application, as shown in *[Figure 2.11](#c02.xhtml_fig2_11)*:

    ![](images/Figure2.11.jpg)

    **Figure 2.11:** The highlighted Install Download Director command button is selected

12.  On some platforms (or with some web browsers), the **`IBM Download Director`** application will not install or run, so the option to use **`HTTP`** can be selected, as illustrated in *[Figure 2.12](#c02.xhtml_fig2_12)*:

    ![](images/Figure2.12.jpg)

    **Figure 2.12:** The option to use ***HTTP*** can be selected for downloading the ***CMOD*** software

13.  If the **`HTTP`** option is used, then the web browser can be used to show the progress of the software package download, as shown in *[Figure 2.13](#c02.xhtml_fig2_13)*:

    ![](images/Figure2.13.jpg)

    **Figure 2.13:** The ***IBM_CMOD_V10.5_LINUX_ML.tar*** package download progress is viewed

14.  We can now create the folder path, **`/opt/CMOD`**, on the Linux server to copy the downloaded **`CMOD`** Version 10.5 software package, as shown in *[Figure 2.14](#c02.xhtml_fig2_14)*:

    ![](images/Figure2.14.jpg)

    **Figure 2.14:** The ***/opt/CMOD*** Linux folder is created

15.  The downloaded **`IBM_CMOD_V10.5_LINUX_ML.tar`** package is moved to the **`/opt/CMOD`** folder, as shown in *[Figure 2.15](#c02.xhtml_fig2_15)*:

    ![](images/Figure2.15.jpg)

    **Figure 2.15:** The ***IBM_CMOD_V10.5_LINUX_ML.tar*** package is moved to the ***/opt/CMOD*** folder

16.  The path to use to copy the **`IBM_CMOD_V10.5_LINUX_ML.tar`** package is selected using the **`+Other Locations`** command, as highlighted in *[Figure 2.16](#c02.xhtml_fig2_16)*:

    ![](images/Figure2.16.jpg)

    **Figure 2.16:** The ***+Other Locations*** command is used to navigate to the ***/opt/CMOD*** target folder

17.  The moved **`IBM_CMOD_V10.5_LINUX_ML.tar`** package file security permissions are modified using the **Linux** command:

    `chmod 775 IBM_CMOD_V10.5_LINUX_ML.tar`

    The **Linux** commands used are summarized in the **Linux** command window, as shown in *[Figure 2.17](#c02.xhtml_fig2_17)*:

    ![](images/Figure2.17.jpg)

    **Figure 2.17:** The ***IBM_CMOD_V10.5_LINUX_ML.tar*** package file security permissions are modified

18.  As shown in *[Figure 2.18](#c02.xhtml_fig2_18)*, the **`IBM_CMOD_V10.5_LINUX_ML.tar`** package file is unpacked using the following command:

    `tar -xvf IBM_CMOD_V10.5_LINUX_ML.tar`

    ![](images/Figure2.18.jpg)

    **Figure 2.18:** The ***IBM_CMOD_V10.5_LINUX_ML.tar*** package file is unpacked

# [Linux Prerequisites for CMOD Release 10.5](#toc.xhtml_s17a)

The following minimum prerequisites are required on the **Linux** system before installing **IBM Content Manager OnDemand 10.5.0.0:**

*   Red Hat Enterprise **Linux** (**RHEL**) **7 update 7 for x86_64** or later
*   **glibc.i686**, **libgcc.i686**, and **libstdc++.i686** for **32bit support**, which are installed using the following **Linux** command:

    `yum install -y libstdc++-devel.i686`

    This installs the package**`libstdc++-devel-8.5.0-20.el8.i686`**, as shown in *[Figure 2.19](#c02.xhtml_fig2_19)*:

    ![](images/Figure2.19.jpg)

    **Figure 2.19:** The package ***libstdc++-devel-8.5.0-20.el8.i686*** is installed

*   **Database**: **IBM Db2 V11.1** or later (other databases are also supported, including Oracle Database 19c all versions and future fix-packs). Microsoft SQL Server database is NOT supported.
*   IBM Spectrum Protect V8.1 or later.
*   IBM Global Security Kit Version 8 (included in the installation packaging).

(Using a **JDBC** connection on **Linux** of:

`jdbc:db2://localhost:25011/ARCHIVE:retrieveMessagesFromServerOnGetMessage=true;`

`)`

The **Linux** command is run as follows:

`yum install -y file file-libs python3-magic`

This command is used to install packages **`file-5.33-25.el8.x86_64`**,**`file-libs-5.33-25.el8.x86_64`**, and **`python3-magic-5.33-25.el8.noarch`**, as shown in *[Figure 2.20](#c02.xhtml_fig2_20)*:

![](images/Figure2.20.jpg)

**Figure 2.20:** Packages ***file-5.33-25.el8.x86_64***, ***file-libs-5.33-25.el8.x86_64***, and ***python3-magic-5.33-25.el8.noarch***

The **Linux** command is run as follows, as shown in *[Figure 2.21](#c02.xhtml_fig2_21)*:

`yum install -y ncurses-libs.i686`

![](images/Figure2.21.jpg)

**Figure 2.21:** The Linux command ***yum install -y ncurses-libs.i686*** is run

The **Linux** command is run as follows:

`yum install -y openssl`

![](images/Figure2.22.jpg)

**Figure 2.22:** The Linux command ***yum install -y openssl*** is run

# [Installing CMOD on RedHat RHEL 8.0 Linux](#toc.xhtml_s18a)

The latest version 10.5 release of IBM Content Manager OnDemand for Multiplatform Server has changes for the default install directory path names. The defaults have been updated to the following paths:

*   **`/opt/IBM/ondemand/V10.5`** for AIX
*   **`/opt/ibm/ondemand/V10.5`** for Linux and Linux on System z
*   **`C:\Program Files\IBM\OnDemand\V10.5`** for Windows

The **LDAP** parameters are initially empty in the **`/opt/ibm/ondemand/V10.5/config/ars.cfg`** file, as shown in *[Figure 2.23](#c02.xhtml_fig2_23):*

![](images/Figure2.23.jpg)

**Figure 2.23:** The ***LDAP*** Parameters are initially empty in the ***ars.cfg*** file

**Note:** *The following commands are necessary to update the file security permissions on the extracted files from the* ***CMOD*** *installation package, but these are not documented in the **`readme.txt`** file:*

`cd /opt/CMOD/linux`

`chmod 775 odlinux.bin`

`chmod 775 *.rpm`

The installation steps for the Base **CMOD** Version **10.5.0.0** are as follows:

1.  To install **CMOD** from the command line, as shown in *[Figure 2.24](#c02.xhtml_fig2_24)*, use:

    `./odlinux.bin -i console`

    (It is just documented as **`odlinux.bin -i console`**, which does not work!)

    ![](images/Figure2.24.jpg)

    **Figure 2.24:** To install ***CMOD*** from the command line, we can use ***./odlinux.bin -i console***

2.  The installer is prompted to enter a number from the list of supported languages (enter **2 for English**). The **`InstallAnywhere`** program then displays the **CMOD** version details, as illustrated in *[Figure 2.25](#c02.xhtml_fig2_25)*:

    ![](images/Figure2.25.jpg)

    **Figure 2.25:** The InstallAnywhere program then displays the CMOD version details

3.  The user is prompted to accept the License, so we **enter** **`1`** to accept this, as shown in *[Figure 2.26](#c02.xhtml_fig2_26):*

    ![](images/Figure2.26.jpg)

    **Figure 2.26:** The user is prompted to accept the License, so we enter 1 to accept this

4.  The default path of **`/opt/ibm/ondemand/V10.5`** is used for the installation by clicking the ***Enter*** (Return) key, as highlighted in *[Figure 2.27](#c02.xhtml_fig2_27)*:

    ![](images/Figure2.27.jpg)

    **Figure 2.27:** The default path of ***/opt/ibm/ondemand/V10.5*** is used for the installation

5.  The default **Authorized User** License option (**`UVU`**) is selected by using the ***Enter*** key, as shown in *[Figure 2.28](#c02.xhtml_fig2_28)*:

    ![](images/Figure2.28.jpg)

    **Figure 2.28:** The default ***Authorized User*** License option (***UVU***) is selected by using the ***Enter*** key

6.  The **CMOD** Version, path, and the required Disk Space (**`1,008,586,179 bytes`**) used for the installation are displayed, as highlighted in *[Figure 2.29](#c02.xhtml_fig2_29)*:

    ![](images/Figure2.29.jpg)

    **Figure 2.29:** The ***CMOD*** Version, path, and Disk Space used for the installation are displayed as highlighted

7.  The ***Enter*** key is pressed to confirm the installation after all checks are completed, as shown in *[Figure 2.30](#c02.xhtml_fig2_30)*:

    ![](images/Figure2.30.jpg)

    **Figure 2.30:** The ***Enter*** key is pressed to confirm the installation after all checks are completed

8.  The second option (2) is entered to display the readme.txt file after the **CMOD** install has been completed, as illustrated in *[Figure 2.31](#c02.xhtml_fig2_31)*:

    ![](images/Figure2.31.jpg)

    **Figure 2.31:** Option (2) is entered to display the readme.txt file after the ***CMOD*** install has been completed

9.  The **`README`** file details confirm the installed version of the **CMOD** system, as shown in *[Figure 2.32](#c02.xhtml_fig2_32)*:

    ![](images/Figure2.32.jpg)

    **Figure 2.32:** The ***README*** file details confirm the installed version of the ***CMOD*** system as highlighted

10.  The ***Enter*** key can be pressed repeatedly to page down through the **`readme.txt`** file until the last page is displayed, as illustrated in *[Figure 2.33](#c02.xhtml_fig2_33)*:

    ![](images/Figure2.33.jpg)

    **Figure 2.33:** The ***Enter*** key can be pressed repeatedly to page down through the ***readme.txt*** file

11.  The ***Enter*** key is pressed to exit the Installation program for the **`IBM OnDemand V10.5`** system, as shown in *[Figure 2.34](#c02.xhtml_fig2_34)*:

    ![](images/Figure2.34.jpg)

    **Figure 2.34:** The ***Enter*** key is pressed to exit the Installation program for ***IBM OnDemand V10.5***

# [Installing the Linux GSKit](#toc.xhtml_s19a)

The **Linux GSKit** installation must be performed as the user **root**.

**Note:** *The IBM Global Security Kit (GSKit) provides libraries and utilities for SSL or TLS secure protocol communication. The* ***-nodeps*** *flag should* ***not*** *be used unless specifically referenced in the instructions below.*

1.  Use the **`rpm`** commands to install the **Linux GSKit** in the default location (**`/usr/local`**), as illustrated in *[Figure 2.35](#c02.xhtml_fig2_35)*:

    `cd /opt/CMOD/linux`

    `rpm -Uv gskcrypt64-8.0.55.12.linux.x86_64.rpm`

    `rpm -Uv gskssl64-8.0.55.12.linux.x86_64.rpm`

    ![](images/Figure2.35.jpg)

    **Figure 2.35:** The ***rpm*** commands to install the ***Linux GSKit*** in the default location ( ***/usr/local***)

2.  The warnings shown in *[Figure 2.36](#c02.xhtml_fig2_36)* do not prevent the installation of the GSKit libraries:

    ![](images/Figure2.36.jpg)

    **Figure 2.36:** The warnings shown do not prevent the installation of the GSKit libraries

# [Installing Apache Zookeeper](#toc.xhtml_s20a)

1.  The **`apache-zookeeper-3.5.6-bin.tar.gz`** compressed file is unpacked using the **Linux** **`tar`** command, as illustrated in *[Figure 2.37](#c02.xhtml_fig2_37)*, using the following:

    `tar -zxvf apache-zookeeper-3.5.6-bin.tar.gz`

    **ZooKeeper** is a service for maintaining configuration information, naming, providing distributed synchronization, and offering group services.

    ![](images/Figure2.37.jpg)

    **Figure 2.37:** The ***apache-zookeeper-3.5.6-bin.tar.gz*** compressed file is unpacked using the ***tar*** command

2.  The **Apache Zookeeper** directory, **`apache-zookeeper-3.5.6-bin`**, is now available.

    The latest information about **Apache ZooKeeper** can be found at: [http://zookeeper.apache.org/](http://zookeeper.apache.org/)

    And on the wiki at: [https://cwiki.apache.org/confluence/display/ZOOKEEPER](https://cwiki.apache.org/confluence/display/ZOOKEEPER)

    The **Apache Zookeeper** directory is shown in *[Figure 2.38](#c02.xhtml_fig2_38):*

    ![](images/Figure2.38.jpg)

    **Figure 2.38:** The Apache Zookeeper directory, ***apache-zookeeper-3.5.6-bin***, is now available

# [Configuring IBM FileNet P8 for a Fixed Content Device Using CMOD](#toc.xhtml_s21a)

The supporting configuration documentation for the **Content Federation Services for Content Manager OnDemand** (**CFS-CMOD**) can be viewed at the following link:

[https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=configuration-configuring-content-manager-cfs-cmod](https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=configuration-configuring-content-manager-cfs-cmod)

First, install IBM FileNet P8 Addon for **CFS-IS** if not already installed. Refer to the link:

[https://www.ibm.com/docs/en/filenet-p8-platform/5.5.12?topic=extensions-cfs-is](https://www.ibm.com/docs/en/filenet-p8-platform/5.5.12?topic=extensions-cfs-is)

And also:

[https://www.ibm.com/docs/en/filenet-p8-platform/5.5.12?topic=iecr-integration-filenet-content-federation-services-content-manager-ondemand](https://www.ibm.com/docs/en/filenet-p8-platform/5.5.12?topic=iecr-integration-filenet-content-federation-services-content-manager-ondemand)

A table of prerequisites can be listed using the link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=management-content-manager-ondemand-integration-filenet-p8](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=management-content-manager-ondemand-integration-filenet-p8)

The following steps can be used to configure an IBM FileNet P8 server for a Fixed Content Device integration to a **CMOD** server:

1.  Installing the Content Manager OnDemand Web Enablement Kit (**ODWEK**) is covered in the following link, which we will expand on step by step in this section:

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod004.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod004.htm)

    To configure the **ODWEK** API in the Content Platform Engine server, log in to the WebSphere Administrative Console for the IBM FileNet Content Engine web application, as shown in *[Figure 2.39](#c02.xhtml_fig2_39):*

    https://localhost:9043/ibm/console/logon.jsp

    ![](images/Figure2.39.jpg)

    **Figure 2.39:** Log in to the WebSphere Administrative Console for the IBM FileNet Content Engine

2.  Navigate to the **`Servers`**->**`Server Types`**->**`WebSphere Application servers`**->**`server1`** page, open the **`Java and Process Management`** section, under the **`Server Infrastructure`** heading, and click on the **`Process definition`** link, as highlighted in *[Figure 2.40](#c02.xhtml_fig2_40)*:

    ![](images/Figure2.40.jpg)

    **Figure 2.40:** Click the ***Process definition*** link as highlighted

3.  Select the **`Java Virtual Machine`** link, as highlighted in *[Figure 2.41](#c02.xhtml_fig2_41):*

    ![](images/Figure2.41.jpg)

    **Figure 2.41:** Select the ***Java Virtual Machine*** link as highlighted

4.  Enter the full path of the **`ODApi.jar`** file in the Java classpath, as shown in *[Figure 2.42](#c02.xhtml_fig2_42)*.

    (We have installed the **`ODWEK API`** jar file in the path:

    **`/opt/ibm/ondemand/V10.5/www/api/ODApi.jar)`**

    ![](images/Figure2.42.jpg)

    **Figure 2.42:** Enter the full path of the ***ODApi.jar*** file in the Java ***Classpath*** text box

    Also, after installing the Fix Pack 7, append the following to the Classpath box, separating each path reference with the colon (“:”) character:

    `:/opt/ibm/ondemand/V10.5/www/api/ODApi.jar:/opt/ibm/ondemand/V10.5/jars/gson-2.10.1.jar:/opt/ibm/ondemand/V10.5/jars/log4j-api-2.20.0.jar:/opt/ibm/ondemand/V10.5/jars/log4j-core-2.20.0.jar`

    Save the changes to the master configuration, and then, in step 5, restart the WebSphere Application Server.

5.  The WebSphere Application Server for the IBM FileNet web application must be restarted for the classpath changes for the **ODWEK API** to be incorporated, as illustrated in *[Figure 2.43](#c02.xhtml_fig2_43)*:

    ![](images/Figure2.43.jpg)

    **Figure 2.43:** The WebSphere Application Server for the IBM FileNet web application must be restarted

    The commands used are as follows:

    `cd /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/bin`

    `./stopServer.sh server1`

    `./startServer.sh server1`

6.  The **root** users **`.bash_profile`** file was edited using the **vi** editor to add the full **ODWEK** Linux installation path name, **`/opt/ibm/ondemand/V10.5`**, to the **`PATH`** environment variable, as shown in *[Figure 2.44](#c02.xhtml_fig2_44)*:

    ![](images/Figure2.44.jpg)

    **Figure 2.44:** The root users ***.bash_profile*** file was edited using the ***vi*** editor to add ***/opt/ibm/ondemand/V10.5*** to the ***PATH*** environment variable

7.  The following IBM documentation link covers the requirement for two JDBC data sources for the IBM CMOD system integration with the IBM FileNet Fixed Content Device interface:

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod005.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod005.htm)

    The **CMOD** Fixed Content Device requires two **JDBC** data sources to be created on the Web Application server, configured for the Content Platform Engine. The two data sources provide **JDBC** links to the database where the **CFS** importer tables will be created by the IBM FileNet P8 Content Engine **acce** web application. The database holds the **CMOD** Fixed Content Device importer tables, which we will create in the next section.

    Creating the **CFS** importer database creates the following tables:

    `CFS_IMP_QUEUE`

    `CFS_IMP_QUEUE_ERROR`

    `CFS_IMP_SESSION`

    `CFS_REPOSITORY_MAP`

    `FDB_VERSION_SERIES`

    See Also:

    Content Manager OnDemand Database Tables - CMOD.wiki:

    [https://cmod.wiki/index.php/Content_Manager_OnDemand_Database_Tables](https://cmod.wiki/index.php/Content_Manager_OnDemand_Database_Tables)

    For creating the DataSources, we use the IBM FileNet Content Engine **`configmgr`** utility as follows:

    First, change to the configuration tool directory for IBM FileNet:

    `cd /opt/IBM/FileNet/ContentEngine/tools/configure`

    Then, edit **`configmgr.ini`** (if the **JRE** cannot be located), as shown in *[Figure 2.45](#c02.xhtml_fig2_45)*:

    From:

    `/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-2.el8_5.x86_64/jre/bin`

    ![](images/Figure2.45.jpg)

    **Figure 2.45:** The default ***JRE*** path in ***configmgr.ini*** is changed

    To:

    `/opt/IBM/Java/jre/bin/`, as shown in *[Figure 2.46](#c02.xhtml_fig2_46):*

    ![](images/Figure2.46.jpg)

    **Figure 2.46:** The JRE path is updated to ***`/opt/IBM/Java/jre/bin/`***

    The following commands were used to run the Linux-based IBM FileNet P8 Content Engine configuration program to create the IBM Content Manager OnDemand Data Sources on the WebSphere application server profile (**AppSrv01** path, **server1**), as illustrated in *[Figure 2.47](#c02.xhtml_fig2_47)*:

    `cd /opt/IBM/FileNet/ContentEngine/tools/configure`

    `./configmgr`

    ![](images/Figure2.47.jpg)

    **Figure 2.47:** The Linux IBM FileNet P8 configuration program is run to create the ***CMOD*** Data Sources

    **Note:** *The Database Test for the Datasource creation may fail, but the task itself can still run successfully (see [Figures 2.48](#c02.xhtml_fig2_48)–[2.58](#c02.xhtml_fig2_58)).*

8.  The **`File`->** **`Open Profile`**… menu option is selected in the **`configmgr`** screen, as illustrated in *[Figure 2.48](#c02.xhtml_fig2_48):*

    ![](images/Figure2.48.jpg)

    **Figure 2.48:** The ***File-> Open Profile***… menu option is selected in the ***configmgr*** screen

9.  The path (**`ContentEngine/tools/configure/profiles`**) to the existing install profile file, **`ASBECM95510NewInstall.cfgp`** (or whatever the initial installation profile filename was called), is navigated to and the **`Open`** command button is selected, as shown in *[Figure 2.49](#c02.xhtml_fig2_49):*

    ![](images/Figure2.49.jpg)

    **Figure 2.49:** The path (***`ContentEngine/tools/configure/profiles`***) to the profile file, ***`ASBECM95510NewInstall.cfgp`***, is navigated to and the ***Open*** command button selected

10.  The loaded profile name, **`ASBECM95510NewInstall`** (or whatever the initial installation profile filename was called), is selected with a **right-**click and the highlighted **`Edit Application Server Properties`…** menu option is clicked, as shown in *[Figure 2.50](#c02.xhtml_fig2_50)*:

    ![](images/Figure2.50.jpg)

    **Figure 2.50:** The loaded profile name, ***ASBECM95510NewInstall***, is selected with a right-click and the highlighted ***Edit Application Server Properties…*** menu option is clicked

11.  The password for the WebSphere Application Server is re-entered and the **`Test Connection`** command button is clicked, as highlighted in *[Figure 2.51](#c02.xhtml_fig2_51)*:

    ![](images/Figure2.51.jpg)

    **Figure 2.51:** The password for the WebSphere Application Server is re-entered and the ***Test Connection*** command button clicked

12.  The Test Results pop-up window indicate that the connection to the application server is successful and the password is correct, as shown in *[Figure 2.52](#c02.xhtml_fig2_52)*:

    ![](images/Figure2.52.jpg)

    **Figure 2.52:** The Test Results indicate that the connection to the application server is successful

13.  The loaded profile name, **`ASBECM95510NewInstall`**, is selected with a **right-** click and the **`Add New Task`**`->` **`Configure Object Store JDBC Data Sources`** task is added, as highlighted in *[Figure 2.53](#c02.xhtml_fig2_53)*:

    ![](images/Figure2.53.jpg)

    **Figure 2.53:** The loaded profile name, ***ASBECM95510NewInstall***, is selected with a ***right-***click and the ***Add New Task***-> ***Configure Object Store JDBC Data Sources*** task added

14.  The **`New_Configure Object Store JDBC Data Sources`** task name is changed by **right**-clicking and selecting the **`Rename Task…`** menu option, as shown in *[Figure 2.54](#c02.xhtml_fig2_54)*:

    ![](images/Figure2.54.jpg)

    **Figure 2.54:** The ***New_Configure Object Store JDBC Data Sources*** task name is changed by ***right***-clicking and selecting the ***Rename Task…*** menu option

15.  The **Task** name is changed to **`Configure CMOD JDBC Data Sources for the Fixed Content Device`**, as shown in *[Figure 2.55](#c02.xhtml_fig2_55)*:

    ![](images/Figure2.55.jpg)

    **Figure 2.55:** The ***Task*** name is changed to ***Configure CMOD JDBC Data Sources for the Fixed Content Device***

16.  **Right-**click on the **`Configure CMOD JDBC Data Sources for the Fixed Content Device`** task is used to select the **`Edit Selected Task`** menu option, as highlighted in *[Figure 2.56](#c02.xhtml_fig2_56):*

    ![](images/Figure2.56.jpg)

    **Figure 2.56:** Right***-***click on the ***Configure CMOD JDBC Data Sources for the Fixed Content Device*** task is used to select the ***Edit Selected Task*** menu

17.  The details are entered, as highlighted in *[Figure 2.57](#c02.xhtml_fig2_57),* to create the required **`ARCHIVEDS`** and **`ARCHIVEDSXA`** data sources for **CMOD.**

    ![](images/Figure2.57.jpg)

    **Figure 2.57:** The details are entered as highlighted to create the required ***ARCHIVEDS*** and ***ARCHIVEDSXA*** data sources for ***CMOD***

18.  The Data Sources, **`ARCHIVEDS`** and **`ARCHIVEDSXA`,** can be tested for connectivity to a **CMOD** **Fixed Content Device** database by using the IBM WebSphere administrators console (**[https://localhost:9043/ibm/console/login.do?action=secure](https://localhost:9043/ibm/console/login.do?action=secure)**) using the menu path **`Resources`->`JDBC`->`Data sources`** and then ticking the boxes and using the **`Test connection`** button, as highlighted in *[Figure 2.58](#c02.xhtml_fig2_58)*:

    ![](images/Figure2.58.jpg)

    **Figure 2.58:** The Data Sources, ***ARCHIVEDS*** and ***ARCHIVEDSXA***, can be tested for connectivity to a ***CMOD*** ***Fixed Content Device*** database

19.  To create the **Content Manager OnDemand** (**CMOD**) **Fixed Content Device**, start the **New Fixed Content Device** wizard in the **IBM FileNet P8** **acce** administration console.

    In the domain navigation pane, right-click the **`Global Configuration`** **>** **`Administration`** **>** **`Fixed Content Devices`** folder, and then click **`New Fixed Content Device`** (as illustrated in *[Figure 2.59](#c02.xhtml_fig2_59)*). Then, complete the wizard as shown in the steps following this step.

    **Note**: *Since the following* ***New Fixed Content Devices*** *steps failed using the Base* ***CMOD*** ***10.5.0.0*** *Linux installation, we looked to install a Fix Pack ref:*

    [https://www.ibm.com/support/pages/ibm-content-manager-ondemand-multiplatforms-v10507-readme-files](https://www.ibm.com/support/pages/ibm-content-manager-ondemand-multiplatforms-v10507-readme-files)

    *See the next section of this chapter for this procedure,* ***Fix Pack 10.5.0.7 Installation****, which should be performed before following the rest of this section.*

    ![](images/Figure2.59.jpg)

    **Figure 2.59:** Click the ***Global Configuration > Administration >*** ***Fixed Content Device***s, and then click ***New***

20.  The **`Fixed Content Device`** object **`Display name`** is entered as **`CMODFCD`**, with a default **`Description`** property, which is set with the same text, as highlighted in *[Figure 2.60](#c02.xhtml_fig2_60),* and then the **`Next`** command button is clicked:

    ![](images/Figure2.60.jpg)

    **Figure 2.60:** The ***Fixed Content Device*** object ***Display name*** is entered as ***CMODFCD***

21.  The **`IBM Content Manager`** **`OnDemand`** option is selected from the **`Type`** dropdown list, as illustrated in *[Figure 2.61](#c02.xhtml_fig2_61)*, and then the `Next` command button is selected:

    ![](images/Figure2.61.jpg)

    **Figure 2.61:** The ***IBM Content Manager OnDemand*** option is selected from the ***Type*** dropdown list

22.  The **`Federation JNDI data source`**, **`Federation JNDI XA data source`**, **`Content Manager OnDemand server name`**, and the **`User`** and **`Password`** fields for the database are entered, as highlighted in *[Figure 2.62](#c02.xhtml_fig2_62)*, and then the **`Next>`** command button is selected:

    ![](images/Figure2.62.jpg)

    **Figure 2.62:** The ***Data Source names*** and ***server, user, and password*** fields for the database are entered

23.  The **`Finish`** command button is selected after reviewing the parameters entered to create the **CMOD** **Fixed Content Device**, as illustrated in *[Figure 2.63](#c02.xhtml_fig2_63)*:

    ![](images/Figure2.63.jpg)

    **Figure 2.63:** The ***Finish*** command button is selected after reviewing the parameters entered to create the ***CMOD Fixed Content Device***

24.  The summary of the creation process for the **CMOD Fixed Content Device** is displayed, as shown in *[Figure 2.64](#c02.xhtml_fig2_64)*:

    ![](images/Figure2.64.jpg)

    **Figure 2.64:** The summary of the creation process for the ***CMOD Fixed Content Device*** is displayed

25.  The Windows server (**`DESKTOP-BSJB93R`**) Fixed Content Device was also created for the **`ADMIN`** user, as shown in *[Figure 2.65](#c02.xhtml_fig2_65):*

    ![](images/Figure2.65.jpg)

    **Figure 2.65:** The Configuration of the ***CMOD Fixed Content Device*** for the Windows server version

26.  The **`Replication Class Mappings`** tab for the **`DOS1`** Object Store for the IBM FileNet P8 Content Engine is selected, as highlighted in the **acce** window in *[Figure 2.66](#c02.xhtml_fig2_66):*

    ![](images/Figure2.66.jpg)

    **Figure 2.66:** The ***Replication Class Mappings*** tab for the ***DOS1*** Object Store for the IBM FileNet P8

27.  A new **`Replication Class Mapping`** can be created using the **`New`** command button and selecting the **`CMODFCD`** Fixed Content Device, as shown in *[Figure 2.67](#c02.xhtml_fig2_67)*:

    ![](images/Figure2.67.jpg)

    **Figure 2.67:** A new ***Replication Class Mapping*** can be created using the ***New*** command button

    The **`OK`** command button in *[Figure 2.67](#c02.xhtml_fig2_67)* results in the listing of the **`OD-BaxterBayCredit`** class with a link that can be clicked, as highlighted in *[Figure 2.68](#c02.xhtml_fig2_68):*

    **Note**: The **`OD-BaxterBayCredit`** class is created as described in *[Chapter 1, Introduction to IBM Content Manager OnDemand](#c01.xhtml)*, in the section “*Creating a custom document class in the Linux IBM FileNet P8 content engine*”.

    ![](images/Figure2.68.jpg)

    **Figure 2.68:** The ***OD-BaxterBayCredit*** class link can be clicked as highlighted

    The basic list of properties is displayed, as shown in *[Figure 2.69](#c02.xhtml_fig2_69)*, and the highlighted **`Replication Property Mappings`** tab is selected:

    ![](images/Figure2.69.jpg)

    **Figure 2.69:** The highlighted tab, ***Replication Property Mappings***, is selected

    On the **`Replication Properties Mappings`** tab, we can select the **`New`** command button, as highlighted in *[Figure 2.70](#c02.xhtml_fig2_70)*:

    ![](images/Figure2.70.jpg)

    **Figure 2.70:** On the Replication Properties Mappings tab, we can select the New command button, as highlighted

    The **`account`** property on the **`Baxter Bay Credit`**, external class is mapped to the **`IBM FileNet P8`** Content Engine class **`OD-BaxterBayCredit`**, **`Document Title`** property, as illustrated in *[Figure 2.71](#c02.xhtml_fig2_71)*:

    ![](images/Figure2.71.jpg)

    **Figure 2.71:** The ***CMOD*** ***account*** property on ***Baxter Bay Credit*** is mapped to the FileNet class ***OD-BaxterBayCredit***, ***Document Title*** property

    The **`OK`** command button is clicked to display the property mapping for the **CMOD** **account** String property, as shown in *[Figure 2.72](#c02.xhtml_fig2_72)*:

    ![](images/Figure2.72.jpg)

    **Figure 2.72:** The display of the property mapping for the ***CMOD*** ***account*** String property

    We can add new **Property Definitions** to the **`IBM FileNet P8`** Content Engine class **`OD-BaxterBayCredit`** by selecting the Object Store **`DOS1`**->**`Data Design`**-> **`Classes`**->**`OD-BaxterBayCredit`** and then clicking on the **`Property Definitions`** tab to access the **`Add`** command button, as displayed in *[Figure 2.73](#c02.xhtml_fig2_73)*:

    ![](images/Figure2.73.jpg)

    **Figure 2.73:** Click on the ***Property Definitions*** tab to access the ***Add*** command and to add new properties

    The **`Filter`** text is set to **`od`** and then the **`Filter`** command button is clicked to display the **CMOD** properties, **`od-CMODDescription`**, **`od-account`**, **`od-balance`**, and **`od-crd_date`**, which we tick to select and then click **`OK`** to save, as highlighted in *[Figure 2.74](#c02.xhtml_fig2_74):*

    ![](images/Figure2.74.jpg)

    **Figure 2.74:** Display the ***CMOD*** properties, ***od-CMODDescription***, ***od-account***, ***od-balance***, and ***od-crd_date***, which we tick to select and then click ***OK*** to save

    The selected properties are displayed and the **`Save`** and **`Refresh`** command buttons are selected in that order to update the **`OD-BaxterBayCredit`** **class** property definition list, as highlighted in *[Figure 2.75](#c02.xhtml_fig2_75)*:

    ![](images/Figure2.75.jpg)

    **Figure 2.75:** The selected properties are displayed and the ***Save*** and ***Refresh*** command buttons are selected in that order to update the ***OD-BaxterBayCredit class***

    The **`New Replication Property Mapping`** can now be used to map the **`name`** property to the **`od-account`** property and confirm by clicking **`OK`**, as shown in *[Figure 2.76](#c02.xhtml_fig2_76)*:

    ![](images/Figure2.76.jpg)

    **Figure 2.76:** The ***New Replication Property Mapping*** can now be used to map the ***name*** property to the ***od-account*** property

    The **`New Replication Property Mapping`** can now be used to map the **`crd_date`** property to the **`od-crd_date`** property and confirm by clicking **`OK`**, as shown in *[Figure 2.77](#c02.xhtml_fig2_77):*

    ![](images/Figure2.77.jpg)

    **Figure 2.77:** The ***New Replication Property Mapping*** can now be used to map the ***crd_date*** property to the ***od-crd_date*** property

    The mapped properties can now be seen in the **`Replication Property Mappings`** tab, as shown in *[Figure 2.78](#c02.xhtml_fig2_78)*:

    ![](images/Figure2.78.jpg)

    **Figure 2.78:** The mapped properties can now be seen in the ***Replication Property Mappings*** tab

28.  We have now created the **IBM Content Manager OnDemand Fixed Content Device**, which is described in the following **URL**:

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod006.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod006.htm)

    **Note:** The main link to IBM Content Federation Services for Content Manager OnDemand configuration - IBM Documentation is as follows:

    [https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=products-content-federation-services-content-manager-ondemand-configuration](https://www.ibm.com/docs/en/filenet-p8-platform/5.2.0?topic=products-content-federation-services-content-manager-ondemand-configuration)

29.  Change the **`ARS_STORAGE_MANAGER=TSM`** parameter using vi to edit (in file **`/opt/ibm/ondemand/V10.5/config/ars.cfg`**), as highlighted in *[Figure 2.79](#c02.xhtml_fig2_79)*.

    From:

    ![](images/Figure2.79.jpg)

    **Figure 2.79:** Change the ARS_STORAGE_MANAGER=TSM parameter using vi to edit

    To:

    **`ARS_STORAGE_MANAGER=CACHE_ONLY`**, as highlighted in *[Figure 2.80](#c02.xhtml_fig2_80):*

    ![](images/Figure2.80.jpg)

    **Figure 2.80:** ***The ars.cfg*** file is updated to ***ARS_STORAGE_MANAGER=CACHE_ONLY*** as highlighted

30.  The **`/arscache`** directory is then created as illustrated in *[Figure 2.81](#c02.xhtml_fig2_81)*:

    ![](images/Figure2.81.jpg)

    **Figure 2.81:** The commands are run to create the ***/arscache/cache1*** Linux directory

    `cd /opt/ibm/ondemand/V10.5/config`

    `mkdir /arscache`

    `mkdir /arscache/cache1`

    `chown -R root:root /arscache*`

    `chmod 700 /arscache/cache1`

    `chmod g-s /arscache/cache1`

# [Fix Pack 10.5.0.7 Installation](#toc.xhtml_s22a)

As the **New Fixed Content Device step** in the previous section initially failed, we looked to install a Fix Pack (ref: [https://www.ibm.com/support/pages/ibm-content-manager-ondemand-multiplatforms-v10506-readme-files](https://www.ibm.com/support/pages/ibm-content-manager-ondemand-multiplatforms-v10506-readme-files))

This FixPack also lists three additional jar files required in the **CLASSPATH** for use with the **ODWEK** Java API (**`ODApi.jar`**):

`gson-2.10.1.jar`

`log4j-api-2.19.0.jar`

`log4j-core-2.19.0.jar`

After the update of the fix pack, **10.5.0.7**, we added the following libraries to the Web Application classpath:

`/opt/ibm/ondemand/V10.5/jars`

`gson-2.10.1.jar`

`log4j-api-2.20.0.jar`

`log4j-core-2.20.0.jar`

1.  First, we need to download the **IBM Content Manager OnDemand** FixPack version **10.5.0.7** from **IBM Fix Central** using the following link, and log in as shown in *[Figure 2.82](#c02.xhtml_fig2_82)*:

    [https://www.ibm.com/support/fixcentral](https://www.ibm.com/support/fixcentral)

    ![](images/Figure2.82.jpg)

    **Figure 2.82:** Select the download option for IBM Content Manager OnDemand FixPacks

    The dropdown selections are made, as shown in *[Figure 2.83](#c02.xhtml_fig2_83):*

    ![](images/Figure2.83.jpg)

    **Figure 2.83:** The dropdown selection boxes are set as highlighted and the Continue command button clicked

2.  The **`Browse for fixes`** radio button option is selected and the **`Continue`** button is clicked, as illustrated in *[Figure 2.84](#c02.xhtml_fig2_84):*

    ![](images/Figure2.84.jpg)

    **Figure 2.84:** The ***Browse for fixes*** radio button option is selected and the ***Continue*** button clicked

3.  The list of fix packs is displayed, as shown in *[Figure 2.85](#c02.xhtml_fig2_85),* and we can select the highlighted fix pack version **`10.5.0.7`** for the **CMOD Multiplatform** install package:

    ![](images/Figure2.85.jpg)

    **Figure 2.85:** We select the highlighted fix pack version 10.5.0.7 for the CMOD Multiplatform install package

4.  The **`Continue`** command is clicked after ticking the box for the required Fix Pack, as shown in *[Figure 2.86](#c02.xhtml_fig2_86):*

    ![](images/Figure2.86.jpg)

    **Figure 2.86:** The highlighted Continue command is clicked after ticking the box for the required Fix Pack

5.  The **`Log in to IBM`** screen is displayed to validate the download for the **Fix Pack**, as shown in *[Figure 2.87](#c02.xhtml_fig2_87)*:

    ![](images/Figure2.87.jpg)

    **Figure 2.87:** The ***Log in to IBM*** screen is displayed to validate the download for the Fix Pack

6.  The Password is entered to continue the download of the Fix Pack, as shown in *[Figure 2.88](#c02.xhtml_fig2_88):*

    ![](images/Figure2.88.jpg)

    **Figure 2.88:** The Password is entered to continue the download of the Fix Pack

7.  The **Download using Download Director** option is selected, as shown in *[Figure 2.89](#c02.xhtml_fig2_89)*:

    ![](images/Figure2.89.jpg)

    **Figure 2.89:** The ***Download using Download Director*** option is selected

8.  The **`Download Director`** program application icon can be seen on the **Linux DeskTop**, as highlighted in *[Figure 2.90](#c02.xhtml_fig2_90)*:

    ![](images/Figure2.90.jpg)

    **Figure 2.90:** The highlighted ***Download Director*** program application icon

9.  The **`IcedTea`** web app is triggered in the Firefox Web Browser, as shown in *[Figure 2.91](#c02.xhtml_fig2_91).*

    (The **IcedTea** Java Web browser plugin works in 64-bit browsers under 64-bit Linux and is used for enabling support for Java applets, such as **IBM Download Director** in **64-bit** **Mozilla Firefox**).

    ![](images/Figure2.91.jpg)

    **Figure 2.91:** The ***IcedTea*** web app is triggered in the Firefox Web Browser

10.  The **`Run`** command is selected in *[Figure 2.92](#c02.xhtml_fig2_92)* to launch the **`IBM Download Director`**:

    ![](images/Figure2.92.jpg)

    **Figure 2.92:** The ***Run*** command is selected to launch the ***IBM Download Director***

11.  The **Version 10.5.0.7** Fix Pack for **IBM Content Manager OnDemand** download progress is displayed in **IBM Download Director**, as shown in *[Figure 2.93](#c02.xhtml_fig2_93)*:

    ![](images/Figure2.93.jpg)

    **Figure 2.93:** The Version 10.5.0.7 Fix Pack for IBM Content Manager OnDemand download progress is displayed

12.  The **IBM Download Director Applet** displays the completed Fix Pack download, as illustrated in *[Figure 2.94](#c02.xhtml_fig2_94)*:

    ![](images/Figure2.94.jpg)

    **Figure 2.94:** The IBM Download Director Applet displays the completed Fix Pack download

The following **Linux** commands were used to set up the **CMOD** Fix Pack directory path:

`cd /opt`

`mkdir CMOD_FP`

`cd CMOD_FP/`

The following **Linux** commands were used to copy the downloaded **Fix Pack** version **10.5.0.7** install files:

`cp /root/DownloadDirector/od*.* .`

`cp /root/DownloadDirector/read*.* .`

These commands are shown in *[Figure 2.95](#c02.xhtml_fig2_95)* with their responses:

![](images/Figure2.95.jpg)

**Figure 2.95:** The ***Linux*** commands used to copy the downloaded ***Fix Pack*** version ***10.5.0.7*** install files

Read the Installation Documentation online at [https://www.ibm.com/docs/cmofm/10.5.0](https://www.ibm.com/docs/cmofm/10.5.0) for further information. We can now apply the current fix pack using the install from the command lines:

`chmod 775 *`

`./odlinux.bin -i console,` as shown in *[Figure 2.96](#c02.xhtml_fig2_96):*

![](images/Figure2.96.jpg)

**Figure 2.96:** We apply the current fix pack using the install from the command line ***./odlinux.bin -i console***

The installer program prompts for the **`Locale`** to use from a list, as shown in *[Figure 2.97](#c02.xhtml_fig2_97)*:

![](images/Figure2.97.jpg)

**Figure 2.97:** The installer program prompts for the ***Locale*** to use from a list

The **`IBM OnDemand V10.5`** installer prompts for the user to continue the install set-up, as shown in *[Figure 2.98](#c02.xhtml_fig2_98):*

![](images/Figure2.98.jpg)

**Figure 2.98:** The ***IBM OnDemand V10.5*** installer prompts for the user to continue the install setup

In *[Figure 2.99](#c02.xhtml_fig2_99)*, the number **`1`** is entered to accept the License:

![](images/Figure2.99.jpg)

**Figure 2.99:** The number 1 is entered to accept the License

The type of License is selected as **`1`** for **`UVU`**, as shown in *[Figure 2.100](#c02.xhtml_fig2_100)*:

![](images/Figure2.100.jpg)

**Figure 2.100:** The type of License is selected as 1 ***for Authorized User (UVU)***

The required disk space is displayed along with the amount of available free disk space on the system, as illustrated in *[Figure 2.101](#c02.xhtml_fig2_101)*:

![](images/Figure2.101.jpg)

**Figure 2.101:** The required disk space, ***833,822,436*** bytes, is displayed along with the amount of available free space

The Return (***Enter***) key is selected to start the installation, as shown in *[Figure 2.102](#c02.xhtml_fig2_102):*

![](images/Figure2.102.jpg)

**Figure 2.102:** The Return (Enter) key is selected to start the installation

The option to view the **`readme.txt`** file is presented by entering **`2`** as the response, as shown in *[Figure 2.103](#c02.xhtml_fig2_103)*:

![](images/Figure2.103.jpg)

**Figure 2.103:** The option to view the readme.txt file is presented by entering 2 as the response

The **`readme.txt`** file is loaded for a scrolling review, showing the **`Fix Pack`** **`Release 10.5.0.7`** on **`August 25th, 2023`**, as highlighted in *[Figure 2.104](#c02.xhtml_fig2_104)*:

![](images/Figure2.104.jpg)

**Figure 2.104:** The ***readme.txt*** file is loaded for a scrolling review, with ***Fix Pack*** ***Release 10.5.0.7***

The ***Enter*** key is then pressed to continue with the installation, as shown in *[Figure 2.105](#c02.xhtml_fig2_105)*:

![](images/Figure2.105.jpg)

**Figure 2.105:** The ***Enter*** key is then pressed to continue with the installation

The installer shows that the **IBM CMOD** Fix Pack version **10.5.0.7** was installed successfully, as displayed in *[Figure 2.106](#c02.xhtml_fig2_106)*:

![](images/Figure2.106.jpg)

**Figure 2.106:** The installer shows that the ***IBM CMOD*** Fix Pack version ***10.5.0.7*** was installed successfully

The security on the files in the **`/opt/ibm/ondemand/V10.5/config`** is modified using the following command:

`chmod 755 *`

As illustrated in *[Figure 2.107](#c02.xhtml_fig2_107)*:

![](images/Figure2.107.jpg)

**Figure 2.107:** The security in ***/opt/ibm/ondemand/V10.5/config*** is modified using the command ***chmod 755 ****

We can now add the following to the **WebSphere Class Path**, as for the **`ODApi.jar`** file

`/opt/ibm/ondemand/V10.5/jars`

`gson-2.10.1.jar`

`log4j-api-2.20.0.jar`

`log4j-core-2.20.0.jar`

First, we need to log into the **IBM FileNet** WebSphere administration console, as shown in *[Figure 2.108](#c02.xhtml_fig2_108):*

![](images/Figure2.108.jpg)

**Figure 2.108:** Log in to the IBM FileNet WebSphere administration console

Then, we navigate to the **`Servers`->`Server Types`->`WebSphere application servers`->`Application servers`** **->** **`server1`** and select the **`Process definition`** link, as shown in *[Figure 2.109](#c02.xhtml_fig2_109)*:

![](images/Figure2.109.jpg)

**Figure 2.109:** Select the ***Servers->Server Types->WebSphere application servers->Application servers -> server1***

The **`Java Virtual Machine`** link is selected, as shown in *[Figure 2.110](#c02.xhtml_fig2_110):*

![](images/Figure2.110.jpg)

**Figure 2.110:** The ***Java Virtual Machine*** link is selected

The **`Classpath`** is updated, as highlighted in *[Figure 2.111](#c02.xhtml_fig2_111)*, with the new **Fix Pack** library files for the **ODWEK API** required at version **10.5.0.7:**

![](images/Figure2.111.jpg)

**Figure 2.111:** The Classpath is updated as highlighted

The **`Apply`** command is clicked to update the repository configuration for WebSphere, as shown in *[Figure 2.112](#c02.xhtml_fig2_112):*

![](images/Figure2.112.jpg)

**Figure 2.112:** The ***Apply*** command is clicked to update the repository configuration for WebSphere

The **`Save`** command is clicked to update the Master repository configuration for WebSphere, as shown in ***[Figure 2.113](#c02.xhtml_fig2_113)***:

![](images/Figure2.113.jpg)

**Figure 2.113:** The Save command is clicked to update the Master repository configuration for WebSphere

The security on the installed **IBM OnDemand** jar library files is updated using the following commands:

`cd /opt/ibm/ondemand/V10.5/jars`

`chmod 775 *.jar`

As illustrated in [Figure 2.114](#c02.xhtml_fig2_114):

![](images/Figure2.114.jpg)

**Figure 2.114:** The security on the installed ***IBM OnDemand*** jar library files is updated

We need to restart the WebSphere server used for the IBM FileNet web application, as shown in *[Figure 2.115](#c02.xhtml_fig2_115)*:

`cd /opt/IBM/WebSphere/AppServer/profiles/AppSrv01`

`cd bin`

`./stopServer.sh server1`

`./startServer.sh server1`

![](images/Figure2.115.jpg)

**Figure 2.115:** We need to restart the ***WebSphere*** server used for the ***IBM FileNet*** web application

The **`ARS_SUPPORT_HOLD=1`** parameter must be added to the **`ARS.CFG`** configuration file to enable the **Content Federation Services** for **Content Manager OnDemand** feature (this is not required for the Windows platform). The **`/opt/ibm/ondemand/V10.5/config/ars.cfg`** file is edited, as highlighted in *[Figure 2.116](#c02.xhtml_fig2_116)*:

![](images/Figure2.116.jpg)

**Figure 2.116:** The ***/opt/ibm/ondemand/V10.5/config/ars.cfg*** file is edited as highlighted

The two highlighted parameters in the list for the **`ars.cfg`** file, shown as follows, are required to enable the **Content Federation Services** for **Content Manager OnDemand** feature:

`ARS_SRVR=LibSrvr`

`ARS_LOCAL_SRVR=ECMUKDEMO22`

`ARS_SUPPORT_HOLD=1`

`ARS_SUPPORT_CFSOD=1`

`ARS_ORIGINAL_CODEPAGE=1208`

The **`/opt/ibm/ondemand/V10.5/config/ars.ini`** file is edited, as highlighted in *[Figure 2.117](#c02.xhtml_fig2_117)*:

![](images/Figure2.117.jpg)

**Figure 2.117:** The ***/opt/ibm/ondemand/V10.5/config/ars.ini*** file is edited

`[@SRV@_ARCHIVE]`

`HOST=ECMUKDEMO22`

`PROTOCOL=2`

`PORT=1445`

`SRVR_INSTANCE=ARCHIVE`

`SRVR_INSTANCE_OWNER=archive`

`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.cfg`

`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.dbfs`

`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.cache`

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`

`[@SRV@_DD]`

`PROTOCOL=1`

Start using

`[root@ECMUKDEMO22 bin]# ./arssock`

**Note:** *For Windows, use the OnDemand Configurator.*

*Start the OnDemand Configurator by clicking:*

***`Start > IBM OnDemand Server V10.5 > OnDemand Configurator V10.5`****.*

***Right-click an instance****.*

*Select* ***`Properties/Server`****.*

*Click* ***`Advanced Options`****, select* ***`Enable CFS-CMOD`****, and then click* ***`OK`****.*

Restart the Content Manager OnDemand instance

On Linux, we installed a new DB2 database instance for the **archive** user, as follows:

The IBM DB2 **`./db2setup`** installer is called, as shown in *[Figure 2.118](#c02.xhtml_fig2_118)*, using the Linux commands as follows:

`cd /opt/IBM/DB2/server_dec`

`export DISPLAY=:0`

`echo $DISPLAY`

`./db2setup`

![](images/Figure2.118.jpg)

**Figure 2.118:** The IBM DB2 ***./db2setup*** installer is called

The **`New Install`** command is selected, as highlighted in *[Figure 2.119](#c02.xhtml_fig2_119):*

![](images/Figure2.119.jpg)

**Figure 2.119:** The ***New Install*** command is selected as highlighted

The **`DB2 Version 11.5.7.0 Server Editions`** option is selected, as highlighted in *[Figure 2.120](#c02.xhtml_fig2_120)*, and the **`Next`** command is clicked:

![](images/Figure2.120.jpg)

**Figure 2.120:** ***The DB2 Version*** ***11.5.7.0*** ***Server Editions*** option is selected

The **`Typical`** command button option is selected, as shown in *[Figure 2.121](#c02.xhtml_fig2_121):*

![](images/Figure2.121.jpg)

**Figure 2.121:** The ***Typical*** command button option is selected and ***Next*** clicked

The highlighted fields are entered to create the **`archive`** **Db2** instance, as shown in *[Figure 2.122](#c02.xhtml_fig2_122):*

![](images/Figure2.122.jpg)

**Figure 2.122:** The highlighted fields are entered to create the **archive** **Db2** instance and **Next** clicked

The fenced user, **`db2fenc1`**, is entered and the **`Next`** command button is clicked, as shown in *[Figure 2.123](#c02.xhtml_fig2_123):*

![](images/Figure2.123.jpg)

**Figure 2.123:** The fenced user, db2fenc1, is entered and the Next command button clicked

The summary for the **Db2 Instance** parameters is displayed, and then the **`Finish`** button is clicked, as shown in *[Figure 2.124](#c02.xhtml_fig2_124)*:

![](images/Figure2.124.jpg)

**Figure 2.124:** The summary for the ***Db2 Instance*** parameters is displayed and then ***Finish*** clicked

The install progress for the **archive** **Db2 Instance** is displayed, as shown in *[Figure 2.125](#c02.xhtml_fig2_125)*:

![](images/Figure2.125.jpg)

**Figure 2.125:** The install progress for the archive Db2 Instance is displayed

The **Db2** Server **archive** instance install validation steps are displayed, as shown in *[Figure 2.126](#c02.xhtml_fig2_126):*

![](images/Figure2.126.jpg)

**Figure 2.126:** The ***Db2*** Server ***archive*** instance install validation steps are displayed

The **`./db2val`** command is run to validate the new **Db2** **`archive`** Instance, as shown in *[Figure 2.127](#c02.xhtml_fig2_127):*

![](images/Figure2.127.jpg)

**Figure 2.127:** The ***./db2val*** command is run to validate the new Db2 archive Instance

The following **Linux** commands are used to build the **CMOD archive** database, as illustrated in *[Figure 2.128](#c02.xhtml_fig2_128):*

`chown archive:db2iadm1 /arsdb`

`su – archive`

`/opt/ibm/ondemand/V10.5/bin/arsdb -I archive -cv`

![](images/Figure2.128.jpg)

**Figure 2.128:** The ***Linux*** commands used to build the ***CMOD archive*** database

The command shows an issue with the archive database creation, as highlighted in *[Figure 2.128](#c02.xhtml_fig2_128):*

`"ARS4069E The new path to the log is not valid"`

Fix for error, refer to the following:

[https://cmod.wiki/index.php/Unable_to_determine_the_database_engine](https://cmod.wiki/index.php/Unable_to_determine_the_database_engine)

“*If you’re not able to see or connect to DB2, make sure you have the correct group membership (sysadm1* (On our RHEL Linux, **Db2** **11.5.7.0**, **db2iadm1** ) *if your* ***IBM CMOD*** *installation was by-the-book), and check to make sure that the appropriate db2 links have been created with the db2ln command. You will need administrative or root access to perform this task.*

*Also check to see that you have the correct environment variables, with the* ***set*** *or* ***setenv*** *commands, depending on your command shell:”*

The **set** command should show:

`DATABASE=ARCHIVE`

`DB2DIR=/opt/ibm/db2/V10.5`

`DB2INSTANCE=archive`

`DB2LIB=/home/archive/sqllib/lib`

`DB2_HOME=/home/archive/sqllib`

`DB2_NET_CLIENT_PATH=`

`HOSTNAME=OnDemand.example.com`

`HOSTTYPE=x86_64`

`IBM_DB_DIR=/home/archive/sqllib`

`IBM_DB_HOME=/home/archive/sqllib`

`IBM_DB_INCLUDE=/home/archive/sqllib/include`

`IBM_DB_LIB=/home/archive/sqllib/lib`

If you don’t have these values, you will need to find the **`db2profile`** script and execute it to set these variables -- it can be found inside the **`'sqllib'`** directory of the database owner’s home directory.

Edit the **`.bash_profile`** using the vi editor to append the following:

`DATABASE=ARCHIVE`

`export DATABASE`

`DB2DIR=/opt/ibm/db2/V10.5`

`export DB2DIR`

`DB2INSTANCE=archive`

`export DB2INSTANCE`

`DB2LIB=/home/archive/sqllib/lib`

`export DB2LIB`

`DB2_HOME=/home/archive/sqllib`

`export DB2_HOME`

`HOSTNAME=ecmukdemo2`

`export HOSTNAME`

`HOSTTYPE=x86_64`

`export HOSTTYPE`

`IBM_DB_DIR=/home/archive/sqllib`

`export IBM_DB_DIR`

`IBM_DB_HOME=/home/archive/sqllib`

`export IBM_DB_HOME`

`IBM_DB_INCLUDE=/home/archive/sqllib/include`

`export IBM_DB_INCLUDE`

`IBM_DB_LIB=/home/archive/sqllib/lib`

`export IBM_DB_LIB`

We also reviewed the schema name, which we discovered was created with a default of **root**, as illustrated with the queries shown in *[Figure 2.129](#c02.xhtml_fig2_129):*

![](images/Figure2.129.jpg)

**Figure 2.129:** The schema name was discovered to be created with a default of ***root***

This schema name was found to be incorrect since **CMOD** was expecting the schema name to be **archive** on our Linux platform from a review of the log files.

The **root** **`.bash_profile`** was edited using the **`vi`** editor to append the environment list we described earlier, as shown in *[Figure 2.130](#c02.xhtml_fig2_130):*

![](images/Figure2.130.jpg)

**Figure 2.130:** The ***root .bash_profile*** was edited using the ***vi*** editor to append the environment list

Finally, IBM **CMOD** updates have been known to have problems co-existing with earlier versions of **CMOD** being installed at the same time. Removing old **CMOD** versions before configuring a new instance using the **`uninstallod`** command should eliminate any errors. IBM recommends that you always back up your configuration files first!

Refer to [https://cmod.wiki/index.php/Unable_to_determine_the_database_engine](https://cmod.wiki/index.php/Unable_to_determine_the_database_engine) to check access to the **CMOD** database is correct, and then perform database maintenance, as follows:

`./arsdb -I archive -mv`

Or, for defaulting to the archive instance:

`./arsdb -mv`

Start the IBM Content Manager OnDemand server:

`./arssockd -I archive -S`

Where, archive is the IBM Content Manager OnDemand instance name.

If this is not specified, the default is **ARCHIVE,** using:

`./arssockd -S`

See also:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=management-content-manager-ondemand-integration-filenet-p8](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=management-content-manager-ondemand-integration-filenet-p8)

1.  Configuring CFS-CMOD for use with Content Manager OnDemand on Oracle

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod007.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod007.htm)

2.  Creating the Content Manager OnDemand fixed storage area

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod008.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod008.htm)

3.  Configuring the Content Manager OnDemand viewer in Workplace XT

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod009.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod009.htm)

4.  Enabling Application Groups

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod010.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod010.htm)

5.  Creating a custom document class

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod011.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod011.htm)

6.  Adding properties to the new custom document class

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod012.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod012.htm)

7.  Mapping FileNet P8 properties to Content Manager OnDemand application group fields

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod013.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod013.htm)

8.  Configuring the CFSOD Export utility for document federation

    [https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod014.htm](https://www.ibm.com/docs/en/SSNW2F_5.2.0/com.ibm.p8.installingcfsod.doc/cfsod014.htm)

# [Older CMOD References](#toc.xhtml_s23a)

Refer to Version 8.4 - Implementing IBM Content Manager OnDemand Solutions:

[https://www.redbooks.ibm.com/redbooks/pdfs/sg247511.pdf](https://www.redbooks.ibm.com/redbooks/pdfs/sg247511.pdf)

# [Creating an Instance of Content Manager OnDemand](#toc.xhtml_s24a)

For information on the creation of an instance of **CMOD**, refer to the following link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=multiplatforms-installing-content-manager-ondemand-linux-servers](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=multiplatforms-installing-content-manager-ondemand-linux-servers)

To install **Db2** on the library server, we use the following procedure list to ensure all the configuration steps have been completed:

We have used the **Db2** Setup wizard since we had this already installed for IBM FileNet and IBM Content Navigator. As the default installation path is already in use, we installed a new Db2 copy. The default path then becomes **`/opt/ibm/db2/V11.5_`*`##`*** for our Linux system, where *##* is a zero-prefixed sequential number in the range **01** to **99**.

1.  Install **Db2** Universal Database Enterprise Edition (we have used **Db2 11.5.0.7**).

    To support **Content Manager OnDemand** on a new **Db2** installation for all the components, the response for the installation type should be selected as **Typical.** Refer to the following free downloads on **ResearchGate**:

    *   For the installation of the IBM Database, Db2 10.5 Installation on RHEL 8.0 V1:

        [https://doi.org/10.13140/RG.2.2.10491.67369](https://doi.org/10.13140/RG.2.2.10491.67369)

    *   Upgrade of IBM FileNet systems from DB2 10.5 FP 10 to the latest DB2 11.5 version on RedHat RHEL 8.0:

        [https://doi.org/10.13140/RG.2.2.29470.69441](https://doi.org/10.13140/RG.2.2.29470.69441)

2.  We have now created the **Db2** instance for **Content Manager OnDemand** as follows:

    Using the following values:

    Instance Name / User: **`archive`**

    Group Name: **`db2iadm1`**

    Home Directory  **`/home/archive`**

    Auto start **Db2** instance

    at boot time **`n`**

    Create a sample database

    For the **Db2** instance**`no`**

    **Note:** *The group must have SYSADM authority and its name must be unique. The group name on Linux is* ***`db2iadm1`***.

    After the **Db2** software is installed, apply the latest fix pack for **Db2**, as detailed in the following link:

    [https://doi.org/10.13140/RG.2.2.29470.69441](https://doi.org/10.13140/RG.2.2.29470.69441).

    You can view the latest fix packs at: [http://www.ibm.com/support/docview.wss?uid=swg27007053](http://www.ibm.com/support/docview.wss?uid=swg27007053).

    After you install **Db2**, you must add the user that owns the **Content Manager OnDemand** instance to the **Db2** instance owner’s group, **`db2iadm1`**.

    For more details, refer to [https://www.ibm.com/docs/en/db2/11.5?topic=idds-installing-db2-servers-by-using-db2-setup-wizard-linux-unix](https://www.ibm.com/docs/en/db2/11.5?topic=idds-installing-db2-servers-by-using-db2-setup-wizard-linux-unix)

    Next, follow these guidelines (step by step as outlined in the previous section):

    As **root**, we ran the **RedHat Linux** commands as follows:

    `subscription-manager repos --enable=codeready-builder-for-rhel-8-x86_64-rpms`

    `yum install xorg-x11-apps`

    Then, log out and log back in as **root** after the installation:

    `cd /opt/IBM/DB2/server_dec`

    `./db2setup`

    **After installing Db2 on the library server:**

    The required steps for a **CMOD archive** instance creation are as follows:

    To start using **Db2,** you need to log in with the **Db2** instance owner’s ID **archive**.

    (You can connect to the **Db2** instance **archive** using the port number **25011**).

    Optional steps are as follows:

    To validate the installation files, instance, and database functionality, IBM recommends that you run the Validation Tool, **`/opt/ibm/db2/V11.5_01/bin/db2val`**.

    The License Activation CD for Db2 can be downloaded from Passport Advantage if it is not part of the physical media pack from IBM.

The Content Manager OnDemand owner user must be added to the Db2 instance owner’s group.

So, if the **Content Manager OnDemand** instance owner is **root**, and the **Db2** instance owner’s group is **`db2iadm1`**, and the **root** user is specified by the **`SRVR_INSTANCE_OWNER`** parameter in the **`ars.ini`** file, add the **root** user to the **`db2iadm1`** group.

The **DB2INSTANCE** parameter in the **`ars.cfg`** file must also be verified.

**Note:** *The* ***DB2INSTANCE*** *value must specify the name of the created* ***Db2*** *instance for* ***CMOD****, which has a default value of* ***archive****. It should also be noted that the value is case-sensitive.*

1.  Add

    **ARS_ORIGINAL_CODEPAGE=1208** `to the` **ars.cfg** `file`

2.  Create the database

    `mkdir /arsdb`

    `mkdir /arsdb_primarylog`

    `mkdir /arsdb_archivelog`

    `chown archive:db2iadm1 /arsdb_primarylog`

    `chown archive:db2iadm1 /arsdb_archivelog`

    `chown archive:db2iadm1 /arsdb`

3.  Log onto the **Db2** database instance user `su – archive` and run the **CMOD** command:

    `/opt/ibm/ondemand/V10.5/bin/arsdb -I archive -cv`

    `[root@ECMUKDEMO22 config]# cd ../bin`

    `[root@ECMUKDEMO22 bin]# chown archive:db2iadm1 ars*`

    `[root@ECMUKDEMO22 bin]# ls -lsa ars*`

    **Note:** *The parameters for identifying the user’s name that the* ***CMOD*** *database runs under must have a matching case for the user name, so if one is set to lowercase ‘****archive****’ and the other is set to uppercase ‘****ARCHIVE****’, then the* ***arssockd*** *program will error with the code* ***ARS0152E****.*

**Add the** **`ARS_SUPPORT_CFSOD=1`** **parameter:**

The **`CFSOD_FED`** function sends documents to **CFS-CMOD** and makes them available to **IBM FileNet P8** features.

To query the database to determine the documents to be sent to **CFS-CMOD**, you can use the following parameters:

*   SQL query (-i)
*   hold name (-l)
*   text search string (-t or -T)
*   load ID (-X)

To enable the **CFS-CMOD** feature, add the following line to the **`ars.cfg`** file:

`ARS_SUPPORT_CFSOD=1`

Ensure that the **CFS-CMOD** function is turned on for the **application group** and you have set the permissions to use the **CFS-CMOD** before you attempt this function. Otherwise, a permission error will occur.

In the **`ars.ini`** file, we have to set the following:

`SRVR_INSTANCE_OWNER=archive`

And in the **`ars.cfg`** file:

`DB2INSTANCE=archive`

**First Run of the CMOD Database creation command using arsdb:**

`[archive@ECMUKDEMO22 arsdb]$` **/opt/ibm/ondemand/V10.5/bin/arsdb -I archive -cv**

`ARS4018I Creating the DB2 archive database`

`ARS4119I Specify the type of archive logging to be used:`

`Do you wish to use` **DISK(1)**`, TSM(2), or CIRCULAR(3)?`

**`Please specify 1, 2, or 3:1`**

`ARS4062I Database created with territory 'US', code page '1208', code set 'UTF-8' and collating sequence ''`

`ARS4068I Updating the archive database configuration`

`ARS4073I Deactivating database archive`

`ARS4071I Backing up the archive database so that the updates can take effect`

`ARS4057I Timestamp for backup image is: 20240323140616`

`ARS4026I Creating table root.arsag`

`ARS4034I Creating index root.arsag_name_idx`

`ARS4034I Creating index root.arsag_agid_idx`

`ARS4042I Updating runstat statistics for table root.arsag`

`ARS4026I Creating table root.arsag2fol`

`ARS4034I Creating index root.arsag2fol_idx`

`ARS4042I Updating runstat statistics for table root.arsag2fol`

`ARS4026I Creating table root.arsagfld`

`ARS4034I Creating index root.arsagfld_idx`

`ARS4042I Updating runstat statistics for table root.arsagfld`

`ARS4026I Creating table root.arsagfldalias`

`ARS4034I Creating index root.arsagfldalias_idx`

`ARS4042I Updating runstat statistics for table root.arsagfldalias`

`ARS4026I Creating table root.arsagindex`

`ARS4034I Creating index root.arsagindex_idx`

`ARS4042I Updating runstat statistics for table root.arsagindex`

`ARS4026I Creating table root.arsagperms`

`ARS4034I Creating index root.arsagperms_idx`

`ARS4042I Updating runstat statistics for table root.arsagperms`

`ARS4026I Creating table root.arsann`

`ARS4034I Creating index root.arsann_idx`

`ARS4042I Updating runstat statistics for table root.arsann`

`ARS4026I Creating table root.arsapp`

`ARS4034I Creating index root.arsapp_idx`

`ARS4034I Creating index root.arsapp_name_idx`

`ARS4042I Updating runstat statistics for table root.arsapp`

`ARS4026I Creating table root.arsappusr`

`ARS4034I Creating index root.arsappusr_idx`

`ARS4042I Updating runstat statistics for table root.arsappusr`

`ARS4026I Creating table root.arscab`

`ARS4034I Creating index root.arscab_name_idx`

`ARS4034I Creating index root.arscab_cid_idx`

`ARS4042I Updating runstat statistics for table root.arscab`

`ARS4026I Creating table root.arscab2fol`

`ARS4034I Creating index root.arscab2fol_idx`

`ARS4042I Updating runstat statistics for table root.arscab2fol`

`ARS4026I Creating table root.arscabnames`

`ARS4034I Creating index root.arscabnames_cid_idx`

`ARS4042I Updating runstat statistics for table root.arscabnames`

`ARS4026I Creating table root.arscabperms`

`ARS4034I Creating index root.arscabperms_idx`

`ARS4042I Updating runstat statistics for table root.arscabperms`

`ARS4026I Creating table root.arscfsodwork`

`ARS4034I Creating index root.arscfsodwork_idx`

`ARS4042I Updating runstat statistics for table root.arscfsodwork`

`ARS4026I Creating table root.arscmfedwork`

`ARS4034I Creating index root.arscmfedwork_idx`

`ARS4042I Updating runstat statistics for table root.arscmfedwork`

`ARS4026I Creating table root.arsfol`

`ARS4034I Creating index root.arsfol_name_idx`

`ARS4034I Creating index root.arsfol_fid_idx`

`ARS4042I Updating runstat statistics for table root.arsfol`

`ARS4026I Creating table root.arsfolfld`

`ARS4034I Creating index root.arsfolfld_idx`

`ARS4042I Updating runstat statistics for table root.arsfolfld`

`ARS4026I Creating table root.arsfolfldusr`

`ARS4034I Creating index root.arsfolfldusr_idx`

`ARS4042I Updating runstat statistics for table root.arsfolfldusr`

`ARS4026I Creating table root.arsfolnames`

`ARS4034I Creating index root.arsfolnames_fid_idx`

`ARS4042I Updating runstat statistics for table root.arsfolnames`

`ARS4026I Creating table root.arsfolperms`

`ARS4034I Creating index root.arsfolperms_idx`

`ARS4042I Updating runstat statistics for table root.arsfolperms`

`ARS4026I Creating table root.arsftiwork`

`ARS4034I Creating index root.arsftiwork_idx`

`ARS4042I Updating runstat statistics for table root.arsftiwork`

`ARS4026I Creating table root.arsgroup`

`ARS4034I Creating index root.arsgroup_gid_idx`

`ARS4034I Creating index root.arsgroup_name_idx`

`ARS4042I Updating runstat statistics for table root.arsgroup`

`ARS4026I Creating table root.arshold`

`ARS4034I Creating index root.arshold_name_idx`

`ARS4034I Creating index root.arshold_hid_idx`

`ARS4042I Updating runstat statistics for table root.arshold`

`ARS4026I Creating table root.arsholdmap`

`ARS4034I Creating index root.arsholdmap_idx`

`ARS4042I Updating runstat statistics for table root.arsholdmap`

`ARS4026I Creating table root.arsholdnames`

`ARS4034I Creating index root.arsholdnames_hid_idx`

`ARS4042I Updating runstat statistics for table root.arsholdnames`

`ARS4026I Creating table root.arsholdperms`

`ARS4034I Creating index root.arsholdperms_idx`

`ARS4042I Updating runstat statistics for table root.arsholdperms`

`ARS4026I Creating table root.arsholdwork`

`ARS4034I Creating index root.arsholdwork_idx`

`ARS4042I Updating runstat statistics for table root.arsholdwork`

`ARS4026I Creating table root.arsload`

`ARS4034I Creating index root.arsload_idx`

`ARS4034I Creating index root.arsload_name_idx`

`ARS4034I Creating index root.arsload_dt_idx`

`ARS4042I Updating runstat statistics for table root.arsload`

`ARS4026I Creating table root.arsloadwork`

`ARS4034I Creating index root.arsloadwork_idx`

`ARS4034I Creating index root.arsloadwork_loadid_idx`

`ARS4042I Updating runstat statistics for table root.arsloadwork`

`ARS4026I Creating table root.arsnameq`

`ARS4034I Creating index root.arsnameq_idx`

`ARS4042I Updating runstat statistics for table root.arsnameq`

`ARS4026I Creating table root.arsnode`

`ARS4028I Inserting default values into table root.arsnode`

`ARS4034I Creating index root.arsnode_idx`

`ARS4034I Creating index root.arsnode_name_idx`

`ARS4042I Updating runstat statistics for table root.arsnode`

`ARS4026I Creating table root.arsprt`

`ARS4034I Creating index root.arsprt_name_idx`

`ARS4034I Creating index root.arsprt_pid_idx`

`ARS4042I Updating runstat statistics for table root.arsprt`

`ARS4026I Creating table root.arsprtopts`

`ARS4034I Creating index root.arsprtopts_idx`

`ARS4042I Updating runstat statistics for table root.arsprtopts`

`ARS4026I Creating table root.arsprtusr`

`ARS4034I Creating index root.arsprtusr_idx`

`ARS4042I Updating runstat statistics for table root.arsprtusr`

`ARS4026I Creating table root.arsres`

`ARS4034I Creating index root.arsres_idx`

`ARS4042I Updating runstat statistics for table root.arsres`

`ARS4026I Creating table root.arsseg`

`ARS4034I Creating index root.arsseg_name_idx`

`ARS4034I Creating index root.arsseg_idx`

`ARS4034I Creating index root.arsseg_cdate_idx`

`ARS4034I Creating index root.arssegssdt_idx`

`ARS4034I Creating index root.arsseg_cdt_idx`

`ARS4042I Updating runstat statistics for table root.arsseg`

`ARS4026I Creating table root.arsset`

`ARS4028I Inserting default values into table root.arsset`

`ARS4034I Creating index root.arsset_name_idx`

`ARS4034I Creating index root.arsset_sid_idx`

`ARS4042I Updating runstat statistics for table root.arsset`

`ARS4026I Creating table root.arssys`

`ARS4028I Inserting default values into table root.arssys`

`ARS4042I Updating runstat statistics for table root.arssys`

`ARS4026I Creating table root.arsuser`

`ARS4028I Inserting default values into table root.arsuser`

`ARS4034I Creating index root.arsuser_id_idx`

`ARS4034I Creating index root.arsuser_name_idx`

`ARS4042I Updating runstat statistics for table root.arsuser`

`ARS4026I Creating table root.arsusrgrp`

`ARS4034I Creating index root.arsusrgrp_idx`

`ARS4034I Creating index root.arsusrgrp_idx2`

`ARS4042I Updating runstat statistics for table root.arsusrgrp`

`ARS4026I Creating table root.arsusrgrpid`

`ARS4034I Creating index root.arsusrgrpid_idx`

`ARS4042I Updating runstat statistics for table root.arsusrgrpid`

`[archive@ECMUKDEMO22 arsdb]$`

Next, we ran the **DB2PROFILE** script file.

The script files can be found in the **`/home/archive/sqllib`** directory, which is the home directory of the instance owner.

You can add the script file to your **.profile** or **.login** file.

For example: **`.` `/export/home/archive/sqllib/db2profile`**

After executing the script file, you can start the **Db2** command line interface and connect to the database. For example:

**db2**

To stop the **Db2** command line interface, enter: **`db2 =>quit`**

See:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=servers-configuring-instances-linux](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=servers-configuring-instances-linux)

Each instance has different security from other instances on the same server. You must define separate users and groups for each instance and set **CMOD** application group and folder permissions for users of each instance. Each instance has its own system log.

The **`ars.ini`** file must contain one section for each instance created. Each section identifies the **`ars.cfg`** file, **`ars.dbfs`** file, and **`ars.cache`** file used by the instance.

There must be a unique copy of the **`ars.cfg`** file for each instance.

IBM recommends that you maintain separate table space file systems and cache storage file systems for each instance, as in an **`ars.dbfs`** file and **`ars.cache`** file for each instance.

Each instance must run on its **own unique TCP/IP port number**. The port for each instance is configured in the **ars.ini** file.

**Instances in the ars.ini file:**

The **`ars.ini`** file contains information about **CMOD** instances.

When you install the **CMOD** software, the **ars.ini** file contains information about the default instance named **archive**, set as follows on our **Linux** system:

In **`/opt/ibm/ondemand/V10.5/config/ars.ini`**`:`

`[@SRV@_ARCHIVE]`

`HOST=ECMUKDEMO22`

`PROTOCOL=2`

`PORT=1445`

`SRVR_INSTANCE=ARCHIVE`

`SRVR_INSTANCE_OWNER=archive`

`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.cfg`

`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.dbfs`

`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.cache`

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`

`[@SRV@_DD]`

`PROTOCOL=1`

You must use the firewall command on Linux to open the 1445 port:

`firewall-cmd --zone=public --permanent --add-port=1445/tcp`

`firewall-cmd --reload`

We cover the running of the **`arrsstash`** program in more detail in *[Chapter 8, CMOD System User Administration on Linux](#c08.xhtml)*. This command was run as follows to encrypt the **archive** instance users password, as shown in *[Figure 2.131](#c02.xhtml_fig2_131)*:

`cd /opt/ibm/ondemand/V10.5/bin`

`./arsstash -a 1 -c -s /opt/ibm/ondemand/V10.5/config/ars.stash -u archive`

![](images/Figure2.131.jpg)

**Figure 2.131:** The command was run to encrypt the ***archive*** instance users password

The `/root/.bash_profile` file is edited to add the environment `SRVR_OD_STASH` variable:

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`

`export SRVR_OD_STASH`

as illustrated in *[Figure 2.132](#c02.xhtml_fig2_132)*:

![](images/Figure2.132.jpg)

**Figure 2.132:** The ***/root/.bash_profile*** file is edited to add the environment ***SRVR_OD_STASH*** variable

The **`ars.ini`** file is edited to add the parameters to the **`[@SRV@_ARCHIVE]`** instance, as shown in *[Figure 2.133](#c02.xhtml_fig2_133)*, and listed as follows:

`[@SRV@_ARCHIVE]`

`HOST=ECMUKDEMO22`

`PROTOCOL=2`

`PORT=1445`

`SRVR_INSTANCE=ARCHIVE`

`SRVR_INSTANCE_OWNER=archive`

`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.cfg`

`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.dbfs`

`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.cache`

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`

`[@SRV@_DD]`

`PROTOCOL=1`

![](images/Figure2.133.jpg)

**Figure 2.133:** The ***ars.ini*** file is edited to add the parameters to the ***[@SRV@_ARCHIVE***] instance

Refer to [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-instances-in-arsini-file](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-instances-in-arsini-file) for further information on setting up a second instance for testing.

**Specifying the ars.cfg file for the instance:**

The **`ars.cfg`** file contains information about the instance.

The values can be changed by following the documentation in the link as follows:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-specifying-arscfg-file-instance](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-specifying-arscfg-file-instance)

**Specifying the ars.dbfs file for the instance:**

The database manager index data is maintained in table spaces, which are listed as files in the ars.dbfs file used on the CMOD library server.

IBM recommends that these table space file systems should be reserved for use only for CMOD application group data. There should be a minimum of two table space file systems defined, with equal amounts of space for each system, and these space sizes should be maintained in tandem.

**Note**: *For the* ***`Db2`*** *option for* ***Automatic Storage*** *for table spaces, the file systems for the database table space containers do not need to be defined in the* ***`ars.dbfs`*** *file*.

Each of the file names that **CMOD** can use to store table spaces is identified and the tablespace type specified in a separate line in the **`ars.dbfs`** file.

The file systems on the library server that can be used by the database manager to maintain index data in table spaces are listed in the ars.dbfs file.

The following procedure was used to edit the **`ars.dbfs`** file for the archive instance:

1.  Log in to the server as the **root** user and change to the following directory with the following cd command:

    `cd /opt/ibm/ondemand/V10.5/config`

    Edit the **`ars.dbfs`** file using the vi text editor**.**

    For each file system that Content Manager OnDemand can use for table spaces, add one line.

2.  Save the file and exit the vi editor using the wr! and q! commands.

    IBM recommends that the defaults for the table space file system are set as the database **`archive`** (instance owner) and **`db2iadm1`** (group). Set the security, for example, assuming the above default owner and group names are used, to:

    `drwxrws--- 3 archive db2iadm1 512 May 17 12:58 /arsdb/db1/SMS`

3.  The following **chown** **Linux** command recursively changes the **owner** and **group** names of all file systems in the **`/arsdb`** directory tree to the **`archive`** user and the **`db2iadm1`** group:

    `chown -R archive:db2iadm1 /arsdb*`

4.  To set the file permissions of the filesystems, the following **chmod Linux** commands were used as an example for the **`/arsdb/db1/SMS`** filesystem:

    `chmod 2770 /arsdb/db1/SMS`

    `chmod g+s /arsdb/db1/SMS`

**Creating the ars.cache file for the instance:**

The **CMOD** **`ars.cache`** file lists the cache storage file systems on the **Linux** object server used by **CMOD**. When there are multiple file systems, **CMOD** should use the file system listed in the ars.cache file with the greatest amount of space free to store the objects.

The following **`ars.cache`** file entries list five cache storage file systems:

`/arscache/cache1`

`/arscache/cache2`

`/arscache/cache3`

`/arscache/cache4`

`/arscache/cache5`

The security on the files can be changed as required, as follows:

`chown archive:db2iadm1 -R /arscache/`

See also,

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=aix-creating-arscache-file-instance](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=aix-creating-arscache-file-instance)

Log in to the server as the **root** user.

`cd /opt/ibm/ondemand/V10.5/config`

Edit the **`ars.cache`** file using the **`vi`** editor.

For each file system, one line is inserted in the **`ars.cache`** file using the server that Content Manager OnDemand can use for cache storage.

**Note:** *The first entry in the* ***`ars.cache`*** *file lists the base cache storage file system.* ***CMOD*** *stores control information in this base storage file system. This base file system must always be present and must remain as the first entry*

Cache file systems must be owned by the **CMOD** instance owner, **`archive`**, and the system group, **`db2iadm1`**`.` **IBM recommends that** **only the user file permissions are set, not the group or other file permissions.**

For example:

`drwx------ 3 root root 512 Sep 22 13:08 /arscache/cache1`

Use the **`chown`** command to set the ownership permissions. The following example shows how to change the user ownership of all file systems in the **`/arscache`** directory tree:

`chown -R root:root /arscache*`

Use the **`chmod`** command to set the file permissions:

`chmod 700 /arscache/cache1`

`chmod g-s /arscache/cache1`

**CMOD** cache storage files and subdirectories should have the following permissions:

`drwx------ for every subdirectory (700)`

`-r-------- for every object that has been migrated to archive storage (400)`

`-rw------- for every object that has not yet been migrated (600)`

`-rwxrwxrwx for every symbolic link under the retr and migr directories (777)`

See:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-creating-arscache-file-instance](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-creating-arscache-file-instance)

**Specifying the arsldap.ini file:**

The **`ARS_LDAP_BIND_MESSAGES_FILE`** parameter enables **CMOD** to display customized message texts returned from an **LDAP** server to warn users that their **LDAP** password is about to expire or that their account is locked.

The messages displayed to users use this parameter. To enable this feature for messaging, create a file with the required message strings and set **`ARS_LDAP_BIND_MESSAGES_FILE`** to the full path of the message text file. The **`arsldap.ini`** file is provided with example message text strings that can be used by the **`ARS_LDAP_BIND_MESSAGES_FILE`** parameter.

The **`arsldap.ini`** file contains the following three sections:

`[BIND_MESSAGES]`

`PASSWORD_EXPIRED="/opt/ibm/ondemand/V10.5/config/password_expired.txt"`

`ACCOUNT_LOCKED="/opt/ibm/ondemand/V10.5/config/account_locked.txt"`

`[PASSWORD_EXPIRED]`

`TDS6="Password has expired"`

`AD="data 532"`

`UDEF1=`

`UDEF2=`

`UDEF3=`

`[ACCOUNT_LOCKED]`

`TDS6="Account is locked"`

`AD="data 775"`

`UDEF1=`

`UDEF2=`

`UDEF3=`

The **`BIND_MESSAGES`** section specifies the path to the files containing the user-defined message text that is displayed to users when their LDAP password is about to expire or their account is locked. Generic files are supplied for customization to the specific CMOD environment.

This is an example message, supplied by IBM, that would be displayed to a user:

Your LDAP password has expired and needs to be changed.

`Log into <company intranet> for password setting instructions.`

IBM Tivoli Directory Server Version 6.x and Microsoft Active Directory (AD) can use the entries in the **`PASSWORD_EXPIRED`** and **`ACCOUNT_LOCKED`** sections.

To allow users to enter their own pattern strings for **LDAP** servers that are not directly supported by **IBM CMOD**, these sections also contain three user-defined entries (**UDEFx**).

When an error is returned from the **LDAP** server, **CMOD** reads the **`ARS_LDAP_BIND_MESSAGES_FILE`** containing the filename and the referenced parameters and searches under the two stanzas, [**`PASSWORD_EXPIRED`**] and [**`ACCOUNT_LOCKED`**], for user-defined text that matches the **LDAP** server error.

**CMOD** will then display the text found in the files defined under the [**`BIND_MESSAGES`**] stanza, if a match is found.

When the **`ARS_LDAP_BIND_MESSAGES_FILE`** parameter has no file referenced or is not defined or the **`PASSWORD_EXPIRED`** or **`ACCOUNT_LOCKED`** files do not exist, a default message is displayed as follows:

**`'The server failed while attempting to logon'`** (Additional display information may be returned by the **LDAP** server when the user’s bind operation fails).

**Note:** ***`PASSWORD_EXPIRED`*** *and* ***`ACCOUNT_LOCKED`*** *are the only two error conditions that are handled. Although the section titles are immutable, the pattern strings and message text displayed can be changed for any two error conditions to be user-defined*.

For more details, refer to [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-specifying-arsldapini-file](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-specifying-arsldapini-file)

**TCP/IP tuning for performance:**

This section provides IBM’s recommendations for TCP/IP performance tuning on a Linux server.

The **CMOD** clients and servers communicate with each other by using transactions. The client programs, for example, **arsload**, **arsdoc**, and the **ODWEK** Java APIs, use sockets to communicate with the server and close the sockets after the completion of a transaction. When the **arsload** program is processing data, there are many TCP/IP sockets opened and closed for each transaction to load a file.

When a **Linux** socket is closed by an application, the default time that **Linux** waits is **60** seconds before closing it and returning it for use. During this time, the port that the socket used is placed in the **`TIME_WAIT`** state and is locked. **Linux** also has a default number of **28232** ports that can be used when an application requires a user port from the system.

If the **Linux** socket defaults can’t supply enough ports during the heavy TCP/IP use generated by the **CMOD** server/client transactions, then they require additional tuning.

The number of ports in a **`TIME_WAIT`** state can be monitored by running the following command:

`netstat -an |grep TIME_WAIT`

The number of available ports on **Linux** can be viewed by running the following command:

`sysctl net.ipv4.ip_local_port_range`

The time-out value on Linux can be viewed by running the following command:

`sysctl net.ipv4.tcp_fin_timeout`

(which returns **60** by default).

To avoid **TCP/IP** connection issues, IBM recommends that you change the Linux default values for the following two parameters for systems that run **CMOD** servers, **CMOD** data loading programs, or **ODWEK** Java APIs.

**Note**: *This solution requires adjusting Linux kernel parameters. IBM recommends that you make a note of the original values so you can reset them if necessary.*

To reduce the **timeout wait time** for closed sockets, change the value of the kernel parameter from its default of **60** to a smaller number, such as **30**:

`sysctl -w net.ipv4.tcp_fin_timeout=30`

To increase the maximum number of ports available to applications, change the value of the kernel parameter from its default of **28232** to a wider range, such as **1024** to **65535**:

`sysctl -w net.ipv4.ip_local_port_range=1024 65535`

**Note:** *After making any changes, restart the Linux server for the changes to take effect.*

# [Conclusion](#toc.xhtml_s25a)

In this chapter, we described the step-by-step download, installation, and configuration of the IBM Content Manager OnDemand version **10.5 base** and **Fix Pack 10.5.0.7** upgrade on a **RedHat Linux** version **8.8** server running on a VMware virtual system.

In the next chapter, *Installing Optional Content Manager OnDemand Software on Linux*, we will cover the installation and administration of the supporting optional software components, including the **Db2 databases**, the **PDF Indexing feature**, the **Distribution Facility** feature, and the **Full Text Search** server feature.

# [Points to Remember](#toc.xhtml_s26a)

*   You must have at least **IBM Silver Level PartnerWorld** accreditation to gain free access to the **IBM Software Access Catalog**.
*   After making any changes, restart the **Linux** server for the changes to take effect.
*   The **CMOD** upgrade to **Fix Pack 10.5.0.7** is required to be sure that all the functionality described in this book can be followed (refer to the section “*Fix Pack 10.5.0.7 Installation”* for the installation of this upgrade).
*   The **DB2INSTANCE** value must specify the name of the created **Db2** instance for **CMOD**, which has a default value of **archive.** It should also be noted that the value is case-sensitive.

# [Multiple Choice Questions](#toc.xhtml_s27a)

1.  Which is the main jar file used for the **ODWEK API**?
    1.  `log4j-core-2.20.0.jar`
    2.  `ODApi.jar`
    3.  `gson-2.10.1.jar`
    4.  `log4j-api-2.20.0.jar`
2.  What is the minimum supported version of IBM RedHat Linux RHEL for **CMOD 10.5**?
    1.  8.0
    2.  8.8
    3.  7.7
    4.  7.0
3.  What is the default target installation path for **IBM CMOD 10.5** on a Linux system?
    1.  `/opt/CMOD`
    2.  `/opt/IBM/ondemand/V10.5`
    3.  `/opt/ibm/ondemand/V10.5`
    4.  `/opt/CMOD/linux`
4.  What level of IBM Business Partner do you need to have for free access to the IBM Software Access Catalog?
    1.  Platinum
    2.  Silver
    3.  Gold
    4.  Bronze

# [Answers](#toc.xhtml_s28a)

1.  b
2.  c
3.  c
4.  b

# [Questions](#toc.xhtml_s29a)

1.  Where would you find a comprehensive blog wiki for the IBM CMOD system?
2.  What are the main uses for IBM Content Manager OnDemand?
3.  What would you do before applying an IBM Content Manager OnDemand Fix Pack?

# [Key Terms](#toc.xhtml_s30a)

*   **RHEL:** RedHat Enterprise Linux operating system
*   **JDBC:** A Java Database Connectivity application programming standard interface usually deployed as a JAR library.
*   **AIX:** A series of Unix operating systems developed and sold by IBM for several of its Hardware computer platforms.
*   **LINUX:** A Unix Operating System with a kernel developed initially by a team of Open-Source system programmers, directed by Linus Torvalds.
*   **LDAP:** Lightweight Directory Access Protocol used to validate user and application name security.
*   **UVU:** Authorized User (User value Unit) License.
*   **PVU:** Processor Value Unit License
*   **GSKit:** Linux GSKit - The IBM Global Security Kit (GSKit) provides libraries and utilities for SSL or TLS secure protocol communication.

# [CHAPTER 3](#toc.xhtml_c03)

# [Installing Optional CMOD Software on Linux](#toc.xhtml_c03)

# [Introduction](#toc.xhtml_s31a)

In this chapter, we cover the installation and administration of the supporting optional software components, such as the **Db2** databases, the **PDF** **Indexing feature**, the **Distribution** **Facility feature**, and the **Full Text Search** **server feature**, including the configuration and testing of the **PDF Indexing feature**. We also expand on the use of the Full Text search feature. The Apache Lucene text search engine that is installed is the same as that used for IBM Db2, IBM Content Manager, and IBM FileNet. We have given a working example of the PDF Indexing feature used to process a typical standard PDF Invoice.

For more details, refer to

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-installing-optional-content-manager-ondemand-software](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=linux-installing-optional-content-manager-ondemand-software)

# [Structure](#toc.xhtml_s32a)

In this chapter, we will discuss the following topics:

*   List of Created Db2 Tables for CMOD in the ARCHIVE Database
*   Removing a CMOD Db2 Archive Database
*   Manually Starting and Stopping CMOD Instances
    *   Starting an Instance
    *   Stopping an Instance
    *   Fixing Errors for arssockd load
*   Updating the archive instance ARCHIVE Database
    *   Moving the Database Schema from Root to Archive on Linux
*   Installing the PDF Indexing Feature
*   Installing the Distribution Facility Feature
*   Installing the Full Text Search Server Feature

# [List of Created Db2 Tables for CMOD in the ARCHIVE Database](#toc.xhtml_s33a)

The **Db2 archive** user’s login is used from the **root** user using the **Linux** command:

1.  The **`db2`** **=>** prompt is then invoked using the **Linux** command:

    `[archive@ECMUKDEMO22 ~]$` **`db2`**

    `(c) Copyright IBM Corporation 1993,2007`

    `Command Line Processor for DB2 Client 11.5.7.0`

    `You can issue database manager commands and SQL statements from the command`

    `prompt.` `For example:`

    `db2 => connect to sample`

    `db2 => bind sample.bnd`

    `For general help, type: ?.`

    `For command help, type: ?` `command, where command can be`

    `the first few keywords of a database manager command.` `For example:`

    `?` `CATALOG DATABASE for help on the CATALOG DATABASE command`

    `?` `CATALOG          for help on all of the CATALOG commands.`

    `To exit db2 interactive mode, type QUIT at the command prompt.` `Outside`

    `interactive mode, all commands must be prefixed with 'db2'.`

    `To list the current command option settings, type LIST COMMAND OPTIONS.`

    `For more detailed help, refer to the Online Reference Manual.`

2.  The **`ARCHIVE`** database is connected using the following command:

    `db2 => connect to ARCHIVE`

    `Database Connection Information`

    `Database server        = DB2/LINUXX8664 11.5.7.0`

    `SQL authorization ID   = ARCHIVE`

    `Local database alias   = ARCHIVE`

3.  The 41 **CMOD** schema tables initially created for the **root** schema are listed as follows:

    `db2 => list tables for schema root`

    `Table/View                      Schema          Type  Creation time`

    `------------------------------- ----------------------------------------`

    `ARSAG                   ROOT            T     2024-03-23-14.06.20.611215`

    `ARSAG2FOL               ROOT            T     2024-03-23-14.06.21.000636`

    `ARSAGFLD                ROOT            T     2024-03-23-14.06.21.284591`

    `ARSAGFLDALIAS           ROOT            T     2024-03-23-14.06.21.544937`

    `ARSAGINDEX              ROOT            T     2024-03-23-14.06.21.794336`

    `ARSAGPERMS              ROOT            T     2024-03-23-14.06.22.069910`

    `ARSANN                  ROOT            T     2024-03-23-14.06.22.369763`

    `ARSAPP                  ROOT            T     2024-03-23-14.06.22.702377`

    `ARSAPPUSR               ROOT            T     2024-03-23-14.06.23.007570`

    `ARSCAB                  ROOT            T     2024-03-23-14.06.23.341712`

    `ARSCAB2FOL              ROOT            T     2024-03-23-14.06.23.631425`

    `ARSCABNAMES             ROOT            T     2024-03-23-14.06.23.894434`

    `ARSCABPERMS             ROOT            T     2024-03-23-14.06.24.151855`

    `ARSCFSODWORK            ROOT            T     2024-03-23-14.06.24.405770`

    `ARSCMFEDWORK            ROOT            T     2024-03-23-14.06.24.688719`

    `ARSFOL                  ROOT            T     2024-03-23-14.06.24.954604`

    `ARSFOLFLD               ROOT            T     2024-03-23-14.06.25.177910`

    `ARSFOLFLDUSR            ROOT            T     2024-03-23-14.06.25.380261`

    `ARSFOLNAMES             ROOT            T     2024-03-23-14.06.25.641017`

    `ARSFOLPERMS             ROOT            T     2024-03-23-14.06.25.875560`

    `ARSFTIWORK              ROOT            T     2024-03-23-14.06.26.120926`

    `ARSGROUP                ROOT            T     2024-03-23-14.06.26.393484`

    `ARSHOLD                 ROOT            T     2024-03-23-14.06.26.711936`

    `ARSHOLDMAP              ROOT            T     2024-03-23-14.06.26.927391`

    `ARSHOLDNAMES            ROOT            T     2024-03-23-14.06.27.126041`

    `ARSHOLDPERMS            ROOT            T     2024-03-23-14.06.27.342755`

    `ARSHOLDWORK             ROOT            T     2024-03-23-14.06.27.588936`

    `ARSLOAD                 ROOT            T     2024-03-23-14.06.27.819988`

    `ARSLOADWORK             ROOT            T     2024-03-23-14.06.28.090861`

    `ARSNAMEQ                ROOT            T     2024-03-23-14.06.28.328585`

    `ARSNODE                 ROOT            T     2024-03-23-14.06.28.671627`

    `ARSPRT                  ROOT            T     2024-03-23-14.06.28.996547`

    `ARSPRTOPTS              ROOT            T     2024-03-23-14.06.29.253779`

    `ARSPRTUSR               ROOT            T     2024-03-23-14.06.29.628808`

    `ARSRES                  ROOT            T     2024-03-23-14.06.29.879247`

    `ARSSEG                  ROOT            T     2024-03-23-14.06.30.182943`

    `ARSSET                  ROOT            T     2024-03-23-14.06.30.474452`

    `ARSSYS                  ROOT            T     2024-03-23-14.06.30.705777`

    `ARSUSER                 ROOT            T     2024-03-23-14.06.31.017138`

    `ARSUSRGRP               ROOT            T     2024-03-23-14.06.31.274577`

    `ARSUSRGRPID             ROOT            T     2024-03-23-14.06.31.543090`

    `41 record(s) selected.`

    `db2 =>`

This shows that the **CMOD** tables have all been created with **root** as the schema name, where the debug errors showed that the services were expecting the tables (for example, **`ARSAG`**) to be created with **archive** as the schema for the tables.

In the next section, we demonstrate the procedure we used to change the schema name from **root** to **archive**.

# [Removing a CMOD Db2 Archive Database](#toc.xhtml_s34a)

During the initial installation of the Linux **CMOD** system, we discovered that the recommended **`Db2`** installation using the **root** user caused the first build of the **`ARCHIVE`** database to have a schema of **root**, which, on inspection of the service log files, was found to cause the **CMOD** services to fail because the expected schema for the **`Db2`** tables built in the **`ARCHIVE`** database was **archive**, the database instance owner. We had the following error:

**`ARS0013E`** `DB Error: [IBM][CLI Driver][DB2/LINUXX8664] SQL0204N`**`\"ARCHIVE.ARSAG\"`** `is an undefined name.  SQLSTATE=42704  -- SQLSTATE=42S02, SQLCODE=-204, File=arsag.c, Line=4275", ""], 0x2c85440 /* 69 vars */`

This error was corrected by changing the initial **root** table schema to the **archive** schema.

So, we decided to remove and rebuild the **`ARCHIVE`** database in order to correct the issue, which allowed the tables to be correctly created with a schema of **archive**, which was achieved using the following procedure.

We logged in as the **archive** DB2 instance user and entered the following commands:

`archive@ECMUKDEMO22 ~]$`**`db2 drop database ARCHIVE`**

`DB20000I  The DROP DATABASE command completed successfully.`

`[archive@ECMUKDEMO22 /]$`**`cd arsdb`**

`[archive@ECMUKDEMO22 arsdb]$`**`rm -Rf *.*`**

See [https://cmod.wiki/dox/CMODv10.1/AdministrationGuide.pdf](https://cmod.wiki/dox/CMODv10.1/AdministrationGuide.pdf) for more details (see especially *Chapter 31, ARSDB*).

The following steps were taken to discover and correct a number of errors, which eventually required the Database removal and rebuild, as covered in this section.

# [Manually Starting and Stopping CMOD Instances](#toc.xhtml_s35a)

First, we tried to restart the installed Linux **CMOD** **ARCHIVE** **instance** system following the procedure, as follows.

In the administration documentation, it advises that you must start a **CMOD** instance before clients can connect to databases on the instance.

**Note**: *It should be noted that a* ***CMOD*** *system will support multiple instances, each one can be defined separately in its own section in the* ***`ars.ini`*** *file and is usually referenced in the Linux command line for the* ***CMOD*** *service programs by using the* ***`-I`*** *parameter.*

**Starting an instance:**

1.  Log on as the **root** user or instance owner.
2.  Start the instance:

    `cd /opt/ibm/ondemand/V10.5/bin/`

    `./arssockd archive`

    Where **`archive`** is the name of the instance that you want to start. The name **`archive`** is the value of the **`SRVR_INSTANCE`** parameter in the **`ars.ini`** file.

    The **`arsobjd`** program controls a **Content Manager OnDemand** instance on an object server. **Content Manager OnDemand** programs that work with an instance on an object server will fail if the **`arsobjd`** program is not running on the object server.

    **Note:** *The* ***`arsobjd`*** *program should be started only on object servers that are running on some other workstation than the library server.*

    The following command line is used on Linux to run the **`arsobjd`** program for the **`archive`** instance:

    `[root@ECMUKDEMO22 bin]#` **`/opt/ibm/ondemand/V10.5/bin/arsobjd -I archive -S`**

3.  Use the **`ps`** command to verify that the instance started:

    `ps -eaf|grep ars`

**Stopping an instance:**

1.  Log on as the **root** user or the instance owner.

    **For the Object server:**

    `[root@ECMUKDEMO22 bin]#` **`ps -eaf|grep arsobj`**

    `archive    21822    9162  0 Apr03 pts/2    00:00:01 arsobjd: (accepting)`

    `root      144247   18122  0 05:50 pts/2    00:00:00 grep --color=auto arsobj`

    `[root@ECMUKDEMO22 bin]#`

    `[root@ECMUKDEMO22 bin]#` **`/opt/ibm/ondemand/V10.5/bin/arsobjd -I archive -T`**

    `ARS0352I The arsobjd instance ARCHIVE is terminating`

    `[root@ECMUKDEMO22 bin]#` **`ps -eaf|grep arsobj`**

    `root      144392   18122  0 05:52 pts/2    00:00:00 grep --color=auto arsobj`

    `[root@ECMUKDEMO22 bin]#`

2.  Use the **`arssockd`** command to stop the initial **`arssockd`** process. If there is more than one **`arssockd`** process running, determine the initial **`arssockd`** process. The initial **`arssockd`** process has a status of accepting:

    `ps -ef | grep ars`

    `root 6022 28991 0 60 13:43:03 - 0:00 arssockd: db (USERID)`

    `root 6018 28991 0 60 13:33:03 - 0:00 arssockd: db (idle)`

    `root 6014 28991 0 60 13:30:13 - 0:00 arssockd -arssockd:`

    `(accepting)`

3.  Then stop the accepting process. For example:

    `./arssockd stop 6014`

The initial process and all of its children will be stopped.

**Fixing errors for** **`arssockd`** **load:**

The initial run for the **`arssockd`** program failed with the error **`ARS0160E`**

See [https://cmod.wiki/index.php?title=ARS0160E](https://cmod.wiki/index.php?title=ARS0160E)

(Also [https://cmod.wiki/dox/CMODv8.5/Messages_and_Codes.pdf](https://cmod.wiki/dox/CMODv8.5/Messages_and_Codes.pdf) and [https://cmod.wiki/dox/CMODv9.5/MessagesAndCodes.pdf](https://cmod.wiki/dox/CMODv9.5/MessagesAndCodes.pdf))

**First Error:**

The initial attempt to load **`arssockd`** had errors as follows:

`arssockd (ARCHIVE): 0 ARSOBJD 2 160` **`ARS0160E`** `Unable to load module >/opt/ibm/ondemand/V10.5/bin/exits/arssmtmsm<.` `The return code is 2`

`arssockd (ARCHIVE) ARSMSG 2 147` **`ARS0147E`** `Unable to initialize the server environment.` `The return code is 1`

1.  The IBM documentation advises to check your **`ars.cfg`** file, and if your server is NOT using secondary storage, change the **`ARS_STORAGE_MANAGER`** parameter as follows:

    `ARS_STORAGE_MANAGER=CACHE_ONLY`

2.  Also, check the following **Db2 Linux** commands have been run as the **archive** **Db2** instance:

    `[archive@ECMUKDEMO22 ~]$` **`db2 start database manager`**

    `SQL1026N  The database manager is already active.`

    `[archive@ECMUKDEMO22 ~]$` **`db2 activate database archive`**

    `DB20000I  The ACTIVATE DATABASE command completed successfully.`

**Second Error (after reboot):**

The Linux server was rebooted and now we get another error:

`arsockd (ARCHIVE) ARSMSG 2 154 ARS0154E Unable to establish server communications with network.` `The return code is 2`

***Note****: The* ***`ARSSOCK= debug`*** *parameter in the* ***`ars.cfg`*** *configuration file can help you troubleshoot TCP/IP errors.*

*Ensure that TCP/IP is running, then try the command again*.

The open ports and services can also be checked using the Linux command:

`firewall-cmd --list-all`

# [Updating the archive instance ARCHIVE database](#toc.xhtml_s36a)

The **archive** instance was updated using the **Linux** commands as follows:

(There is a full listing of the **`ars.cfg,`** **`ars.ini`**, and **`ars.dbfs`** file contents in *[Appendix C, List of Configuration Files and Settings](#appc.xhtml)*).

1.  We need to change to the **CMOD** configuration directory using the following command:

    `[archive@ECMUKDEMO22 ~]$` **`cd /opt/ibm/ondemand/V10.5/config`**

2.  Then, we can list the files available for configuration as follows:

    `[archive@ECMUKDEMO22 config]$` **`ls`**

    `ars.az.smp  ars.fs.smp    ars.ini       ars.s3.smp     trace.settings`

    `ars.cache   ars.gcs.smp   arsodf.xml    ars.swift.smp  unzip`

    `ars.cfg     ars.hdfs.smp  arspdsys.bst  arsxform.xml   zip`

    `ars.dbfs    ars.icos.smp  arspdusr.bst  debug`

3.  The configuration files are edited using the **`vi`** **Linux** editor:

    `[archive@ECMUKDEMO22 config]$` **`vi ars.cfg`**

    `[archive@ECMUKDEMO22 config]$` **`vi ars.ini`**

    `[archive@ECMUKDEMO22 config]$` **`vi ars.dbfs`**

4.  Next, we have to change to the **CMOD** **`bin`** directory:

    `[archive@ECMUKDEMO22 config]$` **`cd ../bin`**

5.  Then, we can run the **ARCHIVE** database **CMOD** update program for **Db2**:

    `[archive@ECMUKDEMO22 bin]$` **`./arsdb -I archive -u`**

    `ARS4030I Dropping index root.arsagindex_idx`

    `ARS4026I Creating table root.arsagindex`

    `ARS4126W Table already exists root.arsagindex`

    `ARS4040I Reorganizing table root.arsagindex`

    `ARS4030I Dropping index root.arscab_name_idx`

    `ARS4030I Dropping index root.arscab_cid_idx`

    `ARS4026I Creating table root.arscab`

    `etc`

    `(The other 39 tables and related Indexes were similarly logged as shown above)`

    `Etc…`

    `ARS4034I Creating index root.arsfolnames_fid_idx`

    `ARS4040I Reorganizing table root.arsfolnames`

    `ARS4034I Creating index root.arsholdnames_hid_idx`

    `ARS4040I Reorganizing table root.arsholdnames`

    `ARS4034I Creating index root.arsloadwork_idx`

    `ARS4034I Creating index root.arsloadwork_loadid_idx`

    `ARS4040I Reorganizing table root.arsloadwork`

    `[archive@ECMUKDEMO22 bin]$`

# [Moving the Database Schema from root to archive on Linux](#toc.xhtml_s37a)

The following procedure was used to rebuild the **CMOD Db2 ARCHIVE** database to change the 41 database tables from the **root** schema to the **archive** schema.

The **CMOD ARCHIVE** database instance was started using the **`arsdb`** program as follows:

(Starting from the **CMOD** **config** directory)

`[archive@ECMUKDEMO22 config]$` **`../bin/arsdb -gkv`**

`ARS4015I Starting the DB2 ARCHIVE database instance`

`ARS4078I The ARCHIVE instance has already been started`

`ARS4017I Activating the DB2 ARCHIVE database`

`[archive@ECMUKDEMO22 config]$`

See:

[https://www.ibm.com/support/pages/simple-way-change-schema-names-db2-linux-unix-and-windows](https://www.ibm.com/support/pages/simple-way-change-schema-names-db2-linux-unix-and-windows)

1.  First, we create an **`outputfile.sql`** **SQL** file to contain the **DDL** for the table structures, with the schema to change:

    `db2look -d ARCHIVE -e -o outputfile.sql`

    The output from this command is displayed in *[Figure 3.1](#c03.xhtml_fig3_1)*:

    ![](images/Figure3.1.jpg)

    **Figure 3.1:** The ***db2look*** command is used to export the build sql for the tables

2.  In the **`outputfile.sql`** file, we need to find and change the **root** schema to the **archive** schema name. We use the Linux text editor, **`vi outputfile.sql`**, and edit the file by using the following **`vi`** command:

    `:1,$s/ROOT   /ARCHIVE/g`

    This command will search and replace all the **ROOT** schema names for the tables to the **ARCHIVE** schema.

3.  Next, we run the **`db2move`** command to create all the files we need:

    `db2move ARCHIVE export`

    This will create several files, including a **`db2move.lst`** file, in the current directory.

    `[archive@ECMUKDEMO22 config]$` **`db2move ARCHIVE export`**

    `Application code page not determined, using ANSI codepage 1208`

    `*****  DB2MOVE  *****`

    `Action:  EXPORT`

    `Start time:  Thu Mar 28 13:10:59 2024`

    `Connecting to database ARCHIVE ...` `successful!  Server : DB2 Common Server V11.5.7`

    `Binding package automatically ...` `/home/archive/sqllib/bnd/db2common.bnd ...` `successful!`

    `Binding package automatically ...` `/home/archive/sqllib/bnd/db2move.bnd ...` `successful!`

    `EXPORT:      0 rows from table "ROOT    "."ARSAG"`

    `EXPORT:      0 rows from table "ROOT    "."ARSAG2FOL"`

    `EXPORT:      0 rows from table "ROOT    "."ARSAGFLD"`

    `EXPORT:      0 rows from table "ROOT    "."ARSAGFLDALIAS"`

    `EXPORT:      0 rows from table "ROOT    "."ARSAGINDEX"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSAGINDEX"`

    `EXPORT:      0 rows from table "ROOT    "."ARSAGPERMS"`

    `EXPORT:      0 rows from table "ROOT    "."ARSANN"`

    `EXPORT:      0 rows from table "ROOT    "."ARSAPP"`

    `EXPORT:      0 rows from table "ROOT    "."ARSAPPUSR"`

    `EXPORT:      0 rows from table "ROOT    "."ARSCAB"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSCAB"`

    `EXPORT:      0 rows from table "ROOT    "."ARSCAB2FOL"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSCAB2FOL"`

    `EXPORT:      0 rows from table "ROOT    "."ARSCABNAMES"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSCABNAMES"`

    `EXPORT:      0 rows from table "ROOT    "."ARSCABPERMS"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSCABPERMS"`

    `EXPORT:      0 rows from table "ROOT    "."ARSCFSODWORK"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSCFSODWORK"`

    `EXPORT:      0 rows from table "ROOT    "."ARSCMFEDWORK"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSCMFEDWORK"`

    `EXPORT:      0 rows from table "ROOT    "."ARSFOL"`

    `EXPORT:      0 rows from table "ROOT    "."ARSFOLFLD"`

    `EXPORT:      0 rows from table "ROOT    "."ARSFOLFLDUSR"`

    `EXPORT:      0 rows from table "ROOT    "."ARSFOLNAMES"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSFOLNAMES"`

    `EXPORT:      0 rows from table "ROOT    "."ARSFOLPERMS"`

    `EXPORT:      0 rows from table "ROOT    "."ARSFTIWORK"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSFTIWORK"`

    `EXPORT:      0 rows from table "ROOT    "."ARSGROUP"`

    `EXPORT:      0 rows from table "ROOT    "."ARSHOLD"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSHOLD"`

    `EXPORT:      0 rows from table "ROOT    "."ARSHOLDMAP"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSHOLDMAP"`

    `EXPORT:      0 rows from table "ROOT    "."ARSHOLDNAMES"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSHOLDNAMES"`

    `EXPORT:      0 rows from table "ROOT    "."ARSHOLDPERMS"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSHOLDPERMS"`

    `EXPORT:      0 rows from table "ROOT    "."ARSHOLDWORK"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSHOLDWORK"`

    `EXPORT:      0 rows from table "ROOT    "."ARSLOAD"`

    `EXPORT:      0 rows from table "ROOT    "."ARSLOADWORK"`

    `EXPORT:      0 rows from table "ARCHIVE "."ARSLOADWORK"`

    `EXPORT:      0 rows from table "ROOT    "."ARSNAMEQ"`

    `EXPORT:      1 rows from table "ROOT    "."ARSNODE"`

    `EXPORT:      0 rows from table "ROOT    "."ARSPRT"`

    `EXPORT:      0 rows from table "ROOT    "."ARSPRTOPTS"`

    `EXPORT:      0 rows from table "ROOT    "."ARSPRTUSR"`

    `EXPORT:      0 rows from table "ROOT    "."ARSRES"`

    `EXPORT:      0 rows from table "ROOT    "."ARSSEG"`

    `EXPORT:      1 rows from table "ROOT    "."ARSSET"`

    `EXPORT:      1 rows from table "ROOT    "."ARSSYS"`

    `EXPORT:      1 rows from table "ROOT    "."ARSUSER"`

    `EXPORT:      0 rows from table "ROOT    "."ARSUSRGRP"`

    `EXPORT:      0 rows from table "ROOT    "."ARSUSRGRPID"`

    `EXPORT:    206 rows from table "SYSTOOLS"."HMON_ATM_INFO"`

    `EXPORT:      0 rows from table "SYSTOOLS"."HMON_COLLECTION"`

    `EXPORT:      5 rows from table "SYSTOOLS"."POLICY"`

    `Disconnecting from database ...` `successful!`

    `End time:  Thu Mar 28 13:11:12 2024`

    `[archive@ECMUKDEMO22 config]$`

4.  Now, we have to edit the generated **`db2move.lst`** file and change the schema name from **`ROOT`** to the new **`ARCHIVE`** name Using the **vi** editor command:

    **`:1,$s/ROOT   /ARCHIVE/g`**

5.  Now, we can drop the existing user tables (this step is used for renaming the schema within the same database) using the following **db2** commands:
    1.  First, we launch the **`db2 =>`** prompt using the Linux command **`db2`**:

        `[archive@ECMUKDEMO22 config]$` **`db2`**

        `(c) Copyright IBM Corporation 1993,2007`

        `Command Line Processor for DB2 Client 11.5.7.0`

        `You can issue database manager commands and SQL statements from the command`

        `prompt.` `For example:`

        `db2 => connect to sample`

        `db2 => bind sample.bnd`

        `For general help, type: ?.`

        `For command help, type: ?` `command, where command can be`

        `the first few keywords of a database manager command.` `For example:`

        `?` `CATALOG DATABASE for help on the CATALOG DATABASE command`

        `?` `CATALOG          for help on all of the CATALOG commands.`

        `To exit db2 interactive mode, type QUIT at the command prompt.` `Outside`

        `interactive mode, all commands must be prefixed with 'db2'.`

        `To list the current command option settings, type LIST COMMAND OPTIONS.`

        `For more detailed help, refer to the Online Reference Manual.`

    2.  Now, we can connect to the **CMOD ARCHIVE Db2** database using the command:

        `db2 =>` **`connect to ARCHIVE`**

        `Database Connection Information`

        `Database server        = DB2/LINUXX8664 11.5.7.0`

        `SQL authorization ID   = ARCHIVE`

        `Local database alias   = ARCHIVE`

    3.  We can now call the **Db2** system stored procedure as follows:

        **`db2 => CALL SYSPROC.ADMIN_DROP_SCHEMA('ROOT', NULL, 'ERRORSCHEMA', 'ERRORTABLE')`**

        `Value of output parameters`

        `--------------------------`

        `Parameter Name  : ERRORTABSCHEMA`

        `Parameter Value : -`

        `Parameter Name  : ERRORTAB`

        `Parameter Value : -`

        `Return Status = 0`

6.  Then, we can exit the **`db2 =>`** command prompt using the **`quit`** command:

    `db2 => quit`

7.  We can now execute the **DDL SQL** to rebuild the **CMOD** database with the **ARCHIVE** schema for all the tables.

    `db2 -tvf outputfile.sql`

    (This runs the output file generated by the **db2look** command to recreate the tables with the new **ARCHIVE** schema name)

8.  Next, we must import the exported database table rows back into the **CMOD ARCHIVE** database:

    `db2move ARCHIVE import`

    (Run to import the data into the tables.)

9.  At this point, we retried the **`arssockd`** program with a **`strace`** command set using the Linux commands as follows:

    `rm strace.out`

    `strace -s 256 -f /opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S 2>strace.out`

    This then gave us the error as follows:

    `ARS0154E Unable to establish server communications with network.` `The return code is 2"`

10.  We checked that we had started the **Db2** database as follows:

    `[root@ECMUKDEMO22 ~]#` **`su - archive`**

    `Last login: Thu Mar 28 14:01:15 PDT 2024 on pts/0`

    `[archive@ECMUKDEMO22 ~]$` **`db2start`**

    `03/28/2024 14:18:14     0   0   SQL1026N  The database manager is already active.`

    `SQL1026N  The database manager is already active.`

    `[archive@ECMUKDEMO22 ~]$` **`db2 activate database archive`**

    `DB20000I  The ACTIVATE DATABASE command completed successfully.`

    `[archive@ECMUKDEMO22 ~]$`

11.  The IBM documentation suggested that we run the **`arsdb -u`** update command as follows, **without the** **`ARS_ORIGINAL_CODEPAGE`** **in the** **`ars.cfg`**, for the setting of the **`ARS_ORIGINAL_CODEPAGE`** page for the command:

    `./arsdb -u -I ARCHIVE`

    After the removal of the line, **`ARS_ORIGINAL_CODEPAGE=1208`**

    The command was then repeated as follows:

    `[archive@ECMUKDEMO22 bin]$` **`./arsdb -u -I ARCHIVE`**

    `ARS4012E Unable to initialize environment.` `The return code is -1\.` `If this is a new (created in version 8.5 or later) instance, then define` **`ARS_ORIGINAL_CODEPAGE=1208`** `in` **`ars.cfg`**`.` `Otherwise, if this is an existing instance (created prior to 8.5), then define ARS_ORIGINAL_CODEPAGE=1208 in ars.cfg.` `Once set, ARS_ORIGINAL_CODEPAGE must never change.`

    `[archive@ECMUKDEMO22 bin]$`

12.  The PDF documentation, as follows, was found, which contains the common error codes:

    [https://audentia-gestion.fr/IBM/PDF/sc271161.pdf](https://audentia-gestion.fr/IBM/PDF/sc271161.pdf)

    The debug flag gave the error as follows:

    `Thu Mar 28 14:29:56 2024: OnDemand(2378) -> bind errno = 98 rc = -1`

13.  Using **Co-pilot** to check this, we got:

    Copilot

    The error message you’re encountering, **`"cmod arssockd error: ondemand(2378) -> bind errno = 98 rc = -1"`**, is related to the **Content Manager OnDemand (CMOD)** system. Let’s break it down:

    1.  **CMOD (Content Manager OnDemand)**: CMOD is an enterprise document management system that allows organizations to store, manage, and retrieve large volumes of documents efficiently.
    2.  **`arssockd`**: This is the **ARS Socket Daemon**, a critical component of CMOD. It handles communication between clients (such as users or applications) and the CMOD server.
    3.  **Error Details**:
        1.  **`ondemand(2378)`**: Refers to the specific process or instance of CMOD. The number 2378 is likely the process ID (PID) associated with this instance.
        2.  **`bind errno = 98 rc = -1`**: Let’s break this down further:
            *   **`bind`**: The **bind** function is used to associate a socket (communication endpoint) with a specific network address and port number.
            *   **`errno = 98`**: The error number 98 corresponds to **“Address already in use”**. This means that the specified port is already being used by another process.
            *   **`rc = -1`**: Indicates that the **bind** operation failed.

    **Possible Causes and Solutions:**

    1.  **Port Conflict**: The most common reason for this error is that the port specified for CMOD’s **`arssockd`** is already in use by another process. To resolve this:
        1.  Check if any other application or service is using the same port (port **2378** in this case).
        2.  If so, either stop the conflicting process or configure **CMOD** to use a different port.
    2.  **`SO_REUSEADDR`** **and** **`SO_REUSEPORT`**: You can try using both **`SO_REUSEADDR`** and **`SO_REUSEPORT`** socket options to allow reusing the address and port. Here’s an example in C++:
        *   const int trueFlag = 1;
        *   if (setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &trueFlag, sizeof(int)) < 0)
        *   error(“Failure”);
        *   // You can use reuse Port in a similar way.
14.  This suggested we have a port conflict, or firewall permission issue, which we can check using the commands as follows:

    `[root@ECMUKDEMO22 ~]#` **`telnet ecmukdemo22 1445`**

    `Trying 192.168.50.134...`

    `telnet: connect to address 192.168.50.134:` **`Connection refused`**

15.  We can add the following ports to the Linux Firewall:

    `[root@ECMUKDEMO22 ~]#`

    **`firewall-cmd --zone=public --permanent --add-port=1445/tcp`**

    **`firewall-cmd --reload`**

    **`firewall-cmd --zone=public --permanent --add-port=2378/tcp`**

    **`firewall-cmd --reload`**

    **`firewall-cmd --zone=public --permanent --add-port=50001/tcp`**

    **`firewall-cmd --reload`**

16.  The final changes to allow the correct running of the **`arssockd`** program on the **Linux** server required the installation of additional libraries, which are covered in *[Chapter 4, Installing the Upgraded Linux GSKit and Supporting Libraries](#c04.xhtml).*

# [Installing the PDF Indexing Feature](#toc.xhtml_s38a)

The IBM documentation for the feature can be found at **“PDF indexer - IBM Documentation”:**

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=ondemand-pdf-indexer](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=ondemand-pdf-indexer)

The use of the PDF Indexer is described in the following link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=data-using-pdf-indexer](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=data-using-pdf-indexer)

(Both links were last updated on **2024-04-24**, at the time of writing).

In addition, there is a Wiki reference link to a PDF document (*Chapter 19, ARSPDUMP reference*) as follows:

[https://cmod.wiki/dox/CMODv9.0/IndexingReference.pdf](https://cmod.wiki/dox/CMODv9.0/IndexingReference.pdf)

1.  First, we need to download the installation program, starting with the link:

    [https://partnerportal.ibm.com/registration/](https://partnerportal.ibm.com/registration/), and then enter the Log in required, as shown in *[Figure 3.2](#c03.xhtml_fig3_2)*:

    ![](images/Figure3.2.jpg)

    **Figure 3.2:** Enter the Log in for the IBM PartnerWorld Portal

2.  The **IBM PartnerWorld Portal** password is prompted for, as illustrated in *[Figure 3.3](#c03.xhtml_fig3_3)*:

    ![](images/Figure3.3.jpg)

    **Figure 3.3:** The ***IBM PartnerWorld Portal*** password is prompted for

3.  The highlighted option can be selected if the logon is not associated with a Registered **IBM PartnerWorld Business Partner** company, as highlighted in *[Figure 3.4](#c03.xhtml_fig3_4):*

    ![](images/Figure3.4.jpg)

    **Figure 3.4:** The highlighted option can be selected if the logon is not associated with a Registered ***IBM PartnerWorld Business Partner*** company

4.  The highlighted option is then selected, as shown in *[Figure 3.5](#c03.xhtml_fig3_5):*

    ![](images/Figure3.5.jpg)

    **Figure 3.5:** The highlighted link, “***Go to the IBM Partner Portal***”, is selected

5.  The **`Explore Benefits`** link in the **`Silver tier in IBM Partner Plus`** notification is clicked, as shown in *[Figure 3.6](#c03.xhtml_fig3_6):*

    ![](images/Figure3.6.jpg)

    **Figure 3.6:** The ***Explore Benefits*** link in the Silver tier in IBM Partner Plus notification is clicked

6.  The highlighted **`Software Access Catalog`** link in the **`Benefits`** node is clicked, as shown in *[Figure 3.7](#c03.xhtml_fig3_7)*:

    ![](images/Figure3.7.jpg)

    **Figure 3.7:** The highlighted Software Access Catalog link in the Benefits node is clicked

7.  The **`Find by Text`** page of the Software Access Catalog page is scrolled down, as shown in *[Figure 3.8](#c03.xhtml_fig3_8):*

    ![](images/Figure3.8.jpg)

    **Figure 3.8:** The Find by Text page of the Software Access Catalog page is scrolled down

8.  The search text **`"Content Manager OnDemand PDF Indexing"`** is entered to display the drop-down list of matching software packages, from which we selected the highlighted package **`"IBM Content Manager OnDemand PDF Indexer V10.5 Multilingual Multiplatform eAssembly"`**, as shown in *[Figure 3.9](#c03.xhtml_fig3_9)*:

    ![](images/Figure3.9.jpg)

    **Figure 3.9:** The search text “***Content Manager OnDemand PDF Indexing***” is entered to display the drop-down list of matching software packages

9.  The **`"IBM Content Manager OnDemand PDF Indexer V10.5 Multilingual Multiplatform eAssembly"`** (Part number **`CC4JGML`**) is ticked and the **`I agree`** radio button is selected, as highlighted in *[Figure 3.10](#c03.xhtml_fig3_10)*:

    ![](images/Figure3.10.jpg)

    **Figure 3.10:** The “***IBM Content Manager OnDemand PDF Indexer V10.5 Multilingual Multiplatform eAssembly” (Part number* ***CC4JGML****)is ticked and the* ***I agree*** *radio button selected***

10.  The **`View details`** link was selected, as highlighted, because we noticed that the **`Size (MB)`** column was referenced as **Mbytes**. This would make the software download size (displayed size of **`156,989,440`**) nearly **157** Terabytes (which we do not have the disk space capacity for!), as shown in *[Figure 3.11](#c03.xhtml_fig3_11)*:

    ![](images/Figure3.11.jpg)

    **Figure 3.11:** The ***View details*** link was selected as highlighted to verify the ***File Size*** of the package

11.  The **`View details`** link displays the actual **`File size`** of **`156,989,440`**, which we can confirm is **not Mbytes**, but **bytes**, as highlighted in *[Figure 3.12](#c03.xhtml_fig3_12)*:

    ![](images/Figure3.12.jpg)

    **Figure 3.12:** The ***View details*** link displays the actual ***File size*** of 156,989,440 ***bytes***

12.  The **`I agree`** radio button must be selected after reading and agreeing to the **License Agreement** link text, in order to be able to download the **`IBM CMOD PDF Indexer`** software package, using the **`Download now`** command button, as highlighted in *[Figure 3.13](#c03.xhtml_fig3_13):*

    ![](images/Figure3.13.jpg)

    **Figure 3.13:** The ***I agree*** radio button must be selected after reading and agreeing to the ***License agreement*** text

13.  The **`Open IBM Download Director`** command button is selected, as shown in *[Figure 3.14](#c03.xhtml_fig3_14):*

    ![](images/Figure3.14.jpg)

    **Figure 3.14:** The ***Open IBM Download Director*** command button is selected

14.  The **`Run`** command button is clicked to launch the **`IBM Download Director`** program, as shown in *[Figure 3.15](#c03.xhtml_fig3_15)*:

    ![](images/Figure3.15.jpg)

    **Figure 3.15:** The ***Run*** command button is clicked to launch the ***IBM Download Director*** program

15.  The status bar of the download of **`IBM_CONTENT_MANAGER_ONDEMAND_PDF_.tar`** is displayed, as shown in *[Figure 3.16](#c03.xhtml_fig3_16)*:

    ![](images/Figure3.16.jpg)

    **Figure 3.16:** The status bar of the download of ***`IBM_CONTENT_MANAGER_ONDEMAND_PDF_.tar`*** is displayed

16.  The **`Details`** command button is clicked to display the download software package details, as highlighted in *[Figure 3.17](#c03.xhtml_fig3_17)*:

    ![](images/Figure3.17.jpg)

    **Figure 3.17:** The ***Details*** command button is clicked to display the download software package details

17.  The three additional **CMOD** downloaded packages are copied from the client’s Windows machine to the Windows server VMware mapped **`Installs`** folder for copying to the RedHat **Linux** virtual system, as illustrated in *[Figure 3.18](#c03.xhtml_fig3_18):*

    ![](images/Figure3.18.jpg)

    **Figure 3.18:** The three additional ***CMOD*** downloaded packages are copied from the client’s Windows machine

    The copied software packages are shown on the Windows server, as highlighted in *[Figure 3.19](#c03.xhtml_fig3_19):*

    ![](images/Figure3.19.jpg)

    **Figure 3.19:** The copied software packages shown on the Windows server

18.  The following Linux commands are run in the command window, logged on as the **root** user:

    `cd /opt`

    `mkdir PDFIndexing`

    `chmod 755 PDFIndexing`

    `cd PDFIndexing/`

    `cp /mnt/hgfs/Installs/IBM_CONTENT_MANAGER_ONDEMAND_PDF_.tar .`

    These commands copy the **`IBM_CONTENT_MANAGER_ONDEMAND_PDF_.tar`** from a Windows **`Installs`** directory to the Linux **`/opt/PDFIndexing`** directory we created, as illustrated in *[Figure 3.20](#c03.xhtml_fig3_20)*:

    ![](images/Figure3.20.jpg)

    **Figure 3.20:** Copy the ***IBM_CONTENT_MANAGER_ONDEMAND_PDF_.tar*** from a Windows ***Installs*** directory to the Linux ***/opt/PDFIndexing*** directory

19.  The **`tar -xvf IBM_CONTENT_MANAGER_ONDEMAND_PDF_.tar Linux`** command is used to unpack the **PDF Indexing feature** installation files, as highlighted in *[Figure 3.21](#c03.xhtml_fig3_21):*

    ![](images/Figure3.21.jpg)

    **Figure 3.21:** The ***tar -xvf IBM_CONTENT_MANAGER_ONDEMAND_PDF_.tar*** ***Linux*** command is used to unpack the ***PDF Indexing feature***

20.  We can now read the **`readme.txt`** file using the **vi** editor, as shown in *[Figure 3.22](#c03.xhtml_fig3_22):*

    ![](images/Figure3.22.jpg)

    **Figure 3.22:** We can now read the ***readme.txt*** file using the ***vi*** editor

21.  For the command-line version, you can use the Linux command to install the **Content Manager OnDemand** **PDF Indexing** feature as follows:

    `./odpdflinux.bin -i console`

    Or for the graphical user interface, we used:

    `./odpdflinux.bin`

    We must first change the security as follows:

    `chmod 775 odpdflinux.bin`

    As illustrated in *[Figure 3.23](#c03.xhtml_fig3_23)*:

    ![](images/Figure3.23.jpg)

    **Figure 3.23:** We run the ***./odpdflinux.bin*** program to install the ***CMOD*** PDF Indexing feature

22.  The **`IBM OnDemand PDF Indexing Feature V10.5`** splash screen is displayed, and we can select the language (Default **`English`**) and then click the **`OK`** command button, as highlighted in *[Figure 3.24](#c03.xhtml_fig3_24)*:

    ![](images/Figure3.24.jpg)

    **Figure 3.24:** The ***IBM OnDemand PDF Indexing Feature V10.5*** splash screen is displayed

23.  The License agreement can be scrolled through and printed off, and then the **`I accept`** radio button must be selected, and the **`N``ext`** command button clicked, as shown in *[Figure 3.25](#c03.xhtml_fig3_25):*

    ![](images/Figure3.25.jpg)

    **Figure 3.25:** The ***I accept*** radio button must be selected and the ***Next*** command button clicked

24.  The summary details are displayed, and we can now click on **`Install`**, as shown in *[Figure 3.26](#c03.xhtml_fig3_26):*

    ![](images/Figure3.26.jpg)

    **Figure 3.26:** The summary details are displayed and we can now click on ***Install***

25.  The **`IBM OnDemand PDF Indexing Feature V10.5`** is successfully installed, and we can click the **Done** command button to exit the **InstallAnywhere** program, as shown in *[Figure 3.27](#c03.xhtml_fig3_27)*:

    ![](images/Figure3.27.jpg)

    **Figure 3.27:** The ***IBM OnDemand PDF Indexing Feature V10.5*** is successfully installed and we can click ***Done***

26.  The **`./arspdump`** program is run just to display the available parameters, as shown in *[Figure 3.28](#c03.xhtml_fig3_28)*:

    ![](images/Figure3.28.jpg)

    **Figure 3.28:** The **`./arspdump`** program is run just to display the available parameters

27.  The **Invoice** PDF test data files, **`invoice_2017-*.pdf`**, are copied to a **Linux** folder, **`/opt/TestData`**, from the mapped Windows server **`/mnt/hgfs/Installs`** folder, as highlighted in *[Figure 3.29](#c03.xhtml_fig3_29)*:

    ![](images/Figure3.29.jpg)

    **Figure 3.29:** The ***Invoice*** pdf test data files, ***invoice_2017-*.pdf***, are copied to a ***Linux*** folder, ***`/opt/TestData`***

# [Running the arspdump Program](#toc.xhtml_s39a)

The example Invoice PDF copied was processed as follows:

The program outputs a row for each text string, which contains the *x,y* coordinates for a box overlaid over the text string (upper left, lower right).

(We have selected just the output lines with fields of interest from our single-page invoice example)

`[root@ECMUKDEMO22 bin]#` **`./arspdump -f "/opt/TestData/invoice_2017-06-04`** **`11_30_53.503.pdf"`**

`ARS4901I` **`/opt/TestData/invoice_2017-06-04 11_30_53.503.pdf`**

`ARS4931I Number of Pages = 1`

`ARS4930I WordFinder version: 3`

`ARS4926I ------------- Page 1 -------------`

**`Description`**

`ul.h = 0.58 ul.v = 3.67 lr.h = 1.53 lr.v = 3.90`

**`Quantity`**

`ul.h = 3.63 ul.v = 3.67 lr.h = 4.33 lr.v = 3.90`

**`Price`**

`ul.h = 5.35 ul.v = 3.67 lr.h = 5.78 lr.v = 3.90`

**`VAT`**

`ul.h = 6.68 ul.v = 3.67 lr.h = 7.04 lr.v = 3.90`

**`GBP14.99`**

`ul.h = 5.35 ul.v = 4.09 lr.h = 6.15 lr.v = 4.32`

**`GBP3.00`**

`ul.h = 6.68 ul.v = 4.09 lr.h = 7.38 lr.v = 4.32`

`---------------------------------------------------`

**`Invoice`**

`ul.h = 3.63 ul.v = 4.50 lr.h = 4.23 lr.v = 4.74`

**`Total:`**

`ul.h = 4.26 ul.v = 4.50 lr.h = 4.74 lr.v = 4.74`

**`GBP17.99`**

`ul.h = 5.35 ul.v = 4.50 lr.h = 6.15 lr.v = 4.73`

**`THEFORMATIONSCOMPANY.`**

`ul.h = 2.75 ul.v = 6.58 lr.h = 4.84 lr.v = 6.78`

**`LTD`**

`ul.h = 5.20 ul.v = 6.58 lr.h = 5.50 lr.v = 6.78`

**`Date:`**

`ul.h = 4.19 ul.v = 2.23 lr.h = 4.61 lr.v = 2.46`

**`Invoice`**

`ul.h = 3.37 ul.v = 2.62 lr.h = 3.92 lr.v = 2.85`

**`Number:`**

`ul.h = 3.95 ul.v = 2.62 lr.h = 4.61 lr.v = 2.85`

**`04-`**

`ul.h = 4.91 ul.v = 2.00 lr.h = 5.17 lr.v = 2.23`

**`06-`**

`ul.h = 5.15 ul.v = 2.00 lr.h = 5.41 lr.v = 2.23`

**`2017`**

`ul.h = 5.39 ul.v = 2.00 lr.h = 5.79 lr.v = 2.23`

**`371858`**

`ul.h = 4.91 ul.v = 2.40 lr.h = 5.49 lr.v = 2.62`

**`VAT`**

`ul.h = 3.32 ul.v = 11.03 lr.h = 3.63 lr.v = 11.23`

**`Number:`**

`ul.h = 3.65 ul.v = 11.03 lr.h = 4.23 lr.v = 11.23`

**`978`**

`ul.h = 4.26 ul.v = 11.03 lr.h = 4.52 lr.v = 11.23`

**`1482`**

`ul.h = 4.54 ul.v = 11.03 lr.h = 4.89 lr.v = 11.23`

**`73`**

`ul.h = 4.91 ul.v = 11.03 lr.h = 5.10 lr.v = 11.23`

`[root@ECMUKDEMO22 bin]#`

Then, we proceed with the second stage of the procedure, creating the indexing parameters using the administrative client.

(See also, [https://www.ibm.com/docs/en/cmofm/9.5.0?topic=indexer-how-create-indexing-parameters](https://www.ibm.com/docs/en/cmofm/9.5.0?topic=indexer-how-create-indexing-parameters))

We can now create the **TRIGGER** and **FIELD** parameters using the *x,y* coordinates, page number, and string values listed in the output from the **`arspdump`** program.

The detailed formats of the **TRIGGER, FIELD**, and **INDEX** for indexing information are described in detail in the following link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=data-indexing-parameters](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=data-indexing-parameters)

The third stage of the procedure uses a program, **`arspdoci`**, which can be used to index a PDF file. The **`arsload`** program calls the **`arspdoci`** program for PDF document types when the PDF indexer is used.

The **`arspdoci`** program uses the locations of text strings, which we created above, with the **`arspdump`** program.

The **Field Index** syntax examples are given in the following link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=pip-field](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=pip-field)

The **CMOD** administrative client provides an edit window you can use to enter and maintain indexing parameters for the application.

# [Installing the Distribution Facility Feature](#toc.xhtml_s40a)

There is a link, as follows, which describes the **IBM OnDemand Distribution Facility** architecture, **“ODF architecture - IBM Documentation”:**

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=introduction-odf-architecture](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=introduction-odf-architecture)

The OnDemand Distribution Facility (ODF) is used to automatically group reports and sections of reports and distribute the resulting reports to multiple users. ODF report distributions can be printed or created as an output file, or they can even be emailed as an attachment.

The ODF report program can retrieve reports that are stored in a Content Manager OnDemand server on any of the operating systems that are supported by Content Manager OnDemand. The **`arsodf`** distribution processing program is launched and uses input from the **`arsload`** process to create the distribution output. Distributions can be a single report or multiple reports that are grouped together, and they can generate email attachments, files, or print output. There are also user exit programs available, which allow for special handling of distributions with unique requirements.

The installation tar file is downloaded by logging in to the IBM website, as shown in the previous section with screenshots from *[Figure 3.2](#c03.xhtml_fig3_2)* to *[Figure 3.8](#c03.xhtml_fig3_8)*. Then, the **IBM OnDemand Distribution Facility** is searched for, as illustrated in *[Figure 3.30](#c03.xhtml_fig3_30)*:

![](images/Figure3.30.jpg)

**Figure 3.30:** The ***IBM OnDemand Distribution Facility*** is searched for

The **`IBM Content Manager OnDemand Distribution Facility V10.5 Mutilingual Multiplatform`** (Part Number, **CC4JHML**) installation tar file can be selected and the **`I agree`** radio button is selected to allow the **`Download`**, after reviewing the IBM **`License agreement`** link, as shown in *[Figure 3.31](#c03.xhtml_fig3_31)*:

![](images/Figure3.31.jpg)

**Figure 3.31:** The ***IBM Content Manager OnDemand Distribution Facility V10.5 Multilingual Multiplatform*** (Part Number, ***CC4JHML***) installation tar file can be selected and the ***I agree*** radio button selected

The **`Download Director`** **`Details`** command shows the downloaded **`IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar`** file, as illustrated in *[Figure 3.32](#c03.xhtml_fig3_32)*:

![](images/Figure3.32.jpg)

**Figure 3.32:** The ***Download Director*** ***Details*** command shows the downloaded ***IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar*** file

The following commands were used to copy the downloaded **`IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar`** installation file from the Windows Installs directory to the Linux **`/opt/DistributionFacility`** folder we created:

`[root@ECMUKDEMO22 ~]# cd /opt`

`[root@ECMUKDEMO22 opt]# mkdir DistributionFacility`

`[root@ECMUKDEMO22 opt]# chmod 755 DistributionFacility/`

`[root@ECMUKDEMO22 opt]# cd DistributionFacility/`

`[root@ECMUKDEMO22 DistributionFacility]# cp /mnt/hgfs/Installs/IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar .`

`[root@ECMUKDEMO22 DistributionFacility]#`

As illustrated in *[Figure 3.33](#c03.xhtml_fig3_33)*:

![](images/Figure3.33.jpg)

**Figure 3.33:** The downloaded ***IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar*** installation file is copied from the Windows ***Installs*** directory to the Linux ***/opt/DistributionFacility*** folder

The copied **`IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar`** is unpacked using the command:

`tar -xvf IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar`

As highlighted in *[Figure 3.34](#c03.xhtml_fig3_34):*

![](images/Figure3.34.jpg)

**Figure 3.34:** The copied ***IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar*** file is unpacked using the command:***tar -xvf IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar***

For the command-line version, you can use the Linux command to install the **Content Manager OnDemand Distribution Facility** feature as follows:

`./ododflinux.bin -i console`

Or for the graphical user interface, we used:

`./ododflinux.bin`

As illustrated in *[Figure 3.35](#c03.xhtml_fig3_35)*:

![](images/Figure3.35.jpg)

**Figure 3.35:** The ***Install Anywhere*** graphical user interface is launched using ***./ododflinux.bin***

The IBM OnDemand Distribution Feature V10.5 Graphical Installation splash screen is displayed, and we select the language and click **`OK`**, as shown in *[Figure 3.36](#c03.xhtml_fig3_36):*

![](images/Figure3.36.jpg)

**Figure 3.36:** The ***IBM OnDemand Distribution Feature V10.5*** Graphical Installation splash screen is displayed

The **`IBM OnDemand Distribution Feature V10.5.0.0`** install details are displayed and the **`Next`** command button is selected, as shown in *[Figure 3.37](#c03.xhtml_fig3_37):*

![](images/Figure3.37.jpg)

**Figure 3.37:** The ***IBM OnDemand Distribution Feature V10.5.0.0*** install details are displayed

The **`IBM OnDemand Distribution Feature V10.5`** License agreement is scrolled down to view. Then, **`I accept`** radio button is selected and **`Next`** is clicked, as shown in *[Figure 3.38](#c03.xhtml_fig3_38)*:

![](images/Figure3.38.jpg)

**Figure 3.38:** The ***IBM OnDemand Distribution Feature V10.5*** License agreement is scrolled down to view, and ***I accept*** radio button selected and ***Next*** clicked

The **`Install`** command button is clicked, as shown in *[Figure 3.39](#c03.xhtml_fig3_39)*:

![](images/Figure3.39.jpg)

**Figure 3.39:** The Install command button is clicked

The **`Done`** command button is clicked to exit the InstallAnywhere program, as shown in *[Figure 3.40](#c03.xhtml_fig3_40):*

![](images/Figure3.40.jpg)

**Figure 3.40:** The ***Done*** command button is clicked to exit the InstallAnywhere program

The program is run using the command **`./arsodf`** as shown to display the available command-line parameters, as illustrated in *[Figure 3.41](#c03.xhtml_fig3_41)*:

![](images/Figure3.41.jpg)

**Figure 3.41:** The program is run using the command ./arsodf as shown to display the available parameters

The link describing the use of the **`arsodf`** program, **“Using the ARSODF program - IBM Documentation”**, is as follows**:**

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=odf-using-arsodf-program](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=odf-using-arsodf-program)

# [Installing the Full Text Search Server Feature](#toc.xhtml_s41a)

The Content Manager OnDemand Full Text Search server feature uses the **Apache Lucene** text search engine library. This text search engine is the same as that used for IBM Db2, IBM Content Manager, and IBM FileNet. The Full Text Search Server processes the text extraction, indexing, and searching of data from the CMOD documents.

Here is the link to a PDF document from IBM, entitled “**Best Practices for Content Manager OnDemand Full Text Search**”:

[https://www.ibm.com/support/pages/sites/default/files/inline-files/Best%20practices%20for%20Using%20Full%20Text%20Searching%20with%20Content%20Manager%20OnDemand-4-22-2020.pdf](https://www.ibm.com/support/pages/sites/default/files/inline-files/Best%20practices%20for%20Using%20Full%20Text%20Searching%20with%20Content%20Manager%20OnDemand-4-22-2020.pdf)

The installation tar file is downloaded by logging into the IBM website, as shown in the previous section with screenshots from *[Figure 3.2](#c03.xhtml_fig3_2)* to *[Figure 3.8](#c03.xhtml_fig3_8)*. Then, the **IBM OnDemand Full Text Search Facility** is searched for, as illustrated in *[Figure 3.42](#c03.xhtml_fig3_42)***:**

![](images/Figure3.42.jpg)

**Figure 3.42:** The ***IBM OnDemand Full Text Search Facility*** is searched for

The **`IBM OnDemand Full Text Search Search V10.5 Multilingual Multiplatform`** (Part number **`CC4JJML`**) is selected and the **`I agree`** radio button is selected, as shown in *[Figure 3.43](#c03.xhtml_fig3_43):*

![](images/Figure3.43.jpg)

**Figure 3.43:** The ***IBM OnDemand Full Text Search Search V10.5 Multilingual Multiplatform*** (Part number ***CC4JJML***) is selected and the ***I agree*** radio button selected

The **`"View details"`** link in *[Figure 3.43](#c03.xhtml_fig3_43)* shows the product details, including the download file size, as displayed in *[Figure 3.44](#c03.xhtml_fig3_44)*:

![](images/Figure3.44.jpg)

**Figure 3.44:** The View details link shows the product details, including the download File size, ***2,566,123,520*** bytes

The **`Download Director`** **`Details`** button confirms the expected file size of **2,566,123,520** bytes for the **`IBM_CONTENT_MANAGER_ONDEMAND_FULL.tar`** installation file, as shown in *[Figure 3.45](#c03.xhtml_fig3_45):*

![](images/Figure3.45.jpg)

**Figure 3.45:** The ***Download Director*** ***Details*** button confirms the expected file size of ***2,566,123,520*** bytes for the ***IBM_CONTENT_MANAGER_ONDEMAND_FULL.tar*** installation file

The Linux commands are run as follows to copy the downloaded **`IBM_CONTENT_MANAGER_ONDEMAND_FULL.tar`** from the **`Installs`** mapped folder to the Linux **`/opt/FullTextSearch`** installation folder, as shown in *[Figure 3.46](#c03.xhtml_fig3_46)*:

`cd /opt`

`mkdir FullTextSearch`

`chmod 755 FullTextSearch/`

`cd FullTextSearch/`

`cp /mnt/hgfs/Installs/IBM_CONTENT_MANAGER_ONDEMAND_FULL.tar` **`.`**

![](images/Figure3.46.jpg)

**Figure 3.46:** The commands to copy the ***`IBM_CONTENT_MANAGER_ONDEMAND_FULL.tar`*** from the ***`Installs`*** folder

The **`IBM_CONTENT_MANAGER_ONDEMAND_FULL.tar`** installation file is unpacked using the command

**`tar -xvf IBM_CONTENT_MANAGER_ONDEMAND_FULL.tar`**, as shown in *[Figure 3.47](#c03.xhtml_fig3_47)*:

![](images/Figure3.47.jpg)

**Figure 3.47:** The installation file is unpacked using the command: ***tar -xvf IBM_CONTENT_MANAGER_ONDEMAND_FULL.tar***

The Linux-based files are unpacked as highlighted in the following listing, as shown in *[Figure 3.48](#c03.xhtml_fig3_48):*

![](images/Figure3.48.jpg)

**Figure 3.48:** The Linux-based files are unpacked as highlighted in the following listing

The **`readme.txt`** file is opened using the vi editor, as shown in *[Figure 3.49](#c03.xhtml_fig3_49):*

![](images/Figure3.49.jpg)

**Figure 3.49:** The ***readme.txt*** file is opened using the vi editor

For the command-line version, you can use the Linux command to install the **Content Manager OnDemand Full Text Search server** feature as follows:

`./odftslinux.bin -i console`

Or for the graphical user interface, we used:

`./odftslinux.bin`

As illustrated in *[Figure 3.50](#c03.xhtml_fig3_50)*:

![](images/Figure3.50.jpg)

**Figure 3.50:** For the graphical user interface, we used the Linux command ***./odftslinux.bin***

The **`IBM OnDemand Full Text Search Server V10.5`** installation splash screen is displayed, as shown in *[Figure 3.51](#c03.xhtml_fig3_51)*. The language is left as the default **`English`** option from the dropdown. The **`OK`** command button is then clicked to start the installation procedure:

![](images/Figure3.51.jpg)

**Figure 3.51:** The ***IBM OnDemand Full Text Search Server V10.5*** installation splash screen is displayed

The **`Next`** command button is clicked, as shown in *[Figure 3.52](#c03.xhtml_fig3_52)*:

![](images/Figure3.52.jpg)

**Figure 3.52:** The ***Next*** command button is clicked

The **`I accept`** radio button is selected after scrolling through the license agreement and the **`Next`** command button is clicked, as highlighted in *[Figure 3.53](#c03.xhtml_fig3_53):*

![](images/Figure3.53.jpg)

**Figure 3.53:** The ***I accept*** radio button is selected after scrolling the license agreement and the ***Next*** command clicked

The default installation path of **/`opt/ibm/odfts/V10.5`** is left and the **`Next`** command is clicked, as highlighted in *[Figure 3.54](#c03.xhtml_fig3_54)*:

![](images/Figure3.54.jpg)

**Figure 3.54:** The default installation path of ***/opt/ibm/odfts/V10.5*** is left and the ***Next*** command is clicked

The installation options are displayed and the **`Install`** command is clicked to begin the installation, as highlighted in *[Figure 3.55](#c03.xhtml_fig3_55)*:

![](images/Figure3.55.jpg)

**Figure 3.55:** The installation options are displayed and the ***Install*** command is clicked

The progress of the installation is displayed, as shown in *[Figure 3.56](#c03.xhtml_fig3_56):*

![](images/Figure3.56.jpg)

**Figure 3.56:** The progress of the installation is displayed

The status of the completed **`IBM OnDemand Full Text Server V10.5`** installation is displayed and the **`Done`** command button is clicked to exit the **InstallAnywhere** installation program, as illustrated in *[Figure 3.57](#c03.xhtml_fig3_57)*:

![](images/Figure3.57.jpg)

**Figure 3.57:** The ***Done*** command button is clicked to exit the ***InstallAnywhere*** installation program

To enable the Full Text Search feature on the RedHat Linux server, we need to edit the **`ars.cfg`** file and add the following parameters:

`ARS_SUPPORT_FULL_TEXT_INDEX=1`

(The value of **`'1'`** enables support for the Full Text search process.)

`ARS_FULL_TEXT_INDEX_TOKEN=fIqBxTQ=`

The **`"fIqBxTQ="`** authentication token is used to establish communication between the CMOD server and the Full Text Server during a search operation.

To check the actual authentication token to use, since upgrades and multiple FTS installations can change this token, IBM Recommend that you run the Linux command as follows:

`cd /opt/ibm/odfts/V10.5/bin`

`./configTool.sh printToken`

As illustrated in *[Figure 3.58](#c03.xhtml_fig3_58):*

![](images/Figure3.58.jpg)

**Figure 3.58:** IBM recommends that you run the Linux command **`./configTool.sh printToken`**

We can provide the required access to the 8191 port that is used using the following Linux Firewall command:

`[root@ECMUKDEMO22 ~]#`

**`firewall-cmd --zone=public --permanent --add-port=8191/tcp`**

**`firewall-cmd --reload`**

**Note:** *Full details for the configuration of the* ***Full Text Search*** *to use with Application Groups and specific fields can be found on pages 14-16 of the PDF available for download at:* *[https://www.ibm.com/support/pages/sites/default/files/inline-files/Best%20practices%20for%20Using%20Full%20Text%20Searching%20with%20Content%20Manager%20OnDemand-4-22-2020.pdf](https://www.ibm.com/support/pages/sites/default/files/inline-files/Best%20practices%20for%20Using%20Full%20Text%20Searching%20with%20Content%20Manager%20OnDemand-4-22-2020.pdf)*

*Documentation on the* ***Full Text Search server*** *authentication error fixes can be found at:*

*[https://www.ibm.com/docs/en/cmofz/10.5.0?topic=tips-authentication-fts-exporter-errors](https://www.ibm.com/docs/en/cmofz/10.5.0?topic=tips-authentication-fts-exporter-errors)*

# [Conclusion](#toc.xhtml_s42a)

In this chapter, we described the installation and administration of the supporting optional software components, including the **Db2** databases, the **PDF Indexing feature**, the **Distribution Facility feature**, and the **Full Text Search server feature**.

In the next *[Chapter 4, Installing the Upgraded Linux GSKit and Libraries](#c04.xhtml)*, we cover the IBM Fix Pack upgrade **`rpm`** files and some additional **Linux** operating system library packages that are required to be installed to support the **GSKit** for **CMOD** version **10.5.0.7**. This chapter describes their installation and the process of debugging the main **`arssockd`** program load and run.

# [Points to Remember](#toc.xhtml_s43a)

*   The **CMOD** system will support multiple instances, each one can be defined separately in its own section, in the **`ars.ini`** file, and is usually referenced in the Linux command line for the **CMOD** service programs by using the **`-I`** parameter.
*   The **`arsobjd`** program should be started only on object servers that are running on some other workstation than the library server.
*   The **`ARSSOCK= debug`** parameter in the **`ars.cfg`** configuration file can help you troubleshoot **TCP/IP** errors.
*   It is important to verify the actual authentication token to use since upgrades and multiple Full Text Search installations can change this token. IBM recommends that you run the Linux command as follows:

    `cd /opt/ibm/odfts/V10.5/bin`

    `./configTool.sh printToken`

# [Multiple Choice Questions](#toc.xhtml_s44a)

1.  Which parameter in the **`ars.ini`** file is used to identify the archive instance (the value set to ARCHIVE, note the case required on a Linux server)?
    1.  `SRVR_INSTANCE_OWNER`
    2.  `SRVR_INSTANCE`
    3.  `SRVR_OD_CFG`
    4.  `SRVR_SM_CFG`
2.  What command is used to start the CMOD ARCHIVE database instance, if you are starting from the **CMOD** config directory?
    1.  `../bin/arsdb -u -I ARCHIVE`
    2.  `./bin/arsdb -gkv`
    3.  `../bin/arsdb -gkv`
    4.  `./arsdb -I archive -u`
3.  Which **CMOD** additional feature program is run to extract the details from a PDF file?
    1.  `./odpdflinux.bin`
    2.  `./odftslinux.bin`
    3.  `./arspdump`
    4.  `./arsodf`
4.  Which **Db2** program is used to create an **`outputfile.sql`,** **SQL** file to contain the **DDL** for the table structures?
    1.  db2look
    2.  db2move
    3.  db2
    4.  db2start

# [Answers](#toc.xhtml_s45a)

1.  b
2.  c
3.  c
4.  a

# [Questions](#toc.xhtml_s46a)

1.  What procedure would you follow if you encountered the error: **`ARS0013E`** `DB Error: [IBM][CLI Driver][DB2/LINUXX8664] SQL0204N` **`\"ARCHIVE.ARSAG\"`** `is an undefined name.`
2.  In the error message **`"OnDemand (2378) -> bind errno = 98 rc = -1"`**, what is the likely reference to 2378 and how could you correct this error?
3.  Which TCP/IP network ports are used by the **CMOD** programs, and which Linux commands can be used to identify and open them for use?

# [Key Terms](#toc.xhtml_s47a)

*   **DDL**: Data Definition Language is a subset of **SQL** used for describing data and its relationships in a database, including the Table structures.

    We used the **db2look** command to generate **DDL** in a script for **Db2** database objects.

    `db2look -d ARCHIVE -e -o outputfile.sql`

*   **SQL:** Structured Query Language is a language used to create, delete, query, insert rows, and update rows in Database structures, such as Tables and Indexes.
*   **PDF:** The Portable Document Format, created by Adobe, provides a standard layout.
*   **TCP/IP**: Transmission Control Protocol/Internet Protocol are communication protocols used to interconnect network devices.
*   **CMOD**: IBM Content Manager OnDemand

# [CHAPTER 4](#toc.xhtml_c04)

# [Installing the Upgraded Linux GSKit and Libraries](#toc.xhtml_c04)

# [Introduction](#toc.xhtml_s48a)

The IBM Fix Pack upgrade **rpm** files and some additional **Linux** operating system library packages are required to be installed to support the **GSKit** for **CMOD** version **10.5.0.7**. This chapter describes the installation of the **rpm** files and the additional **GSKit** libraries, as well as the process of debugging the main **`arssockd`** program load and run.

The GSKit package for IBM Global Security Kit is required for the encryption service used by IBM Content Manager OnDemand.

There is a link, [https://cmod.wiki/index.php?title=IBM_Content_Manager_OnDemand_v10.5.0.7_and_GSKit_support_for_Post-Quantum_Cryptography&mobileaction=toggle_view_desktop](https://cmod.wiki/index.php?title=IBM_Content_Manager_OnDemand_v10.5.0.7_and_GSKit_support_for_Post-Quantum_Cryptography&mobileaction=toggle_view_desktop), which describes the GSKit support for the cryptography used by CMOD.

It recommends that the following is used for an upgraded system of CMOD:

When creating the key database, the **`'-pqc false'`** option must be used in order to use the older method.

The key database must be generated **without the** Post-Quantum Cryptographic methods by adding **`-pqc false`** to the GSKit **`-keydb -create`** command:

`gsk8capicmd_64 -keydb -create -db ars-ssl.kdb -genpw -stash -pqc false`

# [Structure](#toc.xhtml_s49a)

In this chapter, we will discuss the following topics:

*   Installing with the **Linux rpm** command line tool
*   Installing with the **Linux yum** command line tool
*   Creating the **CMOD** Cache Data Area(s)
*   Running the **`arsstash`** Encryption Program
*   **Linux** – How to Debug When **`arssockd`** Fails to Start and No Messages Are Produced
*   Configuring the **LIBPATH**, **LD_LIBRARY_PATH** and **PATH** on **Linux**

# [Installing with the Linux rpm command line tool](#toc.xhtml_s50a)

The installation must be performed as the user **root**. The **`-nodeps`** flag should not be used unless specifically called out in the following instructions:

We have to install using the **rpm** command to perform the installation as follows:

To install in the default location: `/usr/local`

`cd /opt/CMOD/linux`

`rpm -Uv gskcrypt64-8.0.55.12.linux.x86_64.rpm`

`rpm -Uv gskssl64-8.0.55.12.linux.x86_64.rpm`

`rpm -Uv gskcrypt32-8.0.55.12.linux.x86.rpm`

`rpm -Uv gskssl32-8.0.55.12.linux.x86.rpm`

# [Installing with the Linux yum command line tool](#toc.xhtml_s51a)

The following Linux libraries are required to support the **CMOD** **Version 10.5** software:

`[root@ECMUKDEMO22 config]#` **`yum install -y libaio`**

The **Linux C++** library, **`libstdc++-devel-8.5.0-20.el8.i686`**, is installed as shown in *[Figure 4.1](#c04.xhtml_fig4_1)*, using the command:

`[root@ECMUKDEMO22 config]#` **`yum install -y libstdc++-devel.i686`**

![](images/Figure4.1.jpg)

**Figure 4.1:** The ***Linux C++*** library, ***libstdc++-devel-8.5.0-20.el8.i686***, is installed

The following libraries were installed, as defined in the prerequisites for **CMOD**:

`[root@ECMUKDEMO22 config]#` **`yum install -y libstdc numactl-libs`**

`[root@ECMUKDEMO22 config]#` **`yum install -y libstdc pam`**

`[root@ECMUKDEMO22 config]#` **`yum install -y libstdc`**

**Note:** *While* ***rpm*** *(Red Hat Package Manager) is the underlying package format and management tool, defined to be used by IBM for some packages,* ***`yum`*** *and the newer* ***`dnf`*** *command, introduced in* ***RHEL 8.0****, are higher-level installation tools that simplify the process of installing and updating software packages and are easier to use for managing dependencies*.

The **Python** file libraries were installed, as shown in *[Figure 4.2](#c04.xhtml_fig4_2)*:

`[root@ECMUKDEMO22 config]#` **`yum install -y file`**

![](images/Figure4.2.jpg)

**Figure 4.2:** The Python file libraries were installed

The **Linux** library, **`ncurses-libs-6.1-10.20180224.el8.i686`**, is installed as shown in *[Figure 4.3](#c04.xhtml_fig4_3)*, using the **Linux** command as follows:

`[root@ECMUKDEMO22 config]#` **`yum install -y ncurses-libs.i686`**

![](images/Figure4.3.jpg)

**Figure 4.3:** The ***Linux*** library, ***ncurses-libs-6.1-10.20180224.el8.i686,***is installed

Next, we install the **`numactl-libs`**, which provides a library to do allocations with the Non-Uniform Memory Access (NUMA) policy in applications, using the command:

`[root@ECMUKDEMO22 config]#` **`yum install -y numactl-libs`**

(See: [https://en.wikipedia.org/wiki/Non-uniform_memory_access](https://en.wikipedia.org/wiki/Non-uniform_memory_access))

The **Linux Open SSL** security libraries are installed, as shown in *[Figure 4.4](#c04.xhtml_fig4_4)*, using the Linux command as follows:

`[root@ECMUKDEMO22 config]#` **`yum install -y openssl`**

![](images/Figure4.4.jpg)

**Figure 4.4:** The ***Linux Open SSL*** security libraries are installed

# [Creating the CMOD Cache Data Area(s)](#toc.xhtml_s52a)

The cache data directories are required to store the Documents captured by **CMOD**, and are required to have ownership and security set using the Linux commands as follows:

`[root@ECMUKDEMO22 config]#` **`mkdir /data`**

`[root@ECMUKDEMO22 config]#` **`mkdir /data/arscache`**

`[root@ECMUKDEMO22 config]#` **`chmod 700 /data/arscache`**

`[root@ECMUKDEMO22 config]#` **`chown -R archive:db2iadm1 /data*`**

`[root@ECMUKDEMO22 config]#`

# [Running the arsstash Encryption Program](#toc.xhtml_s53a)

The password used by the **ADMIN** user for the **CMOD** system should be encrypted to increase the security of the system; otherwise, we would need to apply the unencrypted password in order to run many of the **CMOD** administration programs. We run the **`arsstash`** program, as shown in *[Figure 4.5](#c04.xhtml_fig4_5)*, using the **Linux** commands as follows:

`cd /opt/ibm/ondemand/V10.5/bin`

`./arsstash -a 1 -c -s /opt/ibm/ondemand/V10.5/config/ars.stash -u archive`

![](images/Figure4.5.jpg)

**Figure 4.5:** The password for the ***ADMIN*** user on the ***CMOD*** system is encrypted using the ***arsstash*** program

The following environment variable is also set to point to the **`ars.stash`** file with the encrypted password, as shown in *[Figure 4.6](#c04.xhtml_fig4_6)*:

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`

`export SRVR_OD_STASH`

![](images/Figure4.6.jpg)

**Figure 4.6:** The ***SRVR_OD_STASH*** environment variable is set in the ***root*** user***/root/.bash_profile*** file using ***vi***

Next, the **`ars.ini`** file is also edited using the **vi** editor to add the parameter, as shown in *[Figure 4.7](#c04.xhtml_fig4_7):*

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`

![](images/Figure4.7.jpg)

**Figure 4.7:** The ***ars.ini*** file is edited using the ***vi*** editor to add the ***SRVR_OD_STASH*** parameter

We also set the security on the **Linux GSKit** root directory and recursively for all the sub-directories and files as follows:

`chmod -R 775 /opt/ibm/ondemand/V10.5/www`

# [Linux – The Method Used for Debugging `ARSSOCKD` with a Trace Logging File Output](#toc.xhtml_s54a)

1.  When either **arssockd** ends before it can write to the System Log or the console does not display any useful error messages, we first need to ensure that **Db2** is running.
2.  If that does not resolve the problem, the **Linux** system trace information can be captured by using a command similar to this:

    `cd /root`

    `strace -s 256 -f /opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S 2>strace.out`

    `cat strace.out`

    We can then examine the **`strace.out`** file and search for **`“arslog.”`**

    Often, **`“arslog”`** will be followed by a **CMOD** message with the error.

    The following is an example from a recent problem record:

    `Line 1125: [pid  7842] execve("/opt/ibm/ondemand/V10.5/bin/arslog", ["/opt/ibm/ondemand/V10.5/bin/arslog", "ARCHIVE", "2024-03-26 11:21:08.947825", "0", "ARSSOCKD", "", "4", "213", "`**`ARS0213I Unable to load the OnDemand DB2 dynamic load library (arsdb2).  Check to make sure DB2 is installed and that the db2ln command has been run"`**`, ""], 0x1bdb640 /* 95 vars */ <unfinished ...>`

    `Line 1317: openat(AT_FDCWD, "/opt/ibm/ondemand/V10.5/bin/arslog", O_RDONLY) = 4`

    `Line 1332: read(11, "#!/bin/ksh\n#\n#` **`arslog`** `- OnDemand User Exit Logging Facility\n#\n#  5622-662 (C) COPYRIGHT IBM CORPORATION 1995\n#  All Rights Reserved\n#  Licensed Materials - Property of IBM\n#\n#  US Government Users Restricted Rights - Use, duplication or\n#  disclosure"..., 65536) = 707`

    **Note:** *The* ***`ARS0213I`*** *message identifies an issue related to the libraries used for DB2 shared object memory:*

    ***`ARS0213I Unable to load the OnDemand DB2 dynamic load library`***

    ***`(arsdb2).`***

    *IBM recommends that you check to make sure* ***Db2*** *is installed and that the* ***`db2ln`*** *command has been run.*

3.  When the **`Db2`** **`db2ln`** command fails to resolve the issue**,** then the `"`**`ldd`**`"` command can be used to check if there are other library file dependency issues related to the **`arssockd`** program.

    Using the userid that would launch the **`arssockd`** program, run:

    `ldd /opt/ibm/ondemand/V10.5/bin/arssockd`

    `[root@ECMUKDEMO22 ~]#` **`ldd /opt/ibm/ondemand/V10.5/bin/arssockd`**

    `linux-vdso.so.1 (0x00007ffe3e741000)`

    `libgsk8ssl_64.so => /lib64/libgsk8ssl_64.so (0x00007ff1b5727000)`

    `libgsk8iccs_64.so => /lib64/libgsk8iccs_64.so (0x00007ff1b5d18000)`

    `libgsk8km_64.so => /lib64/libgsk8km_64.so (0x00007ff1b551b000)`

    `libdl.so.2 => /lib64/libdl.so.2 (0x00007ff1b5317000)`

    `librt.so.1 => /lib64/librt.so.1 (0x00007ff1b510f000)`

    `libstdc++.so.6 => /lib64/libstdc++.so.6 (0x00007ff1b4d7a000)`

    `libm.so.6 => /lib64/libm.so.6 (0x00007ff1b49f8000)`

    `libgcc_s.so.1 => /lib64/libgcc_s.so.1 (0x00007ff1b47e0000)`

    `libpthread.so.0 => /lib64/libpthread.so.0 (0x00007ff1b45c0000)`

    `libc.so.6 => /lib64/libc.so.6 (0x00007ff1b41fb000)`

    `libgsk8cms_64.so => /lib64/libgsk8cms_64.so (0x00007ff1b3cca000)`

    `/lib64/ld-linux-x86-64.so.2 (0x00007ff1b5c71000)`

    `[root@ECMUKDEMO22 ~]#`

4.  Also, later, we had the following error:

    `ARS0013E DB Error: [IBM][CLI Driver][DB2/LINUXX8664] SQL0204N  \"`**`ARCHIVE.ARSAG`**`\" is an undefined name.  SQLSTATE=42704  -- SQLSTATE=42S02, SQLCODE=-204, File=arsag.c, Line=4275", ""], 0x2c85440 /* 69 vars */`

    This error was corrected by changing the initial **root** table schema to the **archive** schema.

    Then we found another issue, as follows:

    `pid 49001] rt_sigprocmask(SIG_SETMASK, [], NULL, 8) = 0`

    `[pid 49001] execve("/opt/ibm/ondemand/V10.5/bin/arslog", ["/opt/ibm/ondemand/V10.5/bin/arslog", "ARCHIVE", "2024-04-04 05:33:22.007330", "0", "ARSMSG", "", "2", "154", "`**`ARS0154E Unable to establish server communications with network.` `The return code is 2`**`", ""], 0x2da2c90 /* 104 vars */ <unfinished ...>`

    This was identified as a **/etc/hosts** file configuration issue. The **ARSSOCK= debug** parameter in the **ars.cfg** file helped to identify the problem.

# [Configuring the LIBPATH, LD_LIBRARY_PATH, and PATH on Linux](#toc.xhtml_s55a)

We have to add the library files to the **`PATH`**, **`LIBPATH`**, and **`LD_LIBRARY_PATH`** environment variables.

See: [https://www.ibm.com/support/pages/how-do-i-resolve-javalangunsatisfiedlinkerror-javalangnoclassdeffounderror-or-ibm-global-security-kit-gskit-errors-when-deploying-odwek-java-api-application](https://www.ibm.com/support/pages/how-do-i-resolve-javalangunsatisfiedlinkerror-javalangnoclassdeffounderror-or-ibm-global-security-kit-gskit-errors-when-deploying-odwek-java-api-application)

We include the directory or directories that contain the **ODWEK** native library and its dependencies as follows. Add the following to **`/root/.bash_profile`** using the **vi** editor:

`LD_LIBRARY_PATH=/opt/ibm/ondemand/V10.5/www`

`export LD_LIBRARY_PATH`

Then, we use the **Linux** **`ldd`** command to check that the **GSKit** can be loaded using the commands:

`ldd /opt/ibm/ondemand/V10.5/www/libars3wapi32.so`

The list of dependencies for the shared object library, **`libars3wapi32.so`** and the paths to these shared object libraries are shown using this command, as illustrated in *[Figure 4.8](#c04.xhtml_fig4_8)*:

![](images/Figure4.8.jpg)

**Figure 4.8:** The list of dependencies for the library, ***libars3wapi32.so***

The list of dependencies for the shared object library, **`libars3wapi64.so`**, and the paths to these shared object libraries are shown, as illustrated in *[Figure 4.9](#c04.xhtml_fig4_9)*:

`ldd /opt/ibm/ondemand/V10.5/www/libars3wapi64.so`

![](images/Figure4.9.jpg)

**Figure 4.9:** The list of dependencies for the library, ***libars3wapi64.so***

Next, we see the error message as follows in the WebSphere server log:

`The fixed content provider could not establish a connection to the fixed content device.` `CMOD server logon, Server:` **`ECMUKDEMO22`** `; Port: 0 ; Username:` **`archive`** `; Adaptor: CMODAdaptor: A5872393-DC5F-4C08-8037-C9E5A02B1DED : ; Method: ODServer.logon ;`

So, we try adding the **archive** user as an **LDAP** user in our **Linux LDAP,** **IBM Security Directory Suite** server, **`ECMUKDEMO77`** (IP address: **`192.168.50.131`**).

The following link was used to load the **LDAP** Administration web application:

[https://192.168.50.131:12101/IDSWebApp/IDSjsp/IDSConsoleFrameWork.jsp](https://192.168.50.131:12101/IDSWebApp/IDSjsp/IDSConsoleFrameWork.jsp)

**Note:** *The* ***Chrome*** *web browser blocked the* ***https*** *site, with the message:*

*This site can’t provide a secure connection.* ***192.168.50.131*** *uses an unsupported protocol.* ***`ERR_SSL_VERSION_OR_CIPHER_MISMATCH`****)*

Next, we browsed using a **FireFox** web browser and logged in using the **`cn=admin`** user account, as shown in *[Figure 4.10](#c04.xhtml_fig4_10)*:

![](images/Figure4.10.jpg)

**Figure 4.10:** The ***Linux LDAP,*** ***IBM Security Directory Suite*** server, ***Adminstration web application***

The **`Directory management`->** **`Manage`** entries node of the navigation tree panel is selected, and the **`cn=localhost`** **RDN** (Relative Distinguished Name) is selected to add our **archive** user, as shown in *[Figure 4.11](#c04.xhtml_fig4_11)***,** by clicking on the highlighted plus icon**:**

![](images/Figure4.11.jpg)

**Figure 4.11:** The ***Directory management-> Manage*** tree node of the navigation tree is selected and the ***cn=localhost*** ***RDN*** is selected to add the archive user

We can now select the **`Add`** command button to add the new **archive** user to the **`cn=localhost`** **RDN** list of users, as shown in *[Figure 4.12](#c04.xhtml_fig4_12)*:

![](images/Figure4.12.jpg)

**Figure 4.12:** The ***Add*** command button is selected to add the new ***archive*** user to the ***cn=localhost*** ***RDN*** list

The **`inetOrgPerson`** Object class is selected as highlighted from the **`Structured object classes`** drop-down, and the **`Next>`** command button is selected, as highlighted in *[Figure 4.13](#c04.xhtml_fig4_13)*:

![](images/Figure4.13.jpg)

**Figure 4.13:** The **inetOrgPerson** object class is selected from the **Structured object classes** drop-down

The **`Auxiliary object classes`** page is skipped by just clicking on the **`Next>`** command button, as illustrated in *[Figure 4.14](#c04.xhtml_fig4_14)*:

![](images/Figure4.14.jpg)

**Figure 4.14:** The ***Auxiliary object classes*** page is skipped by just clicking on the ***Next>*** command button

The **`archive`** username is entered as shown, highlighted in *[Figure 4.15](#c04.xhtml_fig4_15)*, and **`Next>`** selected**:**

![](images/Figure4.15.jpg)

**Figure 4.15:** The ***archive*** username is entered as shown, and the Next> command button selected as highlighted

We can now enter the **archive** user’s password, as highlighted in *[Figure 4.16](#c04.xhtml_fig4_16)*, and select the **`Finish`** command button to store the **archive** user details in the **IBM Security Services Directory** database, as shown in *[Figure 4.16](#c04.xhtml_fig4_16)*:

![](images/Figure4.16.jpg)

**Figure 4.16:** We can now enter the ***archive*** user’s password as highlighted

The web application shows that we have successfully added the **archive** user, and we can select the **`No`** option button to decline the prompt to add another user, as shown in *[Figure 4.17](#c04.xhtml_fig4_17):*

![](images/Figure4.17.jpg)

**Figure 4.17:** The ***No*** option button, is selected to decline the prompt to add another user

The new entry for our **archive** user can now be seen, as highlighted in *[Figure 4.18](#c04.xhtml_fig4_18)*:

![](images/Figure4.18.jpg)

**Figure 4.18:** The new entry for our ***archive*** user can now be seen as highlighted

The updates we have made here were successfully used to create the **IBM Fixed Content Device**, as described in *[Chapter 2, Installing CMOD on Linux Systems](#c02.xhtml)*, in the section, **Configuring IBM FileNet P8 for a Fixed Content Device using CMOD.**

The **`arssockd`** program can now be run, as shown in *[Figure 4.19](#c04.xhtml_fig4_19)*:

![](images/Figure4.19.jpg)

**Figure 4.19:** The command which starts the ***arssockd*** object server and a listener on port ***1445***

See:

[https://cmod.wiki/dox/ODWEK-BasicsAndBeyond.pdf](https://cmod.wiki/dox/ODWEK-BasicsAndBeyond.pdf)

The error was seen as follows:

`Encountered error: The server failed while attempting to logon`

**`Error code: 2163`**

Also see:

[https://www.ibm.com/support/pages/i-receive-following-error-message-when-logging-server-failed-while-attempting-logon](https://www.ibm.com/support/pages/i-receive-following-error-message-when-logging-server-failed-while-attempting-logon)

[https://cmod.wiki/dox/CMODv7.1/Messages%20and%20Codes.pdf](https://cmod.wiki/dox/CMODv7.1/Messages%20and%20Codes.pdf)

# [Conclusion](#toc.xhtml_s56a)

In this chapter, we described the installation of the IBM Fix Pack upgrade **rpm** files and some additional **Linux** operating system library package installs to support the **GSKit** for **CMOD** version **10.5.0.7**. We also covered the process of debugging the main **`arssockd`** program load and run.

In the next chapter, we will cover the step-by-step download, installation, and configuration of the **IBM Content Manager OnDemand** version **10.5** base and **Fix Pack 10.5.0.7** upgrade on a **Windows 11** server.

# [Points to Remember](#toc.xhtml_s57a)

*   Check to make sure **Db2** is installed and that the **`db2ln`** command has been run, if you get the error message: **`ARS0213I`** **`Unable to load the OnDemand DB2 dynamic load library`** `(`**`arsdb2`**`).`
*   To load the IBM **LDAP** Administration web application, you may find that the FireFox browser will work better than the Chrome browser.

# [Multiple Choice Questions](#toc.xhtml_s58a)

1.  Which of the following **Linux** commands can be used to install a **Linux** library required to support the **CMOD** **Version 10.5** software?
    1.  `rpm`
    2.  `yum`
    3.  `chmod`
    4.  `chown`
2.  Which of the following **Linux** commands can be used to change the user and group ownership of the **CMOD Cache** file system?
    1.  `mkdir /data/arscache`
    2.  `chmod 700 /data/arscache`
    3.  `chown -R archive:db2iadm1 /data*`
    4.  `chmod -R 775 /opt/ibm/ondemand/V10.5/www`
3.  Which of the following **Linux** commands is used to set the **Load Library** environment variable directory path for the **CMOD ODWEK** native libraries?
    1.  `ldd /opt/ibm/ondemand/V10.5/www/libars3wapi32.so`
    2.  `ldd /opt/ibm/ondemand/V10.5/www/libars3wapi64.so`
    3.  `chmod -R 775 /opt/ibm/ondemand/V10.5/www`
    4.  `LD_LIBRARY_PATH=/opt/ibm/ondemand/V10.5/www`

# [Answers](#toc.xhtml_s59a)

1.  b
2.  c
3.  d

# [Questions](#toc.xhtml_s60a)

1.  Which **Linux** command would you use to identify the shared object library dependencies of a **Linux** program?
2.  What procedure would you follow to encrypt and store the encrypted password used by the **ADMIN** user for the **CMOD** system?

# [Key Terms](#toc.xhtml_s61a)

*   **RDN**: Relative Distinguished Name is the first component of the Distinguished Name (DN), which is any attribute stored in a **LDAP** directory. This first component is called the Relative Distinguished Name (**RDN**), which is unique in the directory; for example, **cn=localhost**.
*   **CN:** The Common Name is also known as the Fully Qualified Domain Name (**FQDN**) and is the unique name of a specific domain in **LDAP**, localhost in our example.
*   **rpm**: Linux command is the command line package manager for Red Hat Linux systems.
*   **yum**: Yellow-dog Update Manager is used to install, update, and remove packages from **RedHat** **Linux** systems.
*   **ODWEK**: The IBM Content Manager OnDemand Web Enablement Kit consists of a number of Java API programming interfaces that can be called to search and retrieve documents from **CMOD** servers. See: [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=ondemand-content-manager-web-enablement-kit](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=ondemand-content-manager-web-enablement-kit)
*   **CMOD**: IBM Content Manager OnDemand
*   **LDAP:** Lightweight Directory Access Protocol is a protocol that stores User, Object, and Network system data used to authenticate users and systems.

# [CHAPTER 5](#toc.xhtml_c05)

# [Installing CMOD on Windows Systems](#toc.xhtml_c05)

# [Introduction](#toc.xhtml_s62a)

This chapter covers the step-by-step download, installation, and configuration of the **IBM Content Manager OnDemand** (**CMOD**) version **10.5** base and **Fix Pack 10.5.0.7** upgrade on a **Windows 11** server.

The base installation of IBM CMOD 10.5 is installed first and configured on the Windows system, and then the latest available Fix Pack is searched for on the IBM Fix Central web site to demonstrate the procedure steps for upgrading and configuring IBM CMOD to the latest Fix Pack (Version 10.5.0.7 at the time of writing). We also cover the installation of the IBM CMOD Windows client.

# [Structure](#toc.xhtml_s63a)

In this chapter, we will discuss the following topics:

*   Downloading the **Base Installation** Program
*   Downloading the **Fix Pack** **Installation** Program
*   Installing the **Fix Pack** for the Windows Client
*   **ARCHIVE** Database Creation Update Log on **Windows**
    *   Starting the **Linux** Server **arssockd** Process
*   Setting the **Db2 ARCHIVE Port 50001** Access on **Windows**
    *   Opening Ports in **Windows Firewall**
*   Creating the **IBM FileNet Fixed Content Device** Support for **IBM Content Manager OnDemand**

# [Downloading the Base Installation Program](#toc.xhtml_s64a)

1.  First, we log onto the **IBM PartnerPlus** website following the same steps described in *[Chapter 2, Installing **CMOD** on Linux Systems](#c02.xhtml),* using the screenshots illustrated in the chapter, *[Figure 2.1](#c02.xhtml_fig2_1)* to *[Figure 2.3](#c02.xhtml_fig2_3)*, to log onto the IBM website. Then, the Base software installation package for **IBM Content Manager OnDemand** (**CMOD**) Version **10.5** for Windows is selected from the **IBM Software Access catalog** web page by searching for Part Number **`CC4JCML`**, as highlighted in *[Figure 5.1](#c05.xhtml_fig5_1):*

    ![](images/Figure5.1.jpg)

    **Figure 5.1:** The ***IBM Content Manager OnDemand V10.5*** for ***Windows*** is searched for with ***Part Number CC4JCML***

2.  Next, the **Download Director** software is run to obtain the **`IBM_CMOD_V10.5_WIN_ML.zip`** installation zip file, as shown in *[Figure 5.2](#c05.xhtml_fig5_2)*:

    ![](images/Figure5.2.jpg)

    **Figure 5.2:** The ***IBM_CMOD_V10.5_WIN_ML.zip*** installation zip file is downloaded with IBM ***Download Director***

3.  The **`IBM_CMOD_V10.5_WIN_ML.zip`** file is unpacked using **7-zip** to give the file list illustrated in *[Figure 5.3](#c05.xhtml_fig5_3):*

    ![](images/Figure5.3.jpg)

    **Figure 5.3:** The ***IBM_CMOD_V10.5_WIN_ML.zip*** file is unpacked using ***7-zip***

4.  The **`readme.txt`** file highlighted in *[Figure 5.3](#c05.xhtml_fig5_3)* is opened to list the main installation pre-requisites, as listed:

    `2GB of free space on C:\`

    `Installing the IBM Global Security Kit Version 8 :`

    `The GSKit Crypt and SSL components are installed automatically.`

    `Please read the Installation Documentation online at:`

    [`https://www.ibm.com/support/knowledgecenter/SSEPCD_10.5.0`](https://www.ibm.com/support/knowledgecenter/SSEPCD_10.5.0)

    `for further information`

5.  The **`odwin.exe`** program is run and displays the install display, as shown in *[Figure 5.4](#c05.xhtml_fig5_4):*

    ![](images/Figure5.4.jpg)

    **Figure 5.4:** The ***odwin.exe*** program is run and displays the install display

6.  The language in the drop-down is left as the default of **`English`**, and the **OK** command button is selected to display the following install page, confirming the install details, and the **`Next`** command is selected, as highlighted in *[Figure 5.5](#c05.xhtml_fig5_5):*

    ![](images/Figure5.5.jpg)

    **Figure 5.5:** The install page, confirming the install details, and the ***Next*** command is selected

7.  The **`Software`** **`License Agreement`** is scrolled through and the **`I accept`** radio button must be selected, if the installation is to be completed and the **`Next`** command button is selected, as shown in *[Figure 5.6](#c05.xhtml_fig5_6):*

    ![](images/Figure5.6.jpg)

    **Figure 5.6:** The ***I accept*** radio button must be selected and the ***Next*** command button is selected

8.  The default Windows installation path of **`c:\Program Files\IBM\OnDemand\V10.5`** is left, as highlighted, and the highlighted **`Next`** command button is selected, as shown in *[Figure 5.7](#c05.xhtml_fig5_7):*

    ![](images/Figure5.7.jpg)

    **Figure 5.7:** The highlighted ***Next*** command button is selected

9.  The **`Authorized User (UVU)`** License radio button option is selected and the **`Next`** command button is selected, as shown in *[Figure 5.8](#c05.xhtml_fig5_8)*:

    ![](images/Figure5.8.jpg)

    **Figure 5.8:** The ***Authorized User (UVU)*** License radio button option is selected and the ***Next*** command

10.  The **`Install`** command button is selected to start the Installation of **`IBM OnDemand V10.5`**, as displayed in *[Figure 5.9](#c05.xhtml_fig5_9)*:

    ![](images/Figure5.9.jpg)

    **Figure 5.9:** The ***Install*** command button is selected to start the Installation of ***IBM OnDemand V10.5***

11.  The **status bar** is displayed to show the installation progress, as shown in *[Figure 5.10](#c05.xhtml_fig5_10):*

    ![](images/Figure5.10.jpg)

    **Figure 5.10:** The ***status bar*** is displayed to show the installation progress

12.  The option to display the **`readme.txt`** file is displayed in a pop-up window, as shown in *[Figure 5.11](#c05.xhtml_fig5_11):*

    ![](images/Figure5.11.jpg)

    **Figure 5.11:** The option to display the ***readme.txt*** file is displayed in a pop-up window

13.  The **`readme.txt`** file is loaded for display, as shown in *[Figure 5.12](#c05.xhtml_fig5_12):*

    ![](images/Figure5.12.jpg)

    **Figure 5.12:** The ***readme.txt*** file is loaded for display

14.  The base installation of the **IBM Content Manager OnDemand V10.5** software is successfully installed on the **Windows 11** server and the **`Done`** command button is selected to exit the **InstallAnywhere** program, as shown in *[Figure 5.13](#c05.xhtml_fig5_13):*

    ![](images/Figure5.13.jpg)

    **Figure 5.13:** The base installation of the ***IBM Content Manager OnDemand V10.5*** software is successfully installed

# [Downloading the Fix Pack Installation Program](#toc.xhtml_s65a)

1.  The **IBM Fix Central** web page (see [https://www.ibm.com/support/fixcentral](https://www.ibm.com/support/fixcentral)) is selected after logging into the IBM system, as already described in *[Chapter 2, Installing **CMOD** on Linux Systems](#c02.xhtml)*, using the same link, logging on as shown in *[Figure 2.82](#c02.xhtml_fig2_82)* to *[Figure 2.89](#c02.xhtml_fig2_89)*, and then we can display the page, as shown in *[Figure 5.14](#c05.xhtml_fig5_14)*:

    ![](images/Figure5.14.jpg)

    **Figure 5.14:** The ***IBM Fix Central*** web page is selected after logging into the IBM system

2.  The **`IBM Download Director`** program is started using the **`Run`** command button, as shown in *[Figure 5.15](#c05.xhtml_fig5_15)*:

    ![](images/Figure5.15.jpg)

    **Figure 5.15:** The ***IBM Download Director*** program is started using the ***Run*** command button

3.  The **IBM Download Director** program status bar is displayed, showing the progress of the download of the five Fix Pack files for the upgrade Fix Pack **10.5.0.7** for the IBM multi-platform Fix Pack, for **CMOD**, including the **`odwin64.zip`** file for the **Windows 11** server, as shown in *[Figure 5.16](#c05.xhtml_fig5_16)*:

    ![](images/Figure5.16.jpg)

    **Figure 5.16:** The ***IBM Download Director*** program status bar is displayed, with the progress of the download

4.  The complete download status window **`Details`** command button is selected to display the list of the five download files for the **CMOD** **Fix Pack V10.5.0.7**, as shown in *[Figure 5.17](#c05.xhtml_fig5_17):*

    ![](images/Figure5.17.jpg)

    **Figure 5.17:** The completed status window ***Details*** command button is selected to display the download list of files

The downloaded **readme.txt** file can be viewed to show the section for advice on the **Windows** installation prerequisites, as shown here:

**`(2.3) Windows Server`**

**`2.3.10.5.0.0) Release (10.5.0.0)`**

**`- Pre-reqs`**

**`- Windows Server 2016 or later`**

**`- Database`**

**`- DB2 V11.1 or later`**

**`- Oracle 19c or later`**

**`- Microsoft SQL Server 2017 or later`**

**`- Microsoft .NET Framework 4.6.2 or later`**

**`- IBM Spectrum Protect V8.1 or later`**

**`- IBM Global Security Kit Version 8`**

`- Included in the installation packaging`

**`- Installation`**

`- Pre-reqs`

**`- 2GB of free space on C:\`**

`- To install from the command line`

`-` **`odwin.exe`**

`- To uninstall use Programs and Features from the Control Panel`

`- Please read the Installation Documentation online at:`

[`https://www.ibm.com/support/knowledgecenter/SSEPCD_10.5.0`](https://www.ibm.com/support/knowledgecenter/SSEPCD_10.5.0)

`for further information`

`- Installing the IBM Global Security Kit Version 8`

`The GSKit Crypt and SSL components are installed automatically.`

The installation of the **CMOD Windows Server** uses the downloaded **`odwin.exe`** program and the same screenshots for the Fix Pack as for the base system (see *[Figures 5.4](#c05.xhtml_fig5_4)* to *[5.12](#c05.xhtml_fig5_12)*).

# [Installing the Fix Pack for the Windows Client](#toc.xhtml_s66a)

The **Windows** **CMOD 10.5.0.7** Fix Pack program, **odwin64.zip**, is copied down from the downloaded file on the **Linux** server to the **Windows** server using the **Linux** commands as follows:

`[root@ECMUKDEMO22 CMOD_FP]#` **`cd /mnt/hgfs`**

`[root@ECMUKDEMO22 hgfs]#` **`ls`**

**`Installs`**

`[root@ECMUKDEMO22 hgfs]#` **`cp /opt/CMOD_FP/odwin64.zip ./Installs/`**

1.  The details of the **`setup.exe`** program properties confirm we have the **IBM OnDemand** Clients Installer **Version 10.5.0.7**., as shown in *[Figure 5.18](#c05.xhtml_fig5_18)*:

    ![](images/Figure5.18.jpg)

    **Figure 5.18:** The ***setup.exe*** program properties show we have the ***IBM OnDemand*** Clients Installer ***Version 10.5.0.7***

2.  We can click on the **`setup.exe`** program, running as the **Windows Administrator** user, to give the **`IBM OnDemand Clients V10.5 (64-bit)`** splash screen, as shown in *[Figure 5.19](#c05.xhtml_fig5_19)*:

    ![](images/Figure5.19.jpg)

    **Figure 5.19:** The ***setup.exe*** program, running as the ***Windows Administrator*** user

3.  The **`Typical`** installation option is selected, and the **`Next>`** command button is selected, as shown in *[Figure 5.20](#c05.xhtml_fig5_20)*:

    ![](images/Figure5.20.jpg)

    **Figure 5.20:** The ***Typical*** installation option is selected and the ***Next>*** command button selected

4.  The **`Program Folder`** is displayed as **`IBM OnDemand Clients V10.5 (64-bit)`**, as shown in *[Figure 5.21](#c05.xhtml_fig5_21)*:

    ![](images/Figure5.21.jpg)

    **Figure 5.21:** The ***Program Folder*** is displayed as ***IBM OnDemand Clients V10.5 (64-bit)***

5.  The **InstallAnywhere** program lists the details of the files to be copied, and the **`Next>`** command button is selected to start the file copy, as shown in *[Figure 5.22](#c05.xhtml_fig5_22)*:

    ![](images/Figure5.22.jpg)

    **Figure 5.22:** The ***InstallAnywhere*** program lists the details of the files to be copied and the ***Next>*** command button is selected to start the file copy

6.  The ***CMOD Client V10.5*** Installation status bar is displayed, as shown in *[Figure 5.23](#c05.xhtml_fig5_23)*:

    ![](images/Figure5.23.jpg)

    **Figure 5.23:** The ***CMOD Client V10.5*** Installation status bar is displayed

7.  The installation is now complete and prompts for the option to restart the Windows server by selecting the **`Finish`** command button, as shown in *[Figure 5.24](#c05.xhtml_fig5_24)*:

    ![](images/Figure5.24.jpg)

    **Figure 5.24:** The installation is now complete and prompts for the option to restart the Windows server

# [ARCHIVE Database Creation Update Log on Windows](#toc.xhtml_s67a)

Following is the log of the **ARCHIVE** database creation, with the details of the code page and code set of the **Db2** settings:

`ARS4015I Starting the DB2 ARCHIVE database instance`

`ARS4078I The ARCHIVE instance has already been started`

`ARS4018I Creating the DB2 ARCHIVE database`

`ARS4062I Database created with territory 'GB',` **`code page '1208'`**`, code set` **`'UTF-8'`** `and collating sequence ''`

`ARS4068I Updating the ARCHIVE database configuration`

`ARS4073I Deactivating database ARCHIVE`

`ARS4071I Backing up the ARCHIVE database so that the updates can take effect`

`ARS4057I Timestamp for backup image is: 20240326205016`

`ARS4026I Creating table alan_.arsag`

`ARS4034I Creating index alan_.arsag_name_idx`

`ARS4034I Creating index alan_.arsag_agid_idx`

`ARS4042I Updating runstat statistics for table alan_.arsag`

`ARS4026I Creating table alan_.arsag2fol`

`ARS4034I Creating index alan_.arsag2fol_idx`

`ARS4042I Updating runstat statistics for table alan_.arsag2fol`

`ARS4026I Creating table alan_.arsagfld`

`ARS4034I Creating index alan_.arsagfld_idx`

`ARS4042I Updating runstat statistics for table alan_.arsagfld`

`ARS4026I Creating table alan_.arsagfldalias`

`ARS4034I Creating index alan_.arsagfldalias_idx`

`Etc…`

`Repeated for the other 41 tables`

`Etc…`

`ARS4034I Creating index alan_.arsuser_id_idx`

`ARS4034I Creating index alan_.arsuser_name_idx`

`ARS4042I Updating runstat statistics for table alan_.arsuser`

`ARS4026I Creating table alan_.arsusrgrp`

`ARS4034I Creating index alan_.arsusrgrp_idx`

`ARS4034I Creating index alan_.arsusrgrp_idx2`

`ARS4042I Updating runstat statistics for table alan_.arsusrgrp`

`ARS4026I Creating table alan_.arsusrgrpid`

`ARS4034I Creating index alan_.arsusrgrpid_idx`

`ARS4042I Updating runstat statistics for table alan_.arsusrgrpid`

`-------------end of Windows Server-------------------------------------`

**Starting the Linux server arssockd process:**

The arssockd program on the Linux server was started with the following output:

`[archive@ECMUKDEMO22 config]$` **`/opt/ibm/ondemand/V10.5/bin/arssockd`**

`[archive@ECMUKDEMO22 config]$` **`ps -ef|grep ars`**

`archive    23853    4244  0 08:06 pts/0    00:00:00 grep --color=auto ars`

`[archive@ECMUKDEMO22 config]$`

**Updating the permissions for the Linux CMOD configuration files:**

The following commands were used to update the **CMOD** user and group ownership files:

`[root@ECMUKDEMO22 config]#` **`ls ars*`**

`ars.az.smp  ars.cfg   ars.fs.smp   ars.hdfs.smp  ars.ini     arspdsys.bst  ars.s3.smp  ars.swift.smp`

`ars.cache   ars.dbfs  ars.gcs.smp  ars.icos.smp  arsodf.xml  arspdusr.bst  ars.stash   arsxform.xml`

`[root@ECMUKDEMO22 config]#` **`pwd`**

**`/opt/ibm/ondemand/V10.5/config`**

`[root@ECMUKDEMO22 config]#`

`[root@ECMUKDEMO22 config]#` **`chown archive:db2iadm1 ars*`**

**Note:** *For the configuration of a new installation, the following parameters must all match the username that the* ***CMOD*** *database runs under.*

*Also, on a* ***Linux*** *system, these parameters need to have a matching case!*

*If one is set to ‘****ARCHIVE****’ and the other is set to* **`'archive'`***,* **`arssockd`** *will log an* **`ARS0152E`** *error.*

*On the* ***RedHat Linux*** *system, the case of these values must match the case of the username defined in the operating system to avoid failure!*

*In* **`ars.ini`*:***

`SRVR_INSTANCE_OWNER=archive`

*In* **`ars.cfg`**:

*`DB2INSTANCE=archive`*

# [Setting the Db2 ARCHIVE Port 50001 Access on Windows](#toc.xhtml_s68a)

For the **Db2** communications to work through a **JDBC** network connection, the port **50001** used for the **Db2** instance, which we have available on **Windows**, must be open in the **Windows** **Firewall**. The procedure to configure this is described in the following section:

**Opening ports in the Windows Firewall:**

To Open port **50001:**

1.  From the Windows **`Start`** menu, select **`Control Panel`->`Windows Defender Firewall`**, as shown in *[Figure 5.25](#c05.xhtml_fig5_25)*:

    ![](images/Figure5.25.jpg)

    **Figure 5.25:** From the Windows ***Start*** menu, select the ***Control Panel->Windows Defender Firewall***

2.  Select **`Advanced Settings`**, as shown in *[Figure 5.26](#c05.xhtml_fig5_26)*:

    ![](images/Figure5.26.jpg)

    **Figure 5.26:** The ***Advanced Settings*** are selected

3.  Then, choose, under **`Windows Defender Firewall`**, the **`Inbound Rules`**, as shown in *[Figure 5.27](#c05.xhtml_fig5_27)*:

    ![](images/Figure5.27.jpg)

    **Figure 5.27:** Then, choose, under ***Windows Defender Firewall***, the ***Inbound Rules***

4.  Select **`New Rule`** by right-clicking the **`Inbound Rules`** node, as shown in *[Figure 5.28](#c05.xhtml_fig5_28):*

    ![](images/Figure5.28.jpg)

    **Figure 5.28:** Select ***New Rule*** by right-clicking the ***Inbound Rules*** node

5.  Choose the **`Port`** rule type, as highlighted, and select **`Next>`** in *[Figure 5.29](#c05.xhtml_fig5_29)*:

    ![](images/Figure5.29.jpg)

    **Figure 5.29:** Choose the ***Port*** rule type, as highlighted, and select ***Next***

6.  On the **`Protocol and Ports`** page, choose **`TCP`**, select **`Specific local ports`**, enter a value of **`50001`**, and select the **`Next>`** command, as shown in *[Figure 5.30](#c05.xhtml_fig5_30)*:

    ![](images/Figure5.30.jpg)

    **Figure 5.30:** Choose ***TCP*** and select ***Specific Local Ports*** and enter ***50001***, then Select ***Next>***

7.  On the **`Action`** page, select **`Allow the connection`** and select the **`Next>`** command button, as shown in *[Figure 5.31](#c05.xhtml_fig5_31):*

    ![](images/Figure5.31.jpg)

    **Figure 5.31:** On the ***Action*** page, select ***Allow the connection*** and select ***Next>***

8.  On the **`Profile`** page, select the **`Domain`** and **`Private`** options and untick the **`Public`** option, as shown in *[Figure 5.32](#c05.xhtml_fig5_32):*

    ![](images/Figure5.32.jpg)

    **Figure 5.32:** On the ***Profile*** page, select the ***Domain*** and ***Private*** options and untick the ***Public*** option

9.  Select **`Next`**.
10.  On the **`Name`** page, enter the name of **`DB2-CMOD-PORT`** and select **`Finish`**, as shown in *[Figure 5.33](#c05.xhtml_fig5_33)*:

    ![](images/Figure5.33.jpg)

    **Figure 5.33:** On the ***Name*** page, enter the name of ***DB2-CMOD-PORT***

11.  Restart the server.

The user and group security on the Linux server for the **CMOD GSKit** API path was updated:

**`[root@ECMUKDEMO22 ~]# chown archive:db2iadm1 /opt/ibm/db2/V11.5_01/lib64/gskit`**

After **Db2** is installed, IBM recommends that the user who owns the **Content Manager OnDemand** (**CMOD**) instance be added to the **Db2** instance owner’s group (the group name is **`db2iadm1`** on our installation of **Db2**).

After installing **Db2** on the library server, the following steps were followed:

1.  The **archive** user that owns the **CMOD** instance was added to the **Db2** instance owner’s group, **`db2iadm1`**. So, if the **Db2** instance owner’s group is **`db2iadm1`** and the Content Manager OnDemand instance owner is **archive**, specified by the **`SRVR_INSTANCE_OWNER`** parameter in the **`ars.ini`** file, add the **archive** user to the **`db2iadm1`** group.
2.  The **Db2** database links required must be created using the program: `/opt/ibm/db2/V11.5_01/cfg/db2ln`
3.  If a specific table space name for the **CMOD** system tables is created to store them in a separate table space, then the name of the table space should be specified using the **`ARS_DB_TABLESPACE`** parameter in the **`ars.cfg`** file.
4.  The value of the **`DB2INSTANCE`** parameter in the **`ars.cfg`** file must be filled. This value is case-sensitive. It must specify the name of the **Db2** instance (**archive** on our Linux system) that was created during the installation of Content Manager OnDemand. The default value is **archive**.

**IBM Db2** is set up and created with links for its files, using the steps as follows:

1.  The **root** user was logged into (or a user with **`sudo`** command permissions can be used) on the Linux system.
2.  Run the **`db2ln`** command.

Creating links for **Db2** is only required if the following two conditions apply:

*   There is only one copy of **Db2** installed on the computer.
*   The applications are required to be run, avoiding the need to specify the full path to the product libraries and include files.

The following restrictions apply:

*   If there are multiple **Db2** copies that are required to coexist, **do not create links** on the systems.
*   If existing links to the **`/usr/lib`** and **`/usr/include`** directories exist from a previous **Db2** database version, they will be removed automatically when links are created for the current **Db2** database version using the **`db2ln`** command.

**Note:** *To re-establish the links to the libraries of the previous version, run the* **`db2rmln`** *command from a current* ***Db2*** *database version before executing* **`db2ln`** *from the previous* ***Db2*** *database version*

Refer to the following link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=id-adding-user-db2-instance-owner-group](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=id-adding-user-db2-instance-owner-group) and [https://www.columbia.edu/sec/acis/db2/db2ix/db2ix03.htm#ToC_24](https://www.columbia.edu/sec/acis/db2/db2ix/db2ix03.htm#ToC_24)

We used the commands as follows on our **Linux** server:

**`/opt/ibm/db2/V11.5_01/cfg/db2ln`**

**`[root@ECMUKDEMO22 ~]# /opt/ibm/db2/V11.5_01/cfg/db2ln`**

**`[root@ECMUKDEMO22 ~]# su - archive`**

**`Last login: Fri Mar 29 12:09:25 PDT 2024 on pts/0`**

**`[archive@ECMUKDEMO22 ~]$ db2start`**

**`03/29/2024 12:39:32     0   0   SQL1026N  The database manager is already active.`**

**`SQL1026N  The database manager is already active.`**

**`[archive@ECMUKDEMO22 ~]$ db2`**

**`(c) Copyright IBM Corporation 1993,2007`**

`Command Line Processor for` **`DB2 Client 11.5.7.0`**

**`You can issue database manager commands and SQL statements from the command`**

**`prompt.` `For example:`**

**`db2 => connect to sample`**

**`db2 => bind sample.bnd`**

**`For general help, type: ?.`**

**`For command help, type: ?` `command, where command can be`**

**`the first few keywords of a database manager command.` `For example:`**

**`?` `CATALOG DATABASE for help on the CATALOG DATABASE command`**

**`?` `CATALOG          for help on all of the CATALOG commands.`**

**`To exit db2 interactive mode, type QUIT at the command prompt.` `Outside`**

**`interactive mode, all commands must be prefixed with`****`'``db2'.`**

**`To list the current command option settings, type LIST COMMAND OPTIONS.`**

**`For more detailed help, refer to the Online Reference Manual.`**

**`db2 => connect to archive`**

**`Database Connection Information`**

**`Database server        = DB2/LINUXX8664 11.5.7.0`**

**`SQL authorization ID   = ARCHIVE`**

**`Local database alias   = ARCHIVE`**

The following **db2** command was used to confirm that the **CMOD** database **schema** we were using was now set to **ARCHIVE**:

`db2 => list tables for schema archive`

`Table/View                Schema       Type  Creation time`

`----------------------- --------------- ----- --------------------------`

`ARSAG                     ARCHIVE      T     2024-03-28-13.35.31.316665`

`ARSAG2FOL                 ARCHIVE      T     2024-03-28-13.35.31.604908`

`ARSAGFLD                  ARCHIVE      T     2024-03-28-13.35.31.658139`

`ARSAGFLDALIAS             ARCHIVE      T     2024-03-28-13.35.31.720975`

`ARSAGINDEX                ARCHIVE      T     2024-03-28-11.31.20.345698`

`ARSAGPERMS                ARCHIVE      T     2024-03-28-13.35.31.801106`

`ARSANN                    ARCHIVE      T     2024-03-28-13.35.31.869669`

`ARSAPP                    ARCHIVE      T     2024-03-28-13.35.31.929580`

`ARSAPPUSR                 ARCHIVE      T     2024-03-28-13.35.32.026661`

`ARSCAB                    ARCHIVE      T     2024-03-28-11.31.21.858562`

`ARSCAB2FOL                ARCHIVE      T     2024-03-28-11.31.22.042035`

`ARSCABNAMES               ARCHIVE      T     2024-03-28-11.31.23.662214`

`ARSCABPERMS               ARCHIVE      T     2024-03-28-11.31.22.158247`

`ARSCFSODWORK              ARCHIVE      T     2024-03-28-11.31.22.352897`

`ARSCMFEDWORK              ARCHIVE      T     2024-03-28-11.31.23.236261`

`ARSFOL                    ARCHIVE      T     2024-03-28-13.35.32.373894`

`ARSFOLFLD                 ARCHIVE      T     2024-03-28-13.35.32.430213`

`ARSFOLFLDUSR              ARCHIVE      T     2024-03-28-13.35.32.486341`

`ARSFOLNAMES               ARCHIVE      T     2024-03-28-11.31.23.783006`

`ARSFOLPERMS               ARCHIVE      T     2024-03-28-13.35.32.600816`

`ARSFTIWORK                ARCHIVE      T     2024-03-28-11.31.23.454692`

`ARSGROUP                  ARCHIVE      T     2024-03-28-13.35.32.693769`

`ARSHOLD                   ARCHIVE      T     2024-03-28-11.31.22.635837`

`ARSHOLDMAP                ARCHIVE      T     2024-03-28-11.31.22.757879`

`ARSHOLDNAMES              ARCHIVE      T     2024-03-28-11.31.23.909428`

`ARSHOLDPERMS              ARCHIVE      T     2024-03-28-11.31.22.894906`

`ARSHOLDWORK               ARCHIVE      T     2024-03-28-11.31.23.081413`

`ARSLOAD                   ARCHIVE      T     2024-03-28-13.35.32.975066`

`ARSLOADWORK               ARCHIVE      T     2024-03-28-11.31.24.028690`

`ARSNAMEQ                  ARCHIVE      T     2024-03-28-13.35.33.129598`

`ARSNODE                   ARCHIVE      T     2024-03-28-13.35.33.212870`

`ARSPRT                    ARCHIVE      T     2024-03-28-13.35.33.319649`

`ARSPRTOPTS                ARCHIVE      T     2024-03-28-13.35.33.385733`

`ARSPRTUSR                 ARCHIVE      T     2024-03-28-13.35.33.448771`

`ARSRES                    ARCHIVE      T     2024-03-28-13.35.33.496959`

`ARSSEG                    ARCHIVE      T     2024-03-28-13.35.33.553968`

`ARSSET                    ARCHIVE      T     2024-03-28-13.35.33.673071`

`ARSSYS                    ARCHIVE      T     2024-03-28-13.35.33.751672`

`ARSUSER                   ARCHIVE      T     2024-03-28-13.35.33.798383`

`ARSUSRGRP                 ARCHIVE      T     2024-03-28-13.35.33.878501`

`ARSUSRGRPID               ARCHIVE      T     2024-03-28-13.35.33.933519`

`41 record(s) selected.`

The following **db2** command was used to confirm that the **CMOD** database **schema** we were using was no longer set to **ROOT**:

`db2 => list tables for schema root`

`Table/View                      Schema          Type  Creation time            `

`------------------------------- --------------- ------------------------`

`0 record(s) selected.`

`db2 => quit`

`DB20000I  The QUIT command completed successfully.`

`[archive@ECMUKDEMO22 ~]$`

`[archive@ECMUKDEMO22 bin]$ ./arsdb -k`

`/opt/ibm/ondemand/V10.5/bin/arsdd -C <zipfile> (UNIX only) Install OnDemand client files`

# [Creating the IBM FileNet Fixed Content Device Support for IBM Content Manager OnDemand](#toc.xhtml_s69a)

We found the following issue that needs to be corrected:

**`NOTE An unexpected exception occurred.` `Message was: ars3wapi32 Not found in java.library.path was displayed first.`**

To correct this error, we had to modify the **classpath** for the **IBM FileNet WebSphere** application server as follows:

The following was appended to the existing classpath:

**`/opt/ibm/ondemand/V10.5/www/api/ODApi.jar:/opt/ibm/ondemand/V10.5/jars/gson-2.10.1.jar:/opt/ibm/ondemand/V10.5/jars/log4j-api-2.20.0.jar:/opt/ibm/ondemand/V10.5/jars/log4j-core-2.20.0.jar:/opt/ibm/ondemand/V10.5/www/libars3wapi32.so:/opt/ibm/ondemand/V10.5/www/libars3wapi64.so`**

And the **IBM WebSphere Application Server** for IBM FileNet was restarted.

**Note**: *The base classpath configuration is described step-by-step in [Chapter 2, Installing CMOD on Linux Systems](#c02.xhtml), in the section "Configuring IBM FileNet P8 for a Fixed Content Device Using CMOD".*

# [Conclusion](#toc.xhtml_s70a)

In this chapter, we covered the step-by-step download, installation, and configuration of the **IBM Content Manager OnDemand** version **10.5** base and **Fix Pack 10.5.0.7** upgrade on a **Windows 11** server and some configuration on the connected Linux server.

In *[Chapter 6, Restarting the **CMOD** System on Linux](#c06.xhtml),* we will cover the restart of the Linux system server after upgrade and configuration. This covers the restart of the supporting systems, including the systems used for integration: **IBM Security Services** **LDAP** Directory server, **IBM FileNet P8 Content Engine** (used for the **CFS-CMOD** for a **Fixed Content Device**) and the **IBM Content Navigator** (used for the **CMOD** client Desktop and repository configuration).

# [Points to Remember](#toc.xhtml_s71a)

*   On the **RedHat Linux** system, remember that the following parameter values must match the case of the username defined in the operating system to avoid failure:

    In **`ars.ini`**:

    `SRVR_INSTANCE_OWNER=archive`

    In **`ars.cfg`**:

    `DB2INSTANCE=archive`

*   For the installation of **CMOD** on Windows, the following basic disk space is required as a minimum: **2GB** of free space on **C:\**.
*   During the **CMOD** installation on the **Windows** system, the **GSKit Version 8** used for the **Crypt** and **SSL** components are installed automatically.

# [Multiple Choice Questions](#toc.xhtml_s72a)

1.  Which of the following installation files contains **`setup.exe`** for the **IBM Content Manager OnDemand** Client installation for the **Windows 11** server?
    1.  `IBM_CMOD_V10.5_WIN_ML.zip`
    2.  `odwin64.zip`
    3.  `odwin32.zip`
    4.  `IBM_CONTENT_MANAGER_ONDEMAND_DIST.tar`
2.  Which of the following License agreements would be required for frequent **IBM CMOD V10.5** user access of 121 times or more in 12 months?
    1.  Process Value Unit, Production (**PVU**)
    2.  Eligible Participant (Eligible Participant **RVU**)
    3.  Authorized User (**UVU**)
    4.  Processor Value Unit, Non-Production (**Non-Prod PVU**)

# [Answers](#toc.xhtml_s73a)

1.  b
2.  c

# [Questions](#toc.xhtml_s74a)

1.  What security considerations and procedures would you follow to ensure the correct running of an IBM Content Manager OnDemand server system on a Windows 11 server?
2.  What security considerations and procedures would you follow to ensure the correct running of an IBM Content Manager OnDemand server system on a Linux server?

# [Key Terms](#toc.xhtml_s75a)

*   **UVU**: IBM Authorized User License, required for frequent **IBM CMOD V10.5** user access of 121 times or more in 12 months.
*   **PVU**: IBM Process Value Unit, Production License
*   **RVU**: IBM Eligible Participant License
*   **Non-Prod PVU:** IBM Non-Production Processor Value Unit License**.**
*   **TCP:** Transmission Control Protocol network communications use ports that are registered in the range of **1024** to **49151.**

    The ports from **49152** to **65535** can be used dynamically by applications as required. On **Linux** systems, these ports are defined in the **`/etc/services`** file.

# [CHAPTER 6](#toc.xhtml_c06)

# [Restarting the CMOD System on Linux](#toc.xhtml_c06)

# [Introduction](#toc.xhtml_s76a)

This chapter covers the restart of the Linux system server after upgrade and configuration, including the supporting application systems; the **IBM Directory Services**, **LDAP** server; the **IBM Db2**, database server; the **IBM WebSphere** web application server for the **IBM FileNet P8 Content Engine** and the **IBM Content Navigator**, desktop client.

The Linux command for the **root** user to reboot the server is as follows:

`shutdown -r now`

# [Structure](#toc.xhtml_s77a)

In this chapter, we will discuss the following topics:

*   Starting the **IBM Security Directory Services** Server
*   Starting the **Db2** Database Server
*   Starting the **IBM WebSphere** Profiles for **IBM FileNet P8 Content Engine** and **IBM FileNet Content Navigator**
*   Starting the **Linux CMOD** Object Server, the **`arsobjd`** Program
*   Resetting an Expired or Lost **CMOD ADMIN** User Password on **Db2**

# [Starting the IBM Security Directory Services Server](#toc.xhtml_s78a)

There are two configurations of the **IBM Security Directory** services server available, described as follows.

*   Installed as a standalone **.iso disk image** for **RedHat** Linux, the full free **ResearchGate** download installation document can be downloaded.

    See, [http://dx.doi.org/10.13140/RG.2.2.15737.83048](http://dx.doi.org/10.13140/RG.2.2.15737.83048)

    **“IBM BAW 18.0 Installation 18 07 2019 - Install of IBM Security Directory Suite 8.0.1.1 on RHEL 8 using VMWare Workstation Pro 15.1”**

    1.  The **IBM Security Directory Suite V8.0.1.1** web administration application is loaded using the **FireFox** web browser and the following **URL**:

        [https://192.168.50.131:12101/IDSWebApp/IDSjsp/Login.jsp](https://192.168.50.131:12101/IDSWebApp/IDSjsp/Login.jsp)

    2.  The **`User ID`** of **`cn=admin`** and the **`Password`** are entered, as shown in *[Figure 6.1](#c06.xhtml_fig6_1)*:

        ![](images/Figure6.1.jpg)

        **Figure 6.1:** The ***User ID*** of ***cn=admin*** and the ***Password*** are entered

    3.  The **`Server administration`**->**`Start/stop/restart`** **`server`** menu is selected, which allows the administrator to select the **`Start`**, **`Stop`,** and **`Restart`** command buttons as appropriate, depending on the current status of the server, as illustrated in *[Figure 6.2](#c06.xhtml_fig6_2)*:

        ![](images/Figure6.2.jpg)

        **Figure 6.2:** Select the ***Start***, ***Stop,*** and ***Restart*** command buttons as appropriate, depending on the Server status

    4.  The **`Server administration-> View server status`** menu option can be selected to view the details of the **LDAP** server, as shown in *[Figure 6.3](#c06.xhtml_fig6_3)*:

        ![](images/Figure6.3.jpg)

        **Figure 6.3:** The ***Server administration-> View server status*** menu option can be selected to view the server status

*   The **IBM Installation Manager** install procedure can be used to install an **LDAP** server on an existing **Linux** server operating system. There is also a free download from **ResearchGate**, which provides a step-by-step description of the installation steps:

    [http://dx.doi.org/10.13140/RG.2.2.33527.57761](http://dx.doi.org/10.13140/RG.2.2.33527.57761)

    **“IBM Security Directory Services 6.4- Installation on RHEL 8.0”**

    1.  The **Linux** server (which also has an installation of **IBM FileNet P8, Content Engine**) is logged onto as the **root** user, the **`Activities`** menu is selected as highlighted, and the **LDAP** server **`Instance Administration`** load application **icon** is selected, as illustrated in *[Figure 6.4](#c06.xhtml_fig6_4)*:

        ![](images/Figure6.4.jpg)

        **Figure 6.4:** The highlighted Activities menu is selected and the LDAP server Instance Administration load application icon is selected

    2.  The **`Activities`** **->** **`Terminal Window`** icon is selected as highlighted, and then the **Db2** database start commands are entered into the command window, as highlighted in *[Figure 6.5](#c06.xhtml_fig6_5)*:

        ![](images/Figure6.5.jpg)

        **Figure 6.5:** The ***Instance Administration*** icon launches the ***IBM Security Directory*** server control panel

    3.  The **`Start/Stop`** command button, highlighted in *[Figure 6.5](#c06.xhtml_fig6_5)*, is selected to display the **`Start server`** and **`Start administration server`** command buttons, highlighted in *[Figure 6.6](#c06.xhtml_fig6_6)*:

        ![](images/Figure6.6.jpg)

        **Figure 6.6:** The ***Start server*** and ***Start administration server*** command buttons

    4.  The **`Start server`** command button is selected first, and after around five minutes, the **`OK`** icon shown in *[Figure 6.7](#c06.xhtml_fig6_7)* indicates that the **LDAP** server has started.

        ![](images/Figure6.7.jpg)

        **Figure 6.7:** The ***Start server*** command button is selected and after five minutes, the ***OK*** icon is shown

    5.  The **`Start administration server`** command button is then selected, and the completion status of the server start is illustrated in *[Figure 6.8](#c06.xhtml_fig6_8)*:

        ![](images/Figure6.8.jpg)

        **Figure 6.8:** The ***Start administration server*** command button shows the status of the running server and the ***OK*** command can be selected

    6.  The Instance **`Start/Stop`** panel can now be closed using the **`Close`** command button, as highlighted in *[Figure 6.9](#c06.xhtml_fig6_9)*:

        ![](images/Figure6.9.jpg)

        **Figure 6.9:** The ***Instance Start/Stop*** panel is closed using the ***Close*** command

    7.  The main **IBM Security Directory Server Instance** display shows the two service programs have been started, as shown in *[Figure 6.10](#c06.xhtml_fig6_10)*, and this can now be closed:

        ![](images/Figure6.10.jpg)

        **Figure 6.10:** The main ***IBM Security Directory Server Instance*** display with two service programs started

# [Starting the Db2 Database Server](#toc.xhtml_s79a)

1.  The Linux IBM Content Manager OnDemand Db2 database server is started using the commands run by the archive user logging into the Linux server, as shown in *[Figure 6.11](#c06.xhtml_fig6_11):*

    ![](images/Figure6.11.jpg)

    **Figure 6.11:** The ***archive*** user icon is selected on the rebooted ***Linux*** server as highlighted

2.  The **archive** user’s password is prompted for sign-on to the **Linux** desktop, as shown in *[Figure 6.12](#c06.xhtml_fig6_12)*:

    ![](images/Figure6.12.jpg)

    **Figure 6.12:** The ***archive*** user’s password is prompted for sign-on to the ***Linux*** desktop

3.  The **`Activities`** **->`Terminal Window`** icon is selected as highlighted, and then the **Db2** database start commands are entered into the resulting command window, as highlighted in *[Figure 6.13](#c06.xhtml_fig6_13)*:

    ![](images/Figure6.13.jpg)

    **Figure 6.13:** The highlighted Activities menu is selected and the Db2 database start commands are entered

    `[archive@ECMUKDEMO22 ~]$db2 start database manager`

    `SQL1026N  The database manager is already active.`

    `[archive@ECMUKDEMO22 ~]$db2 activate database archive`

    `DB20000I  The ACTIVATE DATABASE command completed successfully.`

    `[archive@ECMUKDEMO22 ~]$`

# [Starting the IBM WebSphere Profiles for IBM FileNet P8 Content Engine and IBM FileNet Content Navigator](#toc.xhtml_s80a)

From the **archive** user’s command window, we can log on as the **root** user, using the command:

`su - root`

We can then change to the **IBM WebSphere** application server **bin** directory and start the **IBM FileNet P8 Content Engine** server (which is using the **IBM WebSphere AppSrv01** web application profile), as shown in *[Figure 6.14](#c06.xhtml_fig6_14)*:

![](images/Figure6.14.jpg)

**Figure 6.14:** We start the ***IBM FileNet P8 Content Engine*** server (which is using the ***AppSrv01*** profile)

The commands to start the **IBM FileNet P8 Content Engine** Web application server, are as follows:

`cd /opt/IBM/WebSphere/AppServer/profiles/AppSrv01/bin`

`./startServer.sh server1`

We can now move to the **IBM Content Navigator** web application server profile (which is using the **AppSrv02** profile) bin directory, and start the web application, as shown in *[Figure 6.15](#c06.xhtml_fig6_15):*

![](images/Figure6.15.jpg)

**Figure 6.15:** We start the ***IBM Content Navigator*** web application server

The commands to start the **IBM Content Navigator** web application server from the **AppSrv02** profile are as follows (assuming we are starting from the **IBM FileNet P8 Web Application bin** directory, **`/opt/IBM/WebSphere/AppServer/profiles/AppSrv01/bin`**):

`cd ../../AppSrv02/bin`

`./startServer.sh server1`

# [Starting the Linux CMOD Object Server, the arsobjd Program](#toc.xhtml_s81a)

The **archive** user logs on to start the **IBM Content Manager OnDemand (CMOD)** Object Server using the following highlighted command after exiting the root user and starting the **IBM FileNet P8** and **IBM Content Navigator** web application servers:

`[root@ECMUKDEMO22 bin]# exit`

`logout`

`[archive@ECMUKDEMO22 ~]$/opt/ibm/ondemand/V10.5/bin/arsobjd -v -S -I archive`

`ARS0462I Server Version: 10.5.0.7`

`ARS0463I Operating System: Linux #1 SMP Fri Jun 2 08:27:19 EDT 2023.4.18.0-477.15.1.el8_8.x86_64`

`ARS0464I Install Location: /opt/ibm/ondemand/V10.5/`

`ARS0465I Limits: Data(unlimited KB) Stack(8192 KB) Core(0 512-blocks) Cpu(unlimited seconds) File(unlimited 512-blocks) Nofiles(1024) Threads(0) Processes(127300)`

`ARS0285I Setting server locale: en_US.UTF-8`

`ARS0288I Object server starting`

`ARS0291I Server instance: ARCHIVE`

`ARS0295I -------- Start of server configuration information --------`

`[@SRV@_ARCHIVE]`

`PROTOCOL=2`

`PORT=1445`

`SRVR_INSTANCE=ARCHIVE`

`SRVR_INSTANCE_OWNER=archive`

`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.cfg`

`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.dbfs`

`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.cache`

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`

`HOST=ECMUKDEMO22`

`[CFG]`

`ARS_SRVR=LibSrvr`

`ARS_LOCAL_SRVR=ECMUKDEMO22`

`ARS_SUPPORT_HOLD=1`

`ARS_SUPPORT_CFSOD=1`

`ARS_ORIGINAL_CODEPAGE=1208`

`ARS_NUM_DBSRVR=0`

`DB2INSTANCE=archive`

`ARS_TMP=/tmp`

`ARS_PRINT_PATH=/tmp`

`ARS_DB_ENGINE=DB2`

`ARS_DB_IMPORT=0`

`ARSSOCK=debug`

`ARS_DB2_DATABASE_PATH=/arsdb`

`ARS_DB2_PRIMARY_LOGPATH=/arsdb_primarylog`

`ARS_DB2_ARCHIVE_LOGPATH=/arsdb_archivelog`

`ARS_DB2_LOGFILE_SIZE=1000`

`ARS_DB2_LOG_NUMBER=40`

`ARS_DB2_TSM_CONFIG=/opt/tivoli/tsm/client/api/bin/dsm.opt.db2`

`ARS_ORACLE_HOME=/oracle`

`ARS_STORAGE_MANAGER=CACHE_ONLY`

`ARS_LDAP_SERVER=ECMUKDEMO77`

`ARS_LDAP_PORT=389`

`ARS_LDAP_BASE_DN=cn=localhost`

`ARS_LDAP_BIND_DN=cn=P8Admin,cn=localhost`

`ARS_LDAP_BIND_DN_PWD=filenet`

`DSMSERV_DIR=/opt/tivoli/tsm/server/bin`

`DSMSERV_CONFIG=/opt/tivoli/tsm/server/bin/dsmserv.opt`

`DSM_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSM_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSM_LOG=/tmp`

`DSMG_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMG_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMG_LOG=/tmp`

`DSMI_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMI_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMI_LOG=/tmp`

`ARS_NUM_LICENSE=1`

`[DBFS]`

`DBFS_NUM=0`

`[CACHE]`

`SMFS1=/arscache/cache1`

`SMFS_NUM=1`

`--------- End of server configuration information ---------`

`ARS0294I Activate server trace for more information`

`[archive@ECMUKDEMO22 ~]$ ARS0351I The arsobjd instance ARCHIVE is ready`

`[archive@ECMUKDEMO22 ~]$`

We can now check that the **IBM CMOD Object** server has loaded correctly and is active using the following **Linux** memory query, as illustrated in *[Figure 6.16](#c06.xhtml_fig6_16)*:

`[archive@ECMUKDEMO22 ~]$`

`[archive@ECMUKDEMO22 ~]$ps -eaf|grep arsobjd`

`archive    13257    5176  0 09:29 pts/0    00:00:00 arsobjd: (accepting)`

`archive    14168    6260  0 09:40 pts/0    00:00:00 grep --color=auto ars`

![](images/Figure6.16.jpg)

**Figure 6.16:** We check that the ***IBM CMOD Object*** server has loaded correctly and is active

# [Resetting an Expired or Lost CMOD ADMIN User Password on Db2](#toc.xhtml_s82a)

We have encountered an error during the installation and use of the Eclipse Java program (covered in detail in *[Chapter 9, CMOD Java API Examples](#c09.xhtml)*)

Using Eclipse, we had the error:

`Encountered error: Change Expired Logon Password`

`Error code: 2061`

The following link provided a solution:

**[https://www.ibm.com/support/pages/recovery-lost-password-super-id-admin-content-manager-ondemand](https://www.ibm.com/support/pages/recovery-lost-password-super-id-admin-content-manager-ondemand)**

The database for **CMOD** is used to store the **ADMIN** user password after logging in for the first time. Because this password is encrypted, it cannot be viewed or copied. So, if the password is lost, it cannot be recovered. The only method to get access to **CMOD** again is to set the password to a **nullstring** in the **CMOD** database table, **`archive.arsuser`**, using the **Db2** database **SQL** command, as follows:

`update arsuser set passwd='' where userid='ADMIN'`

**Note**: *You need to ensure that there is no space between the two single quotes in the statement words* ***`set passwd=''`***.

*After resetting the password to a* ***null string****, the* ***CMOD*** *client system can be used to log on to the server without typing the password and it can then be changed for the* ***ADMIN*** *user to a new value.*

# [Conclusion](#toc.xhtml_s83a)

In this chapter, we covered the step-by-step procedure for restarting the **Linux** system server after an upgrade, configuration, and the required reboot step.

We described the startup order and the steps for starting the supporting application systems; the **IBM Directory Services**, **LDAP** server; the **IBM Db2**, database server; the **IBM WebSphere** web application server for the **IBM FileNet P8 Content Engine** and the **IBM Content Navigator**, desktop client. We also described the procedure to reset the **CMOD ADMIN** user password, and illustrated the command for starting the Linux **CMOD** **Object Server**, using the **arsobjd** program.

In the next chapter, titled ***CMOD*** *Administration on Windows,* we will cover **CMOD** administration using the Windows **OnDemand Configurator** program **V10.5**, the use of the Windows **OnDemand Client configuration** program, the use of the **`arsxml`** command on Windows, and the configuration of the system after installing **CMOD Fix Pack 10.5.0.7**.

# [Points to Remember](#toc.xhtml_s84a)

*   It is important to reboot the **Linux** and **Windows** servers to allow system shared object libraries to be updated in the server memory. The **Linux** command for the **root** user to reboot the server is `shutdown -r now`.
*   There are two different configurations of the **IBM Security Directory Services** server available: the **.iso** disk version, **IBM Security Directory Suite 8.0.1.1,** and the **IBM Installation Manager** installed version, **IBM Security Directory Services 6.4**.
*   You can check that the **IBM CMOD Object server** has loaded correctly and is active using the **Linux** memory query, `ps -eaf|grep arsobjd`
*   The **IBM Content Manager OnDemand, ADMIN** user’s password can be reset by updating the **CMOD** database table, **archive.arsuser**, using the**Db2** database **SQL** command: `update arsuser set passwd='' where userid='ADMIN'`

# [Multiple Choice Questions](#toc.xhtml_s85a)

1.  Which of the following **Linux** commands is used to start the **CMOD Object** Server program?
    1.  `./startServer.sh server1`
    2.  `/opt/ibm/ondemand/V10.5/bin/arsobjd -v -S -I archive`
    3.  `db2 start database manager`
    4.  `../bin/arsdb -gkv`
2.  Which user do we log into after rebooting the **Linux CMOD** server to restart the **IBM CMOD Db2** system?
    1.  `db2inst1`
    2.  `root`
    3.  `archive`
    4.  `ECMUKDEMO22`

# [Answers](#toc.xhtml_s86a)

1.  b
2.  c

# [Questions](#toc.xhtml_s87a)

1.  Why is it important to reboot the **Linux** server after installing an upgrade for the **IBM CMOD** system?
2.  What IBM supporting systems are required to be started first to ensure that the **IBM FileNet P8 Content Engine** server **acce** web application administrator user logon will succeed?
3.  What procedure would you follow if you saw the error as follows:

    `Encountered error: Change Expired Logon Password`

    `Error code: 2061`

4.  Can you list the software dependencies and their functions that are required for the correct operation of the IBM Content Navigator CMOD desktop client?

# [Key Terms](#toc.xhtml_s88a)

*   **API**: Application Programmer’s Interface is a library of callable software subroutines written to support the intercommunication between two or more separate functional software systems.
*   **SQL: Structured Query Language** is a set of commands with a standard syntax, used to **create**, **update**, **query,** or **delete** the **rows**, **tables**, **indexes**, **views**, **stored procedures,** and **functions** in a relational database.
*   **URL: Uniform** **Resource Locator** is a web address reference to a resource on the Internet.

# [CHAPTER 7](#toc.xhtml_c07)

# [CMOD Administration on Windows](#toc.xhtml_c07)

# [Introduction](#toc.xhtml_s89a)

This chapter describes the **Windows** **OnDemand Configurator** program **V10.5**, the **Windows OnDemand Client configuration** program, the use of the **ARSXML** command on **Windows,** and the configuration of the system after installing **CMOD Fix Pack 10.5.0.7**.

We will describe the use of the **ARSXML** program to export and import **CMOD** **Application Groups** and the step-by-step procedure to add a new **Folder** and **Application Group** object using the **Windows OnDemand Administrator** program.

Using the new **Windows OnDemand Administrator V10.5 (64-bit)** program, we can display the graphical user interface (GUI) administration nodes for managing **Users**, **Groups**, **Applications**, **Application Groups**, **Storage Sets**, **Folders**, **Cabinets**, **Printers,** and **Holds**. We will also demonstrate some of the features of the program to create the associated **Fields**, **Field Types,** and **Indexes** of an **Application Group**. We will end this section by describing the procedure and the reasons required for deleting an existing **Application Group**.

# [Structure](#toc.xhtml_s90a)

In this chapter, we will discuss the following topics:

*   Updating the **Windows ADMIN** Password
*   Updating the **Windows Server Firewall**
*   The **OnDemand Configurator V10.5** – Server **Instance** Creation
    *   The **OnDemand Client** Configuration
*   The **arsxml** Command Use on **Windows**
*   Configuring the System After Installing **CMOD Fix Pack 10.5.0.7**

# [Updating the Windows ADMIN Password](#toc.xhtml_s91a)

We have previously described, in *[Chapter 6, Starting the **CMOD** System on **Linux**](#c06.xhtml)*, the **Db2 SQL** used on a **Linux** server to enable the resetting of the **ADMIN** administration user’s password. On the **Windows** server, we entered an **ADMIN** password as part of the installation set with just six characters, which was initially accepted. However, the system subsequently validates the stored password and only accepts a minimum of nine characters!

As referenced earlier, the following link provided a solution:

**[https://www.ibm.com/support/pages/recovery-lost-password-super-id-admin-content-manager-ondemand](https://www.ibm.com/support/pages/recovery-lost-password-super-id-admin-content-manager-ondemand)**

We had to completely remove the encrypted 6-character password from the **Db2** table field to allow a new 9-character password to be entered. The procedure to do this used the following commands:

1.  Using the **Db2** command window on the **Windows** server, as illustrated in *[Figure 7.1](#c07.xhtml_fig7_1):*

    `Db2`

    `Connect to ARCHIVE`

    `select userid from alan_.arsuser;`

    `update alan_.arsuser set passwd='' where userid='ADMIN'`

    `commit`

    `quit`

    ![](images/Figure7.1.jpg)

    **Figure 7.1:** Using the ***Db2*** command window ***SQL*** on the ***Windows*** server to clear the ***ADMIN*** user’s password

2.  We must then start the **CMOD** **`OnDemand`** client and log on to the Windows server, **`DESKTOP-B3JB93R`,** using the **`ADMIN`** user name **without typing the password**, as shown in *[Figure 7.2](#c07.xhtml_fig7_2):*

    ![](images/Figure7.2.jpg)

    **Figure 7.2:** Log on to the Windows server, using the ***ADMIN*** user name ***without typing the password***

3.  We can then open our Windows **`DESKTOP-B3JB93R`** server node and select the **`Users`** node to list the **`ADMIN`** user entry, as highlighted in *[Figure 7.3](#c07.xhtml_fig7_3)*:

    ![](images/Figure7.3.jpg)

    **Figure 7.3:** Select the ***Users*** node to list the ***ADMIN*** user entry

4.  We can then right-click the **`ADMIN`** **`User ID`** field to display the properties, as illustrated in *[Figure 7.4](#c07.xhtml_fig7_4)*:

    ![](images/Figure7.4.jpg)

    **Figure 7.4:** We use a right-click on the ***ADMIN*** ***User ID*** field to display the properties

5.  We can now update the **`ADMIN`** user account to provide a nine-character (minimum) password, as shown in *[Figure 7.5](#c07.xhtml_fig7_5)*:

    ![](images/Figure7.5.jpg)

    **Figure 7.5:** We can now update the ***ADMIN*** user account to provide a nine-character (minimum) password

6.  We enter the **`New Password`** and the **`Verify Password`** fields with the same 9-character password and click the **`Update`** command button, as shown in *[Figure 7.5](#c07.xhtml_fig7_5)*. Then, we must clear the **`Current Password`** field completely and click the **`OK`** command button, as shown in *[Figure 7.6](#c07.xhtml_fig7_6)***,** to set the **`New Password`** we entered:

    ![](images/Figure7.6.jpg)

    **Figure 7.6:** We must clear the ***Current Password*** field completely and click the ***OK*** command button

# [Updating the Windows Server Firewall](#toc.xhtml_s92a)

1.  The Windows Defender Firewall is loaded to update the port used by the **CMOD** program, as shown in *[Figure 7.7](#c07.xhtml_fig7_7)*:

    ![](images/Figure7.7.jpg)

    **Figure 7.7:** The Windows Defender Firewall is loaded to update the port used by the ***CMOD*** program

2.  The **`Add`** command is clicked to load the Windows Server Firewall, as highlighted in *[Figure 7.8](#c07.xhtml_fig7_8):*

    ![](images/Figure7.8.jpg)

    **Figure 7.8:** The ***Add*** command is clicked to load the Windows Server Firewall

3.  The **`Private`** Network type is selected, and the **`OK`** command button clicked, as highlighted in *[Figure 7.9](#c07.xhtml_fig7_9)*:

    ![](images/Figure7.9.jpg)

    **Figure 7.9:** The ***Private*** Network type is selected and the ***OK*** command button clicked

4.  The following options are set for **`IBM Content Manager OnDemand`**, as shown in *[Figure 7.10](#c07.xhtml_fig7_10)*:

    ![](images/Figure7.10.jpg)

    **Figure 7.10:** The options highlighted are set for ***IBM Content Manager OnDemand***

# [The OnDemand Client Folder Selection](#toc.xhtml_s93a)

The **Windows IBM Content Manager OnDemand** server maintains detailed logs of user and system program connections in a **`System Log`** folder and also records documents loaded to the **CMOD** system in a **`System Load`** folder.

The **Administrator** user, **`ADMIN`**, can review these actions recorded in the folders to monitor the document database access for security checks and to check the performance and load on the system using the **Windows Startup Menu** program**, OnDemand Client V10.5 (64-bit)** in the path, **`C:\Program Files\IBM\OnDemand Clients\V10.5\bin\arsgui.exe`**.

We can now run the **`OnDemand`** client and open the **`System Load logging`** folder, as highlighted in *[Figure 7.11](#c07.xhtml_fig7_11)*:

![](images/Figure7.11.jpg)

**Figure 7.11:** The ***OnDemand*** client is selected as highlighted and the ***System Load Logging*** folder opened

# [The OnDemand Configurator Password Load Program Update Option](#toc.xhtml_s94a)

Using the **`ARCHIVE`** **`Properties`** of the OnDemand Configurator program, we can now enter the **`ADMIN`** user name and the 9-character password to be used for the Load program, as shown in *[Figure 7.12](#c07.xhtml_fig7_12)*:

![](images/Figure7.12.jpg)

**Figure 7.12:** Using the ***ARCHIVE*** properties, we can now enter the ***ADMIN*** user name and the 9-character password

The Windows **`OnDemand Configurator`** program is loaded to display the **`ARCHIVE`** services, as shown in *[Figure 7.13](#c07.xhtml_fig7_13)*:

![](images/Figure7.13.jpg)

**Figure 7.13:** The ***Services*** node is selected to list the service program names and statuses

# [The OnDemand Configurator V10.5 – Server Instance Creation](#toc.xhtml_s95a)

1.  We can select the **IBM Content Manager OnDemand Configurator** program to give access to the Server Instance Creation function, as shown in *[Figure 7.14](#c07.xhtml_fig7_14):*

    ![](images/Figure7.14.jpg)

    **Figure 7.14:** The ***IBM Content Manager OnDemand Configurator*** program to give access to the Server Instance Creation function

2.  The first (default) instance we need to create is given the name **`ARCHIVE`,** as shown in *[Figure 7.15](#c07.xhtml_fig7_15)*:

    ![](images/Figure7.15.jpg)

    **Figure 7.15:** The first (default) instance we need to create is given the name of ***ARCHIVE***

3.  The default **Windows** system temporary path of **`c:\arstmp`** for the **Print** and system programs is left, and we are then prompted by the **CMOD Configurator** program to create the **`arstmp`** sub-folder, as shown in *[Figure 7.16](#c07.xhtml_fig7_16)*:

    ![](images/Figure7.16.jpg)

    **Figure 7.16:** We are prompted by the ***CMOD Configurator*** program to create the ***arstmp*** sub-folder

4.  On selecting the **`Next>`** command button, we are prompted to select from the **`Library and Object server`** or **Object server only** options. We choose the **`Library and Object server`** option, and we also choose the **`LDAP`** server as our Linux based **`ECMUKDEMO77`**. Then we click the **`Advanced Options…`** command button, as shown in *[Figure 7.17](#c07.xhtml_fig7_17)*:

    ![](images/Figure7.17.jpg)

    **Figure 7.17:** Click the ***Advanced Options…*** command button

5.  The option to **`Enable CFS-CMOD`** is selected, and the **`OK`** command button is selected, as highlighted in *[Figure 7.18](#c07.xhtml_fig7_18)*:

    ![](images/Figure7.18.jpg)

    **Figure 7.18:** The option to ***Enable CFS-CMOD*** is selected and the ***OK*** command button is selected

6.  On selecting the **`Next>`** command button, the default ports are displayed to connect to an **IBM FileNet P8 Content Engine** server using the **CFS-CMOD** Fixed Content Device (**`32775`**) and the **Non-SSL** client-server port number (**`1445`**). The **`OK`** command button is then selected to confirm these port settings, as highlighted in *[Figure 7.19](#c07.xhtml_fig7_19)*:

    ![](images/Figure7.19.jpg)

    **Figure 7.19:** On selecting the ***Next>*** command button the default ports are displayed

7.  The user and password are entered, and a **`DATA`** load directory is selected using the **`Browse…`** command, as shown in *[Figure 7.20](#c07.xhtml_fig7_20)*:

    ![](images/Figure7.20.jpg)

    **Figure 7.20:** The user and password are entered and a ***DATA*** load directory selected using the ***Browse…*** command

    **Note:** *It is important to enter at least nine characters for the password, as there is no validation of this at this point, and the encrypted password is stored in a database table. A password entered with less than nine characters will lockout the Administrator user.*

8.  After entering the Administrator User and password, the **`Next>`** command is selected, as shown in *[Figure 7.21](#c07.xhtml_fig7_21)*:

    ![](images/Figure7.21.jpg)

    **Figure 7.21:** After entering the Administrator User and password, the ***Next>*** command is selected

9.  The **`java.exe`** program and full path are selected, and the default sleep times are left, as shown in *[Figure 7.22](#c07.xhtml_fig7_22)*:

    ![](images/Figure7.22.jpg)

    **Figure 7.22:** The java.exe program and full path are selected using the ***Browse..*** command and ***Next>*** selected

10.  The database type is selected as **Db2,** the instance name left as the default of **ARCHIVE** and the username of **`alan_`** (the default is the logged on Windows server user), and the **`Next>`** command is selected as shown in *[Figure 7.23](#c07.xhtml_fig7_23)*.

    ![](images/Figure7.23.jpg)

    **Figure 7.23:** The database type is selected as ***Db2*** with a default Instance of ***ARCHIVE*** and the user’s name of ***alan_***

11.  We are prompted to create the **`c:\arsdbpri`** directory with a pop-up window which we select **`Yes`** for, as illustrated in *[Figure 7.24](#c07.xhtml_fig7_24)*:

    ![](images/Figure7.24.jpg)

    **Figure 7.24:** Create the ***c:\arsdbpri*** directory with a pop-up window by selecting ***Yes***

12.  We are prompted to create the **`c:\arsdbarc`** directory with a pop-up window, which we select **`Yes`** for, as illustrated in *[Figure 7.25](#c07.xhtml_fig7_25)*:

    ![](images/Figure7.25.jpg)

    **Figure 7.25:** Create the ***c:\arsdbarc*** directory with a pop-up window by selecting ***Yes***

13.  After selecting the **`Next>`** command button, we select the **`Cache`** file system option and enter the path to the **`c:\arscache1`** folder, as shown in *[Figure 7.26](#c07.xhtml_fig7_26)*:

    ![](images/Figure7.26.jpg)

    **Figure 7.26:** After selecting the ***Next>*** command button, we select the ***Cache*** file system option with ***c:\arscache1***

14.  On selecting the **`Finish`** command button, we enter the required **`User ID`** and **`Password`** of a **Windows Systems** administrator, and select **`OK`**, as shown in *[Figure 7.27](#c07.xhtml_fig7_27):*

    ![](images/Figure7.27.jpg)

    **Figure 7.27:** We enter the required ***User ID*** and ***Password*** of a ***Windows Systems*** administrator, and select ***OK***

15.  After selecting the **`OK`** command button for the required **User ID** and **Password** of a **Windows Systems** administrator, we get the status, as highlighted in *[Figure 7.28](#c07.xhtml_fig7_28)*, and then select the **`Create Local Database Now`** command button:

    ![](images/Figure7.28.jpg)

    **Figure 7.28:** We get the status as highlighted and then select the ***Create Local Database Now*** command button

16.  The status of the **OnDemand Database** and the Log table creation progress are displayed, as shown in *[Figure 7.29](#c07.xhtml_fig7_29):*

    ![](images/Figure7.29.jpg)

    **Figure 7.29:** The status of the Database creation progress are displayed

17.  On the completion of the creation of the Database and Log tables, we get a summary of the final status, as shown in *[Figure 7.30](#c07.xhtml_fig7_30)*:

    ![](images/Figure7.30.jpg)

    **Figure 7.30:** On completion of the creation for the Database and Log/Load tables, the final status is displayed

18.  The **`OnDemand Configurator`** program shows the **`Services`,** **`Current Status`** column as all stopped, as highlighted in *[Figure 7.31](#c07.xhtml_fig7_31)*:

    ![](images/Figure7.31.jpg)

    **Figure 7.31:** The ***OnDemand Configurator*** program shows the ***Services,*** ***Current Status*** column as all stopped

The **`OnDemand`** **`LibSrvr`** service for the **IBM CMOD** system is the core service to enable the storage of **IBM CMOD** documents and their attributes to the **Windows ARCHIVE** instance database.

The **`OnDemand`** **`MVSD`** service supports access to a remote system for downloading data from an **IBM** **zOS** mainframe server to the **Windows ARCHIVE** instance**.**

The **`OnDemand Load Data`** service monitors one or more **Windows** server directory folders to load documents automatically as they are copied to these folders.

The **`OnDemand Scheduler`** service sets up program tasks that maintain the database and cache storage and are required to run on a regular schedule. When a task has been configured and enabled to run, the **IBM Content Manager OnDemand** **Scheduler** service runs the task on the defined schedule.

We can right-click each Service in turn to Start it, as exemplified in *[Figure 7.32](#c07.xhtml_fig7_32):*

![](images/Figure7.32.jpg)

**Figure 7.32:** We can right-click each Service in turn to Start it

The **`Current Status`** column of the **CMOD OnDemand LibSrvr** service for the default **ARCHIVE** instance is now shown as **`Running`**, as highlighted in *[Figure 7.33](#c07.xhtml_fig7_33)*:

![](images/Figure7.33.jpg)

**Figure 7.33:** The ***Current Status*** column of the ***CMOD OnDemand LibSrvr*** service for the default ***ARCHIVE*** instance is now shown as ***Running***

We can now view the **CMOD** **`admin`** local user account created on our Windows server, as shown in *[Figure 7.34](#c07.xhtml_fig7_34)*:

![](images/Figure7.34.jpg)

**Figure 7.34:** We can now view the ***CMOD*** ***admin*** local user account created on our Windows server

# [The OnDemand Client Configuration](#toc.xhtml_s96a)

In this section, we are going to install the **IBM OnDemand** client. The **IBM Content Manager OnDemand** client system can only be installed on **Windows** systems. (There are **32-bit** and **64-bit** versions of the client programs.)

1.  The **Windows OnDemand client 64-bit** installation is unpacked from the downloaded **`odwin64.zip`** file, as shown in *[Figure 7.35](#c07.xhtml_fig7_35)*:

    ![](images/Figure7.35.jpg)

    **Figure 7.35:** The Windows OnDemand client installation is unpacked from the downloaded ***odwin64.zip*** file

2.  The right-click on the **`odwin64.zip`** file is used to select the **`Extract Compressed (Zipped) Folders`** option, as highlighted in *[Figure 7.36](#c07.xhtml_fig7_36)*:

    ![](images/Figure7.36.jpg)

    **Figure 7.36:** Right-click the ***odwin64.zip*** file to select the ***Extract Compressed (Zipped) Folders*** option

3.  The status of the extraction of the 190 Mbytes of installation files is shown in *[Figure 7.37](#c07.xhtml_fig7_37):*

    ![](images/Figure7.37.jpg)

    **Figure 7.37:** The status of the extraction of the 190 Mbytes of installation files

4.  The installed **`OnDemand V10.5 Client (64-bit)`** program can be accessed from the Windows server, as highlighted in *[Figure 7.38](#c07.xhtml_fig7_38)*:

    ![](images/Figure7.38.jpg)

    **Figure 7.38:** The installed ***OnDemand V10.5 Client (64-bit)*** program can be accessed from the Windows server

5.  The Linux **`ECMUKDEMO22`** server can be added, as shown in *[Figure 7.39](#c07.xhtml_fig7_39).*

    (The Attempt Unified Logon option only works for a Windows-based server system. The port for the Linux **`ECMUKDEMO22`** was changed to **1445**.)

    ![](images/Figure7.39.jpg)

    **Figure 7.39:** The Linux ***ECMUKDEMO22*** server can be added

6.  The user name and password are entered, as highlighted in *[Figure 7.40](#c07.xhtml_fig7_40):*

    ![](images/Figure7.40.jpg)

    **Figure 7.40:** The user name and password are entered, as highlighted

7.  The Windows **`OnDemand Command Prompt`** command window is loaded, and we can then run the **`arssockd`** program, as highlighted, to start the default **CMOD** **ARCHIVE** instance:

    This uses the command highlighted in *[Figure 7.41](#c07.xhtml_fig7_41):*

    `arssockd -I ARCHIVE -p`

    ![](images/Figure7.41.jpg)

    **Figure 7.41:** The Windows ***OnDemand Command Prompt*** window is loaded and we run the ***arssockd*** program

8.  The properties of the **`System Table Maintenance`** service for the **`ARCHIVE`** instance are selected using the Windows **`OnDemand Configurator`**, using a right-click, as illustrated in *[Figure 7.42](#c07.xhtml_fig7_42)*:

    ![](images/Figure7.42.jpg)

    **Figure 7.42:** The properties of the ***System Table Maintenance*** service for the ***ARCHIVE*** instance are selected using the Windows ***OnDemand Configurator***

9.  The **`arsdb`** program used for scheduled maintenance of the **`ARCHIVE`** instance **Db2** **Tables** is **`Enabled`** using the tick-box as highlighted in *[Figure 7.43](#c07.xhtml_fig7_43)*:

    ![](images/Figure7.43.jpg)

    **Figure 7.43:** The ***arsdb*** program used for a scheduled maintenance of the ***ARCHIVE*** instance ***Db2*** ***Tables*** is ***Enabled***

10.  The **`arsdb`** program runtime switches can be seen on the **`Options`** tab, as shown in *[Figure 7.44](#c07.xhtml_fig7_44)*:

    (The use of the **`arsdb`** program is covered in more detail in *[Chapter 11, Starting arssockd on the Linux Server](#c11.xhtml)*.)

    ![](images/Figure7.44.jpg)

    **Figure 7.44:** The ***arsdb*** program runtime switches can be seen on the ***Options*** tab

11.  The **`Schedule`** tab allows the **`arsdb`**, **`System Table Maintenance`** program, to be configured to run at a regular time with the settings as required, as illustrated in *[Figure 7.45](#c07.xhtml_fig7_45):*

    ![](images/Figure7.45.jpg)

    **Figure 7.45:** The ***Schedule*** tab allows the ***arsdb***, ***System Table Maintenance*** program to be run at a regular time

12.  The **`OK`** command button on the **`System Table Maintenance (ARCHIVE)`** properties window is selected to display the **OnDemand Configurator** program **`Current Status`**, as highlighted in *[Figure 7.46](#c07.xhtml_fig7_46)*:

    ![](images/Figure7.46.jpg)

    **Figure 7.46:** The ***System Table Maintenance*** (***ARCHIVE***) Scheduled Task Window displays the***Current Status***

13.  The **`OnDemand Configurator`** program **`Services`** node can be selected to view the **IBM CMOD** Service program status window, as illustrated in *[Figure 7.47](#c07.xhtml_fig7_47)*:

    ![](images/Figure7.47.jpg)

    **Figure 7.47:** The ***OnDemand Configurator*** program ***Services*** node showing the ***IBM CMOD*** Service program status

14.  The **`ARCHIVE`** instance node of the **OnDemand Configurator** program can be right-clicked to display the properties window, with the **`Instance`** tab as shown in *[Figure 7.48](#c07.xhtml_fig7_48)*, and click on the **`Parameters`** command button:

    ![](images/Figure7.48.jpg)

    **Figure 7.48:** The ***ARCHIVE*** instance properties window, then click on the ***Parameters*** command button

15.  This opens a window which allows the **CMOD** configuration parameters for the **ARCHIVE** instance to be added or modified, by scrolling down the list of parameters, as illustrated in *[Figure 7.49](#c07.xhtml_fig7_49):*

    ![](images/Figure7.49.jpg)

    **Figure 7.49:** The ***CMOD*** configuration parameters for the ***ARCHIVE*** instance can be added or modified

16.  We can scroll down the list of parameters for the **`ARCHIVE`** instance, as shown in *[Figure 7.50](#c07.xhtml_fig7_50)*:

    ![](images/Figure7.50.jpg)

    **Figure 7.50:** We can scroll down the list of parameters for the ***ARCHIVE*** instance

17.  The **LDAP** Server, **ECMUKDEMO77**, the **CMOD ARCHIVE** Listener port (**`32775`**), and the number of active **Db2** server program copies are highlighted in *[Figure 7.51](#c07.xhtml_fig7_51)***:**

    ![](images/Figure7.51.jpg)

    **Figure 7.51:** The ***LDAP*** Server, ***ECMUKDEMO77***, Listener port and ***Db2*** server program copies are highlighted

18.  We scroll down the **CMOD ARCHIVE** instance properties list to modify the flag **`ARS_SUPPORT_CFSOD`** and set it to **`1`** for the **IBM FileNet P8 Content Engine,** **Fixed Content Device**, which we want to configure, as highlighted in *[Figure 7.52](#c07.xhtml_fig7_52)*:

    ![](images/Figure7.52.jpg)

    **Figure 7.52:** We scroll down the ***CMOD ARCHIVE*** instance properties list to modify the flag ***ARS_SUPPORT_CFSOD*** and set it to ***1***

19.  Next, we select the **“`LDAP server to connect to”`** from the **ARCHIVE** instance **`Server`** tab using the **Parameter** drop-down and enter **`ECMUKDEMO77`**. The **`Communications…`** command button is then clicked, as illustrated in *[Figure 7.53](#c07.xhtml_fig7_53)*:

    ![](images/Figure7.53.jpg)

    **Figure 7.53:** We select the ***“LDAP*** server to connect to” from the ***Parameter*** drop-down and enter ***ECMUKDEMO77***

20.  The **`Server Communications`** tab for the **ARCHIVE** instance of **CMOD** is updated to tick the **`Enable`** box for the **IBM FileNet Listener Port Number** (set as **`32775`**). The **Non-SSL Port Number** is also set to **`1445`**, as highlighted in *[Figure 7.54](#c07.xhtml_fig7_54)*:

    ![](images/Figure7.54.jpg)

    **Figure 7.54:** The ***Server Communications*** tab for the ***ARCHIVE*** instance of ***CMOD*** is updated

21.  The **`arsdb1.log`** file can be seen in the **`c:\arstmp`** folder, as highlighted in *[Figure 7.55](#c07.xhtml_fig7_55)*:

    ![](images/Figure7.55.jpg)

    **Figure 7.55:** The ***arsdb1.log*** file can be seen in the ***c:\arstmp*** folder

22.  The **OnDemand** client program can be used to search for and display Log file content, as exemplified in *[Figure 7.56](#c07.xhtml_fig7_56):*

    ![](images/Figure7.56.jpg)

    **Figure 7.56:** The ***OnDemand*** client program can be used to search for and display Log file content

23.  The **Search Criteria** fields from the Log file record entries can be used to select a sub-set of the Log records to be displayed, as shown in *[Figure 7.57](#c07.xhtml_fig7_57):*

    ![](images/Figure7.57.jpg)

    **Figure 7.57:** The ***Search Criteria*** fields from the Log file record can be used to select a sub-set of the Log records

24.  The **`admin`** user on the Windows server is updated as an **`Administrator`** following the Windows **`User Accounts`** **>** **`Manage Accounts`** **>** **`Change and Account`** **>** **`Change Account Type`** command, as shown in *[Figure 7.58](#c07.xhtml_fig7_58)*:

    ![](images/Figure7.58.jpg)

    **Figure 7.58:** The ***admin*** user on the Windows server is updated as an ***Administrator***

The arsxml Command Use on Windows

The **`arsxml`** program is a very useful utility installed for use with **IBM CMOD** on the **Linux** and **Windows** systems. There is a link, as follows, which has further links to each of its areas of command:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=multiplatforms-arsxml](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=multiplatforms-arsxml)

On **Windows,** the **`ARSXML`** program is accessed by launching the **`OnDemand Command Window V10.5`**, as highlighted in *[Figure 7.59](#c07.xhtml_fig7_59)*:

![](images/Figure7.59.jpg)

**Figure 7.59:** The ***Windows*** ***ARSXML*** program is accessed by launching the ***OnDemand Command Window V10.5***

The **`ARSXML`** program can be used to **export** a **Group Name** held in an attribute input **xml** file (**`exportBaxterBayCredit.xml`** in this example).

The example **`ARSXML`** commands are shown in *[Figure 7.60](#c07.xhtml_fig7_60)*. The following **export** command is used to export the **IBM CMOD** **Application Group** and related data for **Baxter Bay Credit** to an **xml** file, which can then be used for importing to another system:

`ARSXML export -h "localhost" -u ADMIN -p filenet123 -i "C:\cmod\BaxterBay\exportBaxterBayCredit.xml"`

There is also an example **add** command:

`ARSXML add -h "localhost" -u ADMIN -p filenet123 -i "C:\cmod\BaxterBay\addgroups.xml"`

![](images/Figure7.60.jpg)

**Figure 7.60:** The example ***ARSXML*** ***export*** and ***add*** commands

The log file in the **OnDemand System Log** search using the current date shows the recent **`Group Add`** activity, as highlighted in *[Figure 7.61](#c07.xhtml_fig7_61)*:

![](images/Figure7.61.jpg)

**Figure 7.61:** The log file in the ***OnDemand System Log*** search using the current date shows the ***Group Add*** activity

The Log file also lists commands with a **`Severity`** status of **`Error`**, which could be filtered for searching by setting the **`Severity`** field in the **`Search Criteria`** field list to **`Error`**, as illustrated in *[Figure 7.62](#c07.xhtml_fig7_62)*:

![](images/Figure7.62.jpg)

**Figure 7.62:** The log file also lists commands with a ***Severity*** status of ***Error***, which could be filtered for searching

The **OnDemand** window toolbar can be customized to add frequently used menu items, as shown in *[Figure 7.63](#c07.xhtml_fig7_63)*:

![](images/Figure7.63.jpg)

**Figure 7.63:** The ***OnDemand*** window toolbar can be customized to add frequently used menu items

The **`Load`** tab, shown in the **ARCHIVE** instance properties window, is used to add watch folders for the **data loading** and **MVS** download service programs, as illustrated in *[Figure 7.64](#c07.xhtml_fig7_64)*:

![](images/Figure7.64.jpg)

**Figure 7.64:** The ***Load*** tab is used to add watch folders for the ***data loading*** and ***MVS*** download services

# [Configuring the System After Installing CMOD Fix Pack 10.5.0.7](#toc.xhtml_s97a)

After the installation of the **IBM CMOD** **Fix Pack**, version **10.5.0.7,** we have to follow a configuration procedure described in this section. A regularly updated **README.txt** file is also available, which describes the upgrade requirements using the web link URL:

[https://cmod.wiki/dox/CMOD-v10.5-README.txt](https://cmod.wiki/dox/CMOD-v10.5-README.txt)

1.  It can be seen from the Windows Explorer system program launch pop-up window that there are two new versions of the IBM OnDemand client programs now available, **OnDemand Administrator V10.5 (64-bit)** and **OnDemand Monitor V10.5 (64-bit)**, as shown in *[Figure 7.65](#c07.xhtml_fig7_65):*

    ![](images/Figure7.65.jpg)

    **Figure 7.65:** Two new versions of the IBM OnDemand client programs now available, ***OnDemand Administrator V10.5 (64-bit)*** and ***OnDemand Monitor V10.5 (64-bit)***

2.  We can load the new **OnDemand Administrator V10.5 (64-bit)** program to select from the list of **IBM Content Manager OnDemand** servers, and use the right-click to **`Logon`**, as illustrated in *[Figure 7.66](#c07.xhtml_fig7_66)*:

    ![](images/Figure7.66.jpg)

    **Figure 7.66:** Select from the ***IBM Content Manager OnDemand*** servers list, and use the right-click to ***Logon***

3.  The user is prompted to Logon to the server, which we show with the **`ADMIN`** user account, as shown in *[Figure 7.67](#c07.xhtml_fig7_67)*:

    ![](images/Figure7.67.jpg)

    **Figure 7.67:** The user is prompted to Logon to the server

4.  We now see the **`OnDemand Administrator`** program nodes for accessing the system attributes, in the **Tree** navigation panel. We can select the **`Folder`** node and create a **`New Folder`** by using the pop-up menu that appears after right-clicking, as shown in *[Figure 7.68](#c07.xhtml_fig7_68):*

    ![](images/Figure7.68.jpg)

    **Figure 7.68:** We can select the ***Folder*** node and create a ***New Folder*** by right-clicking

5.  On the **New Folder** window **`General`** tab, we can enter a new **`Invoices`** folder, as shown in *[Figure 7.69](#c07.xhtml_fig7_69)*:

    ![](images/Figure7.69.jpg)

    **Figure 7.69:** On the ***New Folder*** window ***General*** tab, we can enter a new ***Invoices*** folder

6.  Next, we can add the security groups and users to allow or restrict access to our new **`Invoices`** folder by selecting the **New Folder** window, **`Permissions`** tab, and adding groups, as illustrated in *[Figure 7.70](#c07.xhtml_fig7_70)*:

    ![](images/Figure7.70.jpg)

    **Figure 7.70:** We add security groups and users to allow or restrict access to our new ***Invoices*** folder

7.  The **`Folder Fields`** can be defined for our new **Invoices** folder by selecting the **`Field Definition`** tab. We enter a **`Year`** field and then select the **`Advanced`** command, as illustrated in *[Figure 7.71](#c07.xhtml_fig7_71)*:

    ![](images/Figure7.71.jpg)

    **Figure 7.71:** We add a new ***Year*** Folder Field to our ***Invoices*** Folder

8.  The **`Advanced Folder Field information`** pop-up window allows additional properties to be added to further define our **`Year`** **Folder Field** for our **`Invoices`** folder, and the **`OK`** command button is selected to confirm the details added, as illustrated in *[Figure 7.72](#c07.xhtml_fig7_72)*:

    ![](images/Figure7.72.jpg)

    **Figure 7.72:** We further define our ***Year*** ***Folder Field*** for our ***Invoices*** folder, and the ***OK*** button is selected

9.  Next, we can select the **`Field Information`** Tab for the **Invoices** folder, **`Year`** field. This allows additional **`Year`** field and search attributes to be added, as illustrated in *[Figure 7.73](#c07.xhtml_fig7_73):*

    ![](images/Figure7.73.jpg)

    **Figure 7.73:** Select the ***Field Information*** Tab for the ***Invoices*** folder, ***Year*** field, to add field and search attributes

10.  If you select a value for the **Defaults** field for the **Year** field (such as we entered, **2024**), then the associated **`Default`** tick box **must** also be set; otherwise, you get the following pop-up error message, as shown in *[Figure 7.74](#c07.xhtml_fig7_74)*:

    ![](images/Figure7.74.jpg)

    **Figure 7.74:** If the ***Defaults*** field has a value, for example, 2024, for the ***Year*** field, then the ***Default*** tick box ***must*** also be set

11.  Finally, if required, the **`Field Mapping`** tab can be selected. This allows an **Invoices** Folder Field to be mapped to an **`Application Group Database Name`** field, as shown in *[Figure 7.75](#c07.xhtml_fig7_75)*:

    ![](images/Figure7.75.jpg)

    **Figure 7.75:** The ***Field Mapping*** tab allows a Folder Field to be mapped to an Application Group Database Field

    The **Folder** **Field** mapping option is described in detail in the **IBM** Knowledge base link, as follows:

    [https://www.ibm.com/docs/en/cmofz/10.5.0?topic=reference-folder-field-mapping](https://www.ibm.com/docs/en/cmofz/10.5.0?topic=reference-folder-field-mapping)

    If the **Field Mapping type** (see the **Field Definition** tab details in *[Figure 7.71](#c07.xhtml_fig7_71)*) is set to **application group**, **annotation text search**, or **annotation color search**, then the field cannot be mapped.

12.  On selecting the **`OK`** command button, we can see our new **Invoices** folder listed in the detail pane **(`Contents of 'Folders'`)** for the **`Folders`** node, as shown in *[Figure 7.76](#c07.xhtml_fig7_76):*

    ![](images/Figure7.76.jpg)

    **Figure 7.76:** Selecting the ***OK*** command button displays our new ***Invoices*** folder

13.  The **`OnDemand Administrator`** program allows us to create a new **`Application Group`** by selecting the **`Application Groups`** node and right-clicking to select the **`New Application Group`** menu item, as highlighted in *[Figure 7.77](#c07.xhtml_fig7_77)*:

    ![](images/Figure7.77.jpg)

    **Figure 7.77:** Create a new ***Application Group*** by selecting the ***Application Groups*** node and right-clicking to select the ***New Application Group*** menu item

14.  The **`Baxter Bay Credit`** Application Group Name is entered, with a Description field of the **`Baxter Bay Credit Demo Application Group`**, and then the **`Advanced…`** command button is selected to add the **`Database Information`** required. One option for this panel (which is defaulted to **`No`**) is the option to **`“Interoperate with FileNet P8 Platform”`** with a radio button choice of **`Yes`** to allow the **`“Use Content Federation Services (CFS-CMOD)”,`** as illustrated in *[Figure 7.78](#c07.xhtml_fig7_78):*

    ![](images/Figure7.78.jpg)

    **Figure 7.78:** The ***Baxter Bay Credit*** Name is entered, and then the ***Advanced…*** command is selected

15.  After selecting the **`OK`** command button on the **Database Information** pop-up window panel, we can select the **`Field Definition`** tab and enter the list of field names to be associated with the **`Baxter Bay Credit Application Group`,** using the **`Add`** command button, as highlighted in *[Figure 7.79](#c07.xhtml_fig7_79)*:

    ![](images/Figure7.79.jpg)

    **Figure 7.79:** On the ***Field Definition*** tab, enter the list of field names for the ***Baxter Bay Credit Application Group***

16.  After entering the list of Field names, we select the **`Field Information`** tab and identify the Field types and validation characteristics, as illustrated in *[Figure 7.80](#c07.xhtml_fig7_80)*:

    On this tab, we also have the opportunity of adding any Database Field mapping information we need.

    The maximum String Field length that is allowed is 254 characters; the string type can be set as Fixed or Variable using a drop-down option. Fixed should be used when you have a known length (such as a banking sort-code field).

    The full details for the **IBM Content Manager OnDemand** Field Information entry attributes can be seen using the link as follows:

    [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=reference-application-group-field-information-options](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=reference-application-group-field-information-options)

    ![](images/Figure7.80.jpg)

    **Figure 7.80:** We select the ***Field Information*** tab and identify the Field types and validation characteristics

    After selecting the **`name`** field from the drop-down list of field names, shown in *[Figure 7.80](#c07.xhtml_fig7_80)*, we can select the field **`Type`** as **`Filter`**, which allows the field to be searched, and then select the **`String Type`** as **`Variable`** and set the maximum length allowed for a **String** as **`254`** bytes, as highlighted in *[Figure 7.81](#c07.xhtml_fig7_81)*:

    ![](images/Figure7.81.jpg)

    **Figure 7.81:** Select the ***String Type*** as ***Variable*** and set the maximum length allowed for a ***String*** as ***254*** bytes

17.  Next, we select the **`account`** field from the drop-down list, and this allows us to set the required attributes for this field, which we set as a **`Fixed`** length, **`Upper`** case **`String`** field of **`11`** bytes, as indicated in *[Figure 7.82](#c07.xhtml_fig7_82)*:

    ![](images/Figure7.82.jpg)

    **Figure 7.82:** We select the ***account*** field with attributes set as a ***Fixed*** length ***Upper*** case ***String*** field of ***11*** bytes

18.  Next, we select the **`crd_date`** field (Credit Date) from the drop-down list, and this allows us to set the required attributes for this field, which we set as a **`Data Type`** of **`Date`,** and set the **`Segmen`t** tick-box option, as indicated in *[Figure 7.83](#c07.xhtml_fig7_83)*:

    IBM recommends that a **`Date`** field defined as a **`Segment`** should always be set as a **`Filter`** type (as we have shown).

    A **`Segment`** field is a **`Date`** or Date/Time field that limits the number of tables that are searched during a folder query. A **`Segment`** date limits folder queries to a single table or a limited set of tables to improve performance. Only one segment field can be set per Application Group.

    ![](images/Figure7.83.jpg)

    **Figure 7.83:** The ***crd_date*** field is selected, and we set it as a ***Data Type*** of ***Date*** and tick the ***Segment*** tick-box

19.  Next, we select the **`balance`** field from the drop-down list, and this allows us to set the required attributes for this field, which we set as a **`Data Type`** of **`DecFloat (16)`**, as shown in *[Figure 7.84](#c07.xhtml_fig7_84)*:

    ![](images/Figure7.84.jpg)

    **Figure 7.84:** We select the ***balance*** field and set it as a ***Data Type*** of ***DecFloat (16)***

20.  Then, we select the **`Advanced Index Information`** tab, as highlighted in *[Figure 7.84](#c07.xhtml_fig7_84)***,** and select the fields **`name`** and **`account`** as an **`Ascending`** **sorted Index** for the database table, as shown in *[Figure 7.85](#c07.xhtml_fig7_85)*:

    ![](images/Figure7.85.jpg)

    **Figure 7.85:** Select the fields ***name*** and ***account*** as an ***Ascending sorted Index*** for the database table

21.  The next tab, **`Permissions`,** allows a selection of **Users** and/or **Groups** to be added to define the **Baxter Bay Credit** **Application Group** security options, as shown in *[Figure 7.86](#c07.xhtml_fig7_86):*

    ![](images/Figure7.86.jpg)

    **Figure 7.86:** The ***Permissions*** tab allows a selection of ***Users*** / ***Groups*** to define the ***Baxter Bay Credit*** security

22.  To use the **`account`** field as part of an **Index**, we have to go back to the **`Field Information`** tab and tick the **`Unique ID`** box to avoid a validation error, as highlighted in *[Figure 7.87](#c07.xhtml_fig7_87)***:**

    ![](images/Figure7.87.jpg)

    **Figure 7.87:** For the ***account*** field to be set as part of an ***Index***, tick the ***Unique ID*** box on the ***Field Information*** tab

23.  To complete the configuration of the **Baxter Bay Credit,** **Application Group,** we select the **`Storage Management`** tab in order to assign a **`Storage Set Name`** to identify the storage area that will be used for documents identified to be loaded from **Baxter Bay Credit** applications, as illustrated in *[Figure 7.88](#c07.xhtml_fig7_88)*:

    The drop-down list of **Storage Set Names** only has our pre-configured **`Cache Only— Library Server`** entry (but multiple **Storage Sets** can be added later to the **IBM CMOD** server)**.**

    The link describing this tab is found at: [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=reference-application-group-storage-management](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=reference-application-group-storage-management)

    ![](images/Figure7.88.jpg)

    **Figure 7.88:** Select the ***Storage Set Name*** list***,*** to use the ***Cache Only – Library Server*** for storing documents

24.  After clicking the **`OK`** command button shown on the screenshot labeled *[Figure 7.88](#c07.xhtml_fig7_88)*, we can see that **`Baxter Bay Credit`** has been added to the **`Name`** column of the display panel for the **`Application Groups`** node of the **OnDemand Administrator** program, as highlighted in *[Figure 7.89](#c07.xhtml_fig7_89)*:

    ![](images/Figure7.89.jpg)

    **Figure 7.89:** ***Baxter Bay Credit*** has been added to the ***Name*** column of the display for the ***Application Groups*** node

25.  We can now click on the **Applications** node, right-click, and use the **`Add an Application`** menu item to show the **`Add an Application`** configuration window, as shown in *[Figure 7.90](#c07.xhtml_fig7_90)*:

    ![](images/Figure7.90.jpg)

    **Figure 7.90:** We click on the ***Applications*** node, right-click and use the ***Add an Application*** menu item

26.  We give the **Application** the **`Name`** as **`BaxterBayCredit`** (with the **`Descriptio`n** as **`Baxter Bay Credit`**), then we use the **`Select…`** command button to add the **`Baxter Bay Credit`** **`Application Group`** from the list of **`Application Groups`**. We then selected the **`Logical Views`** tab, as shown in *[Figure 7.91](#c07.xhtml_fig7_91)*:

    ![](images/Figure7.91.jpg)

    **Figure 7.91:** We select the ***Logical Views*** tab

27.  The **ADMIN** user is added from the list of **Users** box using the **`ADD>>`** command button to add the **ADMIN** user to the **Users with Logical Views** box.

    On clicking the **`OK`** command button, the **`BaxterBayCredit`** **Application** can be seen in the **`Contents of 'Applications'`** Display panel for the **Applications** node of the **OnDemand Administrator** window, Navigation Tree, as highlighted in *[Figure 7.92](#c07.xhtml_fig7_92)*:

    ![](images/Figure7.92.jpg)

    **Figure 7.92:** ***BaxterBayCredit*** is displayed in the ***Contents of ‘Applications’*** panel for the ***Applications*** node

28.  In order to load documents, we need to select an **`Indexer`**, which we set as **`Generic`** for the **`BaxterBayCredit`** Application, which we can set using the **`View an Appliation`**, menu window, as illustrated in *[Figure 7.93](#c07.xhtml_fig7_93)*:

    ![](images/Figure7.93.jpg)

    **Figure 7.93:** We need to select an ***Indexer***, which we set as ***Generic*** for the ***BaxterBayCredit*** Application

    **Note:** *We discovered that we originally had an incorrectly defined field which could not be modified to a different type: See [Appendix B, Recreating an Application Group](#appb.xhtml), which covers the requirement to delete and recreate an* ***Application Group*** *in the case where a field type does not match the expected load configuration.*

29.  The **`Delete`** menu option can be selected by right-clicking the **`Application Groups`** list item where a Field is required, that needs to be updated, as shown in *[Figure 7.94](#c07.xhtml_fig7_94):*

    ![](images/Figure7.94.jpg)

    **Figure 7.94:** The ***Delete*** menu option can be selected by right-clicking the ***Application Groups*** list item

30.  The pop-up window appears in order to enter a valid **`ADMIN`** Administrator and password to allow the **Delete** function to proceed, as shown in *[Figure 7.95](#c07.xhtml_fig7_95)*:

    ![](images/Figure7.95.jpg)

    **Figure 7.95:** Enter a valid, ***ADMIN*** Administrator and password to allow the ***Delete*** function to proceed

31.  The pop-up window then appears, as shown in *[Figure 7.96](#c07.xhtml_fig7_96)*, for us to select **`OK`** to confirm that we want to delete the **`Baxter Bay Credit`** **Application Group**, as shown in *[Figure 7.96](#c07.xhtml_fig7_96)*:

    ![](images/Figure7.96.jpg)

    **Figure 7.96:** Select ***OK*** for us to confirm that we want to delete the ***Baxter Bay Credit*** ***Application Group***

32.  We still have to confirm the final choice to delete the **Baxter Bay Credit Application Group**, by clicking the **`Yes`** command button on a pop-up window, as shown in *[Figure 7.97](#c07.xhtml_fig7_97):*

    ![](images/Figure7.97.jpg)

    **Figure 7.97:** Confirm the deletion of the ***Baxter Bay Credit Application Group***, by clicking on the ***Yes***

33.  After the deletion of the **Baxter Bay Credit Application Group**, it is removed from the list, as shown in *[Figure 7.98](#c07.xhtml_fig7_98)***:**

    ![](images/Figure7.98.jpg)

    **Figure 7.98:** The ***Baxter Bay Credit Application Group*** is removed from the list

# [Conclusion](#toc.xhtml_s98a)

In this chapter, we described the use of the **ARSXML** program to export and import **CMOD** **Application Groups** and the step-by-step procedure to add a new **Folder** and **Application Group** object using the **Windows OnDemand Administrator** program.

We also covered the **Windows** **OnDemand Configurator** program **V10.5**, the **Windows OnDemand Client configuration** program, and the configuration of the system after installing **CMOD Fix Pack 10.5.0.7**.

In *[Chapter 8, **CMOD** System User Administration on **Linux**](#c08.xhtml)*, we will cover the Object Type model and the Object Owner model for decentralizing the system administration users and resetting an expired or lost **CMOD** admin user password on the **Linux Db2** server. The use of the **arsstash** program to store encrypted passwords for users will also be described.

# [Points to Remember](#toc.xhtml_s99a)

*   It is important to enter at least 9 characters for the password during initial configuration, as there is no validation of this at this point, and the encrypted password is stored in a database table. A password entered with less than nine characters will lock-out the Administrator user.
*   Some types of incorrectly defined **Application Group** fields may not be modified to a different type, so sometimes the only solution is to delete the **Application Group** and rebuild it. So, it is important to carefully design, confirm, and validate the Field types and the **Application Group** structures in a development environment before exporting and importing them to the production **CMOD** server.
*   If you select a value for the **Defaults** text box entry for a field, then the associated **Default** tick box **must** also be set, otherwise, you get a pop-up error message.
*   To use a field as part of an **Index**, we have to also use the **Field Information** tab and tick the **Unique ID** box for the field to avoid a validation error.

# [Multiple Choice Questions](#toc.xhtml_s100a)

1.  Which command line program is used to export and import **CMOD** **Application Groups**?
    1.  `arssockd`
    2.  `arsxml`
    3.  `arsdb`
    4.  `arsstash`
2.  Which default **Windows** path is used for the **`arsdb1.log`** log file?
    1.  `c:\arscache1`
    2.  `c:\arstmp`
    3.  `c:\arsdbpri`
    4.  `c:\arsdbarc`
3.  Which port is used for the IBM FileNet Listener Port Number?
    1.  1445
    2.  32775
    3.  9080
    4.  32768
4.  Which CMOD client program is used to create and maintain the Applications Group names and fields?
    1.  OnDemand Administrator V10.5 (64-bit)
    2.  OnDemand Client V10.5 (64-bit)
    3.  OnDemand Monitor V10.5 (64-bit)
    4.  OnDemand Configurator V10.5

# [Answers](#toc.xhtml_s101a)

1.  b
2.  b
3.  b
4.  d

# [Questions](#toc.xhtml_s102a)

1.  Which Windows client programs can connect to the Linux CMOD server?
2.  Why do we need the Windows client installation if we are using IBM Content Manager OnDemand on the Linux server?
3.  Which CMOD programs, covered in this chapter, are only available for installation and running on Windows?
4.  Which CMOD programs, covered in this chapter, are supported on both the Windows and Linux environments?
5.  What procedure would you use to change a String field in an Application Group to a Date field?

# [Key Terms](#toc.xhtml_s103a)

*   **LDAP:** Lightweight Directory Access Protocol is used to communicate with an authentication server security system to validate users, groups, and other named system components to allow controlled access to a system and its programs and file systems.
*   **CFS-CMOD:** The Content Federation Services–Content Manager OnDemand integration software is used for the installation of an IBM FileNet P8 Content Engine Fixed Content Device.

    See the link to the PDF for an overview: [https://public.dhe.ibm.com/software/data/cm/filenet/docs/cfsdoc/cmod/45x/Cfs_cmod_config_guide.pdf](https://public.dhe.ibm.com/software/data/cm/filenet/docs/cfsdoc/cmod/45x/Cfs_cmod_config_guide.pdf)

    (“IBM FileNet Content Federation Services for Content Manager OnDemand”)

*   **SSL**: Secure Socket Layer is a protocol for securing an internet connection by encrypting data sent between a website and a browser or allowing communications between two servers.

# [CHAPTER 8](#toc.xhtml_c08)

# [CMOD System User Administration on Linux](#toc.xhtml_c08)

# [Introduction](#toc.xhtml_s104a)

This chapter covers the **Object Type** model and **Object Owner** model for decentralizing the system administration users and resetting an expired or lost **CMOD** **ADMIN** user password on the **Linux Db2** server. The use of the **arsstash** program to store encrypted passwords for users is also described along with the **CMOD** Generic Indexer and specific file format indexing programs. We also outline the installation of the **Ricoh AFP Workbench Viewer** program, used for viewing print output archive storage of commercial documents.

# [Structure](#toc.xhtml_s105a)

In this chapter, we will discuss the following topics:

*   The **Object Type** Model and **Object Owner** Model for Decentralizing the System Administration
*   Resetting an Expired or Lost **CMOD** **ADMIN** User Password on **Db2**
*   Updating the File Permissions in the **Linux** System for the Program Binaries
*   Running the **arsstash** Program to Encrypt User Passwords
*   Administration of the **CMOD** Generic Indexer

# [The Object Type Model and Object Owner Model for Decentralizing the System Administration](#toc.xhtml_s106a)

**IBM Content Manager OnDemand** (**CMOD**) is capable of supporting a centralized or decentralized model to provide a secure system administration.

For a centralized environment, the system administrator controls the creation and security access to all objects defined on the system.

The decentralized environment allows the system administrator tasks to be divided and assigned to other users. The exact user responsibilities can be varied and configured for each administration user to provide a combination of group administration: application group administration, user administration, folder administration, or any combination of each of the administrative tasks.

**IBM** recommends that the decision to centralize or decentralize the administration of the system should be considered first before any objects are added to the system. This decision can be reversed but the amount of effort required to change from one type of administration is significant if a large number of users, groups, folders, and application groups have already been configured on the system.

Although the method of decentralizing the administration of the system can be implemented in a large number of ways, **IBM** has documented two specific models which we will describe in this section; The “**Object Type** model” and the “**Object Owner** model”.

**Note**: The security structure of this is illustrated in *[Appendix B, Recreating an Application Group](#appb.xhtml)* which covers the application of the security for the **Baxter Bay Credit** example.

# [The Object Type Administrative Model](#toc.xhtml_s107a)

Usually, each logical part requires two administrative users. The first user has the responsibility for creating and maintaining users and groups. The second user has the responsibility for creating and maintaining applications, application groups, and folders.

It is also possible to define one user for the **Object Type** model. All of the objects on the system are grouped into administrative domains depending on the type of the object.

The administrator of a domain, using the **Object Type** model, maintains all of the objects within the domain. So, an application **group/folder/cabinet** administrator maintains all of the **Application**, **Application group**, **Folder**, and **Cabinet** objects on the system.

The details for implementing the “**Object Type** model” are fully described in the link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=administration-object-type-model](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=administration-object-type-model)

# [The Object Owner Administrative Model](#toc.xhtml_s108a)

For the **Object Owner** model, all the system and **CMOD** objects are grouped into administrative domains based on the **creator/owner** of the object. An administrator can configure, update and delete only the objects that they create. So, a user with the **create Application Groups** and **create Folders** permissions can maintain only the **Applications**, **Application Groups**, and **folder** objects that they created.

The **Object Owner** model is maintained by dividing the objects on the system into separate logical parts, such as a department, a company, or another entity so that each part is independent of the other and must be maintained separately.

The authority to create and maintain users, groups, applications, application groups, and folders is divided by these logical parts. So, in this case, a single user would be the system administrator for a logical part of the system.

The details for implementing the “**Object Owner** model” are fully described in the link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=administration-object-owner-model](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=administration-object-owner-model)

See also:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=administration-system](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=administration-system)

# [Resetting an Expired or Lost CMOD ADMIN User Password on Db2](#toc.xhtml_s109a)

As was also covered for the **CMOD** Windows environment in the last chapter, if the **ADMIN** user password is forgotten or has expired and since the password is held in an encrypted form in a **Db2** database table field, **`passwd`,** then the **`passwd`** field in the **`archive.user`** table for the **`ADMIN`** user must be reset to a **null** string using a **SQL** update statement as follows:

`[archive@ECMUKDEMO22 config]$db2`

`db2 => connect to ARCHIVE`

`select userid from archive.arsuser;`

`update archive.arsuser set passwd='' where userid='ADMIN'`

`commit`

`db2 => quit`

`DB20000I  The QUIT command completed successfully.`

`[archive@ECMUKDEMO22 config]$`

The full **`db2`** **SQL** command list to set the **`ADMIN`** user password field to a null string is shown in *[Figure 8.1](#c08.xhtml_fig8_1):*

![](images/Figure8.1.jpg)

**Figure 8.1:** The full ***db2*** SQL command list to set the ***ADMIN*** user password field to a null string

See the link:

[https://www.ibm.com/support/pages/recovery-lost-password-super-id-admin-content-manager-ondemand](https://www.ibm.com/support/pages/recovery-lost-password-super-id-admin-content-manager-ondemand)

The Windows **CMOD** client Administrator program, the **CMOD OnDemand** client, is then logged onto, on a **Windows** server and the **ECMUKDEMO22** **Linux** server logged onto and the password updated as described in *[Chapter 7, CMOD Administration on Windows](#c07.xhtml),* in the section, *Updating the Windows* ***ADMIN*** *Password.*

# [Updating the File Permissions in the Linux System for the Program Binaries](#toc.xhtml_s110a)

The program files in the **Linux CMOD** **`/opt/ibm/ondemand/V10.5/bin`** folder require a change to the ownership from the **root** installation user and group, to the **archive** user and group, using the following commands, with the list of program files and the resulting security, as shown in *[Figure 8.2](#c08.xhtml_fig8_2):*

`cd /opt/ibm/ondemand/V10.5/bin`

`chown archive:db2iadm1 ars*`

`ls -lsa ars*`

![](images/Figure8.2.jpg)

**Figure 8.2:** The ownership is changed from the ***root*** installation ***user*** and ***group***, to the ***archive user*** and ***group***

# [Moving the Database Schema from Root to Archive on Linux](#toc.xhtml_s111a)

The original **CMOD** installation on the **Linux** server, using the **root** user created the **ARCHIVE** instance database Tables with a schema of **ROOT**. This caused errors when attempting to start the service programs, since the referenced **ARCHIVE.ARSAG** table could not be found in the database by the programs. The solution for this was to recreate all the Tables with a Schema of **ARCHIVE** by exporting the complete **DDL** list of tables.

This section is covered in greater detail in *[Chapter 3, Installing Optional CMOD Software on Linux](#c03.xhtml).*

First, we start the **Db2** database for the **ARCHIVE** instance, as follows:

`[archive@ECMUKDEMO22 config]$ ../bin/arsdb -gkv`

`ARS4015I Starting the DB2 ARCHIVE database instance`

`ARS4078I The ARCHIVE instance has already been started`

`ARS4017I Activating the DB2 ARCHIVE database`

`[archive@ECMUKDEMO22 config]$`

Please refer to:

[https://www.ibm.com/support/pages/simple-way-change-schema-names-db2-linux-unix-and-windows](https://www.ibm.com/support/pages/simple-way-change-schema-names-db2-linux-unix-and-windows)

The **`db2look`** command is used to create the **DDL** for the tables and export this to the **`outputfile.sql`**, to allow the **vi** editor to be used to edit the table schema to be updated from the **ROOT** user to the **ARCHIVE** user, as shown in *[Figure 8.3](#c08.xhtml_fig8_3):*

`db2look -d ARCHIVE -e -o outputfile.sql`

![](images/Figure8.3.jpg)

**Figure 8.3:** The command is used to create the ***DDL*** for the tables and export this to the ***outputfile.sql***

The **`ROOT`** schema can then be dropped from the **`ARCHIVE`** instance **Db2** database, by running the commands, as shown in *[Figure 8.4](#c08.xhtml_fig8_4):*

`db2`

`db2 => connect to ARCHIVE`

`db2 => CALL SYSPROC.ADMIN_DROP_SCHEMA('ROOT', NULL, 'ERRORSCHEMA', 'ERRORTABLE')`

`db2 => quit`

![](images/Figure8.4.jpg)

**Figure 8.4:** The ***ROOT*** schema can then be dropped from the ***ARCHIVE*** instance ***Db2*** database

The database update can then be followed from steps 2 through 16 of *[Chapter 3, Installing Optional CMOD Software on Linux](#c03.xhtml)*, in the section “*Moving the Database schema from root to archive on Linux”.*

We can now start the **ARCHIVE** instance using the **`arssockd`** program to run the **Library** server, as shown in *[Figure 8.5](#c08.xhtml_fig8_5):*

(The Linux **`ps`** command line given here is used to confirm that the **`arssockd`** program is running).

`cd /opt/ibm/ondemand/V10.5/config`

`../bin/arssockd -I archive -S`

`ps -eaf|grep ars`

![](images/Figure8.5.jpg)

**Figure 8.5:** We can now start the ***ARCHIVE*** instance using the ***arssockd*** program to run the ***Library*** server

The full path use of the command is:

`/opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S`

This is shown in *[Figure 8.6](#c08.xhtml_fig8_6):*

![](images/Figure8.6.jpg)

**Figure 8.6:** The full path use of the command is : ***`/opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S`***

The **CMOD** Object server can be verified as active using the following command, as shown in *[Figure 8.7](#c08.xhtml_fig8_7):*

`ps -eaf|grep arsobjd`

![](images/Figure8.7.jpg)

**Figure 8.7:** The ***CMOD*** Object server can be verified as active using the ***ps -eaf|grep arsobjd***

# [Running the arsstash Program to Encrypt User Passwords](#toc.xhtml_s112a)

The **`arsstash`** program stores an encrypted copy of the main **CMOD** system user passwords in an **`ars.stash`** file usually stored in the **`/opt/ibm/ondemand/V10.5/config`** **`Linux`** folder path.

The **`-a`*`n`*** **Action** switch on the program command line defines if the action of the program is to store a password or delete the userid and password from the **`ars.stash`** file, using ***n*** (the **`<action>`** number) as listed in the command help list, obtained using the **`arsstash`** program command as follows:

`[archive@ECMUKDEMO22 bin]$ ./arsstash`

`ARS1600I Usage: arsstash [-a <action>] [-c] -s <stash_file> -u <userid>`

`Version:  10.5.0.7`

`-a <action> Action to perform`

`1  - Store the OnDemand userid and password (default)`

`2  - Delete the OnDemand userid and password`

`3  - Store the OnDemand userid and password for ARSLOAD`

`4  - Store the OnDemand userid and password for ODF`

`6  - Store the OnDemand userid and password for PDD`

`7  - Store the LDAP userid and password`

`8  - Store the DB2 userid and password`

`9  - Store the Oracle userid and password`

`10 - Store the ZooKeeper userid and password`

`11 - Store the PKCS11 userid and password`

`12 - Store the SQL Server userid and password`

`If no userid (-u) is given for actions 3 thru 12, then`

`the currently assigned userid for the corresponding`

`OnDemand command or database will be displayed`

`-c Create stash file`

`-s <stash_file> Stash file name`

`-u <userid> Userid`

`-1 <trace_file>  Trace file`

`-2 <trace_level> Trace level`

`[archive@ECMUKDEMO22 bin]$`

As an example, the **`ADMIN`** user password can be stored in the **`ars.stash`** file, as shown here:

`[archive@ECMUKDEMO22 bin]$` **`./arsstash -a1 -s ../config/ars.stash -u ADMIN`**

`OnDemand Password:`**`filenet123`**

`Verify OnDemand Password:`**`filenet123`**

**`[archive@ECMUKDEMO22 bin]$`**

**Note:** *The* ***`ADMIN`*** *user’s password must be at least 8 characters long.*

# [Administration of the CMOD Generic Indexer](#toc.xhtml_s113a)

The **IBM Content Manager OnDemand** Generic Indexer is used to define index data for any type of input file that is required to be stored in the **CMOD** system, but there are indexer programs designed for indexing specific file formats. These programs are listed as follows:

*   The **`arsload`** program can be used to process a PDF input file. When the Applications node **`Indexer Information`** tab defines **`PDF`** as the indexer, as shown in *[Figure 8.8](#c08.xhtml_fig8_8),* **`arsload`** will call the **PDF indexer** to process the input file.

    ![](images/Figure8.8.jpg)

    **Figure 8.8:** The Applications node ***Indexer Information*** tab defines ***PDF*** as the indexer

    The **PDF indexer** then loads the **PDF** input file and applies indexing parameters to determine the location and attributes of the index data. It then extracts index data from the **PDF** file and generates an index file and an output file which contains groups of indexed pages.

*   **IBM** **CMOD** also has an **XML** indexer to allow the indexing and archive of XML documents, this is also launched from the **`arsload`** program.
*   The **`arsacif`** program, the **AFP** Conversion and Indexing Facility (**ACIF**) for **AFP**, the Advanced Function Printing for data and line data. (see [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=indexer-acif-overview](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=indexer-acif-overview))

    The **AFP** printer driver is available for use with **Windows** systems from Ricoh:

    [https://www.ibm.com/support/pages/afp-printer-driver-windows](https://www.ibm.com/support/pages/afp-printer-driver-windows)

    The following link will directly download the AFP driver from Ricoh if you have an entitlement ID:

    [https://dl.ricohsoftware.com/eid/download/MzkwMA%3D%3D/aa9a248e-101c-4aa6-b109-1cf7403f3b4f](https://dl.ricohsoftware.com/eid/download/MzkwMA%3D%3D/aa9a248e-101c-4aa6-b109-1cf7403f3b4f)

    The **AFP** installation program works correctly on a **Windows 10 Home** edition or **Windows 11 Pro** operating system, but the **Windows** **defender** program may block the **Ricoh** viewer and printer program installation as it cannot detect the program publisher details for the installer .exe program. You need to override the **Windows defender** program to install the drivers, and so on (at your own risk!). The **AVG** virus checker found no issues with the two **Ricoh** programs which were installed.

    The installed **AFP Ricoh viewer** program is shown at the end of this chapter.

    For a detailed overview of **AFP**, see the link: [https://en.wikipedia.org/wiki/Advanced_Function_Presentation](https://en.wikipedia.org/wiki/Advanced_Function_Presentation)

    The Ricoh AFP Workbench Viewer program, with the example help screen as shown in our installed copy, refer to *[Figure 8.9](#c08.xhtml_fig8_9):*

    ![](images/Figure8.9.jpg)

    **Figure 8.9:** The ***Ricoh AFP Workbench Viewer*** Help-> About screen for ***Version 03.09.00.00***

The installed **Ricoh AFP Workbench Viewer** program displays the example **`medform.afp`** file which is one of the example files installed with the program, as shown in *[Figure 8.10](#c08.xhtml_fig8_10):*

![](images/Figure8.10.jpg)

**Figure 8.10:** The example ***medform.afp*** file which is one of the example files installed with the program

The **`arsxml`** and **`arsload`** programs have the following switches which can be viewed using the **`--h`** help option:

`[archive@ECMUKDEMO22 bin]$ ./arsxml --h`

`ARS7700I Usage: arsxml add|update|delete|export|validate [options]`

`Version:  10.5.0.7`

`[archive@ECMUKDEMO22 bin]$ ./arsload --h`

`ARS4300I Usage: arsload [options] [load_file]`

The **`-h`** help list for the **`arsload`** program provides the following information for running the **IBM** **CMOD** load program on the **Linux** system for the installed **Version: 10.5.0.7.**

A more detailed description is available at the link**:** **[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=arsload-parameters](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=arsload-parameters)**

The list of switches and their meaning are as follows:

1.  **`-a`** **`<appl>`** The **Application** represented by **`<appl>`** within the **Application Group**

    For example, **`-a Baxter Bay Credit`**

    (This switch defaults to a dependency on the filename conventions.)

2.  **`-A <field>`** The **MVS** (Multiple Virtual Storage) filename component to use for the **IBM OnDemand** application
3.  **`-b <index_number,field>`** The Index number (1-8),index field name to be entered.

    (Where the index number identifies the part of the input file name that the **`arsload`** programs assigns to that index field.)

4.  **`-B <filename_format>`** This format of the input filename for parsing (for example, **PDF** or **AFP**)

    The values of the shorthand sub-components of **`<filename_format>`**, each divided by a full-stop "**`.`**" character can be as described as follows:

    **`WRI`**       short for WRITER

    **`MVS`**       short for Multiple Virtual Storage

    **`JOB`**       short for JOBNAME

    **`DAT`**       short for DATASET

    **`FOR`**       short for FORMS

    **`YY`**        short for YYDDD

    **`HH`**        short for HHMMM

    **`AG`**        short for Application Group

    **`APP`**       short for Application

    **`FLD`**       short for Field placeholder for indexing

    **`1-8`**       Index number (1-8) - Prepend to parts of the

                           filename above being used as indexes

                           (Requires one -b parameter per index number used)

    **`IGN`**       Ignore this part of the filename (cannot be indexed)

    **`.EXT`**      Extension

    The following examples show the result of using these shorthand values for files in the default format:

    For the file defined as follows: **`MVS.JOBNAME.DATASET.FORMS.YYDDD.HHMMM.ARD`** the format could be written as: **`MVS.JOB.DAT.FOR.YY.HH.EXT`**

    The format could also be written as **`MVS.1JOB.DAT.FOR.YY.HH.EXT`** to associate the **JOB** part of the filename as a load **index 1**

    The next example is for files that are not in the default format: **`APPLICATION_GROUP.APPLICATION.MISC.DATE.ARD`**

    The format could be written as

    **`AG.APP.IGN.FLD.EXT`** and **`AG.APP.IGN.1FLD.EXT`** could be used to extract the date information of the filename into a specific index field

5.  **`-c <idx_dir>`** This is the directory for the indexer which defaults to the current directory
6.  **`-C <class>`** (OD/zOS) jes class to monitor
7.  **`-d <dl_dir>`** The download directory, this can be specified more than once
8.  **`-e`** Ignore an empty file as being a failure
9.  **`-E`** Execute the **arsuupdt** user exit program
10.  **`-f`** If load fails, unload the data
11.  **`-F <form>`** (OD/zOS) jes form to monitor
12.  -**`g <appl_grp>`** The **Application Group**, which defaults to filename conventions
13.  **`-G <field>`** The MVS filename component to use for an **OnDemand** **Application Group** For example, for (OD/zOS) we have **`WRITER.MVS.JOBNAME.DATASET.FORMS`** or **`MVS.JOBNAME.DATASET.FORMS`** (Otherwise) **`MVS.JOBNAME.DATASET.FORMS`**

    This switch defaults to **`FORMS`**

14.  **`-h <od_inst>`** The **IBM OnDemand** library server or instance name (same as **`-I`**)
15.  **`-i`** Run the Indexer Only
16.  **`-I <od_inst>`** OnDemand library server or instance name (same as **`-h`**)
17.  **`-J <file_name_delimiter>`** Delimiter character for filename parsing (Default:)
18.  **`-j <parm_file>`** Additional indexing parameters which can be read from a file
19.  **`-l <field>`** Triggers indexing of the entire load filename using the field identifier
20.  **`-n`** Do not remove the loaded files
21.  **`-p <passwd>`** The name of a password stash file
22.  **`-s <input>`** (OD/zOS) JCL ddname to use as input (that is, INPUT)
23.  **`-t <seconds>`** Time interval to sleep, which defaults to 600 seconds
24.  **`-u <userid>`** The IBM CMOD userid, for example **ADMIN**
25.  **`-v`** Verbose The full log output is displayed in the command window
26.  **`-W <writer>`** (OD/zOS) jes writer to monitor
27.  **`-X <indexer>`** The Indexer code letter to be used (this overrides the indexer defined in the application). The Indexer code names are as follows:

    **`A`**: Content Manager OnDemand ACIF Indexer

    **`G`**: Content Manager OnDemand Generic Indexer File Format

    **`P`**: Content Manager OnDemand PDF Indexer

    **`X`**: Content Manager OnDemand XML Indexer

    **`3`**: 390 Indexer

    **`4`**: 400 Indexer

28.  **`-Z <user_def>`** User defined string passed to the load program user exit
29.  **`-1 <trace_file>`** The trace file for writing debug output to for error diagnosis
30.  **`-2 <trace_level>`** The trace level for writing debug output to for error diagnosis

The **Generic** indexer is not an indexing program but refers to a parameter file format.

It is described in detail in the IBM document, *[Chapter 6, Generic Indexer](#c06.xhtml)* of the **`IndexingReference.pdf`** file, which is in the second URL link.

For the **IBM Knowledge Base** URL Link for the IBM **CMOD** Generic Indexer, see

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=ondemand-generic-indexer](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=ondemand-generic-indexer)

There is also a downloadable **Indexing Administration** **pdf** guide available at:

[https://cmod.wiki/dox/CMODv10.5/IndexingReference.pdf](https://cmod.wiki/dox/CMODv10.5/IndexingReference.pdf)

# [Conclusion](#toc.xhtml_s114a)

In this chapter, we described the **Object Type** model and the **Object Owner** model for decentralizing the system administration users and the resetting of an expired or lost **CMOD ADMIN** user password on the **Linux** **Db2** server. The use of the **arsstash** program to store encrypted passwords for users is also described along with the **CMOD** **Generic Indexer** and more specific file format indexing programs.

In *[Chapter 9, **CMOD** Java **API** Examples](#c09.xhtml)*, we will list several examples of Java programs, which have been updated to work with the latest version **10.5.0.7** of the **IBM CMOD OnDemand API**. We will also demonstrate running them in an **Eclipse IDE** environment on a **Linux** server.

# [Points to Remember](#toc.xhtml_s115a)

*   The **ADMIN** user’s password must be at least 8 characters long.
*   **IBM** recommends that the decision to centralize or decentralize the administration of the system should be the first decision, before any objects are added to the system.
*   **IBM** has documented two specific models: the “**Object Type** model” and the “**Object Owner** model”.
*   The **AFP** installation program works correctly on a **Windows 10 Home edition** system, but **Windows defender** will block the **Ricoh viewer** and **printer** program installation as it cannot detect the program publisher details for the installer .exe program. You have to override the defender to install the drivers, and so on (at your own risk!).

# [Multiple Choice Questions](#toc.xhtml_s116a)

1.  Which program is used to store encrypted passwords for users in a Linux file?
    1.  `arsdb`
    2.  `arsstash`
    3.  `arssockd`
    4.  `arsload`
2.  Which switch is used by the program to store user passwords for the **`arsload`** program?
    1.  -a1
    2.  -a2
    3.  -a3
    4.  -a4

# [Answers](#toc.xhtml_s117a)

1.  b
2.  c

# [Questions](#toc.xhtml_s118a)

1.  Which model for administrative user security would you use if you wished to maintain a CMOD system by separating the security on the CMOD objects on the system based on the different company departments?
2.  List three different types of files you might expect to process using CMOD and outline the CMOD indexer you would use to process them.

# [Key Terms](#toc.xhtml_s119a)

*   **ACIF**: The **AFP** Conversion and Indexing Facility (**ACIF**) for **AFP**
*   **AFP:** Advanced Function Presentation **(AFP)** is a set of licensed programs that use the all-points-addressable concept to print text and graphics on a printer.
*   **PDF**: The Adobe “Portable Document Format” is a format that cannot be easily modified but allows anyone to share and print it.
*   **MVS**: Multiple Virtual Storage is an operating system used on an IBM Z mainframe.
*   **DDL:** Data Definition Language (DDL), sometimes called Data Description Language, is a subset of the SQL language, used to create and modify the structure of Tables and Indexes in a database.

# [CHAPTER 9](#toc.xhtml_c09)

# [CMOD Java API Examples](#toc.xhtml_c09)

# [Introduction](#toc.xhtml_s120a)

In this chapter, we will list several examples of Java programs, which we have updated to work with the **IBM CMOD OnDemand API** at version **10.5.0.7,** and demonstrate running them in an **Eclipse IDE** environment on a **Linux** server.

We will start by demonstrating the **ODPing** Java program build and run, which is used to check that the connection from the **Linux** **CMOD API** to the **Windows CMOD** Object Server system is working, and this returns the list of **CMOD** Folders.

Next, we will build and run the Java **CallbackSearchExample** program which connects to the **Windows CMOD** Server **System Log** folder.

The last Java program, **TcLoadDocs**, we will build and run to demonstrate loading an example **AFP** document and its field attributes using the example **Baxter Bay Credit Applications Group** and **Application**.

# [Structure](#toc.xhtml_s121a)

In this chapter, we will discuss the following topics:

*   **ODPing.java** Java Source Code and Testing
    *   **module-info.java**
    *   Run Results for **ODPing**
    *   Setting the **Linux** **archive** User with **IBM FileNet P8** Administrator Permissions
*   **CallbackSearchExample.java** Java Source Code and Testing
    *   Run Results for the **CallbackSearchExample**
*   Configuring and Correcting the Java code
    *   The **IBM CMOD** Password Issue
    *   Run Results for the **CallbackSearchExample**
*   Loading a Document – **TcLoadDocs.java**
    *   Logs for the Document Loaded on the Windows Server, **DESKTOP-B3JB93R**

# [`ODPing.java` Java Source Code and Testing](#toc.xhtml_s122a)

This code has been modified to work on the **CMOD V10.5.0.7** in a **Linux** environment, connecting to an **IBM CMOD V10.5.0.7** system working on a **Windows** server, using the Java code source from the **IBM Redbook for CMOD V8.4**, **ODWEK-BasicsAndBeyond.pdf**.

See:

**[https://cmod.wiki/dox/ODWEK-BasicsAndBeyond.pdf](https://cmod.wiki/dox/ODWEK-BasicsAndBeyond.pdf)**

**Note:** *“IBM’s COPYRIGHT LICENSE: This information contains sample application programs in source language, which illustrate programming techniques on various operating platforms.* ***You may copy, modify, and distribute these sample programs in any form without payment to IBM, for the purposes of developing, using, marketing or distributing application programs conforming to the application programming interface for the operating platform for which the sample programs are written****.” These examples have not been thoroughly tested under all conditions.* ***IBM****, therefore, cannot guarantee or imply reliability, serviceability, or function of these programs.”*

Refer to the following link:

[https://www.ibm.com/support/pages/using-load-capabilities-through-odwek](https://www.ibm.com/support/pages/using-load-capabilities-through-odwek), (see also [https://cmod.wiki/dox/ODapiDoc/v9.5/](https://cmod.wiki/dox/ODapiDoc/v9.5/), and the pdf [https://publibfp.dhe.ibm.com/epubs/pdf/c1892312.pdf](https://publibfp.dhe.ibm.com/epubs/pdf/c1892312.pdf)) describes some of the prerequisites and provides another **Java** code example for the **TcLoadDocs.java** (which we obtained from the **IBM RedBook** **pdf** link).

1.  The **Linux Eclipse IDE** is loaded using **`./eclipse`**, as shown in *[Figure 9.1](#c09.xhtml_fig9_1)*:

    ![](images/Figure9.1.jpg)

    **Figure 9.1:** The ***Linux Eclipse IDE*** is loaded using ***`./eclipse`***

2.  The **Eclipse IDE** program prompts for the workspace directory to use, as shown in *[Figure 9.2](#c09.xhtml_fig9_2)***:**

    ![](images/Figure9.2.jpg)

    **Figure 9.2:** The ***Eclipse IDE*** program prompts for the workspace directory to use

3.  We have a recent **Java JRE 17** version, **Eclipse IDE** program dated **June, 2023**, which shows the version on loading, as shown in *[Figure 9.3](#c09.xhtml_fig9_3)***:**

    ![](images/Figure9.3.jpg)

    **Figure 9.3:** We have a recent ***Java JRE 17*** version, ***Eclipse IDE*** program dated ***June, 2023***

4.  We have created a new Java Project, called **`ODAPI_Tests`**, as shown in *[Figure 9.4](#c09.xhtml_fig9_4)*, to which we have loaded three main Java program code sources for testing, **`CallbackSearchExample.java`**, **`ODPing.java`**, and **`TcLoadDocs.java`**.

    ![](images/Figure9.4.jpg)

    **Figure 9.4:** We have loaded ***Java*** sources, ***CallbackSearchExample.java***, ***ODPing.java*** and ***TcLoadDocs.java***

5.  Running the **ODPing** **Java** program in **Eclipse IDE**, after a number of small code changes and additions of the required library dependencies and folder **PATH** environment settings, gives the **Console** log output displaying the expected **Windows CMOD** server folders, as shown in *[Figure 9.5](#c09.xhtml_fig9_5)*:

    ![](images/Figure9.5.jpg)

    **Figure 9.5:** The ***ODPing*** ***Console*** log output displaying the ***Windows CMOD*** server folders

The **ODPing.java** code listed here was run to produce the result shown in *[Figure 9.5](#c09.xhtml_fig9_5).*

**`package`** `com.asb;`

**`import`** `java.util.Enumeration;`

**`import`** `com.ibm.edms.od.ODConfig;`

**`import`** `com.ibm.edms.od.ODConstant;`

**`import`** `com.ibm.edms.od.ODException;`

**`import`** `com.ibm.edms.od.ODFolder;`

**`import`** `com.ibm.edms.od.ODServer;`

**`import`** `com.google.gson.Gson;      //ASB Added for 10.5 working code`

**`import`** `org.apache.logging.log4j.LogManager;  //ASB Added for 10.5 working code`

`/**`

`* This class demonstrates connecting to an OnDemand`

`* server using Version 10.5 of the ODWEK Java API`

`* by providing a simple ping console utility.`

`*`

`* */`

**`public`****`class`** `ODPing`

`{`

**`public`****`static`****`void`** `main (String[] args) {`

`String serverName = "DESKTOP-B3JB93R"; // Name or IP address //ASB Our windows server`

`//String serverName = "ECMUKDEMO22"; // Name or IP address`

`String userId = "ADMIN"; // User ID  //ASB Default`

`String pwd = "filenet123"; // User password //ASB Must be eight characters minimum`

**`int`** `port = 1445; // Default port for OD.` `Configurable.  //ASB Default port`

`//`

`// Configure a new OnDemand server connection with`

`// the default configuration for this`

`// platform`

`//`

`ODServer odServer =` **`new`** `ODServer (`**`new`** `ODConfig ());`

**`try`** `{`

`//`

`// Set server and log-on credentials`

`//`

`odServer.setConnectType (ODConstant.w`***`CONNECT_TYPE_TCPIP`***`);`

`odServer.setServerName (serverName); // Name or IP address`

`odServer.setPort (port);`

`odServer.setUserId (userId);`

`odServer.setPassword (pwd);`

`//`

`// Initialize the ODServer connection;`

`// once initialized, connection MUST be`

`// terminated when we're finished.`

`// Note use of this class' name, ODPing,`

`// as parameter to initialize().`

`//`

`odServer.initialize ("ODPing");`

`//`

`// Log on`

`//`

`odServer.logon ();`

`//`

`// Report ping status`

`//`

`System.`***`out`***`.println ("OnDemand server " +`

`odServer.getServerName () + " is alive");`

`//`

`//Perform some useful function`

`//`

*`listFolders`* `(odServer);`

`}`

**`catch`** `(ODException e) {`

`//`

`//If server returns a "bad credentials"`

`//code 2107, then it must be alive`

`//`

**`if`** `(e.getErrorId () == 2107)`

`{`

`System.`***`out`***`.print ("OnDemand server " +`

`odServer.getServerName () + " is alive but: ");`

`System.`***`out`***`.println (e.getErrorMsg ());`

`}`

**`else`**

`{`

`System.`***`err`***`.println ("Encountered error: " +`

`e.getErrorMsg ());`

`System.`***`err`***`.println (" Error code: " +`

`e.getErrorId ());`

`}`

`}`

**`catch`** `(Exception e) {`

`//Unknown problem`

`e.printStackTrace ();`

`}`

**`finally`** `{`

`//`

`//Ensure user is logged off`

`//`

**`try`** `{ odServer.logoff (); }`

**`catch`** `(Exception e) { /* ignore any problem */ }`

`//`

`//ALWAYS terminate connections that`

`//are no longer needed`

`//`

`odServer.terminate ();`

`}`

`}`

**`public`****`static`****`void`** `listFolders (ODServer odServer)`

**`throws`** `Exception`

`{`

`Enumeration en = odServer.getFolders ();`

**`while`** `(en.hasMoreElements ()) {`

`System.`***`out`***`w.println ("Folder: " +`

`((ODFolder) en.nextElement ()).getName ());`

`}`

`}`

`}`

# [`module-info.java`](#toc.xhtml_s123a)

The following **`module-info.java`** code module listing is used to reference the dependent classes imported:

`/**`

`*`

`*/`

`/**`

`*`

`*/`

**`module`** `ODAPI_Tests {`

**`requires`** `ODApi;          //ASB required for this Eclipse implementation`

**`requires`** `com.google.gson;  //ASB required`

**`requires`** `org.apache.logging.log4j; //ASB required`

`}`

# [Run Results for ODPing](#toc.xhtml_s124a)

The run results for the **ODPing** program are listed as follows:

`OnDemand server DESKTOP-B3JB93R is alive`

`Folder: Invoices`

`Folder: System Load`

`Folder: System Log`

The **`LD_LIBRARY_PATH`** environment variable, value of **`/opt/ibm/ondemand/V10.5/www`**, is added to the **`ODPing`** properties **`Environment`** tab, as shown in *[Figure 9.6](#c09.xhtml_fig9_6)*:

![](images/Figure9.6.jpg)

**Figure 9.6:** The ***LD_LIBRARY_PATH*** environment path is added as ***/opt/ibm/ondemand/V10.5/www***

We also added the following additional **`Environment`** tab settings, as shown in *[Figure 9.7](#c09.xhtml_fig9_7)*:

![](images/Figure9.7.jpg)

**Figure 9.7:** We also added additional variable values for the Environment variables above

# [Setting the Linux Archive User with IBM FileNet P8 Administrator Permissions](#toc.xhtml_s125a)

1.  The **archive** user was set up as a valid user on the **Linux IBM FileNet P8 Content Engine**, using the **acce** web administration tool, ([http://ecmukdemo22:9080/acce](http://ecmukdemo22:9080/acce)), as shown in *[Figure 9.8](#c09.xhtml_fig9_8)*:

    ![](images/Figure9.8.jpg)

    **Figure 9.8:** The ***archive*** user was set up as a valid user on the ***Linux IBM FileNet P8 Content Engine***

2.  The **acce** web application tool is used to select the **`P85510ECM`** P8 Domain and the **`Security`** tab allows us to use the **`Add Permissions`**-> **`Add User Group Permission`…** menu to add the **`archive`** user from our **`ECMUKDEMO77`** **`LDAP`** server list, as shown in *[Figure 9.9](#c09.xhtml_fig9_9):*

    ![](images/Figure9.9.jpg)

    **Figure 9.9:** The archive user is selected from our ***ECMUKDEMO77*** ***LDAP*** server list

3.  The **archive** user is given the **Full Control** permissions, as shown in *[Figure 9.10](#c09.xhtml_fig9_10)*, to apply to **`"This object and all children"`**.

    ![](images/Figure9.10.jpg)

    **Figure 9.10:** The ***archive*** user is given the permissions to apply to “***This object and all children***”

4.  The **`OK`** command can be used to commit the change in security on the **`Add Users and Groups`** window, resulting in the display to commit the changes using the **`Save`** and **`Refresh`** command buttons, as shown in *[Figure 9.11](#c09.xhtml_fig9_11)***:**

    ![](images/Figure9.11.jpg)

    **Figure 9.11:** The ***Save*** and ***Refresh*** command buttons commit the changes for the ***archive*** user security

The two additional import statements are listed as follows:

**`import`** `com.google.gson.Gson;`

**`import`** `org.apache.logging.log4j.LogManager;`

These statements are added as shown in *[Figure 9.12](#c09.xhtml_fig9_12)* to provide working code for **IBM CMOD** version **10.5.0.7**.

Initially, the **`archive/filenet`** user and password were tested which gave the program error:

`OnDemand server DESKTOP-B3JB93R is alive but: The User ID or Password is not valid for the server`

This was then changed to the **`ADMIN / filenet123`** user and password, which ran successfully.

![](images/Figure9.12.jpg)

**Figure 9.12:** Two additional import statements, highlighted above, are added

The highlighted dependency libraries are added to allow the **`ODPing`** Java program to run, as shown in *[Figure 9.13](#c09.xhtml_fig9_13)*:

![](images/Figure9.13.jpg)

**Figure 9.13:** The highlighted dependency libraries are added to allow the ***ODPing*** Java program to run

An additional **`SRVR_OD_STASH`** environment variable is added to the **`Environment`** tab of the **`ODPing`** program, **`Edit`** command for the program launch properties, shown in *[Figure 9.14](#c09.xhtml_fig9_14):*

![](images/Figure9.14.jpg)

**Figure 9.14:** The ***SRVR_OD_STASH*** environment variable is added to the ***Environment*** tab of the ***ODPing*** program

# [`CallbackSearchExample.java` Java Source Code and Testing](#toc.xhtml_s126a)

The updated working **`CallbackSearchExample.java`** program is shown in the list as follows:

**`package`** `com.asb;`

**`import`** `java.io.BufferedReader;   //ASB Added Import`

**`import`** `java.io.IOException;   //ASB Added Import`

**`import`** `java.io.InputStreamReader;   //ASB Added Import`

**`import`** `com.ibm.edms.od.ODCallback;`

**`import`** `com.ibm.edms.od.ODConfig;      //ASB Added Import`

**`import`** `com.ibm.edms.od.ODConstant;`

**`import`** `com.ibm.edms.od.ODCriteria;`

**`import`** `com.ibm.edms.od.ODFolder;`

**`import`** `com.ibm.edms.od.ODServer;`

`/**`

`* Demonstrates folder search using a custom callback object.`

`*/`

**`public`****`class`** `CallbacksearchExample`

`{`

**`static`** `ODServer` *`odServer`* `=` **`null`**`;`

**`public`****`static`****`void`** `main (String[] args)` **`throws`** `Exception`

`{`

*`connect`* `(`

`"CallbackSearchExample",  `

`"DESKTOP-B3JB93R", 1445,    // ASB Changed from mydocserver to DESKTOP-B3JB93R`

`"ADMIN", "filenet123"             // ASB Changed to ADMIN and filenet123 from myusername", "mypassword`

`);`

**`try`**

`{`

`ODFolder folder =` *`odServer`*`.openFolder ("System Log"); //Recent Folders`

`MyCallback callback =` *`getCallback`* `(folder);`

`ODCriteria crit = folder.getCriteria ("Message");`

`crit.setOperator (ODConstant.`***`OPEqual`***`);  //ASB Changed to setOperator from setOperand`

`crit.setSearchValue ("%pdf%");`

`//crit = folder.getCriteria ("TimeStamp");`

`//crit.setOperator (ODConstant.OPLike);  //ASB Changed to set Operator from setOperand`

`//crit.setSearchValue ("%2024-04-02%");`

`System.`***`out`***`.print("Criteria Description   :" + crit.getDescription() + "\r\n"); //ASB Added for debug`

`System.`***`out`***`.print("Search Operator        :" + crit.getOperator() +    "\r\n"); //ASB Added for debug`

`System.`***`out`***`.print("Search Operator Values :" + crit.getFixedValues() + "\r\n"); //ASB Added for debug`

`folder.search (callback);`

`folder.close ();`

`}`

**`catch`** `(Exception e) { e.printStackTrace (); }`

**`finally`**

`{`

*`disconnect`* `();`

`}`

`}`

**`static`****`void`** `connect`

`(`

`String applicationName,`

`String server,`

**`int`** `port,`

`String usr,`

`String pwd`

`)` **`throws`** `Exception`

`{`

*`odServer`* `=` **`new`** `ODServer (`**`new`** `ODConfig ());`

*`odServer`*`.initialize (applicationName);`

*`odServer`*`.setPort (port);`

*`odServer`*`.setServerName (server);  //ASB Changed to setServerName from setServer`

*`odServer`*`.setUserId (usr);`

*`odServer`*`.setPassword (pwd);`

*`odServer`*`.setConnectType (ODConstant.`***`CONNECT_TYPE_TCPIP`***`);`

*`odServer`*`.logon ();`

`}`

**`static`****`void`** `disconnect ()` **`throws`** `Exception`

`{`

**`if`** `(`*`odServer`* `!=` **`null`**`)`

`{`

*`odServer`*`.logoff ();`

*`odServer`*`.terminate ();`

*`odServer`* `=` **`null`**`;`

`}`

`}`

`/**`

`* Factory method`

`*`

`*` **`@param`** `folder An open ODFolder`

`*` **`@return`** `A callback that prints displayable hit fields`

`* in correct display order for the given`

`* folder`

`*/`

**`public`****`static`** `MyCallback getCallback (ODFolder folder)`

`{`

`String[] displayOrder = folder.getDisplayOrder ();`

`String[] queryOrder = folder.getQueryOrder ();`

**`int`**`[] showIndex =` **`new`****`int`**`[displayOrder.length];`

`display:` **`for`** `(`**`int`** `i=0; i<displayOrder.length; i++)`

`{`

`ODCriteria criterion = folder.getCriteria (displayOrder[i]);`

`showIndex[i] = -1;   // -1 --> don't display`

**`if`** `(criterion !=` **`null`** `&& criterion.isDisplayable ())`

`{`

**`for`** `(`**`int`** `j=0; j<queryOrder.length; j++)`

**`if`** `(queryOrder[j].equals (displayOrder[i]))`

`{`

`showIndex[i] = j;`

**`continue`** `display;`

`}`

`}`

`}`

**`return`****`new`** `MyCallback (showIndex);`

`}`

`/**`

`* Custom callback class that prints search results`

`* to the console.` `Display values for hit fields`

`* are printed in the order given to the constructor.`

`*/`

**`public`****`static`****`class`** `MyCallback` **`extends`** `ODCallback`

`{`

**`int`**`[] displayOrder =` **`null`**`;`

**`public`** `MyCallback (`**`int`**`[] showIndex)`

`{`

`displayOrder =` **`new`****`int`**`[showIndex.length];`

`System.`*`arraycopy`* `(`

`showIndex, 0, displayOrder, 0, showIndex.length);`

`}`

**`public`****`boolean`** `HitCallback (`

`java.lang.String docId,`

**`char`** `type,`

`java.lang.String[] values)`

**`throws`** `java.lang.Exception`

`{`

`// print index field values in display order`

**`for`** `(`**`int`** `i=0; i<displayOrder.length; i++)`

**`if`** `(displayOrder[i] != -1)`

`System.`***`out`***`.print (values[displayOrder[i]] + " ");`

`System.`***`out`***`.println ();`

`System.`***`out`***`.print ("Continue searching (y/n)?` `");`

`String response =` **`null`**`;`

`BufferedReader in =` **`new`** `BufferedReader (`**`new`** `InputStreamReader (System.`***`in`***`));`

**`try`**

`{`

`response = in.readLine ();`

`}`

**`catch`** `(IOException e)`

`{`

`e.printStackTrace ();`

`System.`***`err`***`.println (`

`"Error reading user input; search cancelled.");`

**`return`****`false`**`;`

`}`

**`if`** `(response !=` **`null`** `&&`

`response.toUpperCase ().startsWith ("Y"))`

`{`

**`return`****`true`**`; // true --> continue searching`

`}`

**`else`****`return`****`false`**`; // false --> cancel search`

`}`

`}`

`}`

# [Run Results for the `CallbackSearchExample`](#toc.xhtml_s127a)

`Criteria Description   :The message text of the event`

`Search Operator        :1`

`Search Operator Values :null`

# [Loading a document – `TcLoadDocs.java`](#toc.xhtml_s128a)

We loaded a test **AFP** document using a modified version of the **`TcLoadDocs.java`** program, from the **AFP** file examples, supplied after installing the **Ricoh AFP Viewer** described in *[Chapter 8, CMOD System User Administration on Linux](#c08.xhtml)*. These example **AFP** files were copied to our Linux server, **Eclipse** **`ODAPI_Tests`** project work directory, as shown in *[Figure 9.15](#c09.xhtml_fig9_15),* using the commands**:**

`cd /root/eclipse-workspace/ODAPI_Tests/`

`cp /mnt/hgfs/Installs/AFP_Samples/*.afp .`

![](images/Figure9.15.jpg)

**Figure 9.15:** The ***AFP file*** examples we have from installing the ***Ricoh AFP Viewer*** are copied

The **`TcLoadDocs.java`** source code is modified, as shown in *[Figure 9.16](#c09.xhtml_fig9_16)*, to allow the **`insure.afp`** example file we copied to the **`/root/eclipse-workspace/ODAPI_Tests/`** to be loaded.

![](images/Figure9.16.jpg)

**Figure 9.16:** The ***TcLoadDocs.java*** source code is modified to allow the ***insure.afp*** example file to be loaded

The single-page **`insure.afp`** example file is displayed using the Ricoh Workbench Viewer, as shown in *[Figure 9.17](#c09.xhtml_fig9_17)*:

![](images/Figure9.17.jpg)

**Figure 9.17:** The single-page ***insure.afp*** example file is displayed

We have the following modified Java code working on the **Eclipse IDE** on **Linux** with the successful loading of the test document to our **IBM OnDemand Windows** server, **`DESKTOP-B3JB93R`**, as listed:

**`package`** `com.asb;`

**`import`** `java.io.File;`

**`import`** `java.util.*;`

**`import`** `com.ibm.edms.od.*;`

**`public`****`class`** `TcLoadDocs`

`{`

**`public`****`static`****`void`** `main ( String argv[] )`

`{`

`ODServer    odServer;`

`ODConfig    odConfig;`

`Hashtable<String,String> idxs;`

`File        loadFile;`

`String serverName = "DESKTOP-B3JB93R"; // Name or IP address – The Windows server`

`//String serverName = "ECMUKDEMO22"; // Name or IP address – The Linux server`

`String userId = "ADMIN";   // User ID`

`String pwd = "filenet123"; // User password`

**`int`** `port = 1445; // Default port for OD.` `Configurable.`

`//argv[0]= serverName;`

`//argv[1]= userId;`

`//argv[2]= pwd;`

`//if ( argv.length < 3 )`

`//{`

`//    System.out.println( "usage: java TcLoadDocs <server> <userid> <password> " );`

`//    return;`

`//}`

**`try`**

`{`

`//----------`

`// Set the stage`

`//----------`

`System.`***`out`***`.println( "This testcase should" );`

`System.`***`out`***`.println( "  Demonstrate the ODWEK Load Process" );`

`System.`***`out`***`.println( "" );`

`System.`***`out`***`.println( "---------------------------------------------------" );`

`System.`***`out`***`.println( "" );`

`odConfig =` **`new`** `ODConfig`

`(ODConstant.`***`PLUGIN`***`,`

`ODConstant.`***`APPLET`***`,`

**`null`**`,`

`200,`

`"/applets",`

`"ENU",`

`"c:/temp",`

`"c:/trace",`

`0);`

`odServer =` **`new`** `ODServer(odConfig );`

`odServer.initialize(  "TcLoadDocs.java" );`

`//System.out.println( "Logging on to " + argv[0] + "..."` `);`

`//odServer.logon( argv[0], argv[1], argv[2] );`

`System.`***`out`***`.println( "Logging on to " + serverName + "..."` `);`

`odServer.logon( serverName, userId, pwd );`

`//----------`

`// Step 1 in the ODWEK Load process`

`//----------`

`odServer.loadInit();`

`//----------`

`// Step 2 in the ODWEK Load process`

`// Repeated for each document to be loaded`

`//----------`

`idxs =` **`new`** `Hashtable<String, String>();`

`/*              // ASB We have the following Baxter Bay Credit fields`

`*  name`

`account`

`crd_date`

`balance`

`*/`

`idxs.put("name",    "Geoffrey R.` `Stephens"); // ASB Changed to name from acct_name`

`idxs.put("account",     "32414432551"); // ASB Changed to account from acct_num`

`idxs.put("crd_date","2012-03-25");  // ASB Changed to crd_date from purchase_date`

`idxs.put("balance", "1172.18");  // ASB Changed to balance from purchase_amt`

`//loadFile = new File("c:\\invoices\\acme\\bluePaintingInvoice.afp");`

`loadFile =` **`new`** `File("insure.afp");                        //ASB in path  /root/eclipse-workspace/ODAPI_Tests/`

`odServer.loadAddDoc(4, idxs, loadFile);`

`/*  // ASB Try just one document load at first so we have removed  the other 3 files in the  code to be loaded`

`// ASB This is a repeat of the first set of statements  (they could be refactored into a subroutine method call)`

`*/  // ASB Three other example  document load code  stements have been removed from the original example`

`//----------`

`// Step 3 in the ODWEK Load process`

`// Done adding documents, now call the server to load`

`//----------`

`//odServer.loadCommit("Invoices", "InvoicesWestCoast");//ASB Updated to our CMOD configuration`

`odServer.loadCommit("Baxter Bay Credit", "Baxter Bay Credit"); // "Application Group","Application"`

`// Cleanup`

`//----------`

`odServer.logoff( );`

`odServer.terminate( );`

`System.`***`out`***`.println( "" );`

`System.`***`out`***`.println( "---------------------------------------------------" );`

`System.`***`out`***`.println( "" );`

`System.`***`out`***`.println( "Testcase completed" );`

`System.`***`out`***`.println( "" );`

`}`

**`catch`** `( ODException e )`

`{`

`System.`***`out`***`.println( "ODException: " + e );`

`System.`***`out`***`.println( "  id = " + e.getErrorId( ) );`

`System.`***`out`***`.println( "  msg = " + e.getErrorMsg( ) );`

`e.printStackTrace( );`

`}`

**`catch`** `( Exception e2 )`

`{`

`System.`***`out`***`.println( "exception: " + e2 );`

`e2.printStackTrace( );`

`}`

`}`

`}`

The output of running this program in the **Linux Eclipse IDE** was copied as follows, listed in the **Windows server** client program, by highlighting the text to be copied by dragging the mouse and right-clicking it on the highlighted area to select the **`Edit`->** **`Copy Text`** menu option, as shown in *[Figure 9.18](#c09.xhtml_fig9_18)*:

![](images/Figure9.18.jpg)

**Figure 9.18:** Right-mouse click the highlighted area to select the ***Edit-> Copy Text*** menu option

The highlighted text from the **`System Load`** log, in *[Figure 9.19](#c09.xhtml_fig9_19),* confirms that the **`insure.afp`** file and the associated **Index Fields** have been loaded successfully.

![](images/Figure9.19.jpg)

**Figure 9.19:** The highlighted text confirms that the ***insure.afp*** file and the ***Index Fields*** loaded successfully

# [Logs for the Document Loaded on the Windows Server, DESKTOP-B3JB93R](#toc.xhtml_s129a)

The document load example log file details are shown as follows:

*Status log entry details*

`<delim= >`

`<Action:CFS-OD Add>`

`<Application Group Name:Baxter Bay Credit Agid:5017 Load:14FAA>`

`<Status Code Status Text Aid Table Name name account crd_date,yyyy:MM:dd balance CMODDescription,CFS-OD doc_name doc_off doc_len comp_off comp_len annot comp_type rid pri_nid sec_nid>`

`0x0000 Success                      5018 DAA1 GEOFFREY R.` `STEPHENS 32414432551, 2012:03:25 1172.18 8193 14FAAA 0 61207 0 6747 U O 0 1 0`

`L`

*Summary Log Details:*

`2024-06-09 16:51:56.103624: ARS4315I Processing file >c:\arstmp\Baxter Bay Credit.Baxter Bay Credit.ADMIN.20240609.155155870757.16468.ARD<`

`2024-06-09 16:51:56.110787: ARS4334I Load Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  OS Userid <ADMIN>  Install Location <C:\PROGRA~1\IBM\OnDemand\V10.5\>`

`2024-06-09 16:51:56.120440: ARS4335I Server Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  Database <DB2> <11.05.0400>`

`2024-06-09 16:51:56.137818: ARS4339I Application Group >Baxter Bay Credit<`

`2024-06-09 16:51:56.140461: ARS4340I Application >Baxter Bay Credit<`

`2024-06-09 16:51:56.143095: ARS4341I Storage Set >Cache Only - Library Server<`

`2024-06-09 16:51:56.145726: ARS4342I Storage Node >Cache Only - Library Server<`

`2024-06-09 16:51:56.148360: ARS4347I Encryption >None<`

`2024-06-09 16:51:56.150990: ARS4312I Loading started, 61415 bytes to process`

`2024-06-09 16:51:56.169712: ARS1144I OnDemand Load Id = >5017-1-0-14FAA-20120325000000-20120325000000-5018<`

`2024-06-09 16:51:56.375097: ARS1146I Loaded 1 rows into the database`

`2024-06-09 16:51:56.386282: ARS1175I Document compression type used - OD77.  Bytes Stored = >6881< Rows = >1<`

`2024-06-09 16:51:56.393062: ARS4310I Loading completed`

`2024-06-09 16:51:56.413255: ARS4317I Processing successful for file >c:\arstmp\Baxter Bay Credit.Baxter Bay Credit.ADMIN.20240609.155155870757.16468.ARD<`

`2024-06-09 16:51:56.421795: ARS4349I Load Statistics: Index In >61,415<  Load In >61,207<  Load Out >6,881<  Rows >1<  Pages >4<  Time >0.3105<`

The java **`ODAPI_Tests`,** **Eclipse IDE** project supporting libraries and structure are shown in *[Figure 9.20](#c09.xhtml_fig9_20)*:

![](images/Figure9.20.jpg)

**Figure 9.20:** The java ***ODAPI_Tests,*** ***Eclipse IDE*** project supporting libraries and structure

# [Conclusion](#toc.xhtml_s130a)

In this chapter, we listed several example Java programs, which we have updated to work with the **IBM CMOD OnDemand API** at version **10.5.0.7**. We have also demonstrated running them in an **Eclipse IDE** environment on a **Linux** server.

The Java example programs we built and ran included **ODPing**, used to check that the connection from the **Linux** **CMOD API** to the **Windows CMOD** Object Server system was working and returning the list of Windows **CMOD** Folders: the Java **CallbackSearchExample** program connecting to the **Windows CMOD** Server **System Log** folder and the **TcLoadDocs**, program which we used to demonstrate loading an example **AFP** document and its field attributes using the example **Baxter Bay Credit Applications Group** and **Application**.

In the next chapter, *Connecting* ***CMOD*** *to* ***IBM Content Navigator***, we will outline the procedure required to create a repository for the **Linux** server version of **IBM Content Navigator** and demonstrate the browser access to the **Folders** on a **Windows CMOD** server from the **Content Navigator** desktop we create for accessing the **Windows CMOD** server document repository.

# [Points to Remember](#toc.xhtml_s131a)

*   We based our use of the updated **IBM CMOD** programs on an IBM copyright statement, which stated that the sample application programs are in source code language illustrating programming techniques on various operating platforms, that may be copied, modified, and distributed in any form without payment to IBM.
*   The Java code has been modified to work on the **IBM CMOD V10.5.0.7** in a **Linux** environment, using the **ODWEK API**, connecting to an **IBM CMOD V10.5.0.7** system working on a **Windows** server.
*   Additional Java project **Run Edit** property **Environment** variable and **Dependency** library path tab settings are required to allow the Java programs to run without errors.

# [Multiple Choice Questions](#toc.xhtml_s132a)

1.  Which user is used to successfully connect to the **IBM CMOD Windows** server using the Java programs?
    1.  archive
    2.  ADMIN
    3.  root
    4.  p8admin
2.  Which java library provides the **ODWEK API** core calls for our example Java programs?
    1.  `log4j-core-2.20.0.jar`
    2.  `gson-2.10.1.jar`
    3.  `ODApi.jar`
    4.  `log4j-api-2.20.0.jar`

# [Answers](#toc.xhtml_s133a)

1.  b
2.  c

# [Questions](#toc.xhtml_s134a)

1.  What Index Fields are required to be included to enable a document to be added to the Baxter Bay Credit Application Group?
2.  Which IBM CMOD Log Folder would you use to check the successful loading of a Document file using the TcLoadDocs program?

# [Key Terms](#toc.xhtml_s135a)

*   **API**: Application Programmer’s Interface is a library of callable software subroutines written to support the intercommunication between two or more separate functional software systems.
*   **IDE**: Interactive Development Environment is a general description of a tool for program developers providing functions for project creation for software editing, building, testing, and, with Java IDEs, Java jar file library packaging.
*   **JRE**: Java Runtime Environment is a software layer integrated with the operating system software that provides the Java class libraries and other resources, like multiple language support in the **java.util** and **java.text** packages, that Java programs require to run.
*   **ODWEK**: OnDemand Web Enablement Kit is an API, called from Java using the **ODApi.ja**r and also found in the **LD_LIBRARY_PATH** environment variable path, **`/opt/ibm/ondemand/V10.5/www,`** which is used to change a user’s password, retrieve a document, or delete an annotation and can also be used to load new documents.
*   **AFP**: Advanced Function Presentation **(AFP)** is a set of licensed programs that use the all-points-addressable concept to print text and graphics on a printer.

# [CHAPTER 10](#toc.xhtml_c10)

# [Connecting CMOD to IBM Content Navigator](#toc.xhtml_c10)

# [Introduction](#toc.xhtml_s136a)

This chapter outlines the procedure required to create a repository for the **Linux** server version of **IBM Content Navigator** and demonstrates the browse access to the Folders on a **Windows CMOD** server from the **IBM Content Navigator** desktop created for **CMOD**.

We describe the required **WebSphere** application server **Classpath** which is required to provide access to the supporting **ODWEK API** java jar libraries for the deployed IBM Content Navigator web application.

We also cover the **Linux** **`arsload`** program and the switches that are used to load an example file to **CMOD**.

Finally, we cover the procedure required to deploy a viewer map for IBM Content Navigator.

The viewer map consists of a collection of items, each mapping a document MIME type to a viewer that is available in IBM Content Navigator.

# [Structure](#toc.xhtml_s137a)

In this chapter, we will discuss the following topics:

*   Setting Up the **IBM Websphere** **Classpath**
*   Configuring a New **IBM Content Navigator** **Desktop** for **IBM CMOD**
*   **IBM Content Navigator** Desktop After Loading Documents on **Windows**
*   **arsload** Parameters
*   Another Example of the **arsload** Program Command line on **Linux**
    *   Setting Up a Viewer Map
*   Further References

# [Setting Up the IBM Websphere Classpath](#toc.xhtml_s138a)

Before we start to configure the **IBM Content Navigator** Desktop to create a new **IBM Content Manager OnDemand** repository, we have to add the following supporting **IBM CMOD ODWEK** **API** library files to the **IBM Content Navigator, IBM** **WebSphere** web application server **Classpath**:

`/opt/ibm/ondemand/V10.5/www/api/ODApi.jar:/opt/ibm/ondemand/V10.5/jars/gson-2.10.1.jar:/opt/ibm/ondemand/V10.5/jars/log4j-api-2.20.0.jar:/opt/ibm/ondemand/V10.5/jars/log4j-core-2.20.0.jar:/opt/ibm/ondemand/V10.5/www/libars3wapi32.so:/opt/ibm/ondemand/V10.5/www/libars3wapi64.so`

The **IBM WebSphere Application** server **Administration Console** for the **IBM Content Navigator** profile (**AppSrv02**) is logged onto using the **Linux FireFox** web-browser link: https://localhost:9044/ibm/console/login.do?action=secure

1.  Then, we can navigate to the **`Environment -> Shared`** libraries menu tree node path and select the **`ECMClientSharedLib`** environment variable and enter the **Classpath**, as highlighted in *[Figure 10.1](#c10.xhtml_fig10_1):*

    ![](images/Figure10.1.jpg)

    **Figure 10.1:** We navigate to ***Environment -> Shared libraries*** and select the ***ECMClientSharedLib*** variable

2.  The **`Apply`** command is clicked after entering the **Classpath** list for the additional **Linux** server Java library files to support the **ODWEK API,** used for accessing the **Windows CMOD** server repository, as highlighted in *[Figure 10.2](#c10.xhtml_fig10_2):*

    ![](images/Figure10.2.jpg)

    **Figure 10.2:** The ***Apply*** command is clicked after entering the Classpath list for the ***Linux*** server Java library files

3.  The **`Save`** command is used to update the **IBM WebSphere** master configuration repository, as shown in *[Figure 10.3](#c10.xhtml_fig10_3):*

    ![](images/Figure10.3.jpg)

    **Figure 10.3:** The ***Save*** command is used to update the WebSphere master configuration repository

4.  Normally, we can view the **IBM CMOD System Log** files by running the version **10.5.0.7, IBM Windows OnDemand Client (64-bit)** program to select the **IBM CMOD** server, as shown in *[Figure 10.4](#c10.xhtml_fig10_4):*

    ![](images/Figure10.4.jpg)

    **Figure 10.4:** View the ***IBM CMOD System Log*** files by running ***IBM Windows OnDemand Client (64-bit)***

5.  Then after logging into the **IBM Windows OnDemand Client,** we can select the specific **`System Log`** file folder to search, as shown in *[Figure 10.5](#c10.xhtml_fig10_5):*

    ![](images/Figure10.5.jpg)

    **Figure 10.5:** We can select the specific ***System Log*** file folder to search

6.  This then allows us to select the highlighted **`Search`** command button (after optionally filtering the list of log records, using the **Search Criteria** filter fields), as illustrated in *[Figure 10.6](#c10.xhtml_fig10_6):*

    **Note:** *There are useful expansions of any errors reported, especially* ***`arsdoc`*** *database query errors, which are displayed in the System Log. We will cover specific examples in [Chapter 13, Running **arsload**](#c13.xhtml)*.

    ![](images/Figure10.6.jpg)

    **Figure 10.6:** The Windows ***CMOD OnDemand*** Logging System Log file displayed in the ***IBM CMOD Client*** program

# [Configuring a New IBM Content Navigator Desktop for IBM CMOD](#toc.xhtml_s139a)

1.  After the **IBM Content Navigator** web application **Classpath** has been updated for use of the **ODWEK API**, we can restart the web application and launch and configure the integration with the **Windows CMOD** server using the **Linux, IBM Content Navigator** **admin** desktop, using the web URL: [http://ecmukdemo22:9081/navigator/?desktop=admin](http://ecmukdemo22:9081/navigator/?desktop=admin), as shown in *[Figure 10.7](#c10.xhtml_fig10_7):*

    ![](images/Figure10.7.jpg)

    **Figure 10.7:** The web URL: [http://ecmukdemo22:9081/navigator/?desktop=admin](http://ecmukdemo22:9081/navigator/?desktop=admin), for configuration

2.  This shows the base **Desktop** configuration for **`IBM Content Manager OnDemand`**, pre-built into the **IBM Content Navigator** application (**`IBM Content Navigator`** supports **IBM Content Manager OnDemand** servers running **CMOD version 8.5.0.x** and above). We can now select the **`Repositories`** node and select the **`New Repository`** drop-down for the **`Content Manager OnDemand`** repository type, as highlighted in *[Figure 10.8](#c10.xhtml_fig10_8):*

    ![](images/Figure10.8.jpg)

    **Figure 10.8:** We can now select the ***Repositories*** node and select ***New Repository*** drop-down

3.  Next, we enter the **IBM CMOD** Repository name, **`CMOD_DOCS`**, that we require, and the details, as highlighted in *[Figure 10.9](#c10.xhtml_fig10_9)*, and select the **`Connect`…** command button.

    ![](images/Figure10.9.jpg)

    **Figure 10.9:** We enter the ***IBM CMOD*** name, ***CMOD_DOCS***, and the details and then select the ***Connect…*** button.

4.  The pop-up window prompts us to Log into the Windows **IBM** **CMOD**, **`CMOD-Docs`** repository, using the **`ADMIN`** user and password, as shown in *[Figure 10.10](#c10.xhtml_fig10_10):*

    ![](images/Figure10.10.jpg)

    **Figure 10.10:** The pop-up window prompts us to Log into the Windows ***IBM*** ***CMOD***, ***CMOD-Docs*** repository

5.  The **`Configuration Parameters`** tab can now be selected and any **CMOD** repository specific parameters can be entered as required, as shown in *[Figure 10.11](#c10.xhtml_fig10_11):*

    ![](images/Figure10.11.jpg)

    **Figure 10.11:** The ***Configuration Parameters*** tab shows the ***CMOD*** repository parameters which can be entered

6.  Next, we select the **`Search`** tab to specify the number of returned search result rows allowed from the repository and we select the **`Save and Close`** command button, as highlighted in *[Figure 10.12](#c10.xhtml_fig10_12):*

    ![](images/Figure10.12.jpg)

    **Figure 10.12:** Select the ***Search*** tab, for the search result rows allowed from the repository and ***Save and Close***

7.  The **`Refresh`** command button can be selected to update the browser for the **CMOD-Docs** repository we created as indicated in the pop-up window, as illustrated in *[Figure 10.13](#c10.xhtml_fig10_13):*

    ![](images/Figure10.13.jpg)

    **Figure 10.13:** The ***Refresh*** command button can be selected to update the browser for the ***CMOD-Docs*** repository

8.  The new **CMOD-Docs** repository can now be viewed in the **IBM Content Navigator** **admin** desktop, as highlighted in *[Figure 10.14](#c10.xhtml_fig10_14):*

    ![](images/Figure10.14.jpg)

    **Figure 10.14:** The new ***CMOD-Docs*** repository can now be viewed in the ***IBM Content Navigator*** ***admin*** desktop

9.  We can now create a new **IBM Content Navigator Desktop**, by selecting the **`Desktops`** node and then selecting the **`New Desktop`** command button, as highlighted in *[Figure 10.15](#c10.xhtml_fig10_15):*

    ![](images/Figure10.15.jpg)

    **Figure 10.15:** Select the ***Desktops*** node and then selecting the ***New Desktop*** command button

10.  The **`New Desktop`** tab is opened to enable the **`Name`,** **`ID`,** **`Description`,** and the **`Repository`** we created is selected, as highlighted in *[Figure 10.16](#c10.xhtml_fig10_16):*

    ![](images/Figure10.16.jpg)

    **Figure 10.16:** The ***New Desktop*** tab is opened to enable the ***Name, ID, Description,*** and the ***Repository***

11.  The other tabs were left with the default values, which are set to display the **`Home`** and **`Search`** menus and the **`Save and Close`** command button, shown in *[Figure 10.16](#c10.xhtml_fig10_16)*, is used to display the new Desktop, as highlighted in *[Figure 10.17](#c10.xhtml_fig10_17):*

    ![](images/Figure10.17.jpg)

    **Figure 10.17:** The ***Save and Close*** command button, shown in Figure 10:16, is used to display the new Desktop

12.  We can now log onto the new **IBM Windows CMOD desktop** on the **IBM Content Navigator** **Linux** server’s **FireFox** web-browser using the **ADMIN/filenet123** Windows **CMOD** server password, using the link, as shown in *[Figure 10.18](#c10.xhtml_fig10_18):* [http://ecmukdemo22:9081/navigator/?desktop=ContentManagerOnDemand](http://ecmukdemo22:9081/navigator/?desktop=ContentManagerOnDemand)

    ![](images/Figure10.18.jpg)

    **Figure 10.18:** The log onto the new ***IBM Windows CMOD desktop*** on ***IBM Content Navigator*** for ***Linux***

13.  This shows the **`System Log`** folder search results, as shown in *[Figure 10.19](#c10.xhtml_fig10_19):*

    ![](images/Figure10.19.jpg)

    **Figure 10.19:** The Windows ***System Log*** folder search results on the Linux IBM Content Navigator

14.  We can now select the **`Magazine view`** of the **IBM Content Navigator CMOD** desktop, in the top-right corner, as highlighted in *[Figure 10.20](#c10.xhtml_fig10_20):*

    ![](images/Figure10.20.jpg)

    **Figure 10.20:** We can now select the ***Magazine view*** of the ***IBM Content Navigator CMOD*** desktop

15.  The selected **Magazine view** of the **Desktop** is illustrated in *[Figure 10.21](#c10.xhtml_fig10_21):*

    ![](images/Figure10.21.jpg)

    **Figure 10.21:** The selected ***Magazine view*** of the ***Desktop***

# [IBM Content Navigator Desktop After Loading Documents on Windows](#toc.xhtml_s140a)

1.  The document we described loaded using the **`TcLoadDocs.java`** program in *[Chapter 9, CMOD Java API Examples](#c09.xhtml)*, can be viewed in the **IBM Content Navigator**, **ContentManagerOnDemand** Desktop we created, as shown in *[Figure 10.22](#c10.xhtml_fig10_22):*

    ![](images/Figure10.22.jpg)

    **Figure 10.22:** The document we described loaded using the ***TcLoadDocs.java*** program

2.  The **Magazine view** shows the detail of the **ID** of the loaded document, as illustrated in *[Figure 10.23](#c10.xhtml_fig10_23):*

    ![](images/Figure10.23.jpg)

    **Figure 10.23:** The ***Magazine view*** shows the detail of the ***ID*** of the loaded document from the ***TcLoadDocs*** example

3.  We also try a search date range to show the **Windows** **`arsload`** program document loads for the **Baxter Bay Credit** **Application** group, which we completed earlier on the **Windows** version of the **`arsload`** program, as displayed in *[Figure 10.24](#c10.xhtml_fig10_24):*

    ![](images/Figure10.24.jpg)

    **Figure 10.24:** The earlier load of documents on ***Windows*** is displayed in the ***Magazine view***.

4.  The original default view is shown in *[Figure 10.25](#c10.xhtml_fig10_25):*

    ![](images/Figure10.25.jpg)

    **Figure 10.25:** The original default view of the loaded documents

# [`arsload` Parameters](#toc.xhtml_s141a)

The **Linux** **`arsload`** command line program switch parameters can be listed using the command as follows:

`[root@ECMUKDEMO22 bin]#` **`./arsload -h ARCHIVE`**

`ARS4300I Usage: arsload [options] [load_file]`

`Version: 10.5.0.7`

This shows the **`arsload`** program version number and the details of each switch used.

The detailed description of the available switches for the **`arsload`** program is covered in *[Chapter 8, CMOD System User Administration on Linux](#c08.xhtml)*, in the section titled, *Administration of the CMOD Generic Indexer.*

# [Another Example of the arsload Program Command Line on Linux](#toc.xhtml_s142a)

An example command line to load a **`letters.ind`** file is shown as follows:

`/opt/IBM/ondemand/V10.5/bin/arsload -h ARCHIVE -u archive -n -g Letters letters`

In the above example, we have specified the following parameters to the **arsload** program:

**`-h ARCHIVE`** This is the name of the **CMOD** instance.

**`-u archive`** This is the name of a **CMOD** user with permissions to add documents to the **Application Group**. This is usually a user who has administrator permissions for the **Application Group**.

**`-n`** This is the switch which prevents the input files being deleted.

**`-g Letters`** The name of the **Application Group** to load.

**`letters`** The name of the input file to be processed.

In this example, the **`arsload`** program is run to find the input file **letters.ind** in the same directory where the program was started. The **`letters.ind`** input file contains the index information that can be created in the **Creating index** data (which is a parameter file for the **Generic indexer**).

**Note:** *The full path names of the input files are not specified in the parameter file, in this example, so the input files must be in the directory where the* ***`arsload`*** *program is started.*

*[Appendix A: IBM Content Manager OnDemand Fix Pack Installation](#appa.xhtml) has examples of running the* ***`arsload`*** *program on a* ***Windows*** *server*.

# [Setting Up a Viewer Map](#toc.xhtml_s143a)

Deploying a viewer map for IBM Content Navigator can be a little more complex.

An IBM Content Navigator viewer map consists of a collection of items, each mapping a document MIME type to a viewer that is available in IBM Content Navigator.

**Note:** *Each desktop can have only one viewer map assigned to it at any given time.*

IBM Content Navigator uses one database table to store state information. Here, this database is called **`ECM`** and our schema is named **`ECMUSER`**. The table contains two columns named **ID** (String) and **ATTRIBUTES** (CLOB). The **ID** row has the following format:

**`[COMPONENT_TYPE]`**`.navigator.`**`[COMPONENT_ID]`**

For example, for the plugin we have added:

`db2 =>` **`connect to ECM`**

`Database Connection Information`

`Database server        = DB2/LINUXX8664 11.5.7.0`

`SQL authorization ID   = DB2INST1`

`Local database alias   = ECM`

`db2 =>` **`SELECT * from ECMUSER.CONFIGURATION WHERE ID = 'plugin.navigator.AFPViewerPlugin'`**

Field **ID:**

`plugin.navigator.AFPViewerPlugin`

**Field ATTRIBUTES:**

`filename=/opt/IBM/ECMClient/plugins/AFPViewerPlugin.jar;name=AFP Viewer;ordering=6;checksumValidated=false;actions=;configClass=;enabled=true;checksum=;version=2.0.3.5;dependencies=;optional=false;viewers=`

There is a default **Viewer Map** stored in the IBM Content Navigator configuration database, which can be updated using the IBM Content Navigator admin desktop GUI, following the procedure in the following link:

[https://www.ibm.com/support/pages/configuring-viewers-ibm-content-navigator-desktop](https://www.ibm.com/support/pages/configuring-viewers-ibm-content-navigator-desktop)

1.  The **`Viewer Maps`** node is selected and then a **`New Viewer Map`** command button is selected to show the page shown in *[Figure 10.26](#c10.xhtml_fig10_26):*

    ![](images/Figure10.26.jpg)

    **Figure 10.26:** The ***New Viewer Map*** command button selected shows the command to add a new map

2.  We can now select the **`New Mapping`** command button to enter the **`Repository Type`** and **`Viewe`r**. This will display the **`Available file types`** column mime-type list of the documents available for viewing, which we can double-click as shown in the highlighted **`application/afp`** type example, to add to the **`Selected file types`** list column, as shown in *[Figure 10.27](#c10.xhtml_fig10_27):*

    ![](images/Figure10.27.jpg)

    **Figure 10.27:** Double-click the highlighted ***application/afp*** type example, to add to the ***Selected file types*** list

3.  The **`OK`** command button is selected to save the new **`Viewer Map`**, as highlighted in *[Figure 10.28](#c10.xhtml_fig10_28):*

    ![](images/Figure10.28.jpg)

    **Figure 10.28:** The ***OK*** command button is selected to save the new ***Viewer Map***

4.  The **`New Mapping`** panel describes how the **Viewer Map** types function, as shown in *[Figure 10.29](#c10.xhtml_fig10_29):*

    ![](images/Figure10.29.jpg)

    **Figure 10.29:** The ***New Mapping*** panel describes how the ***Viewer Map*** types function

5.  To store the new **Viewer Map** and **CMODViewerMap0** into the **IBM Content Navigator** configuration database, the **`Save and Close`** command button is selected, as shown in *[Figure 10.30](#c10.xhtml_fig10_30)*:

    ![](images/Figure10.30.jpg)

    **Figure 10.30:** The new ***Viewer Map***, ***CMODViewerMap0***, is saved using the ***Save and Close*** command button

6.  The new **`CMODViewerMap0`** can now be seen listed in the **`Viewer Maps`** list, as highlighted in *[Figure 10.31](#c10.xhtml_fig10_31):*

    ![](images/Figure10.31.jpg)

    **Figure 10.31:** The new ***CMODViewerMap0*** can now be seen listed

7.  We can now associate our **`Content Manager OnDemand`** Desktop with the new **`CMODViewerMap0`,** **`Viewer map`** by selecting it from the drop-down, as highlighted in *[Figure 10.32](#c10.xhtml_fig10_32):*

    ![](images/Figure10.32.jpg)

    **Figure 10.32:** We can now associate our ***Content Manager OnDemand*** Desktop with the new ***CMODViewerMap0***

8.  The detail of the **Viewer map** information icon describes the function they perform, as shown in *[Figure 10.33](#c10.xhtml_fig10_33):*

    ![](images/Figure10.33.jpg)

    **Figure 10.33:** The detail of the ***Viewer map*** information icon describes the function they perform

Alternatively, there is a four-step procedure for deploying a viewer map programmatically:

1\. Deploying the mappings.

Deploying the mappings requires a one row **INSERT** statement for each mapping into the IBM Content Navigator configuration database.

If the **ID** of our viewer map is to be called **CMODViewerMap**, and we want to map an **AFP** IBM Content Manager OnDemand document type to the **`afp2pdf`** viewer, we have to insert the following record to the database:

Field **ID:**

`viewer.navigator.CMODViewerMap0`

Field **ATTRIBUTES:**

`name=CMODViewerMap0;description=CMOD Viewer Map;mappings=CMODViewerMap00,CMODViewerMap01 etc…CMODViewerMap020`

To summarize, we concatenate the name we want to give to our viewer map with a digit, which increments each time we add a new mapping.

Notice that although the order of the mappings in the viewer map are important (for following precedence rules), the numbering scheme task is described in the second step, as follows.

2\. Deploying the viewer map definition.

After the viewer mappings are deployed, we have to define the viewer map by adding the following record to the IBM Content Navigator configuration database.

Field **ID:**

`viewerMapping.navigator.CMODViewerMap00`

Field **ATTRIBUTES:**

`contentTypes=text/html;serverType=p8;viewerName=pdfConversion;id=CMODViewerMap00;previewOnly=false`

and using

`SELECT * from ECMUSER.CONFIGURATION WHERE ID ='viewerMapping.navigator.CMODViewerMap01'`

We can view the next mapping as:

Field **ID:**

`viewerMapping.navigator.CMODViewerMap01`

Field **ATTRIBUTES:**

`contentTypes=text/html;serverType=cm;viewerName=pdfConversion;id=CMODViewerMap01;previewOnly=false`

And the last mapping, which is for the **AFP** viewer:

`SELECT * from ECMUSER.CONFIGURATION WHERE ID ='viewerMapping.navigator.CMODViewerMap020'`

Field **ID:**

`viewerMapping.navigator.CMODViewerMap020`

Field **ATTRIBUTES:**

`contentTypes=application/afp;serverType=od;viewerName=afp2pdf;id=CMODViewerMap020;previewOnly=false`

In this example, the **`CMODViewerMap`** name is used to associate this viewer mapping with all the mappings that which we deployed in the first step (**`CMODViewerMap00,`**

**`CMODViewerMap01…etc CMODViewerMap020`**`).`

3\. Referencing the newly deployed viewer map from our **`ContentManagerOnDemand`** desktop. In this step, the viewer map is assigned to our desktop. To do this step, we can either update the record for the existing **`ContentManagerOnDemand`** desktop or insert a new record into the IBM Content Navigator database if the desktop is being deployed for the first time. The following example is for our desktop, we named **`ContentManagerOnDemand`**:

`"desktop.navigator.ContentManagerOnDemand","...;viewer=CMODViewerMap0;..."`

4\. Declaring the viewer map in IBM Content Navigator. By doing so, it is available to be referenced by other desktops. For the viewer map to be listed in the IBM Content Navigator **`admin`**, Administration Desktop when Viewer Maps is selected, it has to be declared as a global navigator component. This is done by updating the **`application.navigator`** record by adding our viewer map to the viewer attribute:

Field **ID:**

`'application.navigator'`

Field **ATTRIBUTES:**

`'locales=ar,he,en,zh_CN,zh_TW,cs,hr,da,nl,fi,fr,de,el,hu,it,ja,ko,nb,pl,pt,pt_BR,ru,sk,sl,es,sv,th,tr,ro,kk,ca,vi;threadSleepTime=5;`**`plugins`**`=ICMAPIPlugin,CPEAppletsPlugin,ICMPlugin,ICMAdminClientPlugin,ICMMonitor,`**`AFPViewerPlugin`**`;menus=;adminRoles=1693742055003;`**`repositories`**`=icmdos1,icmtos1,`**`CMODDocs`**`;`**`desktops`**`=admin,icm,icmadmin,icmmonitor,AVAOrange,`**`ContentManagerOnDemand`**`;themes=azurite,cordierite,malachite,obsidian,quartz;`**`viewers`**`=default,`**`CMODViewerMap0`**`;redactionReasonsInitialized=false;key=871bf66c911f811fd48a6cc97aea40a4;servers=cm,od,p8,cmis,box;objectExpiration=10;applicationVersion=3.0.3;desktop=default'`

If the preceding steps are not done in the order given, they will still work, but it is important to stop the IBM Content Navigator application in WebSphere and update the IBM Content Navigator database using the four steps above in any order required **before** starting the application again.

IBM Content Navigator makes some server type codes and viewer IDs available by default:

The Server types are:

**`– od`**    For IBM Content Manager OnDemand

**`– cm`**    For IBM Content Manager

**`– p8`**    For IBM FileNet P8 Content Engine

**`– cmis`**    For IBM ECM Content Management Interoperability Services (the open standard)

Viewer IDs:

`– afp2pdf`

`– lineDataApplet`

`– browser`

`– adobeReader`

`– appletViewer`

`– filenetViewer`

`–` **`iccViewer`** `(if the` **`ICCViewer`** `plug-in is installed)`

**Note:** *The viewer attribute is comma-separated if multiple viewer maps exist.*

See the link: [https://www.ibm.com/docs/en/content-navigator/3.1.0?topic=ccnwc-configuring-viewers-used-display-documents-in-web-client](https://www.ibm.com/docs/en/content-navigator/3.1.0?topic=ccnwc-configuring-viewers-used-display-documents-in-web-client)

Each repository uses one record in the IBM Content Navigator database and the **`"application.navigator"`** record is used to make the repository available.

We used:

`db2 =>` **`connect to ECM`**

`Database Connection Information`

`Database server        = DB2/LINUXX8664 11.5.7.0`

`SQL authorization ID   = DB2INST1`

`Local database alias   = ECM`

`db2 =>` **`SELECT * from ECMUSER.CONFIGURATION WHERE ID = 'repository.navigator.CMODDocs'`**

Field **ID:**

`repository.navigator.CMODDocs`

Field **ATTRIBUTES:**

**`searchMaxResults=1000`**`;cmisRepositoryID=*;statusDocCompoundDocument``=false;datetimeOp=;checkinAsMajorVersion=true;customProperties=[];showSecondInSearchView=false;odKeyringDBFile=;maxWorklists=2147483647;teamspaceDeleteTaskEnabled=false;p8DownloadRecord=false;teamspacesEnabled=false;databaseEncodingUTF8=false;directRetrieveEnabled=false;maxDownloadSize=0;conAnonymousUserId=;p8DownloadRecordIgnoreUsersIds=;redactionEnabled=false;idOp=;maxHits=1000;odSSL=false;boxCopyEnabled=false;floatOp=;approvalWorkflowEnabled=true;stringOp=;unifiedSearchesEnabled=false;conGlobalAdminUserIds=;includeWorkflowDefinition=false;version=2.0;objectOp=;conReviewAdminUserIds=;folderDefCols=;`**`serverName=DESKTOP-B3JB93R`**`;statusWorkItemSuspended=false;propertiesMapping=;timeoutInSeconds=60;teamspaceDisplayRecent=false;keepInAutoFolder=true;delimiterForOfficeProperty=\u003B;statusDocNotes=true;addAsMajorVersion=true;compoundDocumentsEnabled=false;enableWSI=false;statusDocHold=true;allClassesSearch=documentsIncludesNonFolders;worklistCountEnabled=false;auditHistoryEnabled=false;conReviewAdminGroupIds=;booleanOp=;restrictedSearchDocumentsType=true;useDefaultWorklistGroupingOrder=true;teamspaceOwnersModifyRoles=false;type=od;matchAll=true;conGlobalAdminGroupIds=;includeFormTemplate=false;restrictedSearchFoldersType=true;transformXMLFile=;docNameProp=;statusWorkItemCheckedOut=false;conActivityStreamEnable=false;statusDocCheckedOut=false;`**`name=CMOD-Docs`**`;maxInMemoryRetrieveSize=0;boxShareEnabled=false;isValid=true;includeMIMETypesInSearchResults=true;showDocLocation=false;includeAttrGroupInAttrDisplayName=true;statusDocUploading=false;cmisBindingType=AtomPub;conSeedlistEnable=false;actionListEnabled=false;redactionAllowMergeSplit=false;odKeyringStashFile=;`**`portNumber=1445`**`;folderSearchExpression=;connectionPoint=;teamspaceDisplayRecentValue=30;useSSO=false;docNamePropSetWithFileName=false;anonymousAccessEnabled=false;afp2pdfConfigFile=;searchDefCols=;syncRepositoryId=0;entryTemplatesEnabled=false;statusDocFavorite=true;usePartFileName=true;traceLevel=0;oAuthEnabled=false;integerOp=;statusWorkItemDeadline=false;burnPDFToPDF=true;officeOnlineEnabled=false;updateStorageCollection=false;conActivityStreamIgnoreUserIds=;isWarn=false;statusDocDeclaredRecord=false;statusWorkItemLocked=false;enableOnlyDocumentItemTypes=false;searchShowHiddenProperties=false;conActivityStreamIgnoreGroupIds=;simpleSearchMaxResults=5000;folderNameProp=;maxItemTypes=2147483647;statusDocBookmarks=false;syncEnabled=false;statusDocMinorVersions=false`

To build the **AFP2PDF** plugin, the documentation from the following **GitHub** link can be followed:

[https://github.com/ibm-ecm/ibm-content-navigator-samples](https://github.com/ibm-ecm/ibm-content-navigator-samples)

(See: [https://github.com/ibm-ecm/ibm-content-navigator-samples/tree/master/AFP2PDFPlusPlugin](https://github.com/ibm-ecm/ibm-content-navigator-samples/tree/master/AFP2PDFPlusPlugin))

On the **Linux** server, the **`AFPViewerPlugin.jar`** plugin and other viewer plugins are already compiled in the **`/opt/IBM/ECMClient/plugins`** directory, as shown in *[Figure 10.34](#c10.xhtml_fig10_34):*

![](images/Figure10.34.jpg)

**Figure 10.34:** The ***AFPViewerPlugin.jar***, the ***XMLViewerPlugin.jar*** and the ***ICCViewerPlugin.jar*** are available

The **`AFP2PDFPlusPlugin`** can be downloaded and built using the documentation in the text file:

`AFP2PDFPlusPlugin/README.md`

## Build the plugin

1.  Ensure the **Apache ANT** installer is installed, as shown in *[Figure 10.35](#c10.xhtml_fig10_35):*

    `yum install ant`

    ![](images/Figure10.35.jpg)

    **Figure 10.35:** The ***ant*** installer is installed on the ***Linux*** server

    (Alternatively, download the **Apache Ant** binary release from [http://ant.apache.org/bindownload.cgi](http://ant.apache.org/bindownload.cgi))

2.  `cd icn-plugins/AFP2PDFPlusPlugin`
3.  If required, copy all the dependencies into the **`lib`** directory:

    `navigatorAPI.jar`

    `j2ee.jar`

4.  **`cd icn-plugins/AFP2PDFPlusPlugin`**
5.  **`ant -f build.xml`**

The **`AFP2PDFPlusPlugin.jar`** is generated under **`icn-plugins/AFP2PDFPlusPlugin`**

See:

[https://cmod.wiki/dox/CMODv9.0/AFP2PDF-TransformGuide.pdf](https://cmod.wiki/dox/CMODv9.0/AFP2PDF-TransformGuide.pdf)

A new plugin can be added using the **IBM Content Navigator admin** administrator **Desktop,** as follows:

1.  The **`Plug-ins`** node is selected, and the **`New Plug-in`** command button is clicked, as highlighted in *[Figure 10.36](#c10.xhtml_fig10_36):*

    ![](images/Figure10.36.jpg)

    **Figure 10.36:** The ***Plug-ins*** node is selected and the ***New Plug-in*** command button is clicked

2.  The path to the **ICN** plugins is entered as **`/opt/IBM/ECMClient/plugins`** and the **`Load`** command button is selected after adding the required plugin .jar file, as shown in *[Figure 10.37](#c10.xhtml_fig10_37):*

    ![](images/Figure10.37.jpg)

    **Figure 10.37:** The path to the ***ICN*** plugins is entered as ***/opt/IBM/ECMClient/plugins*** and the ***Load*** command button is selected

3.  The highlighted **`AFPViewerPlugin.jar`** file is entered, and **`Load`** selected, as shown in *[Figure 10.38](#c10.xhtml_fig10_38):*

    ![](images/Figure10.38.jpg)

    **Figure 10.38:** The highlighted ***AFPViewerPlugin.jar*** file is entered and ***Load*** selected

4.  The version details of the plugin are displayed and the **`Save and Close`** command button is selected, as highlighted in *[Figure 10.39](#c10.xhtml_fig10_39):*

    ![](images/Figure10.39.jpg)

    **Figure 10.39:** The version details of the plugin are displayed and the ***Save and Close*** command is selected

5.  The new **`AFP Viewer`** plug-in is shown in the list and can be committed using the Refresh command to the **ICN** database, as shown in *[Figure 10.40](#c10.xhtml_fig10_40):*

    ![](images/Figure10.40.jpg)

    **Figure 10.40:** The new ***AFP Viewer*** ***Plug-in*** is shown and can be committed using the ***Refresh*** command

6.  The **Content Manager OnDemand** Desktop is selected for **`Edit`**, as shown in *[Figure 10.41](#c10.xhtml_fig10_41):*

    ![](images/Figure10.41.jpg)

    **Figure 10.41:** The ***Content Manager OnDemand*** Desktop is selected for ***Edit***

7.  The **`General`** tab of the **`Content Manager OnDemand`** Desktop is updated to select the **`Enable all deployed plug-ins for use with this desktop`** radio command and the **`Close`** command button is selected, as highlighted in *[Figure 10.42](#c10.xhtml_fig10_42):*

    ![](images/Figure10.42.jpg)

    **Figure 10.42:** The ***General*** tab of the ***Content Manager OnDemand*** Desktop is updated as highlighted.

8.  The **IBM Content Navigator WebSphere**, web application server is restarted in order to update the working system, by using the commands highlighted in *[Figure 10.43](#c10.xhtml_fig10_43):*

    `cd /opt/IBM/WebSphere/AppServer/profiles/AppSrv02/bin`

    `./stopServer.sh server1`

    `./startServer.sh server1`

    ![](images/Figure10.43.jpg)

    **Figure 10.43:** The ***IBM Content Navigator WebSphere***, web application server is restarted

# [Conclusion](#toc.xhtml_s144a)

In this chapter, we outlined the procedure required to create a repository for the **Linux** server version of **IBM Content Navigator** and demonstrated the browse access to the Folders on a **Windows CMOD** server from the **IBM Content Navigator** desktop created for **CMOD**.

We also covered the **Linux** **arsload** program and the switches that are used to load an example file to **CMOD** and the deployment procedures required for an AFP file viewer map for IBM Content Navigator.

In *[Chapter 11, Starting arssockd on the Linux Server](#c11.xhtml),* we will describe the network requirements to be checked for successfully running the **arssockd** program on a **Linux** server and the command parameters to use for running and debugging the program.

# [Points to Remember](#toc.xhtml_s145a)

*   If the full path names of the input files are not specified in the **`arsload`** program parameter file, the input files must be in the directory where the **`arsload`** program is started.
*   Each desktop can have only one viewer map assigned to it at any given time.
*   The viewer attribute is comma-separated if multiple viewer maps exist.

# [Multiple Choice Questions](#toc.xhtml_s146a)

1.  What is the general structure of the IBM Content Navigator **`CONFIGURATION`** table used to store state information?
    1.  `[COMPONENT_ID].navigator.[COMPONENT_TYPE]`
    2.  `[COMPONENT_TYPE].navigator.[COMPONENT_ID]`
    3.  `navigator.[COMPONENT_ID].[COMPONENT_TYPE]`
    4.  `[COMPONENT_ID].[COMPONENT_TYPE].navigator`
2.  Which command button is used to update the browser for the **CMOD-Docs** repository we created in this Chapter?
    1.  The **`Save and Close`** command button
    2.  The **`Save`** command button
    3.  The **`Refresh`** command button
    4.  The **`Close`** command button

# [Answers](#toc.xhtml_s147a)

1.  b
2.  c

# [Questions](#toc.xhtml_s148a)

1.  Describe the procedure required to ensure that the IBM Content Navigation web application can utilize the Java library files to support the **IBM CMOD** **ODWEK API**.
2.  How many mapping document MIME types are defined in the IBM Content Navigator default **Viewer Map** and how can this be verified?

# [Key Terms](#toc.xhtml_s149a)

*   **AFP**: Advanced Function Presentation (AFP) developed by IBM to build an entire page at a time before printing or storing the characters to a file.
*   **ANT**: Originally developed by the Apache Software Foundation as part of the Tomcat Web application, used as a Java based automation tool for building applications, ANT stands for “Another Neat Tool.”
*   **ICN:** The **IBM Content Navigator** web application for client document management of documents held in an **IBM FileNet P8 Content Engine** database.
*   **J2EE:** Stands for Java 2 Enterprise Edition and is a set of Java based application frameworks for managing **EJB** (Enterprise Java Beans), **JSP** (Java Server Pages), Java servlets and programs.
*   **ODWEK API:** OnDemand Web Enablement Kit Application Programmers Interface
*   **od:** Server type for IBM Content Manager OnDemand
*   **cm:** Server type for IBM Content Manager
*   **p8:** Server type for IBM FileNet P8 Content Engine
*   **cmis:** Server type for IBM ECM Content Management Interoperability Services (the open standard)

# [Further References](#toc.xhtml_s150a)

The following URL links provide additional reading for the subjects covered in this chapter, relating to the configuration and extension of the IBM Content Navigator for the support of an IBM Content Manager OnDemand Desktop.

*   [https://www.ibm.com/support/pages/how-configure-ibm-content-navigator-connect-ibm-content-manager-ondemand-105](https://www.ibm.com/support/pages/how-configure-ibm-content-navigator-connect-ibm-content-manager-ondemand-105)
*   [https://www.ibm.com/docs/en/content-navigator/3.0.15?topic=navigator-connecting-configuring-content-manager-ondemand-repositories](https://www.ibm.com/docs/en/content-navigator/3.0.15?topic=navigator-connecting-configuring-content-manager-ondemand-repositories)
*   [https://cmod.wiki/dox/CMODv9.0/Customizing_and_Extending_ICN.pdf](https://cmod.wiki/dox/CMODv9.0/Customizing_and_Extending_ICN.pdf)

    And for CMOD settings, see:

*   [https://www.ibm.com/support/pages/system/files/support/swg/ecmtech.nsf/0/dc59b36624f32aa385257d96007f12ed/$FILE/ICNcfg.pdf](https://www.ibm.com/support/pages/system/files/support/swg/ecmtech.nsf/0/dc59b36624f32aa385257d96007f12ed/$FILE/ICNcfg.pdf)

    For **GitHub** Plugins, see:

*   [https://github.com/ibm-ecm/ibm-content-navigator-samples](https://github.com/ibm-ecm/ibm-content-navigator-samples)

# [CHAPTER 11](#toc.xhtml_c11)

# [Starting arssockd on the Linux Server](#toc.xhtml_c11)

# [Introduction](#toc.xhtml_s151a)

This chapter describes the network requirements to be checked for successfully running the **`arssockd`** program on a **Linux** server and the command parameters for running and debugging the program.

We also cover the configuration of the network to support **IPv6** and changes to the **Linux** kernel network parameters to improve the performance of the **IBM Content Manager OnDemand** document loading services.

Finally, we cover the use of the **IBM OnDemand Full Text Search** service, which utilizes the open source, **Apache Lucene** system and the detailed use of the **`arsdb`** database configuration and maintenance program. We also cover the step-by-step procedure to create a second Linux **IBM CMOD** instance, **ARCHIVE2** using a second **Db2** instance owner, **archive2**.

# [Structure](#toc.xhtml_s152a)

In this chapter, we will discuss the following topics:

*   Starting the **`arssockd`** Program
*   Enabling **IPv6** on **RedHat Linux**
*   Checking to See if **IPv6** is Enabled
*   Checking and Changing the Port Range Limits
*   Linux Server Start up
*   Starting the **IBM OnDemand Full Text Search** Server
*   Running the **`arsdb`** Program and Switch use
    *   Using **`arsdb`** to Create a Second **IBM CMOD** Instance

# [Starting the arssockd Program](#toc.xhtml_s153a)

The **`arssockd`** program is the core program for running an **IBM Content Manager OnDemand** instance on a library server. All the supporting **IBM CMOD** programs, such as the **arsload** data load program and the **`arsadmin`** and **`arsmaint`** maintenance programs, will fail to run when the **`arssockd`** program is not running on the library server the client connections will fail to connect to the **IBM CMOD** instance.

The following commands set the installations for the **IBM OnDemand** systems to be owned by **archive** user with the group **`db2iadm1`**:

`[root@ECMUKDEMO22 ibm]#` **`cd /opt/ibm`**

`[root@ECMUKDEMO22 ibm]#` **`pwd`**

`/opt/ibm`

`[root@ECMUKDEMO22 ibm]#` **`ls`**

`db2  `**`odfts  ondemand`**

`[root@ECMUKDEMO22 ibm]#` **`chown archive:db2iadm1 -R odfts`**

`[root@ECMUKDEMO22 ibm]#` **`chown archive:db2iadm1 -R ondemand/`**

`[root@ECMUKDEMO22 ibm]#` **`ls -lsa`**

`total 4`

`0 drwxr-xr-x.  5 root    root       46 May 15 06:03 .`

`4 drwxrwxrwx.` `29 root    wasadm   4096 May 15 05:36 ..`

`0 drwxr-xr-x.  4 root    root       35 Mar 23 10:31 db2`

`0 drwxrwxr-x.  3` **`archive db2iadm1`**`19 May 15 06:04` **`odfts`**

`0 drwxrwxr-x.  3` **`archive db2iadm1`**`19 Mar 19 11:25` **`ondemand`**

The following command starts the **arssockd** object server and a listener on port **1445,** as shown in *[Figure 11.1](#c11.xhtml_fig11_1)*:

`[root@ECMUKDEMO22 bin]#` **`/opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S`**

`ARS0351I The arssockd instance ARCHIVE is ready`

`[root@ECMUKDEMO22 bin]#` **`ps -eaf|grep arsobjd`**

`[root@ECMUKDEMO22 bin]#` **`lsof -i:1445`**

![](images/Figure11.1.jpg)

**Figure 11.1:** The command which starts the ***`arssockd`*** object server and a listener on port ***`1445`***

The **`arsobjd`** program can be seen to be accepting **IBM CMOD** commands, following the run of the **`ps -eaf|grep arsobjd`** **Linux** command:

`archive   147316    9162  0 06:28 pts/2    00:00:00 arsobjd: (accepting)`

`root      147800   18122  0 06:35 pts/2    00:00:00 grep --color=auto arsobjd`

The **Linux** command can be run as follows to display the **1445** port status:

`[root@ECMUKDEMO22 bin]# [root@ECMUKDEMO22 bin]#` **`lsof -i :1445`**

`COMMAND     PID    USER   FD   TYPE  DEVICE SIZE/OFF NODE NAME`

`arssockd 146239 archive    4u  IPv6 1346468      0t0  TCP *:proxima-lm (LISTEN)`

`[root@ECMUKDEMO22 bin]#`

This status display shows that the **IPv6** network is being used, which we cover in detail in the next section.

Enabling IPv6 on RedHat Linux

To enable IPv6, we can run the command:

`sysctl -w net.ipv6.conf.all.disable_ipv6=0`

`net.ipv6.conf.all.disable_ipv6 = 0`

Then, we restart NetworkManager for the changes to apply.

`systemctl restart NetworkManager`

**Note**: *To permanently disable* ***IPv6****, you can edit the GRUB* ***`/etc/default/grub`*** *file.*

In the line, **`GRUB_CMDLINE_LINUX`**, append the argument **`ipv6.disable=1`** at the end of the line, as shown *in [Figure 11.2](#c11.xhtml_fig11_2):*

![](images/Figure11.2.jpg)

**Figure 11.2:** In the line, **GRUB_CMDLINE_LINUX**, append the argument **ipv6.disable=1**

`GRUB_TIMEOUT=5`

`GRUB_DISTRIBUTOR="$(sed 's, release .*$,,g' /etc/system-release)"`

`GRUB_DEFAULT=saved`

`GRUB_DISABLE_SUBMENU=true`

`GRUB_TERMINAL_OUTPUT="console"`

`GRUB_CMDLINE_LINUX="crashkernel=auto resume=UUID=660f7340-01b5-4c0a-8321-45527b38500b rhgb quiet"` **`ipv6.disable=1`**

`GRUB_DISABLE_RECOVERY="true"`

`GRUB_ENABLE_BLSCFG=true`

# [Checking to See if IPv6 is Enabled](#toc.xhtml_s154a)

The following command can be used to display the system **`ifcfg-ens160`** file contents in order to check the **`IPv6`** enablement status:

`[root@ECMUKDEMO22 bin]#` **`cat /etc/sysconfig/network-scripts/ifcfg-ens160`**

`TYPE=Ethernet`

`PROXY_METHOD=none`

`BROWSER_ONLY=no`

`BOOTPROTO=dhcp`

`DEFROUTE=yes`

`IPV4_FAILURE_FATAL=no`

**`IPV6INIT=yes`**

**`IPV6_AUTOCONF=yes`**

**`IPV6_DEFROUTE=yes`**

**`IPV6_FAILURE_FATAL=no`**

**`IPV6_ADDR_GEN_MODE=stable-privacy`**

`NAME=ens160`

`UUID=343f59ed-dc34-464e-9cd8-682adb59fa2c`

`DEVICE=ens160`

`ONBOOT=yes`

If required, the **IPv6** network system can be checked to view the disable flag settings, as shown in *[Figure 11.3](#c11.xhtml_fig11_3):*

`sysctl -a | grep ipv6.*disable`

![](images/Figure11.3.jpg)

**Figure 11.3:** If required, the ***IPv6*** network system can be checked to view the disable flag settings

The value 0, in the list in *[Figure 11.3](#c11.xhtml_fig11_3)*, indicates that **IPv6** is active. (A value of 1 shows that **IPv6** is disabled).

The following command is used to check the **IPv6** network addresses used by the **Linux** server system:

`[root@ECMUKDEMO22 bin]#` **`ip -6 add`**

`1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 state UNKNOWN qlen 1000`

`inet6 ::1/128 scope host`

`valid_lft forever preferred_lft forever`

`2: ens160: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 state UP qlen 1000`

`inet6 fe80::5706:6437:5e47:d334/64 scope link noprefixroute`

`valid_lft forever preferred_lft forever`

# [Checking and Changing the Port Range Limits](#toc.xhtml_s155a)

IBM recommend that the **IBM Content Manager OnDemand** port ranges should be increased to improve the performance of the system.

The following command is used to display the current range set for the **Linux** server:

`[archive@ECMUKDEMO22 bin]$` **`sysctl net.ipv4.ip_local_port_range`**

`net.ipv4.ip_local_port_range = 32768 60999`

`[archive@ECMUKDEMO22 bin]$`

To increase the maximum number of ports available to applications, change the value of the kernel parameter from its default of **28232** to a higher wider range, for example, **1024 to 65535.** To edit the **`sysctl net.ipv4.ip_local_port_range`** kernel parameter file, we can use the **Linux** **vi** editor on some systems, as follows:

`vi /proc/sys/net/ipv4/ip_local_port_range`

On the RedHat RHEL 8.8 system, we have the following error as shown in *[Figure 11.4](#c11.xhtml_fig11_4):*

![](images/Figure11.4.jpg)

**Figure 11.4:** The RedHat RHEL 8.8 system gives an error when using the vi editor

In this case, if the **`ip_local_port_range`** is set in the file **`/etc/sysctl.conf`**, the value of the parameter is changed at system startup.

So, enter the line:

`net.ipv4.ip_local_port_range = 1024 65535`

# [Linux Server Start up](#toc.xhtml_s156a)

The **archive** database instance user is logged into, and the **archive** database and **ARCHIVE** **CMOD** instance are loaded using the following commands, as shown in *[Figure 11.5](#c11.xhtml_fig11_5):*

![](images/Figure11.5.jpg)

**Figure 11.5:** The ***archive*** user is logged into and the ***archive*** database and ***ARCHIVE*** ***CMOD*** instance is loaded

`[root@ECMUKDEMO22 ~]#` **`su - archive`**

`Last login: Wed Apr 10 05:37:42 PDT 2024 on pts/0`

`[archive@ECMUKDEMO22 ~]$` **`db2 start database manager`**

`SQL1026N  The database manager is already active.`

`[archive@ECMUKDEMO22 ~]$` **`db2 activate database archive`**

`DB20000I  The ACTIVATE DATABASE command completed successfully.`

`[archive@ECMUKDEMO22 ~]$` **`/opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S`**

`[archive@ECMUKDEMO22 ~]$ ARS0351I The arssockd instance ARCHIVE is ready`

Then use the **`exit`** command to return back to the root user’s command line to confirm the port **1445** attachment is actively listening using the **`arssockd`** program:

`[archive@ECMUKDEMO22 ~]$` **`exit`**

`logout`

`[root@ECMUKDEMO22 ~]#`

`[root@ECMUKDEMO22 ~]#` **`ps -eaf|grep arsobjd`**

`archive     4694    3615  0 12:34 pts/0    00:00:00 arsobjd: (accepting)`

`root        4876    4835  0 12:36 pts/1    00:00:00 grep --color=auto arsobjd`

`[root@ECMUKDEMO22 ~]#` **`lsof -i :1445`**

`COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME`

`arssockd 4694 archive    4u  IPv6  69244      0t0  TCP *:proxima-lm (LISTEN)`

***Note:*** *If you get the error message:*

***`ARS1106E Connection cannot be established for the >LibSrvr< server`***

*Then the following link instructions can correct this:*

*[https://www.ibm.com/support/pages/content-manager-ondemand-arsload-servicedaemon-might-fail-loading-all-data](https://www.ibm.com/support/pages/content-manager-ondemand-arsload-servicedaemon-might-fail-loading-all-data)*.

# [Starting the IBM OnDemand Full Text Search Server](#toc.xhtml_s157a)

The **IBM OnDemand Full Text Search** server can be used to add the capability of using text to search for a selection of **IBM OnDemand** documents.

The introduction of a **Full Text Search** capability within **IBM Content Manager OnDemand** (CMOD) (in versions 9.5, 10.1, and 10.5) is based on an install wrapper of the IBM ECM Text Search installer which is based on the **Apache Lucene** project (used by IBM for **Db2**, **Content Manager** and **FileNet**). Previously, the only available **Full Text Search**

(**FTS**) feature required the use of the **IBM CMOD** server-based text search functionality. The previous **Full Text Search** function could only deal with **Line**, **SCS**, **PDF**, **Advanced Function Presentation (AFP)** and **SCS-Extended** documents and was also restricted to finding results for the query string with no “wild” character, limiting the search to exact matches and could only run on the same machine as the **IBM CMOD** server. The full pdf document describing this new feature can be found using the following link:

[https://www.ibm.com/support/pages/system/files/inline-files/Best%20practices%20for%20Using%20Full%20Text%20Searching%20with%20Content%20Manager%20OnDemand-6-18-2020.pdf](https://www.ibm.com/support/pages/system/files/inline-files/Best%20practices%20for%20Using%20Full%20Text%20Searching%20with%20Content%20Manager%20OnDemand-6-18-2020.pdf)

In the preceding note, the command for the check is incorrect; it is listed as

`configTool.sh list –system -showAdvanced`

(The **`-system`** parameter with a leading hyphen character should be **`-system`** with a minus.)

This is run as follows:

`[archive@ECMUKDEMO22 bin]$` **`./configTool.sh list -system -showAdvanced`**

`Usage:`

`configTool list -system [-details] [-showAdvanced] [-<parameter name>]`

`Prints all system-level parameters and their current values.`

`-details`

`Prints detailed information about each parameter, including:`

`description, default value, type, modifiable (true|false)`

`-showAdvanced`

`Prints information about advanced configuration parameters.`

`-<parameter name>`

`Prints detailed information about the specified parameter.`

`configTool list -collectionName <collection> [-details] [-<parameter name>]`

`Prints all collection-level parameters and their current values.`

`-collectionName <collection>`

`Specifies the collection name.` `You can specify the fully qualified`

`path to the collection.`

`-details`

`Prints detailed information about each parameter, including:`

`description, default value, type, modifiable (true|false)`

`-<parameter name>`

`Prints detailed information about the specified parameter.`

`[archive@ECMUKDEMO22 bin]$ ./configTool.sh list -system -showAdvanced`

`NOTE: The available settings and default values listed might differ for your product.`

`Check your product documentation for more information.`

`server:`

`acceptorThreads: 300`

`backLog: 1024`

`blockCacheBlockSizeKB: 4`

`blockCacheSizeMB: 400`

`collectionBaseFolders: *`

`concatenateSmallFiles: true`

`concurrentSearchPoolSize: 16`

`configPath:` **`/opt/ibm/odfts/V10.5/config`**

`containerFileTimeoutMin: 65`

`debugMaxDocSnippetLength: 1000`

`defaultDataDirectory:` **`/opt/ibm/odfts/V10.5/config/collections`**

`docQueueDrainTimeInMillis: 5000`

`documentBatchMemorySize: 1M`

`documentDeleteBatchSize: 100`

`documentQueueSize: -1`

`documentTimeout: 2100`

`enableAsciiFoldingFilter: false`

`enableContinuationQueryOptimization: true`

`enableIndexerLogging: false`

`enablePriorityStrategy: true`

`errorOnClientVersionValidation: true`

`flushToDiskThreshold: 10`

`iPV6: false`

`idleBatchTimeoutMin: 80`

`idleCommitPointTimeoutMS: 300000`

`idleSearchableTimeoutMS: 600000`

`indexingChunkSize: 1M`

`indexingProgressWarningTimeMin: 15`

`indexingTrace: false`

`inputQueueMemorySize: 150M`

`installPath: /opt/ibm/odfts/V10.5`

`keyStoreName: /opt/ibm/odfts/V10.5/bin/ECMTSKeystore`

`keyStoreType: jks`

`logFolder: /opt/ibm/odfts/V10.5/log`

`logLevel: INFO`

`maxConcurrentIndexingCollections: 16`

`maxConcurrentSearchTaskAllocationDelayMS: 25000`

`maxDocumentSizeBytes: 120000000`

`maxExtractedDocumentSizeBytes: 1000000000`

`maxHeapSize: 4000M`

`maxIdleTimeMs: 2000000`

`maxIndexWriteLockMin: 60`

`maxMergeLoadForPurgingDeletions: 3`

`maxSortedResultsAllowed: 10000`

`maxXmlTagsPerMB: 15000`

`monitorQueuesFrequency: 10`

`numberOfIndexerThreads: 8`

`numberOfPreprocessingThreads: 8`

`numberOfSearchables: 12`

`numberOfTokenizers: 20`

`optimizeHighlightedQueryParsing: false`

`outputQueueMemorySize: 150M`

`outsideInMaxProcessableDocuments: 2000`

`pluginsPath: /opt/ibm/odfts/V10.5/plugins`

`port: 8191`

`queryCacheSizeMB: 200`

`queryExpansionLimit: 10000`

`queryHistoryMaxItems: 10000`

`queuePriorityCollectionTimeoutMS: 300000`

`rangeQueryExpansionLimit: 100000`

`removeStopwordsFromBooleanQuery: false`

`searchableRefreshRateMS: 60000`

`searchablesMaintenancePulseMS: 30000`

`securePort: 0`

`stellentEnabled: true`

`stellentPath:` **`/opt/ibm/odfts/V10.5/stellent.linux64`**

`stellentVersion: 8.5.4`

`storeErrorInIndex: false`

`supportedLanguages:`

`Afrikaans (af)`

`Arabic (ar)`

`Catalan (ca)`

`Czech (cs)`

`Danish (da)`

`German (de)`

`Greek (el)`

`English (en)`

`Spanish (es)`

`Finnish (fi)`

`French (fr)`

`Hebrew (he)`

`Italian (it)`

`Japanese (ja)`

`Korean (ko)`

`Norwegian Bokmål (nb)`

`Dutch (nl)`

`Norwegian Nynorsk (nn)`

`Polish (pl)`

`Portuguese (pt)`

`Russian (ru)`

`Swedish (sv)`

`Turkish (tr)`

`Chinese (zh)`

`Generic (generic)`

`Unknown (unknown)`

`tempDirectory:`

`termInfosIndexDivisorCollectionSizeGB: 25`

`textExtractorInitPoolSize: 4`

`textExtractorMaxPoolSize: -1`

`textExtractorTimeoutMS: 900000`

`transformationRetries: 2`

`version: 5.5.4`

`waitOnIdleCollectionSec: 30`

`index:`

`bufferSize: 25`

`defaultConstructorName:`

`directoryTypeForSearch:`

`enableConcurrentSearchOptimization: true`

`enableHebrewMorphologicalDictionary: true`

`enablePunctuationSearch: true`

`enableXMLDateSearch: true`

`enableXMLNameSpaceSearch: true`

`forceNgramForCJK: true`

`indexAllLemmas: true`

`indexUpdateBitSizeMB: 12`

`maxBinaryTextSize: 60000000`

`maxBufferedDocs: 1000000`

`maxConcurrentSearchThreadsPerQuery: 4`

`maxMergeCount: 10`

`maxMergeDocs: 5000000`

`maxMergeMB: 4000`

`maxMergeThreadCount: 5`

`maxTextSize: 60000000`

`maxXmlTextSize: 60000000`

`mergeFactor: 10`

`minDeletePercentageForMergeDeletes: 30`

`minMergeMB: 1.6`

`sweetSpotLength: 50`

`sweetSpotMaxValue: 0.5`

`sweetSpotMinValue: 0.02`

`useCompoundFile: true`

`useQueryCache: true`

`useSynonyms: true`

`query:`

`enableCaseInsensitiveEstimate: false`

`enableQueryLanguageExpansion: true`

`estimateAccuracyThreshold: 100`

`maxQueryCharacterLength: 262144`

`queryTimeout: 0`

`[archive@ECMUKDEMO22 bin]$`

The IBM OnDemand full text search server can be started on Linux as follows:

`[archive@ECMUKDEMO22 bin]$` **`cd /opt/ibm/odfts/V10.5/bin`**

`[archive@ECMUKDEMO22 bin]$` **`ls`**

`adminTool.sh   dumpIndex.sh   SearchCollection.sh  shutdown.sh  stopwordTool.sh`

`configTool.sh  ECMTSKeystore  setup.sh             startup.sh   synonymTool.sh`

`[archive@ECMUKDEMO22 bin]$` **`./setup.sh`**

`[archive@ECMUKDEMO22 bin]$` **`./startup.sh`**

`INFO: To improve indexing performance, the text search startup script changed the value of the 'number of files per process' system setting (ulimit -n) to 65536.`

`System Manager: Starting PCH Listener...`

`System Manager: PCH Listener started.`

`System Manager: Registering my port [`**`41741`**`] with master PCH Listener on [`**`32775`**`]`

`IQQG0337I The server [version: 5.5.4.0-1.1-6219] started successfully.` `The server is listening on port` **`8191`**`.`

`[archive@ECMUKDEMO22 bin]$` **`pwd`**

**`/opt/ibm/odfts/V10.5/bin`**

`[archive@ECMUKDEMO22 bin]$`

**Note:** *The* ***`./setup.sh`*** *shell script sets up the environment variables, so is run each time.*

# [Running the `arsdb` Program and Switch Use](#toc.xhtml_s158a)

The **`arsdb`** program performs database-specific tasks for **IBM CMOD** Servers. This includes installation, maintenance, upgrades, and the tasks for importing and exporting database tables.

The link [https://www.cmod.wiki/index.php/arsdb](https://www.cmod.wiki/index.php/arsdb) provides an overview of the switches which can be used.

The **`arsdb`** program is used to create the initial database for **IBM OnDemand**’s internal tables for the **IBM CMOD** table fields, and field indexes, using the Linux command, logged in as the database user:

`./arsdb -I archive -cv`

# [Using `arsdb` to Create a Second IBM CMOD Instance](#toc.xhtml_s159a)

This command can be repeated to create a second database instance. Before you create the second **ARCHIVE2** instance, you must have completed the following tasks:

(Refer to the link: [https://www.ibm.com/docs/en/cmofz/10.5.0?topic=instances-configuring-multiple](https://www.ibm.com/docs/en/cmofz/10.5.0?topic=instances-configuring-multiple))

1.  Installed and configured the database software (**Db2** or Oracle) and created an **ARCHIVE2** database instance for **IBM Content Manager OnDemand**.
2.  Installed and configured the **IBM Content Manager OnDemand** software for the second instance, including the following files:

    `ars.ini`

    `ars.cfg`

    `ars.dbfs`

    `ars.cache`

    The **`ars.ini`** file is the only shared file for all the instances, so we need to insert the following:

    **`[@SRV@_ARCHIVE2]`**

    **`HOST=ECMUKDEMO22`**

    **`PROTOCOL=2`**

    **`PORT=1444`**

    **`SRVR_INSTANCE=ARCHIVE2`**

    **`SRVR_INSTANCE_OWNER=archive2`**

    **`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.cfg`**

    **`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.dbfs`**

    **`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.cache`**

    **`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.archive2.stash`**

    `[@SRV@_DD]`

    `PROTOCOL=1`

3.  Next, we must copy the first **ARCHIVE** instance **`ars.cfg`** file to **`ars.archive2.cfg`**. We have to edit the new **`ars.archive2.cfg`** server configuration file with the **vi** text editor `[root@ECMUKDEMO22 config]#` **`pwd`**

    `/opt/ibm/ondemand/V10.5/config`

    `[root@ECMUKDEMO22 config]#` **`cp ars.cfg ars.archive2.cfg`**

    `[root@ECMUKDEMO22 config]#` **`vi ars.archive2.cfg`**

    to give the sections with content changed (**in bold**) as follows:

    `#`

    **`#       ars.archive2.cfg`** `- OnDemand Configuration File`

    `#`

    `#  5622-662 (C) COPYRIGHT IBM CORPORATION 2020`

    `#  All Rights Reserved`

    `#######################`

    `# OnDemand Parameters #`

    `#######################`

    `#`

    `ARS_SRVR=`**`ECMUKDEMO22`**

    `ARS_LOCAL_SRVR=`**`ECMUKDEMO22`**

    `ARS_SUPPORT_HOLD=1`

    `ARS_SUPPORT_CFSOD=1`

    `ARS_ORIGINAL_CODEPAGE=`**`1208`**

    `#`

    `# Number of Database SubServers (Library Server Only)`

    **`#   0         - Defaults to connection per client`**

    `#   Otherwise - The number of Database SubServers to handle connections`

    `#               to the database (minimum of 2)`

    `#`

    `ARS_NUM_DBSRVR=0`

    `DB2INSTANCE=`**`archive2`**

    `#`

    `ARS_DB_IMPORT=0`

    `ARSSOCK=debug`

    `#`

    `# Used to specify if the database supports partitioning (Library Server Only)`

    `#   Blank (No partition support)`

    `#`

    `ARS_DB_PARTITION=`

    `########################################`

    `# DB2 Parameters (Library Server Only) #`

    `########################################`

    **`DB2INSTANCE=archive2`**

    `#`

    `# These parameters used only during database creation`

    `#`

    `ARS_DB2_DATABASE_PATH=/`**`arsdb2`**

    `ARS_DB2_PRIMARY_LOGPATH=/`**`arsdb2`**`_primarylog`

    `ARS_DB2_ARCHIVE_LOGPATH=/`**`arsdb2`**`_archivelog`

    `ARS_DB2_LOGFILE_SIZE=1000`

    `ARS_DB2_LOG_NUMBER=40`

4.  Next, we copy the **`ars.cache file`** to a new **`ars.archive2.cache`** file and edit this.

    `[root@ECMUKDEMO22 config]#` **`cp ars.cache ars.archive2.cache`**

    `[root@ECMUKDEMO22 config]#` **`vi ars.archive2.cache`**

    The cache directory in the **`ars.archive2.cache`** file, is updated as follows:

    `/arscache/cache2`

5.  The new cache folder is created initially, owned by **root**, as follows:

    `mkdir /arscache/cache2`

    `chmod 700 /arscache/cache2`

    `chmod g-s /arscache/cache2`

    `chown archive2:db2iadm1 /arscache/cache2 -R`

    `chmod 775 /arscache -R`

6.  The **`ars.dbfs`** file is copied to the **`ars.archive2.dbfs`** file:

    `[root@ECMUKDEMO22 config]#` **`cp ars.dbfs ars.archive2.dbfs`**

7.  Next, we run the following programs:

    As described in *[Chapter 2, Installing CMOD on Linux Systems](#c02.xhtml),* on Linux we install a new DB2 database instance for the **archive2** user, as follows.

    The IBM DB2 **`./db2setup`** installer is called, as was shown in *[Chapter 2](#c02.xhtml), [Figure 2.118](#c02.xhtml_fig2_118)*, using the Linux commands as follows:

    `cd /opt/IBM/DB2/server_dec`

    `export DISPLAY=:0`

    `echo $DISPLAY`

    `./db2setup`

8.  We then follow the same **Db2** installation steps for **archive2**, as we used in *[Chapter 2, Installing CMOD on Linux Systems](#c02.xhtml)* for the **archive** instance, as shown in *[Figure 11.6](#c11.xhtml_fig11_6).*

    ![](images/Figure11.6.jpg)

    **Figure 11.6:** We then follow the same ***Db2*** installation steps for ***archive2***

    The **`archive2`** fence user was set to the existing **`db2fenc1`** user.

    **Note**: *The fenced user is used to run user defined functions and stored procedures to protect Db2 from malware and restricts access outside of the memory address space used by the Db2 database. The default user is* ***`db2fenc1`*** *and the default group is* ***`db2fadm1`****.*

    After using the default Fenced user, **`db2fenc1`**`,` we see the summary page for the second instance installation, as shown in *[Figure 11.7](#c11.xhtml_fig11_7):*

    ![](images/Figure11.7..jpg)

    **Figure 11.7:** After using the default Fenced user, db2fenc1, we see the summary page for the installation

    We can scroll down the **`View Full Summary`** command button pop-up summary window, as shown in *[Figure 11.8](#c11.xhtml_fig11_8):*

    ![](images/Figure11.8.jpg)

    **Figure 11.8:** The ***View Full Summary*** command button with pop-up summary window

    After clicking on the **`Finish`** command, we are asked if we are happy to overwrite the response file which was responded with **`Yes`**.

    The status of the second **archive2** Db2 database instance is shown in the **`Setup`** **`Complete`** window, as shown in *[Figure 11.9](#c11.xhtml_fig11_9)***:**

    ![](images/Figure11.9.jpg)

    **Figure 11.9:** After the ***Finish*** command the status of the second ***archive2*** Db2 database instance is shown

    **Note**: *If you get the following error message:*

    ***`"Instance setup and configuration will be disabled.`***

    ***`DBI1004W  /usr/lib/libdb2.so detected.` `This DB2 copy may encounter problems loading its libraries."`***

    *Then, you have to run the* ***`db2rmln`*** *command to remove* ***symlinks*** *from the installation path where the* ***`db2ln`*** *command was run, and then restart the install.*

    *On our server, this was fixed by running the program as follows:*

    ***`/opt/ibm/db2/V11.5_01/cfg/db2rmln`***

9.  `The post-installation steps are recommended to be run as follows and as shown in` *[Figure 11.10](#c11.xhtml_fig11_10)*`:`

    **`"Required steps:`**

    `In order to start using DB2 you need to logon using a valid user ID such as the DB2 instance owner's ID "`**`archive2`**`".`

    `You can connect to the DB2 instance "`**`archive2`**`" using the port number "`**`25012`**`".` `Record it for future reference.`

    **`Optional steps:`**

    `To validate your installation files, instance, and database functionality, run the Validation Tool,` **`/opt/ibm/db2/V11.5_02/bin/db2val`**`.` `For more information, see "db2val" in the DB2 Information Center.`

    ![](images/Figure11.10..jpg)

    **Figure 11.10:** The post-installation steps are recommended to be run as shown here

    `Open First Steps by running "`**`db2fs`**`" using a valid user ID such as the DB2 instance owner's ID.` `You will need to have DISPLAY set and a supported web browser in the path of this user ID."`

    The output from the **`db2val`** program is shown in *[Figure 11.11](#c11.xhtml_fig11_11)*:

    ![](images/Figure11.11.jpg)

    **Figure 11.11:** The output from the ***db2val*** program

10.  Run the following commands from root:

    `chown archive2:db2iadm1 /opt/ibm/db2/V11.5_02/lib64/gskit`

    `And create the symbolic links to Db2:`

    `/opt/ibm/db2/V11.5_02/cfg/db2ln`

11.  Create the database files as the root user:

    `mkdir /arsdb2`

    `mkdir /arsdb2_primarylog`

    `mkdir /arsdb2_archivelog`

    `chown archive2:db2iadm1 /arsdb2_primarylog`

    `chown archive2:db2iadm1 /arsdb2_archivelog`

    `chown archive2:db2iadm1 /arsdb2`

12.  Run the **`arsdb`** job to create an **IBM CMOD** database and tables for the instance as the **`archive2`** user, as shown in *[Figure 11.12](#c11.xhtml_fig11_12):*

    ![](images/Figure11.12.jpg)

    **Figure 11.12:** Run the ***arsdb*** job to create an IBM CMOD database and tables for the instance

    `su - archive2`

    `/opt/ibm/ondemand/V10.5/bin/arsdb -I archive2 -cv`

    We should see the console log output as follows:

    `ARS4018I Creating the DB2 ARCHIVE2 database`

    `ARS4119I Specify the type of archive logging to be used:`

    `Do you wish to use DISK(1), TSM(2), or CIRCULAR(3)?`

    `Please specify 1, 2, or 3:1`

    `ARS4062I Database created with territory 'US', code page '1208', code set 'UTF-8' and collating sequence ''`

    `ARS4068I Updating the ARCHIVE2 database configuration`

    `ARS4073I Deactivating database ARCHIVE2`

    `ARS4071I Backing up the ARCHIVE2 database so that the updates can take effect`

    `ARS4057I Timestamp for backup image is: 20240626080535`

    `ARS4026I Creating table archive2.arsag`

    `ARS4034I Creating index archive2.arsag_name_idx`

    `ARS4034I Creating index archive2.arsag_agid_idx`

    `ARS4042I Updating runstat statistics for table archive2.arsag`

    `Etc….`

    `ARS4026I Creating table archive2.arsusrgrp`

    `ARS4034I Creating index archive2.arsusrgrp_idx`

    `ARS4034I Creating index archive2.arsusrgrp_idx2`

    `ARS4042I Updating runstat statistics for table archive2.arsusrgrp`

    `ARS4026I Creating table archive2.arsusrgrpid`

    `ARS4034I Creating index archive2.arsusrgrpid_idx`

    `ARS4042I Updating runstat statistics for table archive2.arsusrgrpid`

    `[archive2@ECMUKDEMO22 ~]$`

13.  The firewall must be opened for the ports **`1444`** and the **archive2** database port **`25012`**, using the commands:

    `firewall-cmd --zone=public --permanent --add-port=1444/tcp`

    `firewall-cmd --zone=public --permanent --add-port=25012/tcp`

    `firewall-cmd –reload`

14.  The startup of **`archive2`** runs without error using the command:

    `/opt/ibm/ondemand/V10.5/bin/arssockd -I archive2 -S`

    and the memory shows the two instances are controlled by the **`arsobjd`** object server programs for **IBM CMOD** **10.5**, as shown in *[Figure 11.13](#c11.xhtml_fig11_13):*

    ![](images/Figure11.13.jpg)

    **Figure 11.13:** The startup now shows that ***archive2*** runs without error for ***IBM CMOD***

    See “Adding an instance - IBM Documentation”:

    **[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=instance-creating-database](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=instance-creating-database)**

    **Note**: *After the installation is complete, the internal* ***System Log****,* ***System Load****, and* ***System Migration*** *IBM* ***CMOD*** ***Application Groups*** *are built automatically using the* ***arssyscr*** *command.*

The **IBM CMOD** database routine maintenance to ensure performance and reliability is performed using the following options:

1.  `Run Maintenance and Statistics for the OnDemand system tables`

    `/opt/ibm/ondemand/V10.5/bin/arsdb -I archive2 -msv`

    Gives console output:

    `ARS4040I Reorganizing table archive2.arsag`

    `ARS4042I Updating runstat statistics for table archive2.arsag`

    `ARS4040I Reorganizing table archive2.arsag2fol`

    `ARS4042I Updating runstat statistics for table archive2.arsag2fol`

    `ARS4040I Reorganizing table archive2.arsagfld`

    `ARS4042I Updating runstat statistics for table archive2.arsagfld`

    `Etc..`

    `ARS4042I Updating runstat statistics for table archive2.arsuser`

    `ARS4040I Reorganizing table archive2.arsusrgrp`

    `ARS4042I Updating runstat statistics for table archive2.arsusrgrp`

    `ARS4040I Reorganizing table archive2.arsusrgrpid`

    `ARS4042I Updating runstat statistics for table archive2.arsusrgrpid`

    `[archive2@ECMUKDEMO22 bin]$`

2.  Regular backups, for example, for online backups, use:

    `/opt/ibm/ondemand/V10.5/bin/arsdb -I archive2 -z` *[Device]*`-v`

3.  And for offline backups, use

    `/opt/ibm/ondemand/V10.5/bin/arsdb -I archive2 -yv`

The command **`/opt/ibm/ondemand/V10.5/bin/arsdb`** on its own gives the following help list:

`[archive2@ECMUKDEMO22 ~]$` **`/opt/ibm/ondemand/V10.5/bin/arsdb`**

`ARS4010I Usage: arsdb [options] [table(s)]`

`Version:  10.5.0.7`

`-c (DB2/MSSQL) Create the OnDemand database`

`-d Drop the OnDemand system tables`

`-e Drop the OnDemand system indexes`

`-f Ignore DB Failures`

`-F Do not prompt`

`-g (DB2/MSSQL) Start the OnDemand database`

`-h (DB2/MSSQL) Stop the OnDemand database`

`-i Import data to the OnDemand system tables`

`-I <od_inst> OnDemand instance name`

`-k (DB2) Activate the OnDemand database`

`-m (DB2/MSSQL) Run Maintenance for the OnDemand system tables`

`-o <filename> Output file name`

`-O OnDemand Distribution Facility (ODF)`

`-r Create indexes for the OnDemand system tables`

`-s Run statistics on the OnDemand system tables`

`-t Create the OnDemand system tables`

`-u Update the OnDemand system tables`

`-v Verbose`

`-x Export data from the OnDemand system tables`

`-y <device> (DB2) Backup the OnDemand database offline to the device`

`(MSSQL) Complete OnDemand database backup to the device`

`-Y <device> (DB2) Backup the OnDemand database tablespace(s) offline to the device`

`-X (DB2 only) If -Y or -Z, don't backup tablespace USERSPACE1`

`-z <device> (DB2) Backup the OnDemand database online to the device`

`(MSSQL) Differential OnDemand database backup to the device`

`-Z <device> (DB2) Backup the OnDemand database tablespace(s) online to the device`

`-1 <trace_file> Trace file`

# [Conclusion](#toc.xhtml_s160a)

We covered the use of the **IBM OnDemand Full Text Search** service, which utilized the open source, **Apache Lucene** system and the detailed use of the **`arsdb`** database configuration and maintenance program. Finally, we also covered the step-by-step procedure to create a second Linux **IBM CMOD** database instance, **ARCHIVE2** using a second **Db2** instance owner, **archive2**.

In the next chapter, *Configuring the arsload Program*, the details of the use of the **`arsload`** program parameter settings is covered for creating an **Index**, the use of the **ODWEK**, **Web Enablement Kit** the setting up of **Test Data** for the **Windows ARSLOAD** program and the addition, update, and export of **IBM CMOD Application Groups**.

# [Points to Remember](#toc.xhtml_s161a)

The points to remember are as follows:

*   For a previous installation of the **IBM Content Manager OnDemand Full Text Search** feature, the new version’s installation will become a new install and no data will be migrated from the previous version. Do not uninstall the previous version or begin indexing to the new version before taking the steps described in support item 6588065\.

    See: [https://www.ibm.com/support/pages/node/6588065](https://www.ibm.com/support/pages/node/6588065)

*   If you get the following error message:

    `"`**`Instance setup and configuration will be disabled.`**

    **`DBI1004W  /usr/lib/libdb2.so detected.` `This DB2 copy may encounter problems loading its libraries.`**`"`

    then you have to run the **`db2rmln`** command to remove symlinks from the installation path where the **`db2ln`** command was originally run, and then restart the install.

*   To permanently disable **IPv6**, you can edit the GRUB **`/etc/default/grub`** file.
*   If you get the error message:

    `ARS1106E Connection cannot be established for the >LibSrvr< server`

    Then the following link instructions can correct this:

    [https://www.ibm.com/support/pages/content-manager-ondemand-arsload-servicedaemon-might-fail-loading-all-data](https://www.ibm.com/support/pages/content-manager-ondemand-arsload-servicedaemon-might-fail-loading-all-data)

# [Multiple Choice Questions](#toc.xhtml_s162a)

1.  Which of the following programs is used to start the **IBM CMOD** object server and a listener?
    1.  `./arsdb`
    2.  `./arssockd`
    3.  `./arssyscr`
    4.  `./db2setup`
2.  Which **Linux** command is used to open the **Db2** database port for the second **Linux** **ARCHIVE2 IBM CMOD** database?
    1.  `firewall-cmd --zone=public --permanent --add-port=1444/tcp`
    2.  `firewall-cmd --zone=public --permanent --add-port=25011/tcp`
    3.  `firewall-cmd --zone=public --permanent --add-port=1445/tcp`
    4.  `firewall-cmd --zone=public --permanent --add-port=25012/tcp`

# [Answers](#toc.xhtml_s163a)

1.  b
2.  d

# [Questions](#toc.xhtml_s164a)

1.  What command would you use if you had to correct the error:

    **`DBI1004W  /usr/lib/libdb2.so detected.`**

2.  What procedure would you follow to rectify the error on the **IBM CMOD Linux** server:

    **`ARS1106E Connection cannot be established for the >LibSrvr< server`**

# [Key Terms](#toc.xhtml_s165a)

*   **IPv6**: Internet Protocol version 6 of the Internet Protocol and the next release and update to **IPv4**, the fourth version. It has a similar use as **IPv4**, but it uses a **128-bit** IP address, rather than the **32-bit** IP address used by **IPv4**, which gives it 10^(28) times more addresses than **IPv4**, so around 10^(28) x 4.29 billion addresses!
*   **AFP**: IBM’s Advanced Function Presentation format for files, similar to PDF, but designed to simulate printed pages directly from a printer. Used by **IBM i**, there is a full description downloadable from the link: [https://www.ibm.com/docs/en/ssw_ibm_i_72/rzau6/rzau6pdf.pdf](https://www.ibm.com/docs/en/ssw_ibm_i_72/rzau6/rzau6pdf.pdf)
*   **SCS**: The SCS datastream is a sequential stream format used with some IBM line printers, described in the link:

    [https://www.ibm.com/docs/en/personal-communications/13.0?topic=support-scs-data-stream](https://www.ibm.com/docs/en/personal-communications/13.0?topic=support-scs-data-stream)

*   **SCS-Extended:** The **SCS-Extended** format datastream is a sequential stream format used by IBM i based **CMOD** systems.

    To use the text search function with AFP or SCS-Extended documents, you must have the Portable Application Solutions Environment (PASE; a product option of IBM i) installed. If PASE is not installed, you will receive message 161 in the Content Manager OnDemand system log when attempting to perform a text search on AFP or SCS-Extended documents.

*   **PDF**: Portable Document Format. A protocol for formatting documents developed by Adobe. Designed to be viewable on other hardware operating systems independently from the operating system which was used to create it.

# [CHAPTER 12](#toc.xhtml_c12)

# [Configuring the `arsload` Program](#toc.xhtml_c12)

# [Introduction](#toc.xhtml_s166a)

The details of the use of the **`arsload`** program parameter settings are covered in this chapter. We cover the purpose and supported platforms of the **IBM Content Manager OnDemand** **`arsload`** software and describe the available functions supplied. The chapter outlines the prerequisites for **IBM CMODs** **`arsload`** program, including the creation of the **System Log** and **System Load** database tables using the **`arssyscr`** program. We also describe the use of the **`ARSXML`** **Windows** program and the **Linux****`arsxml`** program to import and export the **IBM CMOD Application Groups** from **XML** files and perform **XML** file validation.

See

[https://www.ibm.com/docs/en/cmofz/10.5.0?topic=files-configuring-arsload-program](https://www.ibm.com/docs/en/cmofz/10.5.0?topic=files-configuring-arsload-program)

# [Structure](#toc.xhtml_s167a)

In this chapter, we will discuss the following topics:

*   Creating the Database System Tables Using **arssyscr**
    *   Creating an Index
    *   Web Enablement Kit Implementation Guide
*   Setting up Test Data for the Windows **ARSLOAD** program
    *   Starting the First run
    *   Adding **IBM CMOD** Application Groups Using **arsxml**
    *   Exporting an **IBM CMOD** Application Group
    *   Updating **IBM CMOD** Application Groups

# [Creating the Database System Tables Using `arssyscr`](#toc.xhtml_s168a)

After the **`arsdb`** program has been used to create the instance or instances, as documented in the last *[Chapter 11, Starting arssockd on the Linux Server](#c11.xhtml)*, in the section titled, *Using arsdb to create a second IBM CMOD instance*, we can run the **`arssyscr`** for initializing the system logging feature for the instances.

# [Initializing the System Load Logging Facility](#toc.xhtml_s169a)

This **IBM Content Manager OnDemand** optional **`arsload`** logging facility can be used to enable the tracking of the **IBM Content Manager OnDemand** **`arsload`** loading activity.

The following command, using the **`-a`** switch, is used on our **Linux IBM CMOD** server, run as the **archive** Db2 instance user, to create the **System Load** feature for the first **archive** instance, as shown in *[Figure 12.1](#c12.xhtml_fig12_1):*

`./arssyscr -a -I archive`

![](images/Figure12.1.jpg)

**Figure 12.1:** The command used on our ***Linux IBM CMOD*** server to create the ***System Load*** feature for ***archive***

The following command, using the **`-a`** switch, is used on our **Linux IBM CMOD** server to create the **System Load** feature for the second, **`archive2`** instance, as shown in *[Figure 12.2](#c12.xhtml_fig12_2):*

`./arssyscr -a -I archive2`

![](images/Figure12.2.jpg)

**Figure 12.2:** The command used on our ***Linux IBM CMOD*** server to create the ***System Load*** feature for ***archive2***

# [Initializing the System Connection Logging Facility](#toc.xhtml_s170a)

The following command, using the **`-l`** switch, is used on our **Linux IBM CMOD** server to create the **System Log** feature for recording user and program connections for the first **archive** instance, as shown in *[Figure 12.3](#c12.xhtml_fig12_3):*

`./arssyscr -l -I archive`

![](images/Figure12.3.jpg)

**Figure 12.3:** The command used on our ***Linux IBM CMOD*** server to create the ***System Log*** feature for ***archive***

The following command, using the **`-l`** switch, is used on our **Linux IBM CMOD** server to create the **System Log** feature for recording user and program connections for the second **`archive2`** instance, as shown in *[Figure 12.4](#c12.xhtml_fig12_4):*

`./arssyscr -l -I archive2`

![](images/Figure12.4.jpg)

**Figure 12.4:** The command used on our ***Linux IBM CMOD*** server to create the ***System Log*** feature for ***archive2***

# [Initializing the System Migration Facility](#toc.xhtml_s171a)

The system migration **`-m`** switch is required by organizations using **IBM CMOD** who plan to migrate Application group index data from the database to archive storage.

After the instance of the **IBM Content Manager OnDemand** has been created, we can run the **`arssyscr`** program to initialize the **IBM Content Manager OnDemand** system migration facility for the instance.

We log into the server as the **root** user and enter the commands for the **archive** instance as shown in *[Figure 12.5](#c12.xhtml_fig12_5):*

`su – archive`

*`(enter the password)`*

`/opt/ibm/ondemand/V10.5/bin/arssyscr -I archive -m`

`exit`

![](images/Figure12.5.jpg)

**Figure 12.5:** The command used on our ***Linux IBM CMOD*** server to create the ***migration table*** feature for ***archive***

We repeat the procedure by entering the commands for the **archive2** instance as shown in *[Figure 12.6](#c12.xhtml_fig12_6):*

`su – archive2`

*`(enter the password)`*

`/opt/ibm/ondemand/V10.5/bin/arssyscr -I archive2 -m`

`exit`

![](images/Figure12.6.jpg)

**Figure 12.6:** The command used on our ***Linux IBM CMOD*** server to create the ***migration table*** feature for ***archive2***

Where **`archive`** and **`archive2`** are the names of the **IBM Content Manager OnDemand** instances we created earlier.

The **IBM Content Manager OnDemand** **arssyscr** program creates the tables that support the system migration facility. The **`arssyscr`** program outputs a series of progress messages as we have shown in *[Figures 12.5](#c12.xhtml_fig12_5) and [12.6](#c12.xhtml_fig12_6).*

# [Creating an Index](#toc.xhtml_s172a)

The **Generic indexer** uses a parameter file of Index data, which must be created for the input files before they can be loaded into an **IBM Content Manager OnDemand** system. The **Generic indexer** is used to load files into the system unless it consists of files of type **AFP**, line data, or **PDF**.

A standard text editor or a program can then be used to create the parameter file. An example of a parameter file that can be used by the **Generic indexer** to process Invoice files stored as `.tif` image files is as follows:

`CODEPAGE:819`

`COMMENT:          input file number 1`

`GROUP_FIELD_NAME:ldate`

`GROUP_FIELD_VALUE:17/06/24`

`GROUP_FIELD_NAME:name`

`GROUP_FIELD_VALUE:Mr.` `John Smith`

`GROUP_FIELD_NAME:company`

`GROUP_FIELD_VALUE:ACME Insurance`

`GROUP_FIELD_NAME:subject`

`GROUP_FIELD_VALUE:optical storage devices`

`GROUP_OFFSET:0`

`GROUP_LENGTH:0`

`GROUP_FILENAME:invoice1.tif`

`COMMENT:          input file number 2`

`GROUP_FIELD_NAME:ldate`

`GROUP_FIELD_VALUE:17/06/24`

`GROUP_FIELD_NAME:name`

`GROUP_FIELD_VALUE:Jan V.` `Geiger`

`GROUP_FIELD_NAME:company`

`GROUP_FIELD_VALUE:ARM Products Company`

`GROUP_FIELD_NAME:subject`

`GROUP_FIELD_VALUE:optical storage devices`

`GROUP_OFFSET:0`

`GROUP_LENGTH:0`

`GROUP_FILENAME:invoice2.tif`

See the link as follows:

[https://www.ibm.com/docs/en/cmofz/10.5.0?topic=files-creating-index-data](https://www.ibm.com/docs/en/cmofz/10.5.0?topic=files-creating-index-data)

# [Web Enablement Kit Implementation Guide](#toc.xhtml_s173a)

The **OnDemand Web Enablement Kit** provides several **Java API** functions, listed as follows:

**Note:** For working examples of the use of the Java API, see *[Chapter 9, CMOD Java API Examples](#c09.xhtml)*

*   **`Add Annotation`**: Enables users to add an annotation to the specified document.
*   **`Change Password`**: Allows users to change their Content Manager OnDemand passwords.
*   **`Delete Annotations`**: Enables users to delete the annotations attached to a specified document.
*   **`Document Hit List:`** Builds the list of items that match the search criteria.
*   **`Logoff`**: Allows users to log off from a Content ManagerOnDemand server.
*   **`Logon`**: Allows the users to log on to a Content Manager OnDemand server.
*   **`Retrieve Document`**: Retrieves a document from Content Manager OnDemand.
*   **`Search Criteria`**: Uses the default search criteria or enter search criteria to search for specific documents.
*   **`Server Print Document`**: Sends a copy of a document to the Content Manager OnDemand server printer.
*   **`Update Document`**: Updates one or more database fields for a specified document.
*   **`View Annotations`**: Views any document annotations attached to the specified document.

See also,

[https://cmod.wiki/images/9/97/ODWEK_Implementation_v95.pdf](https://cmod.wiki/images/9/97/ODWEK_Implementation_v95.pdf) and [https://www.ibm.com/docs/en/cmofi/7.5.0?topic=applications-loading-document](https://www.ibm.com/docs/en/cmofi/7.5.0?topic=applications-loading-document) [https://cmod.wiki/dox/CMODv10.5/WindowsClientCustomizationGuide.pdf](https://cmod.wiki/dox/CMODv10.5/WindowsClientCustomizationGuide.pdf)

# [Setting Up Test Data for the Windows ARSLOAD Program](#toc.xhtml_s174a)

On the Windows server installation of **IBM Content Manager OnDemand** we used the command line:

`ARSLOAD -u ADMIN -p filenet123 -h "localhost" -f -v -n -g "Baxter Bay Credit" "C:\cmod\BaxterBay\OD\BaxterBayData"`

This command required some updates to the **Baxter Bay Credit** Application Group’s Index Fields to provide a working load example, as we cover in the following sections.

# [Starting the First Run](#toc.xhtml_s175a)

The first run is as follows:

`C:\Program Files\ibm\OnDemand\V10.5\bin>ARSLOAD -u ADMIN -p filenet123 -h "localhost" -f -v -n -g "Baxter Bay Credit" "C:\cmod\BaxterBay\OD\BaxterBayData"`

Gave the output to the command windows as follows:

`ARS1609W Specifying passwords on the command line is not secure due to the text being visible.` `See the Installation and Configuration Guide for your platform for information about the arsstash command or using Unified Login.`

`2024-04-08 16:21:42.471686: ARS4315I Processing file >C:\cmod\BaxterBay\OD\BaxterBayData<`

`2024-04-08 16:21:42.476664: ARS4334I Load Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.2860>  OS Userid <ADMIN>  Install Location <C:\PROGRA~1\ibm\OnDemand\V10.5\>`

`2024-04-08 16:21:42.483632: ARS4335I Server Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.2860>  Database <DB2> <11.05.0400>`

`2024-04-08 16:21:42.503067: ARS1110E The application group >Baxter Bay Credit< does not exist or user >ADMIN< does not have permission to access the application group`

`2024-04-08 16:21:42.510037: ARS4318E Processing failed for file >C:\cmod\BaxterBay\OD\BaxterBayData<`

`2024-04-08 16:21:42.717564: ARS4327E Processing has stopped.  The remaining files will NOT be processed.`

`C:\Program Files\ibm\OnDemand\V10.5\bin>`

After the first run, there were two significant errors which prevented the import of the sample data we had:

1.  The **`arsload`** loader program recommended that the password for the **ADMIN** user is stored in an encrypted form in a file, **`ars.stash`**, created using the **`arsstash`** program. (Error message, **ARS1609W).** This message is a warning advisory one and the load will complete if there are no other fatal errors. This warning is denoted by the **W** at the end of the **ARS1609W** code given**.**

    The **`arsload`** switch **`-p`** **`ars.stash`** can be used, where the encrypted user’s password is created and stored in the file **`ars.stash`**`.`

2.  Also, the **Baxter Bay Credit** application group must be loaded and configured for the **ADMIN** user to have full access permissions for loading documents. (Error message, **ARS1110E).** This fatal error is denoted by the **E** at the end of the **ARS1110E** code given**.**

# [Adding IBM CMOD Application Groups Using `arsxml`](#toc.xhtml_s176a)

The **`arsxml`** program can be run to import the required **Baxter Bay Credit** Application Group:

See: [https://cmod.wiki/dox/CMODv10.1/AdministrationGuide.pdf](https://cmod.wiki/dox/CMODv10.1/AdministrationGuide.pdf)

(*Pages 314–315*)

The samples for the **`arsxml`** program can be found in the Linux path:

`/opt/ibm/ondemand/V10.5/xml/samples`

And the Windows server path:

`C:\Program Files\ibm\OnDemand\V10.5\xml\samples`

To add a group of users to an IBM Content Manager OnDemand system.

1.  Create a file called **`addgroups.xml`**.

    `<?xml version="1.0" encoding="UTF-8"?>`

    `<onDemand xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`

    `<!--  This file creates the Baxter  groups.  -->`

    `<group`

    `name="BaxterBayCredit"`

    `description="Baxter Bay Credit"`

    `ownerUser="Admin">`

    `</group>`

    `</onDemand>`

2.  Use a command line function:

    `ARSXML add -h "localhost" -u ADMIN -p filenet123  -i "C:\cmod\BaxterBay\addgroups.xml"`

The example above resulted in the following output:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSXML add -h "localhost" -u ADMIN -p filenet123  -i "C:\cmod\BaxterBay\addgroups.xml"`**

`ARS6822I Attempting login for userid 'ADMIN' on server 'localhost' ...`

`ARS1609W Specifying passwords on the command line is not secure due to the text being visible.` `See the Installation and Configuration Guide for your platform for information about the arsstash command or using Unified Login.`

**`ARS7743E A group object named 'BaxterBayCredit' already exists.`**

We decided to export the existing **BaxterBayCredit** Application group to verify the configuration as shown in the next section.

# [Exporting an IBM CMOD Application Group](#toc.xhtml_s177a)

First, we created a simple text file using the **`notepad.exe`** editor, called **`exportBaxterBayCredit.xml`** with the content as follows:

`<?xml version="1.0" encoding="UTF-8"?>`

`<onDemand xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`

`xsi:noNamespaceSchemaLocation="ondemand.xsd">`

`<group name="`**`BaxterBayCredit`**`"/>`

`</onDemand>`

To export the group named **BaxterBayCredit** and any users and user groups that are referenced by it, we used the following command to export the group:

`ARSXML export -h "localhost" -u ADMIN -p filenet123  -i "C:\cmod\BaxterBay\exportBaxterBayCredit.xml"`

This command created an **XML** output to the screen:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSXML export -h "localhost" -u ADMIN -p filenet123 -i "C:\cmod\BaxterBay\exportBaxterBayCredit.xml"`**

`ARS6822I Attempting login for userid 'ADMIN' on server 'localhost' ...`

`ARS1609W Specifying passwords on the command line is not secure due to the text being visible.` `See the Installation and Configuration Guide for your platform for information about the arsstash command or using Unified Login.`

**`<?xml version="1.0" encoding="UTF-8" ?>`**

**`<!-- 10.5.0.0`**

**`-->`**

**`<onDemand xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`**

**`   <group name="BaxterBayCredit" description="Baxter Bay Credit" updateDate="04/09/24 16:12:05" updateUserid="ADMIN" gid="1080001" ownerUser="ADMIN" >`**

**`   </group>`**

**`</onDemand>`**

`C:\Program Files\ibm\OnDemand\V10.5\bin>`

# [Updating IBM CMOD Application Groups](#toc.xhtml_s178a)

Next, to update the name of the existing group, the **`groupUpdate.xml`** file was created, using the notepad.exe program, which contained the data for the users and their user names.

The following command line function was called:

`ARSXML update -h "localhost" -u ADMIN -p filenet123 -i "C:\cmod\BaxterBay\updategroups.xml"`

The file, **`updategroups.xml`** contains:

`<?xml version="1.0" encoding="UTF-8"?>`

`<onDemand xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`

`<!--  This file updates groups and should be used during an arsxml update.  -->`

`<!-- Add users to the group -->`

`<group`

`name="BaxterBayCredit"`

`description="Baxter Bay Credit">`

`<user task="add" name="Admin"/>`

`<user task="add" name="Alan_"/>`

`</group>`

`</onDemand>`

Running this on the Windows server at first, gave:

`C:\Program Files\ibm\OnDemand\V10.5\bin>ARSXML update -h "localhost" -u ADMIN -p filenet123 -i "C:\cmod\BaxterBay\updategroups.xml"`

`ARS6822I Attempting login for userid 'ADMIN' on server 'localhost' ...`

**`ARS1609W Specifying passwords on the command line is not secure due to the text being visible.` `See the Installation and Configuration Guide for your platform for information about the arsstash command or using Unified Login.`**

`ARS7744E A user object named 'ALAN_' does not exist.`

So, we removed the line for the **`ALAN_`** user and changed the **updategroups.xml** file to:

`<?xml version="1.0" encoding="UTF-8"?>`

`<onDemand xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">`

`<!--  This file updates groups and should be used during an arsxml update.  -->`

`<!-- Add users to the group -->`

`<group`

`name="BaxterBayCredit"`

`description="Baxter Bay Credit">`

`<user task="add" name="Admin"/>`

`</group>`

`</onDemand>`

After rerunning the command on the Windows server:

`C:\Program Files\ibm\OnDemand\V10.5\bin>ARSXML update -h "localhost" -u ADMIN -p filenet123  -i "C:\cmod\BaxterBay\updategroups.xml"`

`ARS6822I Attempting login for userid 'ADMIN' on server 'localhost' ...`

**`ARS1609W Specifying passwords on the command line is not secure due to the text being visible.` `See the Installation and Configuration Guide for your platform for information about the arsstash command or using Unified Login.`**

`ARS7743E A group-user object named 'BaxterBayCredit-ADMIN' already exists.`

After investigation, we discovered that the above error, **`ARS7743E`**`,` was caused because the first run was partially successful. Although one user, **`Alan_`** did not exist, the other user, **ADMIN** was successfully added in the first run.

**Note**: *The users and groups for IBM CMOD security can be added by using the IBM CMOD Administration program*

# [Exporting All the Users](#toc.xhtml_s179a)

To export all the users in an **IBM Content Manager OnDemand** system, the

**`exportallusers.xml`** file was used.

The following command was used:

`./arsxml export -h localhost -i exportallusers.xml -o newusers.xml`

The user can validate the **`newusers.xml`** using the command:

`./arsxml validate -i newusers.xml`

To test this validation feature, we also used the file **`addgroups.xml`,** as shown in *[Figure 12.7](#c12.xhtml_fig12_7):*

![](images/Figure12.7.jpg)

**Figure 12.7:** This ***validate*** switch is tested using the file ***addgroups.xml***

After this validated successfully, we removed the last closing tag, **`</onDemand>`** **,** using the vi editor, to give the error output as shown in *[Figure 12.8](#c12.xhtml_fig12_8):*

![](images/Figure12.8.jpg)

**Figure 12.8:** We removed the last closing tag, ***</onDemand>*** using the vi editor, to give the error output

The missing closing **`</onDemand>`** tag is required and the failed xml is shown in *[Figure 12.9](#c12.xhtml_fig12_9)*:

![](images/Figure12.9.jpg)

**Figure 12.9:** The missing closing ***</OnDemand>*** tag is required and the failed xml is edited

We then edited this back in using the vi editor **`INSERT`** command, as shown highlighted in *[Figure 12.10](#c12.xhtml_fig12_10)*:

![](images/Figure12.10.jpg)

**Figure 12.10:** The missing ***</OnDemand>*** end tag is reinserted using the vi ***INSERT*** command

# [Conclusion](#toc.xhtml_s180a)

In this chapter, we described the use of the **`arsload`** program, the purpose and supported platforms of the **IBM Content Manager OnDemand** **`arsload`** software and the available functions supplied. We also outlined the prerequisites for **IBM CMODs** **`arsload`** program, describing the creation of the **System Log** and **System Load** database tables using the **`arssyscr`** program. Finally, the **`ARSXML`** **Windows** program and the **Linux****`arsxml`** program, examples for importing and exporting **IBM CMOD Application Groups** from **XML** files, and **XML** file validation were presented.

In the next chapter, *Running ARSLOAD,* we will cover the running of the **arsstash** program to store user passwords, further changes to the **Baxter Bay Credit** Application Group Field Indexes to allow the **`arsload`** program to complete a bulk load of a set of reports, and the use of the **`arssockd`** program to display the active Windows services.

# [Points to Remember](#toc.xhtml_s181a)

*   For working examples of the use of the **ODWEK** Java API, see *[Chapter 9, CMOD Java API Examples](#c09.xhtml).*
*   The**`arsload`** program warning messages are denoted by a **W** at the end of the message code (an **E** at the end of a code for a message, denotes a fatal error).
*   The **Generic indexer** is used to load files into the system, unless it consists of files of type **AFP**, line data, or **PDF**.

# [Multiple Choice Questions](#toc.xhtml_s182a)

1.  Which of the following **IBM CMOD** programs is used to create the system migration facility for an instance?
    1.  `arsload`
    2.  `arssockd`
    3.  `arssyscr`
    4.  `arsxml`
    5.  `arsdb`
    6.  `arsstash`
2.  Which of the following **IBM CMOD** programs is used for the creation of the **System Log** and **System Load** database tables?
    1.  `arsload`
    2.  `arssockd`
    3.  `arssyscr`
    4.  `arsxml`
    5.  `arsdb`
    6.  `arsstash`
3.  Which of the following **IBM CMOD** programs is used to import the required **IBM CMOD** **Application Groups**?
    1.  `arsload`
    2.  `arssockd`
    3.  `arssyscr`
    4.  `arsxml`
    5.  `arsdb`
    6.  `arsstash`

# [Answers](#toc.xhtml_s183a)

1.  c
2.  c
3.  d

# [Questions](#toc.xhtml_s184a)

1.  If you get an **`arsload`** program message with a code ending in a **W,** what does this denote?
2.  What procedure should be followed to ensure that the **IBM CMOD** system records all attempted log ons to it?
3.  What procedure would you follow to ensure that an Application Group XML file was syntactically correct after editing it?

# [Key Terms](#toc.xhtml_s185a)

*   **XML**: Extensible Markup Language provides a standard format with start and end tags to define and store data in a common format, for export and transfer to different operating system environments.
*   **API**: Application Programmer’s Interface is a library of callable software subroutines written to support the intercommunication between two or more separate functional software systems.
*   **ODWEK**: OnDemand Web Enablement Kit is an API called from Java using the **`ODApi.ja`**`r` and is also found in the **LD_LIBRARY_PATH** environment variable path, **`/opt/ibm/ondemand/V10.5/www,`** which is used to change a user’s password, retrieve a document, or delete an annotation and can also be used to load new documents.
*   **AFP:** Advanced Function Presentation **(AFP)** is a set of licensed programs that use the all-points-addressable concept to print text and graphics on a printer.
*   **PDF**: The Adobe “Portable Document Format” is a format that cannot be easily modified but allows anyone to share and print it.
*   **TIF:** The file extension for image files in the **TIFF** format, which stands for Tag Image File Format, is used to store raster-based image data in monochrome and color.

# [CHAPTER 13](#toc.xhtml_c13)

# [Running ARSLOAD](#toc.xhtml_c13)

# [Introduction](#toc.xhtml_s186a)

In this chapter, we will cover the **`ARSLOAD`** program example runs, shown for Windows and in the Linux environment. We will start by describing the prerequisite **Index Fields** required for loading documents into the example **Baxter Bay Credit** **Application** group. We will also cover the use of the **`ARSSOCKD`** program to display the list of **IBM CMOD** program services running on the Windows system. The use of the **arsdoc** program to generate the **Generic Index Field** file, used by **`ARSLOAD`**, is another topic covered in this chapter.

# [Structure](#toc.xhtml_s187a)

In this chapter, we will discuss the following topics:

*   Indexing Fields for the **Baxter Bay Credit Application** Group
    *   Running the **`arsdoc`** Program to Generate the **Generic Index** Field File
*   Running **`ARSLOAD`** on Windows
    *   First Run of **`ARSLOAD`** After the Fix Pack 10.5.0.7 Configuration Update
    *   Updating **Baxter Bay Credit Application** Group Fields
    *   Second Run of the **ARSLOAD** Program
    *   Third Run Issue with Date
    *   Fourth Run Success with Date Fixed by Editing the **.ind** File
*   Running ARSLOAD on **Linux**
    *   Running **`ARSSOCKD`** to Display the Services
    *   **CMOD** Video Training Link
    *   References

# [Indexing Fields for the Baxter Bay Credit Application Group](#toc.xhtml_s188a)

The results for successfully loading sample documents using the **arsload** program depends on setting up the archive database **Index Fields** to match the field definitions held in the example **Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit.ind,** **Index Field** definitions file, generated by the **`arsdoc`** command, which uses the **IBM OnDemand** **Generic Index** File Format.

The detailed examples for running the **IBM CMOD** **arsdoc** program, to create the **Generic Index** definitions **Index Field** file we used in this chapter, can be found at the link:

[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=arsdoc-examples](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=arsdoc-examples)

(See especially example 3).

The main details for these fields were obtained from the example code listing comments from the link: [https://cmod.wiki/dox/CMODv8.3/Shared%20Docs/wincust.pdf](https://cmod.wiki/dox/CMODv8.3/Shared%20Docs/wincust.pdf)

([Appendix A](#appa.xhtml). Microsoft Visual Basic 5.0 DDE sample program pages 237 to 238)

After the example code comment on page 232:

`'Open the` **`"Baxter Bay Credit"`** `folder frmStatusDlg.lblStatus.Caption = "Opening folder..."` `Call frmCreditV1.fncOpenFolder`

We can trace through the code to obtain the **Index Field** descriptions for the **Baxter Bay Credit** Folder taken from pages 237 to 238, after the highlighted comment as follows:

`'Look up the account number, contained in the pnlAcctnumData text field 'in the arsvblan.ini file.` `If found, read the respective 'fields.` `If not found display error message.` `acct_num = txtAcctnumData.Text 'Do at least a little validation.`

Then, we can identify the **Baxter Bay Credit** **Index Field** details from the highlighted parameters, as shown in bold in the following code extract:

From page 237:

`If` **`Len(acct_num) <> 11`** `Then`

`MsgBox "`**`Correct format for account # is 000-000-000"`**

`Exit Sub`

`End If`

`'If we have gotten to here we know that we have an` **`account 'number of the format 000-000-000.`**

`If either of the first 'two sections of the number are non-zero or` **`if the third 'section is not between 001-046`** `then` **`default to the account 'number 000-000-001`**`.` `first_num = Int(Mid(acct_num, 1, 3)) second_num = Int(Mid(acct_num, 5, 3)) third_num = Int(Mid(acct_num, 9, 3)) If first_num <> 0 Or second_num <> 0 Or third_num > 46 Then`

Next, from Page 238 we have highlighted the code as follows:

**`acct_num = "000-000-001"`**

`ElseIf third_num = 0 Then`

`MsgBox "Invalid account number!"`

`Exit Sub`

`End`

`If ini_str = fncParmGet(acct_num,` **`"Name"`**`, ininame)`

`If Len(ini_str) = 0 Then`

`MsgBox "'`**`Name`**`' field not found for acct#" + acct_num + "in " + ininame`

`Exit Sub`

`End`

`If pnlNameData.Caption = " " + ini_str ini_str = fncParmGet(acct_num, "`**`SSN`**`", ininame)`

`If Len(ini_str) = 0 Then`

`MsgBox "'`**`SSN`**`' field not found for acct#" + acct_num + "in " + ininame`

`Exit Sub`

`End If`

`pnlSSNData.Caption = " " + ini_str ini_str = fncParmGet(acct_num, "`**`DOB`**`", ininame)`

`If Len(ini_str) = 0 Then`

`MsgBox "'`**`DOB`**`' field not found for acct#" + acct_num + "in " + ininame`

`Exit Sub`

`End`

`If pnlDOBData.Caption = " " + ini_str ini_str = fncParmGet(acct_num, "`**`MaidenName`**`", ininame)`

`If Len(ini_str) = 0 Then`

`MsgBox "'`**`MaidenName`**`' field not found for acct#" + acct_num + "in " + ininame`

`Exit Sub`

`End`

`If pnlMNameData.Caption = " " + ini_str ini_str = fncParmGet(acct_num, "`**`StreetAddress`**`", ininame)`

`If Len(ini_str) = 0 Then`

`MsgBox "'`**`StreetAddress`**`' field not found for acct#" + acct_num + "in " + ininame`

`Exit Sub`

`End`

`If pnlAddrData1.Caption = " " + ini_str ini_str = fncParmGet(acct_nu m, "`**`CityStateZip`**`", ininame)`

`If Len(ini_str) = 0 Then`

`MsgBox "'`**`CityStateZip`**`' field not found for acct#" + acct_num + "in " + ininame`

`Exit Sub`

`End`

`If pnlAddrData2.Caption = " " + ini_str ini_str = fncParmGet(acct_num, "`**`PhoneNum`**`", ininame)`

`If Len(ini_str) = 0 Then`

`MsgBox "'`**`PhoneNu``m`**`' field not found for acct#" + acct_num + "in " + ininame`

`Exit Sub`

`End If`

`pnlPhoneData.Caption = " " + ini_str`

# [Running the arsdoc Program to Generate the Generic Index field file](#toc.xhtml_s189a)

The arsdoc command can be run from a Windows command line, as follows, to create **.ind** **Index Field** files:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`cd c:\`**

`c:\>`**`mkdir CMOD_OUT`**

`c:\>`**`cd CMOD_OUT`**

`c:\CMOD_OUT>`**`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\arsdoc get -h ARCHIVE -u ADMIN -p filenet123 -f "System Load" -a -c -g -o "Baxter Bay Credit" -N -v -i "WHERE applgrp_name = 'Baxter Bay Credit"`**

The first time this was run we had omitted the final single quote (from **`'Baxter Bay Credit")`**, which resulted in the following:

`c:\CMOD_OUT>`**`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\arsdoc get -h ARCHIVE -u ADMIN -p filenet123 -f "System Load" -a -c -g -o "Baxter Bay Credit" -N -v -i "WHERE applgrp_name = 'Baxter Bay Credit"`**

`2024-07-06 15:11:36.664567: ARS6108I Starting arsdoc.  Version:  10.5.0.0`

`2024-07-06 15:11:36.673533: ARS6165I c:\PROGRA~1\ibm\OnDemand\V10.5\bin\arsdoc get -h ARCHIVE -u ADMIN -f System Load -a -c -g -o Baxter Bay Credit -N -v -i WHERE applgrp_name = 'Baxter Bay Credit`

`2024-07-06 15:11:36.687500: ARS1609W Specifying passwords on the command line is not secure due to the text being visible.` `See the Installation and Configuration Guide for your platform for information about the arsstash command or using Unified Login.`

`2024-07-06 15:11:36.704975: ARS6822I Attempting login for userid 'ADMIN' on server 'ARCHIVE' ...`

`2024-07-06 15:11:36.735281:` **`ARS6080I Login successful`**

`2024-07-06 15:11:36.740259: ARS6062I Searching for folder 'System Load' ...`

`2024-07-06 15:11:36.761417: ARS6084I Search successful`

`2024-07-06 15:11:36.766399: ARS6167W The application group 'System Load' contains a segment date.` `For better performance, a segment date range should be specified by using the -S parameter.`

`2024-07-06 15:11:36.781429: ARS6063I Searching for documents in 'System Load' ...`

`2024-07-06 15:11:36.789591: ARS6117I Querying database with SQL string 'WHERE applgrp_name = 'Baxter Bay Credit'`

`2024-07-06 15:11:36.924447:` **`ARS6085E Search unsuccessful`**

**`2024-07-06 15:11:36.928447: ARS6007E The server failed during a search operation.` `View the System Log for additional messages.`**

`2024-07-06 15:11:36.940406: ARS6026I arsdoc completed.`

The system log was searched in **IBM Content Navigator**, using the **IBM CMOD** desktop:

URL, **[`http://ecmukdemo22:9081/navigator/?desktop=ContentManagerOnDemand`](http://ecmukdemo22:9081/navigator/?desktop=ContentManagerOnDemand),** as shown in *[Figure 13.1](#c13.xhtml_fig13_1)*:

![](images/Figure13.1.jpg)

**Figure 13.1:** The system log was searched in ***IBM Content Navigator***, using the ***IBM CMOD*** desktop

The message revealed the issue with the missing single quote, as highlighted in *[Figure 13.2](#c13.xhtml_fig13_2)*:

![](images/Figure13.2.jpg)

**Figure 13.2:** The message revealed the issue with the missing single quote, as highlighted

Rerunning the corrected command gave the following output:

`c:\CMOD_OUT>`**`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\arsdoc get -h ARCHIVE -u ADMIN -p filenet123 -f "System Load" -a -c -g -o "Baxter Bay Credit" -N -v -i "WHERE applgrp_name = 'Baxter Bay Credit'"`**

`2024-07-06 15:14:05.740588: ARS6108I Starting arsdoc.  Version:  10.5.0.0`

`2024-07-06 15:14:05.747563: ARS6165I c:\PROGRA~1\ibm\OnDemand\V10.5\bin\arsdoc get -h ARCHIVE -u ADMIN -f System Load -a -c -g -o Baxter Bay Credit -N -v -i WHERE applgrp_name = 'Baxter Bay Credit'`

`2024-07-06 15:14:05.760089: ARS1609W Specifying passwords on the command line is not secure due to the text being visible.` `See the Installation and Configuration Guide for your platform for information about the arsstash command or using Unified Login.`

`2024-07-06 15:14:05.775028: ARS6822I Attempting login for userid 'ADMIN' on server 'ARCHIVE' ...`

`2024-07-06 15:14:05.804006: ARS6080I Login successful`

`2024-07-06 15:14:05.806992: ARS6062I Searching for folder 'System Load' ...`

`2024-07-06 15:14:05.826446: ARS6084I Search successful`

`2024-07-06 15:14:05.830428: ARS6167W The application group 'System Load' contains a segment date.` `For better performance, a segment date range should be specified by using the -S parameter.`

`2024-07-06 15:14:05.840749: ARS6063I Searching for documents in 'System Load' ...`

`2024-07-06 15:14:05.846678: ARS6117I Querying database with SQL string 'WHERE applgrp_name = 'Baxter Bay Credit''`

`2024-07-06 15:14:05.905075: ARS6085E Search unsuccessful`

`2024-07-06 15:14:05.910053: ARS6034W No hits were found that matched search criteria.`

`2024-07-06 15:14:05.922045: ARS6026I arsdoc completed.`

`c:\CMOD_OUT>`

# [Running `ARSLOAD` on Windows](#toc.xhtml_s190a)

The previous run of the **`arsdoc`** program gave the warning message as follows:

**`ARS1609W`** `Specifying passwords on the command line is not secure due to the text being visible.`

This message is not fatal, but for security we can encrypt the user passwords and store them in an **`ars.stash`** file using the **`arsstash`** command line program.

First, before running the **`arsload`** program, we ran the **IBM OnDemand** Command Window V10.5 as Administrator, then used the **`arsstash`** program command on its own to view the list of options:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`arsstash`**

`ARS1600I Usage: arsstash [-a <action>] [-c] -s <stash_file> -u <userid>`

`Version:  10.5.0.0`

`-a <action> Action to perform`

`1  - Store the OnDemand userid and password (default)`

`2  - Delete the OnDemand userid and password`

`3  - Store the OnDemand userid and password for ARSLOAD`

`4  - Store the OnDemand userid and password for ODF`

`6  - Store the OnDemand userid and password for PDD`

`7  - Store the LDAP userid and password`

`8  - Store the DB2 userid and password`

`9  - Store the Oracle userid and password`

`10 - Store the ZooKeeper userid and password`

`If no userid (-u) is given for actions 3 thru 10, then`

`the currently assigned userid for the corresponding`

`OnDemand command or database will be displayed`

`-c Create stash file`

`-s <stash_file> Stash file name`

`-u <userid> Userid`

`-1 <trace_file>  Trace file`

`-2 <trace_level> Trace level`

`C:\Program Files\ibm\OnDemand\V10.5\bin>`

Then to create a stash file called **`ars.stash`** and store a user (**`Alan_`**) for a password for use with the **`arsload`** **`-p`** switch, the command is run as follows:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`arsstash -a 3 -c  -s ars.stash -u Alan_`**

`OnDemand Password:`*`xxxxxxxxx`*

`Verify OnDemand Password:`*`xxxxxxxxx`*

and then we stored a password in the **ars.stash** file for a second user (**ADMIN**), for the **arsload** program, using the command as follows:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`arsstash -a 3  -s ars.stash -u ADMIN`**

`OnDemand Password:`**`filenet123`**

`Verify OnDemand Password:`**`filenet123`**

`C:\Program Files\ibm\OnDemand\V10.5\bin>`

You can use the **`ARSLOAD`** command on its own to view the list of options, as listed here:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSLOAD`**

`ARS4300I Usage: arsload [options] [load_file]`

`Version: 10.5.0.0`

`-a <appl> The application within the application group`

`Defaults to filename conventions`

`-A <field> MVS filename component to use for OnDemand application`

`-b <index_number,field> Index number (1-8),index field name`

`-B <filename_format> Format of input filename for parsing`

`WRI       WRITER`

`MVS       MVS`

`JOB       JOBNAME`

`DAT       DATASET`

`FOR       FORMS`

`YY        YYDDD`

`HH        HHMMM`

`AG        Application Group`

`APP       Application`

`FLD       Field placeholder for indexing`

`1-8       Index number (1-8) - Prepend to parts of the`

`                 filename above being used as indexes`

`                 (Requires one -b parameter per index number used)`

`IGN       Ignore this part of the filename (Cannot be indexed)`

`.EXT      Extension`

`Example: For files in the default format`

`MVS.JOBNAME.DATASET.FORMS.YYDDD.HHMMM.ARD`

`the format could be written as`

`MVS.JOB.DAT.FOR.YY.HH.EXT`

`The format could be written as`

`MVS.1JOB.DAT.FOR.YY.HH.EXT`

`to associate the JOB part of filename as a load index 1`

`Example: For files not in the default format`

`APPLICATION_GROUP.APPLICATION.MISC.DATE.ARD`

`the format could be written as`

`AG.APP.IGN.FLD.EXT`

`and AG.APP.IGN.1FLD.EXT could be used to extract the date`

`information of the filename into a specific index field`

`-c <idx_dir> The directory to run the indexer`

`Defaults to current directory`

`-C <class> (OD/zOS) jes class to monitor`

`-d <dl_dir> The download directory`

`Can be specified more than once`

`-E Execute the arsuupdt user exit program`

`-f If load fails, unload the data`

`-F <form> (OD/zOS) jes form to monitor`

`-g <appl_grp> The application group`

`  Defaults to filename conventions`

`-G <field> MVS filename component to use for OnDemand application group`

`(OD/zOS) WRITER.MVS.JOBNAME.DATASET.FORMS`

`         or`

`       MVS.JOBNAME.DATASET.FORMS`

`(Otherwise) MVS.JOBNAME.DATASET.FORMS`

`Defaults to FORMS`

`-h <od_inst> OnDemand library server or instance name (same as -I)`

`-i Run the Indexer Only`

`-I <od_inst> OnDemand library server or instance name (same as -h)`

`-J <file_name_delimiter> Delimiter character for filename parsing (Default: .)`

`-j <parm_file> Additional indexing parameters`

`-l <field> Index the entire load filename using the field identifier`

`-n Do not remove files`

`-p <passwd> Password stash file`

`-s <input>`

`(OD/zOS) JCL ddname to use as input (ie.` `INPUT)`

`-t <seconds> Time interval to sleep`

`Defaults to 600 seconds`

`-u <userid> Userid`

`-v Verbose`

`-W <writer> (OD/zOS) jes writer to monitor`

`-X <indexer> Indexer to use (Overrides indexer defined in the application)`

`A: Content Manager OnDemand ACIF Indexer`

`G: Content Manager OnDemand Generic Indexer File Format`

`P: Content Manager OnDemand PDF Indexer`

`X: Content Manager OnDemand XML Indexer`

`3: 390 Indexer`

`4: 400 Indexer`

`-Z <user_def> User defined string passed to load user exit`

`-1 <trace_file> Trace file`

`-2 <trace_level> Trace level`

We can now use the **ARSLOAD** program on Windows, with the following switches to load documents:

`ARSLOAD  -u ADMIN -p ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`

# [First Run of ARSLOAD After the Fix Pack 10.5.0.7 Configuration Update](#toc.xhtml_s191a)

After we applied the IBM Fix Pack version **10.5.0.7**, for **IBM Content Manager OnDemand**, as described in *[Appendix A: IBM Content Manager OnDemand Fix Pack Installation](#appa.xhtml),* we tried a first run of the Windows **`ARSLOAD`** program, as follows:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSLOAD  -u ADMIN -p ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`**

`2024-04-12 22:59:33.353613: ARS4315I Processing file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-12 22:59:33.359586: ARS4334I Load Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  OS Userid <ADMIN>  Install Location <C:\PROGRA~1\ibm\OnDemand\V10.5\>`

`2024-04-12 22:59:33.372585: ARS4335I Server Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  Database <DB2> <11.05.0400>`

`2024-04-12 22:59:33.437508: ARS4339I Application Group >Baxter Bay Credit<`

`2024-04-12 22:59:33.441503: ARS4340I Application` **`>BaxterBayCredit<`**

`2024-04-12 22:59:33.445065: ARS4341I Storage Set >Cache Only - Library Server<`

`2024-04-12 22:59:33.449047: ARS4342I Storage Node >Cache Only - Library Server<`

`2024-04-12 22:59:33.453029: ARS4347I Encryption >None<`

`2024-04-12 22:59:33.457021: ARS4312I Loading started, 714654 bytes to process`

`2024-04-12 22:59:33.489450: ARS1142I Resource c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit.res will be added as resource >2-1-0<.  Compression Type(OD77) Original Size(271127) Compressed Size(6276)`

`2024-04-12 22:59:33.530980: ARS1143I` **`The field name 'name' found in the index file`** `does not match any expected fields.  The field will be ignored.`

`2024-04-12 22:59:33.540563: ARS1143I` **`The field name 'account' found in the index file`** `does not match any expected fields.  The field will be ignored.`

`2024-04-12 22:59:33.547574: ARS1143I` **`The field name 'crd_date' found in the index file`** `does not match any expected fields.  The field will be ignored.`

`2024-04-12 22:59:33.558541: ARS1143I` **`The field name 'balance' found in the index file`** `does not match any expected fields.  The field will be ignored.`

`2024-04-12 22:59:33.565514: ARS1130E 0 fields submitted by the indexer,` **`6 expected`**

`2024-04-12 22:59:33.571066: ARS1146I Loaded 0 rows into the database`

`2024-04-12 22:59:33.574053: ARS4311E Loading failed`

`2024-04-12 22:59:33.577040: ARS4318E` **`Processing failed for file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`**

`2024-04-12 22:59:33.781477: ARS4327E Processing has stopped.  The remaining files will NOT be processed.`

`C:\Program Files\ibm\OnDemand\V10.5\bin>`

# [Updating Baxter Bay Credit Application Group Fields](#toc.xhtml_s192a)

Using the example in the file **`Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit.ind`** we had to update the original**`Baxter Bay Application`** group to add the following **Index Field** names identified in the preceding error log list, as shown in bold:

`GROUP_FIELD_NAME:`**`name`**

`GROUP_FIELD_VALUE:SMITH CYCLERY CO`

`GROUP_FIELD_NAME:`**`account`**

`GROUP_FIELD_VALUE:000-000-000`

`GROUP_FIELD_NAME:`**`crd_date`**

`GROUP_FIELD_VALUE:04/03/95`

`GROUP_FIELD_NAME:`**`balance`**

`GROUP_FIELD_VALUE:1058.110000`

# [Second Run of the ARSLOAD Program](#toc.xhtml_s193a)

After the update of the **Application** group fields for **Baxter Bay Credit**, we reran the Windows **`ARSLOAD`** program:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSLOAD  -u ADMIN -p ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`**

`2024-04-12 23:29:49.371284: ARS4315I Processing file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-12 23:29:49.378587: ARS4334I Load Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  OS Userid <ADMIN>  Install Location <C:\PROGRA~1\ibm\OnDemand\V10.5\>`

`2024-04-12 23:29:49.387581: ARS4335I Server Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  Database <DB2> <11.05.0400>`

`2024-04-12 23:29:49.460143: ARS4339I Application Group >Baxter Bay Credit<`

`2024-04-12 23:29:49.464175: ARS4340I Application >BaxterBayCredit<`

`2024-04-12 23:29:49.471165: ARS4341I Storage Set >Cache Only - Library Server<`

`2024-04-12 23:29:49.476765: ARS4342I Storage Node >Cache Only - Library Server<`

`2024-04-12 23:29:49.483693: ARS4347I Encryption >None<`

`2024-04-12 23:29:49.491715: ARS4312I Loading started, 714654 bytes to process`

`2024-04-12 23:29:49.519428: ARS1140I Resource c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit.res matches the resource >2-1-0<`

**`2024-04-12 23:29:49.544889: ARS1130E 4 fields submitted by the indexer, 10 expected`**

`2024-04-12 23:29:49.549864: ARS1146I Loaded 0 rows into the database`

`2024-04-12 23:29:49.554844: ARS4311E Loading failed`

`2024-04-12 23:29:49.558829: ARS4318E Processing failed for file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-12 23:29:49.746385: ARS4327E Processing has stopped.  The remaining files will NOT be processed.`

`C:\Program Files\ibm\OnDemand\V10.5\bin>`

The original **Baxter Bay Credit Application** group we had created, contained ten fields, six of which we had to remove by deleting and recreating the **Baxter Bay Credit Application** group to leave the fields highlighted, as shown in *[Figure 13.3](#c13.xhtml_fig13_3)*:

![](images/Figure13.3.jpg)

**Figure 13.3:** The original ***Baxter Bay Credit Application*** group we had created, contained ten fields

See also *[Appendix B: Recreating an Application Group](#appb.xhtml)*, which we used to recreate the highlighted fields. We added the fields to the new **Baxter Bay Credit Application** group, as listed here:

`GROUP_FIELD_NAME:`**`name`**

`GROUP_FIELD_VALUE:SMITH CYCLERY CO`

`GROUP_FIELD_NAME:`**`account`**

`GROUP_FIELD_VALUE:000-000-000`

`GROUP_FIELD_NAME:`**`crd_date`**

`GROUP_FIELD_VALUE:04/03/95`

`GROUP_FIELD_NAME:`**`balance`**

`GROUP_FIELD_VALUE:1058.110000`

# [Third Run Issue with Date](#toc.xhtml_s194a)

The updated fields for **Baxter Bay Credit** still failed, but the only error was caused by an incorrect date format, relating to the format of the **`crd_date`** field in the **`.ind`** file, as shown here:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSLOAD  -u ADMIN -p ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`**

`2024-04-13 13:40:37.642030: ARS4315I Processing file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-13 13:40:37.647026: ARS4334I Load Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  OS Userid <ADMIN>  Install Location <C:\PROGRA~1\ibm\OnDemand\V10.5\>`

`2024-04-13 13:40:37.655511: ARS4335I Server Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  Database <DB2> <11.05.0400>`

`2024-04-13 13:40:37.715190: ARS4339I Application Group >Baxter Bay Credit<`

`2024-04-13 13:40:37.718185: ARS4340I Application >Baxter Bay Credit<`

`2024-04-13 13:40:37.722175: ARS4341I Storage Set >Cache Only - Library Server<`

`2024-04-13 13:40:37.725162: ARS4342I Storage Node >Cache Only - Library Server<`

`2024-04-13 13:40:37.728149: ARS4347I Encryption >None<`

`2024-04-13 13:40:37.732132: ARS4312I Loading started, 714654 bytes to process`

`2024-04-13 13:40:37.757179: ARS1142I Resource c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit.res will be added as resource >2-1-0<.  Compression Type(OD77) Original Size(271127) Compressed Size(6276)`

**`2024-04-13 13:40:37.788189: ARS1129E Row 1:  The string "04/03/95" could not be converted to a date from the format of %m/%d/%y %H:%M:%S`**

`2024-04-13 13:40:37.792172: ARS1146I Loaded 0 rows into the database`

`2024-04-13 13:40:37.795168: ARS4311E Loading failed`

`2024-04-13 13:40:37.799150: ARS4318E Processing failed for file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-13 13:40:37.993931: ARS4327E Processing has stopped.  The remaining files will NOT be processed.`

So, we deleted and re-entered the Date field, **`crd_date`** as a new **date** field for the **Baxter Bay Credit** application group.

After this update of the **`crd_date`** field, we still get the following log output:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSLOAD  -u ADMIN -p ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`**

`2024-04-13 14:53:07.285932: ARS4315I Processing file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-13 14:53:07.292154: ARS4334I Load Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  OS Userid <ADMIN>  Install Location <C:\PROGRA~1\ibm\OnDemand\V10.5\>`

`2024-04-13 14:53:07.305114: ARS4335I Server Version <10.5.0.0>  Operating System <Windows 64> <10.0.22621.3374>  Database <DB2> <11.05.0400>`

`2024-04-13 14:53:07.362543: ARS4339I Application Group >Baxter Bay Credit<`

`2024-04-13 14:53:07.365539: ARS4340I Application >Baxter Bay Credit<`

`2024-04-13 14:53:07.369884: ARS4341I Storage Set >Cache Only - Library Server<`

`2024-04-13 14:53:07.374866: ARS4342I Storage Node >Cache Only - Library Server<`

`2024-04-13 14:53:07.383091: ARS4347I Encryption >None<`

`2024-04-13 14:53:07.386075: ARS4312I Loading started, 714654 bytes to process`

`2024-04-13 14:53:07.413037: ARS1142I Resource c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit.res will be added as resource >2-1-0<.  Compression Type(OD77) Original Size(271127) Compressed Size(6276)`

`2024-04-13 14:53:07.442462:` **`ARS1129E Row 1:  The string "04/03/95" could not be converted to a date from the format of %m/%d/%Y`**

`2024-04-13 14:53:07.446452: ARS1146I Loaded 0 rows into the database`

`2024-04-13 14:53:07.449439: ARS4311E Loading failed`

`2024-04-13 14:53:07.452727: ARS4318E Processing failed for file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-13 14:53:07.672154: ARS4327E Processing has stopped.  The remaining files will NOT be processed.`

# [Fourth Run Success with Date Fixed by Editing the `.ind` file](#toc.xhtml_s195a)

After the last failure of the Index Field, **`crd_date`**, we edited all occurrences of the date year field from **/95** to **/1995**, which worked as shown in *[Figure 13.4](#c13.xhtml_fig13_4)***:**

`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ARSLOAD  -u ADMIN -p c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`

![](images/Figure13.4.jpg)

**Figure 13.4:** Fourth run success with date fixed by editing the ***.ind*** file

We can also view the successful load of the 236 rows to the **IBM OnDemand** database in the **IBM Content Navigator** desktop, **ContentManagerOnDemand,** we created, as highlighted in *[Figure 13.5](#c13.xhtml_fig13_5)*:

![](images/Figure13.5.jpg)

**Figure 13.5:** The successful load of the 236 rows to the ***IBM OnDemand*** database

# [Running ARSLOAD on Linux](#toc.xhtml_s196a)

The **`-h`** option can be used with the **IP** address of the Linux server as shown here:

`c:\CMOD_OUT>`**`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ARSLOAD -u ADMIN -p filenet123 -h "192.168.50.134" -f -v -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`**

# [Running ARSSOCKD to Display the Services](#toc.xhtml_s197a)

The services running on Windows can be displayed using the command **`arssockd -I`** **`ARCHIVE -p`**, with the output shown in *[Figure 13.6](#c13.xhtml_fig13_6)***:**

**`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\arssockd -I ARCHIVE -p`**

![](images/Figure13.6.jpg)

**Figure 13.6:** The services running on Windows can be displayed using the command ***arssockd -I ARCHIVE -p***

The services on Linux server can be displayed using the command, as follows, with the output as shown in *[Figure 13.7](#c13.xhtml_fig13_7)***:**

`[root@ECMUKDEMO22 ~]#` **`/opt/ibm/ondemand/V10.5/bin/arssockd -I archive -p`**

![](images/Figure13.7.jpg)

**Figure 13.7:** The services on Linux server can be displayed using the command highlighted

# [CMOD Video Training Link](#toc.xhtml_s198a)

The following link covers the overview of **IBM Content Manager OnDemand**:

[https://www.youtube.com/watch?v=vVY2luUSlrg](https://www.youtube.com/watch?v=vVY2luUSlrg)

# [Conclusion](#toc.xhtml_s199a)

In this chapter, we covered the **`ARSLOAD`** program example runs, shown for **Windows** and in the **Linux** environment. We began by describing the prerequisite **Index Fields** required for loading documents into the example **Baxter Bay Credit** **Application** group. We also covered the use of the **`ARSSOCKD`** program to display the list of **IBM CMOD** program services running on the Windows system. The use of the **`arsdoc`** program to generate the **Generic Index Field** file, used by **`ARSLOAD`**, was also covered.

In *[Chapter 14, Running the ARSXAFP Program on Windows and Linux](#c14.xhtml)*, we show how to process an AFP input file located in a directory and redirect the line data output to a file.

# [Points to Remember](#toc.xhtml_s200a)

*   The results for successfully loading sample documents using the **arsload** program depends on setting up the archive database **Index Fields** to match the field definitions held in the **`Index Field .ind`** input file.
*   The **System Log** table can be searched in **IBM Content Navigator**, using the **IBM CMOD** desktop to identify the reasons for a failure to run **IBM CMOD** programs using the URL:**[http://ecmukdemo22:9081/navigator/?desktop=ContentManagerOnDemand](http://ecmukdemo22:9081/navigator/?desktop=ContentManagerOnDemand)**.

# [Multiple Choice Questions](#toc.xhtml_s201a)

1.  Which program can be used to store passwords in an encrypted form for users?
    1.  `ARSLOAD`
    2.  `ARSSTASH`
    3.  `ARSDOC`
    4.  `ARSSOCKD`
2.  What **-a** action switch code is used to store the user password for the **ARSLOAD** program?
    1.  `7`
    2.  `4`
    3.  `3`
    4.  `6`

# [Answers](#toc.xhtml_s202a)

1.  b
2.  c

# [Questions](#toc.xhtml_s203a)

1.  What procedure would you use to correct the following warning message:

    **`ARS1609W`** `Specifying passwords on the command line is not secure due to the text being visible.`

2.  What procedure would you use to correct the following error message:

    **`ARS1130E 4 fields submitted by the indexer, 10 expected`**

3.  How would you correct the following error message:

    **`ARS1129E Row 1: The string "04/03/95" could not be converted to a date from the format of %m/%d/%y %H:%M:%S`**

# [Key Terms](#toc.xhtml_s204a)

*   **ACIF**: The Advanced Conversion and Indexing Function, is a batch utility program for indexing the print data streams for unformatted **ASCII** and **EBCDIC** data on **z/OS** using **ACIF** application programs. For an overview see: [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=indexer-acif-overview](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=indexer-acif-overview)
*   **ASCII:** The American Standard Code for Information Interchange is a standard for encoding alphanumeric printing, punctuation and control characters in a one-byte (7 bit) value per character for 128 different characters. IBM developed extended **ASCII** in 1981, as an 8-bit code to support an additional 32 control character codes such as carriage return and line feed.
*   **EBCDIC**: Developed by IBM in 1964, Extended Binary Coded Decimal Interchange Code was used in the IBM 360 mainframe Operating system. It is also based on an eight-bit (byte) binary code like ASCII, for alphanumeric characters and punctuation marks but EBCDIC divides the eight bits for each character into two four-bit zones, with one zone indicating the type of character, and the other zone indicating the value within the type.
*   **DB2**: The relational database software developed by IBM supporting the 41 **IBM CMOD** database tables and the related indexes and views.
*   **MVS:** Multiple Virtual Storage (MVS) is an operating system from IBM running on some of IBM’s mainframe servers.
*   **OD/zOS:** IBM OnDemand on the z/OS operating system for use by IBM z mainframes.
*   **IP:** The Internet Protocol is the protocol for transmitting and receiving data and the structure of the data used for telecommunications defined for transmitting data between internet and local client/server hardware systems.
*   **IBM CMOD:** The **IBM Content Manager OnDemand** software system consisting of a large number of service and utility programs to support the capture of electronic documents and print streams, running on multiple hardware and operating systems, which is the subject of this book.

# [CHAPTER 14](#toc.xhtml_c14)

# [Running the ARSXAFP Program on Windows and Linux](#toc.xhtml_c14)

# [Introduction](#toc.xhtml_s205a)

This chapter shows how to process an **AFP** input file located in a directory and redirect the line data output to a file using the **IBM Content Manager OnDemand** **ARSXAFP** program on a Windows and Linux server environment.

The **`ARSXAFP`** program bypasses images and graphics and other non-printing characters present in the input data. The fonts in the input data can be mapped to a monospaced font by naming a file containing the form definition (**CSDEF.FNT** on Windows) and overlay associated with the input file.

# [Structure](#toc.xhtml_s206a)

In this chapter, we will discuss the following topics:

*   **`ARSXAFP`** Program Parameter Options
*   **`ARSXAFP`** Command Line Examples

# [ARSXAFP Program Parameter Options](#toc.xhtml_s207a)

The following program shows how to process an **AFP** input file located in a directory and redirect the line data output to a file. By default, the input file contains 8.5 x 11-inch pages:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`arsxafp`**

`ARS4400I Usage: arsxafp [-c] [-l] [-w] [-h] [-o] [-r] [-f] [-t] [-x] [-y] inputfile`

`Version: 10.5.0.0`

**`-c`** `<chars> Characters per inch (horizontal) (default: 18)`

**`-l`** `<lines> Lines per inch (vertical) (default: 12)`

`-w <inches> Page width (default: 8.5)`

`-h <inches> Page height (default: 11.0)`

**`-o`** `<rot> Page orientation ( 0 |` **`90`** `| 180 | 270)`

`-r <file> Resource group file`

`-f <dir> Font directory`

`-t <file> AFP viewer trace file`

`-x Suppress rules/lines`

`-y Character space reset`

`-1 <trace_file> Trace file`

`-2 <trace_level> Trace level`

The **`-o`** (Page rotation angle) parameter is very important for the correct extraction of the text line data. The **90** degree option is given as the first example in IBM documentation ([https://www.ibm.com/docs/en/cmofm/10.5.0?topic=arsxafp-examples](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=arsxafp-examples)), but the example **AFP** files we have used, required the default 0 degree settings, as shown in the examples following the next section.

# [ARSXAFP Command Line Examples](#toc.xhtml_s208a)

The first run of the **`arsaxafp`** program on Windows was made using a **`SampleAFP.afp`** file with output directed from standard out to a **`SampleAFP.lin`** file, using the following command:

`C:\Program Files\ibm\OnDemand\V10.5\bin>arsxafp -c 12 -l 8 -o 90 C:\cmod\SampleAFP.afp > SampleAFP.lin`

**Note**: *Pop-up messages are displayed where the default character sets required must be replaced with the available defaults on the system*

The prompt pop-up window was displayed, which we selected **`No`**, as shown in *[Figure 14.1](#c14.xhtml_fig14_1)*:

![](images/Figure14.1.jpg)

**Figure 14.1:** The prompt pop-up window was displayed and we select the ***No*** command button

The second prompt pop-up window was displayed, which we selected **`No`**, as shown in *[Figure 14.2](#c14.xhtml_fig14_2)*:

![](images/Figure14.2.jpg)

**Figure 14.2:** The second prompt pop-up window was displayed and we select the ***No*** command button

The **`arsxafp`** program creates an output file in **`SampleAFP.lin`**, as highlighted in *[Figure 14.3](#c14.xhtml_fig14_3)***:**

![](images/Figure14.3.jpg)

**Figure 14.3:** The ***arsxafp*** program creates an output file in ***SampleAFP.lin***

The output written to the **`SampleAFP.lin`** file can then be checked in **`notepad.exe`** for the performance of the extraction of text, compared with the **`SampleAFP.afp`** appearance in the **AFP Workbench Viewer** program. With the **`-o 90`** switch setting, we get the following, as displayed in *[Figure 14.4](#c14.xhtml_fig14_4)***:**

![](images/Figure14.4.jpg)

**Figure 14.4:** The ***SampleAFP.lin*** output from the arsxafp program using the ***-o 90*** switch setting

So, we retried the command for **`arsxafp`** on Windows with the **`-o 0`** switch setting and additionally add the **`-x`** switch, which suppresses the line characters, which we just send to the default **`stdout`** console window, as shown in *[Figure 14.5](#c14.xhtml_fig14_5)*:

`C:\Program Files\ibm\OnDemand\V10.5\bin>arsxafp -c 12 -l 8 -o 0 -x C:\cmod\SampleAFP.afp`

![](images/Figure14.5.jpg)

**Figure 14.5:** With the ***-o 0*** switch setting and additionally we have added the ***-x*** switch

This command provided a much better output, as shown in *[Figure 14.5](#c14.xhtml_fig14_5)***,** which we can then send to a **`SampleAFP_V2.lin`** output file, without the **-x** switch. The **`SampleAFP_V2.lin`** file loaded in the **notepad.exe** program, using

`C:\Program Files\ibm\OnDemand\V10.5\bin>arsxafp -c 12 -l 8 -o 0 C:\cmod\SampleAFP.afp > SampleAFP_V2.lin` is shown in *[Figure 14.6](#c14.xhtml_fig14_6)*:

![](images/Figure14.6.jpg)

**Figure 14.6:** The ***SampleAFP_V2.lin*** file loaded in the ***notepad.exe*** program, run without the ***-x*** switch

Sometimes, if the **`arsaxfp`** program fails to process an **AFP** file on the Windows server platform, it will process the same **AFP** file correctly on the Linux environment.

Running the **`arsaxfp`** program installed on the Windows server, using the **insure.afp** example data from the installation of the **AFP** viewer as follows:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`arsxafp -c 12 -l 8 -o 0 -x  C:\cmod\insure.afp`** did not give any output (see *[Figure 14.5](#c14.xhtml_fig14_5)),* but the same **`insure.afp`** file, using the same parameters on the **Linux** server install, were copied and run as follows:

`[root@ECMUKDEMO22 ~]#` **`cp /root/eclipse-workspace/ODAPI_Tests/insure.afp /opt/ibm/ondemand/V10.5/bin`**

`[root@ECMUKDEMO22 ~]#` **`su - archive`**

**`Last login: Wed Jul 10 05:17:14 PDT 2024 on pts/1`**

`[archive@ECMUKDEMO22 ~]$` **`cd /opt/ibm/ondemand/V10.5/bin`**

`[archive@ECMUKDEMO22 bin]$` **`./arsxafp -c 12 -l 8 -o 0 -x insure.afp`** gave the output displayed in *[Figure 14.7](#c14.xhtml_fig14_7):*

![](images/Figure14.7.jpg)

**Figure 14.7:** The Linux command ***./arsxafp -c 12 -l 8 -o 0 -x insure.afp*** gave the output shown

So, we then tried the **`SampleAFP.afp`** file on the Linux server, using the same command as on Windows, to see if the Linux server could handle both example files, as shown in *[Figure 14.8](#c14.xhtml_fig14_8)***:**

`./arsxafp -c 12 -l 8 -o 0 -x SampleAFP.afp`

![](images/Figure14.8.jpg)

**Figure 14.8:** The ***SampleAFP.afp*** file on Linux, using ***./arsxafp -c 12 -l 8 -o 0 -x SampleAFP.afp***

The sample files **`insure.afp`** and **`SampleAFP.afp`**, were examined in the **AFP Workbench Viewer** program to verify that the extracted text matched the output of the **`arsxafp`** program, as shown in *[Figure 14.9](#c14.xhtml_fig14_9)*, for **`insure.afp`**:

![](images/Figure14.9.jpg)

**Figure 14.9:** The sample ***insure.afp*** file in the ***AFP Workbench Viewer*** program

The sample **`SampleAFP.afp`** file in the **AFP Workbench Viewer** program is displayed in *[Figure 14.10](#c14.xhtml_fig14_10):*

![](images/Figure14.10.jpg)

**Figure 14.10:** The sample ***SampleAFP.afp*** file in the ***AFP Workbench Viewer*** program

The **`insure.afp`** sample file was copied from the **Ricoh AFP Workbench Viewer** program installation **data** directory, as shown in *[Figure 14.11](#c14.xhtml_fig14_11)***:**

![](images/Figure14.11.jpg)

**Figure 14.11:** The ***insure.afp*** sample file, copied from the ***AFP Workbench Viewer*** program install ***data*** directory

The **`SampleAFP.afp`** file was copied from the **c:\cmod** example data directory, as shown in *[Figure 14.12](#c14.xhtml_fig14_12)*:

![](images/Figure14.12.jpg)

**Figure 14.12:** The ***SampleAFP.afp*** file was copied from the ***c:\cmod*** example data directory

# [Conclusion](#toc.xhtml_s209a)

In this chapter, we understood how to process an **AFP** input file located in a directory and redirect the line data output to a file using the **IBM CMOD** **ARSXAFP** program on the Windows and Linux server environments.

In the next *[Appendix A section, IBM Content Manager OnDemand Fix Pack Installation](#appa.xhtml),* we will cover the download extraction and installation of the Windows Fix Pack 7 for **IBM Content Manager OnDemand** version 10.5 and the running of the Windows **IBM Configurator** program. We then describe the changes to the **Baxter Bay Credit Application** group required as a prerequisite to the running of the Windows Server **ARSLOAD** program.

# [Points to Remember](#toc.xhtml_s210a)

*   Pop-up messages are displayed on windows for the **`arsxafp`** program, where the default character sets required must be replaced with the available defaults on the system.
*   The -o (Page rotation angle) parameter is very important for the correct extraction of the text line data. The example AFP files we have used, required the default 0-degree settings.
*   Sometimes, if the **`arsaxfp`** program fails to process an **AFP** file on the Windows server platform, it will process the same **AFP** file correctly on the Linux environment.
*   The **`-x`** switch for the arsxafp program command suppresses the horizontal and vertical line characters from the output.

# [Multiple Choice Questions](#toc.xhtml_s211a)

1.  Which switch option controls the page rotation expected in the input **AFP** file, using the **`arsxafp`** program?
    1.  -r
    2.  -o
    3.  -f
    4.  -t
2.  Which switch option controls the suppression of horizontal and vertical line characters in the output stdout character stream, using the **`arsxafp`** program?
    1.  -f
    2.  -t
    3.  -x
    4.  -y

# [Answers](#toc.xhtml_s212a)

1.  b
2.  c

# [Questions](#toc.xhtml_s213a)

1.  What would one option be if the following command failed to produce any output?

    `C:\Program Files\ibm\OnDemand\V10.5\bin>`**`arsxafp -c 12 -l 8 -o 0 -x C:\cmod\insure.afp`**

2.  Why do you think the size of storage for the **`insure.lin`** output file (**38880** disk blocks) is so much smaller than for the **insure.afp** input file (**61207** disk blocks) processed by the **`arsxafp`** program?

    (Found using the **`ls -lsa insure.*`** Linux command)

    60 -rwxr-xr-x.  1 root    root **61207** Jul 10 07:10 **insure.afp**

    40 -rw-r--r--.  1 archive db2iadm1    **38880** Jul 11 09:49 **insure.lin)**

# [Key Terms](#toc.xhtml_s214a)

*   **AFP**: AFP is the shortened form of **Advanced Function Presentation**, a high-speed, streamed format for printing on the **IBM i** Series servers, composed by generating full pages of data, rather than splitting the output into 132-character lines.
*   **IBM CMOD:** It is the shortened form used for **IBM Content Manager OnDemand.**

# [APPENDIX A](#toc.xhtml_appa)

# [IBM Content Manager OnDemand Fix Pack Installation](#toc.xhtml_appa)

# [Introduction](#toc.xhtml_s215a)

This Appendix covers the download extraction and installation of the Windows and Linux **Fix Pack 7** for **IBM Content Manager OnDemand** version 10.5 and the running of the Windows **IBM OnDemand Configurator** program. We then describe the changes to the **Baxter Bay Credit Application** group required as a prerequisite to the running of the Windows Server **ARSLOAD** program.

# [Structure](#toc.xhtml_s216a)

In this Appendix, we will discuss the following topics:

*   Downloading the **CMOD** Fix Pack
*   Linux Server Start Up
*   First Run of **`ARSLOAD`** after Configuration
    *   Updated Fields for Loading
*   Second Run of the **`ARSLOAD`** Program

# [Downloading the CMOD Fix Pack](#toc.xhtml_s217a)

1.  We have to search the **IBM Fix Central** website to identify the latest **IBM Content Manager OnDemand** fix for our base installation of **IBM CMOD 10.5.0.0**. as shown in *[Figure A.1](#appa.xhtml_figA_1).*

    See [https://www.ibm.com/support/fixcentral](https://www.ibm.com/support/fixcentral)

    ![](images/Figure_A.1.jpg)

    **Figure A.1:** Searching the ***IBM Fix Central*** website to identify the latest ***IBM Content Manager OnDemand*** fix

2.  The **`Support & documentation`** tab has **`the IBM Content Manager OnDemand for`** **`Multiplatforms Version 10.5.0.7`** link, which supports the **Windows** and **Linux** server download platforms, as highlighted in *[Figure A.2](#appa.xhtml_figA_2)***:**

    ![](images/Figure_A.2.jpg)

    **Figure A.2:** The ***Support & documentation*** tab has the ***IBM CMOD for*** ***Multiplatforms Version 10.5.0.7*** link

3.  The **Fix Pack** **10.5.0.7** details can be seen, clicking on the highlighted **`10.5.0.7-CMODMP-Windows-CLIENT`** link, as shown in *[Figure A.3](#appa.xhtml_figA_3)*:

    ![](images/Figure_A.3.jpg)

    **Figure A.3:** The Fix Pack ***10.5.0.7*** details can be seen, clicking on the ***10.5.0.7-CMODMP-Windows-CLIENT*** link

4.  We are prompted to log into the **IBM** website using an **`IBMid`,** to allow us to search and download Fix Packs, as shown in *[Figure A.4](#appa.xhtml_figA_4)*:

    ![](images/Figure_A.4.jpg)

    **Figure A.4:** We are prompted to log into the ***IBM*** web-site using an ***IBMid*** to search and download Fix Packs

5.  We are prompted to enter the **IBMid** user’s password, as shown in *[Figure A.5](#appa.xhtml_figA_5)***:**

    ![](images/Figure_A.5.jpg)

    **Figure A.5:** We are prompted to enter the ***IBMid*** user’s password

6.  The **Fix Pack** details highlighted as **`10.5.0.7-CMODMP-Windows-CLIENT (385.03 MB)`**, can be downloaded by clicking the **`Download now`** command button, as shown in *[Figure A.6](#appa.xhtml_figA_6)***:**

    ![](images/Figure_A.6.jpg)

    **Figure A.6:** The Fix Pack details highlighted as ***10.5.0.7-CMODMP-Windows-CLIENT (385.03 MB)***, can be downloaded by clicking on the ***Download now*** command button

7.  The pop-up window for the **IBM Download Director** application program is shown to prompt for the program to be run, as highlighted in *[Figure A.7](#appa.xhtml_figA_7)***:**

    ![](images/Figure_A.7.jpg)

    **Figure A.7:** The pop-up window for the ***IBM Download Director*** application program is shown

8.  We can now select the **`Run`** command button to launch the **IBM CMOD** Fix Pack Download, as shown in *[Figure A.8](#appa.xhtml_figA_8)***:**

    ![](images/Figure_A.8.jpg)

    **Figure A.8:** We can now select the ***Run*** command to launch the ***IBM CMOD*** Fix Pack version ***10.5.0.7*** Download

9.  The status of each of the file downloads for the **IBM Content Manager OnDemand** Multiplatform Fix Pack download files is shown in *[Figure A.9](#appa.xhtml_figA_9)***:**

    ![](images/Figure_A.9.jpg)

    **Figure A.9:** The status of the file downloads for the ***IBM Content Manager OnDemand*** Multiplatform Fix Pack

10.  The **`Details`** command is selected to list each of the Fix Pack **IBM CMOD** client files, as shown in *[Figure A.10](#appa.xhtml_figA_10)***:**

    ![](images/Figure_A.10.jpg)

    **Figure A.10:** The ***Details*** command is selected to list each of the Fix Pack files

11.  The **`DownloadDirector`** directory shows the highlighted **IBM CMOD Version 10.5.0.7** Fix Pack installation files, **`odwin64.zip`** and **`odwin32.zip`**, as highlighted in *[Figure A.11](#appa.xhtml_figA_11)***:**

    ![](images/Figure_A.11.jpg)

    **Figure A.11:** The ***DownloadDirector*** directory shows the highlighted ***IBM CMOD Version 10.5.0.7*** Fix Pack installation files, ***odwin64.zip*** and ***odwin32.zip***

12.  The **`odwin64.zip`** Fix Pack **Version 10.5.0.7** for the **IBM Content Manager OnDemand Client** installation is shown being copied from the **`DownloadDirector`** folder to the **`c:\CMOD_10.5.0.7FixPack`** install folder, as shown in *[Figure A.12](#appa.xhtml_figA_12)***:**

    ![](images/Figure_A.12.jpg)

    **Figure A.12:** The ***odwin64.zip*** Fix Pack ***Version 10.5.0.7*** for the ***IBM Content Manager OnDemand Client*** is copied

13.  Before the installation of the **Fix Pack 7** upgrade from the base system, **IBM CMOD 10.5.0.0**, the **IBM** **OnDemand Configurator** is used to stop the four supporting Windows services, as shown highlighted in *[Figure A.13](#appa.xhtml_figA_13)***:**

    ![](images/Figure_A.13.jpg)

    **Figure A.13:** The ***IBM*** ***OnDemand Configurator*** is used to stop the four supporting Windows services

14.  The **right-mouse** click on the Windows **`odwin64.zip`** is used to extract the install files to a **`c:\CMOD_10.5.0.7FixPack\odwin64`** subfolder, as shown in *[Figure A.14](#appa.xhtml_figA_14)***:**

    ![](images/Figure_A.14.jpg)

    **Figure A.14:** The right-mouse click on the Windows ***odwin64.zip*** is used to extract the install files to a ***c:\CMOD_10.5.0.7FixPack\odwin64*** subfolder

15.  The list of install files, in the **`c:\CMOD_10.5.0.7FixPack\odwin64`** subfolder, includes the **`setup.exe`** program which we have to select, as shown highlighted in *[Figure A.15](#appa.xhtml_figA_15)***:**

    ![](images/Figure_A.15.jpg)

    **Figure A.15:** The install files in the ***c:\CMOD_10.5.0.7FixPack\odwin64*** subfolder, with the ***setup.exe*** program

16.  Clicking the **`setup.exe`** program allows us to select the **`Modify`** radio button option and then click the **`Next >`** command button, as highlighted in *[Figure A.16](#appa.xhtml_figA_16)***:**

    ![](images/Figure_A.16.jpg)

    **Figure A.16:** Clicking the ***setup.exe*** program allows us to select the ***Modify*** radio button option and then click the ***Next >*** command button

17.  We can now select the **IBM OnDemand** client programs to be installed, **`Client`,** **`Administrator`** and **`Monitor`** and select the **`Next >`** command button, as shown highlighted in *[Figure A.17](#appa.xhtml_figA_17)***:**

    ![](images/Figure_A.17.jpg)

    **Figure A.17:** We select the ***IBM OnDemand*** client programs to be installed, ***Client, Administrator*** and ***Monitor***

18.  We can see the summary list of the **Current Settings** and the **Components** to be installed and then select the **`Next >`** command button, as highlighted in *[Figure A.18](#appa.xhtml_figA_18)***:**

    ![](images/Figure_A.18.jpg)

    **Figure A.18:** We can see the summary list of the ***Current Settings*** and the ***Components*** to be installed

19.  After the installation is completed, we have an option to reboot the **Windows** server, as shown in *[Figure A.19](#appa.xhtml_figA_19)***:**

    ![](images/Figure_A.19.jpg)

    **Figure A.19:** After the installation is completed, we have an option to reboot the Windows server

# [Linux Server Start Up](#toc.xhtml_s218a)

After the **Fix Pack 7** was applied on the **Windows** server, we also applied the **Fix Pack 7** to our **Linux** server.

**Note:** *This is important to keep the* ***Windows*** *and* ***Linux*** *servers in step, because we are using the* ***ODWEK*** ***Java*** ***API*** *libraries to integrate the* ***IBM Content Navigator*** *Desktop running on* ***Linux****, with the* ***IBM CMOD*** *system running on the* ***Windows*** *server to ensure any serialized* ***Java*** *objects and the* ***API*** *call interfaces are compatible.*

After updating the **Linux** server **IBM CMOD Fix Pack 7**, we had to reboot and restart the **Linux** server as follows:

`[root@ECMUKDEMO22 ~]#` **`su - archive`**

`Last login: Wed Apr 10 05:37:42 PDT 2024 on pts/0`

`[archive@ECMUKDEMO22 ~]$` **`db2 start database manager`**

`SQL1026N  The database manager is already active.`

`[archive@ECMUKDEMO22 ~]$` **`db2 activate database archive`**

`DB20000I  The ACTIVATE DATABASE command completed successfully.`

`[archive@ECMUKDEMO22 ~]$` **`/opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S`**

`[archive@ECMUKDEMO22 ~]$ ARS0351I The arssockd instance ARCHIVE is ready`

`[root@ECMUKDEMO22 ~]#` **`ps -eaf|grep arsobjd`**

`archive     4694    3615  0 12:34 pts/0    00:00:00 arsobjd: (accepting)`

`root        4876    4835  0 12:36 pts/1    00:00:00 grep --color=auto arsobjd`

`[root@ECMUKDEMO22 ~]#` **`lsof -i :1445`**

`COMMAND   PID    USER   FD   TYPE DEVICE SIZE/OFF NODE NAME`

`arssockd 4694 archive    4u  IPv6  69244      0t0  TCP *:proxima-lm (LISTEN)`

`[root@ECMUKDEMO22 ~]#`

After the download and unpacking of the **Linux** **`README.txt`** file, we can review the recommendations for the supporting **Java** library .jar files, used for the **`ODWEK`** **API,** as highlighted in the following text:

From the latest installation **README** file, release dated **Apr. 26, 2024**, which can also be downloaded separately from the link:

([https://www.ibm.com/support/pages/system/files/inline-files/README_10.5.0.8_2024-05-06.txt](https://www.ibm.com/support/pages/system/files/inline-files/README_10.5.0.8_2024-05-06.txt) )

`2.1.1.10.5.0.8) Release` **`(10.5.0.8)`**

`- The ARSACIF command is now available as a 64-bit executable.` `To use`

`this new ARSACIF64, you will have to set the environment variable`

`ARS_USE_ACIF64=1 in your arsload environment.` `You will also have to`

`recompile your acif exits as 64-bit and put them in the exits/acif64`

`directory`

`- Updated list of jar files to include in the CLASSPATH for specific`

`Java features of Content Manager OnDemand:`

**`ODWEK Java API (ODApi.jar)`**

**`gson-2.10.1.jar`**

**`log4j-api-2.23.1.jar`**

**`log4j-core-2.23.1.jar`**

`Full Text Search Exporter (ODFTIExporter.jar)`

`ecmts.jar`

`commons-collections4-4.4.jar`

`commons-configuration2-2.10.1.jar`

`commons-lang3-3.14.0.jar`

`commons-logging-1.3.1.jar`

`commons-pool2-2.12.1.jar`

`commons-text-1.11.0.jar`

`gson-2.10.1.jar`

`log4j-api-2.23.1.jar`

`log4j-core-2.23.1.jar`

`<database specific JDBC jar file(s)>`

`CFS-CMOD Exporter (CFSODExporter.jar)`

`<database specific JDBC jar file(s)>`

`arssupport (arssupport.jar)`

`No dependencies`

`REST Services APIs (cmod-rest.war)`

**`commons-pool2-2.12.1.jar`**

**`gson-2.10.1.jar`**

**`log4j-api-2.23.1.jar`**

**`log4j-core-2.23.1.jar`**

**`ODApi.jar`**

`REST Admin (ODRESTAdmin.jar)`

`No dependencies`

`3.6.10.5.0.8) Release (10.5.0.8)`

`Here is the current list of jar files to include in the CLASSPATH for`

`ODWEK Java API of Content Manager OnDemand:`

`ODWEK Java API (`**`ODApi.jar`**`)`

**`gson-2.10.1.jar`**

**`log4j-api-2.23.1.jar`**

**`log4j-core-2.23.1.jar`**

# [First Run of ARSLOAD After Configuration](#toc.xhtml_s219a)

The first run of the **`ARSLOAD`** program, after the Fix Pack upgrade, was used to check the installation of the latest available **IBM Content Manager OnDemand** Version **10.5.0.7**. This is covered in detail in *[Chapter 13, Running ARSLOAD](#c13.xhtml)*.

We tested using the command as follows:

`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ARSLOAD  -u ADMIN -p c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`

This run indicated that the first deployment of the **Baxter Bat Credit Application** group was missing the four fields listed as follows, from the example in our test file **Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit.ind:**

# [Updated Fields for Loading](#toc.xhtml_s220a)

`GROUP_FIELD_NAME:`**`name`**

`GROUP_FIELD_VALUE:SMITH CYCLERY CO`

`GROUP_FIELD_NAME:`**`account`**

`GROUP_FIELD_VALUE:000-000-000`

`GROUP_FIELD_NAME:`**`crd_date`**

`GROUP_FIELD_VALUE:04/03/95`

`GROUP_FIELD_NAME:`**`balance`**

`GROUP_FIELD_VALUE:1058.110000`

# [Second Run of the ARSLOAD Program](#toc.xhtml_s221a)

The following command was tried next, which was also covered in *[Chapter 13, Running ARSLOAD](#c13.xhtml).*

`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ARSLOAD  -u ADMIN -p c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`

This indicated that we needed to update the existing **Baxter Bay Credit** **Application** group which we will cover in *Appendix B, Recreating an Application Group*.

We had the error:

`2024-04-12 23:29:49.544889: ARS1130E 4 fields submitted by the indexer, 10 expected`

**Note***: The first build of the* ***Baxter Bay Credit Application*** *group had 10 fields, but we discovered that we only require 4 of these as listed in the Section, “First run of* ***ARSLOAD*** *after configuration”.*

# [Conclusion](#toc.xhtml_s222a)

This **[Appendix A](#appa.xhtml)** covered the download and installation of the Windows and Linux **Fix Pack 7** for **IBM Content Manager OnDemand** version **10.5.0.0** and the running of the Windows **IBM Configurator** program. We then described the changes to the **Baxter Bay Credit Application** group, required as a prerequisite to the running of the Windows Server **ARSLOAD** program.

In the next appendix, we will describe the step-by-step procedure required to remove and re-add an **IBM CMOD** application group, **Baxter Bay Credit**.

# [Points to Remember](#toc.xhtml_s223a)

*   It is important to keep the Windows and Linux servers in step with regard to Fix Pack versions, because we are using the **`ODWEK`** Java API libraries to integrate the IBM Content Navigator Desktop running on Linux, with the IBM CMOD system running on the Windows server. This ensures that any serialized Java objects and the API call interfaces are compatible.
*   Before installing the Windows Fix Pack, it is important to stop any running services.
*   After installing a Fix Pack, it is recommended that the Linux and Windows servers are rebooted.

# [Multiple Choice Questions](#toc.xhtml_s224a)

1.  Which IBM program is used to stop the Windows Services before starting the Fix Pack installation for **IBM Content Manager OnDemand**?
    1.  `IBM ARSLOAD`
    2.  `IBM OnDemand Configurator`
    3.  `IBM OnDemand Administrator`
    4.  `IBM Download Director`
2.  The order of restarting the support programs on Linux after rebooting the Fix Pack update, is as follows:
    1.  `/opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S, db2 activate database archive, db2 start database manager`
    2.  `db2 activate database archive, db2 start database manager, /opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S`
    3.  `/opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S, db2 start database manager, db2 activate database archive`
    4.  `db2 start database manager, db2 activate database archive, /opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S`

# [Answers](#toc.xhtml_s225a)

1.  b
2.  d

# [Questions](#toc.xhtml_s226a)

1.  What are some of the reasons for maintaining the **IBM Content Manager OnDemand** program with the latest Fix Pack (reviewing the Fix Pack **`README.txt`** file should provide some example reasons)?
2.  Why would you need to maintain a **Windows** **IBM CMOD** system at the same Fix Pack level as a **Linux IBM CMOD** installation?

# [Key Terms](#toc.xhtml_s227a)

*   **`ODWEK`** **API**: The OnDemand Web Enablement Kit, **`ODWEK`** provides an Application Programmers Interface which can be called to run server methods to store and retrieve documents, update passwords or delete a document.
*   **REST:** Representational State Transfer (REST) is a software protocol for communications using an API (Application Programmers Interface) to a web network interface to call server methods from a client using a URL format.

# [APPENDIX B](#toc.xhtml_appb)

# [Recreating an Application Group](#toc.xhtml_appb)

# [Introduction](#toc.xhtml_s228a)

In this Appendix, we will cover the step-by-step procedure required to remove and re-add an **IBM CMOD** application group, demonstrated for the **Baxter Bay Credit Application Group,** which we modified to allow the successful upload of our test data, using the **Windows** **`ARSLOAD`** program, described in *[Chapter 13, Running ARSLOAD](#c13.xhtml)*.

We will describe the procedure used to delete the original **Baxter Bay Credit** **Application Group** and then add this back with an updated set of **Index Fields**. This procedure is required when the original **Index Field** **Type** is set with an incompatible type from the type expected by the **ARSLOAD** program, which it derives from the data to be loaded.

# [Structure](#toc.xhtml_s229a)

In this appendix, we will discuss the following topics:

*   Deleting an Existing Application Group
*   Creating a New Application Group
    *   Third Run Issue with Date
    *   Fourth Run Success After Editing the Data File

# [Deleting an Existing Application Group](#toc.xhtml_s230a)

We found that we could not change some of the **Index Field** types of the first deployment of our **Baxter Bay Credit Application** group, as described in *[Chapter 13, Running ARSLOAD](#c13.xhtml),* so the only solution for successfully loading the example data was to delete and rebuild the group, as follows:

1.  First, we load the program from the Windows Explorer, **`OnDemand Administrator V10.5 (64-bit)`**, from the subfolder **`IBM OnDemand Clients V10.5 (64-bit)`**, as shown in *[Figure B.1](#appb.xhtml_figB_1)*:

    ![](images/Figure_B.1.jpg)

    **Figure B.1:** Select the ***OnDemand Administrator V10.5 (64-bit)*** program

2.  We are prompted to log on to the Windows Server using the **OnDemand Administrator V10.5 (64-bit)** program by right-clicking the server name in the menu tree and selecting the **`Logon`** menu item, as highlighted in *[Figure B.2](#appb.xhtml_figB_2)***:**

    ![](images/Figure_B.2.jpg)

    **Figure B.2:** Logon to the Server using the ***OnDemand Administrator*** by right-clicking the server name

3.  We enter the **`ADMIN`** administration user’s **`User ID`** and **`Password`** into our **`DESKTOP-B3JB93R`** server and enter the **`OK`** command button, as highlighted in *[Figure B.3](#appb.xhtml_figB_3)*:

    ![](images/Figure_B.3.jpg)

    **Figure B.3:** We enter the ***ADMIN*** administration user’s ***User ID*** and ***Password*** into our ***DESKTOP-B3JB93R*** server

4.  After selecting the **Applications Groups** from the navigation Tree panel on the left side of the program, we can see the **`Baxter Bay Credit`** Applications Group name and then we can right-click and select the **`Delete`** menu item, as highlighted in *[Figure B.4](#appb.xhtml_figB_4)*:

    ![](images/Figure_B.4.jpg)

    **Figure B.4:** The ***Baxter Bay Credit*** name is selected and right-clicked for the ***Delete*** menu item

5.  A second security logon is prompted to confirm that we are authorized to delete the **`Baxter Bay Credit`** Application Group, as highlighted in *[Figure B.5](#appb.xhtml_figB_5)***:**

    ![](images/Figure_B.5.jpg)

    **Figure B.5:** A second security logon is prompted to confirm that we are authorized to delete ***Baxter Bay Credit***

6.  We still have a chance to back out of the delete action, by using the **`Cancel`** command button; but we select the **`OK`** command button from the pop-up window to complete the delete action process, as illustrated in *[Figure B.6](#appb.xhtml_figB_6)*:

    ![](images/Figure_B.6.jpg)

    **Figure B.6:** We select the ***OK*** command button from the pop-up window to complete the delete action

7.  The serious nature of deleting anything in the **IBM OnDemand** system is now emphasized, since we get a second window (and another opportunity) to use a **`Cancel`** command to cancel the delete operation for the **Baxter Bay Credit Application Group**.

    We affirm the deletion operation in this final window by selecting the **`Yes`** command button, as highlighted in *[Figure B.7](#appb.xhtml_figB_7)*:

    ![](images/Figure_B.7.jpg)

    **Figure B.7:** We affirm the deletion operation in this final window by selecting the ***Yes*** command button

**Add back the Application Group**

8.  The highlighted **`Application Groups`** tree node now shows just the two remaining **IBM CMOD** system generated **`Application Groups`**, **`System Load`** and **`System Log`**, as illustrated in *[Figure B.8](#appb.xhtml_figB_8)*:

    ![](images/Figure_B.8.jpg)

    **Figure B.8:** The ***Application Groups*** tree node shows the two remaining ***IBM CMOD Application Groups***

9.  In the next section, we will follow the next step which is the procedure to recreate the **`Baxter Bay Credit`** Application Group.

# [Creating a New Application Group](#toc.xhtml_s231a)

1.  The **`Application Groups`** tree node is selected and the **`New Application Group`** menu item is selected to start the creation of a new **Baxter Bay Credit** version, as highlighted in *[Figure B.9](#appb.xhtml_figB_9)***:**

    ![](images/Figure_B.9.jpg)

    **Figure B.9:** The ***Application Groups*** tree node is selected and the ***New Application Group*** menu item is selected

2.  The **`General`** tab is used to enter the **`Name`** and **`Description`** fields for **Baxter Bay Credit** and then the **`Advanced…`** command button is selected to enter the required options. We alter the default **`No`** option (highlighted) to **`Yes`** for use with the **Content Federation Services** (**CFS-CMOD**), as illustrated in *[Figure B.10](#appb.xhtml_figB_10)***:**

    ![](images/Figure_B.10.jpg)

    **Figure B.10:** We alter the default ***No*** option to ***Yes*** for use with the ***Content Federation Services (CFS-CMOD)***

3.  We can now enter the fields we require, as follows:

    `GROUP_FIELD_NAME:`**`name`**

    `GROUP_FIELD_VALUE:SMITH CYCLERY CO`

    `GROUP_FIELD_NAME:`**`account`**

    `GROUP_FIELD_VALUE:000-000-000`

    `GROUP_FIELD_NAME:`**`crd_date`**

    `GROUP_FIELD_VALUE:04/03/95`

    `GROUP_FIELD_NAME:`**`balance`**

    `GROUP_FIELD_VALUE:1058.110000`

    Each field name is entered into the **Database Field Name** text box in the **`Field Definition`** tab, and the **`Add`** command selected to push it to the **Names List** column window, as shown in *[Figure B.11](#appb.xhtml_figB_11)***:**

    ![](images/Figure_B.11.jpg)

    **Figure B.11:** Each field name is entered into the ***Database Field Name*** text box in the ***Field Definition*** tab, and the ***Add*** command selected

4.  Next, we select the **`Field Information`** tab and we can now select each Field in turn from the **`Name`** dropdown box and enter the required **`Type`**, **`Data Type`**, **`Case`**, **`Type`** and **`Length`**, as illustrated in *[Figure B.12](#appb.xhtml_figB_12)***:**

    ![](images/Figure_B.12.jpg)

    **Figure B.12:** Select each Field in turn from the ***Name*** dropdown box and enter the required ***Type***, ***Data Type***, ***Case***, ***Type*** and ***Length***

5.  The **`name`** field is used by **Baxter Bay Credit** for the **account name**, and we set the **`Data Type`** as **`String`** and the **`Type`** as **`Filter`**, which will enable its use as a search field. The string length is set as the maximum allowed of **`254`** characters, as shown in *[Figure B.13](#appb.xhtml_figB_13):*

    ![](images/Figure_B.13.jpg)

    **Figure B.13:** The maximum ***String*** field length is set at 254 characters for the ***name*** field

    **Note***: The maximum* ***String*** *field length is 254 characters.*

6.  The **`account`** field parameters are defined to provide a **`Fixed`** **String** type of 11 characters, as shown in *[Figure B.14](#appb.xhtml_figB_14):*

    ![](images/Figure_B.14.jpg)

    **Figure B.14:** The ***account*** field parameters are defined to provide a ***Fixed String*** type of 11 characters

7.  The **`crd_date`** field parameters are defined so that the field is set as a **`Date`** with a **`Filter`** type, to enable searching. The **`segment`** box is ticked which determines the delete point for the application group data, as shown in *[Figure B.15](#appb.xhtml_figB_15)*:

    ![](images/Figure_B.15.jpg)

    **Figure B.15:** There must be a segment field defined. Also, the new date format was selected for a working load

8.  The **`balance`** field is selected to add the required parameters to define the field as Floating point (**`Data Type`**, **`DecFloat(16)`** ) and then we select the **`Advanced Index Information`** tab, as highlighted in *[Figure B.16](#appb.xhtml_figB_16)*:

    ![](images/Figure_B.16.jpg)

    **Figure B.16:** The ***balance*** field is selected to define the field as Floating point (***Data Type, DecFloat(16)*** )

9.  The **`Advanced Index Information`** tab allows the construction of a multiple field database **Index** for searching and processing for reports. We select the **`Add…`** command button and can then move the **`name`** and **`account`** fields from the **`Available Fields`** list to the **`Selected Fields`** list, using the **`Add >>`** command to form an **`Index 1`** database field, as shown in *[Figure B.17](#appb.xhtml_figB_17)*:

    ![](images/Figure_B.17.jpg)

    **Figure B.17:** The ***Advanced Index Information*** tab allows the construction of a multiple field database ***Index*** for searching and processing for reports

10.  The **`Permissions`** tab is selected to specify the required Security **`Users`** and **`Groups`**. We select all the available **`Groups`**, using the **`Add>>`** command button, as shown in *[Figure B.18](#appb.xhtml_figB_18):*

    ![](images/Figure_B.18.jpg)

    **Figure B.18:** The ***Permissions*** tab is selected and the ***Add>>*** to specify the required ***Security Users*** and ***Groups***

11.  The **`Storage Management`** tab is selected and we use the **`Cache Only - Library Server`** drop-down option, as shown in *[Figure B.19](#appb.xhtml_figB_19)*:

    ![](images/Figure_B.19.jpg)

    **Figure B.19:** The ***Storage Management*** tab is selected and we use the ***Cache Only - Library Server*** drop-down

12.  Finally, back on the **`Field Information`** tab, we select the **`Unique ID`** tick-box for the **`account`** field.

    ![](images/Figure_B.20.jpg)

    **Figure B.20:** On the ***Field Information*** tab, we select the ***Unique ID*** tick-box for the ***account*** field

13.  On selecting the **`OK`** command button on the **`Add an Application Group`** window, we can see that our **`Baxter Bay Credit Application Group`** is now in the list, showing as modified by the **`ADMIN`** user, as highlighted in *[Figure B.21](#appb.xhtml_figB_21)*:

    ![](images/Figure_B.21.jpg)

    **Figure B.21:** On selecting the ***OK*** command button on the ***Add an Application Group*** window, we can see that our ***Baxter Bay Credit*** Application Group is in the list

14.  We can now select the **`Applications`** node and right-click and select the **`New Application`** menu item to load the **`Add an Application`** window and use the **`Select…`** command to select our **`Baxter Bay Credit`** **Applications Group** we have created to finalize the creation of the **`BaxterBayCredit`** **Application,** as shown in *[Figure B.22](#appb.xhtml_figB_22)*:

    ![](images/Figure_B.22.jpg)

    **Figure B.22:** Select the ***Applications*** node and right-click and select the ***New Application*** menu item

15.  On the **`Add an Application`** window, we can now select the **`Logical Views`** tab and add the **`ADMIN`** user from the **`Users`** list to the **`Users with Logical Views`** list using the **`Add>>`** command button, as shown in *[Figure B.23](#appb.xhtml_figB_23)*:

    ![](images/Figure_B.23.jpg)

    **Figure B.23:** On the ***Add an Application*** window we select the ***Logical Views*** tab and add the ***ADMIN*** user

16.  On selecting the **`OK`** command button on the **`Add an Application`** window, we can see the new **BaxterBayCredit Application** we created in the list of **IBM CMOD** **System** created **`Applications`**, as shown in *[Figure B.24](#appb.xhtml_figB_24)*:

    ![](images/Figure_B.24.jpg)

    **Figure B.24:** Selecting the ***OK*** command button on the ***Add an Application*** window, we can see the new ***BaxterBayCredit Application***

17.  Using the right-click on the **BaxterBayCredit** Application we created (shown highlighted in *[Figure B.24](#appb.xhtml_figB_24)*), we can select the **`Properties`** menu item, to load the Window displayed in *[Figure B.25](#appb.xhtml_figB_25)*, and click on the **`Indexer Information`** tab, to select the **`Generic`** Indexer from the dropdown list and then confirm this change using the **`Update`** command button. This is required to allow the data load to process correctly.

    ![](images/Figure_B.25.jpg)

    **Figure B.25:** We select the ***Properties*** menu and click on the ***Indexer Information*** tab, to select a ***Generic Indexer***

We have successfully recreated the **Baxter Bay Credit Applications** **Group.** This enables us to load the test data using the ARSLOAD Windows program, as detailed in the following section.

# [Third Run Issue with Date](#toc.xhtml_s232a)

During this run of the **ARSLOAD** Windows program, we encountered an issue with the **crd_date** field date format, which was in the form **mm/dd/yy**. We discovered from the error message that it needed to be loaded in the new format for the **IBM CMOD** date, **mm/dd/yyyy**.

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSLOAD  -u ADMIN -p ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`**

`2024-04-13 13:40:37.788189: ARS1129E Row 1:  `**`The string "04/03/95" could not be converted to a date from the format of %m/%d/%y %H:%M:%S`**

`2024-04-13 13:40:37.792172: ARS1146I` **`Loaded 0 rows`** `into the database`

`2024-04-13 13:40:37.795168: ARS4311E` **`Loading failed`**

`2024-04-13 13:40:37.799150: ARS4318E` **`Processing failed for file`** `>c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-13 13:40:37.993931: ARS4327E Processing has stopped.  The remaining files will NOT be processed.`

To correct the **Date** **Type** issue, we deleted and re-entered the **Date** field, **`crd_date`** as a **New** **Date** field for the recreated **Baxter Bay Credit Application Group**.

**Note:** *The field types are not editable (the drop-down is greyed out) once they have been entered, so the date type can only be modified after creation of the* ***Application Group*** *by deleting and re-entering the complete* ***Application Group****, as we describe in this Appendix*

We still get a different **Date Index** field error:

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`ARSLOAD  -u ADMIN -p ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`**

`2024-04-13 14:53:07.285932: ARS4315I Processing file >c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-13 14:53:07.442462:` **`ARS1129E Row 1:  The string "04/03/95" could not be converted to a date from the format of %m/%d/%Y`**

`2024-04-13 14:53:07.446452: ARS1146I` **`Loaded 0 rows`** `into the database`

`2024-04-13 14:53:07.449439: ARS4311E` **`Loading failed`**

`2024-04-13 14:53:07.452727: ARS4318E` **`Processing failed for file`** `>c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-13 14:53:07.672154: ARS4327E` **`Processing has stopped`**`.  The remaining files will NOT be processed.`

# [Fourth Run Success After Editing the Data File](#toc.xhtml_s233a)

Next, we edited all occurrences of the date year from **/95** to **/1995**, which worked:

**`c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ARSLOAD  -u ADMIN -p c:\PROGRA~1\ibm\OnDemand\V10.5\bin\ars.stash -h localhost -n -g "Baxter Bay Credit" "c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit"`**

`2024-04-13 15:14:03.711617: ARS1146I` **`Loaded 236 rows into the database`**

`2024-04-13 15:14:03.720583: ARS1175I Document compression type used - OD77.  Bytes Stored = >96860< Rows = >236<`

`2024-04-13 15:14:03.726068:` **`ARS4310I Loading completed`**

`2024-04-13 15:14:03.745986: ARS4317I` **`Processing successful for file`** `>c:\temp\bb\Baxter Bay Credit.3.Baxter Bay Credit.Baxter Bay Credit<`

`2024-04-13 15:14:03.750964:` **`ARS4348I Load Statistics`**`: Index In >714,654<  Load In >714,654<  Load Out >96,860<  Rows >236<  Pages >0<  Time >0.7077<  Resource In >271,127<  Resource Out >6,276<`

# [Creating a New Invoices Folder](#toc.xhtml_s234a)

1.  A new **`Invoices`** folder can be created by right-clicking the **`Folder`** Tree node, as highlighted in *[Figure B.26](#appb.xhtml_figB_26)*:

    ![](images/Figure_B.26.jpg)

    **Figure B.26:** A new Invoices folder can be created by right-clicking the ***Folder*** Tree node

2.  We enter the **`Name`** as **`Invoices`** on the **`General`** tab, as shown in *[Figure B.27](#appb.xhtml_figB_27)*:

    ![](images/Figure_B.27.jpg)

    **Figure B.27:** We enter the ***Name*** as “***Invoices”*** on the ***General*** tab

3.  The **`Permissions`** tab is selected so the required **`Users and Groups`** can be selected using the **`Add>>`** command button, as highlighted in *[Figure B.28](#appb.xhtml_figB_28)*:

    ![](images/Figure_B.28.jpg)

    **Figure B.28:** The ***`Permissions`*** tab is selected so the required ***Users and Groups*** can be selected

4.  The **`Field Definition`** tab is used to enter the **`Year`** **Folder Field**, as highlighted in *[Figure B.29](#appb.xhtml_figB_29)*:

    ![](images/Figure_B.29.jpg)

    **Figure B.29:** The ***Field Definition*** tab is used to enter the ***Year*** Folder Field

5.  The **`Advanced…`** command button is selected (as highlighted in *[Figure B.29](#appb.xhtml_figB_29))* to show the **`Advanced Folder Field Information`** window, as shown in *[Figure B.30](#appb.xhtml_figB_30)*:

    ![](images/Figure_B.30.jpg)

    **Figure B.30:** The ***Advanced…*** command button is selected to show the ***Advanced Folder Field Information*** window

6.  The **`Field Information`** tab is selected to set other **`Year Name`** parameters such as the default value for the field, as shown in *[Figure B.31](#appb.xhtml_figB_31)*:

    ![](images/Figure_B.31.jpg)

    **Figure B.31:** The ***Field Information*** tab is selected to set other ***Year Name*** parameters

7.  After we use the **`Field Information`** tab to set a default **Year** value of **`2024`**, we select the **`OK`** command button, but we prompt a pop-up error box to appear which states that we need to select the **`Default`** check box, as highlighted in *[Figure B.32](#appb.xhtml_figB_32)*:

    ![](images/Figure_B.32.jpg)

    **Figure B.32:** We use the ***Field Information*** tab for a ***Year*** valueand are then prompted for the ***Default*** check box

8.  We select the **`Field Mapping`** tab next, which can be used to associate the folder search and display fields with database fields in application groups. We have nothing we wish to map, so we select the **`OK`** command button to exit the **`Add a Folder`** window, as highlighted in *[Figure B.33](#appb.xhtml_figB_33):*

    ![](images/Figure_B.33.jpg)

    **Figure B.33:** The ***Field Mapping*** tab is used to associate the folder search and display fields with database fields

9.  We can now see the new **`Invoices`** folder in the list of system generated **`Folders`**, as highlighted in *[Figure B.34](#appb.xhtml_figB_34)*:

    ![](images/Figure_B.34.jpg)

    **Figure B.34:** We can now see the new ***Invoices*** folder in the list of system generated Folders

# [Conclusion](#toc.xhtml_s235a)

In this **Appendix**, we covered the step-by-step procedure required to remove and re-add an **IBM CMOD** application group, using the **Baxter Bay Credit Application Group** as an example, which we found was necessary in order to modify the **`crd_date`** field to use the new date field type. We also covered the steps to create a new **Invoices** folder.

In the next *[Appendix C, List of Configuration Files and Settings](#appc.xhtml)*, we will document the windows and **Linux** settings, configured for use in the book.

# [Points to Remember](#toc.xhtml_s236a)

*   The maximum **String** field length is 254 characters for an **Application Group** field.
*   If the application group **Field date** type is set with a **segment** type, then this is used to determine the expiry for deleting the data for the application group. If there is no setting of a date field as a segment, then the date when the input file was loaded is used.
*   The **Field** types are not editable (the drop-down is grayed out) once they have been entered, so the **date** type can only be modified after creation of the **Application Group** by deleting and reentering the complete **Application Group.**
*   We had to edit the input data file to change all the two digit year fields to four digits in order to successfully load our **Baxter Bay Credit** test data.

# [Multiple Choice Questions](#toc.xhtml_s237a)

1.  Which program is required to be run to remove and re-enter the Baxter Bay Credit Application Group?
    1.  OnDemand Client V10.5 (64-bit)
    2.  Windows ARSLOAD
    3.  OnDemand Administrator V10.5 (64-bit)
    4.  OnDemand Monitor V10.5 (64-bit)
2.  Which Field type is flagged as a segment to provide the delete point for the application group data?
    1.  `String`
    2.  `DecFloat(16)`
    3.  `Date`
    4.  `Integer`

# [Answers](#toc.xhtml_s238a)

1.  c
2.  c

# [Questions](#toc.xhtml_s239a)

1.  What tab would you use to associate the folder search and display fields with database fields?
2.  What else do you have to do if you use the **Field Information** tab to set a default **Year** value of **2024**?

# [Key Terms](#toc.xhtml_s240a)

*   **CFS-CMOD:** Content Federation Services for IBM Content Manager OnDemand used to integrate with the IBM FileNet Content Engine.
*   **Arsagfld:** The **Application Group** Fields Table is used to store the user defined field names and types
*   **DecFloat(16):** Used by the **Baxter Bay Credit** application group, **balance** field, this holds a **Decimal** floating-point number with 16 digits of precision**.**
*   **String:** It can be Variable **(**the **name** field**)** or **Fixed (**the **account** field with 11 characters**)** with a maximum size of **254** characters.
*   **Date:** Contains a valid date in the range January 1, 0001 to December 31, 9999.

**Note:** *See* *[https://www.ibm.com/docs/en/cmofm/10.5.0?topic=objects-data-types-field-types](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=objects-data-types-field-types)* *for the full list of Field types available.*

# [APPENDIX C](#toc.xhtml_appc)

# [List of Configuration Files and Settings](#toc.xhtml_appc)

# [Introduction](#toc.xhtml_s241a)

This Appendix lists each of the **IBM CMOD** configuration files and environment settings for the Windows client, Windows server and the Linux server we used in writing this book.

# [Structure](#toc.xhtml_s242a)

In this appendix, we will discuss the following topics:

*   Windows Server Configuration Files
*   CMOD Environment (OnDemand Command Window)
*   Linux Configuration Files
    *   To Clean and Reset a RedHat Linux Subscription
    *   To Drop an Active DB2 ARCHIVE Database
    *   Rebuilding the ARCHIVE Database
    *   Setting the WebSphere Data Sources for the IBM FileNet Content Engine Fixed Content Device
    *   Trace Settings
    *   /root/.bash_profile
    *   /home/archive/.bash_profile
    *   ars.cfg Configuration File
    *   ars.ini Configuration File
    *   ars.dbfs Configuration File
    *   ars.cache Configuration File
    *   The Archive First Instance Start, with Settings Listed
    *   ars.archive2.cache Configuration File
    *   ars.archive2.cfg Configuration File
    *   ars.archive2.dbfs Configuration File
    *   The Archive2 Second Instance Start, with Settings Listed
*   Procedure to Reset an **ADMIN** Password Using the **arsadm.exe** Program

# [Windows Server Configuration Files](#toc.xhtml_s243a)

On the Windows server the configuration of **Users**, **Groups**, **Folders**, **Cabinets**, **Application Groups, Applications, Storage Sets, Printers** and **Holds** are configured using the **OnDemand Administrator V10.5 (64-bit)** client program, which we described for the addition of **Folders, Application Groups** and **Applications** in *[Appendix B, Recreating an Application Group](#appb.xhtml),* for the **Baxter Bay Credit** Application Group*.*

There are also Windows environment variable settings configured during the installation which we will cover in the next section.

# [CMOD Environment (OnDemand Command Window)](#toc.xhtml_s244a)

The **IBM CMOD** command window **`set`** command was used to list the environment variables, and we have identified the significant variables set using the **`"C:\Program Files\ibm\OnDemand\V10.5\bin\arscmd.exe"`** program, in the following list.

This command window is used to run programs such as the **`ARSLOAD`** and **`ARSXML`** programs described earlier.

`C:\Program Files\ibm\OnDemand\V10.5\bin>`**`set`**

`ALLUSERSPROFILE=C:\ProgramData`

`APPDATA=C:\Users\alan_\AppData\Roaming`

**`ARS_CMDTYPE=1`**

**`ARS_INSTALL_SERVER_V105_DIR=C:\PROGRA~1\ibm\OnDemand\V10.5\`**

`AXIS2C_HOME=C:\mEMBOSS\axis2c`

`CLASSPATH=.;C:\PROGRA~1\ibm\SQLLIB~1\java\db2java.zip;C:\PROGRA~1\ibm\SQLLIB~1\java\db2jcc4.jar;C:\PROGRA~1\ibm\SQLLIB~1\java\sqlj4.zip;C:\PROGRA~1\ibm\SQLLIB~1\java\DB2JCC~1.JAR;C:\PROGRA~1\ibm\SQLLIB~1\BIN;C:\PROGRA~1\ibm\SQLLIB~1\java\Common.jar`

`CommonProgramFiles=C:\Program Files\Common Files`

`CommonProgramFiles(x86)=C:\Program Files (x86)\Common Files`

`CommonProgramW6432=C:\Program Files\Common Files`

**`COMPUTERNAME=DESKTOP-B3JB93R`**

`ComSpec=C:\WINDOWS\system32\cmd.exe`

**`DB2INSTANCE=DB2_01`**

`DriverData=C:\Windows\System32\Drivers\DriverData`

`EMBOSS_ACDROOT=C:\mEMBOSS\acd`

`EMBOSS_AXIS2C_HOME=C:\mEMBOSS\axis2c`

`EMBOSS_DATA=C:\mEMBOSS\data`

`EMBOSS_ROOT=C:\mEMBOSS`

`EPLPLOT_LIB=C:\mEMBOSS\data`

`HOMEDRIVE=C:`

`HOMEPATH=\Users\alan_`

`INCLUDE=C:\PROGRA~1\IBM\SQLLIB~1\INCLUDE;C:\PROGRA~1\IBM\SQLLIB~1\LIB`

`LIB=;C:\PROGRA~1\IBM\SQLLIB~1\LIB`

`LOCALAPPDATA=C:\Users\alan_\AppData\Local`

`LOGONSERVER=\\DESKTOP-B3JB93R`

`NUMBER_OF_PROCESSORS=16`

`OneDrive=C:\Users\alan_\OneDrive`

`OneDriveConsumer=C:\Users\alan_\OneDrive`

`OnlineServices=Online Services`

`OS=Windows_NT`

**`Path=C:\PROGRA~1\ibm\OnDemand\V10.5\bin;C:\PROGRA~1\ibm\OnDemand\V10.5\bin32;C:\Program Files\ibm\gsk8\bin;`**`C:\Program Files (x86)\VMware\VMware Workstation\bin\;C:\Program Files (x86)\Common Files\Oracle\Java\javapath;C:\ProgramData\Oracle\Java\javapath;C:\Program Files (x86)\Intel\iCLS Client\;C:\Program Files\Intel\iCLS Client\;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\WINDOWS\System32\OpenSSH\;c:\Program Files (x86)\HP\HP Performance Advisor;C:\mEMBOSS;C:\Program Files\ibm\gsk8\lib64;C:\Program Files (x86)\ibm\gsk8\lib;C:\PROGRA~1\IBM\SQLLIB~1\BIN;C:\PROGRA~1\IBM\SQLLIB~1\FUNCTION;C:\PROGRA~1\IBM\SQLLIB~1\SAMPLES\REPL;C:\Program Files\Microsoft SQL Server\150\Tools\Binn\;C:\Program Files\Microsoft SQL Server\Client SDK\ODBC\170\Tools\Binn\;C:\Program Files (x86)\Microsoft SQL Server\150\Tools\Binn\;C:\Program Files\Microsoft SQL Server\150\DTS\Binn\;C:\Program Files (x86)\Microsoft SQL Server\150\DTS\Binn\;C:\Program Files\Azure Data Studio\bin;C:\Program Files (x86)\IBM\FileNet\ContentEngine\bin;C:\Users\alan_\AppData\Local\Microsoft\WindowsApps;`

`PATHEXT=.COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC`

`platformcode=5X`

`PROCESSOR_ARCHITECTURE=AMD64`

`PROCESSOR_IDENTIFIER=Intel64 Family 6 Model 85 Stepping 4, GenuineIntel`

`PROCESSOR_LEVEL=6`

`PROCESSOR_REVISION=5504`

`ProgramData=C:\ProgramData`

`ProgramFiles=C:\Program Files`

`ProgramFiles(x86)=C:\Program Files (x86)`

`ProgramW6432=C:\Program Files`

`PROMPT=$P$G`

`PSModulePath=C:\Program Files\WindowsPowerShell\Modules;C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules;c:\Program Files\Intel\Wired Networking\;C:\Program Files (x86)\Microsoft SQL Server\150\Tools\PowerShell\Modules\`

`PUBLIC=C:\Users\Public`

`RegionCode=EMEA`

`SystemDrive=C:`

`SystemRoot=C:\WINDOWS`

`TEMP=C:\Users\alan_\AppData\Local\Temp`

`TMP=C:\Users\alan_\AppData\Local\Temp`

**`USERDOMAIN=DESKTOP-B3JB93R`**

**`USERDOMAIN_ROAMINGPROFILE=DESKTOP-B3JB93R`**

`USERNAME=alan_`

`USERPROFILE=C:\Users\alan_`

`windir=C:\WINDOWS`

`__COMPAT_LAYER=Installer`

`C:\Program Files\ibm\OnDemand\V10.5\bin>`

# [Linux Configuration Files](#toc.xhtml_s245a)

This section covers the **Linux** server configuration files which are required to be edited for setting an initial **IBM CMOD** **ARCHIVE** instance to run with Db2 and the second instance, **ARCHIVE2**, which we described in detail earlier.

We have also included a few general Linux administration settings, which we had to run during the installation of the **IBM CMOD** **Version 10.5.0.7**.

# [To Clean and Reset a RedHat Linux Subscription](#toc.xhtml_s246a)

We had to recover the **RedHat Linux** **RHEL 8** system, on the server, **ECMUKDEMO22**, from back up and the restored system was at an earlier version of the **Linux** operating system, so we had errors relating to connecting to the network port **443** used by subscription-manager.

**Note:** *The* ***RedHat*** *subscription is essential to allow the* ***Linux*** ***yum install*** *commands to be run to install the supporting libraries for the* ***IBM CMOD*** *system.*

After some trial and error, we discovered the original subscription needed to be removed completely and re-applied, as shown in *[Figure C.1](#appc.xhtml_figC_1)*:

`subscription-manager clean`

`subscription-manager register --username xxxxxxxx --password yyyyyyy --auto-attach`

![](images/Figure_C.1.jpg)

**Figure C.1:** The original subscription needed to be removed completely and re-applied

A pop-up window appeared as shown in *[Figure C.2](#appc.xhtml_figC_2):*

![](images/Figure_C.2.jpg)

**Figure C.2:** The ***Registration Successful*** message appears after we apply ***subscription-manager register***

# [To Drop an Active DB2 ARCHIVE Database](#toc.xhtml_s247a)

It is possible to run the **`arsdb`** program and create an **`ARCHIVE`** database, but with a failure to create the required tables. In this scenario, the configuration will need to be fixed and **`arsdb`** rerun, but the database **`drop`** command may fail unless the database activity is stopped, as shown here:

`[archive@ECMUKDEMO22 ~]$` **`db2 drop db ARCHIVE`**

`SQL1035N  The operation failed because the specified database cannot be`

`connected to in the mode requested.  SQLSTATE=57019`

`[archive@ECMUKDEMO22 ~]$`

The following commands can then be used to quiesce the **`ARCHIVE`** database and allow it to be dropped, as shown in *[Figure C.3](#appc.xhtml_figC_3)*:

![](images/Figure_C.3.jpg)

**Figure C.3:** The commands that can then be used to quiesce the ARCHIVE database and allow it to be dropped

**`db2 connect to ARCHIVE`**

--This next command forces the users off, asynchronously:

**`db2 quiesce database immediate force connections`**

-- The unquiesce command must be used for the drop command to run

-- Ensure no users are able to get a connection in between running these commands

**`db2 connect reset`**

-- We must also make sure the database isn’t activated....

**`db2 deactivate db ARCHIVE`**

-- Uncomment to backup the database. The drop command will erase all the ARCHIVE table data!

-- db2 backup db ARCHIVE to ‘<path for the exported data>’ compress

**`db2 drop db ARCHIVE`**

# [Rebuilding the ARCHIVE Database](#toc.xhtml_s248a)

We also ran the **`arsobjd`** command to stop this program, using the **archive** database instance owner before running the **`arsdb`** program to generate the new **`ARCHIVE`** database and tables, as shown here:

(We have removed any repeated runstat updates which are processed after every table creation).

`[archive@ECMUKDEMO22 ~]$` **`db2 drop db ARCHIVE`**

`DB20000I  The DROP DATABASE command completed successfully.`

`[archive@ECMUKDEMO22 ~]$` **`/opt/ibm/ondemand/V10.5/bin/arsobjd -I archive -T`**

`[archive@ECMUKDEMO22 ~]$` **`/opt/ibm/ondemand/V10.5/bin/arsdb -I archive -cv`**

`ARS4018I Creating the DB2 ARCHIVE database`

`ARS4119I Specify the type of archive logging to be used:`

`Do you wish to use DISK(1), TSM(2), or CIRCULAR(3)?`

**`Please specify 1, 2, or 3:1`**

`ARS4062I Database created with territory 'US', code page '1208', code set 'UTF-8' and collating sequence ''`

`ARS4068I Updating the ARCHIVE database configuration`

`ARS4073I Deactivating database ARCHIVE`

`ARS4071I Backing up the ARCHIVE database so that the updates can take effect`

`ARS4057I Timestamp for backup image is: 20240722014852`

`ARS4026I Creating table archive.arsag`

`ARS4034I Creating index archive.arsag_name_idx`

`ARS4034I Creating index archive.arsag_agid_idx`

`ARS4026I Creating table archive.arsag2fol`

`ARS4034I Creating index archive.arsag2fol_idx`

`ARS4026I Creating table archive.arsagfld`

`ARS4034I Creating index archive.arsagfld_idx`

`ARS4026I Creating table archive.arsagfldalias`

`ARS4034I Creating index archive.arsagfldalias_idx`

`ARS4026I Creating table archive.arsagindex`

`ARS4034I Creating index archive.arsagindex_idx`

`ARS4026I Creating table archive.arsagperms`

`ARS4034I Creating index archive.arsagperms_idx`

`ARS4026I Creating table archive.arsann`

`ARS4034I Creating index archive.arsann_idx`

`ARS4026I Creating table archive.arsapp`

`ARS4034I Creating index archive.arsapp_idx`

`ARS4034I Creating index archive.arsapp_name_idx`

`ARS4026I Creating table archive.arsappusr`

`ARS4034I Creating index archive.arsappusr_idx`

`ARS4026I Creating table archive.arscab`

`ARS4034I Creating index archive.arscab_name_idx`

`ARS4034I Creating index archive.arscab_cid_idx`

`ARS4026I Creating table archive.arscab2fol`

`ARS4034I Creating index archive.arscab2fol_idx`

`ARS4026I Creating table archive.arscabnames`

`ARS4034I Creating index archive.arscabnames_cid_idx`

`ARS4026I Creating table archive.arscabperms`

`ARS4034I Creating index archive.arscabperms_idx`

`ARS4026I Creating table archive.arscfsodwork`

`ARS4034I Creating index archive.arscfsodwork_idx`

`ARS4026I Creating table archive.arscmfedwork`

`ARS4034I Creating index archive.arscmfedwork_idx`

`ARS4026I Creating table archive.arsfol`

`ARS4034I Creating index archive.arsfol_name_idx`

`ARS4034I Creating index archive.arsfol_fid_idx`

`ARS4026I Creating table archive.arsfolfld`

`ARS4034I Creating index archive.arsfolfld_idx`

`ARS4026I Creating table archive.arsfolfldusr`

`ARS4034I Creating index archive.arsfolfldusr_idx`

`ARS4026I Creating table archive.arsfolnames`

`ARS4034I Creating index archive.arsfolnames_fid_idx`

`ARS4026I Creating table archive.arsfolperms`

`ARS4034I Creating index archive.arsfolperms_idx`

`ARS4026I Creating table archive.arsftiwork`

`ARS4034I Creating index archive.arsftiwork_idx`

`ARS4026I Creating table archive.arsgroup`

`ARS4034I Creating index archive.arsgroup_gid_idx`

`ARS4034I Creating index archive.arsgroup_name_idx`

`ARS4026I Creating table archive.arshold`

`ARS4034I Creating index archive.arshold_name_idx`

`ARS4034I Creating index archive.arshold_hid_idx`

`ARS4026I Creating table archive.arsholdmap`

`ARS4034I Creating index archive.arsholdmap_idx`

`ARS4026I Creating table archive.arsholdnames`

`ARS4034I Creating index archive.arsholdnames_hid_idx`

`ARS4026I Creating table archive.arsholdperms`

`ARS4034I Creating index archive.arsholdperms_idx`

`ARS4026I Creating table archive.arsholdwork`

`ARS4034I Creating index archive.arsholdwork_idx`

`ARS4026I Creating table archive.arsload`

`ARS4034I Creating index archive.arsload_idx`

`ARS4034I Creating index archive.arsload_name_idx`

`ARS4034I Creating index archive.arsload_dt_idx`

`ARS4026I Creating table archive.arsloadwork`

`ARS4034I Creating index archive.arsloadwork_idx`

`ARS4034I Creating index archive.arsloadwork_loadid_idx`

`ARS4026I Creating table archive.arsnameq`

`ARS4034I Creating index archive.arsnameq_idx`

`ARS4026I Creating table archive.arsnode`

`ARS4028I Inserting default values into table archive.arsnode`

`ARS4034I Creating index archive.arsnode_idx`

`ARS4034I Creating index archive.arsnode_name_idx`

`ARS4026I Creating table archive.arsprt`

`ARS4034I Creating index archive.arsprt_name_idx`

`ARS4034I Creating index archive.arsprt_pid_idx`

`ARS4026I Creating table archive.arsprtopts`

`ARS4034I Creating index archive.arsprtopts_idx`

`ARS4026I Creating table archive.arsprtusr`

`ARS4034I Creating index archive.arsprtusr_idx`

`ARS4026I Creating table archive.arsres`

`ARS4034I Creating index archive.arsres_idx`

`ARS4026I Creating table archive.arsseg`

`ARS4034I Creating index archive.arsseg_name_idx`

`ARS4034I Creating index archive.arsseg_idx`

`ARS4034I Creating index archive.arsseg_cdate_idx`

`ARS4034I Creating index archive.arssegssdt_idx`

`ARS4034I Creating index archive.arsseg_cdt_idx`

`ARS4026I Creating table archive.arsset`

`ARS4028I Inserting default values into table archive.arsset`

`ARS4034I Creating index archive.arsset_name_idx`

`ARS4034I Creating index archive.arsset_sid_idx`

`ARS4026I Creating table archive.arssys`

`ARS4028I Inserting default values into table archive.arssys`

`ARS4026I Creating table archive.arsuser`

`ARS4028I Inserting default values into table archive.arsuser`

`ARS4034I Creating index archive.arsuser_id_idx`

`ARS4034I Creating index archive.arsuser_name_idx`

`ARS4026I Creating table archive.arsusrgrp`

`ARS4034I Creating index archive.arsusrgrp_idx`

`ARS4034I Creating index archive.arsusrgrp_idx2`

`ARS4026I Creating table archive.arsusrgrpid`

`ARS4034I Creating index archive.arsusrgrpid_idx`

`ARS4042I Updating runstat statistics for table archive.arsusrgrpid`

`[archive@ECMUKDEMO22 ~]$`

We can now start the new **IBM CMOD** **Object** server:

**`/opt/ibm/ondemand/V10.5/bin/arsobjd -I archive -S`**

`[archive@ECMUKDEMO22 ~]$` **`ps -eaf|grep arsobjd`**

`archive     4289    2710  0 05:11 pts/0    00:00:00 arsobjd: (accepting)`

`archive    16008   15886  0 07:28 pts/1    00:00:00 grep --color=auto arsobjd`

# [Setting the WebSphere Data Sources for the IBM FileNet Content Engine Fixed Content Device](#toc.xhtml_s249a)

1.  The IBM FileNet Configuration Manager settings are shown in *[Figure C.4](#appc.xhtml_figC_4)*:

    ![](images/Figure_C.4.jpg)

    **Figure C.4:** The IBM FileNet Configuration Manager settings for creating ***ARCHIVEDS*** and ***ARCHIVEDSXA***

2.  The **`ARCHIVEDS`** and **`ARCHIVEDSXA`** data sources can then be tested for connectivity using the **IBM WebSphere** application server console for the **IBM FileNet** web application, as shown in *[Figure C.5](#appc.xhtml_figC_5)*:

    ![](images/Figure_C.5.jpg)

    **Figure C.5:** The ***ARCHIVEDS*** and ***ARCHIVEDSXA*** Data Sources are tested using IBM WebSphere application server

# [Trace Settings](#toc.xhtml_s250a)

See [https://www.ibm.com/support/pages/how-enable-trace-ibm-content-manager-ondemand-server](https://www.ibm.com/support/pages/how-enable-trace-ibm-content-manager-ondemand-server)

The **`trace.settings`** file enables debugging of **`arssockd`** program issues. This file is found in the path **`/opt/ibm/ondemand/V10.5/config.`**

If you omit the path name, the trace facility uses the path entered for the **`ARS_TMP`** parameter in the **`ars.cfg`** file (we have used **`ARS_TMP=/tmp`**).

In the **`trace.settings`** file (which IBM have kindly allowed us to publish), we can see the many options available for debugging **IBM CMOD** programs:

`########################################################################`

`#       trace settings - OnDemand Server Trace Settings File           #`

`#                                                                      #`

`#  5622-662 (C) COPYRIGHT IBM CORPORATION 2020                         #`

`#  All Rights Reserved                                                 #`

`#  Licensed Materials - Property of IBM                                #`

`#                                                                      #`

`#  US Government Users Restricted Rights - Use, duplication or         #`

`#  disclosure restricted by GSA ADP Schedule Contract with IBM Corp.   #`

`#                                                                      #`

`#  This program sample is provided on an as-is basis.    #`

`#  `**`The licensee of the OnDemand product is free to copy, #`**

**`#  revise, modify, and make derivative works of          #`**

**`#  this program sample as they see fit`**`.                  #`

`#                                                                      #`

`# File Format:                                                         #`

`#       1) Comments must begin with a # in the first column            #`

`#       2) Comments cannot exist on the same line as a PARM            #`

`#       3) PARM=VALUE, no spaces before PARM, no spaces after VALUE,   #`

`#          and no spaces before/after the equal sign.                  #`

`#       4) Blank lines are ignored.                                    #`

`#                                                                      #`

`# NOTE:  Please see documentation for configuring these parameters.    #`

`#                                                                      #`

`# Component Names:                                                     #`

`#  ALL      (defines all components)                                   #`

`#  CMD      (parms for the current running command)                    #`

`#  WWW                                                                 #`

`#  CACHE                                                               #`

`#  CS                                                                  #`

`#  CSV                                                                 #`

`#  XPORT                                                               #`

`#  COMP                                                                #`

`#  CFG                                                                 #`

`#  XDR                                                                 #`

`#  DB                                                                  #`

`#  DATE                                                                #`

`#  ICU                                                                 #`

`#  LOAD                                                                #`

`#  MEM                                                                 #`

`#  OS                                                                  #`

`#  PDF                                                                 #`

`#  PROF                                                                #`

`#  SEC                                                                 #`

`#  SRVR                                                                #`

`#  COM                                                                 #`

`#  SM                                                                  #`

`#  TSM                                                                 #`

`#  ARSLOAD                                                             #`

`#  390EXP                                                              #`

`#  390PRT                                                              #`

`#  ARSRD                                                               #`

`#  CSL                                                                 #`

`#  ARSXML                                                              #`

`#  LDAP                                                                #`

`#  390SM                                                               #`

`#  ARSADMIN                                                            #`

`#  SADB                                                                #`

`#  MSGS                                                                #`

`#  SOCKET                                                              #`

`#                                                                      #`

`# Trace Levels (`**`add together to form level`**`)                #`

`#                                                                      #`

`#  ERROR     1                                                         #`

`#  WARNING   2                                                         #`

`#  INFO      4                                                         #`

`#  FLOW      8                                                         #`

`#                                                                      #`

`# Examples:                                                            #`

`#   To enable error/warning trace for the current command              #`

`#      TRACE_LEVELS=CMD=3                                              #`

`#   To enable error/warning/info trace for all components, and info    #`

`#   trace for the database level                                       #`

`#      TRACE_LEVELS=ALL=3,DB=7                                         #`

`#                                                                      #`

`# TRACE_FILE    Will be created in the ARS_TMP directory               #`

`# TRACE_LEVELS  Define component(s) and trace levels                   #`

`########################################################################`

`[TRACE]`

`TRACE_FILE=ARCHIVE.trace.log`

`TRACE_LEVELS=ALL=3`

`TRACE_FILE=ARCHIVE.trc`

`APPEND=1`

This setting gives a **`/tmp/arssock.err`** file when running the **`arssockd`** program which is not listed in the comments for the supported programs. (The only configuration parameter used by the **`arssockd`** program appears to be the **`TRACE_LEVELS=ALL=3 parameter`**).

# [`/root/.bash_profile`](#toc.xhtml_s251a)

The environment variables added to the **`root`** user’s **`.bash_profile`** enable additional default system environment variables to be set. This file is listed as follows:

**`[root@ECMUKDEMO22 config]# cat /root/.bash_profile`**

`# .bash_profile`

`# Get the aliases and functions`

`if [ -f ~/.bashrc ]; then`

`.` `~/.bashrc`

`fi`

`# User specific environment and startup programs`

**`PATH=/opt/IBM/Java/jre/bin:$PATH:$HOME/bin:/opt/ibm/ondemand/V10.5`**

`export PATH`

`JAVA_HOME=/opt/IBM/Java/jre`

`export JAVA_HOME`

`CONCOURSE_EXTERNAL_URL=http://localhost:8081`

`export CONCOURSE_EXTERNAL_URL`

**`DATABASE=ARCHIVE`**

`export DATABASE`

**`DB2DIR=/opt/ibm/db2/V10.5`**

`export DB2DIR`

**`DB2INSTANCE=archive`**

`export DB2INSTANCE`

**`DB2LIB=/home/archive/sqllib/lib`**

`export DB2LIB`

**`DB2_HOME=/home/archive/sqllib`**

`export DB2_HOME`

**`HOSTNAME=ecmukdemo22`**

`export HOSTNAME`

`HOSTTYPE=x86_64`

`export HOSTTYPE`

**`IBM_DB_DIR=/home/archive/sqllib`**

`export IBM_DB_DIR`

**`IBM_DB_HOME=/home/archive/sqllib`**

`export IBM_DB_HOME`

**`IBM_DB_INCLUDE=/home/archive/sqllib/include`**

`export IBM_DB_INCLUDE`

**`IBM_DB_LIB=/home/archive/sqllib/lib`**

`export IBM_DB_LIB`

**`LIBPATH=$LIBPATH:/opt/ibm/ondemand/V10.5/www:/usr/local/ibm/gsk8_64/lib64`**

`export LIBPATH`

**`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`**

`export SRVR_OD_STASH`

**`LD_LIBRARY_PATH=/opt/ibm/ondemand/V10.5/www`**

`export LD_LIBRARY_PATH`

`[root@ECMUKDEMO22 config]#`

# [`/home/archive/.bash_profile`](#toc.xhtml_s252a)

The environment variables added to the **`archive`** user’s **`.bash_profile`** enable additional default system environment variables to be set. This file is listed as follows:

`[archive@ECMUKDEMO22 ~]$` **`cat /home/archive/.bash_profile`**

`# .bash_profile`

`# Get the aliases and functions`

`if [ -f ~/.bashrc ]; then`

`.` `~/.bashrc`

`fi`

`# User specific environment and startup programs`

**`PATH=/opt/IBM/Java/jre/bin:$PATH:$HOME/bin:/opt/ibm/ondemand/V10.5`**

`export PATH`

`JAVA_HOME=/opt/IBM/Java/jre`

`export JAVA_HOME`

**`DATABASE=ARCHIVE`**

`export DATABASE`

**`DB2DIR=/opt/ibm/db2/V10.5`**

`export DB2DIR`

**`DB2INSTANCE=archive`**

`export DB2INSTANCE`

**`DB2LIB=/home/archive/sqllib/lib`**

`export DB2LIB`

**`DB2_HOME=/home/archive/sqllib`**

`export DB2_HOME`

**`HOSTNAME=ecmukdemo22`**

`export HOSTNAME`

`HOSTTYPE=x86_64`

`export HOSTTYPE`

**`IBM_DB_DIR=/home/archive/sqllib`**

`export IBM_DB_DIR`

**`IBM_DB_HOME=/home/archive/sqllib`**

`export IBM_DB_HOME`

**`IBM_DB_INCLUDE=/home/archive/sqllib/include`**

`export IBM_DB_INCLUDE`

**`IBM_DB_LIB=/home/archive/sqllib/lib`**

`export IBM_DB_LIB`

**`LIBPATH=$LIBPATH:/opt/ibm/ondemand/V10.5/www:/usr/local/ibm/gsk8_64/lib64`**

`export LIBPATH`

`[archive@ECMUKDEMO22 ~]$`

# [`ars.cfg` Configuration File](#toc.xhtml_s253a)

The **`ars.cfg`** file is used for the initial **IBM CMOD**, **ARCHIVE** instance as listed here:

`[root@ECMUKDEMO22 config]#` **`cat ars.cfg`**

`#`

`#       ars.cfg - OnDemand Configuration File`

`#`

`#  5622-662 (C) COPYRIGHT IBM CORPORATION 2020`

`#  All Rights Reserved`

`#  Licensed Materials - Property of IBM`

`#`

`#  US Government Users Restricted Rights - Use, duplication or`

`#  disclosure restricted by GSA ADP Schedule Contract with IBM Corp.`

`#`

**`#  This program sample is provided on an as-is basis.`**

**`#  The licensee of the OnDemand product is free to copy, revise,`**

**`#  modify, and make derivative works of this program sample`**

**`#  as they see fit.`**

`#`

`# File Format:`

`#       1) Comments must begin with a # in the first column`

`#       2) Comments cannot exist on the same line as a PARM`

`#       3) PARM=VALUE, no spaces before PARM, no spaces after VALUE,`

`#          and no spaces before/after the equal sign.`

`#       4) Blank lines are ignored.`

`#`

`# NOTE:  Please see documentation for configuring these parameters.`

`#`

`#######################`

`# OnDemand Parameters #`

`#######################`

`#`

`# Number of client licenses (Library Server Only)`

`#`

`#  - This should be set to however many licenses are purchased`

`#`

**`ARS_NUM_LICENSE=1`**

`#`

`# Object Server/Library Server definitions (Object Server Only)`

`#`

`#   If Object Server then set`

`#`

`#     ARS_SRVR=<server>`

`#        <server> is name of the OnDemand Library Server`

`#`

`#     ARS_LOCAL_SRVR=<server>`

`#        <server> is name of the local OnDemand Object Server`

`#`

`#   For Example:`

`#`

`#      Server Type (hostname)`

`#     |----------------------|`

`#     | ObjServer   (ObjSrv1)|`

`#     |----------------------|`

`#`

`#     |----------------------|`

`#     | LibServer   (LibSrvr)|`

`#     |----------------------|`

`#`

`#     |----------------------|`

`#     | ObjServer   (ObjSrv2)|`

`#     |----------------------|`

`#`

`#   LibSrvr:`

`#     Neither Variable should be set`

`#`

`#   ObjSrv1:`

`#     ARS_SRVR=LibSrvr`

`#      ARS_LOCAL_SRVR=ECMUKDEMO22`

`#`

`#   ObjSrv2:`

`#     ARS_SRVR=LibSrvr`

`#     ARS_LOCAL_SRVR=ObjSrv2`

`#`

`# NOTES:`

`#        - These names should be exactly what is specified for the server`

`#          in the storage node`

`#        - If CICS client is being used you must specifiy the machines`

`#          internet address instead of hostname or alias.`

`#`

`#`

**`ARS_SRVR=ECMUKDEMO22`**

**`ARS_LOCAL_SRVR=ECMUKDEMO22`**

**`ARS_SUPPORT_HOLD=1`**

**`ARS_SUPPORT_CFSOD=1`**

**`ARS_ORIGINAL_CODEPAGE=1208`**

`#`

`# Number of Database SubServers (Library Server Only)`

`#   0         - Defaults to connection per client`

`#   Otherwise - The number of Database SubServers to handle connections`

`#               to the database (minimum of 2)`

`#`

**`ARS_NUM_DBSRVR=0`**

**`DB2INSTANCE=archive`**

`#`

`# OnDemand Temporary Work Directory (Library/Object Server)`

`#`

`# NOTE:  This directory should have permissions just like /tmp`

`#        drwxrwxrwt   /tmp        These perms are 1777`

`#`

**`ARS_TMP=/tmp`**

**`ARS_PRINT_PATH=/tmp`**

`#######################`

`# Database Parameters #`

`#######################`

`#`

`# Database for OnDemand to use (Library Server Only)`

`#`

`ARS_DB_ENGINE=DB2`

`#`

`# Used for arstblsp command and reloading migrated tables (Library Server Only)`

`#   0 (import)`

`#   1 (load w/TSM - DB2 only)`

`#   2 (load w/DISK - DB2 only, using ARS_TMP)`

`#`

**`ARS_DB_IMPORT=0`**

**`ARSSOCK=debug`**

`#`

`# Used to specify if the database supports partitioning (Library Server Only)`

`#   Blank (No partition support)`

`#`

`ARS_DB_PARTITION=`

`########################################`

`# DB2 Parameters (Library Server Only) #`

`########################################`

**`DB2INSTANCE=archive`**

`#`

`# These parameters used only during database creation`

`#`

**`ARS_DB2_DATABASE_PATH=/arsdb`**

**`ARS_DB2_PRIMARY_LOGPATH=/arsdb_primarylog`**

**`ARS_DB2_ARCHIVE_LOGPATH=/arsdb_archivelog`**

**`ARS_DB2_LOGFILE_SIZE=1000`**

**`ARS_DB2_LOG_NUMBER=40`**

`#`

`# DB2/TSM Parameters`

`#`

**`ARS_DB2_TSM_CONFIG=/opt/tivoli/tsm/client/api/bin/dsm.opt.db2`**

`###########################################`

`# ORACLE Parameters (Library Server Only) #`

`###########################################`

**`ARS_ORACLE_HOME=/oracle`**

`######################################################`

`# Storage Manager Parameters (Library/Object Server) #`

`######################################################`

`#`

`# Storage Manager for OnDemand to use`

`#`

**`ARS_STORAGE_MANAGER=CACHE_ONLY`**

`ARS_MESSAGE_OF_THE_DAY=`

`ARS_TRACE_SETTINGS=`

`###########################################`

`# LDAP Parameters (Library Server Only)   #`

`###########################################`

**`ARS_LDAP_SERVER=ECMUKDEMO77`**

**`ARS_LDAP_PORT=389`**

**`ARS_LDAP_BASE_DN=cn=localhost`**

**`ARS_LDAP_BIND_DN=cn=P8Admin,cn=localhost`**

**`ARS_LDAP_BIND_DN_PWD=filenet`**

`ARS_LDAP_BIND_ATTRIBUTE=`

`ARS_LDAP_MAPPED_ATTRIBUTE=`

`ARS_LDAP_ALLOW_ANONYMOUS=`

`#######################################`

`# TSM Parameters (Object Server Only) #`

`#######################################`

`DSMSERV_DIR=/opt/tivoli/tsm/server/bin`

`DSMSERV_CONFIG=/opt/tivoli/tsm/server/bin/dsmserv.opt`

`DSM_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSM_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSM_LOG=/tmp`

`DSMG_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMG_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMG_LOG=/tmp`

`DSMI_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMI_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMI_LOG=/tmp`

`[root@ECMUKDEMO22 config]#`

# [`ars.ini` Configuration File](#toc.xhtml_s254a)

The **IBM CMOD** **`ars.ini`** file is used to store the main pointers to the other configuration files for each **IBM CMOD** instance created. In the example we created a second instance, called **ARCHIVE2**.

`[root@ECMUKDEMO22 config]#` **`cat ars.ini`**

`[@SRV@_ARCHIVE]`

**`HOST=ECMUKDEMO22`**

**`PROTOCOL=2`**

**`PORT=1445`**

**`SRVR_INSTANCE=ARCHIVE`**

**`SRVR_INSTANCE_OWNER=archive`**

**`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.cfg`**

**`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.dbfs`**

**`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.cache`**

**`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`**

**`[@SRV@_ARCHIVE2]`**

**`HOST=ECMUKDEMO22`**

**`PROTOCOL=2`**

**`PORT=1444`**

**`SRVR_INSTANCE=ARCHIVE2`**

**`SRVR_INSTANCE_OWNER=archive2`**

**`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.cfg`**

**`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.dbfs`**

**`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.cache`**

**`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.archive2.stash`**

`[@SRV@_DD]`

**`PROTOCOL=1`**

`[root@ECMUKDEMO22 config]#`

# [`ars.dbfs` Configuration File](#toc.xhtml_s255a)

The **`ars.dbfs`** file is used to define the **ARCHIVE** instance database file systems, we didn’t set anything since the default of the **Db2 USERSPACE1** tablespace is then used, which was fine for our requirements.

`[root@ECMUKDEMO22 config]#` **`cat ars.dbfs`**

`#`

`#       ars.dbfs - OnDemand Database Filesystems Configuration File`

`#`

`#  5622-662 (C) COPYRIGHT IBM CORPORATION 1995`

`#  All Rights Reserved`

`#  Licensed Materials - Property of IBM`

`#`

`#  US Government Users Restricted Rights - Use, duplication or`

`#  disclosure restricted by GSA ADP Schedule Contract with IBM Corp.`

`#`

`#  This program sample is provided on an as-is basis.`

`#  The licensee of the OnDemand product is free to copy, revise,`

`#  modify, and make derivative works of this program sample`

`#  as they see fit.`

`#`

`#  This file defines the filesystems to use for creating the tablespaces in`

`#  which the tables will be created.`

`#`

`# Tablespace Types:`

`#   - See the OnDemand and DB2/Oracle documentation for specifics about`

`#     tablespaces`

`#`

`#         SMS - System Managed Space`

`#`

`#  NOTE:  OnDemand Application Groups define which tablespace type`

`#         to use (if any).  If tablespaces are not used, then the`

`#         OnDemand Application Group(s) will store data in the:`

`#              DB2 - USERSPACE1 tablespace`

`#              Oracle - default tablespace for OnDemand/Oracle userid`

`#`

`# File Format:`

`# 1) Comments must begin with a # in the first column`

`#       2) Blank lines are ignored.`

`# 3) Put space/tab after filesystem name and before tablespace type.`

`#`

`#`

`# EXAMPLE:`

`# Filesystem                        Tablespace Type (SMS)`

`# --------------------------------------------------------------`

`#/arsdb/SMS    SMS`

`#`

`#`

`# DEFINITIONS:`

`# Filesystem                        Tablespace Type (SMS)`

`# --------------------------------------------------------------`

`[root@ECMUKDEMO22 config]#`

# [`ars.cache` Configuration File](#toc.xhtml_s256a)

This file defines the file systems used by **IBM CMOD** for cache storage. If there are multiple file systems listed in the **`ars.cache`** file, **IBM CMOD** uses the file system with the greatest amount of free space to store the document objects.

`[root@ECMUKDEMO22 config]#` **`cat ars.cache`**

`#`

`#       ars.cache - OnDemand Cache Configuration File`

`#`

`#  5622-662 (C) COPYRIGHT IBM CORPORATION 1995`

`#  All Rights Reserved`

`#  Licensed Materials - Property of IBM`

`#`

`#  US Government Users Restricted Rights - Use, duplication or`

`#  disclosure restricted by GSA ADP Schedule Contract with IBM Corp.`

`#`

`#  This program sample is provided on an as-is basis.`

`#  The licensee of the OnDemand product is free to copy, revise,`

`#  modify, and make derivative works of this program sample`

`#  as they see fit.`

`#`

`# File Format:`

`# 1) Comments must begin with a # in the first column`

`#       2) Blank lines are ignored.`

`#`

`# NOTES:`

`#       1) The first filesystem defined in this file can NEVER change.`

`#       2) Always add new filesystems to the bottom of the list.`

`#`

**`/arscache/cache1`**

`[root@ECMUKDEMO22 config]#`

# [The Archive First Instance Start, with Settings Listed](#toc.xhtml_s257a)

The first **`ARCHIVE`** instance is started with the **`-v`** option, which displays the configuration settings:

`[root@ECMUKDEMO22 ~]# /opt/ibm/ondemand/V10.5/bin/arssockd -I archive -S`

`ARS0351I The arssockd instance ARCHIVE is ready`

`[root@ECMUKDEMO22 ~]# /opt/ibm/ondemand/V10.5/bin/arsobjd -v -S -I archive`

`ARS0462I Server Version: 10.5.0.7`

`ARS0463I Operating System: Linux #1 SMP Fri Jun 2 08:27:19 EDT 2023.4.18.0-477.15.1.el8_8.x86_64`

`ARS0464I Install Location: /opt/ibm/ondemand/V10.5/`

`ARS0465I Limits: Data(unlimited KB) Stack(8192 KB) Core(0 512-blocks) Cpu(unlimited seconds) File(unlimited 512-blocks) Nofiles(1024) Threads(0) Processes(127300)`

`ARS0285I Setting server locale: en_US.UTF-8`

`ARS0288I Object server starting`

`ARS0291I Server instance: ARCHIVE`

`ARS0295I -------- Start of server configuration information --------`

`[@SRV@_ARCHIVE]`

`PROTOCOL=2`

`PORT=1445`

`SRVR_INSTANCE=ARCHIVE`

`SRVR_INSTANCE_OWNER=archive`

`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.cfg`

`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.dbfs`

`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.cache`

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.stash`

`HOST=ECMUKDEMO22`

`[CFG]`

`ARS_SRVR=ECMUKDEMO22`

`ARS_LOCAL_SRVR=ECMUKDEMO22`

`ARS_SUPPORT_HOLD=1`

`ARS_SUPPORT_CFSOD=1`

`ARS_ORIGINAL_CODEPAGE=1208`

`ARS_NUM_DBSRVR=0`

`DB2INSTANCE=archive`

`ARS_TMP=/tmp`

`ARS_PRINT_PATH=/tmp`

`ARS_DB_ENGINE=DB2`

`ARS_DB_IMPORT=0`

`ARSSOCK=debug`

`ARS_DB2_DATABASE_PATH=/arsdb`

`ARS_DB2_PRIMARY_LOGPATH=/arsdb_primarylog`

`ARS_DB2_ARCHIVE_LOGPATH=/arsdb_archivelog`

`ARS_DB2_LOGFILE_SIZE=1000`

`ARS_DB2_LOG_NUMBER=40`

`ARS_DB2_TSM_CONFIG=/opt/tivoli/tsm/client/api/bin/dsm.opt.db2`

`ARS_ORACLE_HOME=/oracle`

`ARS_STORAGE_MANAGER=CACHE_ONLY`

`ARS_LDAP_SERVER=ECMUKDEMO77`

`ARS_LDAP_PORT=389`

`ARS_LDAP_BASE_DN=cn=localhost`

`ARS_LDAP_BIND_DN=cn=P8Admin,cn=localhost`

`ARS_LDAP_BIND_DN_PWD=filenet`

`DSMSERV_DIR=/opt/tivoli/tsm/server/bin`

`DSMSERV_CONFIG=/opt/tivoli/tsm/server/bin/dsmserv.opt`

`DSM_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSM_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSM_LOG=/tmp`

`DSMG_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMG_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMG_LOG=/tmp`

`DSMI_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMI_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMI_LOG=/tmp`

`ARS_DOWNLOAD_DIR=/tmp`

`ARS_DOWNLOAD_TMP_DIR=/tmp`

`ARS_NUM_LICENSE=1`

`[DBFS]`

`DBFS_NUM=0`

`[CACHE]`

`SMFS1=/arscache/cache1`

`SMFS_NUM=1`

`--------- End of server configuration information ---------`

`[root@ECMUKDEMO22 config]$ ARS0351I The arsobjd instance ARCHIVE is ready`

# [`ars.archive2.cache` Configuration File](#toc.xhtml_s258a)

The second **IBM CMOD** Instance, **`ARCHIVE2`** has a cache file system setting, (using **`ars.archive2.cfg`**) as follows:

`[root@ECMUKDEMO22 config]# cat ars.archive2.cache`

`#`

`#       ars.cache - OnDemand Cache Configuration File`

`#`

`#  5622-662 (C) COPYRIGHT IBM CORPORATION 1995`

`#  All Rights Reserved`

`#  Licensed Materials - Property of IBM`

`#`

`#  US Government Users Restricted Rights - Use, duplication or`

`#  disclosure restricted by GSA ADP Schedule Contract with IBM Corp.`

`#`

`#  This program sample is provided on an as-is basis.`

`#  The licensee of the OnDemand product is free to copy, revise,`

`#  modify, and make derivative works of this program sample`

`#  as they see fit.`

`#`

`# File Format:`

`# 1) Comments must begin with a # in the first column`

`#       2) Blank lines are ignored.`

`#`

`# NOTES:`

`#       1) The first filesystem defined in this file can NEVER change.`

`#       2) Always add new filesystems to the bottom of the list.`

`#`

`/arscache/cache2`

`[root@ECMUKDEMO22 config]#`

# [`ars.archive2.cfg` Configuration File](#toc.xhtml_s259a)

The second, **`ARCHIVE2`** instance has a file named **`ars.archive2.cfg`**, which defines its Db2 instance parameters as highlighted here:

`[root@ECMUKDEMO22 config]# cat ars.archive2.cfg`

`#`

`#       ars.archive2.cfg - OnDemand Configuration File`

`#`

`#  5622-662 (C) COPYRIGHT IBM CORPORATION 2020`

`#  All Rights Reserved`

`#  Licensed Materials - Property of IBM`

`#`

`#  US Government Users Restricted Rights - Use, duplication or`

`#  disclosure restricted by GSA ADP Schedule Contract with IBM Corp.`

`#`

`#  This program sample is provided on an as-is basis.`

`#  The licensee of the OnDemand product is free to copy, revise,`

`#  modify, and make derivative works of this program sample`

`#  as they see fit.`

`#`

`# File Format:`

`#       1) Comments must begin with a # in the first column`

`#       2) Comments cannot exist on the same line as a PARM`

`#       3) PARM=VALUE, no spaces before PARM, no spaces after VALUE,`

`#          and no spaces before/after the equal sign.`

`#       4) Blank lines are ignored.`

`#`

`# NOTE:  Please see documentation for configuring these parameters.`

`#`

`#######################`

`# OnDemand Parameters #`

`#######################`

`#`

`# Number of client licenses (Library Server Only)`

`#`

`#  - This should be set to however many licenses are purchased`

`#`

`ARS_NUM_LICENSE=1`

`#`

`# Object Server/Library Server definitions (Object Server Only)`

`#`

`#   If Object Server then set`

`#`

`#     ARS_SRVR=<server>`

`#        <server> is name of the OnDemand Library Server`

`#`

`#     ARS_LOCAL_SRVR=<server>`

`#        <server> is name of the local OnDemand Object Server`

`#`

`#   For Example:`

`#`

`#      Server Type (hostname)`

`#     |----------------------|`

`#     | ObjServer   (ObjSrv1)|`

`#     |----------------------|`

`#`

`#     |----------------------|`

`#     | LibServer   (LibSrvr)|`

`#     |----------------------|`

`#`

`#     |----------------------|`

`#     | ObjServer   (ObjSrv2)|`

`#     |----------------------|`

`#`

`#   LibSrvr:`

`#     Neither Variable should be set`

`#`

`#   ObjSrv1:`

`#     ARS_SRVR=LibSrvr`

`#      ARS_LOCAL_SRVR=ECMUKDEMO22`

`#`

`#   ObjSrv2:`

`#     ARS_SRVR=LibSrvr`

`#     ARS_LOCAL_SRVR=ObjSrv2`

`#`

`# NOTES:`

`#        - These names should be exactly what is specified for the server`

`#          in the storage node`

`#        - If CICS client is being used you must specifiy the machines`

`#          internet address instead of hostname or alias.`

`#`

`#`

`ARS_SRVR=ECMUKDEMO22`

`ARS_LOCAL_SRVR=ECMUKDEMO22`

`ARS_SUPPORT_HOLD=1`

`ARS_SUPPORT_CFSOD=1`

`ARS_ORIGINAL_CODEPAGE=1208`

`#`

`# Number of Database SubServers (Library Server Only)`

`#   0         - Defaults to connection per client`

`#   Otherwise - The number of Database SubServers to handle connections`

`#               to the database (minimum of 2)`

`#`

`ARS_NUM_DBSRVR=0`

`DB2INSTANCE=archive2`

`#`

`# OnDemand Temporary Work Directory (Library/Object Server)`

`#`

`# NOTE:  This directory should have permissions just like /tmp`

`#        drwxrwxrwt   /tmp        These perms are 1777`

`#`

`ARS_TMP=/tmp`

`ARS_PRINT_PATH=/tmp`

`#######################`

`# Database Parameters #`

`#######################`

`#`

`# Database for OnDemand to use (Library Server Only)`

`#`

`ARS_DB_ENGINE=DB2`

`#`

`# Used for arstblsp command and reloading migrated tables (Library Server Only)`

`#   0 (import)`

`#   1 (load w/TSM - DB2 only)`

`#   2 (load w/DISK - DB2 only, using ARS_TMP)`

`#`

`ARS_DB_IMPORT=0`

`ARSSOCK=debug`

`#`

`# Used to specify if the database supports partitioning (Library Server Only)`

`#   Blank (No partition support)`

`#`

`ARS_DB_PARTITION=`

`########################################`

`# DB2 Parameters (Library Server Only) #`

`########################################`

`DB2INSTANCE=archive2`

`#`

`# These parameters used only during database creation`

`#`

**`ARS_DB2_DATABASE_PATH=/arsdb2`**

**`ARS_DB2_PRIMARY_LOGPATH=/arsdb2_primarylog`**

**`ARS_DB2_ARCHIVE_LOGPATH=/arsdb2_archivelog`**

**`ARS_DB2_LOGFILE_SIZE=1000`**

**`ARS_DB2_LOG_NUMBER=40`**

`#`

`# DB2/TSM Parameters`

`#`

`ARS_DB2_TSM_CONFIG=/opt/tivoli/tsm/client/api/bin/dsm.opt.db2`

`###########################################`

`# ORACLE Parameters (Library Server Only) #`

`###########################################`

`ARS_ORACLE_HOME=/oracle`

`######################################################`

`# Storage Manager Parameters (Library/Object Server) #`

`######################################################`

`#`

`# Storage Manager for OnDemand to use`

`#`

`ARS_STORAGE_MANAGER=CACHE_ONLY`

`ARS_MESSAGE_OF_THE_DAY=`

`ARS_TRACE_SETTINGS=`

`###########################################`

`# LDAP Parameters (Library Server Only)   #`

`###########################################`

`ARS_LDAP_SERVER=ECMUKDEMO77`

`ARS_LDAP_PORT=389`

`ARS_LDAP_BASE_DN=cn=localhost`

`ARS_LDAP_BIND_DN=cn=P8Admin,cn=localhost`

`ARS_LDAP_BIND_DN_PWD=filenet`

`ARS_LDAP_BIND_ATTRIBUTE=`

`ARS_LDAP_MAPPED_ATTRIBUTE=`

`ARS_LDAP_ALLOW_ANONYMOUS=`

`#######################################`

`# TSM Parameters (Object Server Only) #`

`#######################################`

`DSMSERV_DIR=/opt/tivoli/tsm/server/bin`

`DSMSERV_CONFIG=/opt/tivoli/tsm/server/bin/dsmserv.opt`

`DSM_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSM_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSM_LOG=/tmp`

`DSMG_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMG_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMG_LOG=/tmp`

`DSMI_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMI_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMI_LOG=/tmp`

`ARS_DOWNLOAD_DIR=/tmp`

`ARS_DOWNLOAD_TMP_DIR=/tmp`

`[root@ECMUKDEMO22 config]#`

# [`ars.archive2.dbfs` Configuration File](#toc.xhtml_s260a)

The second, **`ARCHIVE2`** instance, has an **IBM CMOD** Database Filesystems configuration file, **`ars.archive2.dbfs`**, we didn’t set anything since the default of the **Db2 USERSPACE1** tablespace for the **`ARCHIVE2`** database instance is then used, which was fine for our requirements:

`[root@ECMUKDEMO22 config]# cat ars.archive2.dbfs`

`#`

`#       ars.dbfs - OnDemand Database Filesystems Configuration File`

`#`

`#  5622-662 (C) COPYRIGHT IBM CORPORATION 1995`

`#  All Rights Reserved`

`#  Licensed Materials - Property of IBM`

`#`

`#  US Government Users Restricted Rights - Use, duplication or`

`#  disclosure restricted by GSA ADP Schedule Contract with IBM Corp.`

`#`

`#  This program sample is provided on an as-is basis.`

`#  The licensee of the OnDemand product is free to copy, revise,`

`#  modify, and make derivative works of this program sample`

`#  as they see fit.`

`#`

`#  This file defines the filesystems to use for creating the tablespaces in`

`#  which the tables will be created.`

`#`

`# Tablespace Types:`

`#   - See the OnDemand and DB2/Oracle documentation for specifics about`

`#     tablespaces`

`#`

`#         SMS - System Managed Space`

`#`

`#  NOTE:  OnDemand Application Groups define which tablespace type`

`#         to use (if any).  If tablespaces are not used, then the`

`#         OnDemand Application Group(s) will store data in the:`

`#              DB2 - USERSPACE1 tablespace`

`#              Oracle - default tablespace for OnDemand/Oracle userid`

`#`

`# File Format:`

`# 1) Comments must begin with a # in the first column`

`#       2) Blank lines are ignored.`

`# 3) Put space/tab after filesystem name and before tablespace type.`

`#`

`#`

`# EXAMPLE:`

`# Filesystem                        Tablespace Type (SMS)`

`# --------------------------------------------------------------`

`#/arsdb/SMS    SMS`

`#`

`#`

`# DEFINITIONS:`

`# Filesystem                        Tablespace Type (SMS)`

`# --------------------------------------------------------------`

`[root@ECMUKDEMO22 config]#`

# [The `archive2` Second Instance Start, with Settings Listed](#toc.xhtml_s261a)

The**`archive2`** instance is started using the **`-v`** option to list the configurations as follows:

`[root@ECMUKDEMO22 ~]#` **`/opt/ibm/ondemand/V10.5/bin/arssockd -I archive2 -S`**

`ARS0351I The arssockd instance ARCHIVE2 is ready`

`[root@ECMUKDEMO22 ~]#` **`/opt/ibm/ondemand/V10.5/bin/arsobjd -v -S -I archive2`**

`ARS0462I Server Version: 10.5.0.7`

`ARS0463I Operating System: Linux #1 SMP Fri Jun 2 08:27:19 EDT 2023.4.18.0-477.15.1.el8_8.x86_64`

`ARS0464I Install Location: /opt/ibm/ondemand/V10.5/`

`ARS0465I Limits: Data(unlimited KB) Stack(8192 KB) Core(0 512-blocks) Cpu(unlimited seconds) File(unlimited 512-blocks) Nofiles(1024) Threads(0) Processes(127300)`

`ARS0285I Setting server locale: en_US.UTF-8`

`ARS0288I Object server starting`

`ARS0291I Server instance: ARCHIVE2`

`ARS0295I -------- Start of server configuration information --------`

`[@SRV@_ARCHIVE2]`

`PROTOCOL=2`

`PORT=1444`

`SRVR_INSTANCE=ARCHIVE2`

`SRVR_INSTANCE_OWNER=archive2`

`SRVR_OD_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.cfg`

`SRVR_DB_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.dbfs`

`SRVR_SM_CFG=/opt/ibm/ondemand/V10.5/config/ars.archive2.cache`

`SRVR_OD_STASH=/opt/ibm/ondemand/V10.5/config/ars.archive2.stash`

`HOST=ECMUKDEMO22`

`[CFG]`

`ARS_SRVR=ECMUKDEMO22`

`ARS_LOCAL_SRVR=ECMUKDEMO22`

`ARS_SUPPORT_HOLD=1`

`ARS_SUPPORT_CFSOD=1`

`ARS_ORIGINAL_CODEPAGE=1208`

`ARS_NUM_DBSRVR=0`

`DB2INSTANCE=archive2`

`ARS_TMP=/tmp`

`ARS_PRINT_PATH=/tmp`

`ARS_DB_ENGINE=DB2`

`ARS_DB_IMPORT=0`

`ARSSOCK=debug`

`ARS_DB2_DATABASE_PATH=/arsdb2`

`ARS_DB2_PRIMARY_LOGPATH=/arsdb2_primarylog`

`ARS_DB2_ARCHIVE_LOGPATH=/arsdb2_archivelog`

`ARS_DB2_LOGFILE_SIZE=1000`

`ARS_DB2_LOG_NUMBER=40`

`ARS_DB2_TSM_CONFIG=/opt/tivoli/tsm/client/api/bin/dsm.opt.db2`

`ARS_ORACLE_HOME=/oracle`

`ARS_STORAGE_MANAGER=CACHE_ONLY`

`ARS_LDAP_SERVER=ECMUKDEMO77`

`ARS_LDAP_PORT=389`

`ARS_LDAP_BASE_DN=cn=localhost`

`ARS_LDAP_BIND_DN=cn=P8Admin,cn=localhost`

`ARS_LDAP_BIND_DN_PWD=filenet`

`DSMSERV_DIR=/opt/tivoli/tsm/server/bin`

`DSMSERV_CONFIG=/opt/tivoli/tsm/server/bin/dsmserv.opt`

`DSM_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSM_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSM_LOG=/tmp`

`DSMG_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMG_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMG_LOG=/tmp`

`DSMI_DIR=/opt/tivoli/tsm/client/api/bin64`

`DSMI_CONFIG=/opt/tivoli/tsm/client/api/bin64/dsm.opt`

`DSMI_LOG=/tmp`

`ARS_DOWNLOAD_DIR=/tmp`

`ARS_DOWNLOAD_TMP_DIR=/tmp`

`ARS_NUM_LICENSE=1`

`[DBFS]`

`DBFS_NUM=0`

`[CACHE]`

`SMFS1=/arscache/cache2`

`SMFS_NUM=1`

`--------- End of server configuration information ---------`

# [Procedure to Reset an `ADMIN` Password Using the `arsadm.exe` Program](#toc.xhtml_s262a)

The **`ADMIN`** password expires by default after 90 days. If this is set, then you may see the following error code 2061 message returned from the **ODWEK** Java **API**, as shown in *[Figure C.6](#appc.xhtml_figC_6)*:

![](images/Figure_C.6.jpg)

**Figure C.6:** The following error code ***2061*** message returned from the ***ODWEK*** Java ***API***

To update the expired password, we use the **IBM CMOD** administration program, entitled “**OnDemand Administrator V10.5 (64-bit)**” (in the path, "**`c:\Program Files\IBM\OnDemand Clients\V10.5\bin\`**”). We run the **`arsadm.exe`** IBM CMOD client program on the windows server, as shown in *[Figure C.7](#appc.xhtml_figC_7)*, to update the password for the **`ADMIN`** user:

![](images/Figure_C.7.jpg)

**Figure C.7:** Run the ***`arsadm.exe`*** ***IBM CMOD*** client program to update the password for the ***`ADMIN`*** user

The expired password is entered in the **Current Password** text box (**filenet123** on our system), and the new password (**filenet456** on our system) is entered in the **New Password** text boxes, as shown in *[Figure C.8](#appc.xhtml_figC_8)*:

![](images/Figure_C.8.jpg)

**Figure C.8:** The expired password is entered in the ***Current Password*** text box and the new password is entered in the ***New Password*** text boxes

After selecting the **OK** command button in *[Figure C.8](#appc.xhtml_figC_8)*, the new password is saved in the system. We can view and edit the **IBM CMOD** administration parameters listed in the tree node, as shown in *[Figure C.9](#appc.xhtml_figC_9)*:

![](images/Figure_C.9.jpg)

**Figure C.9:** After selecting the ***OK*** command button, the new password is saved and the parameters displayed

The **IBM ODWEK API** Java program can now be successfully rerun with the new **filenet456** password we entered, as shown in *[Figure C.10](#appc.xhtml_figC_10)*:

![](images/Figure_C.10.jpg)

**Figure C.10:** The ***IBM ODWEK API*** Java program can now be successfully rerun with the new ***filenet456*** password

# [Conclusion](#toc.xhtml_s263a)

This Appendix listed each of the **IBM CMOD** configuration files and environment settings for the Windows Client, Windows server and the Linux Server we used in writing this book.

In the last *[Appendix D, ASB Software Development Limited Publications](#appd.xhtml),* we will list the ResearchGate documents, download links to freely available IBM software documents, and previously published books.

# [Points to Remember](#toc.xhtml_s264a)

*   For a **RedHat Linux RHEL 8** system where the subscription files need to be rebuilt the original subscription can be removed completely and re-applied using the commands:

    `subscription-manager clean`

    `subscription-manager register --username xxxxxxxx --password yyyyyyy --auto-attach.`

*   The database **`drop`** command may fail unless the database activity is stopped.

    Remember that, although the IBM CMOD database drop procedure is usually applied when the table structures fail to be created (that is, an ‘empty’ database is created), it is still a good idea to backup the Db2 database first, just in case the wrong database has been selected.

*   The **`trace.settings`** file enables debugging of **`arssockd`** program issues. This file is found in the path **`/opt/ibm/ondemand/V10.5/config.`**
*   The **IBM CMOD** **`ars.ini`** file is used to store the main pointers to the other configuration files for each **IBM CMOD** instance created.
*   The **`ars.dbfs`** file is used to define the **ARCHIVE** instance database file systems, if you don’t set anything the default of the **Db2 USERSPACE1** tablespace is used.

# [Multiple Choice Questions](#toc.xhtml_s265a)

1.  Which program is used to configure the Users and Groups used in the Windows client version of IBM CMOD?
    1.  OnDemand Client V10.5 (64-bit)
    2.  Windows ARSLOAD
    3.  OnDemand Administrator V10.5 (64-bit)
    4.  OnDemand Monitor V10.5 (64-bit)
2.  Which file, in the config directory, is required to be configured for investigating errors with the **arssockd** program?
    1.  `ars.cfg`
    2.  `trace.settings`
    3.  `ars.ini`
    4.  `ars.dbfs`

# [Answers](#toc.xhtml_s266a)

1.  c
2.  b

# [Questions](#toc.xhtml_s267a)

1.  How would you correct the following error after using the drop database Db2 command:

    `SQL1035N The operation failed because the specified database cannot be`

    `connected to in the mode requested.` `SQLSTATE=57019`

2.  What configuration files would be required to create a third IBM CMOD instance called ARCHIVE3?

# [Key Terms](#toc.xhtml_s268a)

*   **LDAP: Lightweight Directory Access Protocol** is used to authenticate Users and Groups. We have used IBM Directory services (ECMUKDEMO77) for the Linux LDAP server. The windows server uses Microsoft Active Directory for the LDAP communications.
*   **TSM (IBM Tivoli Storage Manager):** Details on using this storage program with IBM CMOD can be found at the following link: [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=multiplatforms-managing-tivoli-storage-manager-storage](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=multiplatforms-managing-tivoli-storage-manager-storage).
*   **DSM:** IBM Disk Storage Manager (DSM) manages archived data stored in the IBM Content Manager OnDemand (CMOD) cache. DSM identifies when a document should be expired by using the last segment date.
*   **CACHE**: **IBM CMOD CACHE** memory storage is used to provide a fast retrieval for stored documents, the alternative archive storage used by **IBM CMOD** can take between six and sixty seconds to mount an optical or tape storage volume. Full details of the features of this storage option are covered in the following link:

    [https://www.ibm.com/docs/en/cmofm/10.5.0?topic=requirements-cache-storage-server](https://www.ibm.com/docs/en/cmofm/10.5.0?topic=requirements-cache-storage-server)

# [APPENDIX D](#toc.xhtml_appd)

# [ASB Software Development Limited Publications](#toc.xhtml_appd)

# [Introduction](#toc.xhtml_s269a)

This appendix describes the **ResearchGate** free download documents and links many of which we have referenced describing the installation of the supporting IBM software and the Linux platform. We have also listed the authors previous book publications and contact details.

# [Structure](#toc.xhtml_s270a)

In this appendix, we have the following lists:

*   ResearchGate Publications
    *   Molecular Biology Installations **- ASB Software Development Limited Publications**
    *   IBM Installations - **ASB Software Development Limited Publications**
*   Contact Details

# [ResearchGate Publications](#toc.xhtml_s271a)

The **ResearchGate** website is used by many University and Corporate research laboratories for the publication and exchange of scientific papers and questions for their community of registered users. The following lists over 30 free publications for download, several of these have already been referenced for setting up the base software systems used in this book.

# [Molecular Biology Installations - ASB Software Development Limited Publications](#toc.xhtml_s272a)

1.  [https://doi.org/10.13140/RG.2.2.26844.33925](https://doi.org/10.13140/RG.2.2.26844.33925)

    Installation of UCSF Chimera 1.4

    [https://doi.org/10.13140/RG.2.2.18753.10083](https://doi.org/10.13140/RG.2.2.18753.10083)

2.  EMBOSS Analysis Of COVID-19 GENOME SEQUENCE AND INSTALLATION ON WINDOWS 10-and RHEL 8.0

# [IBM Installations - ASB Software Development Limited Publications](#toc.xhtml_s273a)

1.  [https://orangeava.com/products/practical-java-programming-with-chatgpt](https://orangeava.com/products/practical-java-programming-with-chatgpt)

    Practical Java Programming with ChatGPT (This book serves as a supporting reference document for the **OrangeAVA** book, ***Practical Java programming for ChatGPT***, illustrating the capabilities of the AI systems we have tested.)

2.  [http://dx.doi.org/10.13140/RG.2.2.24870.13128](http://dx.doi.org/10.13140/RG.2.2.24870.13128)

    NODEJS TypeScript and ConCourse Installation on RedHat Linux8.8

3.  [http://dx.doi.org/10.13140/RG.2.2.17234.73928](http://dx.doi.org/10.13140/RG.2.2.17234.73928)

    ChatGPT [Chapter 13](#c13.xhtml) Addendum for the Additional OpenAI Java 3-Body-Problem Examples from the AVA Orange Book

4.  [https://www.researchgate.net/publication/375755079_ChatGPT_Chapter_3_Addendum_For_the_Additional_OpenAI_API_Examples_from_the_AVA_Orange_Book](https://www.researchgate.net/publication/375755079_ChatGPT_Chapter_3_Addendum_For_the_Additional_OpenAI_API_Examples_from_the_AVA_Orange_Book)

    ChatGPT [Chapter 3](#c03.xhtml) Addendum for the Additional OpenAI API Examples from the AVA Orange Book

5.  [https://link.springer.com/book/10.1007/978-1-4842-8861-0](https://link.springer.com/book/10.1007/978-1-4842-8861-0)

    IBM Software Systems Integration

    (With IBM MQ Series for JMS, IBM FileNet Case Manager, and IBM Business Automation)

6.  [https://www.amazon.co.uk/dp/B093ZNJY9L?linkCode=gs2&tag=uuid07-21](https://www.amazon.co.uk/dp/B093ZNJY9L?linkCode=gs2&tag=uuid07-21)

    Installation and Configuration of IBM Watson Analytics and StoredIQ

    ResearchGate - FREE DOWNLOADS

7.  [https://doi.org/10.13140/RG.2.2.34136.93449](https://doi.org/10.13140/RG.2.2.34136.93449)

    Audit System setup on an IBM DB2 11.5 Database on RedHat Linux RHEL 8.0 using the Go Language

8.  [https://doi.org/10.13140/RG.2.2.29470.69441](https://doi.org/10.13140/RG.2.2.29470.69441)

    Upgrade of IBM FileNet systems from DB2 10.5 FP 10 to latest DB2 11.5 version on RedHat RHEL 8.0

9.  [https://doi.org/10.13140/RG.2.2.15264.12807](https://doi.org/10.13140/RG.2.2.15264.12807)

    Jupyter notebook and its Docker Container Installation on Linux RedHat RHEL 8.0 using VMware 15.5.2

10.  [https://doi.org/10.13140/RG.2.2.27286.50240](https://doi.org/10.13140/RG.2.2.27286.50240)

    IBM Cognos Analytics 11.1.4 Installation - Linux Appendix for Fix for Zlib and Configuration for RHEL 8.0

11.  [https://doi.org/10.13140/RG.2.2.11682.38089](https://doi.org/10.13140/RG.2.2.11682.38089)

    IBM Case Analyzer 5.5 Installation and Configuration on RHEL 8.0 for Case Monitor Dashboard 5.3.3 plugin

12.  [https://doi.org/10.13140/RG.2.2.35304.83208](https://doi.org/10.13140/RG.2.2.35304.83208)

    IBM Content Search Services 5.5.3 Installation on CENTOS 8.0 and Configuration on RHEL 8.0

13.  [https://doi.org/10.13140/RG.2.2.16987.52008](https://doi.org/10.13140/RG.2.2.16987.52008)

    Importing Case Manager Solution Auto Claims example into Case Manager 5.3.3 on RHEL 8.0

14.  [https://doi.org/10.13140/RG.2.2.27057.94561](https://doi.org/10.13140/RG.2.2.27057.94561)

    IBM CEBI Content Engine Bulk Import Document Batch Tool Example on Linux Centos 8

15.  [https://doi.org/10.13140/RG.2.2.26048.69128](https://doi.org/10.13140/RG.2.2.26048.69128)

    Installation of LibreOffice 6.3.3.1 on Linux Centos 8.0

16.  [https://doi.org/10.13140/RG.2.2.12361.49767](https://doi.org/10.13140/RG.2.2.12361.49767)

    IBM Case Manager Preparation of a new Target Object Store in a FileNet P8 Docker Container on CENTOS 8

17.  [https://doi.org/10.13140/RG.2.2.11327.66721](https://doi.org/10.13140/RG.2.2.11327.66721)

    IBM Watson Explorer Foundational Components 12.0.3 Installation and Configuration on CentOS Linux 8.0

18.  [https://doi.org/10.13140/RG.2.2.12248.44803](https://doi.org/10.13140/RG.2.2.12248.44803)

    Watson Explorer 12.0.3 oneWEX Installation on IBM Cloud CENTOS 8.0 Linux with Docker Containers

19.  [https://doi.org/10.13140/RG.2.2.20256.94729](https://doi.org/10.13140/RG.2.2.20256.94729)

    IBM Cloud Private P8 Container CPIT Installation on CENTOS Linux 8.0

20.  [https://doi.org/10.13140/RG.2.2.36842.88007](https://doi.org/10.13140/RG.2.2.36842.88007)

    Installation of Eclipse Codewind and Docker Compose on RHEL 8 Linux with IBM Cloud Private CE (Community Edition)

21.  [https://doi.org/10.13140/RG.2.2.20160.69129](https://doi.org/10.13140/RG.2.2.20160.69129)

    IBM FileNet P8 Java Development on ECM Cloud Private Container P8 Examples

22.  [https://doi.org/10.13140/RG.2.2.27358.18246](https://doi.org/10.13140/RG.2.2.27358.18246)

    IBM Cloud Private P8 Container CPIT Installation on RedHat Enterprise Linux 8.0

23.  [https://doi.org/10.13140/RG.2.2.22030.92486](https://doi.org/10.13140/RG.2.2.22030.92486)

    Problem Resolution Procedures For fixing Software Installation Issues

24.  [https://doi.org/10.13140/RG.2.2.27345.89440](https://doi.org/10.13140/RG.2.2.27345.89440)

    IBM BAW 18.0 Installation phase1 preprint with install of IBM Workflow Center 8.6.1.19002

25.  [https://doi.org/10.13140/RG.2.2.10491.67369](https://doi.org/10.13140/RG.2.2.10491.67369)

    DB2 10.5 Installation on CENTOS 8.0 V1

26.  [https://doi.org/10.13140/RG.2.2.33527.57761](https://doi.org/10.13140/RG.2.2.33527.57761)

    IBM Security Directory Services 6.4- Installation on RHEL 8.0

27.  [https://doi.org/10.13140/RG.2.2.15007.10408](https://doi.org/10.13140/RG.2.2.15007.10408)

    WebSphere 8.5.5.15 Installation 29-06-2019 on VMWare Workstation Pro 15.1

28.  [https://doi.org/10.13140/RG.2.2.15737.83048](https://doi.org/10.13140/RG.2.2.15737.83048)

    IBM BAW 18.0 Installation 18 07 2019 - Install of IBM Security Directory Suite 8.0.1.1 on CENTOS 8 using VMWare Workstation Pro 15.1

29.  [https://doi.org/10.13140/RG.2.2.21708.16001](https://doi.org/10.13140/RG.2.2.21708.16001)

    Case Manager 5.3.3 Installation on RHEL 8.0 with Content Navigator 3.0.6

30.  [https://doi.org/10.13140/RG.2.2.31489.10082](https://doi.org/10.13140/RG.2.2.31489.10082)

    Installation of Oracle 12C on the Linux operating system

31.  [https://doi.org/10.13140/RG.2.2.14590.95049](https://doi.org/10.13140/RG.2.2.14590.95049)

    Content Navigator 3.0.6 Installation on RHEL 8.0_V1.docx

32.  [https://doi.org/10.13140/RG.2.2.21170.76480](https://doi.org/10.13140/RG.2.2.21170.76480)

    Content Foundation 5.5.3 Installation on RHEL 8.0_V2.docx

33.  [https://doi.org/10.13140/RG.2.2.30401.51048](https://doi.org/10.13140/RG.2.2.30401.51048)

    Case Manager Installation on RHEL 8.0_Preparation.docx

# [Contact Details](#toc.xhtml_s274a)

The scope of **IBM CMOD** extends to areas that could not possibly be covered in one book.

For errata encountered in the book, please use the [errata@orangeava.com](mailto:errata@orangeava.com) email address.

The company email provided below offers an opportunity for the reader to ask questions that are **not** errata related. For any queries on the publications referenced in this Appendix, that are specific to ASB Software Development Limited Publications, please contact the author at:

[alan.bluck@asbsoftware.co.uk](mailto:alan.bluck@asbsoftware.co.uk)

# [Index](#toc.xhtml_ind)

Symbols

</onDemand> [413](#c12.xhtml_page413)

A

Apache Zookeeper, installing [45](#c02.xhtml_page45), [46](#c02.xhtml_page46)

ARCHIVE Database, updating [203](#c05.xhtml_page203)-[205](#c05.xhtml_page205)

archive instance, updating [127](#c03.xhtml_page127)-[136](#c03.xhtml_page136)

arsaxafp command, configuring [439](#c14.xhtml_page439)-[446](#c14.xhtml_page446)

arsaxafp program, parameter [438](#c14.xhtml_page438), [439](#c14.xhtml_page439)

arsdb program [387](#c11.xhtml_page387)

arsdb program, features

index, creating [405](#c12.xhtml_page405)

system connection, logging [403](#c12.xhtml_page403)

system load, initializing [402](#c12.xhtml_page402)

system migration, initializing [404](#c12.xhtml_page404), [405](#c12.xhtml_page405)

arsload [153](#c03.xhtml_page153), [312](#c08.xhtml_page312)

ARSLOAD [417](#c13.xhtml_page417)

arsload parameters [358](#c10.xhtml_page358)

ARSLOAD Program, optimizing [428](#c13.xhtml_page428)-[430](#c13.xhtml_page430)

ARSLOAD Program, setting up

application group, exporting [409](#c12.xhtml_page409), [410](#c12.xhtml_page410)

arsxml, adding [408](#c12.xhtml_page408), [409](#c12.xhtml_page409)

first run, analyzing [407](#c12.xhtml_page407), [408](#c12.xhtml_page408)

IBM CMOD, updating [410](#c12.xhtml_page410)-[412](#c12.xhtml_page412)

users, exporting [412](#c12.xhtml_page412), [413](#c12.xhtml_page413)

ARSLOAD With Window, running [423](#c13.xhtml_page423)-[426](#c13.xhtml_page426)

arsmaint [377](#c11.xhtml_page377)

ARS_ORIGINAL_CODEPAGE [134](#c03.xhtml_page134)

arspdoci [153](#c03.xhtml_page153)

arspdump [153](#c03.xhtml_page153)

arspdump program, running [151](#c03.xhtml_page151)-[153](#c03.xhtml_page153)

arssockd [126](#c03.xhtml_page126), [173](#c04.xhtml_page173)

ARSSOCKD [417](#c13.xhtml_page417)

ARSSOCKD, debugging [178](#c04.xhtml_page178), [179](#c04.xhtml_page179)

arssockd program [377](#c11.xhtml_page377), [378](#c11.xhtml_page378)

arsstash encryption program, running [176](#c04.xhtml_page176)-[178](#c04.xhtml_page178)

arsstash program, running [308](#c08.xhtml_page308), [309](#c08.xhtml_page309)

arssyscr [402](#c12.xhtml_page402)

arsxml [272](#c07.xhtml_page272)

ARSXML [401](#c12.xhtml_page401)

B

base software package, installing [190](#c05.xhtml_page190)-[195](#c05.xhtml_page195)

Baxter Bay Credit, identifying [428](#c13.xhtml_page428)

Baxter Bay Credit, indexing [418](#c13.xhtml_page418)-[422](#c13.xhtml_page422)

C

CallbackSearchExample.java [329](#c09.xhtml_page329)

CFS-CMOD [19](#c01.xhtml_page19)

CFS-CMOD, setting up [10](#c01.xhtml_page10)-[17](#c01.xhtml_page17)

CMOD [3](#c01.xhtml_page3)

CMOD 10.5, installing [26](#c02.xhtml_page26)-[35](#c02.xhtml_page35)

CMOD ADMIN Password, updating [233](#c07.xhtml_page233)-[236](#c07.xhtml_page236)

CMOD ADMIN, resetting [228](#c06.xhtml_page228), [229](#c06.xhtml_page229)

CMOD ADMIN User Password, resetting [303](#c08.xhtml_page303), [304](#c08.xhtml_page304)

CMOD Cache Data Area [176](#c04.xhtml_page176)

CMOD Db2 Database, removing [124](#c03.xhtml_page124), [125](#c03.xhtml_page125)

CMOD Fix Pack 10.5.0.7, configuring [276](#c07.xhtml_page276)-[298](#c07.xhtml_page298)

CMOD Instances, optimizing [125](#c03.xhtml_page125)-[127](#c03.xhtml_page127)

CMOD Java API, terms

annotation, adding [406](#c12.xhtml_page406)

delete, annotations [406](#c12.xhtml_page406)

document hit, list [406](#c12.xhtml_page406)

document, retrieve [407](#c12.xhtml_page407)

document, updating [407](#c12.xhtml_page407)

logoff [406](#c12.xhtml_page406)

logon [407](#c12.xhtml_page407)

password, changing [406](#c12.xhtml_page406)

search, criteria [407](#c12.xhtml_page407)

server print, document [407](#c12.xhtml_page407)

view, annotations [407](#c12.xhtml_page407)

CMOD Linux, prerequisites [35](#c02.xhtml_page35), [36](#c02.xhtml_page36)

CMOD References, implementing [101](#c02.xhtml_page101)

CMODViewerMap [365](#c10.xhtml_page365)

Content Navigator Viewer Map, setting up [359](#c10.xhtml_page359)-[372](#c10.xhtml_page372)

crd_date [431](#c13.xhtml_page431)

D

Db2 ARCHIVE, setting up [205](#c05.xhtml_page205)-[213](#c05.xhtml_page213)

Db2 Database Server, configuring [223](#c06.xhtml_page223), [224](#c06.xhtml_page224)

db2look [306](#c08.xhtml_page306)

Db2, steps [210](#c05.xhtml_page210), [211](#c05.xhtml_page211)

Db2 Tables, configuring [122](#c03.xhtml_page122)-[124](#c03.xhtml_page124)

F

Fix Central Web Page, installing [196](#c05.xhtml_page196)-[199](#c05.xhtml_page199)

Fix Pack 10.5.0.7 Configuration, updating [427](#c13.xhtml_page427)

Fix Pack 10.5.0.7, installing [71](#c02.xhtml_page71)-[101](#c02.xhtml_page101)

Fix Pack Program, installing [199](#c05.xhtml_page199)-[203](#c05.xhtml_page203)

G

GRUB_CMDLINE_LINUX [378](#c11.xhtml_page378)

I

IBM CMOD Instance, using [387](#c11.xhtml_page387)-[397](#c11.xhtml_page397)

IBM CMOD, models

administrative model [302](#c08.xhtml_page302)

owner administrative model [303](#c08.xhtml_page303)

IBM Content Manager OnDemand (CMOD) [302](#c08.xhtml_page302)

IBM Content Navigator, configuring [347](#c10.xhtml_page347)-[355](#c10.xhtml_page355)

IBM Content Navigator, preventing [356](#c10.xhtml_page356), [357](#c10.xhtml_page357)

IBM FileNet, extensions [7](#c01.xhtml_page7)-[10](#c01.xhtml_page10)

IBM FileNet Fixed, creating [214](#c05.xhtml_page214)

IBM FileNet P8, configuring [46](#c02.xhtml_page46)-[70](#c02.xhtml_page70)

IBM Hardware, key points [5](#c01.xhtml_page5)

IBM OnDemand Full Text Search Server [382](#c11.xhtml_page382), [386](#c11.xhtml_page386)

IBM OnDemand Port Ranges, improving [380](#c11.xhtml_page380)

IBM SDSS, configuring [217](#c06.xhtml_page217)-[223](#c06.xhtml_page223)

IBM Websphere Classpath, setting up [344](#c10.xhtml_page344)-[347](#c10.xhtml_page347)

IBM WebSphere, configuring [225](#c06.xhtml_page225), [226](#c06.xhtml_page226)

IDM OnDemand Client, configuring [258](#c07.xhtml_page258)-[275](#c07.xhtml_page275)

ip_local_port_range [380](#c11.xhtml_page380)

IPv6, optimizing [378](#c11.xhtml_page378), [379](#c11.xhtml_page379)

L

LD_LIBRARY_PATH [323](#c09.xhtml_page323)

LD_LIBRARY_PATH, configuring [180](#c04.xhtml_page180)-[186](#c04.xhtml_page186)

LIBPATH [180](#c04.xhtml_page180)

Linux ARSSOCKD, optimizing [434](#c13.xhtml_page434)

Linux CMOD File Permissions, updating [305](#c08.xhtml_page305)

Linux CMOD Object Server, configuring [226](#c06.xhtml_page226)-[228](#c06.xhtml_page228)

Linux CMOD Schema, preventing [305](#c08.xhtml_page305)-[308](#c08.xhtml_page308)

Linux GSKit, installing [44](#c02.xhtml_page44)

Linux IBM FileNet P8, creating [21](#c01.xhtml_page21)-[24](#c01.xhtml_page24)

Linux IBM FileNet P8, setting up [325](#c09.xhtml_page325)-[328](#c09.xhtml_page328)

Linux Server, optimizing [381](#c11.xhtml_page381)

M

module-info.java [323](#c09.xhtml_page323)

O

ODAPI_Tests [339](#c09.xhtml_page339)

ODF, installing [153](#c03.xhtml_page153)-[160](#c03.xhtml_page160)

ODPing.java, testing [318](#c09.xhtml_page318)-[320](#c09.xhtml_page320)

ODPing, results [323](#c09.xhtml_page323), [324](#c09.xhtml_page324)

OnDemand Client, selections [240](#c07.xhtml_page240)

OnDemand Configurator Program, updating [240](#c07.xhtml_page240), [241](#c07.xhtml_page241)

OnDemand Configurator V10.5, configuring [242](#c07.xhtml_page242)-[258](#c07.xhtml_page258)

OnDemand Content Manager, creating [102](#c02.xhtml_page102)-[117](#c02.xhtml_page117)

OnDemand Content Manager, installing [160](#c03.xhtml_page160)-[169](#c03.xhtml_page169)

OnDemand Distribution Facility (ODF) [153](#c03.xhtml_page153)

OnDemand Generic Indexer, lists [312](#c08.xhtml_page312)-[314](#c08.xhtml_page314)

OnDemand Generic Indexer, utilizing [309](#c08.xhtml_page309)-[312](#c08.xhtml_page312)

P

PATH [180](#c04.xhtml_page180)

PDF indexer, installing [136](#c03.xhtml_page136)-[150](#c03.xhtml_page150)

R

RedHat RHEL 8.0, installing [37](#c02.xhtml_page37)-[43](#c02.xhtml_page43)

rpm command, installing [174](#c04.xhtml_page174)

S

Segment [288](#c07.xhtml_page288)

Server Communications [269](#c07.xhtml_page269)

SO_REUSEADDR [135](#c03.xhtml_page135)

SO_REUSEPORT [135](#c03.xhtml_page135)

SRVR_OD_STASH [328](#c09.xhtml_page328)

T

TcLoadDocs.java, configuring [333](#c09.xhtml_page333)-[338](#c09.xhtml_page338)

W

Window Server Firewall, updating [237](#c07.xhtml_page237)-[239](#c07.xhtml_page239)

Y

yum command, installing [174](#c04.xhtml_page174), [175](#c04.xhtml_page175)