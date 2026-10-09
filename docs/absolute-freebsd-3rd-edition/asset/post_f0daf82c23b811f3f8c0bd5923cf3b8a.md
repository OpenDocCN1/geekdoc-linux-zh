
That being said, you’re not entirely on your own. The FreeBSD community includes numerous developers, contributors, and users who care very deeply about FreeBSD’s quality, and they’re happy to work with users who are willing to do their share of the labor. FreeBSD provides everything you need: complete access to the source code used to create the system, the tools needed to turn that source code into programs, and the same debuggers used by the developers. Nothing is hidden; you can see the innards, warts and all. You can view FreeBSD’s development history since the beginning, including every change ever made and the reason for it. These tools might be beyond your abilities, but that’s not the Project’s problem. Various community members are even happy to provide guidance as you develop your own skills so you can use those tools yourself. You’ll have lots of help fulfilling your responsibilities.

As a grossly overgeneralized rule, people help those like themselves. If you want to use FreeBSD, you must make the jump from eating what the vendor gives you to learning to cook. Every member of the FreeBSD user community learned how to use it, and they welcome interested new users with open arms. If you just want to know what to type without really understanding what’s going on behind the scenes, you’ll be better off reading the documentation; the general FreeBSD support community simply isn’t motivated to help those who won’t help themselves or who can’t follow instructions.

If you want to use FreeBSD but have neither the time nor the inclination to learn more, invest in a commercial support contract. It might not be able to put you in touch with FreeBSD’s owner, but at least you’ll have someone to yell at. You’ll find several commercial support providers listed on the FreeBSD website.

It’s also important to remember that the FreeBSD Project maintains only FreeBSD. If you’re having trouble with some other piece of software, a FreeBSD mailing list is not the place to ask for help. FreeBSD developers are generally proficient in a variety of software, but that doesn’t mean they want to help you, say, configure KDE.

The first part of your homework, then, is to learn about the resources available beyond this book. These include the integrated manual, the FreeBSD website, the mailing list archives, and other websites.

### Man Pages

*Man pages* (short for *manual pages*) are the primordial way of presenting Unix documentation. While man pages have a reputation for being obtuse, difficult, or even incomprehensible, they’re actually quite friendly—for particular users. When man pages were first created, the average system administrator was a C programmer and, as a result, the pages were written by programmers, for programmers. If you can think like a programmer, man pages are perfect for you. I’ve tried.

### Manual Sections

The FreeBSD manual is divided into nine sections. Roughly speaking, the sections are:

1. General user commands
2. System calls and error numbers
3. C programming libraries
4. Devices and device drivers
5. File formats
6. Game instructions
7. Miscellaneous information
8. System maintenance commands
9. Kernel interfaces

Each man page starts with the name of the command it documents followed by its section number in parentheses, like this: `reboot(8)`. When you see something in this format in other documents, it’s telling you to read that man page in that section of the manual. Almost every topic has a man page. For example, to see the man page for the editor `vi`, type this command:

```bash
$ man vi
```

In response, you should see the following:

```text
VI(1)         FreeBSD General Commands Manual        VI(1)

NAME
       ex, vi, view - text editors

SYNOPSIS
       ex [-FRrSsv] [-c cmd] [-t tag] [-w size] [file ...]
       vi  [-eFRrS] [-c cmd] [-t tag] [-w size] [file ...]
       view [-eFRS] [-c cmd] [-t tag] [-w size] [file ...]

DESCRIPTION
       vi is a screen-oriented text editor. ex is a line-oriented text
       editor. ex and vi are different interfaces to the same program,
       and it is possible to switch back and forth during an edit session.
       view is the equivalent of using the -R (read-only) option of vi.
       :
```

The page starts with the title of the man page (`vi`) and the section number (1), and then it gives the name of the page. This particular page has three names: `ex`, `vi`, and `view`. Typing `man ex` or `man view` would take you to this same page.

### Navigating Man Pages

Once you’re in a man page, pressing the spacebar or the `PGDN` key takes you forward one full screen. If you don’t want to go that far, pressing `ENTER` or the down arrow scrolls down one line. Typing `b` or pressing the `PGUP` key takes you back one screen. To search within a man page, type `/` followed by the word you're searching for. You'll jump down to the first appearance of the word, which will be highlighted. Typing `n` subsequently takes you to the next occurrence of the word.

This assumes that you're using the default BSD pager, `more(1)`. If you're using a different pager, use that pager's syntax. Of course, if you know so much about Unix that you've already set your preferred default pager, you've probably skipped this part of the book.

### Finding Man Pages

New users often say that they'd be happy to read the man pages if they could find the right one. You can perform basic keyword searches on the man pages with `apropos(1)` and `whatis(1)`. To search any man page name or description that includes the word you specify, use `apropos(1)`. To match only whole words, use `whatis(1)`. For example, if you're interested in the `vi` command, you might try the following:

```bash
$ apropos vi
unvis(1) - revert a visual representation of data back to original form
vidcontrol(1) - system console control and configuration utility
vis(1) - display non-printable characters in a visual format
madvise, posix_madvise(2) - give advice about use of memory
posix_fadvise(2) - give advice about use of file data
--snip--
```

This continues for a total of 581 entries, which is probably far more than you want to look at. Most of these have nothing to do with `vi(1)`, however, the letters `vi` just appear in the name or description. Device driver is a fairly common term in the manual, so that's not surprising. On the other hand, `whatis(1)` gives more useful results in this case.

```bash
$ whatis vi
vi, ex, view, nex, nvi, nview(1) - text editors
$
```

We get only one result, clearly with relevance to `vi(1)`. On other searches, `apropos(1)` gives better results than `whatis(1)`. Experiment with both and you'll quickly learn how they fit your style.

The `man -k` command emulates `apropos(1)`, while `man -f` emulates `whatis(1)`.

### Section Numbers and Man

You might find cases where a single command appears in multiple parts of the manual. For example, every man section has an introductory man page that explains the contents of the section. To specify a section to search for a man page, give the number immediately after the `man` command.

```bash
$ man 3 intro
```

This pulls up the introduction to section 3 of the manual. I recommend you read the intro pages to each section of the manual, if only to help you understand the breadth and depth of information available.

### Man Page Contents

Man pages are divided into sections. While the author can put just about any heading he or she likes into a man page, several are standard. See `mdoc(7)` for a partial list of these headings as well as other man page standards:

- *NAME* gives the name(s) of a program or utility. Some programs have multiple names—for example, the `vi(1)` text editor is also available as `ex(1)` and `view(1)`.
- *SYNOPSIS* lists the possible command line options and their arguments, or how a library call is accessed. If I’m already familiar with a program but just can’t remember the option I’m looking for, I find that this header is sufficient to remind me of what I need.
- *DESCRIPTION* contains a brief description of the program, library, or feature. The contents of this section vary widely depending on the topic, as programs, files, and libraries all have very different documentation requirements.
