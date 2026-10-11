
of the script to point to the directory where the various Briscola files are located. To perform the adjustments as instructed in the README file, just follow these steps:

- Open a Console window and find the Tk shell, called Wish, by typing `locate wish`; press ENTER and then note on a piece of paper the location given.
- Now right-click the *briscola.tk* file itself in the briscola folder, and select **Open With ▶ Text Editor** in the pop-up menu.
- When the briscola.tk file opens within Text Editor, change the very first line from `#!/usr/local/bin/wish` to `#!/usr/bin/wish`, which should have been the location given as the result to your *locate* search in step 1. The `#!` at the beginning of the line, in case you’re wondering, indicates the path to a shell, in this case the Tk shell.
- Now, in the second line, change `/usr/local/games/briscola/` to `/usr/local/share/games/briscola/`, which is where you are going to be placing the briscola folder so that all of the users on your computer can play it.
- Once you have done this, go to the Text Editor **File** menu and select **Save**.
- Quit Text Editor.

## 20B-4: Moving the Briscola Folder to a Global Location

If you’re leaving the briscola folder where it is now (in your Home folder), only you would be able to play the game. To make it available to others who have user accounts on your machine, you need to copy it to a global location. Since global locations are all in root territory, you will first have to become root before you do any copying. Here’s what to do:

- Open a Console window (if one isn’t open already), and become root by typing **su** and pressing ENTER.
- When prompted for your root password, type it in and press ENTER.
- Copy the briscola folder to its new global locations by typing `cp -r briscola /usr/local/share/games`. Then press ENTER.
- Exit root mode by typing **exit** and pressing ENTER.

## 20B-5: Running Briscola

You can now run Briscola (and double-check your work) by doing the following:

- In the Console window, move into the new globally located briscola folder by typing `cd /usr/local/share/games/briscola` and pressing ENTER.
- Now run Briscola by typing `./briscola.tk` and pressing ENTER.

> NOTE In case you were wondering (since there is no *briscola.tk* command), your system doesn’t know what to do with your input. The ./ that you typed in step 2 tells your system to run the script you have signified after the slash (briscola.tk).

## 20B-6: Removing the Briscola Folder Within Your Home Folder

Assuming that Briscola ran without problems from your new global location, you can trash the briscola folder that is still in your Home folder. Of course, you can do this by simply dragging it to Trash, but to get some more command practice, do it via the command Console.

- Quit Briscola.
- In the Console, type **cd** and press ENTER to get the Console back into your Home folder.
- Remove the briscola folder by typing **rm -r briscola** and pressing ENTER.
- Quit the Console by typing **exit** and pressing ENTER.

## 20B-7: Creating a Desktop Shortcut for Briscola

The method of running Briscola that you've just used works well enough, but it can get to be quite a pain in the posterior to open up a Console window and type a couple of commands every time you want to play a few tricks of the game. To make things easier on yourself in the future, it would be a good idea to create a desktop shortcut that you can then simply double-click anytime you want to have a hand at the cards, so to speak.

If you are interested, here's what you need to do:

- Right-click any open space on the desktop, and select **Create New > Shortcut** in the pop-up menu. A Create Shortcut Wizard will then appear.
- In the first page of the wizard, select **Program** and then click **Next**.
- In the text box that appears next to the Browse button in the next page of the wizard, type /usr/local/share/games/briscola/briscola.lk, as shown in Figure 20-7. When finished, click **Next**.
- In the final page of the wizard, change the name of the shortcut to **Briscola**, and then click **Finish**.

You will now have a new shortcut for Briscola on your desktop; however, as the icon is, graphically speaking, rather dull, you might want to change it to something more colorful.

- Right-click the **Briscola** shortcut on the desktop, and select **Properties** in the pop-up menu.
- In the Properties window, click the icon button just below the General tab. This will bring up the Select Icon window.
- In that window, scroll around until you find an icon to your liking—the icon of two playing cards in the *package* section would be an appropriate choice.
- Click once on the icon you've chosen once to select it, and then click **OK**.
- Finally, click **OK** in the Properties window to wrap things up.

![](img/3badae5570de77b990135448f8a8a1cc_443_0.png)

Figure 20-7: Creating a desktop shortcut for Briscola

## Playing Briscola

As I already mentioned, Briscola is about as easy a card game as there is. Briscola is a trick-taking game, which means that you put out a card, and then your opponent puts out a card, and the one who puts out the higher point-value card wins the hand, or *trick*, for which points are awarded on the basis of the cards involved in that trick. The winner of the trick then goes on to *lead* the next trick, meaning that the winner puts out his or her card first the next time around. When all the cards are played, the points for each player are then tallied, and the player with the most points wins. It’s all much simpler to do than it is to describe.

## The Cards and Their Rankings

Like many other Italian and Spanish games, Briscola is played with a 40-card deck, consisting of the following cards: K, Q, J, 7, 6, 5, 4, 3, 2, and the Ace. Traditionally, it is played with either French-suited cards (hearts, diamonds, clubs, and spades) or Italian-suited cards (swords, coins, batons, and chalices), usually dependent upon the region in which it is played. In the software version you have just installed, you will be playing with French-suited cards but with images and patterns in the regional style of Tuscany.

Unlike most card games you are probably familiar with, the ranking and point values of the cards in Briscola are somewhat different, as you can see in the following chart.

| Ranking of Cards | Point Value |
| :--- | :--- |
| Ace | 11 |
| Three | 10 |
| King | 4 |
| Queen | 3 |
| Jack | 2 |
| 7 | 0 |
| 4 | 0 |
| 2 | 0 |

While this ranking arrangement might seem odd, it is actually fairly commonly used in card games from the southern and Catholic regions of central Europe. With that bit of information in mind, it should all be pretty easy enough to fathom, taking a religious view, that God (Ace) and the Holy Trinity (3) rank higher than the divine-rights-endowed royals (K, Q, J) and their decidedly mortal subjects (7, 4, 2). The rankings are thus quite sensible, albeit slightly ironic.

## Game Play in Briscola

Once Briscola starts up, it will deal three cards to each player. It will then take the seventh card and place it face up under the down-facing pile of undealt cards, known as the *stok or talon*. That seventh card is called the *Briscola* (from which the game gets its name), and it determines the trump suit for that particular game. This means that any card of the same suit as the Briscola will beat any card of any other suit, even one of a higher ranking. Of course, when you play a trump card against another trump card, the normal rankings of the cards come back into play.

It is important to note at this point that unlike many other trick-taking games, you are neither required to follow the suit of the card led in a trick in Briscola nor to beat it if you can. This means that if your opponent plays a club card, you can play a card of any suit you like, even if you have a card that can beat it, all depending on your own strategy for ultimately winning the game.

It is a good idea to first go to the **Options** menu before getting started and select **Show Score**. This will allow you to know how you're doing as you play. After you've done that, you are ready for action, and since your computer opponent is always kind enough as to allow you to lead, you can begin by clicking the card you want to put into play. The computer will then play its card (Figure 20-8).

Once you've assessed the situation, click one of the blank spaces in your hand, and the points for that trick will be displayed in the *You box* (if you won the trick) or the *Me box* (if the computer won the trick). Of course, if the trick involved only the 7, 4 or 2 cards, no points will appear, as those cards have no point value.
