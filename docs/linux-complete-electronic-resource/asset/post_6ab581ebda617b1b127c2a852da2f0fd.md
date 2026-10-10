
system or as swap space. The lowest-numbered partition is often treated specially— as a boot partition where you can put a kernel to be booted.

Each partition is either *swap space* (used to implement virtual memory) or a *file system* used to hold files. Swap-space partitions are treated as a linear sequence of blocks. File systems, on the other hand, need a way to map filenames to sequences of disk blocks. Because files grow, shrink, and change over time, a file's data blocks will not be a linear sequence but may be scattered all over its partition (from wherever the operating system can find a free block when it needs one).

## Filenames and Directories

Within each file system, the mapping from names to blocks is handled through a structure called an *i-node*. There's a pool of these things near the bottom (lowest-numbered blocks) of each file system (the very lowest ones are used for housekeeping and labeling purposes we won't describe here). Each *i-node* describes one file. File data blocks live above the *i-nodes*.

Every *i-node* contains a list of the disk block numbers in the file it describes. (Actually this is a half-truth, only correct for small files, but the rest of the details aren't important here.) Note that the *i-node* does not contain the name of the file.

Names of files live in *directory structures*. A directory structure maps names to *i-node* numbers. This is why, in Unix, a file can have multiple true names (or *hard links*; they're simply multiple directory entries that happen to point to the same *i-node*).

## Mount Points

In the simplest case, your entire Unix file system lives in just one disk partition. While you'll see this arrangement on some small personal Unix systems, it's unusual. It is more typical for it to be spread across several disk partitions, possibly on different physical disks. So, for example, your system may have one small partition where the kernel lives, a slightly larger one where OS utilities live, and a much bigger one where user home directories live.

The only partition you'll have access to immediately after system boot is your *root partition*, which is (almost always) the one you booted from. It holds the root directory of the file system, the top node from which everything else hangs.

The other partitions in the system have to be attached to this root in order for your entire, multiple-partition file system to be accessible. About midway through the boot process, your Unix will make these non-root partitions accessible. It will mount each one onto a directory on the root partition.

For example, if you have a Unix directory called /usr, it is probably a mount point to a partition that contains many programs installed with your Unix but not required during initial boot.

## How a File Gets Looked Up

Now we can look at a file system from the top down. When you open a file (such as, say, /home/esr/WWW/1dp/fundamentals.sgml) here is what happens.

Your kernel starts at the root of your Unix file system (in the root partition). It looks for a directory there called home. Usually home is a mount point to a large user partition elsewhere, so it will go there. In the top-level directory structure of that user partition, it will look for an entry called esr and extract an i-node number. It will go to that i-node, notice it is a directory structure, and look up WWW. Extracting that i-node, it will go to the corresponding subdirectory and look up 1dp. That will take it to yet another directory i-node. Opening that one, it will find an i-node number for fundamentals.sgml. That i-node is not a directory, but instead holds the list of disk blocks associated with the file.

## How Things Can Go Wrong

Earlier I hinted that file systems can be fragile things. Now you know that to get to a file you have to hopscotch through what may be an arbitrarily long chain of directory and i-node references. Now suppose your hard disk develops a bad spot?

If you're lucky, it will only trash some file data. If you're unlucky, it could corrupt a directory structure or i-node number and leave an entire subtree of your system hanging in limbo—or, worse, result in a corrupted structure that points multiple ways to the same disk block or i-node. Such corruption can be spread by normal file operations, trashing data that was not in the original bad spot.

Fortunately, as disk hardware has become more reliable, this kind of contingency has become quite uncommon. Still, it means that your Unix will want to integrity-check the file system periodically to make sure nothing is amiss. Modern kinds of Unix do a fast integrity check on each partition at boot time, just before mounting it. Every few reboots they’ll do a much more thorough check that takes a few minutes longer.

If all of this makes Unix sound terribly complex and failure-prone, it may be reassuring to know that these boot-time checks typically catch and correct normal problems before they become really disastrous. Other operating systems don’t have these facilities, which speeds up booting but can leave you with more problems when attempting to recover by hand (and that’s assuming you have a copy of Norton Utilities or similar software in the first place).

## How Do Computer Languages Work?

Earlier, we discussed how programs are run. Every program ultimately has to execute as a stream of bytes that are instructions in your computer’s machine language. But human beings don’t deal with machine language very well; doing so has become a rare, black art, even among hackers.

Nowadays almost all Unix code, except a small amount of direct hardware-interface support in the kernel itself, is written in a high-level language. (*High-level* is a historical term meant to distinguish from low-level assembler languages, which are basically thin wrappers around machine code.)

There are several different kinds of high-level languages. In order to talk about these, you’ll find it useful to bear in mind that a program’s source code (the human-created, editable version) has to go through some kind of translation into machine code that the machine can run.

### Compiled Languages

The most conventional kind of language is a compiled language. Compiled languages get translated into runnable files of binary machine code by a special program called (logically enough) a compiler. Once the binary has been generated, you can run it directly without looking at the source code again. (Most software is delivered as compiled binaries made from code you don’t see.)

Compiled languages tend to give excellent performance and have the most complete access to the OS, but also tend to be difficult to program in. C, the language in which Unix is written, is by far the most important of these (with its variant C++). FORTRAN is another compiled language still used among engineers and scientists but years older and much more primitive. In the Unix world no other compiled languages are in mainstream use. Outside the world of Unix, COBOL is widely used for financial and business software.

There used to be many other compiler languages, but most of them have either become extinct or are strictly research tools. If you are a new Unix developer using a compiled language, it is overwhelmingly likely to be C or C++.

### Interpreted Languages

An *interpreted* language depends on an interpreter program that reads the source code and translates it on the fly into computations and system calls. The source has to be reinterpreted (and the interpreter present) each time the code is executed.

Interpreted languages tend to be slower than compiled languages, and often have limited access to the underlying operating system and hardware. On the other hand, they tend to be easier to program and more forgiving of coding errors.

Many Unix utilities, including the shell, bc, sed, and awk, are effectively small interpreted languages. BASH scripts are usually interpreted. So is Tcl. Historically, the most important interpretive language has been LISP (a major improvement over most of its successors). Today Perl is very widely used and steadily growing more popular.

### P-code Languages

Since 1990, *p-code*, a kind of hybrid language that uses both compilation and interpretation, has become increasingly important. P-code languages are like compiled languages in that the source is translated to a compact binary form you actually execute, but which is not machine code. Instead it's *pseudocode* (or *p-code*), which is usually a lot simpler but more powerful than a real machine language. When you run the program, you interpret the p-code.

P-code can run nearly as fast as a compiled binary (p-code interpreters can be made quite simple, small, and speedy). But p-code languages can keep the flexibility and power of a good interpreter.

Important p-code languages include Python and Java.

![](img/a3584dae761d2e3abed8bf40d7637389_92_0.png)
