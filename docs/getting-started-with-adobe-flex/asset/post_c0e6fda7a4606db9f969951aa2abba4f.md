
# Getting Started With Adobe Flex

Ideal for application developers and administrators

by:

Amitava Kundu
Charu Agarwal
Anushka Chandrababu
Mukul Kumar
Karthik Ramanarayanan
Raul F. Chong

![](img/c4119654311ebf24679359ca130a5ee6_0_0.png)

DB2 ON CAMPUS BOOK SERIES

# GETTING STARTED WITH Adobe Flex

A book for the community by the community

Amitava Kundu, Charu Agarwal, Anushka Chandrababu, Mukul Kumar, Karthik Ramanarayanan, Raul F. Chong

FIRST EDITION

First Edition (May 2010)

© Copyright IBM Corporation 2010. All rights reserved.

IBM Canada
8200 Warden Avenue
Markham, ON
L6G 1C7
Canada

## Notices

This information was developed for products and services offered in the U.S.A.

IBM may not offer the products, services, or features discussed in this document in other countries. Consult your local IBM representative for information on the products and services currently available in your area. Any reference to an IBM product, program, or service is not intended to state or imply that only that IBM product, program, or service may be used. Any functionally equivalent product, program, or service that does not infringe any IBM intellectual property right may be used instead. However, it is the user's responsibility to evaluate and verify the operation of any non-IBM product, program, or service.

IBM may have patents or pending patent applications covering subject matter described in this document. The furnishing of this document does not grant you any license to these patents. You can send license inquiries, in writing, to:

IBM Director of Licensing
IBM Corporation
North Castle Drive
Armonk, NY 10504-1785
U.S.A.

For license inquiries regarding double-byte character set (DBCS) information, contact the IBM Intellectual Property Department in your country or send inquiries, in writing, to:

Intellectual Property Licensing
Legal and Intellectual Property Law
IBM Japan, Ltd.
3-2-12, Roppongi, Minato-ku, Tokyo 106-8711

The following paragraph does not apply to the United Kingdom or any other country where such provisions are inconsistent with local law: INTERNATIONAL BUSINESS MACHINES CORPORATION PROVIDES THIS PUBLICATION "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF NON-INFRINGEMENT, MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE. Some states do not allow disclaimer of express or implied warranties in certain transactions, therefore, this statement may not apply to you.

This information could include technical inaccuracies or typographical errors. Changes are periodically made to the information herein; these changes will be incorporated in new editions of the publication. IBM may make improvements and/or changes in the product(s) and/or the program(s) described in this publication at any time without notice.

Any references in this information to non-IBM Web sites are provided for convenience only and do not in any manner serve as an endorsement of those Web sites. The materials at those Web sites are not part of the materials for this IBM product and use of those Web sites is at your own risk.

IBM may use or distribute any of the information you supply in any way it believes appropriate without incurring any obligation to you.

The licensed program described in this document and all licensed material available for it are provided by IBM under terms of the IBM Customer Agreement, IBM International Program License Agreement or any equivalent agreement between us.

Any performance data contained herein was determined in a controlled environment. Therefore, the results obtained in other operating environments may vary significantly. Some measurements may have been made on development-level systems and there is no guarantee that these measurements will be the same on generally available systems. Furthermore, some measurements may have been estimated through extrapolation. Actual results may vary. Users of this document should verify the applicable data for their specific environment.

Information concerning non-IBM products was obtained from the suppliers of those products, their published announcements or other publicly available sources. IBM has not tested those products and cannot confirm the accuracy of performance, compatibility or any other claims related to non-IBM products. Questions on the capabilities of non-IBM products should be addressed to the suppliers of those products.

All statements regarding IBM's future direction or intent are subject to change or withdrawal without notice, and represent goals and objectives only.

This information contains examples of data and reports used in daily business operations. To illustrate them as completely as possible, the examples include the names of individuals, companies, brands, and products. All of these names are fictitious and any similarity to the names and addresses used by an actual business enterprise is entirely coincidental.

COPYRIGHT LICENSE:

