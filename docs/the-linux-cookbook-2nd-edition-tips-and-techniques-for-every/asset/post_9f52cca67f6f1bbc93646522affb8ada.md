
of “free” invites careless violation of license terms and conditions by casual users and amateur publishers alike; enforcement is difficult if not impossible; assistance is nonexistent, since the practice occurs outside of traditional publishing; what constitutes the open “source” for different works is heavily debated; and, while the availability of works on the Internet is generally transnational, it is unclear whether international law or the laws of sovereign nations apply to these licensed works and their copies and derivatives.

Computers have made it possible for machine-readable works to be published in such a way so that anyone can access, distribute, sample from or modify copies of these works, free of charge and without harm to the originals—but this has yet been only demonstrated by individual publishers who released their works under unique licenses that specified these permissions and the terms under which they are given; there is yet no acknowledged universal standard or commons for such works, and no clear economic model to replace the old publication methods—so the future of this practice, and of all the works already so published, is unclear.

## 1.7.7 UNIX and the Tools Philosophy

The fact that the UNIX operating system has survived for more than thirty years should tell us something about the temerity of its design considerations. One of these considerations—perhaps its most endearing—is the “tools” philosophy.

A brief discussion of this philosophy will help clarify the role of this book as “cookbook.” I will show you how tools are used to run commands on Linux, and how specifying commands for the system to execute is a kind of language.

Most operating systems are designed with a concept of files, come with a set of utility programs for handling these files, and then leave it to the large *applications* to do the interesting work: a word processor, a spreadsheet, a presentation designer, a Web browser. (When a few of these applications recognize each other’s file formats or share a common interface, the group of applications is called a “suite.”)

Each of these monolithic applications presumably has an “open file” command to read a file from disk and open it in the application; most of them, too, come with commands for searching and replacing text, checking spelling, printing the current document, and so on. The programming code for handling all of these tasks must be included inside each application—taking up extra space both in memory and on disk. This is the anti-UNIX approach.

In the case of proprietary software, all of the actual program source code is kept from the public—so other programmers can’t use, build on, or learn
a task unpredicted by the function of the individual tools. This is the concept of *synergy*, and it forms the basis of the UNIX tools philosophy.¹⁷

Here’s an example, using two tools. The first tool, called `who`, outputs a list of all the users who are currently logged on to the system (see Recipe 2.6.2 [Listing Who Is on the System], page 39). The second tool is called `wc`, which stands for “word count”; it outputs a count of the number of words (or lines or characters) of the input you give it (see Recipe 12.1 [Counting Text], page 293).

By combining these two tools, giving the output of `who` to the `wc` command, you can build a new command to list the number of users currently on the system, as in Figure 1-2.

```
```text
$ who | wc -l  ↵
      4
$
```
```

*Figure 1-2. Listing the number of users on the system.*

The output of `who`, a list of all the users who are on the system right now, is piped—via a “pipeline,” specified by the vertical bar—to the input of `wc`, which through use of the `-l` option outputs the number of *lines* of its input.

In this example, the numeral 4 is output, indicating that four users are currently logged on to the system.¹⁸

Another famous pipeline from the days before spell-check tools goes something like Figure 1-3.

```
```text
$ tr -cs A-Za-z '\012' | tr A-Z a-z | sort -u |
  comm -23 - /usr/dict/words ↵
```
```

*Figure 1-3. An early spelling checker.*

This command (typed all on one long line) uses the `tr`, `sort`, and `comm` tools to make a spelling checker—after you type this command, the lines of text you type (until you interrupt it) are converted to a single-column list of lowercase words with two calls of `tr`, are then sorted in alphabetical order

¹⁷ Because of this approach, and because of its licensing that gives access to all, I like to call Linux a “synergetic” operating system, in honor of the late R. Buckminster Fuller, who invented a new mathematical system based on these same principles.

¹⁸ Piping the output of `who` to `wc` in this fashion is a classic tools example. A.N. Walker called it “the most quoted pipe in the world”—over twenty years ago! See his book in Appendix D [References for Further Interest], page 731.
