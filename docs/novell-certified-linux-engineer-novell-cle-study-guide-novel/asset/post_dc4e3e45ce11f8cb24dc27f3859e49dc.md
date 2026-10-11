
# We Want to Hear from You

As the reader of this book, *you* are our most important critic and commentator. We value your opinion and want to know what we're doing right, what we could do better, what areas you'd like to see us publish in, and any other words of wisdom you're willing to pass our way.

You can email or write me directly to let me know what you did or didn't like about this book—as well as what we can do to make our books better.

> Please note that I cannot help you with technical problems related to the topic of this book and that due to the high volume of mail I receive, I may not be able to reply to every message.

When you write, please be sure to include this book's title and author as well as your name and email address, or phone number. I will carefully review your comments and share them with the author and editors who worked on the book.

Email: feedback@novellpress.com
Mail: Mark Taber
Associate Publisher
Novell Press/Pearson Education
800 East 96th Street
Indianapolis, IN 46240 USA

# Introduction

**W**elcome to the world of Novell Enterprise Linux Services! As you will see in later chapters of this book, Novell has yet again revolutionized the Information Technology industry by migrating its world-famous network services from the traditional NetWare platform to the up-and-coming Linux operating system.

By giving organizations the opportunity to provide Novell’s productivity-enhancing services on a very inexpensive yet highly stable operating system, Novell has raised a standard that other vendors will be hard-pressed to match. In accordance, Novell Training Services has rolled out a certification program for NNLS: the Certified Linux Engineer (CLE).

Due to the complexity of the CLE certification, Novell wants to make sure candidates really know their stuff with NNLS. To do this, Novell has implemented a practical test for the certification. To pass, you must be able to walk the walk, not just talk the talk.

By gaining your CLE certification, you tell the world that you can actually manage an NNLS deployment, not just answer a bunch of questions about the product in a multiple-choice exam. This gives you a strong competitive edge in a tight job market.

However, this hands-on approach to testing means the CLE exam is much more difficult than most other certification exams you may have taken. The CLE practical exam has a higher failure rate than most written IT certification exams. To pass, you must thoroughly prepare yourself.

That’s where this book comes in! By reading this book, completing the lab exercises, and working through the practice scenario at the end, you will be much better prepared than your average CLE candidate.

In Chapter 1, “Introduction to the CLE Practical Exam,” I introduce you to the NNLS product and the CLE certification program. I also provide you with some important exam tips and strategies that will increase your chances of passing.

In Chapter 2, “Introduction to SUSE Linux,” you will learn some basic Linux skills that you will need to know in order to deploy and manage an NNLS implementation. You will also learn how to install a Linux server in preparation for deploying NNLS.

In Chapter 3, “Linux Administration and Configuration,” you will learn some intermediate-level Linux skills that will also be required to manage NNLS.

In Chapter 4, “Introduction to Novell Enterprise Linux Services (NNLS),” you will be introduced in depth to the NNLS product, including its component parts, features, and benefits. In Chapter 5, “NNLS Installation and Administration,” you will get your hands dirty by installing NNLS on your Linux server. You will also learn how to implement and manage your server's eDirectory tree. You further learn how to keep your NNLS implementation up to date using the Red Carpet daemon.

In Chapter 6, “Managing User Accounts with eGuide and Linux User Management,” you will learn how to provide a company address book portal using eDirectory and eGuide. You will also learn how to redirect Linux user authentication to your eDirectory tree using the Linux User Management component of NNLS.

In Chapter 7, “Synchronizing User Identities with DirXML,” you learn the basics about one of the most powerful and complex components of NNLS: DirXML. You will learn how to configure a basic delimited-text driver and a more advanced eDirectory driver.

In Chapter 8, “Implementing File Services with iFolder, Samba, and NetStorage,” you learn how to increase file accessibility while protecting data integrity using iFolder. You also learn how to implement Samba shares using eDirectory authentication as well as how to provide users with web-based access to the server file system with NetStorage.

In Chapter 9, “Implementing Print Services with iPrint,” you learn how to deploy a location-based, automated printing system using iPrint. In Chapter 10, “Implementing Email Services with NetMail,” you learn how to deploy a web-based, modular email server: NetMail.

In Chapter 11, “Tying It All Together with Virtual Office,” you learn how to tie all the various NNLS components together into a unified, web-based interface using Virtual Office. Finally, in Chapter 12, “CLE Practice Scenario,” you will be presented with an NNLS deployment scenario for a hypothetical company to give you an opportunity to practice for your CLE practical exam.

As you progress through this book, my goal is to provide you with a quality learning experience. I hope you find this book well written and easy to understand. I also hope you find it to be adequate preparation for your CLE exam. However, no text is perfect. If you have suggestions for improvement, features you would like to see added, or corrections you feel need to be made, please feel free to email me at support@nebo-tech.com.

Best of luck to you in your CLE certification pursuits!

# CHAPTER 1
# Introduction to the CLE Practical Exam

Congratulations on your choice to become a Certified Linux Engineer! By purchasing this book, you are on your way to earning one of the hottest new certifications around.

By gaining your CLE certification, you prove to your employer and your co-workers that you truly know your stuff with Novell services on Linux. That’s because Novell’s practical testing strategies ensure that anyone certified as a CLE really can do the job. No paper certifications allowed here! We’ll go into more depth on the CLE in just a moment. For now, let’s take a look at what will be covered in this book.

This chapter provides an overview of Novell’s newest certification program—the Novell Certified Linux Engineer (CLE). The following topics will be covered:

- Introduction to the CLE
- Introduction to the CLE Test Environment
- CLE Test-taking Strategies

# Introduction to the CLE

For years, Novell certifications have represented the pinnacle of Information Technology industry training. Novell pioneered the certification industry with the Certified Novell Engineer (CNE) and Certified Novell Administrator (CNA) programs.

Novell continues this venerable tradition with the Certified Linux Engineer program. Why a whole new certification? The nature of the product CLE certifies you on is dramatically different from prior Novell products. Let’s take a look at the nature of the product you must know in order to become a CLE: Novell Enterprise Linux Services.

# Novell Enterprise Linux Services

In 2003, Novell fused together two very powerful worlds. In one world, there is Linux, one of the most robust, stable, and affordable network operating systems available today. These factors contribute to the popularity of Linux.

Each year Linux is finding its way into more and more organizations. According to IDC, an IT industry organization, “Linux servers have demonstrated six consecutive quarters of year-on-year revenue growth, proving that they are not a flash-in-the-pan technology” (Source: IDC Worldwide Quarterly Server Tracker, November 2003)

Residing in the other world are Novell’s time-proven network services. Historically, these services were provided only on Novell’s high-end NetWare server operating system. Although Novell did eventually port some of these services to the Windows Server platform, very few were made available on Linux.

In 2003, Novell changed all that with the introduction of Novell Enterprise Linux Services (NNLS). In this product, Novell ported its famous services such as iPrint, iFolder, NetStorage, Virtual Office, and DirXML to run on the Linux platform. For the first time, these time-tested services are available on an operating system other than NetWare.

The benefits of this fusion are noteworthy for several reasons. System administrators can implement a reliable, inexpensive, and fully supported open-source network operating system. Embracing Linux allows them to dramatically lower the all-important total cost of ownership (TCO) of the system.

Using eDirectory, administrators can configure the NNLS implementation as a standalone system or integrate it into an existing Novell eDirectory environment. eDirectory also provides administrators with a broad range of user identify management tools and options, depending on which networking platforms are present.
