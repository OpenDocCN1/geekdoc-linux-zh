![](image_rsrc1F6.jpg)

![](image_rsrc1F7.jpg)     Table of Contents

* * *

●          [About Autho](#part0002.xhtml) r●          [How to Contribute](#part0003.xhtml)●          [Legal Notices](#part0004.xhtml)●          [Introduction](#part0005.xhtml)●          [Chapter 1: Linux Shortcut Keys For Terminal](#part0006.xhtml)●          [Chapter 2: Basic Text Editor Command](#part0007.xhtml)●          [Chapter 3: Basic Operating Command](#part0008.xhtml)●          [Chapter 4: pwd Command](#part0009.xhtml)●          [Chapter 5: man Command](#part0010.xhtml)●          [Chapter 6: ls Command](#part0012.xhtml)●          [Chapter 7: mkdir Command](#part0014.xhtml)●          [Chapter 8: rmdir Command](#part0015.xhtml)●          [Chapter 9: rm Command](#part0016.xhtml)●          [Chapter 10: cp Command](#part0018.xhtml)●          [Chapter 11: wc Command](#part0020.xhtml)●          [Chapter 12: cd Command](#part0022.xhtml)●          [Chapter 13: mv Command](#part0024.xhtml)●          [Chapter 14: cat Command](#part0026.xhtml)●          [Chapter 15: touch Command](#part0028.xhtml)●          [Chapter 16: head Command](#part0029.xhtml)●          [Chapter 17: tail Command](#part0031.xhtml)●          [Chapter 18: find Command](#part0033.xhtml)●          [Chapter 19: echo Command](#part0035.xhtml)●          [Chapter 20: Process Command](#part0037.xhtml)●          [Chapter 21: kill Command](#part0038.xhtml)●          [Chapter 22: date Command](#part0040.xhtml)●          [Chapter 23: calendar Command](#part0042.xhtml)●          [Chapter 24: tar Command](#part0043.xhtml)●          [Chapter 25: group Command](#part0044.xhtml)●          [Chapter 26: groupadd Command](#part0045.xhtml)●          [Chapter 27: groupdel Command](#part0045.xhtml_a1BR)●          [Chapter 28: group Command](#part0046.xhtml)●          [Chapter 29: users Command](#part0047.xhtml)●          [Chapter 30: sudo Command](#part0047.xhtml_a1CP)●          [Chapter 31: apt-get Command](#part0047.xhtml_a1DD)●          [Chapter 32: grep Command](#part0047.xhtml_a1DC)●          [Chapter 33: chmod Command](#part0048.xhtml)About AuthorHey, My name Rajdeep Singh.  I created this Book Because I got stuck in Linux Command flags or Options. I started visiting the website, reading books, and a few articles that provide Some Information. But That Article Very Old. So That I'm Relasize This Problem To Find Resource Then Start A Written Book On Linux Commandline Flags. My Dreams About This Book  Every Clear Everyone Contributes On this Book And Improves It. This  Book Freely Available For Every One Read it and Improve it.Read More About the Author:●          [https://medium.com/officialrajdeepsingh/my-learning-path-biology-to-computer-science-70bec32db8ea](https://medium.com/officialrajdeepsingh/my-learning-path-biology-to-computer-science-70bec32db8ea)●          [https://officialrajdeepsingh.medium.com/](https://officialrajdeepsingh.medium.com/)●          [https://www.officialrajdeepsingh.dev/](https://www.officialrajdeepsingh.dev/)Contact Author●    [https://www.officialrajdeepsingh.dev/contact-me/](https://www.officialrajdeepsingh.dev/contact-me/)●    officialrajdeepsingh@gmail.comHow to Contribute

* * *

How To Contribute?
If You Contribute to an Open Source Book. Make Sure You Have Your Own GitHub Account, Require Email(for certification only), and GitHub UserName. You Change On Github Repository.You change According To your own thought then push back Code on Github. We Check and update our book.Secondly, we Add Your Name To the Author Contribute list and Send Your a Contribute certificate on your email.Legal NoticesDisclaimerAll rights reserved. No part of this publication may be reproduced, stored, or transmitted in any form or by any means, electronic, mechanical, photocopying, recording, scanning, or otherwise without written permission from the publisher. It is illegal to copy this book, post it to a website, or distribute it by any other means without permission.Use the concepts, examples, and other content at your own risk. There may be errors and inaccuracies, that may of course be damaging to your system. Although this is highly unlikely, you should proceed with caution. The author does not accept any responsibility for any damage incurred.IntroductionWhat is Linux?Linux Is an Open Source  Unix-like operating system Like Windows, macOS, and iOS. first released Linux System on September 17, 1991, by Linus Torvalds.Who uses Linux?Daily Life the Linux operating system Use  Everywhere. The most popular platform on the planet, Android, is powered by the Linux operating system.Main My Focuses On Linux Command If Interested Linux History Make Sure Follow My Reference Link●          [https://en.wikipedia.org/wiki/Linux](https://en.wikipedia.org/wiki/Linux)●          [https://www.linux.com/what-is-linux/](https://www.linux.com/what-is-linux/)What Inside Book?The Book author tries To Cover Lots of Linux commands and Flags Inside the Book. If Interested To Learn More About Linux Command Option Or Flags Then This Book For YouWhy Read This Book?The Book Author Clear Says That If you are Interested To Learn Linux Command with Flag and  Option Then Read It.If You're Not Interested In Reading This Book. I Highly Recommend You To Watch YouTube Video.Follower This Playlist:[Playlist Name: Linux Command Line For Beginners  By ProgrammingKnowledge](https://www.youtube.com/watch?v=YHFzr-akOas&list=PLS1QulWo1RIb9WVQGJ_vh-RQusbZgO_As)Or Follow any other Youtubers Video and PlaylistChapter 1Linux Shortcut Keys For Terminal

* * *

Open terminal:

| Ctrl + Alt + T |

●         Ctrl + L : Clears the screen, similar to the clear command in the terminal.●        Ctrl + S: Stop all output to the screen. When You run Commands with long output. But this doesn't stop the running command.●         Tab : tab Help Automatic Fill Your Name.●         Ctrl + A : Cursor goes to Start Of Word●         Ctrl + E : Cursor goes to End Of Word.●         Ctrl + F : Move the cursor forward one by one character.●         Ctrl + B : Move the Cursor backward one by one Character.●         Alt + F : Move the cursor forward one by one Word.●         Alt + B : Move the Cursor backward one by one Word.●         Alt + U : Change Character or Word Into Uppercase.●         Alt + l : Change  Character Or Word Into Lower Case.●         Alt  + T : Swap the last two words before the cursor.●         Alt + C : Use Capitalize  Words.●         Alt + D : Delete to end of word starting at the cursor●        Ctrl + K : Cut Word/Line from the current position to the end of the line. also adding it to the clipboard use ctrl + y to paste it again.●        Ctrl + W : Delete the word before the Cursor Position. Also adding it to the clipboard use ctrl + y paste on it●         Ctrl + Y : Paste the last thing from the clipboard that you cut recently.●         Ctrl + D : Delete Character By Character.●         Ctrl + T : Remove White Space.●         Ctrl + Shift + W : close terminal tab.●         Ctrl + Shift + Q : close the entire terminal.●         Shift+Ctrl + N : Open New Window.●          Shift + Ctrl +T : Open New Tab In Window.●          Shift + Ctrl + W : Close Tab.●          Shift + Ctrl + Q : Close Window.●          Shift + Ctrl + C : Use For Copy Text Inside Terminal.●          Shift + Ctrl +  V : Paste Text Inside Terminal.●          Shift + Ctrl + + : Zoom In.●          Shift + Ctrl + - : Zoom Out●          Shift + Ctrl + ) : Zoom Reset●          Shift + Ctrl + I: Add Name Off Each Open TabChapter 2Basic Text Editor Command

* * *

nana : nano is a small and friendly editor inside your cmd tool.Syntax:nano [options] [file ..]

* * *

vim : Vim is a text editor. It can be used to edit all kinds of Programming Language.  It is especially useful for editing inside cmd Tool.Syntax:vim [options] [file ..]Chapter 3Basic Operating Command Terminal

* * *

whatis : whatis Command help to Displays Manual Pages Small Descriptions.Syntax:whatis  [CommandName...]

* * *

which : which help to locate, your Command Storage Location Inside Your Laptop. which command mostly  use your bash scriptingSyntax:which [CommandName...]Chapter 4pwd Command

* * *

pwd :   show current directorypwd --help : display help page document About pwd Command.pwd  --version : Print pwd Command Version.pwd -man : Read pwd Manual Page Use with  -man CommandChapter 5man Command

* * *

man : man Command Provide an interface, This Interface Help To Read Manuals Page reference On Your Terminal.Syntax:ls [OPTION]... [COMMANDS]...Options Working With Command:man -w : this Flag Don't display any manual pages, but print the locations Of Command Which Place Save Inside Your Laptop.man -f or man –whatis : This Flag Show You a short description from the manual page, if Description is available.man man : Provide You To Comand Manual Page InformationOption Which Working Only For Man Command:man --help : This Flag Provides You  help page document About man Command.man --usage : give a short usage message about Commandman -V or man --version : print man Comand versionNote :●           Man Command Provide Lots Off Option We Recommend You Visit Command Man Page For Learn More●          Quit man simple use q for quit or Exit Command.●          Keyboard arrow keys use For Scroll Page up for page up↑  and down for page down ↓ keys.Quiz About man Command

* * *

Q.1 How To Check mkdir Command Manuals Page Reference?Ans. pi@raspberrypi:~ $ man mkdirQ.2 How To Save Command Manuals Page  Information On Laptop in txt File.Ans. pi@raspberrypi:~ $ man ls > lsManPages.txtChapter 6ls Command

* * *

ls : Provide Information About Files Which Present inside the directory. by default Provide current directory Information in alphabetical order.Syntax:ls [OPTION]... [FILE]...Command Options                           Descriptionls -a : Mean all Files Show Inside Terminal.ls  -A : Mean almost all File But Do not Show . and .. Filesls -l  --author : this Command Work With -l Flag Or Option and it prints out the author Information of each filels -b : the ls command provides an option that - when used - prints C-style escape characters for non-printable characters.ls --block-size=SIZE : This Flog Convert Your File With Different Size.Example Megabyte,kilobyte and Other soo.●       ls -l –-block-size=K : Convert File To Kilobyte●       ls -l –-block-size=M : Convert File To Megabytels -c : this Flag Give You Output, Which File Recently You modify and This Option Never Be Work With -l Flagls --color[=WHEN] : Show Output With Colorize. The default can always be auto. if Stop This You Use never.●       ls –color=never●       ls –color=autols -G : Print list Without Group Namesls -h or ls --human-readable : Print Output with with -l and -s. Show File Sizes In CMD like 1K 234M 2G.ls -i or ls --inode : print the index number of each file In Your Cmd.ls -k or ls --kibibytes : this  Flag Show You Block Size Of Each File.By default Each Block Size 1024-byte.-k Flag Working With -s Flagls -l : Print long listing Information format Pattern Inside Your Cmd.ls -m : m flag Show comma separated list of entries Files.ls -n or ls --numeric-uid-gid : Show you numeric user and group Ids.ls -N : -N Flag print File names without comma separated or quoting( , ).ls -o : Print Information Without List Group Information.ls -p   or  ls --indicator-style=slash : append Slash / After Your directories Files Name.Note: Indicate- style Work Same Or Note--indicator-style arguments are:●           ‘none’●           ‘slash’●           ‘file-type’●           ‘classify ’ls -Q or ls --quote-name : Show Your File Name With double quotes .ls --quoting-style=”escape” : Style Your quoting Inside Your TerminalMore arguments are:●           ‘literal’●           ‘shell’●           ‘shell-always’●           ‘shell-escape’●           ‘shell-escape-always’●           ‘c’●           ‘c-maybe’●           ‘escape’●           ‘Locale’●           ‘clocale’ls -r or ls --reverse : Print reverse order Your Files (z to a)ls -R or ls --recursive : print Your All Files With subdirectories Filesls -s or ls --size : Print Size of each file With blocks Formls -S : Sort by File Size, Largest First--sort=’none’ :  Sort Your File, Base On Argument Like time and size Read More Valid More Arguments are:●          ‘none’●          ‘time’●          ‘size’●          ‘extension’●          ‘version’ls -t : Sort Your File Base On Modification Time and Newest Create First.ls -X :  sort Your File Base On alphabetically.ls -1 : Print list one file per line.ls --help : display document About ls Command.ls  --version : Print Ls Command Version.ls -man : Check Your Manual Page Use -man CommandQuiz About Ls Command

* * *

Q1\. How To List Multiple Directory In Ls Command?Ans. pi@raspberrypi:~ $  ls Blog DocumentsQ2\. How To Access Hidden File Inside Directory?Ans. pi@raspberrypi:~ $ ls -aQ3\. How To Print Long listing format Of Files?Ans. pi@raspberrypi:~ $ ls -lQ4\. Print reverse order of D irectory (z to a)Ans. pi@raspberrypi:~ $ ls  -rQ5. How To Read ls Manual Page?Ans. pi@raspberrypi:~ $ man lsChapter 7mkdir Command

* * *

mkdir : mkdir Command Help To Create New directories. If D irectory Present Already in Case Don't Create New Directories and Give A Warning Message Inside Terminal.Syntax:mkdir [OPTION]... DIRECTORY...Command Options                           Descriptionmkdir -m= Mode linuxBook : -m Option Help To Assign  New Permission To File (Like in chmod)Mode Options :●           rwx : read write Execute Permission on this file●           wx : only write Execute Permission on this file●           rx : only Read Execute Permission On This File●           rw : only Read Write Permission On This Filemkdir -p or mkdir –parents : -p option Do Not Show error if File exists. Do Not Overwrite. Your Dir File and File Do Not Exist then Create New directory.mkdir -v or  mkdir –verbose : Check You Working Behind Mkdir Command and Print a message in terminal, after each created directorymkdir --help : display this help and exitmkdir –version : output mkdir Command version information.man mkdir : print mkdir manual page Information Inside Your Cmd Tool.Quiz About mkdir Command

* * *

Q1\. How To Create Multiple D irectory Use Mkdir Command ?Ans. pi@raspberrypi:~ $ mkdir linux linuxBookQ2\. Create A new Linux D irectory And Add Some read and Execute Permission?
 Ans. pi@raspberrypi:~ $ mkdir m=’rx’ LinuxQ3\. Print Mkdir Command Manual Page?Ans. pi@raspberrypi:~ $ man mkdirChapter 8rmdir Command

* * *

rmdir : rmdir Command Help To Remove Empty Directories Inside Your Laptop. You Do Not Remove FilesSyntax:mkdir [OPTION]... DIRECTORY…Command Options                           Descriptionrmdir –ignore-fail-on-non-empty : this option Help When Remove Multiple D irectory. We Do Not Understand Which File Empty Or Not. In case This Flag ignores Non-Empty File And Don't Show Directory not empty Error.rmdir   -p or rmdir  --parents : may Default rmdir Command when use Subdirectory Folder Like  rmdir a/b/c/d in Case rmdir Command Remove Only d Folder. If You Use -p or --parents Flag You Remove the entire Subdirectory.rmdir -v or mkdir –verbose : Print diagnostic Result inside terminal for every directory process.rmdir --help : display this help and exitrmdir –version : output mkdir Command version information.man rmdir : print rmdir manual page Information Inside Your Cmd Tool.Quiz About rmdir Command

* * *

Q1\. How To delete Liunx Empty Directory ?Ans. pi@raspberrypi:~ $ rmdir linuxQ2\. Recently I’m creating a Linux directory With A test.txt File. Now You Tell Me rmDir Command Working Or Not and Why?
 Ans. Not Working. Because rmdir Command Remove Only Empty DirectorQ3\. Print Mkdir Command Manual Page?Ans .  pi@raspberrypi:~ $ man mkdirChapter 9rm Command

* * *

rm :  rm command Help To remove files or directories Both.Syntax:rm [OPTION]... [FILE]...Command Options(Flag)                           Descriptionrm  -f or rm  --force : This Flag Remove All File Or Directory Without asking Prompt Permission.rm   -i :   this  Command Option Firstly Ask You Permission use Prompt To Delete File. You Give Yes, Then Delete a File.rm  -I : Ask Only One Time Permission With prompt. Then Remove All File.             rm  -r   or rm  -R , or rm --recursive : This Flag  removes directories , subdirectories , and File With their contents recursively.rm -d or rm --dir :This Flag  remove  Only empty directories
rmdir -v or mkdir –verbose :   explain what is Behind Working is done
rmdir --help : display this help and exit.
rmdir –version : output mkdir Command version information Information.
man rmdir : print rmdir manual page Information Inside Your Cmd ToolQuiz About rm Command

* * *

Q1\. Remove test.txt File Without Prompt Permission?Ans. pi@raspberrypi:~$ rm -f test.txtQ2\. How To Remove Multiple Files?Ans. pi@raspberrypi:~$ rm -f test.txt test2.txtQ3\. Remove My Subdirectory and File Also Without Prompt  Permission?Ans. pi@raspberrypi:~$ rm -r testQ4\. How To Remove an Empty Linux Directory?Ans. pi@raspberrypi:~$ rm -d LinuxChapter 10cp Command

* * *

cp : use cp Command Help To copy files and directories Inside Your Laptop.Syntax :cp [OPTION]... SOURCE... DIRECTORYCommand Options(Flag)                           Descriptioncp -i or cp --interactive : this Flag Ask You Permission With prompt before overwrite Your Filescp -R or cp -r or cp –recursive : This Flag Use For copy Your directories with All Files.rmdir -v or mkdir –verbose : Print explain message what’s being Work Done, inside terminal.rmdir --help : display this help and exit.rmdir –version : output mkdir Command version information Information.man rmdir : print rmdir manual page Information Inside Your Cmd ToolNote : Read Man Page For Cover All Information about Cp Command.Quiz About cp Command

* * *

Q.1 How To Copy Entire Javascript Directory With All File in js Directory?Ans.  pi@raspberrypi:~ $ cp -r javascript jsQ.2 How to Open cp Man Page Documents?Ans. pi@raspberrypi:~ $ man cpChapter 11wc Command

* * *

wc :  wc command provides word, and byte counts for each file.Syntax :wc [OPTION]... [FILE]...Command Options(Flag)                           Descriptionwc -c or wc –bytes : this Flag Help To print the Size Of the File In byte.wc -m or wc --chars : This Flag prints the character counts of the File.wc -l or wc --lines : print Total line counts In File.wc -L or wc –max-line-length : print the Longest Line in File.wc -w or wc --words : print Total word counts In File.wc --help : display this help and exit.wc –version : output wc Command version information Information.man wc : print wc manual page Information Inside Your Cmd ToolQuiz About wc Command

* * *

Q.1 How To Count File Lines?Ans.  pi@raspberrypi:~ $ wc -l manCommand.txtQ.2 How To Count File Words?Ans.  pi@raspberrypi:~ $ wc -w manCommand.txtQ3 Run wc Command On Multiple File?Ans. pi@raspberrypi:~ $ wc ls.txt test.txtQ.4 How To Find File Size in wc Command?​ Ans. pi@raspberrypi:~ $ wc -c ls.txtChapter 12cd Command

* * *

cd : The cd(change directory) command is used to change the current working directory in Linux.cd is not a command, it's built into your shell by default. This is necessary because your current working directory is controlled by the PWD environment variable named after the pwd or "print working directory" command.Syntax:cd [Directory]cd [-L|[-P [-e]] [-@]] [Directory]Command Options(Flag)                           Descriptioncd ~ : Goto Home Directorycd .. : Go One Folder Backcd –help : Go To Help PageQuiz About cd Command

* * *

Q.1  You are Currently in the /home/pi/Documents/Linux/Linux Book Directory, to Switch to The /home/pi/Documents directory?Ans. pi@raspberrypi:~/Documents/Linux/Linux Book $ cd ../..Q.2 You are Currently in the /home/pi/Documents/Linux/ Directory, to Switch to The  /home/pi/Documents/Linux/Linux/ Book directory?Ans.   pi@raspberrypi:~/Documents/Linux $ cd "Linux Book"Chapter 13mv Command

* * *

mv : mv Command Help move Your File One Place  To Another place and rename Your filesSyntax:mv [OPTION]... SOURCE... DIRECTORYCommand Options(Flag)                           Descriptionmv -f or mv --force :This Flag Over Writing Your All File Without asking Prompt Permission.mv -i or mv –interactive : This  Option Firstly Ask You Permission, use Prompt To Overwrite File. You Give Yes, Then Over Writing File.mv -v or mv –verbose : explain what is being Work done.mv –help : display this help Page Information and exit.mv --version : output Your version information About mv Command and exit.Quiz About mv Command

* * *

Q.1 How To Move linux.txt File Inside Linux Folder?Ans. pi@raspberrypi:~/Documents $ sudo mv linux.txt /LinuxQ.2 How To Overwrite  File With Prompt Permission?Ans. pi@raspberrypi:~/Documents $ sudo mv -i  linux.txt /LinuxChapter 14cat Command

* * *

cat : cat ( concatenate ) command allows us to create single or multiple files, view contain of file, concatenate filesSyntax:cat  [OPTION]  [FILE]...Command Options(Flag)                           Descriptioncat -A or cat --show-all : Print Everything Inside File.cat -b or cat --number-nonblank : Print Line number With File Content By default cat Command Show only Content of File. Count non-Empty Lines.cat -E or cat –show-ends : display $ Symbol at end of Each line.cat -n or cat --number : Print Line number With File Content By default cat Command Show only Content Of File. This Flag Count empty Line With it.cat --help : display this help and exitcat -- version : output cat Command version information.man cat : print cat Command manual page Information Inside Your Cmd Tool.Quiz About cat Command

* * *

Q.1 How To Print cat.txt File  Content Information Inside Cmd Tool?Ans. pi@raspberrypi:~ $ cat cat.txtQ.2 How To Open Cat Command Manual Pages Inside Cmd Tool?Ans. pi@raspberrypi:~ $ man catQ.3 How To Save Manual Page Information Inside Your Operating System?Ans. pi@raspberrypi:~ $ man cat > cat.txtChapter 15touch Command

* * *

touch : Touch Command update file timestamps and Create New Empty File.Syntax:touch [OPTION]...   FILE…Command Options(Flag)                           Descriptiontouch -a : This Flag change only the access time In Your Filetouch -c or touch --no-create : if your File Not Exit This Flag do not create any Empty file.other wish your file Exist then Change Timestamptouch -d or touch --date=”MM DD” : This Flag Help To assign Custom time and Date in Your File. Example : touch --date="Dec 19 " cat.txttouch -m : this flag changes only the modification time.touch -t “MMDDhhmm” : this flag Help To add own Time and Date On Your File.touch --time=”WORD” : this Flag Help To Set Time Using ArgumentsValid arguments for --time flag:●         ‘atime’, ‘access’, ‘use’ : equivalent to -a Flag●         ‘mtime’, ‘modify’ : equivalent to -m Flagtouch --help : display this help and exittouch  -- version : output touch Command version information.man touch : print touch Command manual page Information Inside Your Cmd Tool.Quiz About touch Command

* * *

Q.1  How To Create Empty File Use Of Touch Command?Ans. pi@raspberrypi:~ $ touch linuxBlog.txtQ.2 How To Modify Custom  Date  In File?Ans.  pi@raspberrypi:~ $ touch --date="Jan 01" linuxBlog.txtChapter 16head Command

* * *

head : head Command Print the first 10 lines of each File By Default. You Use head Command On More Then Two FileSyntax:head [OPTION]... [FILE]...Command Options(Flag)                           Descriptionhead -n : This Flag Help To print a specific Line on File Or More Than 10 Line on Each File. Example : pi@raspberrypi:~ $ head -20 cat.txthead –lines=NUM : This Flag Also Prints Specify Line Or More Than 10 Line on Each File. Example: pi@raspberrypi:~ $ head --lines=30 cat.txthead -v or head –verbose : This Flag print File Name On Top And After print headers Informationhead --help : display this help and exithead  -- version : output cat Command version information.man head : print cat Command manual page Information Inside Your Cmd Tool.Quiz About head Command

* * *

Q. 1 How Print the First 20 Lines of linux.txt File?Ans. pi@raspberrypi:~ $ head -20 cat.txtQ.2 How Print File Header Information More Than Two File?Ans. pi@raspberrypi:~ $ head cat.txt   ls.txt    mv.txtChapter 17tail Command

* * *

tail : tail Command Print the last 10 lines of each File. You Use Head Command On More Then Two FileSyntax:tail [OPTION]... [FILE]...Command Options(Flag)                           Descriptiontail -n : This Flag Help To print a specific Line on File Or More Than 10 Line on Each File. Example : pi@raspberrypi:~ $ tail -20 cat.tx ttail --bytes=NUM : This Flag Also Print On Your Files Size. Example: pi@raspberrypi:~ $ tail --bytes=300 cat.txthead -v or head –verbose : This Flags print File Name On Top And After print tail Header Information.head --help : display this help and exithead  -- version : output tail Command version information.man head : print tail Command manual page Information Inside Your Cmd Tool.Quiz About head Command

* * *

Q. 1 How Print the last 30 Lines of linux.txt File?Ans. pi@raspberrypi:~ $ tail -30 cat.txtQ.2 How Print File Header Information More Than Two File?Ans. pi@raspberrypi:~ $ tail cat.txt   ls.txt    mv.txtChapter 18Find Command

* * *

find : Find Command Help To search files in a Directory Hierarchy.Syntax:find [Directory] [Option] [Expression]Command Options(Flag)                           Descriptionfind -name : This Flag Help To Find File By Name.find -size : find files based on the file size, pass the -siz e parameter along with the size criteria. You can use the following suffixes to specify the file size:●          b : 512-byte blocks (default)●          c : bytes●          w : two-byte words●          k : Kilobytes●          M : Megabytes●          G : Gigabytesfind -atime n : this Flug Show last accessed File Example:pi@raspberrypi:~ $ find . -atime 1find -cmin n : this Flag shows File's status which changed at the last minute.find -ctime n : this flog show you status which changed in 24 hours agon mean : Numeric arguments can be specified:●          +n: for greater than n●          -n: for less than n●          n: for exactly nfind -help or find --help : this flag Print a summary of the command-line usage of find and exit.man find : this Command Help You To Print Manual page Information.Note : Find Command Provide You Lots Of Flag Or Option.we Discuss Only 7 flags.Plz Read Manual Page For More Command.Quiz About find Command

* * *

Q.1 How To Find All Txt File Inside My root Directory?Ans. pi@raspberrypi:~ $ sudo find . -name '*.txt'Q.2 How To Find Specific cat.txt  File In A directoryAns. pi@raspberrypi:~ $ sudo find . -name cat.txtChapter 19echo Command

* * *

echo : ech o command is used to display lines of text/string that are passed as an argument.Syntax:echo [SHORT-OPTION]... [STRING]...Command Options(Flags)                           Descriptionecho -n : this flag does not output a newline.echo -e : This Help to enable interpretation of backslash escapes-e: flag Provide Some More Option For You:●         \\ : Add backslash In Your String.●         \b : Remove Space In Your String.●         \n : add new line●         \t : Add New horizontal tab with backspace.●         \v : Add New vertical tabecho -E: disable the interpretation of backslash escapes (default)echo --help :  display this help and exitecho --version : output version information and exitman echo : this Command Help You To Print Manual page Information.Quiz About echo Command

* * *

Q.1 How To Enable interpretation of backslash escapes?Ans. pi@raspberrypi:~ $ echo -e "My \nName \\Is \t Rajdeep Singh"Q2\. How To Disable i nterpretation of backslash escapes?Ans. pi@raspberrypi:~ $ echo -E "My \nName \\Is \t Rajdeep Singh"Chapter 20Process Command

* * *

pidof : pidof Command Help to find the process ID of Your Currently Running Program.Syntax:pidof [programName...]

* * *

ps : ps command tells you a snapshot of the current working processes.Syntax:ps [options]Command Options(Flags)                           Descriptionps -ux : this Flag Tell you all working processes in your laptop.ps -e : this flag tells you a small description or list of the current working process.

* * *

top: the top command will display a list of running processes and how much CPU each process uses.   It provides a dynamic real-time view of the running system.Syntax:top [OPTIONS]Note: All Process Command Provide Own Options Or Flags. Plz Read Manual Page use the man Command.Chapter 21Kill Command

* * *

Kill: Some Time Our program is unresponsive, you can terminate your process manually by using the kill command.Syntax:kill [options] [pid...]Command Options(Flags)                           DescriptionKill [pid] : this flag kill specify or list of Process. Example:  pi@raspberrypi:~ $  kill 2345Kill -9 -1 : this flag Kill All processes currently Working on a laptop or pc.Kill -9 : this flag helps when your process does not terminate by the kill command. use -9 flags you kill the process very easily.kill -Kill : this flag works the same as kill -9 flag.Quiz About Kill Command

* * *

Q.1 How To Kill Multiple Processes By Kill Command?Ans. pi@raspberrypi:~ $  kill 2326 2349Q.2 How To Kill All Processes Currently Running On My Laptop?Ans. pi@raspberrypi:~ $ kill -9 -1Chapter 22date Command

* * *

Date: the date Command print system date and time.Syntex:date [OPTION]... [FORMAT]...Command Options(Flags)                           Descriptiondate -r or date --reference=FILE : This Flag Help To show Last modification time of FILEdate -s or date --set=STRING : this Flag Help To Set Custom or change system Date in your laptop or pcdate -u or date --utc or date --universal : this flag print Coordinated Universal Time (UTC)date --help : display this help and exitdate --version : output version information and exitman date : this Command Help You To Print Manual page Information.Format Options:--●        +%a : print weekday name (e.g., Sun)●        +%A : Print locale's full weekday name (e.g., Sunday)●        +%b : Print locale's Shot month name (e.g., Jan)●        +%B : Print locale's full month name (e.g., January)●        +%c : print locale's date and time (e.g., Thu Mar 3 23:05:25 2005)●        +%C : Print Year With the Last Two-Digit (e.g., 20)●        +%d : print day of the month (e.g., 01)●        +%D : a print date with the same format as %m/%d/%y●        +%e : print date ((e.g. 1-31)●        +%F : print full date same as %Y-%m-%d●        +%g : last two digits of the year of ISO week number (see %G)●        +%G : year of ISO week number (see %V); normally useful only with %V●        +%h : same as %b●        +%H : hour (00..23)●        +%I : hour (01..12)●        +%j : day of the year (001..366)●        +%m : month (01..12)●        +%M : minute (00..59)●        +%n : add a newline●        +%N : Print nanoseconds (000000000..999999999)●        +%p : Print locale's equivalent of either AM or PM; blank if not known●        +%P : like %p, but lower case●        +%r : locale's 12-hour clock time (e.g., 11:11:04 PM)●        +%R : 24-hour hour and minute; same as %H:%M●        +%s : seconds since 1970-01-01 00:00:00 UTC●        +%S : second (00..60)●        +%t : print a tab●        +%T : print time same as %H:%M:%S●        +%u : day of the week (1..7); 1 is Monday●       +%U : week number of year, with Sunday as the first day of the week (00..53)●       +%V: ISO week number, with Monday as the first day of the week (01..53)●        +%w : day of the week (0..6); 0 is Sunday.●       +%W : week number of year, with Monday as the first day of the week (00..53)●        +%x : locale's date representation (e.g., 12/31/99)●        +%X : locale's time representation (e.g., 23:13:48)●        +%y : last two digits of the year (00..99)●        +%Y : Print Full year●        +%Z : alphabetic time zone abbreviation (e.g., EDT)Quiz About date Command

* * *

Q.1 How Set Custom Date use date Command?Ans. pi@raspberrypi:~ $ sudo date -s "12/17/2020 05:26:00"Q.2 How To Print Full Date And Time With PM/AM  use Formats?Ans. pi@raspberrypi:~ $ date '+%A %D %r'Chapter 23calendar Command

* * *

cal : cal command shows a quick view of the calendar in the Linux terminal. By default, the cal command shows the current month calendar as output.Syntax:cal [ [ month ] year]cal [Options] [ [ month ] year]

* * *

ncal : ncal Command Same Work Like cal Command.Syntax:ncal [ [ month ] year]ncal [Options] [ [ month ] year]Chapter 24tar Command

* * *

tar : The Linux tar Command stands for tape archive, is used to create Archive and extract the archive files.Syntaxtar [options] [archive-file] [file or directory to be archived]Command Options(Flags)                           Descriptiontar -c : this flag used to Creates a new archivetar -x :   this flag use for Extracts the archivetar -f : this flag used to creates a new archive with a given filenametar -t :   this flag gives your lists files in the archived filetar -u : this flag archives and adds to an existing archive filetar -v : Displays verbose information.tar -A : this flag helps to concatenate the archive files.tar -z : this flag compresses the tar file using gzip.tar -j : this flag also compresses the tar file using bzip2.tar -W : Verifies an archive file.tar -r : updates or add file or directory in already existing .tar file.tar --hel p : This Flag Provides you a list and a short description of the command.tar --usage : give a short usage message.tar --version : print program version.man tar : print manual pages information on your  terminal.Quiz About tar Command

* * *

Q.1 How To Convert My Linux Folder to a Zip Archive?Ans. pi@raspberrypi:~ $ tar -cvf linux.zip LinuxQ.2 Which Flag Use To Add a Custom Name on tar Command?Ans. -f flag use add Custom Name Inside Tar CommandChapter 25groups Command

* * *

groups : the groups command prints the name of groups and shows the associate user of this group.Syntax:groups [OPTION]... [USERNAME]...Command Options(Flags)                           Descriptiongroups --help : display this help and exitgroups --version : output version information and exitChapter 26groupadd Command

* * *

groupadd : groupadd command is used to create a new user group.Syntax:groupadd [option] group_nameCommand Options(Flags)                           Descriptiongroupadd -f or groupadd --force : This option causes the command to simply exit with success status if the specified group already exists. When used with -g, and the specified GID already exists, another (unique) GID is chosen (i.e. -g is turned off).groupadd -r or groupadd --system : C reate a system group. The numeric identifiers of new system groups are chosen in the SYS_GID_MIN-SYS_GID_MAX range, defined in login. defs, instead of GID_MIN and GID_MAX .groupadd -g or groupadd --gid : This option is used to provide a group id (numeric) to the new group, and it should be non-negative and unique unless explicitly created to be non-unique (using -o option). If this option is not used, the default id is assigned, which is greater than every other group already present.groupadd -h or groupadd --help : Display help message and exit.groupadd -K or groupadd --key : Overrides /etc/login. defs defaults (GID_MIN, GID_MAX, and others). Multiple -K options can be specified. GID_MIN and GID_MAX are the parameters set in /etc/login. efs which defines the minimum and maximum values that a group id can take.groupadd -o or groupadd --non-unique : This option permits to add a group with a non-unique GID.groupadd -p or groupadd --password : The encrypted password, as returned by crypt. The default is to disable the password.Chapter 27groupdel Command

* * *

groupdel : you Create a new group using the groupadd command. If a group is no longer needed and can be removed from the system.groupdel command is used to delete an existing group. It will delete all entry and file, that refers to the groupSyntax :groupdel [OPTIONS] groupNameCommand Options(Flags)                           Descriptiongroupdel -h or groupdel --help : Display help message and exit.groupdel -R or groupdel --root CHROOT_DIR : Apply changes in the CHROOT_DIR directory and use the configuration files from the CHROOT_DIR directory.man groupdel : this Command Help You To Print Manual page Information.Chapter 28group Command

* * *

group : Group Command Tell You Where Is group file Located in my laptop or pc. This Working With Man Command.Note :Group Command Not Official Command. Simple paste group Command in your terminal you see nothing with the man command your read group manual page.Syntax:man groupChapter 29users Command

* * *

useradd : To add/create a new user, you use the useradd or adduser command in your system.Make sure your username must be unique and different from other usernames that already exist on the system.Syntax:useradd [options] Name_Of_The_User

* * *

userdel : userdel command in the Linux system is used to delete a user account and related files.Syntax:userdel [OPTIONS] UserNameCommand Options(Flags)                           Descriptionuserdel -r or userdel --remove : Use the -r flag to force userdel to remove the user’s home directory also.userdel -h or userdel --help : Display help message and exit.userdel -f or userdel --force : This option forces the removal of the user account, even if the user is still logged in. It also forces userdel to remove the user's home directory and mail spool, even if another user uses the same home directory or if the mail spool is not owned by the specified user.Chapter 30sudo Command

* * *

sudo: The sudo ( S uper U ser DO ) command allows you to run programs with the security privileges of another user, by default the root user. sudo is one of the commands that you will use quite frequently.Syntax:sudo [OPTION] [COMMAND]Command Options(Flags)                           Descriptionsudo -V or sudo --version : The option prints the Sudo command version.sudo -l : The -l option will print out the commands allowed Commands List.sudo -h or sudo --help : The -h (help) option prints a short help message and exit.sudo -v : If, given the -v (validate) option, sudo will update the user’s timestamp, prompting for the user’s password if necessary. This extends the sudo timeout for another 5 minutes (or as given in sudoers) but does not run a command. This does not give any output.sudo -k : The -k (kill) option to sudo invalidates the user’s timestamp. So, the next time sudo is run a password will be required. This option does not require a password and was added to allow a user to revoke sudo permissions from a logout file.sudo -K : Similar to the -k option, the -K (sure kill) option is used to remove the user’s timestamp entirely. Likewise, this option does not require a password.sudo -b : The -b (background) option tells Run the given command in the background. Note that it is not possible to use shell job control to manipulate background processes started by sudo. Most interactive commands will fail to work properly in background modesudo -p : The -p (prompt) option allows you to override the default password prompt and use a custom one.Chapter 31apt-get Command

* * *

apt-get : apt-get is the command-line tool for handling packages inside the Debian Linux system. Debian uses the dpkg packaging system. A packaging system is a way to provide programs and applications for installation.APT (Advanced Package Tool) is the command-line tool to interact with this packaging system. you can use it to find and install new packages, upgrade packages, clean your packages, etc.Syntax :Sudo apt-get [options] commandCommand ​ ​                          Descriptionupdate : update Comand Use To Update Own Package in Your Laptop.update Command is a resynchronize the package index files from their sources. The indexes of available packages are fetched from the location(s) specified in /etc/apt/sources.list.update : This command helps update your own package inside your laptop or pc.upgrade : This command is used to install the latest versions of the packages currently installed on the user’s system.install : install Command is followed by one or more packages desired for installation or upgrading in Your System. Each package is an Install By package name inside your system.remove : this command similar to Install Command But mainly difference being that it removes the packages instead of installing them. It does not remove any configuration files created by the package .parge : This command removes the packages, and also removes any configuration files related to the packages.check : This command is used to update the package cache and checks for broken dependenciesdownload : This command is used to download the given binary package in the current directory.autoremov e: Sometimes the packages which are automatically installed to satisfy the dependencies of other packages, are no longer needed. The autoremov e command is used to remove these kinds of packages.Command Options(Flags)                           Descriptionapt-get -q or apt-get  --quiet : When this option is specified, apt-get produces an output that is suitable for logging.apt-get  -V or apt-get  --verbose-versions : Show full versions for upgraded and installed packages.apt-get  --reinstall : Re-install packages that are already installed and at the newest version.apt-get  -h or apt-get --help : this Command Show a short usage summary.apt-get -v or apt-get  --version : This Command Show the program version in Your CMD.Note. We Cover Few Command Or Option Plz Read Manual Page For More Update.Chapter 32grep Command

* * *

grep : grep Command is a Linux based command-line tool used to search for a string and patterns of characters in a specified file.Syntax:grep [OPTION...] PATTERNS [FILE...]Command Generic Program                              Descriptiongrep --help : Output a usage message and exit.grep -V or grep --version : Output the version number of grep and exit.Command Matcher Selection                             Descriptiongrep -i or grep --ignore-case : this flag Help To Match Word Case sensitive And Case Insensitive Also.grep -c : This prints only a count of the lines that match a patterngrep -h : Display the matched lines, but do not display the filenames.grep -i or grep --ignore-case : this flag Help To Match Word Case sensitive And Case Insensitive Also.grep -l : Displays a list of filenames only.grep -n : Display the matched lines and their line numbers.grep -v : This prints out all the lines that do not matches the patterngrep -e exp : Specifies expression with this option. Can use multiple times.grep -f file : Takes patterns from a file, one per line.grep -E : Treats pattern as an extended regular expression (ERE)grep -w : Match whole wordgrep -o : Print only the matched parts of a matching line, with each such part on a separate output line.Note: Read All Option Go To Read Manual Page.Chapter 33chmod Command

* * *

Chmod : We can use the chmod command which stands for 'change mode'. Using the command, we can set permissions (read, write, execute) on a file/directory.Syntax:chmod [Option]... [Permissions] fileNameThe three digits define permissions for the file user, group, and others.r: Permission to read the file.w: Permission to write (or delete) the file.x: Permission to execute the filePermission Example:    ●         Read, write and execute rwx 111●         Read and write rw- 110●         read and execute r-x 101●         Read-only r-- 100●         Write and execute -wx 011●         Write only -w- 010●         Execute only --x 001●         None --- 000Command Options(Flags)                           Descriptionchmod -R or chmod --recursive :  change files and directories recursivelychmod  --help :  display this help and exitchmod  --version :    output version information and exitman chmod : this flags use for Read Manual Pages