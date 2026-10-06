
## How Is This Book Organized?

This book teaches an audience of various levels of experience to find and fix performance problems. To accomplish this, the chapters are presented so that you can pick and read different parts of the book without reading the entire book straight.

Chapter 1 is devoted to the basic methods of performance problem hunting. It contains a series of non-Linux-specific tips and suggestions that prove useful for tracking down performance issues. These guidelines are general suggestions for performance problem hunting and can be applied to tracking down performance issues on any type of computer system.

Chapters 2 through 8 (the bulk of this book) cover the various tools to measure different performance statistics on a Linux system. These chapters explain what tools measure, how they are invoked, and provide an example of each tool used. Each chapter demonstrates what measures aspects of different subsystems, such as system CPU, user CPU, memory, network I/O, and disk I/O. If a tool measures aspects of more than one subsystem, it is presented in more than one chapter. Each chapter describes multiple tools, but only the appropriate tools for a particular subsystem are presented in a given chapter. The descriptions follow this format:

- 1. Introduction—This section explains what the tool is to measure and how it operates.
- 2. Performance tool options—This section does not rehash the documentation. Instead, it explains which options are relevant to the current topic and what options mean. For example, some performance tool man identify the events that a tool measures but not explain what they mean. This section explains the meaning of the events and how-they are relevant to the current subsystem.
- 3. Example—This section provides one or more examples of the tool used to measure performance statistics. This section shows the tool invoked and any output that it generates.

Chapter 9 lists specific and a series of steps to use when confronted with a slow-performing Linux system. It explains how to use the previously described Linux tools to pinpoint the cause of the performance problem. This chapter is the most useful if you want to start with a behaving Linux system and diagnose the problem without necessarily understanding the details of the tools. Chapters 10 through 12 present case studies in which the methodologies and tools previously described are used together to solve real-world problems. The case studies highlight Linux performance tools used to find different types of performance problems: a CPU-bound application, and an I/O bound application.

Chapter 13 covers the performance tools and the opportunities Linux has for improvement.

This book has two appendices. Appendix A contains a table of the performance tools discussed in this book and includes a URL to the version of each tool. Appendix A also identifies Linux distributions support each particular tool. Finally, Appendix B contains information that explains how to install profile, which is a very powerful hard-to-install tool on a few Linux distributions.

## Acknowledgments

First, I want to thank the good people at Prentice Hall, including Jill Harry, Brenda Mulligan, Gina Kanoose, and Keith Cline.

Second, I want to thank all the people who reviewed the initial book proposal and added valuable technical reviews and suggestions, including Karel Baloun, Joe Brazael, Bill Carr, Jonathan Corbet, Matthew Crosby, Robert Hubert, Paul Lussier, Scott Mann, Brent Strong, and George Vish II. I also want to thank all the people who taught me what I know about performance and let me optimize Linux even though the value of Linux optimization was uncertain at the time, John Henning, Greg Tarsa, Dave Stanley, Greg Gaertner, Bill Carr, and the whole BPE tools group (which supported and encouraged me over Linux).

In addition, I want to thank the good folks of SPEC who took me and taught me how benchmarks, when done well, help the entire industry. I specifically want to thank Kaivalya Dixit, whose passion and integrity for benchmarking will be sorely missed.

Thanks also to all the people who helped me my sanity with many games of Carcassonne and Settlers of Catan, including Sarah Ezolt, Dave and Yoko Mitzel, Tim and Maureen Chorma, Ionel and Marina Vasilecu, Joe Doucette, and Jim Zawisa.

Finally, I want to thank my family, including Sasha and Mischief, who remind me that we always have time for a walk or to chase dental floss; Ron and Joni Elias, who cheer me on; Russell, Carol, and Tracy Ezolt, who give their support and encouragement as I worked on this; and to my wife, Sarah, who is the most understanding and supportive person you can imagine.

## About the Author

PHIL EZOLT discovered Linux more than nine years ago when pursuing an undergraduate electrical and computer engineering degree from Carnegie Mellon. For six years, Phil ported and designed Linux performance tools for Compaq's Alpha performance group and represented Compaq in the SPEC CPU subcommittee. During that time, he improved Linux performance on the industry standard SPEC Web and CPU benchmarks using the performance tools he ported and developed. Phil is currently part of a Hewlett-Packard team developing Sepia, a visualization technology that uses Linux XC clusters, OpenGL, and off-the-shelf graphics cards to parallelize real-time high-end visualizations. He is also currently pursuing a master's degree in computer science from Harvard University and is a big fan of German-style board games.

## Chapter 1. Performance Hunting Tips

Solving problems without foresight and planning is painful. You waste time and constantly frustrated the cause of the problem repeatedly slips through your fingers. By following the right set of procedures, you can transform a frustrating performance hunt into an interesting detective story. Each piece of information leads you closer to the true culprit. People can not always be trusted. The evidence will be your only friend. As you investigate the problem, it will take unusual twists and turns, and the information you discovered in the beginning of the hunt may turn out to be what you figure out the problem in the end. The best part is that you will have a thrill of adrenaline and sense of accomplishment when you finally nab the "bad guy" and fix the problem.

If you have never investigated a performance problem, the first steps can be overwhelming. By following a few obvious and nonobvious tips, you can save time and be well on your way to finding the cause of a performance problem. The goal of this chapter is to provide you with a series of tips and guidelines to help you hunt a performance problem. These tips show you how to avoid some of the common traps when investigating what is wrong with your system or application. Most of these were hard-learned lessons that resulted from wasted time and frustrating dead ends. These tips help you solve your performance problem quickly and efficiently.

After reading this chapter, you should be able to:

- Avoid repeating the work of others.
- Avoid repeating your own work.
- Avoid false leads that result from gathering misleading information.
- Create a useful reference document about your investigation.

Although no performance investigation is flawless (you will almost always say, "If only I would have thought of that first"), these tips help you to avoid some of the common mistakes of a performance investigation.

### 1.1. General Tips

### 1.1.1. Take Copious Notes (Save Everything)

Probably the most important thing that you can do when investigating a performance is to record everything you see. A well-organized set of notes allows you to compare how configurations affect the performance. It would be possible just to rerun the test, but usually testing a configuration is time-consuming.

- Record the hardware/software—This involves recording information about hardware (amount of memory, type of CPU, network, disk) as well as software environment (OS and versions). This information may seem early, but when tracking down a problem, you may significantly change the configuration. Save the output of `cat /proc/pci`, `dmesg`, and `uname -a`.

- Save and organize performance results—This can allow you to review results a long time after you run them. It is more efficient to keep your notes organized and avoid repeating work.

- Write down the commands—As you run performance tools, you will often create complicated and complex commands that measure the areas you are interested in. If you want to rerun a test, or run it on a different application, reproducing these commands can be annoying and hard to do on the first try. It is better to record exactly what you used. You can then reproduce the exact command line for a future test, and when reviewing past results, you can also see exactly what you measured. The Linux command `script` (described in detail in Chapter 8, "Utility Tools: Performance Tool Helpers") or "cut and paste" from a terminal is a good way to do this.

- Record information and URLs—As you investigate a performance problem, it is important to record relevant information you found on the Internet, through e-mail, or through personal interactions. If you find a Web site that seems relevant, cut and paste the text into your notes. (Web sites can disappear.) However, also save the URL, because you might need to review the page later or the page may point to information that becomes important later in an investigation.
