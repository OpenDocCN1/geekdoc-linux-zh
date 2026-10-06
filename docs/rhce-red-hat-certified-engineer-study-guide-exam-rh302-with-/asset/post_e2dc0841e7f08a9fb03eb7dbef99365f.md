
# Acknowledgments

contribution) and Ellen Bliss, Technical Editorial Coordinator (think of her as the songwriting manager who had the wisdom to choose Randy and Utiman to write the screenplay). Stars include Dennis Fitzgerald, Production Editor (think of him as this year's best actor); Julie Sakaue, and Suzanne Goraj, Editors (think of them as this year's best actresses in supporting- roles). Each of these folks deserves an Oscar—or perhaps two Oscars—just for putting up with my idiosyncrasies and increasingly poor memory and lack of attention to detail.

Several others who didn't work directly on the book merit special mention. My home crew—Jennifer, Patrick, and Sara—seem by now to have become incurred of my book writing habits. Thanks to them for handling the bills, the moving of furniture, and the household chores while I indulged my writing habit. Finally, and emphatically, I thank the Lord and Savior, Jesus Christ, who knows my many flaws and weaknesses better than any other and nevertheless patiently bears with me knowing that He—how, I don't know—can make something remarkable of me. I can't wait!

# Introduction

Like many in the Linux community, you've probably heard of the Red Hat Certified Engineer (RHCE) program and the related RHCE exam, both of which were created by Red Hat, Inc. You may have heard that the RHCE exam is challenging, or you may have heard that it is not. You may have heard that the exam is focused on Red Hat Linux and that knowledge of Unix or Linux distribution other than Red Hat Linux will not help you pass the exam. Most of all, you may have wondered how RHCE certification might boost your career, or you're a hiring manager help you find qualified employees. I wrote this book to answer these questions and similar questions and provide comprehensive material and exercises designed to prepare you to pass the RHCE exam.

# Is This Book for You?

If you want to learn how to administer a Red Hat system, this is the book for you. In it, you'll find clear and comprehensive explanations of the concepts you need to understand and the procedures you need to be able to perform.

If you plan to take the RHCE exam, you will find this book to be even more valuable, because it focuses on the topics identified by Red Hat, Inc., as central to the RHCE exam. It contains many practice questions and exercises that will help you to prepare and assess your readiness to take the RHCE exam. The book includes both questions and exercises because the RHCE has two kinds of tests: written and performance-based exams. The questions you prepare for the written part of the RHCE exam, and the exercises you prepare for the performance-based part of the exam. Once you will be able to approach the RHCE exam with confidence.

However, the RHCE exam and this book are not for everyone. The RHCE exam is mostly a hands-on exam that attempts to assess your system administration skills. This book will help you to learn and refine these skills, unless you've had some experience with Unix or Linux, you probably won't make much sense of this book or the RHCE exam. To succeed, you don't need to be a Unix or Linux power user who has experience in system installation and administration—although it certainly won't hurt if you are—but you should be at least a Unix or Linux power user who has experience in system installation and administration. figuring out some system administration commands as mount and unmount, you can expect to understand the material in this book.

# What Does This Book Cover?

I've endeavored to cover every topic that is important to a Red Hat system administrator, especially emphasizing those topics that are likely to appear on the RHCE exam. I must write endeavored to, because those—like myself—who have taken the RHCE exam are bound by a non-disclosure agreement and cannot divulge the contents of the exam. Moreover, Red Hat, Inc. regularly updates the RHCE exam with new questions and exercises. So, no program of study for the RHCE exam is or be a substitute for real knowledge. But this book can help you develop exactly the sort and degree of real knowledge required to pass the RHCE exam. Among the central topics covered are the following:

- RHCE certification and the RHCE exam
- A review of PC hardware, Unix, and networking that will help you fill the gaps in what you already know
- Red Hat Linux installation
- Red Hat Linux system and network administration
- Network server administration
- X Window system administration
- Red Hat Linux security administration
- System troubleshooting and repair

At the time of writing, Red Hat, Inc. had just released Red Hat Linux 6.2 and was updating the RHCE exam to reflect the new and changed features of Red Hat Linux 6.2. Thus, this book was written with Red Hat Linux 6.2 and the RHCE exam for Red Hat Linux 6.2 in mind.

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_7_0.png)

If you pass the RHCE exam, your certification will remain current for one year, irrespective of any new versions of Red Hat Linux released during that time.

# How Do You Take the RHCE Exam?

The RHCE exam tests your conceptual understanding and skill in performing Red Hat Linux system administration tasks. The exam takes about seven hours, including a one-hour break for lunch. The exam is challenging: currently one out of three examines fails the exam. However, proper preparation for the exam can significantly increase your likelihood of success.

Red Hat, Inc., offers the RHCE exam about a month at our Durham, NC headquarters and frequently at our Santa Clara, California, Facility. At the time of writing, Red Hat, Inc. had just announced that it will soon offer the RHCE exam in Europe and East Asia. The RHCE exam is also offered in several cities by Red Hat, Inc.’s training partners, including Global Knowledge and IBM Services.

You can take the RHCE exam or a special-day RHCE preparation course, the price of which includes the exam, which is taken the following day. The Red Hat, Inc. course numbers and the cost at the time of writing as follows:

- RHCE exam only RH302 ($749)
- RHCE exam and preparation course RH300 ($2,498)

To register for an RHCE exam or RHCE exam preparation course by Red Hat, Inc., at a U.S. location, call (800) 454-5502 or e-mail training@redhat.com., also check the following Web sites for up-to-the-minute details and additional registration information:

- Red Hat, Inc. www.redhat.com/services/training/training.html
- Global Knowledge db.globalknowledge.com/olm/go.asp?find=redhat
- IBM Services www.ibm.com/services/learning/spotlight.html

> NOTE Chapter 1, “Red Hat Certification,” and Chapter 31, “The RHCE Exam,” provide further information on RHCE certification and the RHCE exam.

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_8_0.png)

# How to Use This Book

This book has quite a few chapters—31, to precise. Most of the chapters are small and focused so that you can quickly find and review topics. Small chapters also help you pace your study so that you avoid burn out. A few chapters, such as the chapter on installing Red Linux, are longer than most, but generally, their length is attributable to screen shots that will help you stay oriented to the procedures those chapters explain.

>> Be sure to read the inside front cover page of this book discusses what's on the companion CD.

Because the chapters are small, the book is organized into parts that group related chapters:

- **Part I: Background** Chapters 1–5 explain RHCE certification and review basic material on PC hardware, Unix, TCP/IP networking, and Linux. You're probably familiar with much of this material already, so feel free to skip these chapters, using these chapters to fill in gaps in your recollection and understanding.
- **Part II: Installation** Chapters 6–8 describe the procedure for installing Red Hat Linux, including pre-installation and advanced installation techniques.
- **Part III: Configuration and Administration** Chapters 9–20 describe and explain Red Hat system administration, including such topics as user accounts, disk quotas, and RPM packages.
- **Part IV: Network Services Administration** Chapters 21–25 describe and explain the administration of network services. They include material on Apache, FGFS, Squid, and a variety of other servers, plus material on network security and system logs.
- **Part V: X Window System Administration** Chapters 26–28 concern the X Window System, the Unix standard graphical user interface.
- **Part VI: Network Administration** Chapters 29 and 30 cover routers and firewalls.
- **Part VII: The RHCE Exam (RH302)** Chapter 31 describes the RHCE exam in detail and gives suggestions for performing well on the.
