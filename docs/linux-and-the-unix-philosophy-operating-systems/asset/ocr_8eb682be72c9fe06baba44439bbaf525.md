# 7.5 Silence is golden

No, we're not saying that Unix programmers shun multimedia. We're talking about so-called user-friendly programs that overstate the obvious or treat the user as though he or she were the software's best friend. Too many programmers believe that they're being helpful by addressing the user in a conversational tone. Unix is unusually dry in that it provides "just the facts, ma'am"-nothing more, nothing less.

Many Unix commands remain silent if they have received no input data or have no data to produce as output. This can be a bit disconcerting to the novice Unix user. For example, on a typical non-Unix system, the user might type the following command in a directory containing no files. Notice how the system responds by informing the user that no files were found:

```
$DIR
DIRECTORY: NO FILES FOUND
$
```

Contrast the above response with that of the Unix `ls` command. When it doesn't find any files in a directory, it simply returns to the command prompt:

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