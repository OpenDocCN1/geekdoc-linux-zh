
argued that program should provide complete context or copy of data and other, taking this notion further, a program strictly following the Unix philosophy would expect to have been given valid source and destination file names at invocation. It would be solely responsible for copying the data. Obviously, if all the program had to do were copy the data, it would be a very small program indeed.

This still leaves us with the question of where the valid source and destination file names come from. The answer is simple: from other small programs. These other programs perform the functions of obtaining a file name, checking whether the file exists, and determining whether it contains more than zero bytes of data.

"Now wait a minute," you may be thinking. Are we saying that Unix contains programs that only check whether a file exists? In a word, yes. The standard Unix distribution comes with hundreds of small commands and utility programs that by themselves do little. Some, such as the test command, perform apparently mundane functions like determining a file’s readability or equivalent. If that doesn’t sound very important, realize that the test command is one of the most heavily used Unix commands.[1]

By themselves, small programs don’t do very much. They often perform one or two functions and little else. Combine them, however, and you begin to experience real power. The whole becomes greater than the sum of the parts. Large, complex tasks can be handled with ease. You can write new applications by simply entering them on the command line.

> [1] Some Unix/Linux shells (command interpreters), such as bash, have made the test command part of the shell itself, eliminating the need to invoke a new process to run the command, thereby reducing overhead. The downside to this is that if you keep adding commands to the shell itself, eventually the shell grows to the point where nonshell commands become costly to execute because of the way Unix/Linux creates new processes. It may be better to rely on the fact that frequently used commands are typically already sitting in the kernel’s buffer cache, so obtaining them from the disk, which would be prohibitively expensive time-wise, would not be necessary.

## 2.2 Software engineering made easy

It has often been said that Unix offers the world's richest environment for programmers. One reason is that tasks that can be difficult, if not impossible, to accomplish on other operating systems are comparatively easy to accomplish under Unix. Could it be that small programs make such tasks easy? Absolutely.

### 2.2.1 Small programs are easy to understand

The "all-business" approach of small programs keeps fluff to a minimum, focusing instead on performing one function well. They contain only a few algorithms, most of which relate directly to the job involved.

Large programs, on the other hand, lean toward complexity and present barriers to understanding. The bigger a program becomes, the more it gets away from its author. The sheer number of code lines becomes overwhelming. For example, the programmer may forget which files the program's subroutines are found in or have trouble cross-referencing variables and remembering their usage. Debugging the code becomes a nightmare task.

Some programs can be difficult to understand, whatever their size, simply because the nature of the function they perform is inherently obscure. Such programs are rare, however. Even programmers with moderate experience readily understand most small programs. This is a distinct advantage small programs have over their larger counterparts.

At this juncture, you may be wondering at what point a small program becomes a large program. The answer is, it depends. Large programs in one environment may be considered average for another. What is spaghetti code to one programmer may be daily pasta to the next. Here are some signs that suggest that your software may be departing from the Unix approach:

- The number of parameters passed to a function call causes the line length on the screen to be exceeded.
- The subroutine code exceeds the length of the screen or a standard piece of 8½/2-by-11 inch paper. Note that smaller fonts and taller windows on a large workstation monitor allow you to comfortably stretch the limit a bit. Just don't get carried away.
- You can no longer remember what a subroutine does without having to read the comments in the code.
- The names of the source files scroll off the screen when you obtain a directory listing.
- You discover that one file has become too unwieldy for defining the program's global variables.
- You're still developing the program, and you cannot remember what condition causes a given error message.
- You find yourself having to print the source code on paper to help you organize it better.

These warning signs are likely to ruffle the feathers of some programmers, namely those in the “big is better” camp. Not every program can be made small, they say. This world is a pretty big place, and there are some pretty big problems out there that we’re trying to solve with some pretty big computers. These problems require that we write some pretty big programs.

That’s a pretty big misconception.

There exists a kind of software engineer who takes pride in writing large programs that are impossible for anyone but himself to comprehend. He considers such work “job security.” You might say that the only thing bigger than his ego is his last application program. Such software engineers are far too common in traditional software engineering environments.

