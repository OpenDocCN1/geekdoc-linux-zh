
With many certifications, it's possible to pass the associated exam even if you lack proficiency with a few objectives, as long as you have a good understanding of the other remaining objectives.

With the CLE, however, you must have a strong working knowledge of all the objectives. To be blunt, the CLE Practicum is an unforgiving pass/fail exam. More candidates fail it than pass it. This is due to the way Novell structured the CLE exam, which will be covered in more depth later in this chapter.

Novell's CLE exam incorporates multiple objectives into a given testing scenario. If you lack proficiency with one of the objectives, you could potentially fail the entire scenario, thus failing the exam.

The objectives in the CLE certification are as follows:

- Describe the characteristics of Linux.
- Use the Linux command-line interface.
- Manage the Linux file system.
- Manage Linux applications.
- Manage Linux network interfaces.
- Describe Novell Nterprise Linux Services (NNLS).
- Perform an NNLS installation.
- Manage NNLS with Red Carpet.
- Describe the purpose of eDirectory.
- Describe how eDirectory works.
- Perform eDirectory administration tasks.
- Manage user objects with iManager.
- View user information with eGuide.
- Access a Linux server with Linux User Management (LUM).
- Describe the purpose of DirXML.
- Describe how DirXML works.
- Install the DirXML Starter Pack on Linux.
- Implement the Delimited Text driver for DirXML.
- Implement the eDirectory driver for DirXML.
- Describe the purpose and architecture of iFolder.
- Install and configure iFolder.
- Describe the purpose and architecture of Samba.
- Install and configure Samba.
- Describe the role and function of NetStorage.
- Install and configure NetStorage.
- Identify the benefits of iPrint.
- Describe how iPrint works.
- Install and configure iPrint.
- Print with iPrint.
- Identify NetMail features.
- Describe NetMail components.
- Describe how NetMail works.
- Install NetMail.
- Configure and use NetMail.
- Describe Virtual Office.
- Install Virtual Office.
- Configure Virtual Office.

## Using This Study Guide

To pass the CLE exam, you must have both the theoretical knowledge and the technical skills reflected in the objectives. This *Study Guide* is designed to provide you with both of these elements.

First, each chapter in this *Study Guide* presents conceptual information related to each CLE objective. For chapters that are heavy with conceptual information, you will find a “Check for Understanding” exercise at the end that you can use to verify that you have mastered the information presented.

It is critical that you take time to complete these activities. Use the results to identify information you may need to review. Doing so will greatly increase the likelihood that you will pass the CLE exam.

Second, each chapter in this study, with the exception of this one, includes one or more hands-on exercises to help you gain the Linux and NNLS skills required to pass the CLE exam. As you progress through this guide, you will build a complete NNLS implementation, piece by piece, from the ground up.

Again, it is absolutely critical that you complete these exercises. The CLE exam requires that you be able to complete these tasks in a live NNLS environment.

This is a departure from most certification exams in the IT industry today. They generally require you to complete an exam that tests your mastery of only the conceptual subject matter. The CLE, on the other hand, tests your ability to do the tasks specified in the objectives.

To complete these exercises, you will need the following equipment:

- **A lab PC**—This computer must meet the following specifications:
  - **CPU**—Pentium III 800MHz or later
  - **Memory**—512MB minimum
  - **Hard disk**—4GB or more
  - **Peripherals**—Printer, monitor, mouse, and keyboard
- **A copy of NNLS 1.0**—An evaluation copy of NNLS is available from Novell at http://www.novell.com.
- **A copy of SLES 8**—An evaluation copy of SLES 8 is available from Novell at http://www.novell.com. It’s important to note that NNLS will run on other Linux distributions. However, the only supported distributions are SUSE Linux Enterprise Server 8 and Red Hat Enterprise Server 2.1. Because SLES 8 is specified in the CLE objectives, this is the distribution used in this *Study Guide*. If you choose to use a different distribution, some of the steps in the hands-on exercises may not work.

### Introduction to the CLE Test Environment

Let’s discuss the CLE exam in a little more detail. As mentioned earlier, the CLE exam is called a “practical” exam, and you may hear it referred to as “The CLE Practicum.” They mean one and the same thing.

### Why Practical Exams Are Used

Traditional certification exams in the IT industry usually provide the student with a series of multiple-choice, fill-in-the-blank, and matching questions, as shown in Figure 1.1.

![](img/c7771e8540507f2b00c088c7a411b57b_25_0.png)

The strength of these types of exams is the fact that they are very effective at evaluating your mastery of theoretical concepts. They are also easier to create and deliver.

Their weakness is the fact that they don't test your ability to actually perform the tasks specified in the objectives. In other words, they tend to evaluate what you know instead of what you can do. You may have heard the term *paper certified* before. This term refers to network administrators who have passed the multiple-choice exam for their certification, but who can't actually perform on the job. Novell wanted to make sure this situation didn't happen with the CLE certification.

Novell has been a pioneer in the field of practical testing since its Certified Directory Engineer (CDE) certification was introduced in 1999. Novell has implemented exams that present you with a scenario and then require you, without guidance, to determine the proper resolution and to implement that resolution correctly.

The strength of this strategy is that it truly verifies whether you have mastered the skills specified in the objectives.

Students who pass a practical test are much more likely to be able to perform better on the job than those who pass traditional exams only. To a job applicant, this is of high value. It gives you bargaining power with an employer, allowing you to provide a higher degree of verification of your skill set.

Unfortunately, "certified" IT job applicants have burned many employers over the years. Because their skills were only verified at the conceptual level, their ability to actually do the job was sometimes less than what was necessary.

Practical certification testing helps employers filter out less qualified job applicants. When you apply for a job, employers can have a higher degree of confidence in your abilities if you have successfully completed a practical exam.

You should, however, be aware that the pass rate on practical exams tends to be much lower than traditional exams. To pass the CLE practical exam, you will probably have to spend twice as much time preparing as you would for a traditional certification exam. Interestingly, Novell reports that even though the pass rate on the CLE exam is lower than a traditional exam, most candidates feel the test was a fair one—even those that fail. Some exam-preparation tips are presented later in this chapter.

## How the CLE Practicum Works

The CLE Practicum is composed of the components shown in Figure 1.2.

![](img/c7771e8540507f2b00c088c7a411b57b_26_0.png)

**FIGURE 1.2**
The CLE Practicum.

The role of each of these components is as follows.

### The Testing Center Computer

The first component in the CLE Practicum is the testing center computer. In order to complete the Practicum, you must schedule a test with a Novell education partner center. This can be done by visiting http://practicum.novell.com/partner_search.php. At the testing center, you will use a Web browser on the testing center computer to access the virtual servers running on the Novell server. The CLE exam interface is shown in Figure 1.3.

![](img/c7771e8540507f2b00c088c7a411b57b_27_0.png)

### The Novell Server

The second component in the Practicum is the Novell server. This server is maintained at Novell’s Provo campus and is used to run VMware, a product that allows multiple operating systems to be run simultaneously on a single computer. More information about VMware can be found at http://www.vmware.com.

### Virtual Servers

The final Practicum component is the group of virtual server sessions running on the Novell server. Each session represents a SUSE Linux server. These servers have been preconfigured using a specific scenario.
