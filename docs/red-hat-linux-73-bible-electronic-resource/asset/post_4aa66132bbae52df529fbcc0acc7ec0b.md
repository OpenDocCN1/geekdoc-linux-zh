
The first time you run LinCity, it asks if it can create a directory in which to save your games. Yes is a good answer to that. Then, when the LinCity window opens, the game helps you get started by letting you load a built-in scene or begin with a random village.

Here are some tips for playing LinCity:

- Right-click a button to see a description of an item before you add it to your community.
- Use the Tips button to create a place to put your trash. If you accumulate too much trash, you may need to burn it (which causes pollution). When the trash area fills up, it gets covered in grass.
- Build monuments to improve unemployment temporarily, add inspiration to a community, and increase the community’s technological capability.
- While a mill can produce goods, be careful because the people who run the mill also consume a lot of food.
- Either import or have farms for producing food. If you run out of food, people will either die or move away.

Figure 7-4 shows an example of a LinCity community in action.

![](img/1744bde8c889adfab3fc911e1687fecf_289_0.png)

# Xgalaga

Xgalaga is your basic Space Invaders-type game. You fire back at alien spaceships as they attack you. Select either keyboard (arrows to move and Spacebar to shoot) or mouse controls (move with mouse, shoot with right-click). Then just move and shoot. There’s not much else to it, but it’s fun if your brain needs to rest for a while. To start Xgalaga, type the following:

```
$ xgalaga
```

You need to install the xgalaga software package. You can find the xgalaga package using the `rpmfind` command. It puts the executable in the `/usr/X11R6/bin` directory. Figure 7-5 shows the Xgalaga window. Your level and score appear at the top.

![](img/1744bde8c889adfab3fc911e1687fecf_290_0.png)

Figure 7-5: Destroy enemy spaceships in Xgalaga.

# Maelstrom

In Maelstrom (Figure 7-6), you maneuver your spaceship to dodge asteroids, then use your shield and plasma cannons to destroy them. Besides asteroids, you need to look out for stars that go nova, Shenobi autonomous mines, vortexes, and Shenobi fleet ships.

Start Maelstrom from the Gnome menu (Programs $\rightarrow$ Games $\rightarrow$ Maelstrom). Then click the P button to start the game, or click the C button to change the keyboard controls for the game. The following table shows the keyboard controls assigned by default and the key each is assigned to:

| Action | Key |
|---|---|
| Fire | Tab |
| Thrust | Up Arrow |
| Shield | Spacebar |
| Turn clockwise | Right arrow |
| Turn counterclockwise | Left Arrow |
| Pause | Pause |
| Abort game | Esc |

![](img/1744bde8c889adfab3fc911e1687fecf_291_0.png)

Figure 7-6: Avoid and destroy asteroids in Maelstrom.

## Character-Based Games

There aren’t many character-based games delivered with the basic Red Hat Linux installation. If you are interested in trying some of the legacy UNIX games, some of which were created many years ago, you can install the *bsd-games* package (which is available from Red Hat FTP sites).

The games that come in the *bsd-games* package include simple card games, shooting games, and adventure games. As previously noted, games are stored in the /usr/games directory by default, so you may want to add that directory to your *PATH*.

Some of the games have score files, which should be created as writable by everyone (if multiple people use your system). Or you can make those games that write to score files into setgid games, and then make the file permissions 664. The owner and group of each game command is root by default. Only one game (Hunt) allows multiple players and has a daemon program (in /usr/sbin) for coordinating game play.

> **CROSS-REFERENCE:** See Chapter 3 for information on adding a directory to your PATH and setting file permissions.

If you want to control who runs these games and when the games are run, you can use the dm command (Dungeon Master) for controlling access to games. You can add controlled games into a hidden directory (/usr/games/.dm), then create a configuration file (/etc/dm.conf) to determine when each controlled game can be run.

Table 7-3 lists all of the games available in the bsd-games package. For a simple game, try Fish (/usr/games/fish). If you are adventurous, try Adventure (/usr/games/adventure). Here are a few hints that will help you with Adventure:

