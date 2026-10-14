
| *.txt | Matches all files that end with .txt |
| file* | Matches all files beginning with the word file |
| file*.txt | Matches all files beginning with the word file and ending with .txt |

## Match Any Letter: ?

The star is powerful, no doubt about it. Sometimes, in fact, it’s too powerful. Because it can stand for any number of characters, it can potentially match things you don’t want to match. Luckily, there is a more restrained metacharacter: The ? will match one letter exactly, regardless of what the character at that position is. However, there must be a letter in the position you specify, or there’s no match. See Table 14.2 for examples.

## Table 14.2 Examples of Using the Question Mark

| Example | Description |
| file?.txt | Matches all files that begin with file, are followed by a single character, and end in .txt |
| ? | Matches all files that have a one-letter name |
| ?? | Matches all files that have a two-letter name |

## Match in a Range: []

Sometimes you want to match a variety of options. Let’s say you wanted to use metacharacters to find file1.txt and file2.txt but not file3.txt. In that case, you need to provide a set of options enclosed by brackets, like this:

```
file[12].txt
```

This pattern will match file1.txt and file2.txt—nothing else.

If you want to find a continuous range of characters—say you wanted to match the numbers 0 through 5—you can specify them as [0–5] instead of [012345].

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

Previous Table of Contents Next

## Negating a Range: !

Sometimes it’s easier to specify what you don’t want matched. For example, if you had files named f11, f12, f13, f14, and f15, and you wanted to move only f12-f15, you could specify the range as I did here. But it might be easier to specify the files you don’t want by using f11[!1]. In this case, every file but f11 will be matched.

## Command History

Every time you type a command on the shell, the shell remembers it in what is called a history list. You can view the history by typing history on the bash prompt. A list of all the commands you have typed will be listed. Each command will have a number associated with it.

You can “recycle” commands that appear in your history to avoid having to retype them. To re-issue a command which appears in your command history, just type an exclamation point (!) followed by the number of the command you want to re-issue:

```
[alberto@digital alberto]$ !138
```

The very last command you entered is special. If you want to repeat it, just enter two exclamation points (!!). For example, you could type this:

```
[alberto@digital alberto]$ !!
```

You can move up through your command history by using the up arrow on your keyboard. Doing so will put the command on your prompt so you have a chance to edit it before you re-execute it.

How many commands your history holds will depend on the setting of the HISTSIZE environment variable. By default, it is set to remember your last 100 commands.

## Jobs: Working on Multiple Things Using a Shell

Some command line jobs will take a while to complete. For example, the command ls -R / > filelist.txt 2> error.txt could easily take several minutes before it is done. If you have a lot of files and are listing several network drives, expect it to run for half an hour or so.

With Linux being multitasking, you’d probably want to do something else while the command runs. You can do this very easily by running the command concurrently or in the background. To execute the same command in the background, enter the following:

```
ls -R / >filelist.txt 2>error.txt &
```

The key here is the ampersand (&) at the end of the command line. This tells the shell to run the job in the background. After issuing the command, you’ll see something like the following:

```
[alberto@digital alberto]$ ls -R / > filelist.txt 2> error.txt &
[1] 872
[alberto@digital alberto]$
```

The job starts and your command line comes back. The number in brackets is the job number or process id assigned to your command. The 872 is the process id for the job in the system-wide process list. The process id for a job is useful in case you need to kill the job (see “Killing a Process: kill” in Chapter 22, “System Monitoring: Keeping an Eye on Your System”). Jobs are a little easier to remember than a process id of 872. When referring to a job number, always precede it with a percent (%) symbol. Both give you a way of controlling the command and to return it back to the front. When the job is completed, you’ll see a line like this:

```
[1]-  Done              ls -R / >filelist.txt 2>errors.txt
```

This means your job is done running. Note that programs which produce lots of output on the display should not be run in the background unless the output is redirected. Otherwise, your command prompt will be difficult to use, since output from the background command will continue to appear as you type!

Some programs will require interactive input, so every once in a while you’ll see this:

```
[1]+  Stopped (tty output)    telnet localhost
```

This means that the job needs input, and has paused to wait for keystrokes from you. To bring the job back to the front and enter the required keystrokes, use the command fg:

```
[alberto@digital alberto]$ fg %1
```

This will bring job number one (%1) back to the foreground. Note that there’s a percent symbol (%) before the job number.

To list all jobs started from inside the current shell, use the jobs command, like this:

```
[alberto@digital alberto]$ jobs
[1]+  Stopped (tty output)    telnet localhost
```

## Suspending a Job

You can suspend a process that is running in the foreground by hitting Ctrl+Z. This will put the process to sleep:

```
[alberto@digital alberto]$ ls -R / > filelist.txt 2> errors.txt

[1]+  Stopped                ls -R / >filelist.txt 2>errors.txt
[alberto@digital alberto]$ bg %1
```

```
[1]+ ls -R / >filelist.txt 2>errors.txt &
```

In this listing, I started a lengthy process in the foreground. I then put it to sleep (stopped it) by pressing Ctrl+Z and revived it in the background with a bg %1. bg does the opposite of the fg command.

## Killing a Job

To kill the current foreground process, you can issue a Ctrl+C. This will terminate the process. To kill a job running in the background, you can use the kill command followed by its job number or its process id:

```
[alberto@digital alberto]$ kill %1
[alberto@digital alberto]$ kill 872
```

As you can see, the shell both is powerful and complex. Even though we have only barely scratched its surface, what you know can help you to get loads of work done!

## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)

Author(s): Manuel Ricart

ISBN: 078971826x

Publication Date: 12/22/98

Bookmark It

Search this book:

Previous Table of Contents Next

## Chapter 15
Help Please

## In This Chapter

- Accessing the UNIX Manual Pages
- Searching for Help by Keyword
- The Whatis Database
- Getting Online Help
- Finding Your Answer with HOWTO Documents
- The Linux Documentation Project (LDP)
- Reading Info Pages

So far, you have been relying on this book for information about Linux. The commands discussed represent only a tiny fraction of what are available. This book doesn’t explain how to configure or use many things that you will eventually want to run on your system; for that I would need an additional 400 pages.

Before you despair, remember that this book is intended to get you up to speed with many basic topics related to both Linux and UNIX. In order for you to gain a full understanding, you will have to supplement the information you find here with additional sources. Some of these sources are already in your computer; others are available from other books or from resources freely available over the Internet.

In this chapter, you’ll take a short tour on the various resources you can utilize to get up to speed with Linux. This will empower you to find and solve problems on your own. You will learn a great deal by reading and tinkering as your needs require.

One interesting thing about Linux is that it is well documented. Whereas other operating systems (OSs) provide you with detailed information about certain aspects of your system, you will soon realize that Linux provides abundant information on just about everything installed in it. This is mostly due to the open nature of Linux. In a world where the tools are added by a distributed collection of programmers,
