script from the file, make it executable, and run it. Then you should find a file called /dev/sndstat generated for you.

There are several error messages you may see in /dev/sndstat that help you determine the problem with your sound card. Table 21.2 shows the most common messages, the reason they are generated, and a possible solution. In each case the error message is preceded by the device name.

**TABLE 21.2.** /dev/sndstat ERROR MESSAGES.

| Error message | Reason generated and solution |
| :--- | :--- |
| No such device | The kernel does not contain the sound card drivers. Rebuild the kernel. |
| No such device or address | The sound card driver couldn't find the sound card at the configuration you specified. Check the configuration settings. |

# # Applications for Sound Cards

There are quite a number of applications that work with your sound card, depending on what you want to do. Most of these applications are available from FTP sites or may be included with your CD-ROM Linux distribution. To check whether the files are on your system or your CD-ROM, use the find command to look for the executable program's name.

We're not going to look at each application that is available for Linux because there are several dozen. Instead, we'll pick a few representative examples. Checking out the FTP sites will show you all the others that are available.

# ## vplay, vrec, splay, and srec

The vplay utility and its three partners are a suite of sound tools called snd-util developed by Hannu Savolainen and Michael Beck. These are straightforward sound recording and playback utilities developed in the early stages of Linux, but work well even today if you are willing to use a command-line interface instead of a fancy GUI. The srec tool records sounds and splay replays them. (To record, you need either a microphone or other input device such as a feed from a CD.)