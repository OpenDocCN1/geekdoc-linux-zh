NEW TERM

Notice that the nroff command is used on the command line instead of groff. This is because the nroff command installed on your system is a shell script, written to use the GNU groff formatting program to emulate the nroff command. All OpenLinux man pages are written using a special set of nroff commands called man macros. You can use the groff command to use man macros to format your own manual pages. For example, if you create a manual page for a new game called nw, the manual page, called nw.6, might look like the following:

```
.TH Nano-Warrior 6 Games 1/1/98 Linux
.SH NAME
nw - play Nano-Warrior
.SH SYNOPSIS
nw
.B -d
.PP
-d = play deathmatch mode
.SH DESCRIPTION
.PP
The nw command is used to play a game of Nano-Warrior on your Linux console. Play continues until you are wiped out by hordes of alien invaders swarming down the screen.
.PP
Don't give up the fight!
.SH FILES
/usr/games/nw
.PP
$HOME/.nw_scores
.SH BUGS
Probably too many.
```

You can process this manual page and send it to your display with the following:

```
# groff -Tascii -man nw.6
```

```
Nano-Warrior(6)               Linux                       Nano-Warrior(6)

NAME

nw - play Nano-Warrior

SYNOPSIS

nw -d
    -d = play deathmatch mode

DESCRIPTION

    The nw command is used to play a game of Nano-Warrior on
your Linux console. Play continues until you are wiped out
by hordes of alien invaders swarming down the screen.

    Don't give up the fight!
```