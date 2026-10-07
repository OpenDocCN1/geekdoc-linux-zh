
- Cost Justification ..................................................................................... 281
- Lease or Buy? ........................................................................................ 285
- User Education ....................................................................................... 287
- IBMLink Support ................................................................................ 288
- Ergonomics ................................................................................................ 289
  - Comfort for the Eyes ................................................................. 289
  - Workstation Comfort ................................................................ 290
- What About Noise? ................................................................................ 291
- Security ................................................................................................ 291
  - Loss Prevention ....................................................................... 291
  - Theft Prevention ..................................................................... 292
  - Service ................................................................................................ 292

# Introduction

# What This Book Is

This book is dedicated to IBM eServer pSeries™ servers, the UNIX® systems of the IBM eServer brand, which encompasses the complete range of IBM hardware architectures and operating systems. The IBM eServer pSeries follows in the tradition of IBM RS/6000 systems. For simplicity in this book, we will use “pSeries” to include both pSeries and RS/6000 unless distinctions between the product families are necessary. Currently, only four RS/6000 entry server systems are still available. Although some pSeries and RS/6000 systems can be configured as workstations, UNIX workstations are included in the IBM IntelliStation® family and are not part of the pSeries family.

The flow of this book is follows: First, pSeries and currently available RS/6000 computers will be introduced. The features of these systems, including options and peripherals, will be reviewed in a way understandable to non-computer experts. Following a chapter on application and operating system software, the book covers how to apply pSeries to solve problems, improve productivity, competitive advantages, and so on. Proper selection and use of pSeries products is impossible unless you understand how you can use these components to fill your needs. Specific hardware and software configurations for typical environments will be offered. Many important computer automation issues will also be discussed, such as financial justification, lease versus purchase, facilities considerations, and ergonomics.

# What This Book Is Not

Many computers try to be all things to all people. They start by explaining checkbook balancing and end by covering the space shuttle’s redundant flight computer complex. This book is not a general-view of computers. It is specific to IBM eServer pSeries computers (a subject matter not broad enough for a single book). This book is not a technical reference manual (IBM will sell you that), nor is intended to teach computer programming. It provides a good-understanding of pSeries computers and how to use them in various environments.

This book does not assume you are a computer professional. Although some technical discussions are necessary, these discussions have been kept as light and concise as possible while conveying necessary and useful information.

# How To Use This Book

Chapter 1 first introduces the entire pSeries family and provides an view of each chapter. The latter part of the chapter examines the elements (architecture, graphics, auxiliary storage, etc.) that make up pSeries computers.

Chapter 2 surveys the many hardware options available for pSeries systems, including storage devices, communications adapters, and attached devices such as displays and printers. This information is provided as a reference to inform you about the types of options that are available and to help you select the proper options for your pSeries computer. It should not be used as a comprehensive catalog of features available for any specific model. You should contact IBM or refer to their on-line product information (www.maxpress.com) available to you with this book has links to IBM Web sites for such information.

Chapter 3 discusses operating systems and some basic types of industry-specific application programs. The question of "prewritten" versus "custom" programs is addressed. The chapter continues with discussion of operating systems. First, basic operating system concepts such as "multiuser" and "interactive processing" are defined in nontechnical terms. The AIX 5L™ operating system and its optional extension products are described, and a description of pSeries support for the increasingly popular Linux operating system is given.

Chapter 4 shows how specific pSeries options and software products are used to participate in common computer communications environments.

Chapter 5 covers issues related to the selection of pSeries hardware and software to meet the needs of both commercial and technical users. Hypothetical organizations are described and outfitted with the appropriate pSeries systems. Important topics such as user training, maintenance, security, and facilities planning are discussed.

To help you understand the topics covered in this book, key terms and phrases are defined and given in boldface type when they are first introduced. These key terms are also listed in the index at the back of this book. While reading you you forget the definition of a key term or phrase elsewhere, the index will quickly point you to the page(s) where the term is discussed.

# “Members Only” Web Site

The pSeries world changes every day. That's why there is a companion Web site associated with this book. On the site you will find the latest pSeries news, expanded information, and other pSeries-related resources. However, you have to be a member of the “pSeries Insiders Club” to gain access to this site.

When you purchased this book, you automatically became a member (in fact, that's the only way to join), so you now have privileges of the “pSeries Insiders Club.” To get into the “members only” section of the companion Web site, go to the Maximum Press Web site (www.maxpress.com) and follow the links to the Exploring IBM eServer pSeries companion Web site. When you try to enter, you will be asked for a user ID and password.

- For your user ID, enter: pSeries12e
- For your password, enter: crossover

You will then be granted full access to the “members only” area. Visit the site often and enjoy the updates and resources with our compliments—and thanks again for buying the book. We ask that you not share the user ID and password for this site with anyone else.

# Exploring IBM @server pSeries

# A Glance Backward

To appreciate the pSeries family and the AIX 5L operating system fully, it is helpful to be familiar with some basic history. The AIX 5L operating system is IBM's version of the UNIX operating system, which was originally developed by AT&T Bell Labs in 1969. The original UNIX was not intended to be a commercial product but rather a tool for computer programmers at AT&T. In fact, at that time AT&T was not in the business of selling computers or operating systems. However, in 1975 AT&T began to license universities to use the UNIX operating system at no charge and soon the UNIX operating system became widely used in the academic community. Students quickly took advantage of the freedom in the academic world to make their own improvements to the UNIX operating system, often resulting in new commands that although obvious to the creator seemed cryptic to others. For example, the BFF command used to pick up electronic mail stored in the computer system was added to the UNIX operating system. Why BFF? Because the student who made the enhancement had a dog named BFF who was trained to go out and get the newspaper every morning. In 1981, the University of California at Berkeley offered its version of the UNIX operating system with many enhancements. Berkeley's version of the UNIX operating system, known as Software Distribution 4 (BSD 4), became a very popular operating system in its own right—so that most of the enhancements contained in the Berkeley version were incorporated by AT&T's later versions of the UNIX operating system.

Meanwhile, IBM was busy on the “801 project,” which was started in 1975. Named after the building in which it was resident, the 801 project was an experiment to develop a minicomputer bucked the existing trend toward complex computer programming instructions. Under the leadership of IBM scientist John Cocke, the 801 approach was to simplify the range of instructions used to perform tasks and optimize the computer to execute this limited range of instructions with extreme efficiency. Born of this approach is the name “Reduced Instruction Set Computing,” or RISC.

In January 1986, IBM announced the first product to use the RISC approach, the IBM RT PC (for RISC Technology Personal Computer),
