
- The Internet 217
- Domains 217
- Hostname 218
- Hardware Address 218
- Basic Communication 219
- IP Addressing 219
- Address Classes 220
- Addresses 220
- Network Mask 221
- Setting Up a Network 222
- Gateway 223
- Access Controls 224
- Other Network Services 224
- Domain Name Service (DNS) 224
- Dynamic Host Configuration Protocol (DHCP) 225
- Network File System (NFS) 225
- Samba 226
- sendmail 226
- Apache 226
- Network Applications 227
- Web Browsers 227
- Mail Managers 227
- FTP Clients 227
- Telnet 228
- Practice Questions 229
- Need to Know More? 234

## Chapter 13 Applications 235
- The Linux WYSIWYG Debate 236
- WYSIWYG Applications 236
- Markup Languages 237
- Document Processing Managers 237
- WordPerfect 238
- Star Office 238
- Applixware 238
- KOffice 239
- GNOME Office 239
- Text Processing Managers 239
- vi 239
- ispell 240
- Graphical Applications 240
- GIMP 241
- xfig 241
- Practice Questions 243
- Need to Know More? 247

## Chapter 14 Troubleshooting
- Problem-Solving Philosophy 250
- Quick Tools 250
- Scientific Method 251
- System Logs 252
- Log Locations 252
- System Log Messages 253
- Installation Issues 253
- Read Errors 254
- Archive Errors 254
- Not Enough Space 254
- Bad Hard Disk Blocks 255
- Other Installation Issues 255
- Rescue Disk Help 256
- Creating a Boot Floppy 256
- Components of the Boot Floppy 256
- Problems with the Master Boot Record (MBR) 257
- Incorrect Operating System 257
- Shell Problems 257
- Restoring Passwords 257
- Restoring Passwords with a Boot Floppy 258
- Dynamic Library Modules 258
- Printer Problems 258
- Other Problems 259
- Weird Characters 260
- Num Lock 260
- Keyboard Repeat Rate 260
- Synchronizing Time 260
- X Window Thrashing 261
- Problem Opening the X Window 261
- Practice Questions 262
- Need to Know More? 270

## Chapter 15 Sample Test 271
- Questions, Questions, Questions 272
- Choosing Proper Answers 272
- Decoding Ambiguity 273
- Working within the Framework 274
- Deciding What to Memorize 274
- Preparing for the Test 275
- Taking the Test 275
- Sample Test 277

## Chapter 16 Answer Key 295
## Appendix 307
## Glossary 315
## Index 339

## Introduction
Welcome to Sair Linux/GNU Installation and Configuration Exam Cram! This book aims to help you get ready to take—and pass—the Sair Linux/GNU Installation and Configuration Level 1 certification exam 3X0-101. This Introduction explains Sair's certification programs in general and talks about how the Exam Cram series can help you prepare for Sair's certification exams.

Exam Cram books help you understand and appreciate the subjects and materials you need to pass Sair certification exams. Exam Cram books are aimed strictly at test preparation and review. They do not teach you everything you need to know about a topic (such as the ins and outs of building your own RPMs). Instead, I present and dissect the questions and problems I've found that you're likely to encounter on a test. I've worked from Sair's own training materials, preparation guides, and tests. My aim is to bring together as much information as possible about Sair Linux/GNU certification exams.

Nevertheless, to completely prepare yourself for any Sair Linux/GNU exam, you should begin by taking the Self-Assessment included in this book (immediately following this Introduction). This tool will help you evaluate your knowledge base against the requirements for an LCA or LCP under both ideal and real circumstances.

Based on what you learn from that exercise, you might decide to begin your studies with some classroom training, or you might pick up and read one of the many Linux guides available from Sair or third-party vendors. I strongly recommend that you also install and configure at least four versions of Linux, because nothing beats hands-on experience and familiarity when it comes to understanding the questions you're likely to encounter on a certification test. Book learning is essential, but hands-on experience is the best teacher of all.

You can find more information on the benefits associated with Linux Certification at www.linuxcertification.com/reasons.php.

## The Linux Certified Administrator (LCA) Program
Each LCA exam consists of 50 questions. The candidate must receive a score of 74 percent on the exam, which corresponds to 37 correct questions.

The best place to keep tabs on the LCA program and its various certifications is on the Linux Certification Web site. The current URL for this program is www.linuxcertification.com. Details of the LCA program change frequently; make sure to monitor the "News" and the "Exams" links often for the latest and most accurate information about the LCA programs.

## The Linux Certified Professional (LCP) Program
Passing either the Installation and Configuration Level 1 exam 3X0-101 or the System Administration Level 1 exam 3X0-102 also qualifies you as a Linux Certified Professional (LCP). You'll receive a card in the mail along with your certificate once you pass one of these two exams that lists your LCP status, name, and serial number.

## Taking a Certification Exam
Alas, testing is not free. Your exam will cost $99, and is administered by Prometric/ Thomson Learning (formerly known as Sylvan Prometric). To reach the people behind the Sair Linux/GNU exams, email questions@sairinc.com.

You can sign up for a test through Prometric's Web site at www.prometric.com. Or, you can register by phone at 800-755-3926 (within the United States or Canada) or at 410-843-8000 (outside the United States and Canada).

To sign up for a test, you must possess a valid credit card, or contact either company for mailing instructions to send them a check (in the United States). Only when payment is verified, or a check has cleared, can you actually register for a test.

To schedule an exam, call the number or visit either of the Web pages at least one day in advance. To cancel or reschedule an exam, you must call before 7 P.M. pacific standard time the day before the scheduled test time (or you may be charged, even if you don't appear to take the test). When you want to schedule a test, have the following information ready:

- Your name, organization, and mailing address.
- Your Test ID. (Inside the United States, this means your Social Security number; citizens of other nations should call ahead to find out what type of identification number is required to register for a test.)
- The name and number of the exam you wish to take.
- A method of payment. (As we've already mentioned, a credit card is the most convenient method, but alternate means can be arranged in advance, if necessary.)

All exams are completely closed-book. In fact, you will not be permitted to take anything with you into the testing area, but you will be furnished with a blank sheet of paper and a pen or, in some cases, an erasable plastic sheet and an erasable pen. We suggest that you immediately write down on that sheet of paper all the information you've memorized for the test. In Exam Cram books, this information appears on a tear-out sheet inside the front cover of each book. You will have some time to compose yourself, record this information, and take a sample orientation exam before you begin the real thing. We suggest you take the orientation test before taking your first exam, but because they're all more or less identical in layout, behavior, and controls, you probably won't need to do this more than once.

## How to Prepare for an Exam
Preparing for any Linux exam requires that you obtain and study materials designed to provide comprehensive information about the specific exam for which you are preparing. The following list of materials will help you study and prepare:

- Online documentation can be found on the Linux Certification Web site (www.linuxcertification.com).
- The Linux Documentation Project (online resource can be found on www.linuxdoc.org).

In addition, you may find training courses from Sair's Accredited Centers of Education (ACE) useful in your quest for Sair Linux/GNU expertise. Training has been available on a limited basis for free at past Linux World Expo conferences in the San Francisco Bay Area as well as in New York. If you can get to one of these conferences, monitor the www.linuxcertification.com and www.linuxworldexpo.com Web sites for news. You may get lucky. In addition, you may also find the following series useful:

- Study guides—Several publishers—including The Coriolis Group—offer Linux titles. The Coriolis Group series includes the following:
- The Exam Cram series—These books give you information about the material you need to know to pass the tests.
