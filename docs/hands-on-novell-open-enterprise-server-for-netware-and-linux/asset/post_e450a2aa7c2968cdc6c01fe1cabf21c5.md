
## Chapter features

- **Chapter objectives**—Each chapter begins with a detailed list of the concepts to be mastered. This list gives you a quick reference to the chapter's contents and is a useful study aid.

- **Chapter summary**—Each chapter’s text is followed by a summary of the concepts introduced in that chapter. These summaries are a helpful way to review the material covered in each chapter.

- **Key terms**—All terms introduced with boldfaced text are gathered into the Key Terms list at the end of the chapter. This list gives you an easy way to check your understanding of important terms.

- **Review questions**—The end-of-chapter assessment begins with a set of review questions that reinforce the material introduced in each chapter. Answering these questions ensures that you have mastered the important concepts. The review questions can also be used to help prepare for the CNA exam.

- **Case projects**—These projects are intended to make you think about the chapter concepts and how they can be applied to planning, designing, and troubleshooting network information systems.

- **Hands-on projects**—These projects give you the opportunity to reinforce and apply the chapter's concepts and techniques by building the Business Division for the Universal AeroSpace network on your own. Although each chapter's projects build on previous chapters, they are independent of the hands-on activities, meaning that you don't need to do the projects to complete hands-on activities in subsequent chapters.

- **Novell Open Enterprise Server software**—This book includes two CDs with an evaluation copy of NetWare 6.5 Open Enterprise Server and a bootable DVD with SUSE Linux Enterprise Server 9. For more information on these products and their licensing, refer to the previous section “Novell Software Included with This Book.”

## Text and Graphic Conventions

Additional information and exercises have been added to this book to help you better understand what’s being discussed in the chapter. Icons throughout the text alert you to these additional materials:

- **TIP icon** Tips offer extra information on resources, how to attack problems, and time-saving shortcuts.

- **NOTE icon** Notes present additional helpful material related to the subject being discussed.

- **CAUTION icon** The Caution icon identifies important information about potential mistakes or hazards.

- **ACTIVITY icon** Each Hands-on Activity or Project in this book is preceded by the hands-on icon.

- **CASE PROJECTS icon** Case project icons mark the end-of-chapter Universal AeroSpace projects, which are scenario-based assignments that ask you to independently apply what you have learned in the chapter.

- **EXAMPLE icon** The Example icon points out step-by-step instructions for procedures that aren't covered in hands-on activities but are common tasks that network administrators perform.

## INSTRUCTOR'S MATERIALS

The following supplemental materials are available when this book is used in a classroom setting. All supplements are provided to the instructor on a single CD. You can also retrieve these supplemental materials from the Course Technology Web site, www.cengage.com, by going to the page for this book under “Download Instructor Files & Teaching Tools.”

**Electronic Instructor’s Manual.** The Instructor’s Manual that accompanies this book includes:

- Additional instructional material to assist in class preparation, including suggestions for classroom activities, discussion topics, and additional projects.

- Solutions to all hands-on activities and end-of-chapter materials, including the review questions and case projects.

**ExamView®.** This book is accompanied by ExamView, a powerful testing software package that instructors can use to create and administer printed, computer (LAN-based), and Internet exams. ExamView includes hundreds of questions that correspond to the topics covered in this text, enabling students to generate detailed study guides with page references for further review. The computer-based and Internet testing components allow students to take exams at their computers, and they save instructors time by grading each exam automatically.

**PowerPoint presentations.** This book comes with Microsoft PowerPoint slides for each chapter. These slides are included as a teaching aid for classroom presentation, to make available to students on the network for chapter review, or to be printed for classroom distribution. Instructors, please feel free to add your own slides for additional topics you introduce to the class.

**Figure files.** All figures and tables in the book are reproduced on the Instructor’s Resource CD in bitmap format. Similar to the PowerPoint presentations, they are included as a teaching aid for classroom presentation, to make available to students for review, or to be printed for classroom distribution.

## LAB REQUIREMENTS

