
## 8.4 Case study
263

### 8.4.1 Memory card
263

### 8.4.2 OSA
264

### 8.4.3 DASD errors
265

### 8.4.4 Network interface error upon reboot
266

### 8.4.5 DASD recognition problem in boot process
267

# Chapter 9. Installation and setup problems
269

## 9.1 Understanding the installation process
270

## 9.2 Gathering information regarding installation process
275

## 9.3 Scenarios
282

### 9.3.1 Trouble during the installation
282

### 9.3.2 Trouble after the installation
283

# Chapter 10. Booting problems
285

## 10.1 Understanding the boot process
286

### 10.1.1 IPL phase
287

### 10.1.2 Boot loader phase
287

### 10.1.3 Kernel phase
290

### 10.1.4 Init phase
293

## 10.2 Where to gather information regarding boot process
297

## 10.3 Commands
305

## 10.4 Boot problem examples
306

## 10.5 Scenarios
308

### 10.5.1 IPL failure
308

### 10.5.2 Failing in kernel booting
309

### 10.5.3 Failing since the init phase
309

### 10.5.4 Failure to start a service
311

# Chapter 11. Case study: slow responding Web site
313

## 11.1 Three-tier Web application environment
314

### 11.1.1 Trade 6 Web serving application
314

### 11.1.2 Our Web serving setup
315

### 11.1.3 WebSphere Studio Workload Simulator
317

## 11.2 Symptoms of the problem
317

### 11.2.1 Investigation of the problem
320

### 11.2.2 Post investigation tuning
322

### 11.2.3 What if the load is increased - does the problem reappear
322

## 11.3 z/VM to the rescue
323

## 11.4 Emergency scanning
329

**Related publications**
333

Online resources
333

How to get Redbooks
334

Help from IBM
334

**Index**
335

# Notices

This information was developed for products and services offered in the U.S.A.

IBM may not offer the products, services, or features discussed in this document in other countries. Consult your local IBM representative for information on the products and services currently available in your area. Any reference to an IBM product, program, or service is not intended to state or imply that only that IBM product, program, or service may be used. Any functionally equivalent product, program, or service that does not infringe any IBM intellectual property right may be used instead. However, it is the user's responsibility to evaluate and verify the operation of any non-IBM product, program, or service.

IBM may have patents or pending patent applications covering subject matter described in this document. The furnishing of this document does not give you any license to these patents. You can send license inquiries, in writing, to:
IBM Director of Licensing, IBM Corporation, North Castle Drive, Armonk, NY 10504-1785 U.S.A.

The following paragraph does not apply to the United Kingdom or any other country where such provisions are inconsistent with local law: INTERNATIONAL BUSINESS MACHINES CORPORATION PROVIDES THIS PUBLICATION "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESS OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF NON-INFRINGEMENT, MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE. Some states do not allow disclaimer of express or implied warranties in certain transactions, therefore, this statement may not apply to you.

This information could include technical inaccuracies or typographical errors. Changes are periodically made to the information herein; these changes will be incorporated in new editions of the publication. IBM may make improvements and/or changes in the product(s) and/or the program(s) described in this publication at any time without notice.

Any references in this information to non-IBM Web sites are provided for convenience only and do not in any manner serve as an endorsement of those Web sites. The materials at those Web sites are not part of the materials for this IBM product and use of those Web sites is at your own risk.

IBM may use or distribute any of the information you supply in any way it believes appropriate without incurring any obligation to you.

Information concerning non-IBM products was obtained from the suppliers of those products, their published announcements or other publicly available sources. IBM has not tested those products and cannot confirm the accuracy of performance, compatibility or any other claims related to non-IBM products. Questions on the capabilities of non-IBM products should be addressed to the suppliers of those products.

This information contains examples of data and reports used in daily business operations. To illustrate them as completely as possible, the examples include the names of individuals, companies, brands, and products. All of these names are fictitious and any similarity to the names and addresses used by an actual business enterprise is entirely coincidental.

# COPYRIGHT LICENSE:

This information contains sample application programs in source language, which illustrate programming techniques on various operating platforms. You may copy, modify, and distribute these sample programs in any form without payment to IBM, for the purposes of developing, using, marketing or distributing application programs conforming to the application programming interface for the operating platform for which the sample programs are written. These examples have not been thoroughly tested under all conditions. IBM, therefore, cannot guarantee or imply reliability, serviceability, or function of these programs.

# Trademarks

IBM, the IBM logo, and ibm.com are trademarks or registered trademarks of International Business Machines Corporation in the United States, other countries, or both. These and other IBM trademarked terms are marked on their first occurrence in this information with the appropriate symbol (® or ™), indicating US registered or common law trademarks owned by IBM at the time this information was published. Such trademarks may also be registered or common law trademarks in other countries. A current list of IBM trademarks is available on the Web at http://www.ibm.com/legal/copytrade.shtml

The following terms are trademarks of the International Business Machines Corporation in the United States, other countries, or both:

| AIX® | IBM® | System z9® |
|---|---|---|
| DB2® | Lotus® | Tivoli® |
| developerWorks® | OMEGAMON® | TotalStorage® |
| ECKD™ | OS/390® | WebSphere® |
| ESCON® | Redbooks® | z/OS® |
| eServer™ | Redbooks (logo)® | z/VM® |
| FICON® | REXX™ | z9™ |
| GDDM® | S/390® | zSeries® |
| HiperSockets™ | System z™ | |

The following terms are trademarks of other companies:

SUSE, the Novell logo, and the N logo are registered trademarks of Novell, Inc. in the United States and other countries.

Oracle, JD Edwards, PeopleSoft, Siebel, and TopLink are registered trademarks of Oracle Corporation and/or its affiliates.

J2EE, Java, JavaServer, JVM, Voyager, and all Java-based trademarks are trademarks of Sun Microsystems, Inc. in the United States, other countries, or both.

Excel, Windows, and the Windows logo are trademarks of Microsoft Corporation in the United States, other countries, or both.

UNIX is a registered trademark of The Open Group in the United States and other countries.

Linux is a trademark of Linus Torvalds in the United States, other countries, or both.

Other company, product, or service names may be trademarks or service marks of others.
