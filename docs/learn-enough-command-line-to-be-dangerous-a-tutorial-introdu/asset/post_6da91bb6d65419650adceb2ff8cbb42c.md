
![](img/4dec9c51e73c9027d3d8a4fab4408fe6_0_0.png)

# Learn Enough™ Command Line to Be Dangerous

TUTORIAL BY MICHAEL HARTL

## Contents

1. Basics . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
   1.1 Running a terminal . . . . . . . . . . . . . . . . . . . . . . . . . 7
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 10
   1.2 Our first command . . . . . . . . . . . . . . . . . . . . . . . . 10
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 14
   1.3 Man pages . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 14
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 18
   1.4 Editing the line . . . . . . . . . . . . . . . . . . . . . . . . . . 20
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 22
   1.5 Cleaning up . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 22
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 23
   1.6 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 23
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 23

2. **Manipulating files** . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 24
   2.1 Redirecting and appending . . . . . . . . . . . . . . . . . . . . . 26
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 29
   2.2 Listing . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 29
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 34
   2.3 Renaming, copying, deleting . . . . . . . . . . . . . . . . . . . 35
      Unix terseness . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 38
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 39
   2.4 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 39
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 39

3. **Inspecting files** . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 41
   3.1 Downloading a file . . . . . . . . . . . . . . . . . . . . . . . . . . . 41
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 44
   3.2 Making heads and tails of it . . . . . . . . . . . . . . . . . . . . 44
      Wordcount and pipes . . . . . . . . . . . . . . . . . . . . . . . . . . . . 45
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 47
   3.3 Less is more . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 47
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 51
   3.4 Grepping . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 52
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 56
   3.5 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 57
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 57

4. **Directories** . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 58
   4.1 Structure . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 58
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 61
   4.2 Making directories . . . . . . . . . . . . . . . . . . . . . . . . . . 63
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
   4.3 Navigating directories . . . . . . . . . . . . . . . . . . . . . . . . 65
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 69
   4.4 Renaming, copying, and deleting directories . . . . . . . . 69
      Grep redux . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 71
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 73
   4.5 Summary . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 73
      Exercises . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 74

5. **Conclusion** . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75

*Learn Enough™ Command Line to Be Dangerous* is an introduction to the command line for complete beginners, the first in a series of tutorials designed to teach the common foundations of “computer magic” (Box 1). It is aimed both at those who work with software developers and those who aspire to become developers themselves. *Learn Enough™ Command Line to Be Dangerous* assumes no prerequisites other than general computer knowledge (how to launch an application, how to use a web browser, etc.), which among other things means that it doesn't assume you know how to use a text editor, or even what a text editor is. Indeed, this tutorial doesn't even assume you know what a command line is, so if you're confused by the title, you're still in the right place. Finally, even if you already have some familiarity with the command line, you might enjoy following this tutorial (and doing the exercises) to brush up on the basics.

### Box 1. The magic of computer programming

Computer programming may be as close as we get to *magic* in the real world: we type incantations into a machine, and—if the incantations are right—the machine does our bidding. To perform such magic, computer witches and wizards rely not only on words, but also on wands, potions, and an ancient tome or two. Taken together, these tricks of the trade are known as *software development*: computer programming, plus tools like *command lines, text editors,* and *version control.* Knowledge of these tools is perhaps the main line between “technical” and “non-technical” people (or, to put it in magical terms, between wizards or witches and *Muggles*). The present tutorial represents the first step needed to cross this line and *learn enough* software development to be *dangerous*—to be able to cast computer spells, and get the machine to do our bidding.

My name is *Michael Hartl*, and I am perhaps best known as the creator of the Ruby on Rails Tutorial, *a book* and *screencast series* that together constitute one of the leading introductions to web development. (You may also know me, in my more mathematical mode, as the founder of *Tau Day* and author of *The Tau Manifesto.*) One of the most frequently asked questions about the Rails Tutorial is, "Is the Rails Tutorial good for complete beginners?" The answer is, "Not really."

> While it is possible for complete beginners to learn web development with the Ruby on Rails Tutorial (and an impressively large number have), it can be challenging and occasionally frustrating, and I don’t generally recommend it. Instead, I recommend starting here.

Many programming tutorials either gloss over the command line or assume you already know it. But understanding the basics of the command line is absolutely essential to becoming a skilled developer.<sup>1</sup> Indeed, if you look at the desktop of an experienced computer programmer, even on a system with a polished graphical user interface like Macintosh OS X, you are likely to find a large number of “terminal windows”, each containing a series of commands at a command line (Figure 1). Proficiency at the command line is also useful for anyone who needs to work with developers, such as product managers, project managers, and designers.<sup>2</sup> Making this valuable skill accessible to as broad an audience as possible is the goal of Learn Enough™ Command Line to Be Dangerous.

## 1 Basics

As author Neal Stephenson famously put it, “In the Beginning was the Command Line.” Although a graphical user interface (GUI) can dramatically simplify computer use, in many contexts the most powerful and flexible way to interact with a computer is through a command-line interface (CLI). In such an interface, the user types commands that tell the computer to perform desired tasks. These commands can then be combined in various ways to achieve a variety of outcomes. An example of a typical command-line command appears in Figure 2.

This tutorial covers the basics of the Unix command line, where Unix refers to a family of operating systems that includes Linux, Android, iOS, and Mac OS. <sup>3</sup> Unix systems serve most of the software on the World Wide Web, run most mobile and tablet devices, and power many of the world’s desktop computers as well. As a result of Unix’s central role in modern computing, this tutorial covers the Unix way of developing software. The main exception to Unix’s dominance is Microsoft® Windows™, which is not part of the Unix tradition, but those who mostly develop using native Windows development tools will still benefit from learning the Unix command line. Among other things, at some point such users are likely to need to issue commands on a Unix server (e.g., via the “secure shell” command **ssh**), at which point familiarity with Unix commands becomes essential. As a result, Windows users are strongly encouraged to run a free *Linux virtual machine* (as described in Box 2) in order to get the most out of this tutorial. Another good option is to use a cloud IDE<sup>4</sup> such as [Cloud9](http://www.example.com/cloud9); to go this route, follow the “*Development environment*” section in the [Ruby on Rails Tutorial book](http://www.example.com/ruby-on-rails-tutorial-book).

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_6_0.png)

*Figure 1: Terminal windows on the desktop of an experienced developer.*

```
[projects]$ rm -f foo.txt
```

*Figure 2: A typical command-line command.*

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_7_0.png)

### Box 2. Running a virtual machine

In order to complete this tutorial, Windows users should install a couple of free programs to run a *virtual machine* (a simulation of a computer) that allows Windows to host a version of the Linux operating system. The steps appear as follows:

- 1. Install the right version of VirtualBox for your system (free).
- 2. Download the TutorialPath Virtual Machine (large file).
- 3. Once the download is complete, double-click the resulting “OVA” file and follow the instructions to install the Virtual Machine (VM).
- 4. Double-click the VM itself and log in using the default user’s password, which is “foobar!”.

<sup>1</sup> As discussed in Section 1, this statement applies to the Unix tradition, which is the principal computing tradition behind the Internet and the World Wide Web, and the tradition followed by this tutorial.

<sup>2</sup> Knowing the command line is also essential for system administrators (sysadmins).

<sup>3</sup> In a fairly typical turn of events, the name Unix started as a pun on a rival system called Multics.

<sup>4</sup> An IDE, or integrated development environment, typically integrates several development tools (such as a command line and a text editor) into one application.
