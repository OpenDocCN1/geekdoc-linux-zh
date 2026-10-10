STEP 5
Stringing several commands and piping them through can be what makes scripting such a powerful element to an OS. Using the while command, for example, together with toilet, can yield some impressive results. Enter:
while true; do echo "$(date '+%d %T')" | toilet -f term; -F border -:-metal); sleep 1; done.

![](bbox=[0.05, 0.23, 0.47, 0.38])

STEP 8
Used as a music demo from the old Amiga and DOS days, the bb command reminds us of getting hold of three and a half inch floppies crammed with all manner of dosmode goodies. We've already installed bb from the previous step, so just enter bb. Follow the on-screen instructions, and turn up your volume.

![](bbox=[0.52, 0.23, 0.95, 0.38])

STEP 6
Talking computers were the craze of the 80s, enter: speak "Hello, this is Linux Mint" to have the computer repeat the text inside the quotes to you. Make sure your volume is turned up and try the following: ls > folders.txt && speak -f folders.txt. This will have Mint read back the contents of the ls command.

![](bbox=[0.05, 0.5, 0.47, 0.65])

STEP 9
This entry is in two parts. First you need to get hold of the necessary packages: sudo apt-get install libcurses-perl. When that's done enter: cd Downloads/ && wget http://search.cpan.org/CPAN/authors/id/K/KB/KBALCOM/Term-Animation-2.4.tar.gz && tar -xf Term-Animation-2.4.tar.gz && cd Term-Animation-2.4/. Then: perl Makefile.PL && make && make test && sudo make install.

![](bbox=[0.52, 0.51, 0.95, 0.66])

STEP 7
A roaring ASCII fire isn't the most useful command to have at your disposal, but it's fun. Install it with: sudo apt-get install libaa-bin, then when installed use: aafire. It's not exactly warming but you get the idea. To expand the above, enter: sudo apt-get install bb caca-utils, then, caca-fire.

![](bbox=[0.05, 0.79, 0.47, 0.94])

STEP 10
With that little lot done, onto the next: Enter cd . . && wget http://www.rorobunny.com/projects/asciiarium/asciiarium.tar.gz && tar -xf asciiarium.tar.gz && cd asciiarium-1.1/ && chmod +x asciiarium. Providing all went well, enter ./asciiarium and enjoy your very own ASCII-based aquarium.

![](bbox=[0.52, 0.79, 0.95, 0.94])