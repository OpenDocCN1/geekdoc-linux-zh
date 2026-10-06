# 286 Part II: Using Fedora and RHEL

| Game | Description |
| --- | --- |
| KMines | Minesweeper clone. Click safe spaces and avoid the bombs. |
| Kolor Lines | Move marbles to form five-in-a-row and score points. |
| Konquest | Expand your interstellar empire in this multiplayer game. |
| Potato Guy | Build your own potatohead face. |
| SameGame | Erase game to score points.

The games on the KDE menu range from diverting to quite challenging. If you are used to playing games in Windows, KMines and Patience will seem like old favorites. KAsteroids and KPoker are good for the mindless game category.

# Adding more games from Fedora repository

As Fedora continued its role as a proving ground for the Red Hat Enterprise Linux products, some-just-for software packages were pushed out of what was called Core. Luckily, many of them were pushed into Fedora Extras. With the merging of Fedora Extras and Core, all games are now back in the main repository.

Because the Fedora Games SIG is an on-going initiative, you can check the Fedora Project Web site to see if there are more games than shown in Table 7-3 available in Fedora by opening the PackageKit and selecting games.

You can install each game from the Fedora DVD included with this book. Most, but not all, of the games available in the Fedora repository are included on the DVD. To check packages that have been added later, type yum groupinfo games. To install a version of the game from the Fedora repository, use the following type, replacing game with the name of one of the games listed in Table 7-3:

```
# yum install game
```

Table 7-3 contains a sample from the growing list of games available from the Fedora repository. There are now over 200 games packages in Fedora. Except where noted, all games in Table 7-3 can be launched from the Games list on the Applications menu.

# Table 7-3: Games in Fedora

| Game | Description |
| --- | --- |
| Abe (abe) | Scrolling, platform-jumping, ancient pyramid exploring game. |
| Beneath a Steel Sky (beneath-a-sky) | A popular commercial science fiction adventure game from the early 1990s, in a repressive, futuristic city. |
| BSD Games (bsd-games) | Text-based card games and adventure games dating back to early UNIX systems of the 1970s. (Run from the shell.) |
| BZFlag (bzflag) | 3D multi-player tank battle game.