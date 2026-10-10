
# More Fun Things to do in the Terminal

If the previous list of fun, and quite bizarre, things to do in the Terminal has you wanting more, you're in luck. We've put together another batch of some useful, and some not so useful, commands for you to try out.

## MORE FUN, YAY

Since the Terminal session is already open, and your keyboard digits are nicely warmed up, here are another two pages of Terminal nonsense.

- **STEP 1** Remember the old ZX Spectrum days of computing, when you could type in `10 print "Hello", 20 goto 10` and Hello would list down the screen? Well, in Linux Mint you can do the same. Simply `more` yes followed by some text, i.e. `yes Linux ts ace`. It'll keep going until you press `Ctrl+C`.

![](img/5019375da05cbf0090115165d80772a1_61_0.png)

- **STEP 2** The Matrix was one of the most graphically copied films ever released; there's even a version of the Matrix code available for Linux Mint. Install it with: `sudo apt-get install cmatrix`. When it's done enter: `cmatrix` and follow the white rabbit. Neo. Unlike the real Matrix though, you can press `Ctrl+C` to exit.

![](img/5019375da05cbf0090115165d80772a1_61_2.png)

- **STEP 3** Having a little white cat chase your mouse pointer around the desktop may sound like a terrible waste of time. Oddly though, it isn't. Enter: `sudo apt-get install oneko`, then type `oneko` to have the cat appear. Move your 'mouse' cursor around the screen and the cat will chase it. Use `Ctrl+C` to exit the action.

![](img/5019375da05cbf0090115165d80772a1_61_1.png)

- **STEP 4** This entry is a little more serious than the previous. It's called the **Fork Bomb** and what it does, basically, is continually replicate itself until it has used up all the available system resources, thus causing your computer to crash. You don't have to try it but it's interesting nonetheless. Simply enter: `:(){ :|:& };:`; and be prepared to reboot.

![](img/5019375da05cbf0090115165d80772a1_61_3.png)

- **STEP 5** Stringing several commands and piping them through can be what makes scripting such a powerful element to an OS. Using the `while` command, for example, together with `toilet`, can yield some impressive results. Enter:
  ```bash
  while true; do echo "$(date '+%d %T')" | toilet -f term -F border -f metal; sleep 1; done
  ```

![](img/5019375da05cbf0090115165d80772a1_62_0.png)

- **STEP 6** Talking computers were the craze of the 80s, enter: `speak "Hello, this is Linux Mint"` to have the computer repeat the text inside the quotes to you. Make sure your volume is turned up and try the following: `ls > folders.txt && speak -f folders.txt`. This will have Mint read back the contents of the `ls` command.

![](img/5019375da05cbf0090115165d80772a1_62_2.png)

- **STEP 7** A roaring ASCII fire isn't the most useful command to have at your disposal, but it's fun. Install it with: `sudo apt-get install libaa-bin`, then when installed use: `aafire`. It's not exactly warming but you get the idea. To expand the above, enter: `sudo apt-get install bb caca-utils`, then, `caca-fire`.

![](img/5019375da05cbf0090115165d80772a1_62_4.png)

- **STEP 8** Used as a music demo from the old Amiga and DOS days, the `bb` command reminds us of getting hold of three and a half inch floppies crammed with all manner of dosmode goodies. We've already installed `bb` from the previous step, so just enter `bb`. Follow the on-screen instructions, and turn up your volume.

![](img/5019375da05cbf0090115165d80772a1_62_1.png)

- **STEP 9** This entry is in two parts. First you need to get hold of the necessary packages: `sudo apt-get install libcurses-perl`. When that's done enter:
  ```bash
  cd Downloads/ && wget http://search.cpan.org/CPAN/authors/id/K/KB/KBALCOM/Term-Animation-2.4.tar.gz && tar -xf Term-Animation-2.4.tar.gz && cd Term-Animation-2.4/
  ```
  Then:
  ```bash
  perl Makefile.PL && make && make test && sudo make install
  ```

![](img/5019375da05cbf0090115165d80772a1_62_3.png)

- **STEP 10** With that little lot done, onto the next:
  ```bash
  cd ~ && wget http://www.rorobunny.com/projects/asciiarium/asciiarium.tar.gz && tar -xf asciiarium.tar.gz && cd asciiarium-1.1/ && chmod +x asciiarium
  ```
  Providing all went well, enter `./asciiarium` and enjoy your very own ASCII-based aquarium.

