
# Summary

In this chapter, you saw the essentials of three different FTP servers. You saw where to get an FTP server and in some cases how to configure and start it. All of these FTP servers are open source and can be found on the Internet and downloaded free of charge. With each of the FTP servers that we actually configured, we did a basic configuration. It would be advisable for you to spend some time studying any FTP server you want to use in more detail. This chapter was meant to get you started with FTP servers. Also, you should note that you should have only one FTP server running at a time. If you have more than one running, they will conflict with each other and neither will work.

## Review Questions

1. What port do FTP servers work on?
2. What does FTP stand for?
3. What is the main configuration file for VSFTP?
4. What is the most commonly used FTP server?
5. What happens to a user who is added to the vsftpdusers file?
6. In vsftp, what does the ftpd_banner setting do?

## Answers

1. Port 21
2. File Transfer Protocol
3. /etc/vsftpd/vsftpd.conf
4. wu-ftp
5. He is blocked from accessing the FTP server.
6. Shows that message to each user when he logs on to your FTP server.

# Chapter 17: Fun and Games in Linux

## Introduction

Throughout this book we have focused on solid, practical Linux features and Linux-related applications. The final section of the book, which follows this chapter, is one of very intense and serious Linux shell manipulation that is certainly not for the faint of heart. Now seems like an appropriate time to relax a bit and find out how we can have some fun with Linux.

It is a fact that many, if not most, PC users spend at least some of their time playing games on their computers. Some users, like the author, spend far too much time playing games! Before you can truly embrace Linux, you will probably want to know what games Linux has for you. The unfortunate fact is that many of the major commercial PC games are not available for Linux. However, the good news is that some are, and Linux ships with several games already installed. In this chapter we will first look at the games Linux comes with, and then we will explore where you can find other games.

When you go to the Start menu, you will find a section for games. This includes a few obvious games like K Poker and KBackgammon. These are simply KDE versions of Poker and Backgammon. If you know how to play the traditional versions of those games, you should have no problem with the Linux versions. We want to explore a few games that might not be so obvious, but that can be quite fun!

## Kolf

What would the world of PCs be without computerized golf? Even people who don’t enjoy playing real golf on a golf course can find playing computer golf a relaxing diversion. The KDE interface has such a game, called Kolf, and its main screen is shown in Figure 17.1.

![](img/12d790664598bbf390261087fbe55bbc_353_0.png)

To start a new game, select the Game menu and choose New Game. You will see the screen that is shown in Figure 17.2. Here is where you set up your new game. Obviously you have to pick your players’ names, but there is a lot more here for you to do.

![](img/12d790664598bbf390261087fbe55bbc_353_1.png)

On the Course tab of this screen, shown in Figure 17.3, you can set up the parameters of your course. You can select the type of course, create a new course, and set the par for that course. For our example we will choose the Really Easy course.

![](img/12d790664598bbf390261087fbe55bbc_354_0.png)

**Figure 17.3:** Setting up a course.

You are then taken to the game screen. Here you move your mouse to where you want your club and press the mouse button. The longer you hold down the mouse button, the more power will be in your swing. This is shown in Figure 17.4. When you let go, you will swing and hit the ball. You can use the arrow keys at the top of the screen to move on to the next hole if you wish to skip the current hole. Kolf probably won't improve your real golf score, but it could certainly be a fun way to spend a little time.

![](img/12d790664598bbf390261087fbe55bbc_354_1.png)

**Figure 17.4:** Swinging at the golf ball.

## KBattleship

This is a fun one for you military simulation lovers. The KBattleship game, shown in **Figure 17.5**, allows you to battle it out in a naval campaign. In this game, one player is the server, the other player connects to that server, and you match wits on the simulated high seas.

![](img/12d790664598bbf390261087fbe55bbc_355_0.png)

**Figure 17.5**: KBattleship.

When you choose the Game menu, shown in **Figure 17.6**, you have the option to make your game the server or to connect to another server. To connect to another server, you must both be on some sort of network or connected via the Internet.

![](img/12d790664598bbf390261087fbe55bbc_355_1.png)

**Figure 17.6**: The Game menu.

When you first choose to start your machine as the server, you will be asked to provide a nickname for yourself in the game and to pick a port for the other player to connect to. This is shown in **Figure 17.7**. The other player connects to the server. He also must pick a nickname and then enter the IP address and port number of your machine.

![](img/12d790664598bbf390261087fbe55bbc_356_0.png)

**Figure 17.7**: Starting your PC as a game server.

Under the Help menu, you will also find documentation and further help and hints regarding the KBattleship game.

## KAsteroids

This one is an oldy but a goody. Asteroids was a very popular arcade game in the early 1980s. KAsteroids is a Linux version of this game. You can see the KAsteroids screen in Figure 17.8. The goal of KAsteroids is to use your spaceship to destroy asteroids and not get smashed by any asteroids. The KAsteroids game actually has much more realistic asteroids than did the original game.

![](img/12d790664598bbf390261087fbe55bbc_357_0.png)

**Figure 17.8:** KAsteroids.

The game itself is very simple. You use the L key to launch the game, then you maneuver your ship using the arrow keys. You fire at asteroids with the spacebar. Destroy as many asteroids as you can without getting smashed by one yourself. Figure 17.9 shows KAsteroids in action. This game may not prepare you for NASA, but it can be a lot of fun.

![](img/12d790664598bbf390261087fbe55bbc_358_0.png)

**Figure 17.9:** Playing KAsteroids.

## KMines

This game is essentially a replica of the ever-popular Microsoft Minesweeper® game. The board, shown in **Figure 17.10**, even looks much the same. You try to guess where flags are while not picking a square with a mine. This game will make you feel like you were back on a Windows machine.

![](img/12d790664598bbf390261087fbe55bbc_359_0.png)

**Figure 17.10**: KMines.

## KWin4

A very popular game among children and therefore parents of children is Connect Four®. If you happen to be a fan of this particular game, you will be pleased to know that an analog of it exists in the world of Linux. This game is KWin4, shown in Figure 17.11. This game works exactly like the traditional game. The idea is to connect four of your pieces in a row before your opponent does. In this case, your opponent is the computer.

![](img/12d790664598bbf390261087fbe55bbc_360_0.png)

This game also can be played over the Internet or a network connection with another person as your opponent. To set this up, go to the File menu and select Network Configuration. You will be taken to the screen shown in Figure 17.12. Here you can set up yourself as the game server or connect to someone else's server.

![](img/12d790664598bbf390261087fbe55bbc_361_0.png)

**Figure 17.12:** Network configuration.

There are several other interesting games that ship with Red Hat Linux. For example, there is the KSpaceDuel, shown in **Figure 17.13**, and chess, shown in Figure 17.14. The important thing to keep in mind is that there are a lot of games available for Linux. While some commercial hits might not be available for Linux, you should keep in mind that Red Hat Linux installs with far more games than any version of Windows.

![](img/12d790664598bbf390261087fbe55bbc_361_1.png)

**Figure 17.13:** KSpaceDuel.
