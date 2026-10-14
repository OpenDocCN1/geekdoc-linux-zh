
# Contents

## 12  User Administration  488
- Creating UNIX User Accounts  490
- Windows 2000 Users and Groups  506
- Windows 2000 User Profiles and Home Folders  518
- Windows 2000 User Environment  522
- UNIX and Windows 2000 Account Integration  527
- Summary  528

## 13  Backups  530
- Backup Methodology  532
- Backup Methods  541
- Summary  565

## 14  Performance Monitoring  568
- Key Components  570
- Unix Performance Tools  573
- Windows 2000 Performance Tools  588
- Summary  599

## 15  Software Administration  602
- Managing UNIX Applications  604
- Distributing Files and Applications  614
- Windows 2000 Software Administration  622
- Summary  625

## 16  Web Servers  630
- Apache Web Server  632
- Internet Information Server 5.0  652
- Summary  659

## Appendix A  661

## Index  667

# INTRODUCTION

A few years ago, while teaching a course in UNIX system administration, a student approached me at the end of the day. He was concerned about implementing backup strategies for the systems he would soon have to manage. I was surprised. The gentleman had been an NT administrator for quite a while, managing a rather large infrastructure. When I took the time to explain how the concepts of backups were the same, only the commands differed, he was greatly relieved. That and many similar experiences over the last several years inspired this book. Our intent is to convey the fundamentals of system administration as an independent skill set, with the specific operating system as the application.

This book is an introduction to the complexity of supporting the user environment in a multi-vendor installation. *UNIX and Windows 2000 Handbook: Planning, Integration & Administration* is designed to assist system administrators of all levels in creating and maintaining a productive environment for their users. This book includes a discussion of the issues, guidelines for solving the related problems, technical examples where applicable, and a more philosophical discussion of the nature of support and the policy issues involved in planning and administering a heterogeneous environment.

Over the years, the separation among UNIX variants, and the resulting advocacy of administrators and programmers has resulted in a lack of commonality within the administrative functions of the systems. The inclusion of Windows NT/2000 and the increased capabilities of the personal computer have further complicated the issue of administration. Applications exist to span this diversity; implementations of DNS, NIS, and NFS are three notable examples.

Throughout this book, we present the tasks of System Administration and how they are implemented in the UNIX and Windows 2000 environments. The intent is to view system administration tasks as independent concepts and the support of a specific operating system as an application of those concepts.

## Who is This Book For

This book is intended for individuals who are competent users of one or more of the operating systems, but not necessarily a system administrator in any. The basic concepts are provided, as well as moderate to advanced discussions on topics related to creating an integrated user environment.

## How this Book is Organized

The book is structured to serve as a tutor as well as a reference. The fundamental issues of installation planning and the role of the system administrator will be thoroughly discussed. The book has been divided into three parts: Planning, Integration, and Administration. As the book progresses, the overlapping nature of these areas will become increasingly evident. We placed individual administration tasks in a particular area based on our perception of the task constraints. For example, upgrades and patches are administrative tasks, but careful planning is required for efficiency and stability. The latter constraint outweighs the former, and we placed the chapter in the Planning part of the book.

# PART 1: PLANNING

The first section of this book relates to the foundational concepts required to begin system administration. In presenting these concepts, we introduce and explain the need for planning carefully. Planning is always good, but it
