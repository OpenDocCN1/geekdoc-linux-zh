
around the world in email for years before personal computers discovered the concept of the Internet. Many UNIX users, however, are still stuck making attachments by hand—which seems a little unfair because it’s UNIX machines that do the work of making the Internet possible for the personal computer users. If you aren’t using one of the more user-friendly email clients (more on email clients in Lesson 18, “Accessing the Network Resources”) that can handle attachments automatically, you’ll need to create them manually and insert them into your email yourself. Still, it isn’t a very difficult task. The more difficult task is convincing the personal computer users you might have to interact with to use a cross-platform attachment format, such as uuencode, instead of whichever proprietary format the popmail-client authors decide to favor this week.

The uuencode program accepts any file as input, and it produces an encoding of the file that can be included in an email message. To a person, the contents of this file look like random characters; on the receiving end, however, the user can use the uudecode program to extract the original file. Because every email program is different, you’ll need to consult the documentation for your email client on how to include a file in a message. Here, you’ll just learn how to create the uuencoded file from your original, and how to uudecode it again on the other side.

To use the uuencode command, you need to follow these steps:

- 1. Determine the name of the file you want to encode for email transmission.
- 2. Determine what you want the file to call itself at the other end.
- 3. Issue the uuencode command as uuencode <filename> <callmethis> > <filename>.uue (Yes, you need to type the > before the <filename>.uue argument.)

Your computer will then produce a file named <filename>.uue which contains the uuencoded version of the file.

For example, if you have a file named sendtojoe and you want to uencode it, you can type the following:

```
> uuencode sendtojoe hijoe > joe.uue
```

Your computer produces a file named joe.uue, which when decoded by Joe is named hijoe and contains the contents of your sendtojoe file.

Now you can copy and paste, or include, or do whatever you need to do to insert the file you just created into an email message and send it wherever you want.

Of course, if you receive a uuencoded file, you need to know how to decode the file. Decoding a uuencoded file is also extremely simple; issue the uudecode command as `uudecode <filename.uue>`.

Your machine will produce a file in the current directory identical to the one originally uuencoded.

> **Clearing up .uue** The filename of the .uue file and the filename to which it will decode itself do not have to be the same. This is sometimes confusing. If you receive a file named kludge.uue, issue the uudecode kludge.uue command, and do not find a file named kludge in your directory, don't be alarmed. The uuencoded file contains the filename as well as the uuencoded file contents. To find out what the uudecoded file will be named, use the head command to look at the first few lines of the uuencoded file. The filename to which it will decode appears on the first line.

## KDE ARCHIVING TOOLS

Desktop environments also now provide convenient drag-and-drop file compression and archiving tools. The KDE environment, for example, provides the KZip archive and compression tool.

To access the KZip tool, click the K on the KDE toolbar, choose Utilities from the pop-up menu and Zip from its submenu. A window similar to the one shown in Figure 10.1 will appear.

![](img/2c005cbaad58c25c7f54da948131a75e_121_0.png)

*Figure 10.1 The KDE built-in archive manager, KZip.*

The KDE KZip tool can work with tar and gzip files: choose Open from the File menu and select your archive. The KZip tool provides convenient features such as display of archive entry contents by simply double-clicking the entry, and drag-and-drop addition of files to archives.

## SUMMARY

When you need to conserve disk space or shorten file transmission times, you might need to resort to compacting your files with some sort of compression utility. Here's a look at what was learned in this lesson:

- The three common compression utilities on UNIX systems are the omnipresent compress, the newer and smarter gzip, and the cross-platform zip programs. A relatively new addition to the UNIX compression scene is bzip2, which appears to produce better compression than compress or gzip.
- When you need to provide a collection of files to other users or simply archive a set of files for future use, you can use tar to create tar-files that contain all your files in one convenient package.
- Don't be an impolite user and use tar to archive individual files. Instead, put all the files you want to archive in a directory and tar the directory.
- If you need to send a file to someone via email, you can create an email-able encoding of the file by using the uuencode command.
- Don't be alarmed if you uudecode a file and can't immediately find it—the real filename is stored in plain text at the beginning of the file.

![](img/2c005cbaad58c25c7f54da948131a75e_123_0.png)

## LESSON 11
### PROCESSES

*In this lesson you will learn how to work with processes: view them, kill them, and bend them to your whims!*

Everything that you've run on your system in the previous lessons, and everything that you're going to be running in the rest of the lessons, created processes on your system. Each command creates a process that the UNIX operating system runs until it is finished or killed. Unlike some desktop operating systems, you can create processes that run entirely in the background, or that start and run in the middle of the night—without you even needing to be logged into the computer.

## More Than One Command at a Time

UNIX enables you to run more than a single command at a time. This capability is known as multi-tasking and is available in different forms on some other operating systems as well. What makes UNIX different is that absolutely everything on UNIX is a process: Want a clock? Run a program. Need to copy files? That's a process too. Opening a window—yet another process. Although many personal computer OSes enable you to run a few applications at the same time, most handle large portions of their functionality by having it all be part of one big program. On UNIX, the actual operating system is very small, and it runs lots of programs simultaneously to provide the interface and other functionality to you.

Along with UNIX's absolute requirement to run many simultaneous programs just to provide the environment to the user comes the fact that the user can run as many simultaneous programs as he or she wants. On a UNIX box, you run programs for anything that you want to do. As a consequence of the way the OS works, it doesn't actually matter whether or not you're logged in while they run. Your being logged in is—you got it—just another process.

## PUTTING A COMMAND INTO THE BACKGROUND: &

Making a command run in the background is simple; you simply add an & to the end of the line containing the command.

For example, suppose you are running a program called analog to analyze your Web server logfiles. Most log analysis takes quite some time for a busy Web server, so you probably don't want to wait around for the command to finish. In order to run analog in the background, you can just type the following:

```
>analog /var/log/httpd/access_log &
[3] 32566
>
```

The results are a bit cryptic, but you can see that you are returned to the command line, ready to go about your business! The two numbers that are returned identify the process on the system. The first result, [3], identifies this as process number 3 that you've sent to the background. The second number, 32566, is the process ID. Your UNIX system potentially has hundreds of processes running on it, and each one is assigned a unique number. Whatever number your process happens to be assigned is returned as the second result value.

![](img/2c005cbaad58c25c7f54da948131a75e_124_0.png)

> Running More than One Command To run several commands, one after the other, and put the whole group into the background, you can use the following syntax: {<command 1>; <command 2>; <command 3>} &. This creates a new shell to execute the commands and places it in the background. For example, if you wanted to run the analog utility on two files, you might use something such as the following: (analog /var/log/httpd/access_log; analog /var/log/httpd/new_access_log) &
