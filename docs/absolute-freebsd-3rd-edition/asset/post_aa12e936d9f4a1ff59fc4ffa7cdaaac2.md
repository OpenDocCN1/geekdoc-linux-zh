
GhostBSD: run raw FreeBSD. Yes, I know, now that dog food doesn’t sound so bad. But learning an operating system is like learning a language; total immersion is the quickest and most powerful way to learn. That’s what I did, and today I can make a Unix-like system do anything I want. I’ve written entire books on a FreeBSD laptop, using the open source text editor XEmacs and the LibreOffice.org business suite. I’ve also used FreeBSD to watch movies, rip and listen to MP3s, balance my bank accounts, process my email, and surf the web. The desktop in my lab has a dozen animated BSD daemons running around the window manager, and I occasionally take a break to zap them with my mouse. If this doesn’t count as a Stupid Desktop Trick, I don’t know what does.

Many Unix system administrators these days come from a Windows background. They’re beavering away in their little world when their manager swoops by and says, “You can handle one more system, can’t you? Glad to hear it! It’s a Unix box, by the way,” and then vanishes into the managerial ether. Once the new Unix administrator decides not to quit her job and start a fresh and exciting career as a whale necropsy technician, she tentatively pokes at the system. She learns that `ls` is like `dir` and that `cd` is the same on both platforms. She can learn the commands by rote, reading, and experience. What she can’t learn, coming from this background, is how a Unix machine thinks. Unix will not adjust to you; you must adjust to it. Windows and macOS require similar adjustments but hide them behind a glittering facade. With that in mind, let’s spend a little time learning how to think about Unix.

## How to Think About Unix

These days, most Unix systems come with pretty GUIs out of the box, but they’re just eye candy. No matter how graphically delicious the desktop looks, the real work happens on the command line. The Unix command line is actually one of Unix’s strengths, and it’s responsible for its unparalleled flexibility.

Unix’s underlying philosophy is *many small tools, each of which does a single job well*. My mail server’s local programs directory (`/usr/local/bin`) has 262 programs in it. I installed every one of them, either directly or indirectly. Most are small, simple programs that do only one task. This array of small tools makes Unix extremely flexible and adaptable. Many commercial software packages try to do everything; they wind up with all sorts of capabilities but only mediocre performance in their core functions. Remember, at one time you needed to be a programmer to use a Unix system, let alone run one. Programmers don’t mind building their own tools. The Unix concept of pipes encouraged this.

## Pipes

People used to GUI environments, such as Windows and macOS, are probably unfamiliar with how Unix handles output and input. They’re used to clicking something and seeing either an OK message, an error, nothing, or (all too often) a pretty blue screen with nifty high-tech letters explaining in the language called *Geek* why the system crashed. Unix does things a little differently.

Unix programs have three channels of communication, or *pipes*: standard input, standard output, and standard error. Once you understand how each of these pipes works, you’re a good way along to understanding the whole system.

- **Standard input** is the source of information. When you’re at the console typing a command, the standard input is the data coming from the keyboard. If a program is listening to the network, the standard input is the network. Many programs can rearrange standard input to accept data from the network, a file, another program, the keyboard, or any other source.

- **Standard output** is where the program’s output is displayed. This is frequently the console (screen). Network programs usually return their output to the network. Programs might send their output to a file, to another program, over the network, or anywhere else available to the computer.

- **Standard error** is where the program sends its error messages. Frequently, console programs return their errors to the console; others log errors in a file. If you set up a program incorrectly, it just might discard all error information.

These three pipes can be arbitrarily arranged, a concept that's perhaps the biggest hurdle for new Unix users and administrators. For example, if you don't like the error messages appearing on the terminal, you can redirect them to a file. If you don't want to repeatedly type a lot of information into a command, you can put the information into a file (so you can reuse it) and dump the file into the command's standard input. Or, better still, you can run a command to generate that information and put it in a file, or just pipe (send) the output of the first command directly to the second, without even bothering with a file.

## Small Programs, Pipes, and the Command Line

Taken to their logical extreme, these input/output pipes and the variety of tools seem overwhelming. When I saw a sysadmin type something like the following during my initial Unix training session, I gave serious consideration to changing careers.

```
$ tail -f /var/log/messages | grep -v popper | grep -v named &
```

Lines of incomprehensible text began spilling across the screen, and they kept coming. And worse still, my mentor kept typing as gibberish poured out! If you're from a point-and-click computing environment, a long string of commands like this is definitely intimidating. What do all those funky words mean? And an ampersand? You want me to learn *what?*

Think of learning to use the command line as learning a language. When learning a language, we start with simple words. As we increase our vocabulary, we also learn how to string the words together. We learn that placing words in a certain order makes sense, and that a different order makes no sense at all. You didn't speak that well at three years old—give yourself some slack and you'll get there.

Small, simple programs and pipes provide almost unlimited flexibility. Have you ever wished you could use a function from one program in another program? By using a variety of smaller programs and arranging the inputs and outputs as you like, you can make a Unix system behave in any manner that amuses you. Eventually, you’ll feel positively hoggied if you can’t just run a command’s output through `sort -rnk 6 | less`.

## Everything Is a File

You can’t be around Unix for very long before hearing that everything is a file. Programs, account information, and system configuration are all stored in files. Unix has no Windows-style registry; if you back up the files, you have the whole system.

What’s more, the system identifies system hardware as files! Your CD-ROM drive is a file, `/dev/cd0`. Serial ports appear as files like `/dev/cua0`. Even virtual devices, such as packet sniffers and partitions on hard drives, are files.

When you have a problem, keep this fact in mind. Everything is a file, or is in a file, somewhere on your system. All you have to do is find it!

## Notes on the Third Edition

*Absolute BSD* (No Starch Press, 2002) was my first technology book and was written when the various BSD operating systems had more in common than they wanted to admit. The second edition, *Absolute FreeBSD* (No Starch Press, 2007), came out after the BSDs had diverged, and detailed FreeBSD’s advances in the previous five years. With another decade of growth, FreeBSD has evolved to compete with the best commercial operating systems. You’ll find multiple top-tier filesystems. Disk management has changed to accommodate new partitioning methods. Virtualization is now a thing, and FreeBSD supports it as either a client or a host.

This growth has driven changes in this book.

We won’t discuss configuring mail, DNS, or web servers. You have more software choices for these tasks than ever before. Entire books have been written about those choices and how to use them. I’ve written