The problem with this approach to job security is that the companies they work for inevitably realize that these engineers will eventually move on, leaving their companies holding the bag. The wiser companies take steps to prevent that. They hire individuals who understand that easily maintained software is more valuable.

No longer can the software designer say, “Heaven help the next guy.” Good designers must go out of their way to make their software easy to maintain. They comment their code thoroughly—but not too thoroughly. They keep subroutines short. They pare the code down to what is absolutely necessary. This usually results in small programs that are easier to maintain.

### 2.2.2 Small programs are easy to maintain

Since a small program is usually easy to understand, it is likely to be easy to maintain as well, for understanding a program is the first step in maintaining it. No doubt you’ve heard this before, but many programmers ignore the subject of maintenance. They figure that if they took the time to write a program, then someone else will be just as willing to take the time to maintain it after them.

Most software engineers are not satisfied with maintaining other peoples’ programs for a living. They believe—perhaps rightfully so—that the real money is made in writing new programs, not fixing past mistakes. Unfortunately, users don’t see it quite the same way. They expect software to work the first time. If it doesn’t, they get very upset with the program’s vendor. Companies that fail to maintain their software do not remain in business for long.

Since maintaining software is not very glamorous work, programmers seek out ways to make the task easier or even avoid it altogether. Most cannot eliminate this duty entirely, however. If they’re lucky, they probably could turn over maintenance chores to a junior individual. But more often than not, software support responsibilities usually fall upon the original author, who must settle for making the task more palatable any way he or she can. Small programs meet this need quite nicely.

### 2.2.3 Small programs consume fewer system resources

Because their executable images occupy very little memory, the operating system finds it much easier to allocate space for them. This greatly reduces the need for swapping and paging, often resulting in significant performance gains. A popular term in the Unix world is "lightweight" (i.e., small programs are often considered lightweight processes).

Large programs, with their huge binary images, extract a heavy price from the operating system when loaded. Paging and swapping commonly occur, causing performance to suffer. Operating system designers, aware of the resource requirements of large programs, attempt to deal with this issue by building enhancements such as dynamic loading and sharable runtime libraries. These address the symptom, not the problem.

A computer hardware engineer I met in the early days of my career often joked, "All programmers ever want is more core! All we need to stop your whining is to give you another memory board." He was partly right, of course. Give a programmer more memory, and the programs will run faster and take less time to write, greatly increasing productivity.

Reflect upon the "more core" cure for a moment. My hardware engineer friend unwittingly based his statements on the tendency of the programmers in his sphere to write large, complex programs. It's not surprising. The operating system we were using for applications development then was not Unix.

Had we been using Unix and embracing its small-program philosophy, the need for more memory would have been less evident. The joke would have been, "All programmers ever want is more MIPS!" (MIPS stands for millions of instructions per second, a popular though not necessarily accurate measure of CPU performance.)

Why has the metric of MIPS become such a hot issue in the computer world today? Because as Unix usage has become more prevalent, the use of small programs has proliferated as well. Small programs, although they usurp little system memory when executing, derive the most benefit from the injection of additional CPU horsepower. Load them into memory, and they do their job quickly, freeing up the memory for use by other small programs. Obviously, if the CPU capacity is lacking, then each program must spend a longer time in memory before the next small program can be loaded to do its job.

Systems employing small programs benefit from additional memory, too. Larger amounts of memory allow more small programs to remain in the kernel buffer cache longer, reducing reliance on secondary storage. Smaller programs can also be laid out in the buffer cache more easily. As we shall see later, the more small programs you can run at once, the higher the overall system performance. This forms the basis of a tenet of the Unix philosophy that we'll be discussing later.

### 2.2.4 Small programs can easily be combined with other tools

Anyone who has ever worked with large, complex programs knows this. Monolithic programs are worlds unto themselves. In trying to provide every feature that anyone could possibly want in a single program, they build barriers that hinder easy interfacing with other applications.