This information contains sample application programs in source language, which illustrate programming techniques on various operating platforms. You may copy, modify, and distribute these sample programs in any form without payment to IBM, for the purposes of developing, using, marketing or distributing application programs conforming to the application programming interface for the operating platform for which the sample programs are written. These examples have not been thoroughly tested under all conditions. IBM, therefore, cannot guarantee or imply reliability, serviceability, or function of these programs. The sample programs are provided "AS IS", without warranty of any kind. IBM shall not be liable for any damages arising out of your use of the sample programs.

References in this publication to IBM products or services do not imply that IBM intends to make them available in all countries in which IBM operates.

If you are viewing this information softcopy, the photographs and color illustrations may not appear.

Adobe product screenshot(s) reprinted with permission from Adobe Systems Incorporated.

## Trademarks

IBM, the IBM logo, and ibm.com are trademarks or registered trademarks of International Business Machines Corp., registered in many jurisdictions worldwide. Other product and service names might be trademarks of IBM or other companies. A current list of IBM trademarks is available on the Web at "Copyright and trademark information" at www.ibm.com/legal/copytrade.shtml.

Adobe, the Adobe logo, Flex, Flex Builder, PostScript, and the PostScript logo are either registered trademarks or trademarks of Adobe Systems Incorporated in the United States, and/or other countries.

Java and all Java-based trademarks are trademarks of Sun Microsystems, Inc. in the United States, other countries, or both.

Microsoft and Windows are trademarks of Microsoft Corporation in the United States, other countries, or both.

Linux is a registered trademark of Linus Torvalds in the United States, other countries, or both.

UNIX is a registered trademark of The Open Group in the United States and other countries.

Other company, product, or service names may be trademarks or service marks of others.

# Table of Contents

- Preface ..... 14
  - Who should read this book? ..... 14
  - How is this book structured? ..... 14
  - A book for the community ..... 15
  - Conventions ..... 15
  - What's next? ..... 15
- About the Authors ..... 17
- Contributors ..... 19
- Acknowledgements ..... 19
- Chapter 1 — Introduction to Adobe Flex ..... 20
  - 1.1 A brief history of Adobe Flex ..... 20
  - 1.2 Pros and cons of Flex applications ..... 25
  - 1.3 Versions and editions of Adobe Flex ..... 26
    - 1.3.1 Adobe Flex 3 SDK ..... 26
    - 1.3.2 Adobe Flex Builder 3 ..... 26
    - 1.3.3 Adobe Data Services ..... 27
  - 1.4 The Flex Community ..... 27
    - 1.4.1 Developer Resources ..... 27
    - 1.4.2 Discussion Forums ..... 28
    - 1.4.3 Adobe Flex Blogs ..... 28
  - 1.5 Comparing Adobe Flex with similar products ..... 28
    - 1.5.1 Adobe Flex and HTML/JavaScript/Ajax ..... 28
    - 1.5.2 Adobe Flex and Flash IDE ..... 29
    - 1.5.3 Adobe Flex and Java/JavaFX ..... 29
    - 1.5.4 Adobe Flex and Java Server Faces (JSF) ..... 29
    - 1.5.5 Adobe Flex and Microsoft Silverlight ..... 30
  - 1.6 Summary ..... 30
  - 1.7 Review questions ..... 30
- Chapter 2 — Installing Flex ..... 32
  - 2.1 Installing Flex: The big picture ..... 32
  - 2.2 Installing Flex using the setup wizard ..... 33
    - 2.2.1 Installing Eclipse ..... 33
    - 2.2.2 Installing Flex Builder ..... 33
  - 2.3 Launching Flex Builder ..... 38
  - 2.4 Developing your first Flex application ..... 40
    - 2.4.1 Building and running the "Hello Flex" application ..... 40
    - 2.4.2 Debugging the Flex application ..... 50
  - 2.5 Exercises ..... 53
  - 2.6 Summary ..... 53
  - 2.7 Review questions ..... 53
- Chapter 3 - Introduction to MXML and ActionScript ..... 55
  - 3.1 MXML and ActionScript — the Big Picture ..... 55
  - 3.2 MXML ..... 57
