# 01 Get Pygame dependencies

The best way to install Pygame for your system is to compile it. To do this you need to first install the right dependencies. Open up the terminal and install the following packages, which in Ubuntu looks like:

```
$ sudo apt-get install mercurial python-dev python-numpy libav-tools libsdl-image1.2-dev libsdl-mixer1.2-dev libsdl-ttf2.0-dev libsmpeg-dev libsdl1.2-dev libportmidi-dev libswscale-dev libavformat-dev libavcodec-dev
```

![](bbox=[0.07, 0.32, 0.31, 0.52])

# 02 Get the Pygame code

Next we need to download the code for Pygame direct from the source. Still in the terminal, you can do this by typing in:

```
$ hg clone https://bitbucket.org/pygame/pygame
```

Which will download it to the folder 'pygame'. Move to that using CD pygame in the terminal so we can continue building it.

![](bbox=[0.07, 0.79, 0.66, 0.92])

# 03 Build the Pygame module

To install it, we need to do it in two steps. First we need to prepare the code to install using the terminal with:

```
$ python setup.py build
```

Once that's finished you can then actually install it with:

```
$ sudo python setup.py install
```

This won't take too long.

![](bbox=[0.34, 0.12, 0.89, 0.46])

# 04 Install in other ways

If the above doesn't work (or is a bit daunting) you can check the website for binary and executable files that will work on other operating systems and Linux distros. Head to http://pygame.org/download.shtml to get the files you need for your specific system, including Windows and OS X. The rest of the tutorial will work in any OS.

# 05 Get the visual novel files

We've uploaded the code to FileSilo, and here we're going to walk you through what we've done to make it work. Download the files for the visual novel and unzip them. The two files we care about for the moment are the visualnovel.py and script.py python files – this is where all the important code is.

![](bbox=[0.64, 0.75, 0.88, 0.84])

# 06 Understand the script file

For the moment the script file is small and literally just holds the script for the game. It's made up of events for the visual novel to move between, line by line, by splitting it up into scenes. This includes the location of each line, the character, the actual line itself and information on how the game flows. These are matrices with the information in, and are completely customisable.