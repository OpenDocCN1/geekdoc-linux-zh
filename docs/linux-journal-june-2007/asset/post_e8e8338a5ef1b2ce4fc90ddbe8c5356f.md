
(after cursing loudly at the programming gods). But, it was fun and a challenge. And, it was the “will of the machine” versus the pure logic of 1s and 0s. I was hooked.

During this same period, I switched from being an Electrical Engineer to a major that was both engineering and business, with a minor in what became Computer Science. I studied several different languages: Aigol, Lisp, PL/I, SNOBOL and APL, each one with its own special niche in the computer field.

I remember SNOBOL as a language for string processing, and although I do not remember much of it, I do remember thinking that almost any string of characters input into a SNOBOL compiler would generate some type of syntactically correct program. I remember thinking that the only syntax error that might be generated was the lack of the END statement.

APL, on the other hand, was an array programming language that was very powerful. It even fostered its own special set of symbols that meant you had to paint them on the side of the keys of your regular keyboard, and (in the case of an IBM Selectric typewriter) use a print head specifically made for APL.

In a class on comparative language design, our professor gave us a challenge of re-implementing a 40-line FORTRAN program in as few lines of APL as possible. Most of us reduced the FORTRAN program to three lines of APL, some to two lines of APL. And, one of the brightest students in the class (David Erb) had stayed up the entire night reducing the program to only one line of APL. It was a truly amazing line of code.

After inputting the data to the program and seeing the correct result, the professor (with a gleam in his eye) asked David to explain how the program worked. David, having finished the program only hours before, tried desperately to remember how it actually worked, but he could not explain how he had come to that particular single line, or even how it would produce the desired result.

As a class, we had experienced our first “write-only” language. It was a lesson remembered over the next 38 years—never write a program you could not easily change or re-use.

It was an interesting time in the days before Computer Science degrees. It was more like “Computer Black Magic”, where the computers were owned by the Math Department, the Electrical Engineering Department, the Business school, the Physics Department and so forth. I even had one professor who told me I never would be able to make a living writing software. It has yet to be seen if he was correct.

And, as time went on and computers became more and more important to the world, universities started granting Computer Science, Computer Engineering, Network Engineering and Information Science degrees. And, what we experienced as very painful steps toward understanding these procedures became formalized into what we now call (generally) Computer Science.

I eventually graduated from Drexel University, and in looking for my first job, I was determined that I would not program in a “higher-level language”, such as FORTRAN or COBOL. I wanted to program in assembly language. I turned down many jobs, looking for that chance.

Eventually, that chance came to me: to program in the systems programming group of Aetna Life and Casualty in Basic Assembly Language (BAL) for the IBM 360 series computer—an assembly language and computer system I had never seen before. They asked me if I could program in assembly language. I said, “Sure, just show me the book.”

Fortunately there was a book, *Programming the IBM 360 in BAL*, and after reading it and practicing a few days at Aetna, I started a four-year career of system programming there—a time in my life where I learned many, many things.

The one “language”, if I may call it that, which sustained me over the years, however, was the 1s and 0s of machine code.

It was machine code that allowed me to learn how compilers and interpreters can translate different languages to what the machine can follow. It was machine code that showed me how reentrant and recursive languages worked, and how minute changes in the code of a program could cut many minutes, if not hours or days, off a program’s execution.

It was the study of machine code and machine architecture that allowed me to know how the operating system really worked, and allowed me to understand the protocols of networking. And, it was machine code and looking at the sources of it that let me understand the issues of big-endian versus little-endian and single-precision versus double-precision.

And, it was the knowledge of machine language that allowed me to find places where the compilers had made mistakes in doing the translation of source code to those 1s and 0s. People who knew only higher-level languages could have kept looking at the source code of those high-level languages forever and would not have found the problems.

Nevertheless, other than brief excursions into teaching machine and assembly language courses (the last time was in 1985 when I taught a course in PDP-11 assembly language, another assembly language that I taught myself), I have not actually written in assembly or machine language since I left Aetna in 1977.

The simple reason is that it takes too long to write in those low-level languages, and it is too error-prone.

Compiler optimization techniques have gotten better, CPUs faster, memories cheaper and people’s time more expensive. Don’t get me wrong; there still are plenty of places where assembly language and machine code are used, particularly in places that need absolutely the best performance or the smallest size. But overall, the compilers are doing a pretty good job, and the average person’s mind does not adapt well to the tedious task of writing in assembly.

Yet, when I do sit down and write a bit of code in some modern machine language, I do two things.

- I think about whether there is a language that can do the program better and in a clearer, more human-maintainable way.
- I think about what that language may be generating in machine language and whether changes to the source code or to the algorithm or to the way the data is positioned in memory might affect the speed at which the program runs.

A friend of mine, David Mosberger, once did a study of multiplying two very large arrays. One multiplication was done in the standard linear-algebra “textbook” fashion of analyzing rows and columns. The second multiplication took into account the cache of the CPU and memory, knowing how the 1s and 0s were arranged. The second multiplication took one-fourth of the time on an Alpha processor (which had large cache memories), and one-tenth of the time on an Intel processor (with smaller cache memories).

During the years, I have been exposed to many new languages and many new technologies. I have been able to understand each and every one because I stop to think about what the 1s and 0s are doing. There have been few new computer technologies that have stumped me in the past 38 years.

This is why I object to colleges and universities who feel that high-level languages, such as Java (or Python, or PHP, or you name it) are the only languages worth teaching, and that machine and assembly languages are not worth teaching to students.

In the end, it all comes down to 1s and 0s, and if you do not know what they are doing, and how the machine actually works, you are at the mercy of others.

In a lot of ways, machine code and assembly language are like Latin—perhaps little used, but still useful to know for the serious language enthusiast and programmer.

*Carge dies from the Agape.*

> Jon “maddog” Hall is the Executive Director of Linux International (www.lfi.org), a nonprofit association of end users who wish to support and promote the Linux operating system. Within his career in commercial computing, which started in 1969, Mr Hall has been a programmer, systems designer, systems administrator, product manager, technical marketing manager and educator. He has worked for such companies as Western Electric Corporation, Aetna Life and Casualty, Bell Laboratories, Digital Equipment Corporation, VA Linux Systems and SGI. He is now an independent consultant in Free and Open Source Software (FOSS) Business and Technical issues.