To do the case projects and set up your own version of the Universal AeroSpace network, you will be using your own dedicated NetWare server or be assigned to a NetWare classroom server and given a student reference number (an Admin user name preceded by your student number) and a data volume identified with your student number. If you’re using a shared classroom server, your user account will have the necessary privileges to build your own network system by creating and managing network objects, such as users, groups, printers, and files, without affecting other students’ use of the server. Your assigned data volume is the work area on the classroom server where you have been given all rights to create and manage files and directories so that you can complete the projects and activities. If you’re doing the activities and projects on your own dedicated server, you need to use VMware as described in Appendix C or must have one computer designated as the NetWare server and a second computer to use as a client. You can also use VMware to run the NetWare or Linux server with the client on your desktop. For more information on VMware, see Appendix C and visit www.vmware.com.

### Minimum Lab Requirements

**Hardware:**

- With a shared classroom server, each student system requires at least 256 MB RAM, an Intel Pentium or compatible processor running at 300 MHz or higher, and a minimum of 5 GB free space on the hard disk. The system needs to be able to dual-boot between Windows XP and SUSE Linux Enterprise Server 9. A CD-ROM drive is also important for loading software and performing certain activities.

- If you're using VMware to host dedicated server and client systems, each student system needs 1 GB RAM, a Pentium III processor running at 1.5 GHz minimum, and 10 GB free space on the hard drive.

- To set up a shared classroom server for NetWare 6.5, you need a classroom server with at least 1 GB RAM, an Intel Pentium III or higher processor running at 700 MHz or higher (Intel Pentium 4 1.2 GHz recommended), a minimum 8 GB hard drive (6 GB for the SYS volume and at least 500 MB for each student), a CD-ROM drive, a SuperVGA or higher resolution display adapter and monitor, and a mouse.

**Software:**

- Windows XP Professional on each student system

- A copy of the Novell Open Enterprise Server DVD and CDs, which include both NetWare 6.5 and SUSE Linux Enterprise Server 9

In addition to the Novell software included with the book's CDs and DVD, additional software available as free downloads is recommended. Although the following software isn't required to complete the chapter activities, it will help enhance your learning experience:

- **SUSE Linux 10**—Appendix B includes information on installing and using Novell SUSE Linux 10 as a client system. You might want to use that appendix to perform a SUSE Linux 10 installation before Chapter 3. You can then use your SUSE Linux 10 system to perform many of the chapter activities. You can download a free copy of SUSE Linux 10 from www.novell.com/products/suse/download/suse-linux/index.html.

- **VMware Workstation**—VMware Workstation allows you to create and run other operating systems, such as Novell NetWare and SUSE Linux Enterprise Server 9, as applications on your Windows XP desktop. Appendix C provides information on installing and running VMware Workstation. You can download a 30-day evaluation of VMware Workstation at www.vmware.com and use it to create virtual machines for your NetWare and Linux servers.

- **VMware Player**—Although you can't use this product to create new virtual machines or install a new operating system, Appendix C describes how you can use it to run virtual machines created by VMware Workstation. You can download a free copy of VMware Player from www.vmware.com.

## ACKNOWLEDGEMENTS

Although I have spent many hours rewriting this book for the Novell Open Enterprise Server product, it would never have been completed without the help of Course Technology management and staff, especially Amy Leav, who directed and managed the project, and Will Pittkin, for his vision for the book and his persistence in working with Novell to obtain the latest information. I want to express my many thanks to my excellent editor, Lisa Lord, whose patient help and hard work, along with her mastery of technical jargon (also known as GeekSpeak) and the English language, brought life to the words in these chapters. Credit for eliminating technical problems with the hands-on activities goes to Christian Kunkel, Danielle Shaw, and Scott Pollard, who did an excellent job of checking each step and offering suggestions and alternative solutions. No book can be completed without all the work required to get it ready for printing. I feel fortunate to have had such an excellent production editor as Delphine Barros to make sure this book was ready for publication. I take my hat off to the excellent reviewers—David Brown of Gibbs College-Lymington and COMPDACS, John Crowley of Bucks County Community College, Nina Hahberger of Madison Area Technical College, and Brett Nichols of Vatterott College—for their countless hard work in ensuring that the contents and activities would meet the practical demands of teaching NetWare concepts in the classroom environment. My thanks also to my excellent technical editor, David Manfrey from Danwoods College of Technology, who contributed so much to the technical content and
