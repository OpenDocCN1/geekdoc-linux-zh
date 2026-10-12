You can use xboard to play online against others by connecting an xboard session to an Internet Chess Server (ICS). To start xboard as an interface to an ICS, type the following command line:

```
$ xboard -ics -ichost name
```

In this example, name should be replaced by the name of the ICS host (see the list of hosts below). In ICS mode, you can just watch games, play against other users, or replay games that have finished. The ICS host acts as a gathering place for enthusiasts who want to play chess against others on the Internet, watch games, participate in tournaments, or just meet chess people. Here is an example of starting an ICS session at chess.net from a Terminal window:

```
$ xboard -ics -ichost chess.net
Please wait.
Press return to enter chess.net as "guest 141":
chess$ <Enter>
```

After pressing Enter, you are logged into the chess server as a guest. The xboard window opens on your screen. Keep an eye on the Terminal window where you started the session. Someone will probably challenge you to a game within a few moments. For example, if a challenge ended with “Type /accept 102’ to accept the sought challenge.” you would type:

```
chess$ /accept 102
```

You can begin playing. To learn more about how to play, visit http://chess.net/help. Select the Beginners Manual to start. Other chess servers you can try include the Internet Chess Club (ICC) at thechessclub.com or Free Internet Chess Server at freechess.org.

# Freeciv

With Freeciv, you create a civilization that challenges competing civilizations for world dominance. Freeciv is a free clone of the popular Civilization game series from Atari. A commercial port of Civilization Call to Power to Linux was created a few years ago by Loki Games (described later in this chapter).

The version of Freeciv that comes with Fedora contains both client software (to play the game) and server software (to connect players together). You can connect to your server and try the game yourself or (with a network connection) play against up to 14 other players on the Internet.

You can start Freeciv from the Red Hat menu (as a non-root user) by clicking Games → Freeciv (isometric tile set). If Freeciv doesn’t start, try starting it from a Terminal window by typing:

```
$ civ s
```