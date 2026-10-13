
## Introduction

Welcome to *Teach Yourself Unix System Administration in 24 Hours*! This book has been designed so that it's helpful for both beginning system administrators and those with previous Unix experience. This text is helpful as a guide as well as a tutorial. The reader of this book is assumed to be intelligent, and to have at least a basic familiarity with Unix. If you would like to brush up on your Unix prior to delving into this book, I suggest the companion title *Teach Yourself Unix in 24 Hours*, a top-selling introductory title that'll get you up to speed with the intricacies of Unix faster than you can say "supercalifragilisticexpialidocious!" (or type it, for that matter!)

## What This Book Isn't

I'd like to state my intent with this book up front, while you're still browsing in the bookstore: This book is not intended to be the only system administration material you ever study. Indeed, this book grew out of a course I taught, an *introduction* to Unix system administration. The reason for this distinction is because there are a number of very good reference works on administration (that typically run 800–1,100 pages) that offer a cookbook approach of "if this is wrong, do this to fix it." That's very helpful, and I have these titles on my reference shelf, but they don't teach you *how to approach, diagnose, and solve problems the Unix way*. That's a major goal for this book.

When you finish exploring this book, you will know how to think like a good system administrator, regardless of what variation of Unix you encounter. You'll learn how to hypothesize about problems, dig through man pages and configuration files, postulate solutions, then test and verify that they've worked. And have fun in the process too!

In the same vein, this book isn't 1,001 ways to fine-tune your Unix installation. In fact, we're going to gloss over the question of installation, because for most users the system is either already installed (like Mac OS X or Solaris), or has very good installation and configuration documentation. (Red Hat and Mandrake Linux distributions are standouts in this regard.)

## What Flavors of Unix?

This book covers both the System V and BSD Unix worlds—the specific operating systems explored are Red Hat Linux 7.2 (with the 2.4.7 kernel), Solaris 8 (running on Intel, though it's identical to the SPARC version), and Darwin, the BSD OS hidden underneath Mac OS X (release 10.1.2).

Between them, these three represent the major families of Unix, with Red Hat representing the strong but anarchic Linux world; Solaris, the commercial Unix release; and Mac OS X, a direct descendant of the BSD school of Unix.

There are, of course, hundreds of different Unix distributions, ranging from free downloads to operating systems that only run on expensive, million-dollar supercomputers. That's why a major goal of Teach Yourself Unix System Administration in 24 Hours is to teach you how to work within the tools of generic Unix to diagnose and solve problems, rather than how to use vendor-supplied platform-specific tools.

## Does Each Chapter Take an Hour?

You can learn the concepts in each of the 24 chapters in one hour. If you want to experiment with what you learn in each chapter, something I highly recommend, you might take longer than an hour. However, all the concepts presented herein are straightforward. If you are familiar with Windows applications or the Macintosh, you will be able to progress more quickly, and if you're already comfortable at the Unix command line, well, this book might well only be "12-16 hours" worth of studying!

## What If I Take Longer than 24 Hours?

Since the publication of the first edition of my Unix book, I've received a considerable amount of praise and positive feedback, but the one message that's always been a surprise is "I finished your book, but it took me a lot longer than 24 hours." Now you can read here, direct from the author: It's okay! Take your time and make sure you try everything as you go along. Learning and remembering is more important than speed. Remember, too, that 24 hours doesn't necessarily mean 24 consecutive hours. And if you do finish it in 24 hours, let me know!

## How to Use This Book

This book is designed to teach you topics in one-hour sessions. All the books in the Sams Teach Yourself series enable you to start working and become productive as quickly as possible. This book will do that for you.

Each hour, or session, starts with an overview of the topic to inform you what to expect in each lesson. The overview helps you determine the nature of the lesson, and whether the lesson is relevant to your needs.

## Main Section

Each lesson has a main section that discusses the lesson topic in a clear, concise manner by breaking the topic down into logical component parts and explaining each component clearly.

Interspersed in each lesson are special elements, called Notes, Tips, and Cautions, which provide additional information.

![](img/5ced0c78d748bd190e9027e5549a3622_19_0.png)

Notes are designed to clarify the concept that is being discussed. It elaborates on the subject, and if you are comfortable with your understanding of the subject, you can bypass them without danger.

![](img/5ced0c78d748bd190e9027e5549a3622_19_1.png)

Tips inform you of tricks or elements that are easily missed by most computer users. You can skip them, but often Tips show you an easier way to do a task.

![](img/5ced0c78d748bd190e9027e5549a3622_19_2.png)

A Caution deserves at least as much attention as a Tip, because Cautions point out a problematic element of the topic being discussed. Ignoring the information contained in the Caution could have adverse effects on the task at hand. These are the most important special elements in this book.

This book uses different typefaces to differentiate between code and regular English, and also to help you identify important concepts. Therefore, code lines, commands, statements, variables, and any text you see onscreen appear in a computer typeface. Additionally, any text you type as input appears in a bold computer typeface.

## Tasks

This book offers another special element called a Task. These step-by-step exercises are designed to quickly walk you through the most important skills you can learn in different areas of Unix system administration.

## Q&As and Workshops

A Q&A and Workshop section are at the end of each lesson. The Q&A section and Quiz questions reinforce concepts you learned in the lesson and help you apply them in new situations. You can skip this section, but it is advised that you go through the questions to see how the concepts can be applied to other common tasks.

## The Online Component

There are lots of sample code listings, shell scripts, and other types of information throughout this book that you'll want to download from the official book Web site rather than type in:

```
http://www.intuitive.com/tyusa/
```

In addition, there's an errata area and an all-important errata report form on the site too: Any time you find any sort of hiccup or oddness with a command you try, please let us know! We'll keep an up-to-date errata list and make sure they're all fixed in the next edition of the book. Thanks!

![](img/5ced0c78d748bd190e9027e5549a3622_21_0.png)

## PART I

## Installing Unix

Hour

1 Installing Unix 7

![](img/5ced0c78d748bd190e9027e5549a3622_23_0.png)

## Hour 1

## Installing Unix

If you're reading this book, I bet that you already have a Unix operating system installed on a system you run. Whether it's a shared server that you're renting space on for your Web site, a file server in your office, or even a PC that you've used as a Unix test platform, this first hour will possibly be the least interesting one in this book.

However, it's also possible that you've read through some Unix books (perhaps even my own Teach Yourself Unix in 24 Hours), and are eager to learn more about the internals of Unix and how you can ensure that yours is stable.

This first hour, therefore, is going to go through a typical Red Hat Linux installation on a PC, with all the default configuration options specified. Then we'll look at some of the great online Unix and Linux help sites. If you have a different flavor of Unix you're interested in, your installation will doubtless be different (I have experimented with SuSE, Mandrake, Red Hat, Solaris, AIX, HP-UX, Mac OS X, FreeBSD and NetBSD, to name a few). The basic concepts, however, will prove similar in almost all cases.
