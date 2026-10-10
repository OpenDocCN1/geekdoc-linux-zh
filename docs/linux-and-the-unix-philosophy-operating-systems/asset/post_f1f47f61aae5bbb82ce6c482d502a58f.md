
## 7.3 Use lowercase and keep it short

One thing people first notice about the Unix system is that everything is done in lower case. Instead of operating with the lock key on all the time, Unix users enter everything in lower case letters.

There are a couple of reasons for this. First, lowercase letters are much easier on the eyes. If a person must work with text for an extended period, it soon becomes apparent that viewing lower case text is much more pleasant than eyeing uppercase. Second, and perhaps more important, lowercase letters use ascenders and descenders, the tiny lines that extend above or below the baseline of text, such as those found on the letters "l," "g," and "p." They transmit intelligible cues that your eyes pick up on when you read. They make reading easier.

Case is also significant in Unix. For example, "MYFILE.TXT" and "MyFile.txt" do not represent the same file. Unix employs lowercase letters for frequently used commands and file names. The upper case is normally used to grab someone’s attention. For example, naming a file "README" in a directory is a visual cue inviting the user to read the contents of the file before proceeding. Also, file names in directories are usually sorted alphabetically by the `ls` command, with capitalized names appearing before lowercase ones in a file list. This draws additional attention to the file.

While case sensitivity often causes much frustration for people who come to Unix after having used a case-insensitive operating system for a long time, they eventually adapt to it. Many even learn to like it.

Another quirk about Unix is that file names tend to be very short. Most frequently used command names are no more than two or three letters long. Terse-ness is golden here, and you will find such cryptic names as `ls`, `mv`, `cp`, and so on. Very long, multiword command names are often abbreviated to just the first letters of the words. For example, "parabolic anaerobic statistical table analyzer" reduces simply to "pasta."

The use of terse names is historical. Unix was originally developed on systems that had teletypes instead of CRT terminals. Typing on teletypes was accompanied by bzzzt-clunk sounds whenever one struck a key, and a fast teletypist could do about fifteen to twenty words per minute. Hence, shorter names for things were quite in vogue. The fact that most computer programmers back then didn’t know how to type had nothing to do with it. (Well, maybe a little.)

Why do Linux users persist in using the shorter names today? Certainly today’s PC keyboards can handle much higher speeds, so such brevity is no longer necessary. The reason is that shorter names allow you to cram much more on a command line. Remember that Linux shells have a pipe mechanism that allows you to string the output of one command into another on the command line.

This powerful feature is very popular with Linux users. They often string so many commands together on a single line that, if longer names were used, they would exceed the width of the window they’re using. One solution to the problem is to keep the lengths of individual commands short so more of them will fit within smaller windows when you have several adjacent windows open on the screen.

Of course, you may be with that of the Unix `ls` command. When it doesn't find any files in a directory, it simply returns to the command prompt:

```
sh> ls
sh>
```

Many people familiar with non-Unix systems often criticize Unix for failing to inform the user that the directory is empty. Unix advocates, on the other hand, argue that Unix has indeed informed the user that no files were proof with the refusal of the `ls` command to print any file names. The lack of file names is proof itself that the directory is empty. It's like saying that it's dark in a room instead of saying that there are no lights on. A subtle difference, yes, but an important one.

Are there any advantages to having commands that operate silently when no data is present? For one thing, your screen contains only meaningful data instead of being cluttered with commentary that transmits little useful information. It is easier to find trickles of data if they are not surrounded by an ocean of detail.

Although this keeps things simple, there is a more technical reason. As we discussed earlier, most Unix commands act as filters that are often combined using the Unix pipe mechanism. For example:

```
ls -l | awk '{print $4}' | sort
```

The `-l` parameter instructs `ls` to produce a longer, comprehensive file listing. The pipe symbol `'|'` connects the `ls` command's output to the `awk` command's input. The `'{print $4}'` part directs `awk` to print only the fourth field of each line of text produced by `ls` and discard the rest. This field is passed to the `sort` command, which sorts each field in alphabetical order.

In the typical scenario, such as when the directory contains several files, everything works