![](img/5019375da05cbf0090115165d80772a1_62_5.png)

# Linux Tips and Tricks

As you've seen, the Linux Terminal is quite an exceptional environment. With a few extra apps installed, and a smidgen of command knowledge, incredible, and often quite strange, things can be accomplished.

## TAKING COMMAND

There are countless Linux tips, secrets, hacks and tricks out there. Some are very old, originating from Linux's Unix heritage, while others are recent additions to Linux lore. Here's our favourite ten tips and tricks.

### EASTER EGGS

Emacs, the text editor, is a great piece of software; however, did you know it also contains a hidden Easter Egg? With Emacs installed (`sudo apt-get install emacs25`), drop to a Terminal session and enter:

```bash
emacs --batch -l dunnet
```

Dunnet is a text adventure written by Ron Schell in 1982, and hidden in Emacs since 1994.

![](img/5019375da05cbf0090115165d80772a1_63_0.png)

### TERMINAL BROWSING

Ever fancied being able to browse the Internet from the Terminal? While not particularly useful, it is quite a fascinating thing to behold. To do so, enter:

```bash
sudo apt-get install elinks
```

Enter the website you want to visit.

![](img/5019375da05cbf0090115165d80772a1_63_1.png)

### MOON BUGGY

Based on the classic 1982 arcade game, Moon Patrol, Moon Buggy appeared on the home computers of 1985 amid much praise. It's a cracking Atari game, and it's available in the Linux Terminal by entering:

```bash
sudo apt-get install moon-buggy
```

Then:

```bash
moon-buggy
```

Enjoy.

![](img/5019375da05cbf0090115165d80772a1_63_2.png)

### LET IT SNOW

Snowing in the Terminal console isn't something you come across every day. If you're interested, however, enter:

```bash
wget https://gist.githubusercontent.com/sentek/1505483/raw/7d024716e057e69fb52632fee09f42753631c4d2/snowjob.sh
chmod +x snowjob.sh
./snowjob.sh
```

![](img/5019375da05cbf0090115165d80772a1_63_3.png)

### MEMORY HOGS

If you need to see what apps are consuming the most memory on Linux, simply enter:

```bash
ps aux | sort -rnk 4
```

This sorts the output by system memory use.

![](img/5019375da05cbf0090115165d80772a1_64_0.png)

### BBS

Back in the days of dial-up connections, the online world was made up of Bulletin Board Systems. These remote servers provided hang-outs for users to chat, swap code, play games and more. Using `telnet` in Linux, we can still connect to some active BBSes:

```bash
telnet battlebbs.tarballs.dynnds.org
```

There are countless operable BBSes available, check out https://www.telnetbbsguide.com/bbslist/detail/, for more.

![](img/5019375da05cbf0090115165d80772a1_64_1.png)

### SHREDDER

When you delete a file, there’s a chance of someone with the right software being able to retrieve it. However, to securely and permanently delete a file, use Shred:

```bash
shred -zvu NAMEOFFILE.txt
```

Replace `NAMEOFFILE` with the name of the file to delete.

![](img/5019375da05cbf0090115165d80772a1_64_2.png)

### DIRECTORY TREES

If you want to create an entire directory (or folder) tree with a single command, you can use:

```bash
mkdir -p New-Dir/{subfolder1,subfolder2,subfolder3,subfolder4}
```

This creates a `New-Dir` with four sub folders within.

![](img/5019375da05cbf0090115165d80772a1_64_3.png)

### ASCII ART

ASCII art can be quite striking when applied to some images. However, it’s often difficult to get just right. You can create some great ASCII art from the images you have by using `img2txt`:

```bash
img2txt NAMEOFIMAGEFILE.png
```

Replace `NAMEOFIMAGEFILE` with the actual name of the image file on your system. If `img2txt` is not installed, use:

```bash
sudo apt-get install caca-utils
```

![](img/5019375da05cbf0090115165d80772a1_64_4.png)

### FORGOTTEN COMMANDS

It’s not easy trying to remember all the available Linux commands. Thankfully, we can use `apropos` to help us. Simply use it, along with a description of the command:

```bash
apropos "copy files"
apropos "rename files"
```

![](img/5019375da05cbf0090115165d80772a1_64_5.png)
