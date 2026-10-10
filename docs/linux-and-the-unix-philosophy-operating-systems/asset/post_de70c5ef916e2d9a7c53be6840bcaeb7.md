
| Command | Description |
| :--- | :--- |
| tail | Display the last $n$ lines of a file |
| test | Compare two strings for equality |
| tr | Replace selected characters in a file |
| wc | Count the number of lines, words, or characters in a file |

Many of these utilities have other features besides those mentioned in the above list. For example, awk can mix alphabetical and numeric text interchangeably. Test can check the modes of files to learn whether they are writable by the user. Lex provides an interface to the C programming language driven by matching string expressions in the input stream. Sed by itself is powerful enough to replace commands like grep, head, and tail.

The mixed-mode capabilities of these commands tend to blur the line between text and what is traditionally thought of as data. Hence, it is easier to represent in textual form that which was formerly stored in binary files. Unix programmers usually store numerical data in text files because the Unix environment provides a rich set of tools to manipulate those files.

Storing data as text and then manipulating it with a diverse set of small, text-oriented tools makes Unix systems formidable data processors. With tools such as awk, sed, and grep available on virtually all Unix and Linux systems, the ability to select, modify, and move data becomes more accessible to everyone. Even people who aren't programmers find it easy to read and interpret data stored in flat text files.

The developers of Hewlett-Packard's OpenVMS [1] operating system may be right in thinking that most people are afraid of the computer. Instead of shielding users from the system, though, Unix takes them inside it. It leads them through the labyrinthine logic trails, while they hold onto their last vestige of familiarity—namely, their data in a format that can be read and understood. For all the criticism of the "unfriendly Unix user interface," Unix may well be the friendliest system of all. Users can always look at their data without having to be system gurus skilled at interpreting complex binary file formats.

## 4.2.4 Increased portability overcomes the lack of speed

Throughout this discussion, you've probably been thinking, "Yeah, portability is nice, but what about performance?" It's true that using flat text files slows things down a bit. It takes two or three characters to represent the contents of one binary byte. So you're potentially talking about a 3:1 reduction in performance. This sounds significant, but it really isn't at all, except in high-resolution real-time applications or the rare multiterabyte data warehouse application. Even in, say, a huge data warehouse application, however, the user has the ability to absorb and analyze only a minuscule (by human standards, anyway) abstraction of the data. So at some point, the amount of data is reduced to an amount that is insignificant by CPU-cycle standards.

Eventually, every application program is ported to a new system, or else it becomes extinct. The unreleenting progress of computer manufacturers assures us that what may have been prohibitively expensive today will be dirt cheap tomorrow. It doesn't pay to run an application on a slow system that is becoming increasingly costly to maintain.

The payoff in using text comes when you must port your application to a new architecture. If you had enough foresight to make your program portable, then with text it becomes a trivial matter to move your data to a new platform as well. Woe to software engineers who must port both data and program code. The data will be stale by the time it ever sees the new memory boards. The cumulative time lost by a 3:1 performance reduction pales in comparison with the weeks or months lost in moving the data to the new platform.

## 4.2.5 The lack of speed is overcome by next year's machine

We've acknowledged that text files impose a drag on performance. You could possibly realize up to a 3:1 reduction in speed. However, if the application meets today's minimum performance requirements, you can expect that next year's machine will yield a dramatic improvement— if your data can be ported.

As of this writing, next year's machine usually offers enough additional computing power to render any of today's performance concerns about text files superfluous. In other words, if your application barely performs adequately today, its speed will be ample tomorrow. In a few years you may even have to start thinking about how to slow it down so people can use it!

## **Case Study: One Unix Philosopher's Bag Of Tricks**

We have seen that given a choice between high efficiency and high portability, Unix programmers' preference weighs heavily with the latter. As a result, their applications are often among the first to run on new platforms as they become available. This gives their software a definite edge in the marketplace. In a world where windows of opportunity open overnight and slam shut as soon as a month later, pursuing the portability priority can mean the difference between being an industry leader or being one of the others that wish they were.

How did Unix programmers come to embrace such beliefs? Most early software engineers weren't taught the importance of portability in school, at least not with any sense of conviction. More likely, they learned the value of portable code and data the best way: through firsthand experience.

Most Unix "gurus," as they're called, carry a collection of programs and shell scripts that make up their personal tool kit. These tools have followed them as they've moved from machine to machine, job to job, and company to company. For purposes of illustration, let's look at a Unix philosopher's bag of tricks.

My personal collection of tools has varied through the years. Here is a partial sample of those that have stood the tests of time and portability:

| Tool | Description |
| :--- | :--- |
| cal | A shell script front end to the Unix cal program that allows you to specify textual names for months instead of numbers. Borrowed from *The Unix Programming Environment* by Brian Kernighan and Rob Pike. [a] |
| cp | A “fumble finger” front end to the Unix `cp` program that prevents you from unintentionally overwriting an existing file |
| l | Runs the `ls` command with the `-F` switch specified |
| ll | Runs the `ls` command with the `-l` switch specified |
| mv | Similar to the `cp` script, it prevents you from unintentionally overwriting an existing file by renaming another file to a file with the same name. |
| vit | Invokes the `vi` editor with the `-t` flag for use with tags and tag files. Tags make it easy to locate subroutines in a collection of files. |

I have converted some scripts into aliases for use with the C shell, an interactive command interpreter originally found on Berkeley Unix systems. Aliases allow you to specify alternative forms of heavily used commands without having to resort to putting everything into shell scripts. Like shell scripts, they, too, are portable.

I originally built these tools under Unix Version 7 on a Digital PDP-11/70 at a small company engaged in the manufacture of newspaper composition systems. As the company added new systems for software development, I moved them to PDP-11/34, PDP-11/44, and LSI-11/23 systems also running Unix. This doesn't sound like a grand feat, given the renowned compatibility of the PDP-11 line, but wait. It gets better.

Eventually, I left the company in pursuit of other career opportunities, taking my tools with me on a nine-track tape. The C programs and shell scripts had soon found a home on a Digital VAX-11/750. The VAX-11/750 had more horsepower than the smaller PDP-11s I'd been using. Consequently, they ran a bit faster at the new company. The tools picked up even more speed when the company replaced the VAX-11/750 with a VAX-11/780. All this happened without modifications to the tools whatsover.

About that time, workstations—those wondrous you-mean-I-can-have-the-whole-darn-computer-to-myself boxes—vaulted onto the scene. Everyone flocked to buy the hot new machines from Sun Microsystems, my employer included. So the tools that had been moved from the PDP-11 to the VAX line suddenly found themselves running without modifications on Sun workstations.

Having spent the greater part of my software engineering career in New England, I found the latest equipment from the original digital equipment maker to be fairly common within a hundred miles of Boston. Again, I ported my old reliable C programs and shell scripts to the Digital line, this time to the VAX 8600 series and later to the VAX 8800 series. Again, the tools ran without modification.

Necessity is the mother of midnight invention. A software engineer I was working with had noticed a large cache of Digital Professional 350s collecting dust in a warehouse. An enterprising individual concluded that these 350s would make fine personal computers for us at home, especially if they were running Unix. So he proceeded to port a version of Unix
