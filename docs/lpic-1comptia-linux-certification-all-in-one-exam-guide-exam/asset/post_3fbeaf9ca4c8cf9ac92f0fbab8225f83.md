
## Taking the Exams

As I mentioned earlier, I’ve written a number of industry certification exams in addition to developing training materials for them. Because I’ve done this, I have some insights as to what goes on inside the devious minds of exam developers. I’m going to share them with you here.

- Carefully read the text of each question (called the stem). Some of the information in the stem is superfluous and intended to distract you. However, the question stem usually contains one or two critical pieces of information that influence the correct answer. If your testing center provides you with writing materials (and they should), I suggest you quickly jot down the key points from the stem.
- Carefully read each response. Don’t just skim them. Exam authors deliberately include responses that are almost correct, but not quite. (We call them red herrings.) The intent is to distract you away from the real answer. I know it sounds sneaky, but the intent is to make the exam such that you can’t divide the correct answer without really knowing your stuff.
- Eliminate responses that are obviously wrong. Each item will have one or more responses that are blatantly wrong. (Usually, it’s because the exam author couldn’t think of anything better to include as a response.) Eliminate these answers and focus only on the responses that could be correct.
- Make your best choice and move on. My experience has been that your first impression is usually the correct one. If you agonize over the answers, you can over-think the question and end up picking the wrong response. You also waste valuable time. After carefully reading the question and each response, go with your intuition and then go on to the next item.
- If you get stuck on a particularly difficult item, don’t waste a lot of time trying to figure out the right answer. You can skip the item and come back to it later. Many students get obsessed with finding the right answer to a particularly difficult question and end up with insufficient time to answer the rest of the items on the exam. Answer the questions that you can and then come back to the difficult questions that will require more time.

After you finish your exams, your results will be automatically printed out for you. The report will be embargoed by your test proctor to certify the results. Don’t lose these reports; it’s the only hard copy you will receive! I’ve heard of candidates who’ve had to send a paper copy of their exam report back to CompTIA when technical problems prevented their test results from being transmitted correctly.

The report will display your performance on each section of the exams. The LPIC-1/CompTIA Linux+ exams are pass-fail. If you score 500 or better, you pass! A candidate with a score of 577 is every bit as certified as a candidate with a score of 798.

If you didn’t pass, you can use the information on your report to identify the areas where you need to study. You can retake the exams immediately, if you wish. However, there are two things you need to keep in mind before you do this:

- You have to pay full price for the retake.
- The retake exam probably won’t be the same as the first. CompTIA publishes multiple forms of the LPIC-1/CompTIA Linux+ exams.

However, if you don’t pass again, you must wait at least 14 days before you will be allowed to take the exam a third time.

If you fail, I suggest that you step back, take a deep breath, go home, and study up on the items you missed. Then schedule your retake within a day or two. If you wait any longer than that, your mind will probably go “cold” and you may need to go through the entire preparation process again from scratch.

## Introduction to Linux

In this chapter you will learn about:

- The role and function of Linux
- The historical development of Linux
- Linux distributions
- Common Linux roles

The introduction and adoption of Linux has been an interesting drama to observe. When Linux was first introduced back in the early 1990s, it was greeted with a collective yawn. The big operating system vendors of the day, including Microsoft, IBM, Oracle, and Novell, barely even noticed. At the time, Linux was considered a hobbyist's plaything, reserved for only the geekiest of geeks.

Since that time, however, Linux has made steady progress into the server room in an increasing number of organizations around the world. So much so, in fact, that everyone in the information technology industry is starting to pay attention, including the big four just mentioned.

Linux has even started making inroads into the desktop market, in many cases replacing the Microsoft Windows operating system used by employees in many organizations. Since its introduction in the early '90s, Linux has gone from a programmer's pet project to a major force for change in the information technology industry.

As such, there is a growing demand for network administrators who can implement, maintain, and support the Linux operating system. If you've had any experience with Linux, you know that it is very different than the operating systems most users are familiar with, such as Microsoft Windows. Migrating from these systems to Linux requires a degree of expertise. By the time we're done with this book, you will have the knowledge and skills required to make this happen. You will also be able to pass the LPIC-1/CompTIA Linux+ exam!

Before I can launch into a discussion of how to install and configure Linux, you need to have a solid understanding of where Linux came from, how you can get it, the roles it can play in your network, and the tools you can use to interact with the operating system.

### The Role and Function of Linux

When learning about Linux, you must first understand the role Linux plays in a computer system. Linux is an *operating system*, not an application. All operating systems, including Linux, provide five key functions in a computer system:

- **Application platform** An operating system provides a platform where applications can run, managing their access to the CPU and system memory.
- **Hardware moderator** The operating system also serves as a mediator between running applications and the system hardware. Most applications are not written to directly address a computer's hardware. Instead, most operating systems include prewritten code that can be called from an application to access system hardware, such as memory, hard drives, and communication ports. This feature makes life much easier for programmers. Instead of having to write code for completing these tasks in each and every program, they can simply reuse this existing code provided by the operating system. It also ensures that one application running on the system doesn't try to use memory already in use by another application, and that applications don't use an inordinate amount of CPU time.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_45_0.png)

> **TIP** Operating systems manage applications by allocating each application a memory range it can use. The operating system manages memory access to ensure that one application doesn't try to use memory that's being used by another application. The operating system also controls access to the CPU.

- **Data storage** The operating system is also responsible for providing an efficient and reliable means for storing information. Usually this is done using some type of storage device, such as a hard disk drive, that has been formatted with a particular type of file system that organizes the information in an easily retrievable format.
- **Security** The operating system is responsible for providing a degree of security for the data stored in it. The system administrator can create rules and grant rights that determine who can access what information. Some operating systems, such as Linux and later versions of Windows, do this job very well. Older operating systems, such as DOS or Windows 98, provided little or no security.
- **Connectivity** The operating system manages connectivity between computer systems using a variety of network media and interfaces, including infrared, Ethernet, RS-232, and 802.11x wireless.

Believe it or not, I occasionally encounter people who don't understand the role Linux plays in a computer system. They are under the mistaken impression that Linux is some kind of killer application that they can run under Windows on their workstation.
