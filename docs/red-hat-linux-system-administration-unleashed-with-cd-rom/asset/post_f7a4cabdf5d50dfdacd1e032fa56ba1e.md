
The two utilities that allow you to perform job automation under Red Hat Linux were covered in detail; they are the at and cron utilities. You should be able to use either of those utilities to automate jobs, using at for one-time tasks and cron for regular tasks. I believe that you will find both utilities to be very helpful in your system administration duties.

Finally, this chapter looked at debugging cron jobs, a useful skill for any Red Hat Linux system administrator to master. Things can go wrong with cron jobs and because they execute automatically, it can be difficult to isolate problems.

In closing, I hope you have gained some useful knowledge and skills from this chapter and that you can find new and interesting ways of automating your system administration tasks.

## System Tuning and Kernel Building

### PART X

### In This Part
- 34 Tuning Your Linux System 1047
- 35 Customizing the Linux Kernel 1081
- 36 Centennial School District, Portland, Oregon 1135

## Tuning Your Linux System

### In This Chapter
- General Areas of Tuning 1049
- Weighing Costs and Benefits 1052
- Understanding Performance Measurement Techniques 1055
- Understanding Network Performance 1067
- Memory and Swap Space 1068
- Swap Space Priorities 1071
- Swap Partitions Versus Swap Files 1074
- Tunable Parameters in /proc 1075
- Using echo to Alter System Behavior 1078

Linux systems require a great deal of maintenance and care. Performance tuning is the art of making a Linux system operate at its best possible level. This chapter focuses on performance considerations including techniques, costs and benefits, memory, swap space and priorities, swap partitions, and manipulating the /proc filesystem (the interface to the Linux Kernel).

Among the many chores and tasks a systems administrator must perform, tuning is definitely one of the most rewarding (perhaps second to installation activities). Tuning means that the administrator has taken the time and effort to make sure the system operates at a level of acceptable performance. Most often this can be measured by the user's experience. For example, a terminal user who is on the local network expects immediate response from listing files, whereas a programmer expects a certain time to elapse while compiling a project he is working on. Over time, the administrator will develop an affinity for how the system should perform at different time intervals and periods.

All systems, including Linux, require some degree of performance tuning. Perhaps not immediately, but it is rare that a system's tasks do not grow to the point where the system's performance must be examined. As the system's functions become more complex, require more processor time, and put more demand on memory and disk I/O, tuning becomes an important factor in the growth and well-being of the system.

Users are what ultimately matter. Linux provides a strong base to operate from (as do HURD and many commercial versions of UNIX). However, no system will ever operate at the level users expect it to. What users expect and what they receive is very important. Of all people, a systems administrator should expect (and sympathize with) what the user wants. Just because you like Linux does not mean the average user does; you must forget how you perceive the system and see how the users perceive it. Many users outright dislike UNIXish systems. This is where tuning takes its shape, beating what is expected by delivering what is real and giving your system as much power as it can have. This is the essence of performance tuning.

Tuning a system sounds great, but what are some of the aspects of tuning, or perhaps more appropriately, where are the aspects of tuning and what does a systems administrator have to take into account when approaching bottlenecks and other performance issues? Let's take that two-part question and address the first half, general areas of tuning.

## General Areas of Tuning

Problems come in three major areas, two of which (I/O and CPU) are nearly directly related (it is important to note that all three are related in one way or another). The three general areas are

- CPU
- I/O (disk writes and reads)
- Memory (excessive paging—related to disk I/O)

Initially, these seem relatively simple. If it is the CPU, how can better load balancing be achieved? Perhaps with another CPU or faster chipset? If it is excessive paging, the answer may be more memory or a change in how swapping is done. If it is I/O, a change in how disks are arranged and formatted may be required. What if it is a specific user or process that is causing performance issues? How do you ascertain whether an I/O problem is in the disks or swapping? Note the use of perhaps, maybe, and if in this paragraph thus far. That is how performance monitoring is—a great deal of “ifs” until the problem is eventually found and rectified.

## Specific Tuning Aspects and Questions

Well, it gets worse. Along with the aforementioned rudimentary questions you have to take into account when attacking a performance issue, there are a handful of more complex (yet succinctly related) questions that come into play as well.

## What Is a Bottleneck?

Aside from the more obvious portion of a beer bottle, in system’s terms a bottleneck is anything that slows down the system to a point where it is readily apparent (or not so readily apparent).

A readily apparent bottleneck might be something like users saying they listed a directory and it took two minutes to list ten entries.

A not so readily apparent bottleneck (or as I like to call them, “creeping death”) are those that are potential bottlenecks. A case in point might be the gradual increase of use on an ftp server. Although it is still running fast now, after a certain point in time it will become quite apparent that it is too slow.

## Frequency of Bottlenecks

How often does a particular bottleneck occur? This is a very big question that pertains mostly to user inquiries. More often than not, you may discover later that there was no cause for alarm because the user was doing something that was not routine or that was a one-time, isolated incident. Some good examples of this are when a user improperly invokes a command or application, when a user is trying a new way of performing some task, or when a user is trying something completely new. This can happen a great deal in very progressive environments where change is the norm. Such an environment, for example, is one in which new systems and methods are being developed and brought online rapidly. Sometimes, users may not even be aware of them until they start wondering why a job is taking so long.

## Bottleneck Location

Where exactly is the bottleneck occurring? This will be examined later in this chapter in the section “Performance Measurement Techniques,” but it is worth glancing at now. Is the bottleneck staring at you right now? If so, you may want to investigate it as soon as possible. Prolonged, easily identifiable bottlenecks should at least be made known so that users and/or managers might better understand that there is a problem, that you know what it is, and that you will identify a recourse. Sometimes bottlenecks can mask other bottlenecks or are a result of another bottleneck. Figuring which is happening can be puzzling, especially when you consider it can be only one of three general areas. Where this is seen most often is between paging and disk I/O.

## Bottleneck Duration

Is the bottleneck sustained? This is a very important and often overlooked factor about performance—a “take it with a grain of salt” issue. When a user complains that the system is sluggish or perhaps you look at a quick snapshot of the CPU and notice high usage, how long does it really last? Is it long enough to become apparent to other users? A prime example of this might be a user compiling a program. Of course, to the user and even to the system it will appear to be very resource-intensive—but how long does it take to finish and what sort of system-level impact is it having?
