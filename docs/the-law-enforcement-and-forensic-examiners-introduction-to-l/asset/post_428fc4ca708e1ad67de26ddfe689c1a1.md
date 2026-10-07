
# A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

contents of the file offset. The file hits.txt should give you a list of lines that contains the words in your searchlist.txt. In front of each line is a number that represents the byte offset for that "hit" in the image file. For illustration purposes, the search terms are underlined, and the bytes offset are bold in the output:

```
barry@forensic:~ cat analysis/hits.txt
75441:I have enough of your mindless corporate piracy and we no longer stand
for it. You will recieve another letter next week. It will have a single bank
account number and bank name. I want you to deposit $50.00 in the account
day you receive the letter.
75767:Don't try anything, and dont contact the cops. If you do, I will unleash a virus that will bring down your network and destroy your consumer's
confidence.
```

Keeping with our command line philosophy, we will use xxd to display the data found at each offset. xxd is a command line hex dump tool, useful for examining files. Do this for each offset in the list of hits. The -s option to xxd is so we can "seek" into the file specified number of bytes. This would yield some interesting results if you scroll above and below the offsets. We'll use xxd and seek to the first hit by offset 75441 with the -s option. We pipe the output to the head command, which will show us the first 10 lines of output. You can view the rest of the output by piping through less indent.

```
barry@forensic:~ xxd -s 75441 fat.raw | head
0012b1: 6976 7520 616e 6426 796f 7572 2065 6274 you and your ent
0012c6: 6972 6520 6275 7369 6465 7373 2072 6176 ire business ran no
0012d6: 736f 622e 00a0 5468 6363 2069 7365 626f som...This is no
0012e6: 7465 6272 6965 6464 6265 7069 7461 6466 t a pike...I have hav
0012f8: 6561 6568 6565 6465 6775 606e 2068 6062 e had enough of
0012g8: 7272 6973 6265 6174 706f 7061 6379 7371 r your mindless co
0012h7: 7278 7976 6572 2864 6065 6373 7060 6272 7072 rote piracy a
0012i7: 6e64 6260 2079 6963 626f 6265 6665 6776 nd we will be no
0012j7: 7361 7374 7364 6265 666f 7272 6974 2072 stand for it.
0012k7: 596f 7520 7769 6363 2072 6563 6965 7605 You will receive
```

Please note the use of grep in this manner is fairly limited. There are characters that the common versions of grep (and strings) will not support. Doing a physical search for a string on an image file is really only for what it shows you. In other words, negative results for a grep search of an image can be misleading. The strings or keywords in the image are far not recognizable to grep or strings. There are tools that this addresses, and we will discuss some of them.

In addition to the structure of the commands and the issues of image sizes, we also have to be concerned with memory usage and our tools. You might find that grep, when used illustrated in small image analysis example, might not work as expected with larger images and the causes could exit with an error similar to:

```
grep: memory exhausted
```

The most apparent cause for this is that grep does its searches line by line. When you are “grepping” a large disk image terabytes in size, you might find that you have a huge number of bytes to read before grep comes across a newline. What if grep had to read several gigabytes of data before coming across a newline? It would “exhaust” itself (the input buffer fills up). There are many variables that affect this, and the causes are actually far complex.

One potential solution is to force-feed some newlines. In our analysis we are “grepping” for text. We are not concerned with non-text characters at all. If we could the input stream to grep and change the non-text characters to newlines, in cases grep would have no problem. Note that changing the input stream to grep does not change the image itself. Also, remember that we are still looking for a byte offset. Luckily, the character sizes remain the same, and the offset does not change as we feed newlines into the stream (simply replacing one “character” with another).

Let's say we want to take all of the control characters streaming into grep from the disk image and change them to newlines. We can use the translate command, tr, to accomplish this. Check out tr for more information about this powerful command:

```
barry@forensic1:-$ tr '[:ctrl:]' '\n' < fat_fs.raw | grep -abif analysis/searchlist.txt
```

7541:i have enough of your minded corporate piracy and will no longer stand for it. you will receive another letter next. It will have a single bank account number and bank name. I want you to deposit $50,000 in the account the day receive the letter.

7567:Don't try anything, and contact the cops. If you do, I will unleash a virus that will bring your whole network and destroy your consumer's confidence.

This command would: “Translate all the characters contained in the set of characters [:ctrl:] to newlines \n. Take the input to tr from fat_fs.raw (we are redirecting in the opposite direction this time) and pipe the output to grep, and then to head. The output does not change. The translation occurs in the stream, and it’s for a character swap.

This is only one of many possible problems you could come across. My point is that when these issues arise, you need to be familiar with the Linux tools to be able to understand why such errors might have been produced, and how you can get around them. Remember, the shell tools and the GNU software that accompany a Linux distribution are extremely powerful, and are capable of tackling nearly any task. Where the standard shell fails, you might look at perl or python as options. These subjects are outside of the scope of the current presentation, but are introduced as fodder for further experimentation.

Be sure to unmount the image when you are finished:

```
barry@forensic1:-$ su -
root@forensic1:-$ umount /mnt/
root@forensic1:-$ exit
```

# VIII. Advanced (Beginner) Forensics

The following sections are more advanced and detailed. New tools are introduced to help round out some of your knowledge of the command line. Although they are still at the beginner level, it is important that you follow along on your own system as typing at the keyboard is the best way to learn.

# The Command Line on Steroids

Let's dig a little deeper into the command line. Often there are arguments about the usefulness of the command line interface (CLI) versus a GUI tool for analysis. I would argue that in the case of large sets of regimented data, the CLI can be faster and more flexible. As an example, we will look at a set of log files from a single Unix system. We are not analyzing them for any sort of evidentiary data. The point here is to illustrate the ability of commands from the CLI to organize and parse data by using pipes to show a series of commands together and achieve the desired output. Follow along with the example, and keep in mind to get anywhere near with this will require a great deal of payoff. The payoff is enormous. Create a directory called Logs and download the file logs.v3.tar.gz into that directory:

```
barry@forensic1:~$ mkdir Logs
barry@forensic1:~$ cd Logs
barry@forensic1:~/Logs$ wget http://www.linuxleo.com/Files/logs.v3.tar.gz
--2017-05-20 15:16:41-----
Resolving www.linuxleo.com (www.linuxleo.com)... 216.250.120.84
Connecting to www.linuxleo.com (www.linuxleo.com)|216.250.120.84|80..: connected.
HTTP request sent, awaiting response... 200 OK
Length: 5144 (5.0K) [application/gzip]
Saving to 'logs.v3.tar.gz'
logs.v3.tar.gz         100%[====================]> 5.02K  --KB/s  in 0s
2017-05-20 15:16:41 (401 MB/s) - 'logs.v3.tar.gz' saved [5144/5144]
```
