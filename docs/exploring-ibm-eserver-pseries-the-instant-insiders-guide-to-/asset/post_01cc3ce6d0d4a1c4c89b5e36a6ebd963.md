
software for pSeries systems. Some of the key applications areas in which pSeries servers include enterprise resource planning (ERP), supply chain management (SCM), customer relationship management (CRM), banking, retail, science and technology, e-business/e-commerce, and business intelligence (BI).

There is a lot of overlap among these categories, since nearly every business or enterprise has some of the same computing requirements. For example, almost all organizations have customers or clients to support, and many have supplier interactions to manage. Today, almost every organization must manage Web-based interfaces for customers and employees. Finally, many different kinds of customers need real-time data to measure levels of service, orders and deliveries, and inventory.

## Custom Application Programs

Although cross-industry and industry-specific application programs fit many needs, others require software designed to perform unusual and specific tasks or to conform with existing procedures. In these cases, it is often better to develop custom application programs written to exact specifications.

Custom application programs may be written by programmers within the company or by an outside consulting firm. In either case, the basic development steps are first to write a software specification that describes what the program will do. Then a preliminary version of the program is written that demonstrates the function that will eventually be in the final program. This preliminary version is evaluated by the user, and the specification is altered to reflect any needed changes. The final program is written and installed at the user's location. Typically, training will be provided by the developer and any problems iron out. Once the user accepts the program, the software then has to be supported. That is, users need a place to go when they have questions not addressed by the manuals. Support also includes making changes to the application program as the user's needs change over time. This kind of ongoing support is critical to the success of any computer automation project.

Custom application program development is expensive and time-consuming, compared to the prewritten application program approach. But some companies may find that this additional expense and time can be recovered by the increased productivity and competitive advantage that result from custom applications that precisely fit their needs. For customers who choose the custom software approach, pseries systems and the programming tools available for the AIX 5L operating system provide a very productive software development environment.

## Operating System

Few areas in information processing create more confusion and apprehension over the operating system layer of our software model, shown in Figure 3.3. The following discussion will help remove some of the mystery associated with the Advanced Interactive e (AIX) operating system using all pSeries and RS/6000 systems. The reader will become familiar with basic operating system terms such as “active processing” and “multuser,” and then move for a closer look at the AIX 5L operating system.

The description of AIX in this chapter provides AIX 5L for POWER Version 5 Release 1 (AIX 5L v5.1) and Release 2 (AIX 5L v5.2). AIX Version 4 (AIX 4.3) has been withdrawn from marketing and service will be discontinued December 31, 2003. Users of existing p servers can upgrade to AIX 5L, and only AIX 5L is available with new systems. All earlier AIX versions and releases have been withdrawn as newer versions have been announced. IBM supports two levels of AIX at any time, the latest level (version N) and the prior level (version N-1), at which time are AIX 5L v5.2 and v5.1.

## Introduction to Operating System Concepts

The operating system provides the necessary interface that allows the user and application programs to interact with pSeries systems. The user can interact directly with the operating system’s user interface to manage files on a disk, start application programs, print files, and so on. The operating system also performs tasks directly under the control of application programs without any user assistance. The application program initiates tasks by interacting with the operating system through the application program interface (API). This is simply a set of operating system commands that can be issued directly by the application program. The API simplifies the job of the application programmer, who need not get involved with the details of hardware interaction. Further, when an application program uses the API, it is shielded from changes in the computer hardware as new computers are developed. That is, the operating system (and device drivers) can be changed to support new computer hardware while preserving the API unchanged and allowing application programs to run unchanged on the new computer.

To understand the job of the operating system, it is necessary to understand a few basic concepts:

- Batch versus interactive processing
- Multuser
- Multitasking
- Multiprocessing

### Batch Versus Interactive Processing
There are two basic types of work a computer can perform: batch processing and interactive processing. To understand the difference between these two concepts, let's use an analogy and examine the difference between two communications through the postal service and through the telephone.

If you wish to ask a distant friend some questions, you can either write a letter or phone. With the first option you gather all of your thoughts, put them on paper, and submit the letter to a mailbox. A few days later (assuming your friend is responsive) you go to your mail box and get the responses to your questions in the form of a document. This is analogous to batch processing with a computer that you can submit a request for the computer to answer some question(s) or perform task(s). Some time later (from minutes to days), you can go to the printer and get the computer's responses in the form of a report. In the early days of computing, batch processing was the only alternative for computer interaction. Today, batch processing still has its place, but interactive processing is the norm.

Moving back to our analogy, sometimes you can't simply write down your list of questions in a letter because some of the questions you have depend on the answer to one or more initial questions. In this case, you either have to send several letters back and forth between yourself and your friend or call your friend on the phone. Having a conversation with your friend over the phone is analogous to interactive processing on a computer. With interactive processing, you have a dialogue with the computer system from a PC. You enter questions or requests for activity, and the computer immediately responds. Interactive processing gives the user an immediate response, which is required and expected in most applications (e.g., airline reservations or a retail checkout line).

Some applications use a combination of batch and interactive processing. For example, a payroll clerk might enter information from time cards in a dialogue style (interactive processing). Once all time cards are entered and verified to be correct, the clerk issues a command that tells the computer to print all checks (a batch job). The clerk would later get the checks from the printer. AIX, like other operating systems, supports both batch and interactive processing.

### What Is Multiuser?
A computer system is said to be a multiuser system if two or more users share the system at the same time. With a multiuser system, from two to many hundreds of computer terminals are attached to a single computer. Each terminal provides its user with a “window” into the computer system and allows the user to perform tasks independent of all other users. Although the single computer system is being used simultaneously by many users, each user is unaware of the activities of the other users and seems to have his own computer system. However, a user may see the computer slow down (increase response time) as more and more users sign on to the computer and start working.

A multiuser computer system has several advantages over singleuser systems. Because the system hardware and programs can be simultaneously shared by many users, no one has to stand in line waiting for a turn on the computer. Everyone (assuming there are enough terminals attached) has access to the computer whenever it is needed to do a job. Other advantages offered by a multiuser system are in the areas of security, accounting, backup/recovery, and so on. The pSeries running the AIX 5L operating system can act as either a single-user or a multiuser computer system.

### What Is Multitasking?
Many people confuse multitasking with the term “multiuser” just discussed. As was just noted, “multiuser” refers to the capability to share a
