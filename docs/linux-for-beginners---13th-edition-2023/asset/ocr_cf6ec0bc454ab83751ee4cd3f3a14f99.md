# More Fun Things to do in the Terminal

+   **STEP 5** Stringing several commands and piping them through other commands is what makes scripting such a powerful element to an OS. Using the while command, for example, together with toilet, can yield some impressive results. Enter: `while true; do echo "$date '+%D %T' | toilet -f term -f border --metal);"; sleep 1; done.`

+   **STEP 8** Used as a music demo from the old Amiga and DOS days, the **bb** command reminds us of getting hold of three and a half floppies crammed with all manner of demoscene goodies. We've already installed bb from the previous step, so just enter `bb`. Follow the on-screen instructions, and turn up your volume.

![](bbox=[0.07, 0.18, 0.47, 0.37])

![](bbox=[0.53, 0.2, 0.92, 0.36])

+   **STEP 6** Talking computers were the craze of the 80s, enter: `speak "Hello, this is Linux Mint"` to have the computer repeat the text inside the quotes to you. Make sure your volume is turned up, and try the following: `ls > folders.txt && speak -f folders.txt`. This will have Mint read back the contents of the ls command.

+   **STEP 9** This entry is in two parts. First you need to get hold of the necessary packages: `sudo apt-get install liburses-perl`. When that's done enter: `cd Downloads/ && wget http://search.cpan.org/CPAN/authors/id/K/KB/KBAUCOM/Term-Animation-2.4.tar.gz && tar -xf Term-Animation-2.4.tar.gz && cd Term-Animation-2.4/`. Then: `perl Makefile.PL && make && make test && sudo make install`.

![](bbox=[0.07, 0.46, 0.47, 0.65])

![](bbox=[0.53, 0.49, 0.92, 0.64])

+   **STEP 7** A roaring ASCII fire isn't the most useful command to have at your disposal, but it's fun. Install it with: `sudo apt-get install libaa-bin`, then when installed use: `aafire`. It's not exactly warming but you get the idea. To expand the above, enter: `sudo apt-get install bb caca-utils,` then, `cacfire`.

+   **STEP 10** With that little lot done, onto the next. Enter: `cd .. && wget http://www.robo bunny.com/projects/asciiquarium/asciiquarium.tar.gz && tar -xf asciiquarium.tar.gz && cd asciiquarium_1.1/ && chmod +x asciiquarium`. Providing all went well, enter `./asciiquarium` and enjoy your very own ASCII-based aquarium.

![](bbox=[0.07, 0.74, 0.47, 0.94])

![](bbox=[0.53, 0.75, 0.92, 0.93])