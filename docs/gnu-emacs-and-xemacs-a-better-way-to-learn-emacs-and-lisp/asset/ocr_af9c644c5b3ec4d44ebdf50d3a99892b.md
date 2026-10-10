the puzzle encounters as processors increase in speed is that the action happens too quickly for the human eye to follow. In the XEmacs version, the transitions are lightning fast with my midrange processor, an Athlon 700 MHz. The GNU Emacs version incorporates a configurable delay (a 1-second default) that slows down the puzzle enough so you can follow the logic of the gradual solution, move by move. This new version also can use different faces for the odd and even rings as well as the poles. Several settings, including these, can be changed using **Customize**. Press M-x and type

```
customize-group
```

At the minibuffer prompt, type

```
hanoi
```

While in this buffer, you can change the delay time, turn faces on and off, and affect several other variables. Remember to save your changes before you kill the buffer.

The Hanoi mode can be thought of as a demonstration of the mathematical and logical functions available to the Emacs-Lisp programmer.

# Gomoku

Gomoku, shown in Figure 21.5, is an old Oriental board game related to the Japanese game Go. The rules are deceptively simple. Bad game opponent (in this version, Emacs) take turns placing counters on a grid. Whoever manages to construct a horizontal, vertical, or diagonal line made up of five counters wins. It sounds simple, but the play can be tricky, because you have to block your opponent's attempts while trying to extend your own lines.

Start the game by pressing M-x and typing

```
gomoku
```

The screen displays a grid of dots. You are asked if you would like to make the first move.

This game can be addictive. The snide comments left in the minibuffer when the machine wins tend to make you want a rematch.

The keybindings are basic. The arrow keys move you from point to point on the grid, and the spacebar and Enter place your counter. Ctrl-c Ctrl-p begins another game. You can also click the middle mouse button to place your counter.

This is a simple game, quick to play and logically challenging.