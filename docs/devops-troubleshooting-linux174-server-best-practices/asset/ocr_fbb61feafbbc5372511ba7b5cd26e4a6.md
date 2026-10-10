the inevitable blame to be heaped on them for their “bloated” or “buggy”

code, at which point they will complain about the unstable, underpowered

server; or maybe everyone will redirect the blame at QA for not finding the

problem before it hit production. All the while, the actual problem is not

any closer to being solved.

In a DevOps organization, cooperation between all the teams is stressed,

but when it comes to troubleshooting, often people still fall into their tra-

ditional roles even if there’s no blame game. Why? Well, even if every-

one wants to work together, without the same troubleshooting skills and

techniques, everyone may still be waiting on everyone else to troubleshoot

their part. The goal of this book is to get every member of your DevOps

team on the same page when it comes to Linux troubleshooting. When

everyone has the same Linux troubleshooting skills, the QA team will bet-

ter be able to diagnose problems before they hit production, developers

will be better at tracking down why that latest check-in doubled the load

on the system, and sysadmins can be more confident in their diagnoses, so

when a problem strikes, everyone can pitch in to help.

This book is broken into ten chapters based on some of the most com-

mon problems you’ll face on Linux systems, and the chapters are ordered

so that techniques you learn in some of the earlier chapters (particularly

about how to diagnose high load and how to troubleshoot network prob-

lems) can be helpful as you get further into the book. That said, I realize

you may not read this book cover-to-cover, but instead you will probably

just turn to the chapter that’s relevant to your particular problem. So when

topics in other chapters are helpful, I will point you to them.

+   * **Chapter 1: Troubleshooting Best Practices** Before you learn how to
+   
+   troubleshoot specific problems, it may be best to learn an overall
+   
+   approach to troubleshooting that you can apply to just about any kind
+   
+   of problem, even outside of Linux systems. This chapter talks about
+   
+   general troubleshooting principles that you will use when you try spe-
+   
+   cific troubleshooting steps throughout the rest of the book.

+   * **Chapter 2: Why Is the Server So Slow? Running Out of CPU, RAM, and
+   Disk I/O** This chapter introduces troubleshooting principles
+   
+   that you will apply to one of the most common problems you’ll have