- Move around the caves in Adventure by asking for an adjacent room or by naming a direction (N, S, E, SW, NE, etc.).
- As you explore the caves, draw a map as you go — it helps you return to places later.
- Take valuable things and bring them back to the building.
- Typing xyzzy and plugh sometimes transports you to a remote location.

### Table 7-3: Games in the bsd-games Package

| Game | Description | Game | Description |
| --- | --- | --- | --- |
| adventure | Explore the Colossal caves and find treasures. | arithmetic | Answer simple, timed arithmetic questions. |
| atc | Air traffic controller game. Direct jets and propeller planes through flight area and airports. | backgammon | Backgammon board game. |
| Banner | Print large-letter banners on your printer. | battlestar | A tropical adventure game. |
| canfield | The canfield solitaire game. | cribbage | The cribbage board game. |
| dm | Dungeon master to regulate game playing. | factor | Factor numbers. |

### Table 7-3 (Continued)

| Game | Description | Game | Description |
|---|---|---|---|
| fish | The go fish card game. | gomoku | Two-player game to get five in a row. |
| hunt | Multiplayer maze game with the object of killing the other players. | mille | The Mille Bornes game. |
| monop | The Monopoly game for multiple players. | number | Converts arabic numbers to words. |
| phantasia | Role playing fantasy game for fighting monsters. | pig | Reformat input as pig latin. |
| pom | Displays the current phase of the moon. | primes | Generate prime numbers. |
| quiz | Answer questions on selected topics. | rain | Displays animated raindrops. |
| random | Generate random numbers. | robots | Fight evil robots. |
| sail | Multiuser fighting ships game. | snake | Avoid getting eaten by a snake. |
| tetris-bsd | Tetris game. | trek | Trekkie space game. |
| wargames | No thermonuclear warfare. Not dangerous. | worm | A growing worm game. |
| worms | Animated worms. | wump | Shoot at the wumpus in an underground cave. |

# The xmame Gaming Emulator

Creators of gaming emulators set out to take games that were designed for home gaming consoles or arcades and have those games run on a computer. As a result, games that were created for gaming machines that are now outdated or broken can be resurrected on your home computer.

A compilation of gaming emulators has been put together into one project called Multiple Arcade Machine Emulator (MAME). Nicola Salmoria started the MAME project in January 1997. There are now more than 100 contributors. An X Window System version of MAME called xname runs in Red Hat Linux. There are also several other versions that run in different video modes, allowing the use of 3Dfx, SVGALIB, and other video technologies.

No games are delivered with the xname package. Games that can be used with the xname package are listed in a file that comes with xname. That file lists more than 600 games that are supported by xname. (Up to 2000 games have been listed as compatible with MAME on other computing platforms — in particular, old Windows 3.1/95 platforms.)

You can download the most recent version of xname from links at the X-MAME home page at http://x.mame.net. (the RPMS from there that I tried worked well, after some setup). Although it can be a bit trickier getting xname installed and working, the real trick is getting legal software (ROMs) and getting them to run properly. (I discuss that a bit later.)

## Supported xname hardware

To control your gaming, xname supports several different types of gaming hardware, including:

- **Joysticks** — Xname supports i386-style joystick driver, the Fm Town Pad, the X11 input extension joystick, and the newer i386 linux 1.x.x joystick driver, if those drivers are compiled into Linux.
- **Mouse** — Common device for moving the pointer on the screen.
- **Trackball** — A ball device, used instead of a mouse particularly on laptop computers, for controlling how the pointer moves on the screen.
- **Game pad** — A pad device (accessible through the `/dev/pad00` device).

For sound, the audio device is defined as `/dev/dsp`. If you want to change any of the game controlling devices or sound device, you can edit the `xnamerc` file in your `$HOME/xname` directory. You can set the system-wide configuration information in `/usr/lib/games/xname/xnamerc`.

To use a gaming device for a particular game, indicate that on the xname command line. To use a joystick, add -joy; to use a mouse, add -mouse; to use a trackball, add -trak; and to use a game pad, add -pad. (The game pad requires the Linux FM-TOWNS game pad driver.)
For example, to add a mouse for a particular game, type:

```
$ xname -mouse game
```
