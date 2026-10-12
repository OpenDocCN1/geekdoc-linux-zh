
# Table 7-2: Games for the KDE Desktop

| Game | Description | Game | Description |
| :--- | :--- | :--- | :--- |
| **Arcade Games** | | | |
| KAsteroids | Destroy asteroids in the classic arcade game. | KBounce | Add walls to block in bouncing balls. |
| KFoul Eggs | Squish eggs in this Tetris-like game. | KSirtet | Tetris clone. Try to fill in lines of blocks as they drop down. |
| KSmileTris | Tetris with smiley faces. | KSnakeRace | Race your snake around a maze. |
| SpaceDuel | Fire at another spaceship as you spin around a planet. | Tron | Snake-style race game. |
| **Boardgames** | | | |
| KBackgammon | Online version of backgammon. | KBattleship | Sink the opponent's battleship in this online version of the board game. |
| KBlackBox | Find hidden balls by shooting rays. | Kenolaba | Move game pieces to push opponents pieces off the board. |
| KMahjongg | Classic oriental tile game. | KReversi | Flip game pieces to outmaneuver the opponent. |
| Shisen-Sho | Tile game similar to Mahjongg. | Kwin4 | Drop colored pieces to get 4-in-a-row. |
| **Cardgames** | | | |
| Patience | Choose from nine different solitaire card games. | KPoker | Video poker clone. Play five-card draw, choosing which cards to hold and which to throw |
| Lieutenant Skat | Play the card game Skat. | | |

| Game | Description | Game | Description |
| :--- | :--- | :--- | :--- |
| **Tactics and Strategy** | | | |
| KJumping Cube | Click squares to increase numbers and take over adjacent squares. | KAtomic | Move pieces to create different chemical compounds. |
| Konquest | Expand your interstellar empire in this multiplayer game. | Kolor Lines | Move marbles to form five-in-a-row and score points. |
| KMines | Minesweeper clone. Click safe spaces and avoid the bombs. | KSokoban | The Japanese warehouse keeper game. |
| KsnameGame | Erase game pieces to score points. | | |

The games on the KDE menu range from diverting to quite challenging. If you are used to playing games in Windows, KMines and Patience will seem like old favorites. KAsteroids and KPoker are good for the mindless game category. For a mental challenge (it's harder than it looks), try KSokoban. For a challenging multiuser game on the Gnome menu, try FreeCiv. For chess enthusiasts, there is Chess (xboard version of gnuchess).

If the games that run in X that come with KDE aren't enough for you, lots of X games are available for download from the Web. For example, the Freshmeat site lists more than 200 games in its application index that you can be downloaded to run in X (go to http://ibiblio.org/pub/Linux/X11/games!INDEX.html).

The following sections describe a couple of the more interesting Red Hat Linux games that run in X. First is the xboard game and some related chess programs. Next is a description of FreeCiv.

### Chess games

Chess was one of the first games played on computer systems. While the game hasn't changed over the years, the way it's played on computers has. The set of chess programs that come with Red Hat Linux lets you play against the computer (in text or graphical modes), has the computer play against itself, or replays stored chess games. You can even play chess against other users on the Internet using Internet Chess Servers (ICS).

The xboard program is an X-based chess game that provides a graphical interface for gnuchess. GNU Chess (represented by the gnuchess package) describes itself as a communal chess program. It has had many contributors, and it seeks to advance a “more open and friendly environment of sharing” among the chess community.

With xboard, you can move graphical pieces with your mouse. To play against the computer, click Programs → Games → Chess from the GNOME menu, then start by just moving a piece with your mouse. While in the xboard window, select Mode → Two Machines to have the computer play itself. Select File → Load Game to load a game in Portable Game Notation (PGN). Figure 7-1 shows the xboard window with a game in progress.

![](img/1744bde8c889adfab3fc911e1687fecf_282_0.png)

Figure 7-1: In the xboard window, you can set xgame to either play against the computer or to replay saved games.

You can use xboard to play online against others, by connecting an xboard session to an Internet Chess Server (ICS). To start xboard as an interface to an ICS, type the following command line:

```
$ xboard -ics name
```

In this example, name is the name of the ICS host. In ICS mode, you can just watch games, play against other users, or replay games that have finished. The ICS host acts as a gathering place for enthusiasts who want to play chess against others on the Internet, watch games, participate in tournaments, or just meet chess people. Here are ICS host computers you can connect to by substituting the name above with the address shown below:

- **Internet Chess Club**: ICC (chessclub.com)
- **Chess.net** (chess.net)
- **Free Internet Chess Server** (freechess.org)

As an alternative to xboard, you can sometimes use Web-based applications to play chess on the Internet. For example, if you were to visit the Chess.net Web site (www.chess.net), you could click the Play Chess link to start. You could then choose the chess software to use. (Chess.net for Java works in Red Hat Linux with Netscape.) After the software downloads, you can sign up for a Chess.net account. After that, the window that appears lets you choose someone to play against or to watch a game in progress.

Chess-related commands that come with Red Hat Linux in the gnuchess package provide different ways of playing chess or manipulating chess output. Here are some examples:

- **game** — A command that takes the output of gnuchess (a chess.lst file) and outputs a PostScript file, board by board. The move and current score are printed with each board.
- **gnuchess** — A simple, curses-based chess game that runs on character terminals or in an xterm window. (The curses interface in UNIX is used for creating and using menus and screen controls in character terminals.)
- **gnuchessn** — A command that is similar to gnuchess, but produces a fancier version (using features such as reverse video).
- **gnuchessr** — A completely ASCII-based version of chess.
- **gnuchessx** — Another ASCII-based chess game that is compatible with xboard.
- **gnuanalyze** — A command that is used to analyze a chess game.
- **zic2xpm** — A command that translates ZIICS chess pieces into xboard pieces. (ZIICS was a popular interface for creating chess pieces that could be displayed in DOS.)

### FreeCiv

With FreeCiv, you create a civilization that challenges competing civilizations for world dominance. The version of FreeCiv that comes with Red Hat Linux contains both client software (to play the game) and server software (to connect players together). You can connect to your server and try the game yourself or (with a network connection) play against up to 14 others on the Internet.

You can start FreeCiv from the Gnome menu (as a non-root user) by clicking on Programs → Games → FreeCiv (either the Isometric, Engels, or Trident tile set). If for some reason FreeCiv doesn't start, try starting it from a Terminal window by typing:

```
$ civ &
```

Figure 7-2 shows the two windows that appear when you start FreeCiv. The Connect to FreeCiv Server window contains your user name, host name, and port number. The FreeCiv window is where you play the game.

![](img/1744bde8c889adfab3fc911e1687fecf_284_0.png)

Figure 7-2: Play Freeciv to build civilizations and to compete against others.

> NOTE: If Freeciv won't start, one reason may be because you are logged in as root. You must be logged in as a regular user to run the civ command. (The root user is prevented from running Freeciv for security reasons.)

### Starting Freeciv

You can go ahead and play a few games by yourself, if you like, to get to know the game before you play against others on the network. The following procedure describes how to start your first practice Freeciv game.

1. Start Freeciv (K → Games → FreeCiv, or type `civ&`).
   The Freeciv windows appear, as shown in Figure 7-2.
2. From a Terminal window, start the Freeciv server by typing:

   ```
   $ civserver
   You can learn a lot about Freeciv at http://www.freeciv.org
   1: Now accepting new client connections.

   Get a list of available commands with 'help'.
   ```

3. Click Connect from the Connect to Freeciv Server window.
4. From the server prompt, type the following:

   ```
   > start
   Starting game.
   1: Loading rulesets
   >
   ```
